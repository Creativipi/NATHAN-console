# Requis — Projet NATHAN Console v2.0

**Date :** 2026-05-28
**Session :** PMC660 (S6, E2026)

> Ce fichier regroupe les **requis haut niveau** du projet.
> Les requis définissent **ce que** le système doit accomplir, pas **comment** (pas de choix de composants).
> Voir `BESOINS.md` pour les besoins en amont, `TACHES.md` pour les tâches détaillées.

---

## Légende

| Priorité | Description |
|----------|-------------|
| **E** | Essentiel : MVP, doit être livré |
| **I** | Important : attendu mais non bloquant |
| **S** | Souhaitable : si le temps le permet |

---

## 1. Requis fonctionnels — Expérience utilisateur

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-01 | **Jeu sans retour visuel** : le joueur peut jouer à un jeu complet uniquement par le son et le toucher | E | 1 personne non-voyante complète une session de 15 min sans assistance |
| R-02 | **Localisation sonore 3D** : le joueur localise la direction d'un son dans l'espace grâce à l'audio binaural au casque | E | 3/3 testeurs localisent une source sonore avec une erreur < 30° |
| R-03 | **Feedback haptique directionnel** : le joueur sent la direction d'un contact physique (bâton, mur) | E | Un testeur identifie la direction (gauche/centre/droite) dans 4/5 cas |
| R-04 | **Navigation inter-pièces** : le joueur se repère entre les pièces grâce aux signatures musicales des zones adjacentes | E | Un joueur aux yeux bandés identifie >= 3 pièces par leur son depuis le couloir |
| R-05 | **Bâton d'aveugle virtuel** : le joueur détecte les obstacles avec un retour sonore et haptique selon la surface touchée | E | Le joueur distingue >= 3 types de surfaces par le son et le toucher |
| R-06 | **Apprentissage rapide** : un nouveau joueur comprend les contrôles de base en < 5 min grâce à un tutoriel audio intégré | E | 2 nouveaux joueurs naviguent de façon autonome en < 5 min |
| R-07 | **Mini-jeux tiers** : le joueur peut programmer et jouer à des mini-jeux créés par des tiers (MicroPython) | I | Un mini-jeu écrit par un tiers fonctionne sans modification du firmware |

---

## 2. Requis fonctionnels — Contenu de jeu

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-08 | **Zones jouables** : le jeu comporte >= 4 zones distinctes jouables (sur 6 planifiées) | E | 4 zones avec ambiance propre et >= 2 interactions chacune |
| R-09 | **Identité sonore par zone** : chaque zone a une ambiance sonore unique et reconnaissable | E | 3/3 testeurs identifient au moins 3 zones par leur son seul |
| R-10 | **Instrument jouable** : le jeu inclut au moins un instrument de musique jouable (guitare ou batterie) | I | Un joueur produit une séquence musicale reconnaissable |
| R-11 | **Mini-jeux d'exemple** : le système inclut >= 2 mini-jeux démontrant l'API MicroPython | I | 2 mini-jeux jouables depuis le hub de la Salle de Mini-Jeux |
| R-12 | **Banque de sons** : la banque contient >= 50 sons uniques (ambiances, effets, voix, musiques) | E | Inventaire documenté >= 50 fichiers WAV |
| R-13 | **Narration audio** : le jeu inclut une narration pour le tutoriel et les instructions | E | >= 10 clips de narration intégrés |

---

## 3. Requis de performance

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-14 | **Sources spatiales simultanées** : le système supporte >= 4 sources sonores spatiales sans artefact audible | E | 4 sources jouent en simultané pendant 1 min sans coupure ni distorsion |
| R-15 | **Latence audio** : la latence bout-en-bout (action → son au casque) est < 50 ms | E | Mesure instrumentée < 50 ms |
| R-16 | **Latence haptique** : la latence (action → vibration moteur) est < 100 ms | E | Mesure instrumentée < 100 ms |
| R-17 | **Fréquence de polling** : le polling des entrées est >= 100 Hz | E | Intervalle moyen entre lectures < 10 ms |
| R-18 | **Stabilité** : aucun crash ni fuite mémoire pendant 1h de jeu continu | E | Test de stabilité de 1h sans crash; heap libre stable |
| R-19 | **Temps de démarrage** : le boot prend < 5 secondes du power-on au menu principal | I | Mesure au chronomètre < 5 s |

