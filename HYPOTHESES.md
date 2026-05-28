# Hypothèses de Travail — Projet NATHAN Console v2.0

**Date :** 2026-05-27
**Session :** PMC660 (S6, E2026)

> Les hypothèses de travail sont des **suppositions acceptées comme vraies** pour la planification,
> mais qui **pourraient s'avérer fausses** et nécessiter un ajustement.
> Chaque hypothèse est suivie en continu : si elle est invalidée, le plan de contingence s'active.
> Voir `CONTRAINTES.md` pour les limitations fixes non négociables.

---

## Légende

| Statut | Description |
|--------|-------------|
| **Acceptée** | Hypothèse validée par observation ou preuve |
| **Active** | Hypothèse en vigueur, pas encore validée ni invalidée |
| **À valider** | Hypothèse qui doit être vérifiée à une date précise |
| **Invalidée** | Hypothèse qui s'est avérée fausse — contingence activée |

---

## 1. Hypothèses sur le partenaire et les utilisateurs

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-01 | L'APHVE accepte de s'engager comme partenaire officiel et de signer la convention SARIC | Active | Présentation du MIP à l'APHVE (sem 4-5) | Chercher un autre organisme pour personnes DV (ex: IRDPQ, INLB) ou poursuivre sans partenaire formel |
| H-02 | L'APHVE peut recruter un groupe d'utilisateurs non-voyants disponibles pour >= 2 sessions de test pendant le projet | Active | Discussion avec l'APHVE lors de la présentation du MIP (sem 4-5) | Recruter des testeurs DV via d'autres organismes ou via la communauté Discord du projet |
| H-03 | Le CER approuve le protocole de test avec personnes DV dans un délai de 1-2 semaines (pas de CER complet requis) | Active | Soumission du formulaire d'avis (>= 4 sem avant le test) | Si CER complet requis : prévoir 4-8 semaines supplémentaires. Soumettre plus tôt que prévu (dès S7). |
| H-04 | Le partenaire APHVE ne demande pas de clause de confidentialité empêchant la publication open-source | Active | Négociation de la convention SARIC | Négocier une exclusion pour le code source et les fichiers de conception. En dernier recours : retarder la publication. |

---

## 2. Hypothèses techniques — Audio HRTF

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-05 | Le rendu HRTF en temps réel (convolution, >= 4 sources) est **faisable en software pur** sur un microcontrôleur embarqué de la gamme visée (~240 MHz, ~8 MB RAM) | À valider | Benchmark PC (S7 sem 6-8) → estimation des besoins → benchmark sur le MCU choisi (S7 sem 10-14) | **Fallback 1 :** Réduire la taille des filtres HRTF (128 au lieu de 512 samples). **Fallback 2 :** Limiter à 2-3 sources simultanées. **Fallback 3 :** Ajouter un DSP matériel externe (budget additionnel ~30$). **Fallback 4 :** Audio stéréo simple (panoramique L/R sans HRTF). |
| H-06 | Un dataset HRTF open-source (MIT KEMAR, CIPIC ou SOFA) offre une qualité de spatialisation suffisante pour la localisation sonore (erreur < 30°) | À valider | Tests perceptuels au casque (S6-S7, tâche C.06) | Tester plusieurs datasets. Si aucun n'est satisfaisant : envisager des HRTF individualisées (plus complexe) ou accepter une précision moindre. |
| H-07 | Les tables HRTF tiennent en mémoire embarquée (<= 1.5 MB RAM) en laissant suffisamment de marge pour le game engine et les buffers audio | À valider | Mesure de la taille mémoire des HRTF pendant le prototypage PC | Compresser les HRTF (réduction du nombre de positions). Utiliser des HRTF à résolution réduite. |
| H-08 | La bibliothèque audio PC choisie (miniaudio, libsoundio, etc.) est portable et n'introduit pas de dépendance bloquante pour le portage embarqué | À valider | Choix de la bibliothèque (S6 sem 2-3, tâche C.02) | Écrire un wrapper minimal. Le contrat SpatialAudioEngine isole de toute façon le game engine de l'implémentation audio. |

---

