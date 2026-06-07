# ADR-0001 — Architecture PC-first et contrats d'interface

- **Statut :** Accepté
- **Date de la décision :** 2026-05-15 (gel des interfaces) · **Consigné :** 2026-06-07 (rétroactif)
- **Décideurs :** ENG, AUD, ELEC
- **Contexte projet :** S6, jalon « interfaces gelées »
- **Liens :** C-05 (engine agnostique du matériel), C-06 (PC-first), R-31, [[planning/TACHES]] Bloc 0 (`TECH-01`, `TECH-02`), [[0003-choix-mcu-benchmark-driven]], [[0004-option-repli-audio-fpga]]

## Contexte et problème

La console est embarquée mais **le microcontrôleur n'est pas encore choisi** (voir ADR-0003). L'équipe est pluridisciplinaire (logiciel / audio / électronique) et doit avancer **en parallèle**. Si le jeu et le moteur sont couplés directement au matériel, **rien ne peut progresser avant le choix du MCU** — ce qui bloquerait tout le projet et empêcherait de tester tôt.

## Options envisagées

- **A — Développer directement sur le MCU** choisi tôt. *Contre :* bloque tout jusqu'au choix MCU, difficile à tester, décision matérielle prématurée et risquée.
- **B — Architecture en contrats d'interface (retenue) :** définir 5 contrats (Input, SpatialAudio, Haptic, Storage, MiniGame), avec des implémentations **PC d'abord**, **embarquées ensuite** (simple *swap* d'implémentation). *Pour :* développement parallèle, tests sur PC, choix MCU différé au benchmark. *Contre :* discipline de gel des interfaces requise.

## Décision

Adopter l'architecture **PC-first** : 5 contrats d'interface gelés en début de S6 (`TECH-02`). **Le game engine ne sait jamais s'il parle à une manette Xbox ou à la manette NATHAN.** Phase PC (S6-S7) → swap embarqué (S8).

## Conséquences

- **+** Développement parallèle sur tous les blocs ; stratégie benchmark-driven possible (ADR-0003) ; absorbe les implémentations de repli (`EmbeddedAudio`, et `HardwareAudio` FPGA — ADR-0004) sans refonte.
- **−** Tout changement d'interface après le gel exige l'accord des 2 équipes ; léger surcoût d'abstraction.

## Suivi / quand re-questionner

Si une interface se révèle inadaptée au portage embarqué (S7-S8), ouvrir un nouvel ADR la remplaçant plutôt que de modifier celui-ci.
