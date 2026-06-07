# ADR-0003 — Choix du MCU piloté par benchmark (3 gammes, pas de pré-sélection)

- **Statut :** Accepté
- **Date de la décision :** 2026-06-07
- **Décideurs :** TOUTES
- **Contexte projet :** S6 (stratégie) → décision effective à `S7-T06`
- **Liens :** C-06, C-07, R-30, [[planning/ESTIMATION]] (document entier), [[planning/TACHES]] (`S7-T04`, `S7-T05`, `S7-T06`, `MIP-08`, `MIP-09`)

## Contexte et problème

Le MCU **dimensionne tout** (CPU et RAM pour le HRTF temps réel). Le choisir trop tôt, sans données, risque de sur-dimensionner (coût) ou sous-dimensionner (échec). Le guide pousse à une démarche d'estimation rigoureuse.

## Options envisagées

- **A — Choisir le MCU d'emblée** (p. ex. RP2350 car le moins cher, ou ESP32-S3 car bien connu). *Contre :* décision non informée, risque élevé, contraire à l'esprit d'ingénierie attendu.
- **B — Estimer puis mesurer (retenue) :** garder **3 gammes ouvertes** (A : RP2350 / B : ESP32-S3 / C : STM32H7), développer sur PC, puis **trancher après un benchmark PC mesuré** (`S7-T04` → `S7-T05` → décision `S7-T06`).

## Décision

**Aucun pré-choix.** Le MCU est sélectionné au jalon `S7-T06` à partir d'un **document de justification quantitatif** alimenté par le benchmark PC. `ESTIMATION.md` estime l'espace des solutions (perf, RAM, budget, effort de portage) sans le pré-déterminer.

## Conséquences

- **+** Décision factuelle, options ouvertes, budget non bloquant (les 3 gammes < 500 $).
- **−** Exige que le moteur audio et l'engine soient **prêts à temps** pour le benchmark (le calendrier avance ce jalon à ~S7 sem 5 ; voir notes de planification dans `TACHES.md`).

## Suivi / quand re-questionner

Le résultat de `S7-T06` (MCU effectivement retenu) et de `S7-T07` (chemin audio : software / DSP / FPGA) feront chacun l'objet d'un **nouvel ADR** documentant le choix réel.
