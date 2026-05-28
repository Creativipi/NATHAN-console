# Besoins — Projet NATHAN Console v2.0

**Date :** 2026-05-28
**Session :** PMC660 (S6, E2026)

> Les besoins décrivent **ce que le mandataire et les utilisateurs attendent** du produit.
> Ils expriment le **pourquoi** : les problèmes à résoudre et les résultats souhaités.
> Voir `REQUIS.md` (spécifications mesurables), `CONTRAINTES.md` (limites), `HYPOTHESES.md` (suppositions).

---

## 1. Besoins du mandataire (APHVE)

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-01 | **Aucune console dédiée n'existe** : un produit conçu dès le départ pour un utilisateur qui ne voit pas | Les solutions existantes sont des adaptations partielles de consoles visuelles (manettes adaptées > 300$). L'APHVE confirme ce besoin non comblé dans sa communauté. | R-01, R-02, R-14 |
| B-02 | **Immersion sonore 3D** : localiser les objets, murs et personnages uniquement par le son au casque | Le son spatial remplace la vue pour comprendre l'environnement de jeu. | R-01, R-02, R-04 |
| B-03 | **Retour tactile directionnel** : sentir la direction des contacts et obstacles par vibrations, comme un bâton d'aveugle | Le toucher complète le son pour percevoir l'espace immédiat. | R-03, R-05, R-22 |
| B-04 | **Jouer de la musique** : guitare, batterie de manière intuitive | Répond à l'intérêt des personnes DV pour la musique comme mode d'expression privilégié. | R-10 |
| B-05 | **Produit abordable** : accessible aux personnes et organismes desservant les personnes DV | Comparé aux solutions existantes (manettes adaptées, équipements spécialisés > 300$). | R-60 |
| B-06 | **Open-source** : reproductible, modifiable et améliorable par d'autres | Permet la pérennité et la diffusion au-delà du cadre académique. | R-61 |
| B-07 | **Validation par les utilisateurs DV** : tester avec un groupe recruté via l'APHVE | S'assurer que le produit répond réellement aux besoins du public cible. | R-56, R-58 |

---

## 2. Besoins des utilisateurs finaux (joueurs non-voyants)

### 2.1 Expérience de jeu

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-08 | **Jouer sans aide extérieure** : prendre la console, l'allumer et jouer de façon autonome | L'autonomie est fondamentale pour les personnes DV. Dépendre d'un tiers annule le plaisir. | R-01, R-06 |
| B-09 | **Comprendre les contrôles rapidement** : apprendre sans lire de manuel | L'apprentissage doit être entièrement audio, via un tutoriel vocal intégré. | R-06 |
| B-10 | **Se repérer dans l'espace** : savoir où on est et dans quelle direction aller, sans carte visuelle | Le son spatial 3D et le bâton virtuel remplacent la carte et la vision. | R-02, R-04, R-05 |
| B-11 | **Distinguer les zones** : chaque lieu a une identité sonore propre | Comme dans la vie réelle, une personne aveugle se repère par les sons ambiants. | R-09 |
| B-12 | **Feedback immédiat** : son + vibration à chaque action, sans délai perceptible | Sans retour visuel, un délai crée de l'incertitude et de la frustration. | R-15, R-16 |
| B-13 | **Confort prolongé** : jouer 30+ min sans fatigue des mains ni inconfort | La manette doit être ergonomique, légère et son autonomie ne doit pas couper une session. | R-24, R-27 |

### 2.2 Accessibilité physique

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-14 | **Identifier chaque contrôle au toucher** : savoir instantanément quel bouton ou joystick on touche | Les contrôles doivent avoir formes, tailles ou textures distinctes. | R-28 |
| B-15 | **Brancher le casque facilement** : port jack 3.5mm localisable au toucher | Un port mal placé crée une frustration disproportionnée sans la vue. | R-23 |
| B-16 | **Connaître l'état de la console** : allumée/éteinte/en charge via un feedback non visuel | Les LEDs de statut sont inutiles; le feedback doit être sonore ou haptique. | R-01 |

---

