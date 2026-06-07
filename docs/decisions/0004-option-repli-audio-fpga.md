# ADR-0004 — Garder une option de repli audio matérielle (FPGA/CPLD)

- **Statut :** Accepté *(option conservée ouverte ; son **activation** est conditionnelle et sera tranchée à `S7-T07`)*
- **Date de la décision :** 2026-06-07
- **Décideurs :** AUD, ELEC
- **Contexte projet :** repli ultime de l'hypothèse H-07
- **Liens :** [[specs/HYPOTHESES]] (H-07), R-14, R-15, E5 (latence < 20 ms), [[planning/ESTIMATION]] §2.6/§4.2, [[planning/TACHES]] Bloc 2b (`AUDHW-01`…`AUDHW-06`), `S7-T07`, [[0002-librairie-son-spatial-maison]]
- **Source :** ancien `OPTION-AUDIO-MATERIELLE.md` (fusionné ici)

## Contexte et problème

Si le benchmark (`S7-T04`/`S7-T05`) montre qu'**aucun MCU abordable** ne calcule le HRTF temps réel voulu (assez de sources, filtres assez longs, latence assez basse), le projet ne doit pas être bloqué. Il faut un **repli**.

Le son spatial = **convolution par filtres FIR** (les HRIR du dataset HRTF). On peut **déporter ce calcul hors du MCU** dans un circuit dédié.

## Options pour réaliser le « banc de filtres »

| Option | Description | Verdict |
|--------|-------------|---------|
| **MCU en logiciel** | Le MCU calcule les filtres (défaut, ADR-0003) | Chemin par défaut |
| **DSP audio tout-fait** (ADAU1701 / SigmaDSP…) | Puce à moteur de filtres **programmable mais figé** | Possible mais peu « maison », taps limités — déconseillé |
| **FPGA / CPLD** *(retenu comme repli)* | **Notre** banc de filtres FIR gravé en **logique programmable** (calcul parallèle) ; le MCU ne fait plus que *streamer* | **Repli retenu** |
| **Circuit analogique / discret** de filtres fixes | Composants passifs/actifs figés | **NON viable** (voir ci-dessous) |
| ASIC (puce sur mesure) | — | Hors budget / hors délai |

### Réponse à « ne pourrait-on pas un simple circuit de filtres ? »

Oui, l'intuition est juste : **le HRTF EST un banc de filtres**. Mais il doit être **numérique et reprogrammable**, pas analogique/discret, parce que les filtres :
1. sont **longs** (128 à 512 coefficients par oreille),
2. **changent en temps réel** selon la position de **chaque source** qui bouge autour de la tête (187+ positions HRTF, interpolées),
3. tournent pour **plusieurs sources simultanées**.

Un circuit analogique à composants fixes **ne peut pas recharger dynamiquement des centaines de coefficients par source mobile**. Le **FPGA/CPLD est exactement ce « circuit de filtres », mais programmable en logique numérique** — il réalise l'idée tout en restant dynamique.

### « Le FPGA, seulement pour tester ? »

**Non.** Si l'option est activée, le FPGA est **dans le produit final** : on **prototype** sur une carte devkit (~40 $ CA), puis on **produit** avec la **puce nue (~7-10 $ CA)**. Ce n'est pas un banc d'essai — c'est une **architecture de production conditionnelle**.

## Décision

**Conserver l'option FPGA/CPLD** comme repli de production, **à activer seulement si** le benchmark le justifie (décision à `S7-T07`, élargie à « software pur / DSP externe / FPGA-CPLD maison »). Toolchain **open-source** (yosys/nextpnr, C-25). C'est une **3ᵉ implémentation du contrat `SpatialAudioEngine`** (`HardwareAudio`), à côté de `PCAudio` et `EmbeddedAudio` — absorbée par l'architecture (ADR-0001).

## Conséquences

- **+** Découple la performance audio de la puissance du MCU (qualité élevée **même avec le MCU économique**) ; reste 100 % maîtrisé et open-source.
- **−** Si activé : **~+330 h** (surtout conception HDL), **remplace `S8-T02`**, **contraint le schéma/layout PCB** (le FPGA doit y être prévu), et ajoute une **interface MCU→FPGA à geler**.

## Suivi / quand re-questionner

Réévaluer à `S7-T07` (après benchmark). Si activée, produire un ADR « chemin audio retenu » documentant le choix définitif et l'impact PCB.
