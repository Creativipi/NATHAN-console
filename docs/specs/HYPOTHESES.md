# Hypothèses de Travail — Projet NATHAN Console v2.0

**Date :** 2026-05-28
**Session :** PMC660 (S6, E2026)

> Les hypothèses de travail sont des **suppositions acceptées comme vraies** pour la planification,
> mais qui **pourraient s'avérer fausses** et nécessiter un ajustement.
> Chaque hypothèse est suivie en continu : si elle est invalidée, le plan de contingence s'active.
> Voir `CONTRAINTES.md` pour les limitations fixes non négociables.

---

## Légende

| Statut | Description |
|--------|-------------|
| **Acceptée** | Validée par observation ou preuve |
| **Active** | En vigueur, pas encore validée ni invalidée |
| **À valider** | Doit être vérifiée à une date précise |
| **Invalidée** | S'est avérée fausse : contingence activée |

---

## 1. Partenaire et utilisateurs DV

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-01 | **Engagement APHVE** : l'APHVE accepte de s'engager comme partenaire officiel et de signer la convention SARIC | Active | Présentation du MIP à l'APHVE (sem 4-5) | Chercher un autre organisme DV (IRDPQ, INLB) ou poursuivre sans partenaire formel |
| H-02 | **Recrutement testeurs** : l'APHVE aide à recruter >= 5 personnes DV pour tester/consulter tout au long du projet | Active | Présentation du MIP à l'APHVE (sem 4-5) | Recruter via d'autres organismes DV ou la communauté Discord du projet |
| H-03 | **Délai CER** : le CER approuve le protocole DV en 1-2 semaines (pas de CER complet requis) | Active | Soumission du formulaire d'avis (>= 4 sem avant le test) | Si CER complet requis : prévoir 4-8 semaines de plus. Soumettre dès S7. |
| H-04 | **Pas de clause de confidentialité bloquante** : l'APHVE n'empêche pas la publication open-source | Active | Négociation de la convention SARIC | Négocier une exclusion pour le code et les fichiers de conception. En dernier recours, retarder la publication. |
| H-05 | **Discord accessible** : un serveur Discord est utilisable par les personnes DV (compatible lecteur d'écran) | Active | Création du serveur et test avec 1-2 utilisateurs DV (sem 5-6) | Utiliser un canal alternatif (email, WhatsApp, Telegram) si Discord n'est pas accessible |
| H-06 | **Engagement durable du groupe** : les membres DV répondent à >= 3 consultations sur la durée du projet | Active | Suivi de l'engagement tout au long du projet | Recruter de nouveaux membres en cas de départs; proposer des incitatifs (accès prioritaire au prototype) |

---

## 2. Audio HRTF

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-07 | **HRTF faisable sur MCU** : le rendu HRTF temps réel (>= 4 sources) tient sur un microcontrôleur de la gamme visée | À valider | Benchmark PC (S7) → estimation → benchmark sur le MCU choisi (S7) | Fallbacks : filtres courts (128 vs 512 samples); 2-3 sources max; DSP externe (~30$); stéréo simple sans HRTF |
| H-08 | **Qualité du dataset HRTF** : un dataset open-source (MIT KEMAR, CIPIC, SOFA) donne une localisation suffisante (erreur < 30°) | À valider | Tests perceptuels au casque (S6-S7) | Tester plusieurs datasets; envisager des HRTF individualisées ou accepter une précision moindre |
| H-09 | **HRTF en mémoire** : les tables tiennent en <= 1.5 MB RAM en laissant de la marge pour le moteur et les buffers | À valider | Mesure de la taille mémoire pendant le prototypage PC | Compresser les HRTF (moins de positions) ou réduire la résolution |
| H-10 | **Bibliothèque audio portable** : la bibliothèque PC choisie n'introduit pas de dépendance bloquante pour le portage | À valider | Choix de la bibliothèque (S6) | Écrire un wrapper minimal; le contrat SpatialAudioEngine isole déjà le moteur de l'implémentation |

---

## 3. Firmware et intégration

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-11 | **MicroPython intégrable** : l'interpréteur s'intègre dans le firmware C/C++ sans conflit mémoire ni scheduler | À valider | Prototypage d'intégration (S7) | Utiliser Lua (plus léger, mieux intégré en C) et adapter le format de mini-jeu |
| H-12 | **Interfaces suffisantes** : les interfaces de Phase 0 couvrent tous les cas d'usage du développement | Active | Tout au long du dev; validation formelle au SYNC 1 (sem 6) | Modifier l'interface avec accord des 2 équipes; l'architecture limite l'impact |
| H-13 | **GamepadMapper fidèle** : la manette PS4/Xbox est un substitut suffisant malgré l'absence de 5 moteurs | Active | Premiers tests de jeu sur PC (S6) | Mode de simulation haptique avancé (logs d'intensité) ou gamepad à retour haptique plus riche |
| H-14 | **Portage sans réécriture majeure** : le passage du PC au MCU se limite aux implémentations d'interface | À valider | Portage effectif (S8) | Prévoir du temps supplémentaire; l'architecture en blocs isole les changements |

---

