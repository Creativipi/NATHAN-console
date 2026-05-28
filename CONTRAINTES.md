# Contraintes du Projet NATHAN Console v2.0

**Date :** 2026-05-27
**Session :** PMC660 (S6, E2026)

> Les contraintes sont des **limitations fixes** que le projet doit respecter.
> Elles ne sont pas négociables — elles encadrent l'espace de solution.
> Voir `HYPOTHESES.md` pour les suppositions de travail qui, elles, pourraient changer.

---

## 1. Contraintes d'accessibilité

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-01 | Le système doit fonctionner **entièrement sans retour visuel** — aucun écran, aucune LED nécessaire au gameplay | Le public cible est constitué de personnes non-voyantes. Tout feedback visuel serait inutile et exclurait l'utilisateur principal. |
| C-02 | L'audio doit être restitué **au casque stéréo uniquement** (pas de haut-parleurs) | L'audio spatial binaural (HRTF) nécessite un casque pour produire l'effet de spatialisation 3D. Des haut-parleurs détruiraient l'illusion directionnelle. |
| C-03 | Tous les contrôles physiques (boutons, joysticks) doivent être **différenciables au toucher** sans indication visuelle | L'utilisateur ne peut pas lire d'étiquettes ni voir les couleurs des boutons. La forme, la taille et la position doivent suffire à identifier chaque contrôle. |
| C-04 | Tous les menus et interactions du jeu doivent être **navigables exclusivement par le son** | Aucun menu textuel ne peut être affiché. La navigation repose sur des annonces vocales, des signatures musicales et des sons d'interface. |

---

