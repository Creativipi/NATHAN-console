# Requis du Projet NATHAN Console v2.0

**Projet :** NATHAN — Narrative Audio Terminal for Humans with Alternative Navigation
**Date :** 2026-05-26
**Session :** PMC660 (S6, E2026)

> Ce fichier regroupe les **requis haut niveau** du projet.
> Les requis définissent **ce que** le système doit accomplir, pas **comment** (pas de choix de composants).
> Les tâches détaillées et la chronologie se trouvent dans `TACHES.md`.

---

## Légende

| Priorité | Description |
|----------|-------------|
| **E** | Essentiel — MVP, doit être livré |
| **I** | Important — attendu mais non bloquant |
| **S** | Souhaitable — si le temps le permet |

---

## 1. Requis Fonctionnels — Expérience Utilisateur

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-01 | Le joueur doit pouvoir jouer à un jeu complet **sans aucun retour visuel**, uniquement par le son et le toucher | E | 1 personne non-voyante complète une session de 15 min sans assistance |
| R-02 | Le joueur doit pouvoir localiser la direction d'un son dans l'espace 3D grâce à l'audio binaural au casque | E | 3/3 testeurs localisent une source sonore avec une erreur < 30° |
| R-03 | Le joueur doit pouvoir sentir la direction d'un contact physique (bâton, mur) par un feedback haptique directionnel | E | Un testeur identifie correctement la direction (gauche/centre/droite) dans 4/5 cas |
| R-04 | Le joueur doit pouvoir naviguer entre les pièces d'un environnement en se repérant par les signatures musicales des zones adjacentes | E | Un joueur aux yeux bandés identifie >= 3 pièces par leur son depuis le couloir |
| R-05 | Le joueur doit pouvoir utiliser un bâton d'aveugle virtuel pour détecter les obstacles, avec un retour sonore et haptique selon la surface touchée | E | Le joueur distingue >= 3 types de surfaces par le son et le toucher |
| R-06 | Un nouveau joueur doit comprendre les contrôles de base en < 5 min grâce à un tutoriel audio intégré | E | 2 nouveaux joueurs complètent le tutoriel et naviguent de façon autonome en < 5 min |
| R-07 | Le joueur doit pouvoir programmer et jouer à des mini-jeux créés par des tiers (en MicroPython) | I | Un mini-jeu écrit par un tiers fonctionne sur la console sans modification du firmware |

---

## 2. Requis Fonctionnels — Contenu de Jeu

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-08 | Le jeu "La Maison de Nathan" doit comporter >= 4 zones distinctes jouables (sur 6 planifiées) | E | 4 zones avec ambiance propre et >= 2 interactions chacune |
| R-09 | Chaque zone doit avoir une ambiance sonore unique et reconnaissable | E | 3/3 testeurs identifient correctement au moins 3 zones par leur son seul |
| R-10 | Le jeu doit inclure au moins un instrument de musique jouable (guitare ou batterie) | I | Un joueur produit une séquence musicale reconnaissable |
| R-11 | Le système doit inclure >= 2 mini-jeux d'exemple démontrant l'API MicroPython | I | 2 mini-jeux jouables depuis le hub de la Salle de Mini-Jeux |
| R-12 | La banque de sons doit contenir >= 50 sons uniques (ambiances, effets, voix, musiques) | E | Inventaire documenté >= 50 fichiers WAV |
| R-13 | Le jeu doit inclure une narration audio (voix de Nathan) pour le tutoriel et les instructions | E | >= 10 clips de narration intégrés |

---

## 3. Requis de Performance

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-14 | Le système doit supporter >= 4 sources sonores spatiales simultanées sans artefact audible | E | 4 sources jouent en simultané pendant 1 min sans coupure ni distorsion |
| R-15 | La latence audio bout-en-bout (action utilisateur -> son au casque) doit être < 50 ms | E | Mesure instrumentée < 50 ms |
| R-16 | La latence haptique (action utilisateur -> vibration moteur) doit être < 100 ms | E | Mesure instrumentée < 100 ms |
| R-17 | Le polling des entrées doit être >= 100 Hz | E | Intervalle moyen entre lectures < 10 ms |
| R-18 | Le système ne doit pas avoir de crash ni de fuite mémoire pendant 1h de jeu continu | E | Test de stabilité de 1h sans crash; heap libre stable |
| R-19 | Le boot de la console doit prendre < 5 secondes du power-on au menu principal | I | Mesure au chronomètre < 5 s |

---

