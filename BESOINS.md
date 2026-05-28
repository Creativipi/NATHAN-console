# Besoins du Projet NATHAN Console v2.0

**Date :** 2026-05-27
**Session :** PMC660 (S6, E2026)

> Les besoins décrivent **ce que le mandataire et les utilisateurs attendent** du produit.
> Ils expriment le **pourquoi** — les problèmes à résoudre et les résultats souhaités.
> Les requis (`REQUIS.md`) traduisent ensuite ces besoins en spécifications mesurables.
> Les contraintes (`CONTRAINTES.md`) définissent les limites, les hypothèses (`HYPOTHESES.md`) les suppositions.

---

## 1. Besoins du mandataire (APHVE)

### 1.1 Besoin fondamental

| ID | Besoin | Contexte |
|----|--------|----------|
| B-01 | **Il n'existe aucune console de jeu dédiée aux personnes non-voyantes.** Les solutions existantes sont des adaptations partielles de consoles visuelles (manettes adaptées > 300$, jeux avec mode accessibilité limité). Le mandataire a besoin d'un produit conçu **dès le départ** pour un utilisateur qui ne voit pas. | Les personnes non-voyantes n'ont accès à aucune console de jeu qui leur offre une expérience immersive comparable à ce qu'un joueur voyant vit avec une console traditionnelle. L'APHVE confirme ce besoin non comblé dans sa communauté. |

### 1.2 Besoins spécifiques du mandataire

| ID | Besoin | Lien avec les requis |
|----|--------|---------------------|
| B-02 | Le joueur doit pouvoir **s'immerger dans un monde sonore 3D** où il peut localiser les objets, les murs et les personnages autour de lui uniquement par le son au casque | R-01, R-02, R-04 |
| B-03 | Le joueur doit pouvoir **sentir physiquement** la direction des contacts et des obstacles grâce à des vibrations directionnelles, comme un retour tactile du bâton d'aveugle | R-03, R-05 |
| B-04 | Le joueur doit pouvoir **jouer de la musique** sur la console (guitare, batterie) de manière intuitive, répondant à l'intérêt des personnes DV pour la musique comme mode d'expression privilégié | R-10 |
| B-05 | Le produit doit être **abordable** pour les personnes et les organismes qui desservent les personnes DV, comparé aux solutions existantes (manettes adaptées, équipements spécialisés) | R-37 (< 100$ unitaire) |
| B-06 | Le produit doit être **open-source** pour que d'autres développeurs, organismes ou institutions puissent le reproduire, le modifier et l'améliorer | R-38 |
| B-07 | Le mandataire souhaite pouvoir **valider le produit** en le testant avec un groupe d'utilisateurs DV recrutés via l'APHVE pour s'assurer qu'il répond réellement aux besoins de ce public | R-39, tâches ETH-01 à ETH-05 |

---

## 2. Besoins des utilisateurs finaux (joueurs non-voyants)

### 2.1 Besoins d'expérience de jeu