## 4. Matériel

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-15 | **MCU adéquat disponible** : un MCU satisfait CPU, RAM, I2S, USB OTG, >= 4 ADC, >= 5 PWM pour < 15$ | À valider | Analyse des candidats MCU (S6-S7) | Relâcher une contrainte (USB ou PWM via puce externe); accepter un coût unitaire plus élevé |
| H-16 | **Livraison PCB <= 3 semaines** : le fabricant (JLCPCB/PCBWay) respecte ce délai | Active | À chaque commande de PCB | Commander plus tôt; garder un plan de test breadboard comme repli temporaire |
| H-17 | **Moteurs ERM assez rapides** : temps de réponse < 100 ms pour un feedback perceptible | À valider | Tests sur breadboard (S7) | Passer à des moteurs LRA avec driver DRV2605L (plus rapides, ~5$/unité) |
| H-18 | **Autonomie suffisante** : la batterie LiPo (>= 2000 mAh) donne >= 4h en usage typique | À valider | Test d'autonomie sur prototype assemblé (S8) | Augmenter la capacité (3000+ mAh); optimiser la consommation (sleep Wi-Fi, PWM réduit) |
| H-19 | **Boîtier 3D solide et ergonomique** : utilisable 30+ min sans inconfort | À valider | Test d'ergonomie (S8) | Itérer le design; passer au PETG (plus résistant); ajouter du rembourrage |

---

## 5. IDE

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-20 | **Stack IDE adéquat** : la stack choisie permet un IDE accessible (TTS, ARIA, clavier) dans les délais | À valider | Prototype IDE (S7) | Réduire le périmètre (éditeur + transfert USB); fallback vers VSCode + extension custom |
| H-21 | **TTS français suffisant** : la Web Speech API (ou équivalent) vocalise correctement code et diagnostics | À valider | Tests TTS lors du prototype IDE (S7) | Bibliothèque TTS tierce (eSpeak, pico2wave) ou service cloud (Google TTS) |
| H-22 | **USB série fiable** : la communication (Web Serial ou serialport npm) fonctionne de façon fiable IDE → console | À valider | Tests d'intégration IDE-console (S7) | Script de transfert en ligne de commande comme repli |
| H-23 | **Assistant IA faisable** : l'intégration d'un LLM dans l'IDE tient dans le périmètre | À valider | Prototypage en S7 (si temps disponible) | Reporter l'IA en post-livraison; l'IDE reste fonctionnel sans IA |

---

## 6. Ressources

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-24 | **Équipe stable** : les 7 membres restent actifs, dont >= 1 GE et >= 1 spécialisé signal/audio | Active | Formation des équipes (S6 sem 1) | Redistribuer les responsabilités; confier le PCB à un GI expérimenté si pas de GE |
| H-25 | **Laboratoires accessibles** : labos de la Faculté disponibles (l'équipe a ses propres imprimantes 3D) | Active | Réservation des locaux (S7-S8) | Réserver tôt; utiliser les imprimantes de l'équipe comme solution principale |
| H-26 | **Composants en stock** : disponibles chez les fournisseurs (DigiKey, Mouser, Amazon), livrables en <= 2 semaines | Active | À chaque commande | Commander en avance; identifier des composants alternatifs (second source) |
| H-27 | **Budget suffisant** : 500$ couvre le prototype complet (imprévus inclus) | Active | Suivi financier continu | Réduire le périmètre (3 moteurs au lieu de 5); financement additionnel; composants récupérés |
| H-28 | **Production audio interne** : l'équipe peut produire les assets (enregistrements, création) et compléter avec du CC0 | Active | Production des sons (S6) | Sourcer les sons manquants sur Freesound.org (CC0); outils de synthèse sonore |

---

## 7. Gestion

| ID | Hypothèse | Statut | Validation prévue | Plan de contingence |
|----|-----------|--------|-------------------|---------------------|
| H-29 | **Implication des membres** : chacun investit ~135h/session et respecte le contrat d'équipe | Active | Suivi hebdomadaire des heures | Mécanisme PME (évaluation par les pairs); discussion avec le superviseur; redistribution |
| H-30 | **Méthode de gestion adaptée** : la méthode choisie (traditionnelle, agile, hybride) convient au projet | Active | Évaluation après le SYNC 1 (sem 6) | Ajuster ou changer de méthode en cours de projet |
| H-31 | **Feedbacks intégrables** : les retours du coaching n'exigent pas de remise en question fondamentale | Active | Après chaque coaching | L'architecture en interfaces absorbe la plupart des changements; sinon réévaluer le périmètre |
| H-32 | **Convention SARIC dans les délais** : la convention de partenariat se conclut sans bloquer le projet | Active | Suivi du dossier SARIC (S6-S7) | Avancer le développement en parallèle; relancer la coordination PMC en cas de retard |

---

## Suivi des hypothèses

Le statut de chaque hypothèse est revu aux points de synchronisation :

| Moment | Hypothèses à valider en priorité |
|--------|----------------------------------|
| **SYNC 1** (sem 6) | H-01 (partenaire), H-02 (recrutement), H-05 (Discord), H-08 (qualité HRTF), H-12 (interfaces), H-13 (GamepadMapper), H-24 (équipe) |
| **SYNC 2** (sem 14) | H-07 (HRTF embarqué), H-09 (mémoire HRTF), H-10 (bibliothèque audio), H-11 (MicroPython), H-15 (MCU), H-20 (stack IDE), H-21 (TTS) |
| **SYNC 3** (sem 22) | H-06 (engagement DV), H-14 (portage), H-16 (livraison PCB), H-17 (moteurs ERM), H-18 (autonomie), H-19 (boîtier), H-22 (USB série IDE) |

---

*Document vivant — mettre à jour le statut de chaque hypothèse dès qu'une information nouvelle est disponible.*
