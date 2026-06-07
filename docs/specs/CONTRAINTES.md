# Contraintes — Projet NATHAN Console v2.0

**Date :** 2026-05-28
**Session :** PMC660 (S6, E2026)

> Les contraintes sont des **limitations fixes** que le projet doit respecter.
> Elles ne sont pas négociables : elles encadrent l'espace de solution.
> Voir `HYPOTHESES.md` pour les suppositions de travail qui, elles, pourraient changer.

---

## 1. Contraintes d'accessibilité

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-01 | **Aucun retour visuel** : le système fonctionne sans écran ni LED nécessaire au gameplay | Le public cible est non-voyant. Tout feedback visuel serait inutile et exclurait l'utilisateur principal. |
| C-02 | **Casque stéréo uniquement** : pas de haut-parleurs | L'audio binaural (HRTF) nécessite un casque; des haut-parleurs détruiraient l'illusion directionnelle. |
| C-03 | **Contrôles différenciables au toucher** : sans indication visuelle | L'utilisateur ne peut lire d'étiquettes ni voir les couleurs. Forme, taille et position doivent suffire. |
| C-04 | **Menus navigables au son** : toutes les interactions exclusivement par l'audio | Aucun menu textuel ne peut être affiché. Annonces vocales, signatures musicales et sons d'interface. |

---

## 2. Contraintes techniques

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-05 | **Game engine agnostique** : interfaces abstraites (contrats) entre le moteur et le matériel | Permet le développement parallèle sur PC et le portage ultérieur sans réécriture. Stratégie fondamentale du projet. |
| C-06 | **Développement PC-first** : développer sur PC avant tout portage embarqué | Le choix du MCU dépend des besoins mesurés par benchmark. Développer sur PC évite d'être bloqué par le matériel. |
| C-07 | **Choix du MCU basé sur benchmark** : décision quantitative (CPU, RAM, I/O) mesurée pendant le dev PC | Choisir un MCU avant de connaître les besoins risquerait de sélectionner un composant inadéquat. |
| C-08 | **Format audio standard** : WAV 16 bits, 44.1 kHz, mono (effets) ou stéréo (ambiances) | Compatible avec les pipelines audio embarqués. Le mono est requis pour la spatialisation HRTF. |
| C-09 | **Mini-jeux en MicroPython** : pas en C/C++ | MicroPython est accessible aux débutants, y compris les personnes DV apprenant la programmation. |
| C-10 | **Sandbox isolé** : les mini-jeux n'accèdent ni au firmware ni aux fichiers hors de leur dossier | Sécurité : un mini-jeu tiers ne doit pas corrompre le système ni les données d'autres jeux. |
| C-11 | **Communication via USB CDC** : port série virtuel entre la console et l'IDE | Protocole simple et universel, sans driver spécifique. Interface de transfert entre l'IDE et le firmware. |
| C-12 | **Stockage amovible** : assets et mini-jeux sur carte micro SD | Permet de mettre à jour le contenu sans reflasher le firmware; facilite le développement et les tests. |

---

## 3. Contraintes financières

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-13 | **Budget <= 500$ CAD** : prototype, incluant une réserve de ~30% pour imprévus | Aucune contribution financière des départements pour les projets PMC (Guide 2.2); autofinancement ou partenaire. |
| C-14 | **Coût de production cible < 100$ CAD** : par unité | Pour rendre la console accessible vs. les solutions existantes (> 300$). |
| C-15 | **Achats tracés** : factures conservées et consignées dans un rapport de dépenses | Exigence du guide étudiant (section 2.2.2) pour la gestion financière. |

---

## 4. Contraintes temporelles

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-16 | **3 sessions** : S6 (été 2026), S7 (hiver 2027), S8 (automne 2027) | Cadre du cours PMC660-760-860. Non modifiable. |
| C-17 | **540h/personne** : 135h (S6) + 270h (S7) + 135h (S8) sur les 3 sessions | Estimé du guide étudiant : 135h par tranche de 3 crédits (S6=3cr, S7=6cr, S8=3cr). |
| C-18 | **Interfaces gelées avant le développement** : fin de la semaine 2 | Tout retard dans la définition des interfaces bloque le développement parallèle de tous les blocs. |
| C-19 | **Protocole d'essai >= 2 semaines avant tout test** : du prototype | Exigence du guide (section 2.1.5). Tester sans protocole approuvé est une faute grave. |
| C-20 | **Formulaire CER >= 4 semaines avant tout test DV** : avec des personnes vulnérables | Exigence du guide (section 2.1.4). Le CER peut prendre 1-2 semaines, plus si un CER complet est requis. |

---

## 5. Contraintes réglementaires et légales

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-21 | **Cession de droits signée** (Annexe A) : l'UdeS est propriétaire du prototype pendant le projet | Exigence PMC. Sans signature → note "Incomplet" (IN). Le prototype est restitué à la fin. |
| C-22 | **Convention de partenariat signée avant tout legs** au partenaire (SARIC) | Exigence du guide (section 2.1.2, étape 5). Protection légale et assurance. |
| C-23 | **Approbation éthique du CER** : pour les tests avec personnes vulnérables (non-voyantes) | Les personnes DV sont une population vulnérable; le CER évalue les risques et approuve le protocole. |
| C-24 | **Santé et sécurité UdeS** : Politique 2500-004 et Directive 2600-042 | Obligation légale pour tout travail en laboratoire ou atelier de l'UdeS. |
| C-25 | **Composants sous licence libre** : compatible avec la publication open-source | Le projet est open-source (R-61). Tout composant propriétaire est incompatible. |

---

## 6. Contraintes matérielles et de fabrication

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-26 | **Boîtier en impression 3D FDM** : PLA ou PETG | L'équipe dispose de ses propres imprimantes 3D et accède à celles de la Faculté. Pas de budget pour l'injection. |
| C-27 | **PCB fabriqué en externe** : JLCPCB, PCBWay ou équivalent | La Faculté ne fabrique pas de PCB multicouches. Délai typique : 2-3 semaines. |
| C-28 | **Soudure et assemblage à l'UdeS ou chez le partenaire** | Exigence d'assurance (Guide 2.1.7). Les activités hors UdeS/partenaire ne sont pas couvertes. |
| C-29 | **Taille tenant en main** : largeur <= 16 cm | Contrainte ergonomique pour une manette portable. Au-delà, la prise en main devient inconfortable. |

---

## 7. Contraintes de contenu et de propriété intellectuelle

| ID | Contrainte | Justification |
|----|-----------|---------------|
| C-30 | **Assets audio libres ou produits par l'équipe** : licence libre (CC0, CC-BY) ou créations propres | Le projet est open-source; des assets sous copyright rendraient la redistribution illégale. |
| C-31 | **IDE intégré au projet** : développé, accessible et fonctionnel pour la livraison | L'IDE permet aux utilisateurs (y compris non-voyants) de programmer et transférer des mini-jeux. Indissociable de NATHAN. |
| C-32 | **PI gérée par la convention SARIC** : et la cession de droits UdeS | Pendant le projet, l'UdeS est propriétaire; à la fin, l'équipe/le partenaire récupère les droits. |

---

*Document vivant — à mettre à jour si une contrainte change (avec justification et accord des parties concernées).*
