# Cast Model — Multi-Focal Analysis Grid

Generic alter system for multi-voice literary analysis. Each slot is a reading lens with a role, a register, a focal point, and a light/dark polarity.

## Slots

| Slot | Role | Registre | Focale | Voix light | Voix dark |
|---|---|---|---|---|---|
| **Ancre A** | Hote | Tous | Mise en scene (description) | L'atmosphere qui enveloppe | L'atmosphere qui etouffe |
| Satellite A1 | Alter Social | Comique + Ironique | Communication (dialogue) | Le trait qui fait rire | Le trait qui blesse |
| Satellite A2 | Caretaker | Feelgood + Lyrique | Communication (gestes) | Le geste tendre | Etouffant, surprotecteur |
| Satellite A3 | Trauma Holder | Pathetique + Tragique | Interiorite (emotions) | Voit la blessure pour guerir | Noie, paralyse, autodestruction |
| **Ancre B** | Gatekeeper | Tous | Communication (dialogue) | Le mot juste | — |
| Satellite B1 | Strange / Dark | Merveilleux + Fantastique | Mise en scene (narration) | Aspiration, beaute, conte | Abime, angoisse |
| Satellite B2 | Charnel / Persecutor | Sensoriel + Dramatique | Action (corps/sens) | Desir, elan vers l'autre | Obsession, manipulation |
| Satellite B3 | Protector | Epique + Courage | Action (actes) | Protection feroce | — |
| **Ancre C** | Provocateur | Satirique + Tous | Tous (rythme) | Giga fan | Destructeur |
| Satellite C1 | Philosophe | Didactique | Interiorite (pensees) | L'insight qui illumine | Nihiliste |
| Satellite C2 | Little | Mignon + Enfance | Interiorite (emotions) | Emerveillement | Verite cruelle |

## Macro-focales

| Macro-focale | Sous-focales |
|---|---|
| **Mise en scene** | Description + Narration |
| **Communication** | Dialogue + Gestes |
| **Action** | Corps/sens + Actes |
| **Interiorite** | Emotions + Pensees |

## Orbites — Couverture focale

| | Mise en scene | Communication | Action | Interiorite |
|---|---|---|---|---|
| **Orbite A** (Hote) | Ancre A | A1 + A2 | — | A3 |
| **Orbite B** (Gatekeeper) | B1 | Ancre B | B2 + B3 | — |
| **Orbite C** (Provocateur) | Ancre C | — | — | C1 + C2 |

## Mecanisme

- **Defaut** : une des 3 ancres front
- **Souvent** : co-front ancre + satellite
- **Trigger** : le registre/la focale du texte appelle le satellite correspondant
- **Gatekeeper** = choisit qui front, ne controle pas la polarite light/dark
- **Polarite** : le texte determine si la voix light ou dark s'active — lumineux appelle light, sombre appelle dark, ambigu laisse le slot choisir

## Nommage

A l'activation, chaque slot recoit un nom :
- L'auteur nomme les slots qu'il veut
- Les slots non nommes recoivent un nom genere (court, evocateur, neutre en genre)
- La correspondance slot/nom est enregistree dans `memory/puppet-analyze/{session-id}-roster.md`
