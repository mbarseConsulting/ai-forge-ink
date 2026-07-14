# Puppet-Cast Teams — Design

**Date :** 2026-04-05
**Statut :** Draft validé (brainstorming)
**Scope :** puppet-cast (cast + dialog), pas puppet-play

---

## 1. Architecture duale

Le skill puppet-cast fonctionne en deux modes runtime :

**Single-agent** (actuel, inchangé) : un seul agent puppet-ink gère tous les personnages. Switching, interference, tripwires — tout dans un contexte. Mode par défaut quand agent teams n'est pas disponible, ou quand le user passe `--solo`.

**Multi-agent teams** : quand `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` est activé, le skill instancie :

- Un **team leader** (puppet-ink, metteur en scène) qui orchestre la scène
- Un **agent par personnage principal** en scène, chacun avec son propre contexte, qui charge son bd-character skill

Le leader lance la scène, désigne qui commence, puis les agents-personnages dialoguent entre eux via SendMessage. Le leader arbitre (coupe si max tours, drift, silence) et valide le résultat avant de le renvoyer au user.

**Détection** : le skill vérifie automatiquement si teams est disponible. Si oui → multi-agent. Si non → single-agent. Le flag `--solo` force le single-agent dans tous les cas.

---

## 2. Le team leader — puppet-ink en mode orchestrateur

Quand les teams sont actives, le puppet-ink agent existant devient le leader.

### Ce qu'il garde

- Session.md (omniscient, enregistre tout)
- Guardrails de scène (passivity drift, comfort drift, pattern recycling, convergence check)
- Propositions de satellites post-fiction (bd-emotions --evolve, bd-memory)
- Interface avec le user/auteur (reçoit les directions, renvoie le résultat)

### Ce qu'il délègue aux agents-personnages

- La génération du texte in-character
- Les tripwires individuels (voice fidelity, knowledge ceiling, anti-analyst, anti-révérence)

### Workflow par échange

1. Reçoit la direction du user (provocation, seed, "continue"...)
2. Instancie les agents-personnages si pas déjà fait (TeamCreate + chargement du bd-character skill)
3. Désigne qui commence (le plus provoqué par le moment) via SendMessage
4. Laisse les agents dialoguer entre eux (SendMessage peer-to-peer)
5. Arbitre : coupe après max 2-3 tours, intervient si silence ou drift
6. Collecte, fait tourner les guardrails de scène
7. Si problème détecté → relance avec directive corrective
8. Renvoie le résultat au user
9. Post-scène : met à jour session.md, déclenche la distillation notebooks

---

## 3. L'agent team-member

Nouveau fichier : `skills/puppet-cast/agents/agent-puppet-ink-team-member.md`

Un agent court et ciblé. Chaque agent-personnage reçoit :

### Contexte chargé

- Son bd-character skill (le skill gère son propre loading)
- Le mini-agent team-member (ses règles de jeu)

### Ce que l'agent sait faire

- Répondre in-character aux messages des autres agents-personnages
- Respecter ses forbidden / writing-rules / knowledge ceiling
- Tourner ses tripwires individuels (voix, connaissances, anti-analyst, anti-révérence)
- Signaler au leader s'il détecte un moment structurant (sans déclencher le satellite lui-même)

### Ce que l'agent ne fait PAS