| ID | Besoin | Contexte | Lien avec les requis |
|----|--------|----------|---------------------|
| B-08 | **Jouer sans aide extérieure** : l'utilisateur doit pouvoir prendre la console, l'allumer et jouer de façon autonome sans qu'une personne voyante doive l'assister | L'autonomie est un besoin fondamental pour les personnes DV. Dépendre d'un tiers pour jouer annule le plaisir et l'intérêt. | R-01, R-06 |
| B-09 | **Comprendre les contrôles rapidement** : un nouveau joueur doit pouvoir apprendre à jouer sans lire un manuel (qu'il ne peut de toute façon pas lire visuellement) | L'apprentissage doit être entièrement audio. Un tutoriel vocal intégré guide le joueur pas à pas. | R-06 |
| B-10 | **Se repérer dans l'espace** : le joueur a besoin de savoir où il est, ce qui l'entoure et dans quelle direction aller, sans carte visuelle | Le son spatial 3D (HRTF) et les signatures musicales par zone remplacent la carte visuelle. Le bâton d'aveugle virtuel remplace la vision pour la détection d'obstacles. | R-02, R-04, R-05 |
| B-11 | **Distinguer les zones du jeu** : chaque lieu doit avoir une identité sonore propre pour que le joueur sache où il se trouve | Comme dans la vie réelle, une personne aveugle se repère par les sons ambiants (cuisine = bruits de vaisselle, extérieur = bruits de rue). | R-09 |
| B-12 | **Recevoir un feedback immédiat** à chaque action (son + vibration) pour ne jamais être dans le doute sur ce qui se passe | Sans retour visuel, un délai ou une absence de feedback crée de l'incertitude et de la frustration. La latence doit être imperceptible. | R-15, R-16 |
| B-13 | **Jouer confortablement pendant une durée prolongée** (30+ minutes) sans fatigue des mains ni inconfort | La manette doit être ergonomique, légère et adaptée à des mains de tailles variées. L'autonomie de la batterie ne doit pas interrompre une session. | R-24, R-27 |

### 2.2 Besoins d'accessibilité physique

| ID | Besoin | Contexte | Lien avec les requis |
|----|--------|----------|---------------------|
| B-14 | **Identifier chaque contrôle au toucher** sans hésitation : le joueur doit instantanément savoir quel bouton ou joystick il touche | Les boutons doivent avoir des formes, tailles ou textures distinctes. Les joysticks doivent être à des positions symétriques et naturelles. | R-28 |
| B-15 | **Brancher le casque facilement** : le port jack 3.5mm doit être localisable au toucher et le branchement intuitif | Un port mal placé ou trop serré crée une frustration disproportionnée pour un utilisateur qui ne voit pas. | R-23 |
| B-16 | **Savoir si la console est allumée / éteinte / en charge** par un feedback non visuel (son de démarrage, vibration de confirmation) | Les LEDs de statut sont inutiles pour un utilisateur non-voyant. Le feedback doit être sonore ou haptique. | R-01 |

---

## 3. Besoins des utilisateurs créateurs (programmeurs de mini-jeux)

| ID | Besoin | Contexte | Lien avec les requis |
|----|--------|----------|---------------------|
| B-17 | **Programmer un mini-jeu sans connaissances avancées** en programmation : le langage doit être simple et l'API intuitive | Le public cible inclut des personnes non-voyantes qui apprennent la programmation. MicroPython est choisi pour sa simplicité. | R-07, R-35 |
| B-18 | **Disposer d'un IDE entièrement accessible** (TTS, lecteur d'écran, clavier) pour écrire du code sans dépendre d'un éditeur tiers non adapté | Les IDE standards (VSCode, etc.) ne sont pas optimisés pour une utilisation sans vision. L'IDE NATHAN doit être conçu dès le départ pour ce public. | R-42 à R-52 |
| B-19 | **Recevoir de l'aide pendant la programmation** : l'IDE doit guider le créateur via des diagnostics vocaux, des modèles de code et un assistant IA | Un débutant non-voyant a besoin d'un feedback immédiat et vocal sur ses erreurs, pas d'un soulignement rouge invisible. | R-48, R-49, R-53 |
| B-20 | **Transférer un mini-jeu sur la console facilement** depuis l'IDE, sans procédure complexe de compilation ou de flashage | Un simple transfert de fichier .py via USB suffit. Pas de toolchain à installer, pas de compilation croisée. | R-55, R-58 |
| B-21 | **Tester un mini-jeu rapidement** : le cycle écrire → transférer → jouer doit être court (< 1 min) | Un cycle de développement long décourage les créateurs, surtout les débutants. | R-58 |
| B-21b | **Voir les logs de la console en temps réel** dans l'IDE pour déboguer un mini-jeu | Sans feedback visuel du jeu, les logs sont le seul moyen de comprendre ce qui se passe pendant l'exécution. | R-56 |
| B-21c | **Accéder à une API claire et documentée** pour le son spatial, l'haptique et les entrées | Les fonctions `nathan.audio.play()`, `nathan.haptic.pulse()`, `nathan.input.joystick()` doivent être auto-explicatives. | R-35 |

---