---

## 4. Requis hardware (caractéristiques, sans choix de composants)

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-20 | **Joysticks** : 2 joysticks analogiques double-axe avec bouton intégré | E | 4 axes analogiques + 2 clicks lus par le firmware |
| R-21 | **Boutons** : >= 7 boutons numériques (A, B, C, L1, R1, Start, Select) | E | Chaque bouton détecté sans ambiguïté par le firmware |
| R-22 | **Moteurs haptiques** : >= 5 moteurs de vibration en arc, contrôlables individuellement en intensité | E | 5 moteurs vibrent indépendamment à des intensités différentes |
| R-23 | **Sortie audio** : stéréo via jack 3.5mm, qualité suffisante pour le HRTF binaural (>= 44.1 kHz, >= 16 bits, SNR > 80 dB) | E | Son spatial perceptible au casque; pas de bruit de fond gênant |
| R-24 | **Alimentation** : batterie rechargeable via USB-C | E | Autonomie >= 4h en usage typique; charge par USB-C |
| R-25 | **Stockage amovible** : assets et mini-jeux sur support amovible (carte SD ou équivalent) | E | Lecture de fichiers WAV depuis le stockage |
| R-26 | **Communication PC** : la console communique avec un PC via USB (port série virtuel) | E | Transfert bidirectionnel fonctionnel via USB |
| R-27 | **Ergonomie** : la console tient dans les mains d'un adulte (largeur <= 16 cm) | E | 3/3 testeurs confortables après 30 min |
| R-28 | **Contrôles au toucher** : tous les contrôles sont différentiables au toucher sans retour visuel | E | 5/5 identifications correctes par un testeur les yeux bandés |
| R-29 | **Fabrication 3D** : le boîtier est fabricable par impression 3D FDM | E | Impression réussie, assemblage sans outil spécialisé |
| R-30 | **Choix du MCU mesuré** : le microcontrôleur est choisi selon les besoins réels mesurés (CPU, RAM, I/O) après le développement PC | E | Document de justification basé sur le benchmark du jeu sur PC |

---

## 5. Requis d'architecture logicielle

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-31 | **Game engine agnostique** : le moteur est indépendant du matériel via des interfaces abstraites (entrées, son, haptique, stockage) | E | Le même code de jeu fonctionne avec une manette PS4/Xbox sur PC ET avec la manette finale |
| R-32 | **Deux implémentations par interface** : chaque interface a >= 2 implémentations (dev PC + matériel final) | E | Swap d'implémentation sans recompilation du game engine |
| R-33 | **Interfaces gelées tôt** : les interfaces sont définies et gelées avant le développement (Phase 0) | E | Fichiers de contrat signés par les équipes concernées |
| R-34 | **Sandbox mini-jeux** : les scripts MicroPython s'exécutent dans un sandbox isolé | E | Script exécuté; tentative d'accès hors sandbox bloquée |
| R-35 | **API `nathan.*`** : expose audio (play, stop, set_ambient), haptic (pulse, sweep), input (joystick, button), game (score, end) | E | Chaque fonction appelable depuis un script MicroPython |

---

## 6. Requis de l'IDE de programmation

L'IDE fait partie intégrante du projet. Architecture en 5 couches : UX accessible → Édition → Assistant IA → Déploiement → Matériel.

### 6.1 Couche UX accessible

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-36 | **TTS français** : l'IDE vocalise tout feedback, diagnostic et navigation en français | E | Chaque action de l'éditeur produit une annonce vocale pertinente en fr-FR |
| R-37 | **Lecteur d'écran et clavier** : compatible ARIA et navigable entièrement au clavier | E | Un utilisateur DV écrit du code et transfère un fichier sans aide visuelle |
| R-38 | **Shell vocal (STT)** : l'utilisateur peut dicter des commandes ou du code | I | Commande vocale "ouvrir fichier main.py" exécutée correctement |
| R-39 | **Mode d'affichage accessible** : grand texte, contraste élevé | I | Police et contraste ajustables; lisible à 200% de zoom |