## 2b. Hypothèses — Communauté et groupe d'utilisateurs DV

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-26 | L'APHVE peut aider à recruter >= 5 personnes DV intéressées à participer comme testeurs/consultants tout au long du projet | Active | Présentation du MIP à l'APHVE (sem 4-5), début du recrutement | Élargir le recrutement via d'autres organismes DV (IRDPQ, INLB) ou réseaux sociaux |
| H-27 | Un serveur Discord est un canal de communication accessible et adapté pour les personnes DV (compatibilité lecteur d'écran) | Active | Création du serveur et test avec 1-2 utilisateurs DV (sem 5-6) | Si Discord n'est pas accessible : utiliser un groupe de messagerie alternatif (email, WhatsApp, Telegram) |
| H-28 | Les membres du groupe d'utilisateurs DV restent engagés et disponibles pour répondre à >= 3 consultations sur la durée du projet | Active | Suivi de l'engagement tout au long du projet | Recruter de nouveaux membres si des départs surviennent. Proposer des incitatifs (accès prioritaire au prototype). |

---

## 3. Hypothèses techniques — Firmware et intégration

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-09 | MicroPython est intégrable dans un firmware C/C++ embarqué via `micropython-embed` (ou équivalent) sans conflit de mémoire ni de scheduler | À valider | Prototypage d'intégration (S7 sem 6-10, tâche E.01) | **Fallback :** Utiliser Lua (plus léger et mieux intégré en C). Adapter le format de mini-jeu. |
| H-10 | Les interfaces définies en Phase 0 couvrent tous les cas d'usage rencontrés pendant le développement du jeu | Active | Tout au long du développement; validation formelle au SYNC 1 (sem 6) | Modifier l'interface avec accord des deux équipes concernées. Documenter le changement. L'architecture en interfaces limite l'impact. |
| H-11 | Le GamepadMapper (manette PS4/Xbox) fournit un substitut suffisamment fidèle pour le développement du jeu (joysticks, boutons) malgré l'absence de 5 moteurs haptiques | Active | Dès les premiers tests de jeu sur PC (S6 sem 4-6) | Ajouter un mode de simulation haptique avancé (affichage console de l'intensité par moteur) ou utiliser un gamepad avec retour haptique plus riche. |
| H-12 | Le portage du game engine du PC vers le MCU choisi ne nécessite **pas de réécriture majeure** grâce à l'architecture en interfaces | À valider | Portage effectif (S8 sem 3-7) | Prévoir du temps supplémentaire pour le portage. L'architecture en blocs isole les changements à chaque implémentation d'interface. |

---

## 4. Hypothèses matérielles

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-13 | Il existe un microcontrôleur sur le marché qui satisfait simultanément les besoins en CPU, RAM, I2S stéréo, USB OTG, >= 4 canaux ADC et >= 5 canaux PWM, pour < 15$ unitaire | À valider | Analyse des candidats MCU (S6-S7, tâches F.01-F.04) | Relâcher une contrainte (ex: USB via puce externe, PWM via expandeur I2C). Accepter un coût unitaire plus élevé. |
| H-14 | Le fabricant de PCB (JLCPCB/PCBWay) livre en <= 3 semaines après commande | Active | À chaque commande de PCB | Commander plus tôt. Avoir un plan de test sur breadboard comme solution de repli temporaire. |
| H-15 | Les moteurs de vibration ERM à 3V ont un temps de réponse suffisant pour un feedback haptique perceptible (< 100 ms start/stop) | À valider | Tests sur breadboard (S7 sem 8-12) | Passer à des moteurs LRA (Linear Resonant Actuator) avec driver DRV2605L, plus rapides mais plus chers (~5$/unité). |
| H-16 | La batterie LiPo choisie (>= 2000 mAh) offre une autonomie >= 4h en usage typique (jeu actif, audio continu, haptique intermittent) | À valider | Test d'autonomie sur prototype assemblé (S8) | Augmenter la capacité de la batterie (3000+ mAh). Optimiser la consommation (sleep Wi-Fi, PWM moteurs réduit). |
| H-17 | Le boîtier imprimé en 3D FDM est suffisamment solide et ergonomique pour une utilisation prolongée (30+ min) sans inconfort | À valider | Test d'ergonomie (S8 sem 5-7) | Itérer sur le design du boîtier. Changer de matériau (PETG plus résistant que PLA). Ajouter du rembourrage. |

---