## 4. Requis Hardware — Caractéristiques (sans choix de composants)

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-20 | La console doit avoir 2 joysticks analogiques double-axe avec bouton intégré | E | 4 axes analogiques + 2 boutons de click lus par le firmware |
| R-21 | La console doit avoir >= 7 boutons numériques (A, B, C, L1, R1, Start, Select) | E | Chaque bouton détecté sans ambiguïté par le firmware |
| R-22 | La console doit avoir >= 5 moteurs de vibration disposés en arc, contrôlables individuellement en intensité | E | 5 moteurs vibrent indépendamment à des intensités différentes |
| R-23 | La sortie audio doit être stéréo via jack 3.5mm, avec une qualité suffisante pour le HRTF binaural (>= 44.1 kHz, >= 16 bits, SNR > 80 dB) | E | Son spatial perceptible au casque; pas de bruit de fond gênant |
| R-24 | La console doit être alimentée par batterie rechargeable via USB-C | E | Autonomie >= 4h en usage typique; charge par USB-C |
| R-25 | Le stockage des assets (sons, mini-jeux) doit être sur support amovible (carte SD ou équivalent) | E | Lecture de fichiers WAV depuis le stockage |
| R-26 | La console doit pouvoir communiquer avec un PC via USB (port série virtuel) pour le transfert de mini-jeux | E | Transfert bidirectionnel fonctionnel via USB |
| R-27 | La console doit tenir dans les mains d'un adulte (largeur <= 16 cm) et être ergonomique | E | 3/3 testeurs confortables après 30 min |
| R-28 | Tous les contrôles doivent être différentiables au toucher (sans retour visuel) | E | 5/5 identifications correctes par un testeur les yeux bandés |
| R-29 | Le boîtier doit être fabricable par impression 3D FDM | E | Impression réussie, assemblage sans outil spécialisé |
| R-30 | Le microcontrôleur doit être choisi en fonction des besoins réels mesurés (CPU, RAM, I/O) à la suite du développement PC | E | Document de justification basé sur le benchmark du jeu sur PC |

---

## 5. Requis d'Architecture Logicielle

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-31 | Le game engine doit être **agnostique du matériel** grâce à des interfaces abstraites (contrats) pour les entrées, le son, l'haptique et le stockage | E | Le même code de jeu fonctionne avec une manette PS4/Xbox sur PC ET avec la manette finale |
| R-32 | Chaque interface (Input, Audio, Haptic, Storage) doit avoir au minimum 2 implémentations : une pour le dev PC, une pour le matériel final | E | Swap d'implémentation sans recompilation du game engine |
| R-33 | Les interfaces doivent être définies et gelées avant le début du développement (Phase 0) | E | Fichiers de contrat signés par les équipes concernées |
| R-34 | Le système de mini-jeux doit permettre l'exécution de scripts MicroPython dans un sandbox isolé | E | Script MicroPython exécuté; tentative d'accès hors sandbox bloquée |
| R-35 | L'API MicroPython `nathan.*` doit exposer les fonctions : audio (play, stop, set_ambient), haptic (pulse, sweep), input (joystick, button), game (score, end) | E | Chaque fonction appelable depuis un script MicroPython |

---

## 5b. Requis de l'IDE de programmation

L'IDE fait partie intégrante du projet. Son architecture est en 5 couches :
UX accessible → Édition → Assistant IA → Déploiement → Matériel.

### Couche 1 — UX accessible

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-42 | L'IDE doit intégrer un **TTS (text-to-speech)** en français pour vocaliser tout feedback, diagnostic et navigation | E | Chaque action de l'éditeur produit une annonce vocale pertinente en fr-FR |
| R-43 | L'IDE doit être compatible avec les **lecteurs d'écran** (ARIA live regions, rôles sémantiques) et navigable **entièrement au clavier** | E | Un utilisateur DV navigue dans l'éditeur, écrit du code et transfère un fichier sans aide visuelle |
| R-44 | L'IDE doit supporter un **shell vocal** (STT — speech-to-text) permettant de dicter des commandes ou du code | I | Commande vocale "ouvrir fichier main.py" exécutée correctement |
| R-45 | L'IDE doit offrir un **mode d'affichage accessible** (grand texte, contraste élevé) | I | Taille de police et contraste ajustables; lisible à 200% de zoom |