## 4. Besoins de l'équipe de projet

| ID | Besoin | Contexte | Lien avec les requis |
|----|--------|----------|---------------------|
| B-21 | **Travailler en parallèle** sans blocage entre les équipes (ELEC, ENG, AUD, JEU) | Avec 4 sous-équipes sur 3 sessions, le risque de blocage croisé est le danger principal. L'architecture en interfaces (contrats) résout ce problème. | R-31, R-32, R-33 |
| B-22 | **Développer et tester le jeu sans attendre le matériel final** | Le matériel (PCB, boîtier) ne sera prêt qu'en S8. Le jeu doit être développable et jouable sur PC dès S6 avec une manette USB de substitution. | R-31, contrainte C-06 |
| B-22b | **Disposer d'un IDE accessible** pour programmer, transférer et tester les mini-jeux | L'IDE fait partie intégrante du projet. Il doit être accessible aux personnes DV (TTS, screen reader) et permettre un cycle écrire → transférer → jouer rapide. | R-07, R-26, contrainte C-31 |
| B-23 | **Choisir le microcontrôleur sur des données concrètes**, pas sur des spéculations | Le benchmark PC mesure les besoins réels en CPU, RAM et I/O avant de sélectionner le MCU. Cela évite de choisir un composant inadéquat. | R-30, contrainte C-07 |
| B-24 | **Respecter le cadre académique** : produire les livrables PMC (MIP, RPC1, RPC2, RLP, RAE) dans les délais et avec la qualité attendue | Le projet est autant un exercice de gestion de projet d'ingénierie qu'un défi technique. Les deux dimensions comptent pour la note. | R-40 |
| B-25 | **Démontrer le prototype à l'Expo MégaGÉNIALE** de manière convaincante et accessible au public | L'Expo est le point culminant du projet. Le prototype doit être fonctionnel, présentable et impressionnant pour un public varié. | R-41 |

---

## 5. Besoins de la communauté et de la société

| ID | Besoin | Contexte | Lien avec les requis |
|----|--------|----------|---------------------|
| B-26 | **Démocratiser l'accès au jeu vidéo** pour les personnes ayant une déficience visuelle | Le jeu vidéo est un loisir universel dont les personnes DV sont largement exclues. NATHAN vise à combler cette lacune. | Finalité F1 du cadre logique |
| B-27 | **Impliquer les utilisateurs DV tout au long du projet**, pas seulement aux tests finaux | Le feedback continu d'un groupe d'utilisateurs DV (via Discord) permet de valider les choix de conception au fur et à mesure et d'éviter de construire un produit qui ne répond pas aux vrais besoins. | R-61, R-62 |
| B-28 | **Créer une plateforme pédagogique** : permettre aux personnes DV d'apprendre la programmation via la création de mini-jeux | La programmation est un outil d'autonomisation. MicroPython + l'IDE accessible rendent cela possible. | R-07, R-09 |
| B-29 | **Favoriser la contribution communautaire** via l'open-source pour que le projet survive au-delà du cadre académique | Un projet open-source bien documenté peut être reproduit et amélioré par d'autres universités, organismes ou individus. | R-67 |

---

## Traçabilité Besoins → Requis

| Besoin | Requis associés |
|--------|----------------|
| B-01, B-02 | R-01, R-02, R-14 |
| B-03 | R-03, R-05, R-22 |
| B-04 | R-10 |
| B-05 | R-37 |
| B-06, B-28 | R-38 |
| B-07 | R-39 |
| B-08, B-09 | R-01, R-06 |
| B-10, B-11 | R-02, R-04, R-05, R-09 |
| B-12 | R-15, R-16 |
| B-13 | R-24, R-27 |
| B-14 | R-28 |
| B-17, B-18, B-19, B-20 | R-07, R-26, R-35 |
| B-21, B-22, B-23 | R-30, R-31, R-32, R-33 |
| B-24 | R-40 |
| B-25 | R-41 |

---

*Document vivant — à réviser après chaque rencontre avec le partenaire pour s'assurer que les besoins reflètent toujours les attentes réelles.*