## 3. Besoins des utilisateurs créateurs (programmeurs de mini-jeux)

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-17 | **Programmer sans connaissances avancées** : langage simple et API intuitive | Le public cible inclut des personnes DV apprenant la programmation; MicroPython pour sa simplicité. | R-07, R-35 |
| B-18 | **IDE entièrement accessible** : TTS, lecteur d'écran, clavier, sans éditeur tiers non adapté | Les IDE standards ne sont pas optimisés pour une utilisation sans vision. | R-36 à R-46 |
| B-19 | **Aide pendant la programmation** : diagnostics vocaux, modèles de code, assistant IA | Un débutant DV a besoin d'un feedback immédiat et vocal sur ses erreurs. | R-42, R-43, R-47 |
| B-20 | **Transfert facile** : envoyer un mini-jeu sur la console sans compilation ni flashage | Un simple transfert de fichier .py via USB suffit. | R-49, R-52 |
| B-21 | **Test rapide** : cycle écrire → transférer → jouer court (< 1 min) | Un cycle long décourage les créateurs, surtout les débutants. | R-52 |
| B-22 | **Logs en temps réel** : voir les logs de la console dans l'IDE pour déboguer | Sans feedback visuel du jeu, les logs sont le seul moyen de comprendre l'exécution. | R-50 |
| B-23 | **API claire et documentée** : son spatial, haptique, entrées | Les fonctions `nathan.*` doivent être auto-explicatives. | R-35 |

---

## 4. Besoins de l'équipe de projet

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-24 | **Travailler en parallèle** : pas de blocage entre les équipes (ELEC, ENG, AUD, JEU) | Avec 4 sous-équipes sur 3 sessions, le blocage croisé est le danger principal; les interfaces le résolvent. | R-31, R-32, R-33 |
| B-25 | **Développer sans attendre le matériel** : jeu jouable sur PC dès S6 avec manette USB | Le matériel ne sera prêt qu'en S8; le développement ne doit pas être bloqué. | R-31 |
| B-26 | **IDE intégré au projet** : développé par l'équipe, accessible et fonctionnel à la livraison | L'IDE est indissociable de l'expérience NATHAN (programmation des mini-jeux). | R-36, R-49 |
| B-27 | **Choisir le MCU sur des données concrètes** : pas sur des spéculations | Le benchmark PC mesure les besoins réels avant de sélectionner le composant. | R-30 |
| B-28 | **Respecter le cadre académique** : produire les livrables PMC dans les délais | Le projet est autant un exercice de gestion qu'un défi technique. | R-62 |
| B-29 | **Démontrer à l'Expo MégaGÉNIALE** : présentation convaincante et accessible au public | L'Expo est le point culminant; le prototype doit être fonctionnel et présentable. | R-63 |

---

## 5. Besoins de la communauté et de la société

| ID | Besoin | Contexte | Requis liés |
|----|--------|----------|-------------|
| B-30 | **Démocratiser le jeu vidéo** : pour les personnes ayant une déficience visuelle | Le jeu vidéo est un loisir universel dont les personnes DV sont largement exclues. | Finalité F1 (cadre logique) |
| B-31 | **Impliquer les utilisateurs DV en continu** : pas seulement aux tests finaux | Le feedback continu (via Discord) valide les choix de conception au fur et à mesure. | R-55, R-56 |
| B-32 | **Plateforme pédagogique** : apprendre la programmation via la création de mini-jeux | La programmation est un outil d'autonomisation pour les personnes DV. | R-07 |
| B-33 | **Contribution communautaire** : survie du projet au-delà du cadre académique | Un projet open-source documenté peut être repris par d'autres institutions. | R-61 |

---

## Traçabilité Besoins → Requis

| Besoin | Requis associés |
|--------|----------------|
| B-01, B-02 | R-01, R-02, R-04, R-14 |
| B-03 | R-03, R-05, R-22 |
| B-04 | R-10 |
| B-05 | R-60 |
| B-06, B-33 | R-61 |
| B-07, B-31 | R-55, R-56, R-58 |
| B-08, B-09 | R-01, R-06 |
| B-10 | R-02, R-04, R-05 |
| B-11 | R-09 |
| B-12 | R-15, R-16 |
| B-13 | R-24, R-27 |
| B-14, B-15, B-16 | R-23, R-28 |
| B-17, B-23 | R-07, R-35 |
| B-18, B-19, B-26 | R-36 à R-52 |
| B-20, B-21, B-22 | R-49, R-50, R-52 |
| B-24, B-25 | R-31, R-32, R-33 |
| B-27 | R-30 |
| B-28 | R-62 |
| B-29 | R-63 |
| B-32 | R-07 |

---

*Document vivant — à réviser après chaque rencontre avec le partenaire pour s'assurer que les besoins reflètent toujours les attentes réelles.*