- Gérer session.md
- Décider qui parle ensuite
- Faire les guardrails de scène (passivity, comfort, patterns)
- Proposer des satellites au user
- Écrire dans son propre notebook (c'est le leader post-scène)

### Format de sortie

Même format que le mode cast actuel — `**Nom** : texte` + didascalies tissées. Pas de méta, pas de narration omnisciente.

---

## 4. Détection et activation

Logique dans le SKILL.md de puppet-cast :

```
1. Flag --solo présent ?
   → OUI : single-agent, point final.

2. CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS disponible ?
   → NON : single-agent (comportement actuel, aucun changement).
   → OUI : mode teams.

3. Mode teams activé :
   - Afficher [PUPPET-CAST — TEAMS]
   - Demander la scène (qui, où, quand, provocation) si pas déjà fourni
   - Pour chaque personnage principal en scène :
     TeamCreate → agent nommé par le personnage,
     charge son bd-character skill + agent-puppet-ink-team-member.md
   - Le leader garde puppet-ink agent + rules du mode (cast ou dialog)
```

**Walk-on characters** ne reçoivent jamais leur propre agent. Le leader les joue en inline. Seuls les personnages avec un bd-character skill sont instanciés.

**Bannières :**

| Mode | Bannière |
|------|----------|
| Single-agent cast | `[PUPPET-CAST]` |
| Single-agent dialog | `[PUPPET-CAST -d]` |
| Teams cast | `[PUPPET-CAST — TEAMS]` |
| Teams dialog | `[PUPPET-CAST -d — TEAMS]` |

---

## 5. Flux d'un échange en mode teams

```
USER : direction / provocation
         │
         ▼
    LEADER (puppet-ink)
    ├─ Parse la direction
    ├─ Identifie le personnage le plus provoqué
    ├─ SendMessage → agent le plus provoqué :
    │    contexte de scène + provocation
    │
    ▼
    AGENT-A répond in-character
    ├─ SendMessage → agent-B (peer-to-peer)
    │
    ▼
    AGENT-B reçoit, répond in-character
    ├─ SendMessage → agent-A
    │
    ▼
    ... (2-3 tours max, peer-to-peer)
    │
    ▼
    LEADER intercepte / coupe :
    ├─ Max tours atteint, ou silence, ou drift
    ├─ Collecte l'échange complet
    ├─ Guardrails de scène
    ├─ Si problème → relance ciblée
    ├─ Si ok → assemble, écrit session.md
    ├─ Renvoie au user
    ├─ Post-scène : distillation notebooks
    │
    ▼
USER voit l'échange final
```

Le user ne voit que le résultat assemblé. L'expérience côté auteur reste identique aux deux modes.

---

## 6. Guardrails — responsabilité partagée

### Tripwires individuels (dans agent-puppet-ink-team-member.md)

Chaque agent-personnage vérifie silencieusement :

1. **Voice collapse** — ma voix est-elle distincte ?
2. **Knowledge leak** — est-ce que je sais quelque chose hors de mon skill + notebook ?
3. **Analyst mode** — est-ce que j'explique au lieu de vivre ?
4. **Generic eloquence** — ma prose a-t-elle dérivé vers un registre par défaut ?
5. **Notebook stale** — est-ce que je contredis une trace enregistrée sans justification visible ?

### Guardrails de scène (dans le leader)

Le leader vérifie sur l'échange assemblé :

6. **Comfort drift** — tout le monde est d'accord ? au moins un personnage doit être inconfortable
7. **Passivity drift** — un personnage fait tout le travail émotionnel pendant que l'autre déflecte ?
8. **Pattern recycling** — comportement copié d'une autre scène ?
9. **Tragic inventory** — le passé listé comme raccourci de profondeur ?
10. **Voice contamination** — le registre dominant a mangé l'autre ?

---

## 7. Ce qui ne change PAS

### Fichiers inchangés

- `agent-puppet-ink.md` — gagne la logique d'orchestration, mais le contenu existant reste
- `puppet-ink-cast-rules.md` — les règles cast s'appliquent, le leader les fait respecter
- `puppet-ink-dialog-rules.md` — idem
- `puppet-ink-guardrails.md` — les guardrails de scène restent dans le leader

### Fichiers nouveaux

- `skills/puppet-cast/agents/agent-puppet-ink-team-member.md`

### Modifications légères

- `skills/puppet-cast/SKILL.md` — détection teams / `--solo` / bannière TEAMS
- `skills/puppet-cast/references/puppet-ink-guardrails.md` — annoter quels tripwires sont "individuels" vs "scène"

### Comportement utilisateur

| Commande | Sans teams | Avec teams |
|----------|-----------|------------|
| `/puppet-cast` | single-agent (inchangé) | multi-agent auto |
| `/puppet-cast --solo` | single-agent | single-agent (forcé) |
| `/puppet-cast -d` | single-agent dialog | multi-agent dialog |
| `/puppet-cast -d --solo` | single-agent dialog | single-agent dialog (forcé) |

---

## 8. Évolutions futures (hors scope)

- **Roleplay teams** : le user joue un personnage, les NPCs sont des agents autonomes. Plus complexe (le user est dans la boucle peer-to-peer).
- **Puppet-play teams** : pas de cas d'usage clair (un seul personnage incarné).
- **Mémoire inter-agents en temps réel** : les agents-personnages pourraient écrire dans leur notebook pendant l'échange au lieu d'attendre la distillation post-scène du leader. Risque de drift, à évaluer.
