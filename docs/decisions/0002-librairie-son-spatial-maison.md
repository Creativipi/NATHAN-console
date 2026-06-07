# ADR-0002 — Développer notre propre librairie de son spatial (HRTF maison)

- **Statut :** Accepté
- **Date de la décision :** 2026-06-07
- **Décideurs :** AUD, ENG
- **Contexte projet :** S6, cœur du produit
- **Liens :** R-14, R-23, C-08, [[specs/HYPOTHESES]] (H-07), [[planning/ESTIMATION]] §2, [[planning/TACHES]] Bloc 2 (`TECH-13`, `TECH-14`, `AU-03`, `S7-T01`, `S8-T02`), [[0004-option-repli-audio-fpga]]

## Contexte et problème

Le cœur du produit est le **rendu binaural HRTF temps réel**. La cible finale est embarquée (MCU), avec une possible décharge matérielle (ADR-0004). Il faut un moteur audio **portable et maîtrisé**.

## Options envisagées

- **A — Bibliothèque de spatialisation tierce** (Steam Audio, OpenAL HRTF, etc.). *Pour :* rapide à démarrer. *Contre :* boîte noire, portage embarqué difficile voire impossible, **non gravable en logique** (interdit l'option FPGA), contraintes de licence pour un projet open-source.
- **B — Notre propre moteur de convolution HRTF (retenue).** *Pour :* contrôle total, portable sur MCU, **condition nécessaire à l'option FPGA** (on ne grave en logique qu'un algorithme que l'on maîtrise), 100 % open-source. *Contre :* plus d'effort et de risque.

## Décision

Développer **notre propre librairie de son spatial**. Les bibliothèques existantes servent uniquement à l'**I/O audio** (playback, ex. miniaudio) et comme **référence de benchmark** — jamais comme moteur de spatialisation final.

## Conséquences

- **+** Portabilité, contrôle, propriété intellectuelle, « FPGA-ready » (ADR-0004), open-source.
- **−** Effort supérieur (flux audio ~560 h) ; risque de performance couvert par les replis de `H-07` (filtres plus courts, moins de sources, DSP, stéréo, FPGA).

## Suivi / quand re-questionner

Si le benchmark PC (`S7-T04`) révèle que même optimisé le moteur maison ne tient pas sur le MCU le plus performant abordable → activer la décharge matérielle (ADR-0004) plutôt que de revenir à une lib tierce.