## 2. Contraintes techniques

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-05 | Le game engine doit être **agnostique du matériel** via des interfaces abstraites (contrats d'interface) | L'architecture en blocs avec interfaces permet le développement parallèle sur PC et le portage ultérieur sans réécriture. C'est la stratégie fondamentale du projet. |
| C-06 | Le développement logiciel doit se faire **d'abord sur PC** avant tout portage embarqué | Le choix du microcontrôleur dépend des besoins réels mesurés par benchmark. Développer sur PC permet d'avancer sans être bloqué par le matériel. |
| C-07 | Le choix du microcontrôleur doit être basé sur un **benchmark quantitatif** des besoins réels (CPU, RAM, I/O) mesurés pendant le développement PC | Choisir un MCU avant de connaître les besoins réels risquerait de sélectionner un composant inadéquat (trop faible ou surdimensionné). |
| C-08 | Les assets audio doivent être au format **WAV 16 bits, 44.1 kHz, mono** (effets) ou **stéréo** (ambiances) | Format standard compatible avec les pipelines audio embarqués courants. Le mono est requis pour les sources spatialisées (le moteur HRTF applique la stéréo). |
| C-09 | Les mini-jeux utilisateurs doivent être écrits en **MicroPython** (pas en C/C++) | MicroPython est accessible aux débutants, y compris des personnes non-voyantes apprenant la programmation. Le C/C++ serait une barrière trop élevée. |
| C-10 | Les mini-jeux doivent s'exécuter dans un **sandbox isolé** sans accès au firmware ni aux fichiers hors de leur dossier | Sécurité : un mini-jeu tiers ne doit pas pouvoir corrompre le système, écraser le firmware ou accéder aux données d'autres jeux. |
| C-11 | La communication entre la console et l'IDE doit passer par **USB CDC** (port série virtuel) | Le protocole USB CDC est simple, universel et ne nécessite pas de driver spécifique sur la plupart des OS. L'IDE et le firmware utilisent ce protocole comme interface de transfert. |
| C-12 | Le stockage des assets et des mini-jeux doit être sur **support amovible** (carte micro SD) | Permet de mettre à jour le contenu sans reflasher le firmware. Facilite aussi le développement et les tests. |

---

## 3. Contraintes financières

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-13 | Budget total du prototype <= **500$ CAD** (incluant une réserve de ~30% pour imprévus) | Aucune contribution financière des départements ou programmes pour les projets PMC (Guide 2.2). Le financement est en autofinancement ou via le partenaire. |
| C-14 | Coût de production unitaire cible < **100$ CAD** | Pour que la console soit réellement accessible et abordable par rapport aux solutions existantes (manettes adaptées > 300$). |
| C-15 | Tous les achats doivent être **tracés avec factures** et consignés dans un rapport de dépenses | Exigence du guide étudiant (section 2.2.2) pour la gestion financière et la reddition de comptes. |

---

## 4. Contraintes temporelles

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-16 | Durée totale du projet : **3 sessions** (S6 été 2026, S7 hiver 2027, S8 automne 2027), soit ~78 semaines au total | Cadre du cours PMC660-760-860. Non modifiable. |
| C-17 | Disponibilité par personne : **135h/session** (soit 540h/personne sur les 3 sessions) | Estimé de base du guide étudiant (section 1, note 7) : 135h par tranche de 3 crédits. |
| C-18 | Les **contrats d'interface doivent être gelés** avant le début du développement (fin de la semaine 2) | Tout retard dans la définition des interfaces bloque le développement parallèle de tous les blocs. |
| C-19 | Le **protocole d'essai** pour tout test du prototype doit être soumis **>= 2 semaines avant** l'expérimentation | Exigence du guide étudiant (section 2.1.5). Fabriquer/tester sans protocole approuvé est une faute grave. |
| C-20 | Le **formulaire d'avis au CER** doit être soumis **>= 4 semaines avant** tout test avec des personnes vulnérables (DV) | Exigence du guide étudiant (section 2.1.4). Le CER peut prendre 1-2 semaines pour répondre, plus si un CER complet est requis. |

---

## 5. Contraintes réglementaires et légales

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-21 | Chaque membre doit signer la **cession de droits** (Annexe A) — l'UdeS est propriétaire du prototype pendant le projet | Exigence PMC. Sans cette signature → note "Incomplet" (IN) pour la session. Le prototype est restitué à la fin du projet. |
| C-22 | La **convention de partenariat** (SARIC) doit être signée **avant de léguer quoi que ce soit** au partenaire | Exigence du guide étudiant (section 2.1.2, étape 5). Protection légale et assurance. |
| C-23 | Les tests avec personnes vulnérables (non-voyantes) nécessitent une **approbation éthique du CER** | Les personnes DV sont considérées comme population vulnérable. Le CER doit évaluer les risques et approuver le protocole. |
| C-24 | Le projet doit respecter la **Politique santé et sécurité de l'UdeS** (2500-004) et la **Directive 2600-042** | Obligation légale pour tout travail en laboratoire ou atelier de l'UdeS. Formation sécurité requise si applicable. |
| C-25 | Les logiciels et datasets utilisés doivent être sous **licence libre** compatible avec la publication open-source | Le projet est open-source (R-38). Tout composant propriétaire ou sous licence restrictive est incompatible. |

---

## 6. Contraintes matérielles et de fabrication

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-26 | Le boîtier doit être **fabricable par impression 3D FDM** (PLA ou PETG) | L'équipe dispose de ses propres imprimantes 3D et a accès à celles de la Faculté. Pas de budget ni de volume pour l'injection plastique. |
| C-27 | Le PCB doit être **fabriqué par un service externe** (JLCPCB, PCBWay ou équivalent) | La Faculté ne fabrique pas de PCB multicouches. Délai de fabrication typique : 2-3 semaines. |
| C-28 | La **soudure et l'assemblage** doivent être réalisés dans les ateliers de l'UdeS ou chez le partenaire | Exigence de sécurité et d'assurance (Guide 2.1.7). Les activités hors UdeS/partenaire ne sont pas couvertes par l'assurance. |
| C-29 | La console doit tenir dans les mains d'un adulte : **largeur <= 16 cm** | Contrainte ergonomique pour une manette de jeu portable. Au-delà, la prise en main devient inconfortable. |

---

## 7. Contraintes de contenu et de propriété intellectuelle

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-30 | Tous les assets audio (samples, musiques) doivent être sous **licence libre** (CC0, CC-BY) ou **produits par l'équipe** (enregistrements et créations sonores propres) | Le projet est open-source. Des assets sous copyright rendraient la redistribution illégale. L'équipe produit une partie significative des assets elle-même. |
| C-31 | L'IDE de programmation de mini-jeux fait **partie intégrante** du projet : il doit être développé, accessible et fonctionnel pour la livraison | L'IDE est le moyen par lequel les utilisateurs (y compris non-voyants) programment et transfèrent des mini-jeux sur la console. Il est indissociable de l'expérience NATHAN. |
| C-32 | La propriété intellectuelle du projet est gérée par la **convention SARIC** et la cession de droits UdeS | Pendant le projet, l'UdeS est propriétaire. À la fin, l'équipe/le partenaire récupère les droits selon la convention. |

---

*Document vivant — à mettre à jour si une contrainte change (avec justification et accord des parties concernées).*