### 6.2 Couche édition

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-40 | **Coloration MicroPython** : coloration syntaxique avec reconnaissance des fonctions `nathan.*` | E | Mots-clés Python colorés; `nathan.audio.play` reconnu |
| R-41 | **Explorateur de fichiers** : créer, supprimer et organiser les projets de mini-jeux | E | Arborescence navigable; opérations CRUD fonctionnelles |
| R-42 | **Linter vocal** : détecte les erreurs et les annonce via TTS | E | Erreur de syntaxe détectée et annoncée en < 2 secondes |
| R-43 | **Bibliothèque de modèles** : snippets/templates de mini-jeux pour débutants | I | >= 3 templates disponibles (réaction, quiz sonore, exploration) |
| R-44 | **Raccourcis clavier** : raccourcis standards (Ctrl+S, Ctrl+F, Ctrl+Shift+P) | E | Raccourcis fonctionnels et annoncés au lecteur d'écran |
| R-45 | **Terminal intégré** : exécution de commandes avec streaming de sortie | E | Commandes exécutées avec sortie en continu |
| R-46 | **Recherche et remplacement** : dans les fichiers | E | Recherche case-insensitive, remplacement global fonctionnel |

### 6.3 Couche assistant IA

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-47 | **Assistant IA** : répond aux questions sur l'API `nathan.*` et aide à écrire du code | I | L'utilisateur demande "comment jouer un son à droite?" et reçoit un snippet fonctionnel |
| R-48 | **Application de modifications par l'IA** : insertion/correction de code avec validation avant application | S | Suggestion appliquée au code après confirmation de l'utilisateur |

### 6.4 Couche déploiement

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-49 | **Transfert USB** : transfert de fichiers .py vers la console via USB CDC | E | Fichier .py de 5 KB transféré en < 10 s; intégrité vérifiée |
| R-50 | **Logs temps réel** : affichage des logs de la console via USB | E | Logs visibles dans le terminal pendant l'exécution d'un mini-jeu |
| R-51 | **Gestionnaire de mini-jeux** : liste des jeux sur la carte SD de la console (commande LIST) | E | Liste récupérée et affichée; suppression possible (DELETE) |
| R-52 | **Cycle de développement rapide** : écrire → transférer → jouer en < 1 min | E | Temps mesuré du save au lancement sur console < 60 s |

### 6.5 Couche visualisation (optionnel)

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-53 | **Visualisateur de scène 2D** : placement des sources sonores (coordonnées x/y/z) | S | Drag & drop des entités; preview visuel des positions |
| R-54 | **Simulation HRTF** : prévisualisation du son spatial via WebAudio avant envoi | S | Son spatialisé audible au casque depuis l'IDE |

---

## 7. Requis communauté et utilisateurs DV

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-55 | **Serveur Discord** : créer et animer un serveur pour le groupe d'utilisateurs DV | E | Serveur avec canaux accessibles; >= 5 membres DV actifs |
| R-56 | **Feedback continu** : le groupe DV donne du feedback tout au long du projet | E | >= 3 consultations documentées sur la durée du projet |
| R-57 | **Recrutement actif** : l'équipe recrute les testeurs en collaboration avec l'APHVE | E | Processus documenté; >= 5 personnes DV inscrites |
| R-58 | **Tests CER** : les tests formels suivent un protocole approuvé par le CER | E | Lettre CER + rapport de test documenté |

---

## 8. Requis de gestion et académiques

| ID | Requis | Priorité | Critère de validation |
|----|--------|----------|-----------------------|
| R-59 | **Budget** : budget total prototype <= 500$ CAD | E | Rapport de dépenses <= 500$ |
| R-60 | **Coût de production** : cible < 100$ CAD par unité | I | BOM de production estimé et documenté |
| R-61 | **Open-source** : code et fichiers de conception publiés sous licence libre | E | Dépôt GitHub public avec fichier LICENSE |
| R-62 | **Livrables PMC** : MIP (S6), RPC1 (S6), RPC2 (S7), RLP (S8), RAE (S6/S7/S8) | E | Documents déposés aux dates requises |
| R-63 | **Expo MégaGÉNIALE** : démonstration fonctionnelle (S8) | E | Prototype jouable devant le public |

---

## Résumé

| Priorité | Nombre |
|----------|--------|
| **E** (Essentiel) | 51 |
| **I** (Important) | 9 |
| **S** (Souhaitable) | 3 |
| **Total** | **63** |

---

*Document vivant — à réviser aux points de synchronisation et après chaque coaching.*
