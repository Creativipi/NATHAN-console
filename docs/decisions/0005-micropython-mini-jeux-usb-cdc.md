# ADR-0005 — MicroPython pour les mini-jeux + transfert USB CDC

- **Statut :** Accepté
- **Date de la décision :** fondatrice du projet · **Consigné :** 2026-06-07 (rétroactif)
- **Décideurs :** ENG
- **Contexte projet :** modèle de programmation de la console
- **Liens :** [[specs/CAHIER-DES-CHARGES]], [[planning/TACHES]] (`S7-T11`, `S7-T12`, `S7-T15`, `S7-T16`), [[0006-ide-accessible-assistance-vocale]]

## Contexte et problème

La console doit permettre à la **communauté** — et à Nathan lui-même — de **créer et charger des mini-jeux facilement**, dans une optique d'accessibilité et d'open-source. Le modèle de programmation conditionne le firmware, l'IDE et le protocole de transfert.

## Options envisagées

- **A — Mini-jeux compilés en C/C++** flashés dans le firmware. *Contre :* cycle de développement lent, inaccessible aux non-experts, pas de chargement dynamique de jeux.
- **B — Interpréteur MicroPython embarqué (retenue) :** mini-jeux en `.py` chargés dynamiquement via **USB CDC** depuis l'IDE. *Pour :* itération rapide, accessible aux débutants, chargement sans reflash.

## Décision

Embarquer **MicroPython** pour les mini-jeux ; définir un **protocole USB CDC** (LIST / UPLOAD / DELETE / LOG) pour le transfert IDE ↔ console.

## Conséquences

- **+** Accessibilité et itération rapide ; chargement dynamique ; cohérent avec l'IDE (ADR-0006).
- **−** Coût RAM/CPU de l'interpréteur → **à intégrer au dimensionnement MCU** (ADR-0003) ; nécessite un gestionnaire de mini-jeux côté IDE (`S7-T16`).

## Suivi / quand re-questionner

Si le benchmark montre que MicroPython + HRTF ne tiennent pas ensemble sur le MCU retenu, réévaluer (sous-ensemble MicroPython, ou bytecode précompilé) via un nouvel ADR.
