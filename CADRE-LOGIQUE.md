# Cadre Logique — Projet NATHAN Console v2.0

**Projet :** NATHAN — Narrative Audio Terminal for Humans with Alternative Navigation
**Date :** 2026-05-26
**Session :** PMC660 (S6, E2026)

---

## Niveau 4 — FINALITÉ

| Niveaux descriptifs | Indicateurs objectivement vérifiables | Moyens de vérification | Conditions critiques |
|---|---|---|---|
| **Offrir aux personnes non-voyantes une console de jeu accessible, open-source et abordable, où l'expérience est entièrement auditive et haptique.** | F1. Au moins 1 personne non-voyante (du groupe de testeurs recrutés via l'APHVE) complète une session de jeu de 15 min sans assistance extérieure, avec un score de satisfaction >= 3/5 sur l'immersion | Test utilisateur filmé avec protocole CER approuvé; questionnaire post-test avec échelle Likert 1-5 | Le partenaire APHVE reste disponible et recrute des testeurs DV; le CER approuve le protocole dans les délais |
| | F2. Coût de production unitaire estimé < 100$ CAD vs. solutions existantes (manettes adaptées > 300$) | BOM de production documenté; comparaison tarifaire avec 3 alternatives du marché | Prix des composants stables; pas de rupture d'approvisionnement |
| | F3. Code source, PCB et fichiers de boîtier publiés sous licence open-source | Dépôt GitHub public avec fichier LICENSE; Gerbers, STL et source accessibles | Aucune clause de confidentialité n'empêche la publication |

---

## Niveau 3 — OBJECTIFS DU PROJET

