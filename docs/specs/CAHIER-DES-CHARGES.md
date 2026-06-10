# Cahier des Charges — Projet NATHAN Console (v2.0)

**Projet :** NATHAN — Narrative Audio Terminal for Humans with Alternative Navigation
**Version du document :** 2.0
**Date :** 2026-03-05
**Auteur :** Arthur Olivier Fortin
**Statut :** Phase de conception majeure

---

## Table des matières

1. [Contexte et vision du projet](#1-contexte-et-vision-du-projet)
2. [État actuel du projet (v1.0)](#2-état-actuel-du-projet-v10) — *inclut jeu existant GlassBreaker et IDE*
3. [Objectifs du projet majeur (v2.0)](#3-objectifs-du-projet-majeur-v20)
4. [Public cible](#4-public-cible)
5. [Équipes, rôles et stratégie de développement parallèle](#5-équipes-rôles-et-stratégie-de-développement-parallèle)
6. [Spécifications hardware (v2.0)](#6-spécifications-hardware-v20)
7. [Spécifications firmware et logiciel bas niveau](#7-spécifications-firmware-et-logiciel-bas-niveau)
8. [Spécifications du game engine](#8-spécifications-du-game-engine)
9. [Spécifications du premier jeu — La Maison de Nathan](#9-spécifications-du-premier-jeu--la-maison-de-nathan)
10. [Système de mini-jeux](#10-système-de-mini-jeux)
11. [Contraintes et risques techniques](#11-contraintes-et-risques-techniques)
12. [Planification par workstreams et dépendances](#12-planification-par-workstreams-et-dépendances)
13. [Budget](#13-budget)
14. [Livrables](#14-livrables)

---

## 1. Contexte et vision du projet

### 1.1 Origine

Le projet NATHAN est né en 2022 d'une collaboration entre Arthur Olivier Fortin et une personne non-voyante, musicien et passionné de synthétiseurs. L'objectif initial était de concevoir une console de jeu entièrement accessible aux personnes non-voyantes, dans laquelle le son et les sensations tactiles remplacent intégralement l'image. Le projet est réalisé en partenariat avec l'APHVE (Association des Personnes Handicapées Visuelles de l'Estrie), qui accompagne l'équipe avec un groupe d'utilisateurs non-voyants tout au long du développement.

### 1.2 Mission

Créer une console de jeu **open-source**, **abordable** et **inclusive**, où l'expérience est entièrement auditive et haptique. La console doit permettre à un utilisateur non-voyant de jouer les yeux fermés, avec une immersion complète par le son spatial 3D et le retour vibratoire directionnel.

### 1.3 Vision long terme

- Être la première console de jeu grand public dédiée aux personnes ayant une déficience visuelle.
- Permettre aux utilisateurs de **créer leurs propres mini-jeux** sans barrière technique (MicroPython).
- Constituer une **plateforme pédagogique** : initiation à la programmation pour les personnes non-voyantes.
- Rester open-source pour favoriser la contribution communautaire.

---

## 2. État actuel du projet (v1.0)

### 2.1 Ce qui est complété

| Composant | État | Détails |
|-----------|------|---------|
| Modèles 3D boîtier | ✅ Complet | 3 pièces SolidWorks (.SLDPRT, importables dans Onshape — géométrie conservée), STL générés |
| PCB KiCAD | ✅ Complet | Gerbers prêts pour fabrication |
| BOM (liste de matériaux) | ✅ Documenté | Composants sourcés |
| Documentation README | ✅ Rédigé | Histoire, vision, fonctionnalités |

### 2.2 Matériel actuel (v1.0)

| Composant | Spécification |
|-----------|---------------|
| Microcontrôleur | Raspberry Pi Pico (RP2040) |
| Boutons | 5 (3 arcade 30mm + 2 micro switches) |
| LEDs | 5 (indicateurs visuels) |
| Moteurs haptiques | 2 (moteurs Xbox rumble) |
| Audio | Jack stéréo 3.5mm |
| Stockage | Module micro SD |
| Alimentation | 3x piles AA |
| Potentiomètre | WH148 1kΩ |

### 2.3 Ce qui n'existe pas encore (côté console v2.0)

- Firmware embarqué : **non démarré** (à écrire en C/C++, MCU à déterminer)
- Game engine spatial : **non démarré**
- IDE mini-jeux (intégration NATHAN) : **en cours** (voir 2.5)

### 2.4 Jeu existant — GlassBreaker (CircuitPython, Raspberry Pi Pico)

Un jeu complet est déjà fonctionnel dans le dépôt `NATHAN-code`. Il tourne sur le **Raspberry Pi Pico** en **CircuitPython 8.x** et constitue la référence directe pour l'architecture des mini-jeux futurs.

**Dépôt :** `C:\Users\arthu\OneDrive\NATHAN\NATHAN-code` (GlassBreaker Safe CP)

#### Architecture du jeu existant

```
GlassBreaker Safe CP/
├── main.py              # Orchestre tous les managers
├── input/buttons.py     # ButtonManager — lecture GPIO
├── output/audio.py      # AudioManager — PWM 22050Hz mono
├── output/leds.py       # LEDManager — 7 LEDs
├── output/motors.py     # MotorManager — 2 moteurs rumble
├── game/logic.py        # GameLogic + GameState
├── game/menu.py         # MenuSystem + MenuExtension
├── utils/memory.py      # MemoryManager — scores SD card
├── sounds/              # Fichiers WAV sur carte SD
└── lib/                 # Bibliothèques Adafruit CircuitPython
```

#### Mécaniques de jeu

- **Type :** Jeu de réaction bouton (audio-first)
- **5 modes :** Arcade (sons), Voice (voix), Reverse, Light (visuel), Megamix (aléatoire)
- **Difficulté progressive :** `timeout = max(0.5, 1.0 - (0.001 × score))`
- **Jalons :** Annonces audio à 25, 50, 75, 100 points
- **Persistance :** High scores par mode sur carte SD (FAT32)

#### Ce que cela implique pour v2.0

| Aspect | GlassBreaker (v1) | NATHAN v2.0 |
|--------|-------------------|-------------|
| Langage jeu | CircuitPython | C/C++ (game engine) |
| Langage mini-jeux | CircuitPython | MicroPython (quasi-identique) |
| Audio | PWM mono 22050 Hz | I2S stéréo binaural HRTF |
| Entrées | 5 boutons | 2 joysticks + boutons |
| Haptique | 2 moteurs (on/off) | 5 moteurs arc (PWM intensité) |
| Pattern module | Manager + MenuExtension | HAL + API game engine |

> **Note de compatibilité :** CircuitPython et MicroPython partagent ~95% de leur syntaxe. Les mini-jeux écrits pour v2.0 s'inspireront directement des modules GlassBreaker. Le `MenuExtension` pattern existant (classe avec `run()` et métadonnées) devient le modèle du format mini-jeu MicroPython.

#### Pattern MenuExtension (référence pour le format mini-jeu)

```python
# Modèle inspiré de game/menu.py (GlassBreaker)
class MonMiniJeu:
    META = {
        "title": "Mon Mini-Jeu",
        "author": "Arthur",
        "description": "Description audio du jeu"
    }

    def __init__(self, managers):
        self.audio = managers["audio"]
        self.buttons = managers["buttons"]
        self.motors = managers["motors"]

    def run(self):
        """Boucle principale — retourne True si succès, False si échec"""
        pass
```

### 2.5 IDE de programmation (Electron + React + TypeScript)

L'IDE fait partie intégrante du projet NATHAN. C'est l'application desktop qui permet aux utilisateurs (y compris non-voyants) de programmer et de transférer des mini-jeux sur la console.

**Stack :** Electron 28 + React 18 + TypeScript 5.3 + Vite 5

#### Ce qui est déjà implémenté dans l'IDE

| Fonctionnalité | État | Détail |
|----------------|------|--------|
| Éditeur de code multi-onglets | ✅ Complet | Textarea + coloration syntaxique custom |
| Explorateur de fichiers (sidebar) | ✅ Complet | Arborescence avec create/delete |
| Recherche & remplacement | ✅ Complet | Case-insensitive, replace-all |
| Terminal intégré | ✅ Complet | Exécution de commandes shell avec streaming |
| Accessibilité vocale (TTS) | ✅ Complet | Web Speech API, **français par défaut (fr-FR)** |
| Screen reader (ARIA live) | ✅ Complet | Annonces assistives |
| Raccourcis clavier | ✅ Complet | Ctrl+F, Ctrl+S, Ctrl+Shift+P, etc. |
| Palette de commandes | ✅ Complet | Ctrl+Shift+P |
| Maestro backend (IA, C# .NET) | ✅ Intégré | Sidecar HTTP, agent "Jarvis" (ask) |
| Coloration syntaxique TypeScript/JS | ✅ Complet | Tokenizer regex custom |

#### Ce qui reste à développer dans l'IDE pour NATHAN

| Fonctionnalité | Priorité | Notes |
|----------------|----------|-------|
| Coloration syntaxique MicroPython | Critique | Remplacer/compléter le tokenizer TS |
| Auto-complétion API `nathan.*` | Critique | Nécessite Monaco Editor ou extension |
| Communication USB série (console) | Critique | Web Serial API ou `serialport` npm |
| Upload de `.py` vers carte SD via USB | Critique | Dépend de la communication USB |
| Visualisateur de scène 2D (sons spatiaux) | Haute | Drag & drop, coordonnées x/y/z |
| Simulation audio WebAudio HRTF | Moyenne | Aperçu avant envoi sur console |
| Gestionnaire de mini-jeux (liste SD) | Haute | Lecture liste depuis console |
| Mode d'affichage accessible (grand texte, contraste) | Haute | Accessibilité DV |

> L'IDE est développé dans le cadre de ce projet sous `ide/`. L'intégration avec la console NATHAN se fait via le protocole USB CDC défini dans la section 7.4.

---

## 3. Objectifs du projet majeur (v2.0)

Le projet v2.0 constitue une **refonte complète** articulée autour de quatre axes :

### Axe 1 — Refonte hardware
Remplacer le Raspberry Pi Pico par un **microcontrôleur adapté** (choisi après benchmark), ajouter **2 joysticks analogiques**, **5 moteurs de vibration en arc**, et migrer vers une **batterie LiPo USB-C rechargeable**.

### Axe 2 — Game engine embarqué
Développer un moteur de jeu en **C/C++** tournant sur le microcontrôleur choisi, avec un système de placement 2D+hauteur permettant le calcul automatique d'**audio spatial binaural (HRTF)**.

### Axe 3 — Premier jeu : La Maison de Nathan
Développer le jeu de démonstration de la console : un jeu entièrement auditif et haptique mettant en scène Nathan, un aveugle, dans sa maison.

### Axe 4 — Système de mini-jeux
Permettre aux utilisateurs de programmer et jouer à des mini-jeux écrits en **MicroPython** via l'IDE du projet.

---

## 4. Public cible

### 4.1 Utilisateurs finaux (joueurs)

- **Primaire :** Personnes non-voyantes ou malvoyantes, tous âges
- **Secondaire :** Personnes voyantes souhaitant une expérience sensorielle immersive

### 4.2 Utilisateurs créateurs (programmeurs de mini-jeux)

- **Primaire :** Personnes non-voyantes apprenant la programmation
- **Secondaire :** Développeurs souhaitant créer du contenu pour la plateforme
- **Niveau requis :** Débutant (MicroPython simplifié, interface graphique)

### 4.3 Contraintes d'accessibilité prioritaires

- Toute interface de jeu doit fonctionner **sans retour visuel**
- Tous les menus et interactions doivent être **entièrement navigables au son**
- Le boîtier doit être **ergonomique** et les contrôles **facilement différenciables au toucher**

---

## 5. Équipes, rôles et stratégie de développement parallèle

### 5.1 Composition des équipes

| Équipe | Code | Profil | Responsabilité |
|--------|------|--------|----------------|
| **Électrique** | ELEC | Génie électrique | Schéma, PCB, boîtier, soudure, validation matérielle |
| **Engine** | ENG | Génie informatique | Game engine, scènes, collisions, bâton, MicroPython, HAL |
| **Audio spatial** | AUD | Génie informatique (spécialisé signal/audio) | Pipeline HRTF, mix binaural, évaluation software vs DSP |
| **Jeu / Contenu** | JEU | Génie informatique / design | Design des pièces, mécaniques de jeu, banque de sons, narration |

### 5.2 Principe fondamental : zéro temps d'attente entre équipes

Le plan de développement est conçu pour que **aucune équipe ne soit bloquée** par une autre. Cela repose sur trois stratégies :

#### Stratégie A — Manette de substitution (découple ELEC ↔ ENG/JEU)

Dès le **jour 1** du projet, les équipes logicielles utilisent une **manette USB grand public** (type DualShock 4 / Xbox One, ~30$ CAD) pour développer et tester toute la logique de jeu.

Un module **InputMapper** abstrait complètement le matériel :

```
┌───────────────────────────────────────────────┐
│                 Game Engine                     │
│                                                 │
│    scene.update(input, dt)                      │
│         │                                       │
│    ┌────▼─────┐                                 │
│    │InputMapper│  ← Interface abstraite          │
│    └────┬─────┘                                 │
│         │                                       │
│    ┌────┴──────────────┬──────────────────┐     │
│    │                   │                  │     │
│  GamepadMapper    NathanMapper       DebugMapper│
│  (DualShock/Xbox) (manette réelle)   (clavier)  │
│  PHASE 1-2        PHASE 3+           DEBUG      │
└───────────────────────────────────────────────┘
```

| Implémentation | Utilisée par | Phase | Description |
|----------------|-------------|-------|-------------|
| `GamepadMapper` | ENG, JEU, AUD | Phases 1-2 | Manette USB standard. Joystick L/R mappés directement, vibration mono simulée. |
| `DebugMapper` | ENG | Toutes | Clavier + souris pour tests rapides sans manette |
| `NathanMapper` | ENG, ELEC | Phase 3+ | Manette NATHAN réelle. Joysticks ADC, 5 moteurs PWM, boutons GPIO. |

**Mapping de substitution (GamepadMapper):**

| Contrôle NATHAN | Substitut DualShock/Xbox |
|-----------------|--------------------------|
| Joystick gauche | Joystick gauche (identique) |
| Joystick droite | Joystick droite (identique) |
| Boutons A/B/C | ×/○/△ (ou A/B/Y) |
| Gâchettes L1/R1 | L1/R1 (identique) |
| 5 moteurs arc | Vibration unique du gamepad (intensité = moteur central) |
| Start/Select | Start/Select (identique) |

**Pour le haptique**, le gamepad n'a qu'un moteur. Le GamepadMapper simule les 5 moteurs en arc par :
- Vibration unique pour tout contact de bâton
- Logs console indiquant quel moteur NATHAN serait activé (pour debug)
- La validation réelle des 5 moteurs se fait à la Phase 3 (intégration)

#### Stratégie B — Développement audio PC-first (découple AUD ↔ ELEC)

Le développeur audio ne touche **jamais** au microcontrôleur avant la Phase 3. Tout le développement HRTF se fait sur PC :

```
Phase 1 : Recherche + prototypage PC (C/C++ + miniaudio ou libsoundio)
Phase 2 : Module audio spatial fonctionnel sur PC, testé au casque
Phase 3 : Portage vers le MCU choisi, benchmark CPU/latence
Phase 3b: Décision : software pur OU ajout DSP matériel externe
```

L'interface entre le game engine et le module audio est un **contrat** défini dès la Phase 0 (voir 5.3). Tant que le contrat est respecté, les implémentations PC et ESP32 sont interchangeables.

#### Stratégie C — Contrats d'interface (découple toutes les équipes)

Avant tout développement, les équipes définissent ensemble les **interfaces contractuelles** entre les modules. Chaque interface a une **implémentation stub** qui permet de tester sans dépendance.

### 5.3 Contrats d'interface (Phase 0 — à définir en priorité)

Les 5 contrats suivants sont les **premiers livrables du projet**. Ils doivent être définis et validés par toutes les équipes avant le début du développement.

#### Contrat 1 — InputMapper (ENG ↔ ELEC)

```c
// Abstraction des entrées : toute source d'input implémente cette interface
typedef struct {
    float left_x, left_y;     // Joystick gauche (-1.0 à 1.0)
    float right_x, right_y;   // Joystick droite (-1.0 à 1.0)
    bool buttons[9];           // A, B, C, L1, R1, L2, R2, Start, Select
    bool left_click;           // Joystick gauche appuyé
    bool right_click;          // Joystick droite appuyé
} InputState;

void input_mapper_init(void);
InputState input_mapper_read(void);
```

#### Contrat 2 — SpatialAudioEngine (ENG ↔ AUD)

```c
// Abstraction audio : le game engine place des sons, l'implémentation les rend binauraux
typedef int SoundHandle;

void spatial_audio_init(int sample_rate, int max_sources);
void spatial_audio_shutdown(void);

SoundHandle spatial_audio_play(const char* wav_path, float x, float y, float z, bool loop);
void spatial_audio_stop(SoundHandle h);
void spatial_audio_set_position(SoundHandle h, float x, float y, float z);
void spatial_audio_set_volume(SoundHandle h, float vol);

void spatial_audio_update_listener(float px, float py, float orientation_deg);
void spatial_audio_render(int16_t* stereo_buffer, int frame_count);

// Ambiance (non spatialisé, stéréo direct)
void spatial_audio_play_ambient(const char* wav_path, float volume);
void spatial_audio_stop_ambient(void);
```

**Implémentations prévues :**

| Implémentation | Utilisée par | Phase | Backend |
|----------------|-------------|-------|---------|
| `StubAudio` | ENG | Phase 1 | Pas de son, logs console uniquement |
| `PCAudio` | AUD, JEU | Phase 1-2 | `miniaudio` + HRTF sur PC |
| `EmbeddedAudio` | Tous | Phase 3+ | I2S + DAC + HRTF embarqué (MCU choisi après benchmark) |

#### Contrat 3 — HapticEngine (ENG ↔ ELEC)

```c
// Abstraction haptique : 5 moteurs logiques en arc
// Motor IDs : 0=extrême gauche, 1=gauche, 2=centre, 3=droite, 4=extrême droite

void haptic_init(void);
void haptic_pulse(int motor_id, float intensity, int duration_ms);
  // motor_id: 0-4, intensity: 0.0-1.0
void haptic_sweep(float direction, float intensity);
  // direction: -1.0 (gauche) → 1.0 (droite)
void haptic_pattern(const char* pattern_name);
  // Patterns prédéfinis: "cane_wall", "cane_floor", "cane_sweep", "hit", "strum"
void haptic_stop_all(void);
```

**Implémentations prévues :**

| Implémentation | Phase | Comportement |
|----------------|-------|--------------|
| `StubHaptic` | Phase 1 | Logs console uniquement |
| `GamepadHaptic` | Phase 1-2 | Vibration unique du gamepad USB |
| `NathanHaptic` | Phase 3+ | 5 moteurs PWM réels via GPIO du MCU choisi |

#### Contrat 4 — StorageProvider (ENG)

```c
void storage_init(void);
bool storage_file_exists(const char* path);
int  storage_read_file(const char* path, uint8_t* buffer, int max_size);
int  storage_write_file(const char* path, const uint8_t* data, int size);
char** storage_list_dir(const char* path, int* count);
```

#### Contrat 5 — MiniGameRunner (ENG)

```c
typedef struct {
    char title[64];
    char author[32];
    char description[128];
} MiniGameMeta;

bool minigame_load(const char* dir_path);
MiniGameMeta minigame_get_meta(void);
bool minigame_setup(void);
bool minigame_loop(void);  // retourne false quand le mini-jeu se termine
void minigame_unload(void);
```

### 5.4 Matrice de responsabilité (RACI)

| Livrable | ELEC | ENG | AUD | JEU |
|----------|------|-----|-----|-----|
| Schéma / PCB (MCU choisi) | **R** | C | — | — |
| Boîtier v2.0 (Onshape) | **R** | C | — | — |
| Soudure et validation matérielle | **R** | — | — | — |
| Contrats d'interface (Phase 0) | C | **R** | C | I |
| InputMapper (toutes implémentations) | C | **R** | — | — |
| Game engine (scènes, collisions, bâton) | — | **R** | — | I |
| Pipeline HRTF (recherche + implémentation) | — | I | **R** | — |
| Portage audio embarqué | C | I | **R** | — |
| Intégration MicroPython | — | **R** | — | I |
| Design des pièces du jeu | — | I | I | **R** |
| Banque de sons et musiques | — | — | C | **R** |
| Narration audio (tutoriel, voix personnage) | — | — | — | **R** |
| Mécaniques guitare/batterie | — | C | C | **R** |
| Tests d'intégration finale | C | **R** | C | C |
| Tests utilisateur (groupe DV via APHVE) | I | C | C | **R** |
| IDE de programmation | — | **R** | — | C |

> **R** = Responsable, **C** = Consulté, **I** = Informé

---

## 6. Spécifications hardware (v2.0)

### 6.1 Microcontrôleur — À déterminer

Le microcontrôleur sera choisi **après le benchmark du jeu sur PC**, qui mesurera les besoins réels en CPU, RAM et I/O. Cette décision est le jalon clé du chemin critique (voir `TACHES.md`).

**Besoins minimaux identifiés :**

| Paramètre | Besoin minimum | Justification |
|-----------|----------------|---------------|
| CPU | >= 2 cœurs, >= 160 MHz | Un cœur dédié au rendu audio HRTF, un à la logique de jeu |
| RAM | >= 4 MB (PSRAM) | Tables HRTF (~1 MB) + buffers audio + game engine + MicroPython |
| Flash | >= 8 MB | Firmware + interpréteur MicroPython |
| I2S | >= 1 interface stéréo | Connexion au DAC audio externe |
| ADC | >= 4 canaux, >= 10 bits | 2 joysticks × 2 axes |
| PWM | >= 5 canaux | 5 moteurs haptiques individuels |
| USB | USB OTG ou CDC natif | Communication avec l'IDE (port série virtuel) |
| SPI | >= 1 | Lecteur carte micro SD |
| GPIO | >= 9 numériques | 7 boutons + 2 clicks joystick |

**Candidats préliminaires** (analyse détaillée dans le MIP) :

| MCU | CPU | RAM | I2S | USB | Prix (~) |
|-----|-----|-----|-----|-----|----------|
| ESP32-S3 | 2× 240 MHz | 8 MB PSRAM | 2× | USB OTG natif | ~5$ |
| RP2350 | 2× 150 MHz | 520 KB + ext | 2× | USB 1.1 | ~1$ |
| STM32H7 | 1× 480 MHz | 1 MB + ext | 2× | USB OTG | ~10$ |

> Le choix final sera documenté dans un **rapport de justification quantitatif** basé sur le benchmark PC (voir `TACHES.md`, jalon "Choix du MCU").

### 6.2 Système audio

**Le DAC audio sera choisi en même temps que le MCU.** Les besoins sont :

| Paramètre | Besoin |
|-----------|--------|
| Interface | I2S (compatible avec le MCU choisi) |
| Résolution | >= 16 bits, >= 44.1 kHz |
| SNR | >= 80 dB |
| Sortie | Jack stéréo 3.5mm (casque uniquement) |

**Note importante :** Le jeu est conçu pour une écoute au **casque stéréo uniquement**. Le son spatial binaural (HRTF) requiert un casque pour l'effet 3D.

#### Pipeline audio spatial

```
Positions 3D des sons (via SpatialAudioEngine)
        ↓
Calcul azimut/élévation/distance
        ↓
Application HRTF (lookup table, MIT KEMAR ou équivalent open-source)
        ↓
Mix audio binaural (canal L + canal R)
        ↓
Buffer DMA → I2S → DAC → Jack 3.5mm
```

#### Format audio des assets

- Samples : **WAV 16 bits, 44.1 kHz, mono** (le moteur applique la spatialisation)
- Musiques d'ambiance : **WAV 16 bits, 44.1 kHz, stéréo** (non spatiales, lecture directe)
- Stockage sur carte micro SD

### 6.3 Système haptique — 5 moteurs en arc

#### Topologie

Les 5 moteurs vibrants sont disposés en arc de cercle dans le corps de la manette :

```
Position physique :  [M0]  [M1]  [M2]  [M3]  [M4]
Direction simulée :  ←←   ←     ↑     →     →→
```

#### Spécifications moteurs

| Paramètre | Valeur |
|-----------|--------|
| Type | Moteur à vibration excentrique (ERM) ou LRA |
| Tension nominale | 3V |
| Contrôle | PWM individuel par canal (intensité variable) |
| Driver | MOSFET N-CH par moteur (ex: 2N7002) OU DRV2605L (recommandé) |
| Fréquence PWM | 1 kHz minimum |

#### Cas d'usage

| Interaction | Moteurs activés | Pattern |
|-------------|-----------------|---------|
| Bâton touche mur à gauche | M0, M1 | Impulsion courte, forte |
| Bâton touche sol | M0 à M4 (tous, faible) | Vibration continue faible |
| Bâton touche obstacle à droite | M3, M4 | Impulsion courte, forte |
| Coup de bâton en combat | M0 à M4 (séquence) | Sweep directionnel |
| Guitare — strumming | M2, M3 | Vibration rhythmique |
| Drum — impact | M correspondant à la zone | Impulsion forte courte |

### 6.4 Entrées utilisateur

#### Joysticks

| Paramètre | Valeur |
|-----------|--------|
| Quantité | 2 (gauche + droite) |
| Type | Joystick analogique double axe (modèle Xbox/PS) |
| Résolution ADC | 12 bits (0–4095) |
| Canaux requis | 4 entrées ADC (X/Y par joystick) |
| Bouton intégré | Oui (appui joystick = bouton numérique) |

#### Boutons

| Bouton | Type | Usage principal |
|--------|------|-----------------|
| A (×) | Arcade 30mm | Action principale |
| B (○) | Arcade 30mm | Action secondaire |
| C (△) | Arcade 30mm | Action tertiaire / menu |
| L1 | Micro switch | Gâchette gauche |
| R1 | Micro switch | Gâchette droite |
| Start | Bouton tactile | Menu / pause |
| Select | Bouton tactile | Retour / annuler |

### 6.5 Alimentation

| Paramètre | Besoin |
|-----------|--------|
| Batterie | LiPo 1S (3.7V) — capacité min. 2000 mAh |
| Connecteur de charge | USB-C |
| Protection | Surcharge, décharge profonde, court-circuit |
| Régulateur | LDO 3.3V pour le MCU |
| Autonomie cible | >= 4 heures en usage typique |

> L'estimation de consommation détaillée sera calculée une fois le MCU et le DAC choisis.

### 6.6 Connectivité

| Interface | Usage |
|-----------|-------|
| USB-C | Charge + connexion à l'IDE NATHAN (USB CDC) |
| Wi-Fi 2.4 GHz | Mise à jour OTA (optionnel v2.0) |
| Micro SD | Stockage assets audio, jeux, mini-jeux |

### 6.7 Boîtier (refonte ergonomique)

#### Contraintes de refonte

- Intégrer 2 joysticks (gauche + droite)
- Intégrer 5 moteurs en arc dans les poignées
- Passer à une batterie LiPo + port USB-C
- Conserver l'inspiration Xbox pour l'ergonomie
- Rester fabricable par impression 3D FDM
- **Dimensions maximales :** Tenir dans une main adulte (largeur ~16 cm)

#### Fichiers à mettre à jour

- `CAD_Files/Console/NATHAN-console-asm.SLDASM` — refonte complète
- `CAD_Files/Console/parts/*.SLDPRT` — toutes les pièces
- `3D Print Models/*.STL` — regenerer depuis les nouveaux SLDPRT
- `CAD_Files/PCB/` — nouveau schéma et PCB pour le MCU choisi

---

## 7. Spécifications firmware et logiciel bas niveau

### 7.1 Environnement de développement

| Paramètre | Valeur |
|-----------|--------|
| SDK | Dépend du MCU choisi (ex: ESP-IDF, Pico SDK, STM32 HAL) |
| Langage principal | C / C++17 |
| Build system | CMake |
| Tests | Unity test framework (embarqué) |

> Le SDK et les outils de débogage seront déterminés après le choix du MCU.

### 7.2 Architecture firmware

```
┌─────────────────────────────────────────────────────────┐
│                      APPLICATION                         │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────────┐  │
│  │  Game Engine │  │ MicroPython  │  │   USB Bridge   │  │
│  │   (C/C++)   │  │  Sandbox     │  │   (CDC)        │  │
│  └──────┬──────┘  └──────┬───────┘  └───────┬────────┘  │
│         └────────────────┴──────────────────┘            │
│  ┌─────────────────────────────────────────────────────┐ │
│  │         Contrats d'interface (section 5.3)          │ │
│  │  InputMapper | SpatialAudioEngine | HapticEngine    │ │
│  └─────────────────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────────────────┐ │
│  │              Hardware Abstraction Layer (HAL)        │ │
│  │  NathanMapper | ESP32Audio | NathanHaptic | Storage │ │
│  └─────────────────────────────────────────────────────┘ │
│  ┌──────────┐ ┌────────┐ ┌────────┐ ┌────────┐          │
│  │ ESP-IDF  │ │FreeRTOS│ │  I2S   │ │  SPI   │          │
│  └──────────┘ └────────┘ └────────┘ └────────┘          │
└─────────────────────────────────────────────────────────┘
```

### 7.3 Tâches FreeRTOS

| Tâche | Priorité | Core | Rôle |
|-------|----------|------|------|
| `task_audio_render` | Très haute | Core 0 | Rendu HRTF + DMA I2S |
| `task_game_logic` | Haute | Core 1 | Logique de jeu, état |
| `task_input_poll` | Haute | Core 1 | Lecture entrées via InputMapper à 100 Hz |
| `task_haptic_ctrl` | Moyenne | Core 1 | Contrôle moteurs via HapticEngine |
| `task_usb_bridge` | Basse | Core 1 | Communication USB avec IDE NATHAN |
| `task_sd_io` | Basse | Core 0 | Lecture assets depuis SD |

### 7.4 Protocole USB CDC (pont avec l'IDE NATHAN)

Le firmware expose un port série virtuel (USB CDC) avec un protocole simple :

| Commande | Direction | Description |
|----------|-----------|-------------|
| `LIST` | IDE → Console | Lister les mini-jeux sur SD |
| `UPLOAD <path> <size>` | IDE → Console | Envoyer un fichier vers SD |
| `DELETE <path>` | IDE → Console | Supprimer un fichier sur SD |
| `LOG` | Console → IDE | Stream des logs/erreurs en temps réel |
| `META <path>` | IDE → Console | Lire les métadonnées d'un mini-jeu |

> C'est l'unique point de contact entre ce projet et l'IDE. Tant que ce protocole est respecté, les deux projets évoluent indépendamment.

### 7.5 Support MicroPython embarqué

Le firmware intègre un interpréteur **MicroPython** via la bibliothèque `micropython-embed` compilée en tant que composant ESP-IDF.

**Note de continuité :** Le jeu existant GlassBreaker tourne en CircuitPython sur Pico. MicroPython et CircuitPython partagent la même syntaxe Python et des APIs très proches — le passage à MicroPython pour v2.0 est transparent pour les mini-jeux.

- Les mini-jeux sont des fichiers `.py` sur la carte SD (dossier `/sd/minigames/`)
- L'interpréteur est lancé dans un contexte sandboxé avec accès limité aux APIs HAL
- Un module C expose l'API du moteur à MicroPython :
  - `nathan.audio.play(sound_id, x, y, z)`
  - `nathan.haptic.pulse(motor, intensity)`
  - `nathan.input.read_joystick(id)` → `(x, y)`
  - `nathan.input.read_button(id)` → `bool`
- Les sons des mini-jeux sont stockés dans `/sd/minigames/<nom_jeu>/sounds/`

---

## 8. Spécifications du game engine

### 8.1 Philosophie du moteur

Le moteur est conçu pour un jeu **entièrement auditif**. Il n'y a pas de rendu graphique. Le "monde" est une grille 2D avec une coordonnée de hauteur. Les sons sont les seuls retours d'état du monde.

**Toute interaction avec le hardware passe par les contrats d'interface (section 5.3).** Le game engine n'appelle jamais directement I2S, GPIO, ou ADC.

### 8.2 Représentation du monde

#### Espace de coordonnées

```
        Y (profondeur)
        ^
        |
        |    * Son à (x=2, y=3, z=1)
        |
        +----------→ X (droite/gauche)

Z = hauteur (sol=0, plafond=3m env.)
Joueur toujours à Z=0 (sol)
```

- Grille 2D en centimètres entiers
- Hauteur Z flottante (0.0 à 3.0 m typiquement)
- Le joueur a une position `(px, py)` et une orientation `θ` (angle en degrés)

#### Calcul HRTF (responsabilité de l'équipe AUD)

Pour chaque source sonore à `(sx, sy, sz)` avec le joueur en `(px, py)` orienté à `θ` :

```
dx = sx - px
dy = sy - py
distance = sqrt(dx² + dy² + sz²)
azimut = atan2(dy, dx) - θ   (relatif à l'orientation du joueur)
élévation = atan2(sz, sqrt(dx² + dy²))
```

Application d'une HRTF lookup table (MIT KEMAR dataset, open-source, 187 positions) :
- Sélection des 2 HRTF les plus proches par interpolation
- Atténuation par distance : `gain = 1 / (1 + distance * k)`
- Rendu stéréo par convolution avec les réponses impulsionnelles HRTF gauche/droite

> **Note équipe AUD :** Le game engine fournit les positions via `spatial_audio_update_listener()` et `spatial_audio_set_position()`. Le calcul HRTF est entièrement encapsulé dans le module audio. L'équipe AUD est libre de choisir l'algorithme, la taille des filtres, et l'implémentation tant que l'API du contrat 2 est respectée.

### 8.3 API du game engine

```cpp
// Gestion de scène
Scene* scene_create(const char* name);
void scene_load(Scene* s);
void scene_unload(Scene* s);

// Entités sonores (délègue au SpatialAudioEngine)
SoundEntity* entity_create(float x, float y, float z, const char* sound_file);
void entity_set_position(SoundEntity* e, float x, float y, float z);
void entity_set_looping(SoundEntity* e, bool loop);
void entity_play(SoundEntity* e);
void entity_stop(SoundEntity* e);

// Joueur
void player_set_position(float x, float y);
void player_set_orientation(float angle_deg);
void player_move(float dx, float dy);

// Collisions (murs/obstacles)
void world_add_wall(float x1, float y1, float x2, float y2);
bool world_check_collision(float x, float y, float radius);

// Audio ambiant (non spatial, via SpatialAudioEngine)
void ambient_play(const char* sound_file, float volume);
void ambient_stop();

// Haptique (délègue au HapticEngine)
void engine_haptic_cane(float contact_x, float contact_y);
```

### 8.4 Système de collisions et bâton

Le bâton d'aveugle est simulé comme un **rayon** (raycast) partant du joueur dans la direction du joystick droit.

```
Joueur (px, py)
      \
       \  ← direction joystick droit
        \
         * point de contact (cx, cy)
         |
         | MURS ou OBSTACLES
```

- La distance au contact détermine l'intensité de vibration (proche = plus fort)
- La direction du contact (gauche/droite/avant) détermine quels moteurs activés
- Le son de frottement change selon la surface (bois, béton, herbe) via le tag de surface du mur

---

## 9. Spécifications du premier jeu — La Maison de Nathan

### 9.1 Concept général

**Titre :** La Maison de Nathan
**Genre :** Jeu de vie / exploration sensorielle
**Perspective :** Première personne sonore (FPS audio)
**Durée :** Jeu ouvert (exploration libre + quêtes)

Le joueur incarne **Nathan**, un adolescent aveugle. Il doit accomplir des tâches quotidiennes, explorer sa maison, jouer de la musique, aller à l'école, et affronter des adversaires imaginaires avec son bâton.

### 9.2 Structure de la maison

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│  ┌──────────┐  ┌──────────┐  ┌────────────────┐    │
│  │  CUISINE │  │  SALON   │  │    CHAMBRE     │    │
│  │          │  │  (HUB)   │  │                │    │
│  └──────────┘  └────┬─────┘  └────────────────┘    │
│                     │                               │
│  ┌──────────┐  ┌────┴─────┐  ┌────────────────┐    │
│  │ SALLE DE │  │          │  │  SALLE DE      │    │
│  │ MUSIQUE  │  │ COULOIR  │  │  MINI-JEUX     │    │
│  │          │  │          │  │                │    │
│  └──────────┘  └────┬─────┘  └────────────────┘    │
│                     │                               │
│             ┌───────┴──────┐                        │
│             │    ÉCOLE     │                        │
│             │  (extérieur) │                        │
│             └──────────────┘                        │
└─────────────────────────────────────────────────────┘
```

### 9.3 Pièce 1 — Le Salon (Hub principal)

**Rôle :** Point de départ et hub de navigation.

**Audio :** Musique d'ambiance douce (genre lo-fi / jazz calme). Sons de la maison : horloge, ventilation, sons extérieurs filtrés.

**Gameplay :**
- Premier endroit où le joueur apprend à se déplacer avec le joystick gauche
- Apprentissage de la navigation au son (chaque pièce a une signature musicale)
- Tutoriel intégré au jeu (voix du personnage explique ses sens)

**Éléments interactifs :**
- Canapé (son d'assise)
- Téléviseur (son — Nathan écoute un programme audio)
- Fenêtre (sons extérieurs, météo)

### 9.4 Pièce 2 — La Cuisine

**Audio :** Musique rythmée type jazz. Sons de cuisine (réfrigérateur, eau, vaisselle).

**Mini-jeu principal : Faire à manger**
- Objectif : Suivre une recette audio étape par étape
- Mécanique : Les joysticks imitent des gestes culinaires (mélanger = rotation joystick gauche, couper = up/down joystick droit)
- Feedback haptique : résistance simulée selon la texture des aliments
- Succès/échec évalué par la précision du geste et le timing

**Éléments interactifs :**
- Réfrigérateur (inventaire d'ingrédients, son caractéristique)
- Casserole (sons de cuisson évolutifs)
- Robinet (son de l'eau)

### 9.5 Pièce 3 — La Chambre

**Audio :** Musique calme / ASMR. Sons de chambre (ventilateur, pluie sur la fenêtre, horloge).

**Mini-jeux :**
- **Se lever le matin :** réveil, s'habiller (séquence de boutons au son)
- **Exploration libre :** Fouiller les tiroirs, découvrir des souvenirs audio

**Éléments interactifs :**
- Lit (point de sauvegarde)
- Radio (change la musique d'ambiance)
- Bureau (accès aux devoirs — mini-jeu de mémorisation sonore)

### 9.6 Pièce 4 — La Salle de Musique

**Audio :** Selon l'instrument joué. Réverbération de pièce simulée.

#### Instrument 1 — La Guitare

| Contrôle | Action |
|----------|--------|
| Joystick gauche (vertical) | Sélection de case (montée/descente sur le manche) |
| Joystick gauche (horizontal) | Sélection de corde |
| Joystick droit (vertical rapide ↓) | Strum vers le bas |
| Joystick droit (vertical rapide ↑) | Strum vers le haut |
| Bouton A | Accord de base (accord ouvert) |
| Bouton B | Accord barré |
| Bouton C | Accord spécial / sustain |

**Sons :** Samples de guitare acoustique réelle (banque de sons, licence libre).
**Feedback haptique :** Vibration légère des moteurs à chaque strum.

#### Instrument 2 — La Batterie

| Contrôle | Action |
|----------|--------|
| Joystick gauche ↑ | Grosse caisse (kick drum) |
| Joystick gauche ↓ | Charleston fermé (hi-hat closed) |
| Joystick gauche ← | Tom basse |
| Joystick gauche → | Tom aigu |
| Joystick droit ↑ | Snare |
| Joystick droit ↓ | Charleston ouvert (hi-hat open) |
| Gâchette L1 | Cymbale crash gauche |
| Gâchette R1 | Cymbale crash droite |
| Joystick droit appuyé | Ride cymbal |

**Sons :** Samples de batterie acoustique (banque libre).
**Feedback haptique :** Impact fort et court sur le/les moteurs correspondants.

**Mode enregistrement :** Possibilité d'enregistrer une séquence et de la rejouer (sequencer simple).

### 9.7 Pièce 5 — La Salle de Mini-Jeux

**Audio :** Musique arcade 8-bit. Sons d'ordinateur/console.

**Gameplay :**
- Hub des mini-jeux créés par l'utilisateur via l'IDE NATHAN
- Nathan s'assoit à son poste et peut lancer un mini-jeu de la liste sur la carte SD
- Navigation dans la liste par audio (lecture du titre depuis les métadonnées)
- Retour au salon après fin d'un mini-jeu

### 9.8 Zone 6 — L'École (extérieur)

**Audio :** Sons de rue, bruits urbains, cour d'école, voix des camarades.

**Mécanique principale : Navigation avec le bâton**

C'est ici que le bâton d'aveugle est le contrôle primaire :
- **Joystick droit** : contrôle la direction du bâton (360°)
- Le raycast détecte obstacles, bordures de trottoir, portes
- Les **5 moteurs** donnent la direction du contact
- Le **son** de frappe change selon la surface

**Sous-zones de l'école :**
- Trajet aller (navigation en rue — obstacles mobiles : piétons)
- Cour de récréation (interactions sociales audio avec personnages)
- Salle de classe (mini-jeux pédagogiques : maths, mémoire, musique)

**Combats imaginaires :**
- Déclenchés optionnellement dans certaines zones
- Le bâton devient arme : mêmes contrôles, adversaires signalés par sons directionnels
- Détection de coup : le raycast touche un ennemi → impact fort + son
- L'ennemi riposte → vibration directionnelle + son d'attaque (le joueur peut parer)

### 9.9 Contrôles de déplacement global

| Contrôle | Action |
|----------|--------|
| Joystick gauche | Déplacement du personnage (marche/direction) |
| Joystick droit | Direction du bâton (mode bâton) / action contextuelle |
| Bouton A | Interagir / confirmer |
| Bouton B | Annuler / reculer |
| Bouton C | Menu contextuel de la pièce |
| Start | Menu pause |
| L1 | Mode bâton (activer/désactiver bâton) |
| R1 | Sprint |

### 9.10 Système de navigation sonore inter-pièces

Chaque pièce émet une **signature musicale** différente. Depuis le couloir, les musiques des pièces adjacentes sont audibles en spatialisation. Plus le joueur approche d'une porte, plus la musique de la pièce correspondante est forte et plus son positionnement directionnel est précis.

---

## 10. Système de mini-jeux

### 10.1 Architecture générale

```
┌─────────────────────┐         ┌─────────────────────────┐
│     PC / Mac        │  USB-C  │      MCU NATHAN         │
│                     │◄───────►│                         │
│  IDE NATHAN       │ (CDC)   │  MiniGameRunner         │
│  (développé         │         │  ┌──────────────────┐   │
│   séparément)       │         │  │  mini_game.py    │   │
│                     │         │  │                  │   │
│                     │         │  │  nathan.audio    │   │
│                     │         │  │  nathan.haptic   │   │
│                     │         │  │  nathan.input    │   │
│                     │         │  └──────────────────┘   │
└─────────────────────┘         └─────────────────────────┘
```

> L'IDE NATHAN est développé dans un dépôt séparé et sera intégré sous `ide/` une fois le protocole USB CDC (section 7.4) stabilisé. Le développement de l'IDE n'apparaît pas dans la planification de ce cahier des charges.

### 10.2 API MicroPython exposée aux mini-jeux

```python
import nathan

# Audio spatial
nathan.audio.play(sound_id: str, x: float, y: float, z: float = 0.0)
nathan.audio.stop(sound_id: str)
nathan.audio.set_ambient(sound_id: str)

# Haptique
nathan.haptic.pulse(motor: int, intensity: float, duration_ms: int)
  # motor: 0-4 (gauche à droite)
  # intensity: 0.0 à 1.0
nathan.haptic.sweep(direction: float, intensity: float)
  # direction: -1.0 (gauche) à 1.0 (droite)

# Entrées
x, y = nathan.input.joystick(id: int)  # id: 0=gauche, 1=droite
pressed = nathan.input.button(id: int)  # id: 0=A, 1=B, 2=C, 3=L1, 4=R1

# Contrôle du jeu
nathan.game.score(points: int)
nathan.game.end(success: bool)
nathan.game.set_title(title: str)

# Utilitaires
nathan.sleep_ms(ms: int)  # attente non bloquante
nathan.time_ms() -> int   # temps depuis démarrage
```

### 10.3 Format de mini-jeu

Le format est **directement inspiré** de l'architecture GlassBreaker existante (`game/menu.py`). Un mini-jeu est une **classe Python** avec métadonnées et méthodes standardisées.

```python
# Structure d'un mini-jeu NATHAN (MicroPython)
import nathan

META = {
    "title": "Mon Mini-Jeu",          # Lu à voix haute dans le hub
    "author": "Arthur",
    "description": "Un jeu de mémoire sonore"
}

class MonMiniJeu:
    def __init__(self):
        self.score = 0

    def setup(self):
        """Appelé une fois au démarrage."""
        nathan.audio.set_ambient("arcade_ambient.wav")
        nathan.audio.play("intro.wav", 0, 0, 0)

    def loop(self) -> bool:
        """
        Appelé à chaque frame.
        Retourne True pour continuer, False pour terminer.
        """
        x, y = nathan.input.joystick(0)
        if nathan.input.button(0):   # Bouton A
            nathan.audio.play("confirm.wav", 0, 0, 0)
            nathan.haptic.pulse(2, 0.8, 100)
            self.score += 1
        if self.score >= 10:
            nathan.game.end(success=True)
            return False
        return True

# Point d'entrée appelé par le MiniGameRunner
def create():
    return MonMiniJeu()
```

**Structure de fichiers sur la carte SD :**
```
/sd/minigames/
└── mon_mini_jeu/
    ├── main.py          # Fichier principal (contient META + classe)
    └── sounds/          # Sons du mini-jeu (WAV 16 bits, 44.1kHz, mono)
        ├── intro.wav
        ├── confirm.wav
        └── arcade_ambient.wav
```

---

## 11. Contraintes et risques

> Les contraintes détaillées, les hypothèses de travail et les plans de contingence sont documentés dans :
> - `CONTRAINTES.md` — 32 contraintes fixes (accessibilité, techniques, financières, réglementaires)
> - `HYPOTHESES.md` — 32 hypothèses de travail avec validation prévue et plan de contingence

### 11.1 Risques techniques principaux (résumé)

| Risque | Niveau | Mitigation |
|--------|--------|------------|
| HRTF temps réel sur MCU embarqué | Critique | Benchmark PC d'abord → choix MCU adapté → fallbacks : filtres courts, moins de sources, DSP externe, stéréo simple |
| Autonomie batterie | Élevé | Gestion PWM moteurs, sleep Wi-Fi, batterie >= 2000 mAh |
| Intégration MicroPython dans le firmware | Moyen | Prototypage précoce, fallback vers Lua si incompatible |
| Ergonomie boîtier | Moyen | Itérations rapides en impression 3D, tests avec utilisateurs DV |
| Désynchronisation entre équipes | Élevé | Contrats d'interface gelés Phase 0, 3 SYNC, tests d'interface |
| Accessibilité de l'IDE | Moyen | Prototypage TTS/ARIA précoce, tests avec utilisateurs DV du groupe Discord |

### 11.2 Contraintes techniques reconnues

- Micro SD : Latence de lecture (~few ms) — les samples audio doivent être pré-chargés en RAM
- MicroPython : Vitesse d'exécution ~10-50x plus lente que C — les mini-jeux sont des jeux simples
- Le volume audio doit être géré par software (la plupart des DAC I2S n'ont pas de contrôle hardware)

---

## 12. Planification

> La planification détaillée (tâches, chronologie, chemins critiques parallèles, jalons de convergence,
> point de transition manette Xbox → manette NATHAN) est documentée dans `TACHES.md`.

### 12.1 Principe de planification

Le projet suit une approche **PC-first** avec 6 flux parallèles convergeant à des jalons clés :

1. **Game Engine** (ENG) — développé sur PC avec manette USB de substitution
2. **Audio HRTF** (AUD) — développé sur PC, porté après benchmark
3. **Hardware** (ELEC) — conçu après le choix du MCU basé sur les benchmarks
4. **Contenu de jeu** (JEU) — développé sur PC indépendamment du matériel
5. **IDE** (ENG) — développé en parallèle, intégré via USB CDC
6. **Communauté DV** — feedback continu via Discord tout au long du projet

### 12.2 Points de référence avec le code existant (GlassBreaker)

| Élément v2.0 | Référence dans GlassBreaker | Notes |
|---|---|---|
| InputMapper | `input/buttons.py` (ButtonManager) | Même pattern, étendre avec joysticks |
| SpatialAudioEngine | `output/audio.py` (AudioManager) | Logique de gestion WAV réutilisable |
| HapticEngine | `output/motors.py` (MotorManager) | Passer de 2 à 5 moteurs avec intensité |
| StorageProvider | `utils/memory.py` (MemoryManager) | Même principe, FAT32 sur SD |
| MiniGameRunner | `game/menu.py` (MenuExtension) | Même pattern classe + `run()` |

---

## 13. Budget

> Le budget détaillé et le suivi financier sont gérés dans `TACHES.md` (section Budget prévisionnel du RPC1).

**Contrainte budgétaire :** <= 500$ CAD pour le prototype (incluant réserve imprévus ~30%)
**Objectif de production :** < 100$ CAD par unité

**Tous les outils logiciels sont gratuits :** SDK du MCU (open-source), MicroPython (MIT), KiCAD, datasets HRTF (MIT KEMAR), Electron (MIT).

> Le coût exact du prototype dépend du MCU choisi. Une estimation par scénario MCU est réalisée dans le MIP (tâche MIP-03c).

---

## 14. Livrables

> La liste complète des livrables par session (académiques + techniques) et leur checklist
> se trouvent dans `TACHES.md`.

### 14.1 Livrables techniques

- Manette physique (PCB + boîtier + batterie) avec le MCU choisi
- Game engine fonctionnel (scènes, collisions, bâton, navigation, audio spatial)
- Module audio spatial (PCAudio + implémentation embarquée)
- Jeu "La Maison de Nathan" (>= 4 zones jouables)
- Système MicroPython (interpréteur + module `nathan` + sandbox + 2 mini-jeux)
- IDE de programmation accessible (éditeur + transfert USB + TTS)
- Documentation (API game engine, API MicroPython, protocole USB CDC)

### 14.2 Livrables académiques

- MIP, RPC1 (S6) — RPC2 (S7) — RLP (S8)
- RAE individuels (chaque session)
- Audits d'équipe et numériques
- Démonstration Expo MégaGÉNIALE (S8)

---

*Document vivant — à mettre à jour à chaque jalon atteint.*
*NATHAN Console — Open-source, accessible, pour tous.*
