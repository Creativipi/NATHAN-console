# ADR-0006 — IDE accessible à assistance vocale (TTS/STT + IA)

- **Statut :** Accepté *(orientation ; le **stack** technique sera tranché à `TECH-19` → futur ADR)*
- **Date de la décision :** 2026-06-07
- **Décideurs :** ENG
- **Contexte projet :** outil de création de mini-jeux pour personnes non-voyantes
- **Liens :** [[specs/REQUIS]] (accessibilité), [[planning/TACHES]] Bloc 6 (`TECH-19`, `TECH-20`, `IDE-01`…`IDE-04`, `S7-T14`, `S8-T08`), [[0005-micropython-mini-jeux-usb-cdc]]

## Contexte et problème

L'IDE doit permettre à une **personne non-voyante** d'écrire et de charger des mini-jeux MicroPython (ADR-0005). L'**accessibilité est le critère #1**, pas une option ajoutée après coup.

## Options envisagées

- **A — IDE visuel classique + lecteur d'écran tiers.** *Contre :* expérience d'édition de code pauvre et frustrante pour une personne DV.
- **B — IDE conçu accessible d'emblée (retenue) :** TTS, ARIA, navigation clavier complète, **plus** assistance vocale (STT pour la saisie, TTS pour le retour) et **fonctionnalités d'IA** (assistance au code).

## Décision

Concevoir un **IDE accessible-first** avec **TTS/STT + IA**. Le démarrage est planifié en **S7** (pas de dépendance matérielle avant l'intégration USB). Le **choix du stack** (Electron/React, Tauri, …) reste à trancher (`TECH-19`).

## Conséquences

- **+** Réellement utilisable par une personne DV ; différenciateur fort du projet.
- **−** Dépendance à des **services d'IA** (coûts à estimer, `IDE-03`) ; arbitrage **backend/frontend** à lever (`IDE-04`) ; accessibilité = effort soutenu (`S7-T14`, `S8-T08`).

## Suivi / quand re-questionner

Produire un ADR « stack IDE » à la décision `TECH-19`. Réévaluer le recours à l'IA cloud selon les coûts (`IDE-03`) et la confidentialité.