| Niveaux descriptifs | Indicateurs objectivement vérifiables | Moyens de vérification | Conditions critiques |
|---|---|---|---|
| **O1. Développer un game engine embarqué agnostique du matériel, avec audio spatial binaural HRTF fonctionnel au casque** | O1.1. Le même code de jeu fonctionne sans modification avec 2 sources d'entrées différentes (manette USB sur PC et manette finale) grâce aux interfaces abstraites | Démonstration du swap d'implémentation (GamepadMapper → NathanMapper) sans recompilation du game engine | Les interfaces définies en Phase 0 couvrent tous les cas d'usage; pas de changement majeur en cours de route |
| | O1.2. Audio spatial : 3/3 testeurs localisent une source sonore à +/- 30° au casque; >= 4 sources simultanées sans artefact; CPU coeur audio < 80% | Test perceptuel : sources à 0°, 90°, 180°, 270°, taux de localisation >= 80%; profiling CPU documenté | Le dataset HRTF open-source est compatible avec les contraintes mémoire du MCU choisi |
| | O1.3. Latence bout-en-bout (action → son au casque) < 50 ms; latence haptique < 100 ms | Mesure instrumentée (oscilloscope ou timer haute résolution) | Le MCU choisi a la puissance suffisante (validée par benchmark PC préalable) |
| **O2. Concevoir et fabriquer une manette de jeu ergonomique avec le microcontrôleur choisi selon les besoins mesurés** | O2.1. Microcontrôleur choisi sur la base d'un document de justification quantitatif (CPU, RAM, I2S, USB, ADC) comparant >= 3 candidats | Document de justification avec benchmark PC comme baseline; matrice de décision pondérée | Le benchmark PC est réalisé avant le choix (sem 12-14) |
| | O2.2. PCB fabriqué et fonctionnel : 0 court-circuit, tensions conformes (3.3V +/- 5%), tous les sous-systèmes testés individuellement | Tests électriques documentés (continuité, tensions à l'oscilloscope); firmware boot réussi | Le fabricant livre le PCB dans les 2-3 semaines |
| | O2.3. Boîtier ergonomique : 3/3 testeurs confortables pendant 30 min; 5/5 contrôles identifiés au toucher les yeux bandés; autonomie >= 4h | Test d'ergonomie avec protocole; test d'autonomie chronométré | Imprimante 3D disponible; batterie de capacité suffisante disponible |
| **O3. Créer "La Maison de Nathan", un jeu entièrement audio-haptique avec >= 4 zones jouables** | O3.1. >= 4 zones (Salon, Cuisine, Chambre, Salle de Musique) jouables avec ambiance distincte + >= 2 interactions par zone | Démonstration devant le superviseur : parcours des 4 zones au casque avec checklist | Les assets audio (>= 50 sons, >= 10 narrations) sont disponibles à temps |
| | O3.2. Navigation inter-pièces : joueur aux yeux bandés identifie >= 3 pièces par leur signature musicale directionnelle | Test documenté : joueur départ au Salon, identifie les directions | L'audio spatial (O1) est fonctionnel avant l'intégration du jeu (sem 10) |
| | O3.3. Tutoriel intégré : nouveau joueur comprend les contrôles en < 5 min | Test avec 2 nouveaux joueurs; temps mesuré | Narration vocale enregistrée à temps |
| **O4. Permettre la programmation de mini-jeux MicroPython exécutés depuis une carte SD** | O4.1. Mini-jeu de < 50 lignes utilisant l'API `nathan.*` (audio, haptic, input) fonctionne sur la console | Démonstration : écriture, upload USB, exécution sur console | L'interpréteur MicroPython s'intègre dans le firmware sans conflit |
| | O4.2. >= 2 mini-jeux d'exemple livrés et jouables depuis le hub | Mini-jeux jouables lors de la démo finale | Mini-jeux testés avant la livraison |

---

## Niveau 2 — EXTRANTS

| Niveaux descriptifs | Indicateurs objectivement vérifiables | Moyens de vérification | Conditions critiques |
|---|---|---|---|
| **E1. Contrats d'interface gelés (5 contrats : Input, Audio, Haptic, Storage, MiniGame)** | 5 fichiers `.h` validés et signés par les équipes à la semaine 2; chaque contrat a >= 2 implémentations fonctionnelles | Revue croisée; tests unitaires passent avec chaque implémentation | Toutes les équipes participent à la Phase 0 |
| **E2. Game engine fonctionnel sur PC (scènes, collisions, bâton, navigation, audio spatial)** | Session de jeu de 15 min sur PC sans crash ni fuite mémoire; heap libre stable après 10 transitions de scène | Démonstration PC au SYNC 2 (sem 14); rapport de stabilité | PCAudio (E4) prêt avant la sem 10 |
| **E3. Rapport de benchmark PC** | Document quantitatif : CPU par source audio, RAM totale, taille buffers, latence mesurée; comparaison avec >= 3 MCU candidats | Rapport écrit avec mesures; validé par l'équipe AUD et ENG | Outils de profiling disponibles |
| **E4. Module audio spatial PCAudio** | Toutes les fonctions du contrat SpatialAudioEngine implémentées; 4+ sources; taux de localisation >= 80% (test perceptuel 3 testeurs) | Démo audio au SYNC 1 (sem 6); test perceptuel documenté | Bibliothèque audio PC (miniaudio ou autre) fonctionnelle |
| **E5. Module audio embarqué** | Audio spatial fonctionnel sur MCU choisi; même qualité perceptuelle que PCAudio (test A/B); latence < 20 ms | Démo au SYNC 3 (sem 22); rapport benchmark embarqué | Portage HRTF faisable en software pur (ou DSP ajouté au budget) |
| **E6. Manette physique (PCB + boîtier + batterie)** | PCB fonctionnel (0 erreur ERC/DRC); boîtier imprimé; assemblage complet; test d'ergonomie passé | Photos assemblage; captures ERC/DRC; rapport tests électriques | Fabricant PCB livre à temps; imprimante 3D disponible |
| **E7. Jeu "La Maison de Nathan" (code + assets)** | >= 50 WAV 16bit/44.1kHz; >= 4 zones avec interactions; >= 10 clips narration; >= 6 ambiances musicales | Inventaire des assets; test de chaque zone avec checklist | Microphone/logiciel d'enregistrement disponible |
| **E8. Intégration MicroPython + module `nathan` + 2 mini-jeux** | Module `nathan` expose >= 10 fonctions API testées unitairement; sandbox vérifié; 2 mini-jeux jouables | Tests unitaires; démo des mini-jeux | `micropython-embed` compatible avec le MCU choisi |
| **E10. IDE de programmation accessible (5 couches : UX accessible, Édition, Assistant IA, Déploiement, Matériel)** | IDE fonctionnel : éditeur MicroPython avec coloration + linter + TTS + screen reader + transfert USB CDC + logs en temps réel + gestionnaire de mini-jeux; cycle écrire→transférer→jouer < 1 min | Démonstration : écriture d'un mini-jeu dans l'IDE, upload, exécution sur console; test d'accessibilité avec lecteur d'écran et 1 utilisateur DV du groupe Discord | Stack technologique maîtrisée; Web Serial API ou serialport npm fonctionnel; TTS français de qualité suffisante |
| **E9. Documentation + BOM** | README à jour; API game engine documentée (>= 15 fonctions); API MicroPython (>= 10 fonctions); BOM avec prix réels <= 500$ | Documents dans le dépôt; BOM comparé aux factures | Temps alloué à la documentation |

---

## Niveau 1 — INTRANTS

| Niveaux descriptifs | Indicateurs objectivement vérifiables | Moyens de vérification | Conditions critiques |
|---|---|---|---|
| **I1. Équipe de 7 étudiants (GE + GI)** | 7 membres actifs; 135h/personne/session (>= 945h total S6); >= 1 GE, >= 1 GI signal/audio, >= 2 GI firmware | Feuilles de temps hebdomadaires; matrice de compétences | Pas d'abandon; membres inscrits à PMC660 |
| **I2. Budget <= 500$ CAD** | Achats tracés; réserve imprévus 30% (100$) planifiée | Tableau de suivi financier; factures conservées | Financement confirmé (autofinancement ou partenaire) |
| **I3. Matériel de développement initial** | >= 2 manettes USB (PS4/Xbox); casque stéréo; achetés avant sem 3 | Confirmation de réception | Livraison <= 2 semaines |
| **I4. Matériel MCU et prototypage** | DevKit du MCU choisi + DAC + moteurs + joysticks + batterie; achetés après la décision F.04 (sem 14) | Confirmation de commande post-SYNC 2 | Composants disponibles chez les fournisseurs |
| **I5. Outils logiciels** | Toolchain du MCU installée sur >= 2 postes; KiCAD; SolidWorks (licence UdeS); bibliothèque audio PC | Build réussi sur 2 postes | Licences actives; machines suffisantes |
| **I6. Locaux et équipement** | Accès laboratoire UdeS (soudure, oscilloscope); imprimante 3D | Réservation confirmée; formation sécurité complétée | Disponibilité Faculté de génie |
| **I7. Temps : 26 semaines, 3 sessions** | SYNC 1 (sem 6), SYNC 2 (sem 14), SYNC 3 (sem 22); contrats gelés sem 2 | Gantt/tableau de planification; PV des SYNC | Chemin critique respecté (benchmark → choix MCU → portage) |
| **I8. Partenaire, communauté DV et approbation éthique** | >= 2 rencontres avec l'APHVE; serveur Discord créé; >= 5 utilisateurs DV recrutés (par l'équipe + APHVE); >= 3 consultations documentées; formulaire CER soumis >= 4 sem avant test; réponse CER obtenue | PV rencontres; liste des membres Discord; logs des consultations; email CER; lettre d'approbation/dispense | APHVE disponible; Discord accessible aux personnes DV; CER traite dans les délais |

---

## Lecture causale (de bas en haut)

1. **Si** les intrants sont disponibles **et** les conditions critiques du niveau 1 sont respectées,
   **alors** les extrants seront produits.

2. **Si** les extrants sont produits **et** les conditions critiques du niveau 2 sont respectées,
   **alors** les objectifs seront atteints.

3. **Si** les objectifs sont atteints **et** les conditions critiques du niveau 3 sont respectées,
   **alors** la finalité sera réalisée.

---

*Document vivant — à réviser à chaque coaching et SYNC.*