## 4b. Hypothèses — IDE

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-29 | Le stack technologique choisi (Electron/React/TypeScript ou équivalent) permet de créer un IDE accessible (TTS, ARIA, navigation clavier) dans les délais du projet | À valider | Prototype IDE en S7 sem 1-4 | Réduire le périmètre de l'IDE (éditeur + transfert USB seulement). Utiliser un éditeur existant (VSCode + extension custom) comme fallback. |
| H-30 | La Web Speech API (ou équivalent) fournit un TTS de qualité suffisante en français pour vocaliser le code et les diagnostics | À valider | Tests TTS lors du prototype IDE (S7 sem 2-4) | Utiliser une bibliothèque TTS tierce (eSpeak, pico2wave) ou un service cloud (Google TTS). |
| H-31 | La communication USB série (Web Serial API ou `serialport` npm) fonctionne de manière fiable depuis l'IDE vers la console | À valider | Tests d'intégration IDE-console (S7 sem 8-12) | Utiliser un script de transfert en ligne de commande comme solution de repli. |
| H-32 | L'intégration d'un assistant IA (LLM) dans l'IDE est faisable dans le périmètre du projet | À valider | Prototypage en S7 (si temps disponible) | L'assistant IA est priorité I/S — le reporter en post-livraison si nécessaire. L'IDE reste fonctionnel sans IA. |

---

## 5. Hypothèses sur les ressources

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-18 | Les 7 membres de l'équipe restent actifs sur toute la durée du projet, incluant >= 1 étudiant GE et >= 1 spécialisé en signal/audio | Active | Formation des équipes (S6 sem 1) | Redistribuer les responsabilités. Si pas de GE : confier la partie PCB à un GI avec expérience électronique, ou simplifier le design. |
| H-19 | Les laboratoires de la Faculté de génie sont accessibles quand nécessaire (l'équipe dispose déjà de ses propres imprimantes 3D) | Active | Réservation des locaux (S7-S8) | Réserver tôt. Utiliser les imprimantes 3D de l'équipe comme solution principale. |
| H-20 | Les composants électroniques nécessaires sont en stock chez les fournisseurs (DigiKey, Mouser, Amazon) et livrables en <= 2 semaines | Active | À chaque commande | Commander en avance. Identifier des composants alternatifs (second source) pour les pièces critiques. |
| H-21 | Le budget de 500$ est suffisant pour couvrir le prototype complet (incluant imprévus) | Active | Suivi financier continu | Réduire le périmètre (ex: 3 moteurs au lieu de 5). Chercher du financement additionnel via le partenaire. Utiliser des composants récupérés. |
| H-22 | L'équipe est en mesure de produire les assets audio nécessaires (enregistrements propres, création sonore) et de compléter avec des sources libres (CC0) si nécessaire | Active | Production des sons (S6 sem 3-10) | Sourcer les sons manquants sur Freesound.org (CC0). Utiliser des outils de synthèse sonore. |

---

## 6. Hypothèses de gestion

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence si invalidée |
|----|-----------|--------|-------------------|----------------------------------|
| H-23 | Chaque membre investit effectivement ~135h/session et respecte ses engagements du contrat d'équipe | Active | Suivi hebdomadaire des heures | Mécanisme PME (évaluation par les pairs). Discussion avec le superviseur. Redistribution des tâches si nécessaire. |
| H-24 | La méthode de gestion choisie (traditionnelle, agile ou hybride) est adaptée au projet et à l'équipe | Active | Évaluation après le SYNC 1 (sem 6) | Ajuster la méthode en cours de projet. Passer d'une approche à une autre si nécessaire. |
| H-25 | Les feedbacks du coaching et des superviseurs sont intégrables sans remise en question fondamentale de l'architecture | Active | Après chaque coaching | L'architecture en interfaces absorbe la plupart des changements. Si un changement fondamental est requis : réévaluer le périmètre. |

---

## Suivi des hypothèses

Le statut de chaque hypothèse doit être revu aux points de synchronisation :

| Moment | Hypothèses à valider en priorité |
|--------|----------------------------------|
| **SYNC 1** (sem 6) | H-01 (partenaire), H-06 (qualité HRTF), H-10 (interfaces), H-11 (GamepadMapper), H-18 (équipe), H-26 (recrutement DV), H-27 (Discord accessible) |
| **SYNC 2** (sem 14) | H-05 (HRTF embarqué), H-07 (mémoire HRTF), H-08 (bibliothèque audio), H-13 (MCU), H-09 (MicroPython), H-29 (stack IDE), H-30 (TTS) |
| **SYNC 3** (sem 22) | H-12 (portage), H-14 (livraison PCB), H-15 (moteurs ERM), H-16 (autonomie), H-17 (boîtier), H-31 (USB série IDE), H-28 (engagement DV) |

---

*Document vivant — mettre à jour le statut de chaque hypothèse dès qu'une information nouvelle est disponible.*