### Couche 2 — Édition

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-46 | L'IDE doit permettre d'écrire du code **MicroPython** avec **coloration syntaxique** et reconnaissance des fonctions `nathan.*` | E | Mots-clés Python colorés; `nathan.audio.play` reconnu et coloré |
| R-47 | L'IDE doit inclure un **explorateur de fichiers** (arborescence) pour créer, supprimer et organiser les projets de mini-jeux | E | Arborescence navigable; opérations CRUD fonctionnelles |
| R-48 | L'IDE doit inclure un **analyseur syntaxique (linter)** qui détecte les erreurs et les annonce via TTS | E | Erreur de syntaxe détectée et annoncée vocalement en < 2 secondes |
| R-49 | L'IDE doit inclure une **bibliothèque de modèles** (snippets/templates) de mini-jeux pour aider les débutants | I | >= 3 templates disponibles (jeu de réaction, quiz sonore, exploration) |
| R-50 | L'IDE doit supporter les **raccourcis clavier** standards (Ctrl+S, Ctrl+F, Ctrl+Shift+P palette de commandes) | E | Raccourcis fonctionnels et annoncés au lecteur d'écran |
| R-51 | L'IDE doit inclure un **terminal intégré** pour exécuter des commandes | E | Commandes exécutées avec streaming de sortie |
| R-52 | L'IDE doit supporter la **recherche et remplacement** dans les fichiers | E | Recherche case-insensitive, remplacement global fonctionnel |

### Couche 3 — Assistant IA

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-53 | L'IDE doit intégrer un **assistant IA** capable de répondre à des questions sur l'API `nathan.*` et d'aider à écrire du code | I | L'utilisateur pose "comment jouer un son à droite?" et reçoit un snippet fonctionnel |
| R-54 | L'assistant IA doit pouvoir **appliquer des modifications au code** (insertion, correction) avec validation avant application | S | Suggestion de l'IA appliquée au code après confirmation de l'utilisateur |

### Couche 4 — Déploiement

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-55 | L'IDE doit permettre de **transférer des fichiers .py vers la console** via USB CDC | E | Fichier .py de 5 KB transféré en < 10 secondes; intégrité vérifiée |
| R-56 | L'IDE doit afficher les **logs de la console en temps réel** via USB | E | Logs visibles dans le terminal intégré pendant l'exécution d'un mini-jeu |
| R-57 | L'IDE doit inclure un **gestionnaire de mini-jeux** affichant la liste des jeux sur la carte SD de la console (commande LIST) | E | Liste des mini-jeux récupérée et affichée; possibilité de supprimer (DELETE) |
| R-58 | L'IDE doit permettre un **cycle de développement rapide** : écrire → transférer → jouer en < 1 min | E | Temps mesuré du save au lancement du jeu sur console < 60 secondes |

### Couche 5 — Visualisation (optionnel)

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-59 | L'IDE doit inclure un **visualisateur de scène 2D** montrant le placement des sources sonores (coordonnées x/y/z) | S | Drag & drop des entités sonores; preview visuel des positions |
| R-60 | L'IDE doit permettre une **simulation audio HRTF** (via WebAudio) pour prévisualiser le son spatial avant envoi sur la console | S | Son spatialisé audible au casque depuis l'IDE |

---

## 6. Requis Communauté et Utilisateurs DV

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-61 | Créer et animer un **serveur Discord** pour le groupe d'utilisateurs DV recrutés via l'APHVE | E | Serveur créé avec canaux accessibles; >= 5 membres DV actifs |
| R-62 | Le groupe d'utilisateurs DV doit pouvoir **donner du feedback continu** tout au long du projet (pas seulement aux tests finaux) | E | >= 3 consultations documentées avec le groupe (questions, sondages, retours) sur la durée du projet |
| R-63 | L'équipe doit **recruter activement** le groupe de testeurs en collaboration avec l'APHVE | E | Processus de recrutement documenté; >= 5 personnes DV inscrites |
| R-64 | Les tests utilisateurs formels doivent être réalisés avec **protocole approuvé par le CER** | E | Lettre CER + rapport de test documenté |

---

## 7. Requis de Gestion et Académiques

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-65 | Budget total prototype <= 500$ CAD | E | Rapport de dépenses <= 500$ |
| R-66 | Coût de production unitaire cible < 100$ CAD | I | BOM de production estimé et documenté |
| R-67 | Code et fichiers de conception publiés sous licence open-source | E | Dépôt GitHub public avec fichier LICENSE |
| R-68 | Livrables académiques PMC : MIP (S6), RPC1 (S6), RPC2 (S7), RLP (S8), RAE (S6/S7/S8) | E | Documents déposés aux dates requises |
| R-69 | Démonstration fonctionnelle à l'Expo MégaGÉNIALE (S8) | E | Prototype jouable devant le public |

---

## Résumé

| Priorité | Nombre |
|----------|--------|
| **E** (Essentiel) | 48 |
| **I** (Important) | 8 |
| **S** (Souhaitable) | 3 |
| **Total** | **59** |

---

*Document vivant — à réviser aux points de synchronisation et après chaque coaching.*
