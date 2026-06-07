# Tâches et Chronologie — Projet NATHAN Console v2.0

**Date :** 2026-06-07
**Session :** PMC660 (S6, E2026) — **semaine 6** (semaine du 8 juin 2026)
**Révision :** planification GANTT — ajout estimations, dates de début/fin et dépendances ; structure hybride par **blocs** ; intégration du travail de **stage** (capacité réduite).

> Ce document regroupe **toutes** les tâches du projet : administratives, académiques et techniques.
> Il suit la logique réelle du projet et les exigences du guide étudiant PMC660-760-860.
> **Statut de ce document :** brouillon pour revue d'équipe (2 jours). Une fois validé → import JIRA (le `.md` est déjà « export-CSV-ready » : 1 tâche = 1 ligne avec ID, dépendances et dates).

---

## Légende

**Colonnes des tableaux de tâches**

| Champ | Sens |
|-------|------|
| **ID** | Identifiant unique (sert de clé pour les dépendances et l'import JIRA) |
| **Tâche** | Description courte |
| **Rôle** | Bloc/discipline responsable : `ENG` (logiciel/game engine/IDE), `AUD` (audio HRTF), `ELEC` (électronique/PCB/méca), `JEU` (contenu de jeu), `ÉQUIPE`, `INDIV`, `GESTION` |
| **Est.** | Estimation d'effort en **heures-équipe** (± 20 %, `H-14`) |
| **Début / Fin** | Dates planifiées (ISO `AAAA-MM-JJ`), alignées sur les semaines de session |
| **Dépend de** | ID(s) prédécesseur(s) — `—` si aucune |
| **Statut** | `[ ]` à faire · `[x]` fait · `~~…~~` annulé/déplacé |

**Schéma des ID** — Les tâches existantes conservent leur ID (`ADM-`, `PART-`, `COM-`, `ETH-`, `MIP-`, `RPC1-`, `TECH-`, `S7-T`, `S8-T`, `EVAL-`…). Les tâches **ajoutées à cette révision** portent un préfixe de bloc : `GE-` (game engine), `AU-` (audio), `PCB-`, `BOI-` (boîtier), `JEU-`, `IDE-`.

---

## Calendrier de référence (dates fournies par l'équipe)

| Période | Code | Type | Début | Fin | Capacité/pers | Capacité équipe (7) |
|---------|------|------|-------|-----|---------------|---------------------|
| Été 2026 | **S6** | Session PMC660 (3 cr) | 2026-05-04 | 2026-08-14 | 9 h/sem (135 h) | **945 h** |
| Automne 2026 | **T4** | **Stage** | 2026-09-08 | 2026-12-18 | ~4 h/sem (~60 h) | **~420 h** (réduit) |
| Hiver 2027 | **S7** | Session PMC760 (6 cr) | 2027-01-05 | 2027-04-30 | 18 h/sem (270 h) | **1890 h** |
| Été 2027 | **T5** | **Stage** | 2027-05-03 | 2027-08-13 | ~4 h/sem (~60 h) | **~420 h** (réduit) |
| Automne 2027 | **S8** | Session PMC860 (3 cr) | 2027-08-30 | 2027-12-23 | 9 h/sem (135 h) | **945 h** |

**Stages (T4, T5).** Le guide ne prévoit **pas** de temps projet pendant les stages, mais l'équipe y travaillera à **capacité réduite (~4 h/sem/pers)**. Ce temps est concentré sur **le chemin critique** (engine → benchmark → MCU → PCB) et sur le travail **parallélisable sans temps d'équipe synchrone** (production de sons, contenu de jeu, maturation audio, pré-travail PCB). Les stages **dé-risquent** le calendrier : ils permettent d'arriver « benchmark-ready » au début de S7.

**Ancrage vérifié :** Coaching 2 = 28 mai 2026 = S6 sem 4 ✓ · « semaine 6 » = semaine du 8 juin 2026 ✓.

**Repère semaines ↔ dates (lundis)**
- **S6** : s1 05-04 · s4 05-25 · s6 06-08 · s8 06-22 · s10 07-06 · s13 07-27 · s15 08-10 (fin 08-14)
- **S7** : s1 01-05 · s3 01-18 · s6 02-08 · s8 02-22 · s10 03-08 · s12 03-22 · s15 04-12 (fin 04-30)
- **S8** : s1 08-30 · s3 09-13 · s6 10-04 · s10 11-01 · s13 11-22 (**Expo ~11-27/28**) · s17 12-20 (fin 12-23)

---

# PARTIE 1 — Gestion & Académique

> Piloté par des **échéances** → organisé par session. Tâches transversales (toutes disciplines).

## S6 — PMC660 (été 2026)

### 1A. Formalités contractuelles et légales

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| ADM-01 | Cession de droits (Annexe A), par membre | INDIV | 2h | 2026-05-11 | 2026-05-15 | — | [ ] | Obligatoire — IN si manquant |
| ADM-02 | Entente de confidentialité (Annexe D) | INDIV | 1h | 2026-05-11 | 2026-05-15 | — | [ ] | Obligatoire — IN si manquant |
| ADM-03 | Autorisation photos/vidéos (Annexe E) | INDIV | 1h | 2026-05-11 | 2026-05-15 | — | [ ] | Obligatoire |
| ADM-04 | Engagement à la confidentialité (Annexe H) | INDIV | 1h | 2026-05-11 | 2026-05-15 | — | [ ] | Si infos confidentielles |
| ADM-05 | Contrat d'équipe (rôles, responsabilités) | ÉQUIPE | 12h | 2026-05-11 | 2026-05-22 | — | [ ] | Inclus dans le MIP (Annexe P) |
| ADM-06 | Dépôt des formulaires signés (SharePoint PMC) | GESTION | 3h | 2026-05-18 | 2026-05-22 | ADM-01,ADM-02,ADM-03 | [ ] | Vérifier liste livrables PMC660 |

### 1B. Partenariat APHVE (via SARIC)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| PART-01 | ~~Identifier un organisme partenaire~~ | GESTION | — | — | — | — | [x] | APHVE identifié |
| PART-02 | ~~Présenter le projet à l'APHVE~~ | GESTION | — | — | — | — | [x] | Acceptation reçue |
| PART-03 | Présenter le MIP à l'APHVE (valider mandat) | ÉQUIPE | 6h | 2026-05-25 | 2026-06-05 | MIP-01 | [ ] | Confirme le mandat avant convention |
| PART-04 | Modalités de partenariat (2 pages) | ÉQUIPE | 10h | 2026-05-25 | 2026-06-05 | PART-03 | [ ] | 2 scénarios possibles (Guide 2.1.2) |
| PART-05 | Signature des Modalités par l'APHVE | GESTION | 3h | 2026-06-01 | 2026-06-12 | PART-04 | [ ] | Envoyer à pmc-coordination@usherbrooke.ca |
| PART-06 | Ouverture du dossier SARIC (par coord. PMC) | — | 2h | 2026-06-08 | 2026-06-26 | PART-05 | [ ] | Délai possible de quelques semaines |
| PART-07 | Rencontre conseillère SARIC | ÉQUIPE | 4h | 2026-06-15 | 2026-07-10 | PART-06 | [ ] | Délai possible entre PART-05 et PART-06 |
| PART-08 | Convention de partenariat (20-30 p., 3 parties) | TOUTES | 30h | 2026-06-22 | 2026-07-24 | PART-07 | [ ] | **Signée AVANT de léguer au partenaire** |

### 1C. Communauté d'utilisateurs DV (Flux F)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| COM-01 | Serveur Discord accessible (lecteur d'écran) | ÉQUIPE | 8h | 2026-05-18 | 2026-05-22 | — | [ ] | Tester accessibilité avec 1-2 pers. DV |
| COM-02 | Processus de recrutement (avec APHVE) | ÉQUIPE | 6h | 2026-05-18 | 2026-05-29 | COM-01 | [ ] | Critères définis avec l'APHVE |
| COM-03 | Recrutement ≥ 5 personnes DV | ÉQUIPE | 20h | 2026-05-25 | 2026-06-26 | COM-02 | [ ] | APHVE, réseaux, bouche-à-oreille |
| COM-04 | 1ʳᵉ consultation (besoins et attentes) | ÉQUIPE | 12h | 2026-06-08 | 2026-06-26 | COM-03 | [ ] | Documenter le feedback |
| COM-05 | Consultations régulières (≥ 3 sur le projet) | ÉQUIPE | 30h | 2026-06-22 | 2027-12-11 | COM-04 | [ ] | Continue — proto PC, proto matériel |
| COM-06 | Tests utilisateurs formels (protocole CER) | ÉQUIPE | — | 2027-10-18 | 2027-10-29 | ETH-05,S8-T09 | [ ] | Voir S8-T10 — CER approuvé avant |

### 1D. Considérations éthiques (CER — tests avec personnes DV)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| ETH-01 | Prendre connaissance de l'outil d'aide CER | ÉQUIPE | 3h | 2026-05-11 | 2026-05-15 | — | [ ] | Lien sur le site PMC |
| ETH-02 | Formulaire de demande d'avis au CER | ÉQUIPE | 16h | 2027-01-05 | 2027-01-23 | — | [ ] | ≥ 4 sem avant test (S8) — soumettre tôt |
| ETH-03 | Réponse du CER | — | — | 2027-01-26 | 2027-02-13 | ETH-02 | [ ] | 1-2 sem; si CER complet → plus long |
| ETH-04 | Protocole d'essai (tests DV) | ÉQUIPE | 16h | 2027-09-13 | 2027-09-27 | ETH-03 | [ ] | ≥ 2 sem avant test — gabarit PMC |
| ETH-05 | Soumission du protocole au superviseur | ÉQUIPE | 2h | 2027-09-27 | 2027-10-02 | ETH-04 | [ ] | **Obligatoire avant toute expérimentation** |

> **Rappel :** tout essai du prototype (même partiel) exige un protocole d'essai préalablement validé (Guide 2.1.5).

### 2A. Rédaction du MIP (Mémoire d'identification de projet)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| MIP-01 | Description du projet (situation actuelle/désirée) | ÉQUIPE | 12h | 2026-05-11 | 2026-05-22 | — | [ ] | Haut niveau, pas de composants |
| MIP-02 | Analyse de l'environnement (systèmes similaires) | ÉQUIPE | 10h | 2026-05-11 | 2026-05-22 | — | [ ] | Documenter les sources |
| MIP-03 | Analyse des parties prenantes | ÉQUIPE | 6h | 2026-05-11 | 2026-05-22 | — | [ ] | Ne PAS inclure les superviseurs |
| MIP-04 | Tableau du cadre logique (indicateurs mesurables) | ÉQUIPE | 8h | 2026-05-11 | 2026-05-22 | — | [ ] | Voir `CADRE-LOGIQUE.md` |
| MIP-05 | Analyse d'impact (social/environ./éco.) | ÉQUIPE | 6h | 2026-05-11 | 2026-05-22 | — | [ ] | Accessibilité, open-source, coût |
| MIP-06 | Recherche de systèmes similaires (état de l'art) | ÉQUIPE | 10h | 2026-05-11 | 2026-05-22 | — | [ ] | Métriques, aspects novateurs |
| MIP-07 | Diagramme d'architecture système (5 interfaces) | ÉQUIPE | 8h | 2026-05-18 | 2026-05-29 | TECH-01 | [ ] | PC vs embarqué. Inclure l'IDE |
| MIP-08 | Analyse préliminaire des MCU candidats (≥ 3) | ELEC | 12h | 2026-05-18 | 2026-05-29 | TECH-18 | [ ] | Identifier/estimer, ne pas choisir. Voir `ESTIMATION.md` |
| MIP-09 | Estimation budgétaire par scénario MCU | ELEC | 8h | 2026-05-18 | 2026-05-29 | MIP-08 | [ ] | Impact du MCU sur le budget |
| MIP-10 | Estimation de l'effort et calendrier | ÉQUIPE | 8h | 2026-05-18 | 2026-05-29 | — | [ ] | **Ce document** alimente MIP-10 |
| MIP-11 | Ressources financières et matérielles | ÉQUIPE | 4h | 2026-05-18 | 2026-05-29 | MIP-09 | [ ] | Budget ~500$ ventilé par bloc |
| MIP-12 | Risques principaux | ÉQUIPE | 6h | 2026-05-18 | 2026-05-29 | — | [ ] | HRTF, MCU, accessibilité IDE, ergonomie |
| MIP-13 | Stratégie de gestion retenue | ÉQUIPE | 4h | 2026-05-18 | 2026-05-29 | — | [ ] | Justifier (trad./agile/hybride) |
| MIP-14 | Conclusion et recommandations | ÉQUIPE | 4h | 2026-05-25 | 2026-05-29 | MIP-12 | [ ] | |
| MIP-15 | Références (sources complètes) | ÉQUIPE | 4h | 2026-05-25 | 2026-05-29 | — | [ ] | |
| MIP-16 | Contrat d'équipe (inclus au MIP) | ÉQUIPE | — | 2026-05-25 | 2026-05-29 | ADM-05 | [ ] | Voir ADM-05 |
| MIP-17 | Relecture et mise en forme (max 20 p.) | ÉQUIPE | 12h | 2026-05-25 | 2026-06-05 | MIP-14 | [ ] | Times New Roman 12, interligne 1.5 |
| MIP-18 | **Dépôt du MIP** (canal Teams) | ÉQUIPE | 1h | 2026-06-05 | 2026-06-08 | MIP-17 | [ ] | ⚠️ **Date exacte à confirmer (Teams)** |

> **À éviter :** expliquer la théorie du cadre logique ; remplir les catégories non pertinentes de l'Annexe P ; phrases creuses.

### 3A. Rédaction du RPC1 (Rapport de projet de conception 1)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| RPC1-01 | Contexte, objectifs, requis, contraintes (MAJ MIP) | ÉQUIPE | 10h | 2026-06-01 | 2026-06-12 | MIP-18 | [ ] | Cadre logique à jour |
| RPC1-02 | Systèmes similaires et état de l'art | ÉQUIPE | 8h | 2026-06-01 | 2026-06-12 | MIP-06 | [ ] | Consoles access., jeux audio, HRTF |
| RPC1-03 | Concept global (schémas, blocs, images) | ÉQUIPE | 12h | 2026-06-01 | 2026-06-19 | MIP-07 | [ ] | Interfaces, PC vs embarqué |
| RPC1-04 | Description des modules (E/S, specs, tests) | ÉQUIPE | 16h | 2026-06-08 | 2026-06-26 | RPC1-03 | [ ] | Engine, Audio, HW, Jeu, μPython, IDE |
| RPC1-05 | Options évaluées et recommandation | ÉQUIPE | 10h | 2026-06-08 | 2026-06-26 | RPC1-04 | [ ] | Ex : MCU via benchmark |
| RPC1-06 | Incertitudes et risques | ÉQUIPE | 8h | 2026-06-08 | 2026-06-26 | — | [ ] | |
| RPC1-07 | Critères de vérification (tests/module) | ÉQUIPE | 8h | 2026-06-08 | 2026-06-26 | RPC1-04 | [ ] | |
| RPC1-08 | WBS (2 niveaux dans le rapport) | ÉQUIPE | 8h | 2026-06-15 | 2026-06-26 | — | [ ] | Ou backlog si Agile |
| RPC1-09 | Planification temporelle (Gantt) | ÉQUIPE | 10h | 2026-06-15 | 2026-06-26 | MIP-10 | [ ] | **Ce document** = base du Gantt. S6→S8 |
| RPC1-10 | Interactions partenaire (fréquence, type) | ÉQUIPE | 3h | 2026-06-15 | 2026-06-26 | — | [ ] | |
| RPC1-11 | Livrables intermédiaires (dates) | ÉQUIPE | 3h | 2026-06-15 | 2026-06-26 | — | [ ] | Jalons de convergence (Partie 3) |
| RPC1-12 | Budget prévisionnel (± 10 %) | ÉQUIPE | 8h | 2026-06-15 | 2026-06-26 | MIP-11 | [ ] | Voir `ESTIMATION.md` |
| RPC1-13 | Analyse des risques (proba, impact, mitig.) | ÉQUIPE | 8h | 2026-06-15 | 2026-06-26 | RPC1-06 | [ ] | Inclure risques Expo |
| RPC1-14 | Sommaire et recommandations | ÉQUIPE | 4h | 2026-06-22 | 2026-07-03 | RPC1-13 | [ ] | |
| RPC1-15 | Références | ÉQUIPE | 4h | 2026-06-22 | 2026-07-03 | — | [ ] | |
| RPC1-16 | Relecture et mise en forme (max 35 p.) | ÉQUIPE | 16h | 2026-06-29 | 2026-07-03 | RPC1-14 | [ ] | Étudier le feedback MIP |
| RPC1-17 | **Dépôt du RPC1** (canal Teams) | ÉQUIPE | 1h | 2026-07-06 | 2026-07-10 | RPC1-16 | [ ] | ⚠️ **Date exacte à confirmer (Teams)** |

### 3C. Activités d'évaluation S6

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| EVAL-01 | Coaching 1 (30 min) | ÉQUIPE | 2h | 2026-05-11 | 2026-05-15 | — | [x] | Fait |
| EVAL-02 | Coaching 2 (30 min) | ÉQUIPE | 2h | 2026-05-25 | 2026-05-28 | — | [x] | 28 mai 2026 |
| EVAL-03 | Coaching 3 (30 min) | ÉQUIPE | 2h | 2026-06-08 | 2026-06-12 | — | [ ] | Sem 6 |
| EVAL-04 | Coaching 4 (30 min) | ÉQUIPE | 2h | 2026-06-22 | 2026-06-26 | — | [ ] | Sem 8 |
| EVAL-05 | Rencontres suivi-technique (45 min × 6) | ÉQUIPE | 30h | 2026-05-18 | 2026-08-14 | — | [ ] | Tableau de bord le jeudi avant 8h |
| EVAL-06 | Audit d'équipe S6 (1h, tous présentent) | ÉQUIPE | 24h | 2026-07-13 | 2026-07-24 | — | [ ] | Annexe R |
| EVAL-07 | Évaluation par les pairs (PME × 3) | INDIV | 6h | 2026-05-25 | 2026-08-14 | — | [ ] | Module les notes d'équipe |
| EVAL-08 | RAE (rapport d'auto-évaluation) | INDIV | 14h | 2026-08-03 | 2026-08-14 | — | [ ] | Annexe X |

> **Rencontres hebdomadaires (dès sem 3) :** tableau de bord (2-3 p. PDF) déposé dans Teams **le jeudi avant 8h** — voir contenu détaillé en Partie 3.

## S7 — PMC760 (hiver 2027)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| S7-01 | Rencontres de suivi (30 min × 10) | ÉQUIPE | 20h | 2027-01-05 | 2027-04-30 | — | [ ] | Tableau de bord hebdo |
| S7-02 | Rencontres techniques (60 min × 10) | ÉQUIPE | 40h | 2027-01-05 | 2027-04-30 | — | [ ] | Présentation PowerPoint Teams |
| S7-03 | Audits d'équipe (× 2) | ÉQUIPE | 40h | 2027-02-15 | 2027-04-09 | — | [ ] | Tous présentent (Annexe R) |
| S7-04 | Audit numérique individuel (vidéo 10 min) | INDIV | 20h | 2027-04-05 | 2027-04-23 | — | [ ] | Annexe S |
| S7-05 | Évaluations par les pairs (PME × 3) | INDIV | 6h | 2027-01-05 | 2027-04-30 | — | [ ] | |
| S7-06 | RAE | INDIV | 14h | 2027-04-19 | 2027-04-30 | — | [ ] | Annexe X |
| S7-07 | **RPC2** (max 80 p. avec annexes) | ÉQUIPE | 200h | 2027-03-01 | 2027-04-26 | S7-T06 | [ ] | Annexe U — conception détaillée + plan d'essais. `git tag RPC2` |

> **RPC2 (Annexe U) :** (1) description technique (architecture, modules, choix, fabrication, validation) ; (2) suivi de gestion (finances, heures, écarts, projection S8) ; (3) annexes (code tag Git, plans, calculs).

## S8 — PMC860 (automne 2027)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| S8-01 | Rencontres suivi-technique (45 min × 10) | ÉQUIPE | 30h | 2027-08-30 | 2027-12-11 | — | [ ] | |
| S8-02 | Audit d'équipe (× 1) | ÉQUIPE | 24h | 2027-10-11 | 2027-10-22 | — | [ ] | |
| S8-03 | Audit numérique individuel (vidéo 10 min) | INDIV | 20h | 2027-11-29 | 2027-12-11 | — | [ ] | |
| S8-04 | Évaluations par les pairs (PME × 3) | INDIV | 6h | 2027-08-30 | 2027-12-11 | — | [ ] | |
| S8-05 | RAE | INDIV | 14h | 2027-12-07 | 2027-12-18 | — | [ ] | |
| S8-06 | **RLP** (rapport de livraison de projet) | ÉQUIPE | 80h | 2027-11-01 | 2027-12-11 | S8-T09 | [ ] | Annexe W |
| S8-07 | **Expo MégaGÉNIALE** (démo publique) | ÉQUIPE | 40h | 2027-11-27 | 2027-11-28 | S8-T13 | [ ] | ⚠️ **27-28 nov. à confirmer (comité/Teams)**. Sondage info-projet ≤ 15 sept |
| S8-08 | Avis de fin de projet (Annexe J) | ÉQUIPE | 4h | 2027-12-18 | 2027-12-23 | S8-T13 | [ ] | Remis avant midi dernier jour — IN si manquant |

---

# PARTIE 2 — Développement technique (par bloc)

> 6 blocs + fondations transversales + intégration finale. Chaque bloc avance **en parallèle** grâce aux interfaces gelées (`TECH-02`).
> **Dépendances inter-blocs (vue d'équipe) :** Boîtier(interne) → PCB → [benchmark Engine+Audio → MCU] ; Engine ↔ Audio (interface commune) ; Jeu → Engine+Audio ; IDE → indépendant (jusqu'à l'intégration USB).

## Bloc 0 — Fondations & interfaces (transversal)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-01 | Contrats d'interface (Input, Audio, Haptic, Storage, MiniGame) | ENG | 40h | 2026-05-04 | 2026-05-11 | — | [ ] | **Phase 0 — fondation de tout le projet** |
| TECH-02 | **Gel des interfaces** (revue croisée) | TOUTES | 8h | 2026-05-11 | 2026-05-15 | TECH-01 | [ ] | Tout changement futur = accord des 2 équipes |
| TECH-03 | Achat manettes USB (2-3 PS4/Xbox) | ENG | 4h | 2026-05-04 | 2026-05-15 | — | [ ] | ~60$ |
| TECH-04 | Setup du repo (structure, build, conventions) | ENG | 16h | 2026-05-04 | 2026-05-15 | — | [ ] | Document de conventions |

## Bloc 1 — Game Engine (ENG) · *Flux A*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-05 | GamepadMapper (USB → InputState) | ENG | 40h | 2026-05-11 | 2026-05-29 | TECH-02,TECH-03 | [ ] | 1ʳᵉ implé. de l'interface Input |
| TECH-06 | StubAudio + StubHaptic (logs, sans HW) | ENG | 24h | 2026-05-11 | 2026-05-29 | TECH-02 | [ ] | Tester la logique sans son |
| TECH-09 | Système de scènes (create/load/unload/transition) | ENG | 40h | 2026-05-25 | 2026-06-12 | TECH-04 | [ ] | Sur PC |
| TECH-10 | Monde 2D+Z (grille, entités sonores) | ENG | 40h | 2026-05-25 | 2026-06-12 | TECH-09 | [ ] | Sur PC |
| TECH-11 | Déplacement joueur (joystick gauche) | ENG | 32h | 2026-06-01 | 2026-06-19 | TECH-05,TECH-10 | [ ] | |
| TECH-12 | Système de collisions (murs, obstacles) | ENG | 32h | 2026-06-01 | 2026-06-19 | TECH-10 | [ ] | |
| GE-01 | **Jeu V1 sur PC** (test d'engine jouable) | ENG | 48h | 2026-06-15 | 2026-07-10 | TECH-11,TECH-12,TECH-13 | [ ] | **Livrable « blitz » S6** — valide l'engine + audio de base |
| GE-02 | Raffinement engine + harness de benchmark | ENG | 60h | 2026-09-08 | 2026-12-18 | GE-01 | [ ] | **Stage T4** — prépare le benchmark de S7 |
| S7-T02 | Bâton d'aveugle (raycast + haptique directionnel) | ENG | 48h | 2027-01-05 | 2027-01-29 | TECH-12 | [ ] | |
| S7-T03 | Intégration PCAudio dans le game engine | ENG | 32h | 2027-01-15 | 2027-01-22 | S7-T01,TECH-09 | [ ] | Son spatial au casque |
| S7-T04 | **Benchmark du jeu sur PC** (CPU/RAM/sources/latence) | ENG+AUD | 40h | 2027-01-22 | 2027-01-29 | S7-T03,S7-T01,GE-02 | [ ] | **⚑ AVANCÉ (était S7 sem 6-8). Clé du choix MCU** |
| S7-T05 | Estimation des besoins MCU (à partir du benchmark) | AUD+ENG | 16h | 2027-01-29 | 2027-02-02 | S7-T04 | [ ] | Comparer aux MCU candidats |
| S7-T06 | **◆ DÉCISION : choix du microcontrôleur ◆** | TOUTES | 16h | 2027-02-02 | 2027-02-08 | S7-T05,TECH-18,MIP-08 | [ ] | **Jalon pivot — convergence A+B+C.** Doc de justification quantitatif |
| S7-T11 | Intégration MicroPython (firmware) | ENG | 60h | 2027-02-08 | 2027-03-12 | S7-T06 | [ ] | |
| S7-T12 | Protocole USB CDC (spec + implé.) | ENG | 40h | 2027-02-08 | 2027-03-12 | — | [ ] | Alimente l'IDE (S7-T15) |
| S8-T04 | NathanMapper + NathanHaptic (manette réelle) | ENG | 48h | 2027-09-13 | 2027-10-22 | S8-T01 | [ ] | Swap d'implémentation Input/Haptic |
| S8-T05 | Intégration audio embarqué dans le game engine | ENG | 40h | 2027-09-27 | 2027-10-29 | S8-T02,S8-T04 | [ ] | |

## Bloc 2 — Audio HRTF (AUD) · *Flux B*

> **Stratégie audio (2 temps) :** le benchmark initial s'appuie sur des **librairies existantes** (I/O playback + une lib de spatialisation **de référence**) pour obtenir vite des chiffres de dimensionnement MCU — **mais le livrable est NOTRE propre librairie de son spatial** (convolution HRTF maison). C'est le seul moyen d'avoir le contrôle requis pour le portage embarqué et l'optimisation temps réel sur MCU.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-07 | Recherche HRTF (datasets MIT KEMAR, CIPIC, SOFA) | AUD | 24h | 2026-05-11 | 2026-05-29 | — | [ ] | Tableau comparatif |
| TECH-08 | Choix lib audio PC : **I/O playback** (miniaudio…) + lib spatialisation **de référence** | AUD | 16h | 2026-05-11 | 2026-05-22 | — | [ ] | Lib existante = I/O + baseline benchmark ; **pas** la spatialisation finale |
| TECH-13 | **Notre lib de son spatial** — proto 1 source (convolution HRTF maison) | AUD | 40h | 2026-05-18 | 2026-06-05 | TECH-08,TECH-07 | [ ] | Son qui tourne au casque |
| TECH-14 | **Notre lib** — multi-sources (4-6 sur PC) | AUD | 60h | 2026-06-01 | 2026-07-03 | TECH-13 | [ ] | |
| AU-01 | Benchmark conso/perf — **lib de référence + notre proto** | AUD | 32h | 2026-07-06 | 2026-07-31 | TECH-14 | [ ] | **Blitz S6** — chiffres pour le MCU ; comparer référence vs maison |
| AU-02 | Pré-décision : audio sur MCU vs module séparé | AUD | 16h | 2026-07-27 | 2026-08-14 | AU-01 | [ ] | **Orientation** (décision formelle = S7-T07) |
| AU-03 | Maturation de **notre lib** (multi-source robuste, interpolation, distance) | AUD | 80h | 2026-09-08 | 2026-12-18 | TECH-14 | [ ] | **Stage T4** — rend l'audio « benchmark-ready » |
| S7-T01 | **Notre librairie de son spatial — complète** (contrat SpatialAudioEngine) | AUD | 60h | 2027-01-05 | 2027-01-22 | AU-03 | [ ] | **Le vrai livrable audio.** Front-load pour permettre S7-T04 |
| S7-T07 | **DÉCISION audio : software pur / DSP externe / FPGA-CPLD maison** | AUD+ELEC | 8h | 2027-02-08 | 2027-02-12 | S7-T06,AU-02 | [ ] | **⚑ AVANCÉ.** Critère = benchmark (`S7-T04`/`S7-T05`). Si MCU insuffisant → option matérielle (Bloc 2b), informée par `AUDHW-01` |
| S8-T02 | Portage de **notre lib de son spatial** sur le MCU choisi | AUD | 100h | 2027-08-30 | 2027-10-09 | S7-T06,S7-T07,S8-T01 | [ ] | Le plus complexe. **Remplacé par le Bloc 2b si l'option FPGA est retenue à `S7-T07`** |

### Bloc 2b — Option conditionnelle : décharge audio matérielle (FPGA/CPLD)

> **⚠️ Option CONDITIONNELLE — repli ultime de `H-07`.** À n'activer **que si** le benchmark (`S7-T04`) + l'estimation MCU (`S7-T05`) montrent qu'**aucun MCU abordable ne suffit**. La décision se prend à `S7-T07`. Principe : déporter la convolution HRTF dans un **FPGA/CPLD** (calcul parallèle) — le MCU ne fait plus que streamer les échantillons. **Possible uniquement parce que le moteur audio est maison** (`S7-T01`) : on ne grave en logique qu'un algorithme que l'on maîtrise. C'est une **3ᵉ implémentation du contrat `SpatialAudioEngine`** (à côté de `PCAudio` et `EmbeddedAudio`) → absorbée par l'architecture en interfaces. **Si activée, ces tâches REMPLACENT `S8-T02`** (le MCU ne calcule plus le HRTF). Détails : `ESTIMATION.md` §2.6/§4.2.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| AUDHW-01 | Étude de faisabilité : dimensionner le FIR HRTF en logique (taps × sources × ressources FPGA) | AUD+ELEC | 40h | 2027-02-02 | 2027-02-08 | S7-T05 | [ ] | **Conditionnel** — alimente la décision `S7-T07` |
| AUDHW-02 | Choix du composant : FPGA/CPLD (iCE40 UP5K…) vs DSP tout-fait + ajout au BOM | ELEC | 16h | 2027-02-12 | 2027-02-19 | S7-T07 | [ ] | **Si `S7-T07` retient le matériel.** À trancher tôt pour que le schéma `S7-T17` intègre le FPGA |
| AUDHW-03 | Implémentation HDL du moteur HRTF (convolution parallèle, Verilog/VHDL) + simulation | AUD+ELEC | 160h | 2027-02-22 | 2027-09-18 | S7-T01,AUDHW-02 | [ ] | **Effort principal.** Toolchain open-source yosys/nextpnr (`C-25`). Couvre S7 → stage T5 → début S8 |
| AUDHW-04 | Interface de streaming MCU → FPGA (protocole + DMA/I2S) | ENG+ELEC | 48h | 2027-08-30 | 2027-09-25 | AUDHW-02 | [ ] | **Nouvelle interface à geler** |
| AUDHW-05 | Intégration du module audio matériel sur le PCB + tests électriques | ELEC | 40h | 2027-09-27 | 2027-10-15 | S8-T01,AUDHW-03,AUDHW-04 | [ ] | Impacte `S7-T17`/`S7-T18` (le PCB doit prévoir l'empreinte/alim du FPGA) |
| AUDHW-06 | Validation A/B : qualité/latence vs version logicielle | AUD+ENG | 24h | 2027-10-18 | 2027-10-29 | AUDHW-05 | [ ] | Critère : latence < 20 ms (extrant `E5`) |

## Bloc 3 — PCB / Électronique (ELEC) · *Flux C (électronique)*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-18 | Recensement MCU candidats (ESP32-S3, RP2350, STM32H7…) | ELEC | 24h | 2026-06-08 | 2026-07-03 | — | [ ] | **Avancé** (blitz). Alimente MIP-08 |
| PCB-01 | Définition de l'interface des contrôles (E/S) | ELEC | 24h | 2026-06-08 | 2026-06-26 | TECH-01 | [ ] | **S6** — indépendant du MCU |
| PCB-02 | Conception préliminaire du BMS (batterie + murale) | ELEC | 40h | 2026-06-22 | 2026-07-24 | — | [ ] | **S6** — faisable avant le choix MCU |
| PCB-03 | Section alim. + connecteurs + lib. d'empreintes | ELEC | 40h | 2026-09-08 | 2026-12-18 | PCB-01,PCB-02 | [ ] | **Stage T4** — tout le pré-travail indépendant du MCU |
| S7-T08 | Breadboard MCU (valider I2S, ADC, PWM, USB) | ELEC | 48h | 2027-02-08 | 2027-03-05 | S7-T06 | [ ] | |
| S7-T17 | Schéma KiCAD v2.0 complet | ELEC | 60h | 2027-02-15 | 2027-03-19 | S7-T06,S7-T08,PCB-03 | [ ] | **⚑ AVANCÉ** (était sem 10-13) |
| S7-T18 | Layout PCB + commande de fabrication | ELEC | 48h | 2027-03-08 | 2027-04-02 | S7-T17 | [ ] | **⚑ AVANCÉ** |
| PCB-04 | Fabrication PCB (délai externe JLCPCB) | ELEC | 8h | 2027-03-29 | 2027-04-23 | S7-T18 | [ ] | **2-3 sem incompressibles** (`H-16`) — commander tôt |
| S8-T01 | Soudure PCB + tests électriques | ELEC | 40h | 2027-08-30 | 2027-09-18 | PCB-04 | [ ] | |

## Bloc 4 — Boîtier (ELEC / méca) · *Flux C (mécanique)*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| BOI-01 | Mockup CAD de la coque (extérieur + ergonomie) | ELEC | 40h | 2026-06-08 | 2026-07-03 | — | [ ] | **S6** — pulled early. Aucune dépendance (extérieur seulement) |
| BOI-02 | Itérations d'impression de la coque (sans interne) | ELEC | 32h | 2026-06-29 | 2026-07-31 | BOI-01 | [ ] | **S6** — itérer l'ergonomie de la main |
| BOI-03 | Polish ergonomie + consultations DV | ELEC | 24h | 2026-09-08 | 2026-12-18 | BOI-02,COM-05 | [ ] | **Stage T4** — test de polish, retours DV |
| BOI-04 | Conception interne (supports PCB/batterie/moteurs) | ELEC | 40h | 2027-03-08 | 2027-04-09 | S7-T18 | [ ] | **Dépend du PCB** (dimensions/positions) |
| S8-T03 | Impression 3D finale + assemblage complet | ELEC | 32h | 2027-09-13 | 2027-10-01 | S8-T01,BOI-04 | [ ] | |

## Bloc 5 — Jeu & Contenu (JEU) · *Flux D*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| JEU-01 | Conception papier du jeu complet (sprites/scènes/map/mini-jeux/sons) | JEU | 40h | 2026-05-11 | 2026-06-12 | — | [ ] | **S6** — permet le dev parallèle dès S7 |
| TECH-15 | Design de la carte (plan coté 2D) | JEU | 24h | 2026-05-11 | 2026-05-29 | JEU-01 | [ ] | Dimensions, positions des murs |
| TECH-16 | Liste des sons (inventaire exhaustif) | JEU | 16h | 2026-05-18 | 2026-06-05 | JEU-01 | [ ] | |
| TECH-17 | Banque de sons (production interne + CC0) | JEU | 120h | 2026-05-25 | 2026-12-18 | TECH-16 | [ ] | Long, parallélisable — **continue en stage T4** |
| S7-T09 | Développement des zones (Salon, Cuisine, Chambre, Musique) | JEU | 120h | 2027-01-05 | 2027-03-12 | TECH-09,TECH-12,S7-T01 | [ ] | Avec GamepadMapper + PCAudio |
| S7-T10 | Narration audio (enregistrement des voix) | JEU | 40h | 2027-01-25 | 2027-02-26 | JEU-01 | [ ] | |
| S8-T06 | École + mini-jeux d'exemple (zone extérieure) | JEU | 48h | 2027-09-13 | 2027-10-22 | S7-T11,S7-T09 | [ ] | |
| S8-T10 | Test utilisateur DV (protocole CER approuvé) | JEU | 24h | 2027-10-18 | 2027-10-29 | S8-T09,ETH-05 | [ ] | Groupe recruté via l'APHVE |

## Bloc 6 — IDE accessible (ENG) · *Flux E*

> **Changement vs plan initial :** l'IDE **démarre en S7** (et non S6) — décision d'équipe pour concentrer S6 sur le blitz engine+audio. Aucune dépendance matérielle jusqu'à l'intégration USB.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-19 | Choix du stack (Electron/React, Tauri…) | ENG | 24h | 2027-01-05 | 2027-01-15 | — | [ ] | **Déplacé de S6 → S7.** Critère : accessibilité |
| IDE-01 | Mockups interface (avec AI) | ENG | 24h | 2027-01-05 | 2027-01-22 | — | [ ] | |
| IDE-02 | TTS/STT + test isolé des fonctionnalités AI | ENG | 48h | 2027-01-18 | 2027-02-12 | IDE-01 | [ ] | Codage vocal : entrée STT, retour TTS |
| IDE-03 | Estimation des coûts (services AI cloud) | ENG | 8h | 2027-01-18 | 2027-01-29 | IDE-02 | [ ] | |
| IDE-04 | Résolution dépendance backend/frontend | ENG | 16h | 2027-01-25 | 2027-02-12 | TECH-19 | [ ] | Lève la dépendance interne de l'IDE |
| TECH-20 | Prototype éditeur (coloration μPython, explorateur) | ENG | 48h | 2027-01-11 | 2027-02-12 | TECH-19 | [ ] | Valider le stack |
| S7-T14 | Accessibilité (TTS, ARIA, navigation clavier) | ENG | 60h | 2027-01-25 | 2027-02-26 | TECH-20,IDE-02 | [ ] | **Priorité : utilisable par une personne DV** |
| S7-T15 | Transfert USB (client CDC : LIST/UPLOAD/DELETE/LOG) | ENG | 40h | 2027-02-22 | 2027-03-26 | S7-T12 | [ ] | Dépend du protocole CDC |
| S7-T16 | Gestionnaire de mini-jeux (liste, upload) | ENG | 40h | 2027-03-08 | 2027-04-09 | S7-T15 | [ ] | |
| S8-T07 | Tests d'intégration (écrire → transférer → jouer) | ENG | 32h | 2027-09-27 | 2027-10-29 | S8-T01,S7-T16 | [ ] | Avec la console réelle |
| S8-T08 | Polish et accessibilité finale | ENG | 40h | 2027-10-11 | 2027-11-06 | S8-T07 | [ ] | Tests lecteur d'écran, doc utilisateur |

## Bloc 7 — Intégration système & clôture (transversal, S8)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| S8-T09 | Tests d'intégration complets (matériel réel) | TOUTES | 32h | 2027-10-11 | 2027-10-22 | S8-T05,S8-T03,S8-T07 | [ ] | **◆ Console complète** |
| S8-T11 | Ajustements post-tests | TOUTES | 32h | 2027-10-25 | 2027-11-06 | S8-T10 | [ ] | |
| S8-T12 | Optimisation et profiling | ENG+AUD | 24h | 2027-10-18 | 2027-11-06 | S8-T09 | [ ] | |
| S8-T13 | Préparation Expo MégaGÉNIALE (kiosque, démo) | TOUTES | 40h | 2027-11-01 | 2027-11-26 | S8-T11 | [ ] | |
| S7-T19 | Soumission au CER (formulaire d'avis) | ÉQUIPE | — | 2027-01-05 | 2027-01-23 | — | [ ] | = ETH-02. ≥ 4 sem avant test DV |
| S7-T20 | Soumission du protocole d'essai (superviseur) | ÉQUIPE | — | 2027-09-27 | 2027-10-02 | — | [ ] | = ETH-05. ≥ 2 sem avant test DV |

---

# PARTIE 3 — Chronologie, jalons et chemins critiques

## Réconciliation capacité ↔ charge planifiée

| Période | Capacité équipe | Charge planifiée (est.) | Marge | Lecture |
|---------|-----------------|-------------------------|-------|---------|
| **S6** | 945 h | **~945 h** | ~0 h | ⚠️ **Tendu** : MIP + RPC1 **et** blitz engine/audio dans une session de 3 cr |
| **T4** (stage) | ~420 h | ~350 h | ~70 h | Absorbe le débordement S6 + travail parallélisable |
| **S7** | 1890 h | ~1350 h | ~540 h | Session lourde (6 cr) mais marge confortable |
| **T5** (stage) | ~420 h | ~300 h | ~120 h | Finalisation contenu + préparation portage |
| **S8** | 945 h | ~650 h | ~295 h | Intégration + tests + Expo + RLP |

> **⚠️ Risque principal : S6 est saturée.** Deux livrables académiques majeurs (MIP **et** RPC1) tombent dans la même session de 135 h/pers, en plus du blitz technique. **Mitigations intégrées :** (1) l'IDE est déplacé en S7 (libère ~150 h en S6) ; (2) la production de sons (`TECH-17`), la maturation audio (`AU-03`), le polish boîtier (`BOI-03`) et le pré-travail PCB (`PCB-03`) sont **reportés sur le stage T4** ; (3) prioriser : MIP/RPC1 = échéances dures, le blitz vise le **cœur** engine+audio (`GE-01`, `AU-01`), le reste glisse en T4 si nécessaire.

## Jalons de convergence

| Jalon | Quand (date) | Ce qui converge | Ce qui est débloqué |
|-------|--------------|-----------------|---------------------|
| **Interfaces gelées** | 2026-05-15 (S6 s2) | Tous les flux démarrent | Développement parallèle sur tous les blocs |
| **Jeu V1 jouable sur PC** | 2026-07-10 (S6 s10) | Engine + audio de base + GamepadMapper | Démos, consultations DV, premier benchmark |
| **« Benchmark-ready »** | 2027-01-05 (S7 s1) | PCAudio mûr (T4) + engine raffiné (T4) | Benchmark formel immédiat |
| **◆ Choix du MCU ◆** | **~2027-02-08 (S7 s5)** | Benchmark (A) + besoins audio (B) + analyse MCU (C) | Breadboard, schéma, PCB, portage. **⚑ ~3 sem plus tôt qu'au plan initial (sem 8-9)** |
| **Manette NATHAN opérationnelle** | ~2027-10-09 (S8 s6) | PCB soudé + boîtier + NathanMapper/Haptic + audio embarqué | **Transition : on lâche la manette Xbox** |
| **Console complète** | ~2027-10-22 (S8 s8) | Manette + engine porté + jeu + IDE | Tests d'intégration, tests DV formels |
| **Expo MégaGÉNIALE** | **2027-11-27/28** *(à confirmer)* | Tout | Démonstration publique |

## Architecture en blocs et interfaces

```
┌──────────────────────────────────────────────────────────────────┐
│                        GAME ENGINE (C/C++)                       │
│    Scènes, Collisions, Bâton, Navigation, Logique de jeu        │
│    ┌──────────┐  ┌──────────────┐  ┌───────────┐  ┌──────────┐ │
│    │ InputMap │  │ SpatialAudio │  │ HapticEng │  │ Storage  │ │
│    │ INTERFACE│  │  INTERFACE   │  │ INTERFACE │  │ INTERFACE│ │
│    └────┬─────┘  └──────┬───────┘  └─────┬─────┘  └────┬─────┘ │
└─────────┼───────────────┼────────────────┼──────────────┼────────┘
    ┌─────┴─────┐   ┌─────┴─────┐   ┌─────┴─────┐  ┌────┴─────┐
    │ Gamepad   │   │  PCAudio  │   │ Gamepad   │  │ PC File  │   PHASE PC
    │ Mapper    │   │  (HRTF)   │   │ Haptic    │  │ System   │   (S6→S7)
    └───────────┘   └───────────┘   └───────────┘  └──────────┘
          ↑ Même interface — swap d'implémentation ↓               PHASE MATÉRIEL
    ┌───────────┐   ┌───────────┐   ┌───────────┐  ┌──────────┐   (S8)
    │ Nathan    │   │ Embarqué  │   │ Nathan    │  │ SD Card  │
    │ Mapper    │   │ Audio     │   │ Haptic    │  │ FAT32    │
    └───────────┘   └───────────┘   └───────────┘  └──────────┘
```

**Le game engine ne sait jamais s'il parle à une manette Xbox ou à la manette NATHAN.** C'est ce qui permet de développer le jeu complet sur PC avant d'avoir choisi le microcontrôleur.

> L'interface `SpatialAudioEngine` admet une **3ᵉ implémentation conditionnelle** — `HardwareAudio` (FPGA/CPLD, **Bloc 2b**) — à côté de `PCAudio` (PC) et `EmbeddedAudio` (MCU). Le même contrat absorbe le repli matériel sans refonte.

## Flux parallèles (S6 → T4 → S7 → T5 → S8)

```
        S6 (été 26)      T4 (stage)     S7 (hiver 27)        T5 (stage)    S8 (aut. 27)
        ───────────      ──────────     ─────────────        ──────────    ────────────
ENG     interfaces       raffinement    bâton+benchmark      —             NathanMapper
        +mapper+engine   +harness       +intégration                       +audio embarqué
        +Jeu V1
AUD     proto→multi-src  maturation     PCAudio complet      —             portage MCU
        +benchmark prél. PCAudio        +DÉCISION audio
ELEC    MCU candidats    pré-travail    breadboard→schéma    —             soudure
(PCB)   +E/S+BMS prél.   PCB (alim.)    →layout→fab
ELEC    mockup CAD       polish +       conception interne   —             impression
(boît.) +impressions     consult. DV    (dépend PCB)                       +assemblage
JEU     design+sons      production     zones+narration      finition      école+mini-jeux
                         sons (suite)                        contenu       +tests DV
IDE     —                —              stack+AI+TTS/STT      raffinement   intégration
                                        +accessibilité+USB                 +polish
```

## Chemin critique (le plus long — hardware)

```
Interfaces gelées (2026-05-15)
 → Engine + Audio sur PC (S6 + maturation T4)
   → Benchmark PC (2027-01, S7 s3-4)
     → ◆ Choix MCU (2027-02-08, S7 s5)
       → Breadboard (S7 s6-9) → Schéma KiCAD (S7 s7-11) → Layout PCB (S7 s10-13)
         → Fabrication PCB (2-3 sem, externe) → Soudure+tests (S8 s1-3)
           → NathanMapper/Haptic + audio embarqué (S8 s3-6)
             → ◆ Transition manette (S8 s6) → Intégration (S8 s8)
               → Tests DV (S8 s8-9) → Expo (2027-11-27/28)
```

**Goulots non compressibles :** benchmark PC (bloque le MCU) · choix MCU (convergence A+B+C) · fabrication PCB (délai externe, `H-16`) · portage audio embarqué (`S8-T02`, le plus complexe) · approbation CER (≥ 4 sem, soumettre dès S7) · **[conditionnel]** décharge audio matérielle (`AUDHW-03/04/05`) si activée à `S7-T07` — devient un **sous-chemin critique parallèle** entre le choix MCU et l'intégration S8, et **contraint le schéma/layout PCB** (le FPGA doit y être prévu).

## Transition manette Xbox → NATHAN (S8, swap d'implémentation)

Conditions : PCB soudé (`S8-T01`) · NathanMapper/Haptic (`S8-T04`) · audio embarqué (`S8-T02`/`S8-T05`) · boîtier assemblé (`S8-T03`). **Incrémentale :** Input → Haptic → Audio → Storage.

---

## Pondérations des livrables (Annexe L)

**PMC660 (S6) :** MIP 6 % · RPC1 9 % · Audit d'équipe 15 % · Rencontres techniques 30 % · RAE 5 %.
**PMC760 (S7) / PMC860 (S8) :** pondérations similaires — voir Annexe L pour les valeurs exactes.

## Tableau de bord hebdomadaire (dès S6 sem 3, jeudi avant 8h)

Nom/date/photos+rôles · objectifs projet & session · ordre du jour · tâches faites/en cours/à venir · courbe en S ou burndown · heures/membre · taux d'atteinte · suivi des risques · protocoles d'essais · état des dépenses · problèmes · sujet rencontre technique.

## Checklist des livrables par session

**S6 :** Annexes A/D/E/H · contrat d'équipe · modalités partenariat (SARIC) · MIP (≤20 p.) · RPC1 (≤35 p.) · RAE · tableaux de bord · présentations techniques.
**S7 :** RPC2 (≤80 p.) · RAE · audit numérique · convention partenariat (si pas faite) · CER + protocole soumis · code tagué (`git tag RPC2`).
**S8 :** RLP · RAE · audit numérique · avis de fin de projet (Annexe J) · démo Expo MégaGÉNIALE · prototype fonctionnel livré.

---

## Notes de révision (à valider par l'équipe — points de jugement)

1. **Décision MCU avancée (~S7 sem 5 / début février au lieu de sem 8-9 / fin février-début mars).** Justifiée par le blitz S6 + la maturation audio/engine pendant le stage T4 → on arrive « benchmark-ready » au début de S7. **À valider :** réaliste seulement si `AU-03` et `GE-02` avancent vraiment pendant T4.
2. **Boîtier (extérieur) pulled en S6** (`BOI-01/02`) ; **interne** reste dépendant du PCB (`BOI-04`, S7). Conforme à votre découpe « extérieur sans interne ».
3. **IDE déplacé en S6 → S7** (votre décision : « IDE S6 = rien »). Libère ~150 h en S6 mais resserre légèrement l'IDE ; reste faisable (pas de dépendance matérielle avant l'USB).
4. **Capacité de stage : 4 h/sem/pers** (~60 h/pers, ~420 h équipe nominal) — appliquée surtout au chemin critique et au travail parallélisable. Charge réellement planifiée en T4/T5 < capacité nominale.
5. **Estimations horaires** dérivées des totaux par flux de `ESTIMATION.md` (± 20 %). À affiner par les responsables de bloc.
6. **Dates de dépôt MIP/RPC1 et dates exactes d'audits** : placées selon les semaines du guide — **⚠️ à confirmer sur Teams**.
7. **Date Expo (27-28 nov. 2027)** : fournie par l'équipe (comité organisateur) ; le guide ne la fixe pas — **à confirmer sur Teams**.
8. **Librairie de son spatial maison = livrable clé.** Le benchmark initial utilise des librairies existantes (I/O + spatialisation de référence) pour dimensionner le MCU, mais l'objectif est **notre propre lib HRTF** : `TECH-13` → `TECH-14` → `AU-03` → `S7-T01` → portage `S8-T02`. Plus d'effort/risque qu'une lib clé en main — déjà reflété dans le flux audio (~560 h) et les fallbacks `H-07`.
9. **Option audio matérielle FPGA/CPLD = branche conditionnelle** (Bloc 2b, `AUDHW-01..06`). Repli ultime de `H-07` : à activer **seulement si** `S7-T04`/`S7-T05` montrent qu'aucun MCU abordable ne suffit (décision élargie à `S7-T07`). Si activée : **remplace `S8-T02`**, ajoute **~330 h** (surtout HDL) à financer via la contingence / arbitrage de portée, et **contraint le calendrier PCB** (le FPGA doit être prévu au schéma `S7-T17`). Décision consignée dans **[ADR-0004](../decisions/0004-option-repli-audio-fpga.md)** ; détail chiffré dans `ESTIMATION.md` §2.6/§4.2. Reste à synchroniser `HYPOTHESES.md` (`H-07`) avec l'ADR.

---

*Document vivant — à mettre à jour chaque semaine dans le tableau de bord. Prochaine étape : revue d'équipe (2 j) → import JIRA (génération CSV depuis ce fichier).*
