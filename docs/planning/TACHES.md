# Tâches et Chronologie — Projet NATHAN Console v2.0

**Date :** 2026-06-07
**Session :** PMC660 (S6, E2026) — **semaine 6** (semaine du 8 juin 2026)
**Révision :** GANTT re-calé sur **aujourd'hui** (8 juin) : aucune tâche non terminée n'est datée dans le passé. Séquence S6 = **MIP d'abord (formative 11 juin, finale 18 juin), puis blitz technique (audio + game engine) à partir de la semaine 8**. Dates de coachings/livrables alignées sur l'**Annexe M** (horaires-types) ; pondérations sur l'**Annexe L**.

> Ce document regroupe **toutes** les tâches du projet : administratives, académiques et techniques.
> Il suit la logique réelle du projet et les exigences du guide étudiant PMC660-760-860.
> **Statut :** brouillon pour revue d'équipe (2 jours). « Export-CSV-ready » (1 tâche = 1 ligne avec ID, dépendances, dates) pour un import JIRA ultérieur.

---

## Légende

| Champ | Sens |
|-------|------|
| **ID** | Identifiant unique (clé des dépendances et de l'import JIRA) |
| **Tâche** | Description courte |
| **Rôle** | `ENG` (logiciel/engine/IDE), `AUD` (audio HRTF), `ELEC` (électronique/PCB/méca), `JEU` (contenu), `ÉQUIPE`, `INDIV`, `GESTION` |
| **Est.** | Effort en **heures-équipe** (± 20 %, `H-14`) |
| **Début / Fin** | Dates planifiées (ISO `AAAA-MM-JJ`) |
| **Dépend de** | ID(s) prédécesseur(s) — `—` si aucune |
| **Statut** | `[ ]` à faire · `[x]` fait · `~~…~~` annulé/déplacé |

**Schéma des ID** — Tâches existantes : `ADM-`, `PART-`, `COM-`, `ETH-`, `MIP-`, `RPC1-`, `TECH-`, `S7-T`, `S8-T`, `EVAL-`. Tâches ajoutées : préfixe de bloc `GE-`, `AU-`, `PCB-`, `BOI-`, `JEU-`, `IDE-`, `AUDHW-`.

---

## Calendrier de référence

| Période | Code | Type | Début | Fin | Capacité/pers | Capacité équipe (7) |
|---------|------|------|-------|-----|---------------|---------------------|
| Été 2026 | **S6** | Session PMC660 (3 cr) | 2026-05-04 | 2026-08-14 | 9 h/sem (135 h) | **945 h** |
| Automne 2026 | **T4** | **Stage** | 2026-09-08 | 2026-12-18 | ~4 h/sem (~60 h) | **~420 h** (réduit) |
| Hiver 2027 | **S7** | Session PMC760 (6 cr) | 2027-01-05 | 2027-04-30 | 18 h/sem (270 h) | **1890 h** |
| Été 2027 | **T5** | **Stage** | 2027-05-03 | 2027-08-13 | ~4 h/sem (~60 h) | **~420 h** (réduit) |
| Automne 2027 | **S8** | Session PMC860 (3 cr) | 2027-08-30 | 2027-12-23 | 9 h/sem (135 h) | **945 h** |

**⚠️ Re-calage au 8 juin.** Le plan est dressé en semaine 6. Les semaines 1-5 (mai → 5 juin) sont **passées** : seules les tâches réellement faites y restent (`[x]`). Tout le reste démarre **≥ 8 juin**. Conséquence : la S6 utile = **semaines 6-15 (~10 sem)**, dont 6-7 dédiées au MIP → le **technique ne démarre qu'en semaine 8** (22 juin).

**Repère semaines S6 ↔ dates (lundis) :** s3 05-18 · s4 05-25 · s5 06-01 · **s6 06-08** · s7 06-15 · **s8 06-22** · s9 06-29 · s10 07-06 · s11 07-13 · s12 07-20 · s13 07-27 · s14 08-03 · s15 08-10 (fin 08-14).
**Jalons fixes (Annexe M / équipe) :** Coachings #1-3 ✅ (s3/s4/s5) · **Coaching #4 = formative MIP, 11 juin (s6)** · **MIP final 18 juin (s7)** · Audit d'équipe s14 · Audit numérique + RPC1 + RAE s15.

---

# PARTIE 1 — Gestion & Académique

> Piloté par des **échéances** → organisé par session.

## S6 — PMC660 (été 2026)

### 1A. Formalités contractuelles et légales

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| ADM-01 | Cession de droits (Annexe A), par membre | INDIV | 2h | 2026-06-08 | 2026-06-12 | — | [ ] | Obligatoire — IN si manquant |
| ADM-02 | Entente de confidentialité (Annexe D) | INDIV | 1h | 2026-06-08 | 2026-06-12 | — | [ ] | Obligatoire — IN si manquant |
| ADM-03 | Autorisation photos/vidéos (Annexe E) | INDIV | 1h | 2026-06-08 | 2026-06-12 | — | [ ] | Obligatoire |
| ADM-04 | Engagement à la confidentialité (Annexe H) | INDIV | 1h | 2026-06-08 | 2026-06-12 | — | [ ] | Si infos confidentielles |
| ADM-05 | Contrat d'équipe (rôles, responsabilités) | ÉQUIPE | 12h | 2026-06-08 | 2026-06-15 | — | [ ] | Inclus dans le MIP (Annexe P) |
| ADM-06 | Dépôt des formulaires signés (SharePoint PMC) | GESTION | 3h | 2026-06-11 | 2026-06-17 | ADM-01,ADM-02,ADM-03 | [ ] | Vérifier liste livrables PMC660 |

### 1B. Partenariat APHVE (via SARIC)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| PART-01 | ~~Identifier un organisme partenaire~~ | GESTION | — | — | — | — | [x] | APHVE identifié |
| PART-02 | ~~Présenter le projet à l'APHVE~~ | GESTION | — | — | — | — | [x] | Acceptation reçue |
| PART-03 | Présenter le MIP à l'APHVE (valider le mandat) | ÉQUIPE | 6h | 2026-06-08 | 2026-06-12 | MIP-01 | [ ] | Confirme le mandat avant la convention |
| PART-04 | Modalités de partenariat (2 pages) | ÉQUIPE | 10h | 2026-06-08 | 2026-06-11 | — | [ ] | Prêtes à envoyer le 11 juin. 2 scénarios (Guide 2.1.2) |
| PART-05 | Signature des Modalités + courriel pmc-coordination | GESTION | 3h | 2026-06-11 | 2026-06-12 | PART-04 | [ ] | **Envoi le 11 juin** |
| PART-06 | Ouverture du dossier SARIC | — | 2h | 2026-06-11 | 2026-06-26 | PART-05 | [ ] | **Ouverture cette semaine (11 juin)** ; coaching SARIC en s6 ; délai de quelques semaines ensuite |
| PART-07 | Rencontre conseillère SARIC (convention) | ÉQUIPE | 4h | 2026-06-29 | 2026-07-24 | PART-06 | [ ] | Latence 1-2 sem entre étapes |
| PART-08 | Convention de partenariat (20-30 p., 3 parties) | TOUTES | 30h | 2026-07-27 | 2026-09-25 | PART-07 | [ ] | **Signée AVANT de léguer au partenaire.** Peut déborder en stage T4 |

### 1C. Communauté d'utilisateurs DV (Flux F)

> **Le recrutement formel via l'APHVE ne peut PAS précéder la convention signée** (`PART-08`). Seuls la préparation (Discord, processus) se fait avant. → Tout le flux DV glisse vers le **stage T4**.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| COM-01 | Serveur Discord accessible (lecteur d'écran) | ÉQUIPE | 8h | 2026-06-22 | 2026-06-26 | — | [ ] | Préparation — testable avec 1-2 pers. DV |
| COM-02 | Processus de recrutement (avec APHVE) | ÉQUIPE | 6h | 2026-06-22 | 2026-07-03 | COM-01 | [ ] | Critères définis avec l'APHVE (préparation) |
| COM-03 | Recrutement ≥ 5 personnes DV | ÉQUIPE | 20h | 2026-09-28 | 2026-10-23 | PART-08,COM-02 | [ ] | **Après la convention signée** → stage T4 |
| COM-04 | 1ʳᵉ consultation (besoins et attentes) | ÉQUIPE | 12h | 2026-10-26 | 2026-11-20 | COM-03 | [ ] | T4 — documenter le feedback |
| COM-05 | Consultations régulières (≥ 3 sur le projet) | ÉQUIPE | 30h | 2026-10-26 | 2027-12-11 | COM-04 | [ ] | Continue T4 → S7 → S8 (proto PC, proto matériel) |
| COM-06 | Tests utilisateurs formels (protocole CER) | ÉQUIPE | — | 2027-10-18 | 2027-10-29 | ETH-05,S8-T09 | [ ] | Voir S8-T10 — CER approuvé avant |

### 1D. Considérations éthiques (CER — tests avec personnes DV)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| ETH-01 | Prendre connaissance de l'outil d'aide CER | ÉQUIPE | 3h | 2026-06-22 | 2026-06-26 | — | [ ] | **Pas encore fait** — re-daté en s8. Lien sur le site PMC |
| ETH-02 | Formulaire de demande d'avis au CER | ÉQUIPE | 16h | 2027-01-05 | 2027-01-23 | ETH-01 | [ ] | ≥ 4 sem avant test (S8) — soumettre tôt |
| ETH-03 | Réponse du CER | — | — | 2027-01-26 | 2027-02-13 | ETH-02 | [ ] | 1-2 sem ; si CER complet → plus long |
| ETH-04 | Protocole d'essai (tests DV) | ÉQUIPE | 16h | 2027-09-13 | 2027-09-27 | ETH-03 | [ ] | ≥ 2 sem avant test — gabarit PMC |
| ETH-05 | Soumission du protocole au superviseur | ÉQUIPE | 2h | 2027-09-27 | 2027-10-02 | ETH-04 | [ ] | **Obligatoire avant toute expérimentation** |

> **Rappel :** tout essai du prototype (même partiel) exige un protocole d'essai préalablement validé (Guide 2.1.5).

### 2A. Rédaction du MIP — *finalisation cette semaine (s6), remise finale 18 juin (s7)*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| MIP-01 | Description du projet (situation actuelle/désirée) | ÉQUIPE | 12h | 2026-06-08 | 2026-06-11 | — | [ ] | Ébauché aux coachings 1-3 ; finalisation s6 |
| MIP-02 | Analyse de l'environnement (systèmes similaires) | ÉQUIPE | 10h | 2026-06-08 | 2026-06-11 | — | [ ] | Documenter les sources |
| MIP-03 | Analyse des parties prenantes | ÉQUIPE | 6h | 2026-06-08 | 2026-06-11 | — | [ ] | Ne PAS inclure les superviseurs (sauf si partenaire) |
| MIP-04 | Tableau du cadre logique (indicateurs mesurables) | ÉQUIPE | 8h | 2026-06-08 | 2026-06-11 | — | [ ] | Voir `CADRE-LOGIQUE.md` |
| MIP-05 | Analyse d'impact (social/environ./éco.) | ÉQUIPE | 6h | 2026-06-08 | 2026-06-11 | — | [ ] | Accessibilité, open-source, coût |
| MIP-06 | Recherche de systèmes similaires (état de l'art) | ÉQUIPE | 10h | 2026-06-08 | 2026-06-11 | — | [ ] | Métriques, aspects novateurs |
| MIP-07 | Diagramme d'architecture système (5 interfaces) | ÉQUIPE | 8h | 2026-06-08 | 2026-06-11 | — | [ ] | PC vs embarqué. Inclure l'IDE. Voir `docs/architecture/` |
| MIP-08 | Analyse préliminaire des MCU candidats (≥ 3) | ELEC | 12h | 2026-06-08 | 2026-06-11 | — | [ ] | **Préliminaire pour le MIP** (sans dépendre de TECH-18). Voir `ESTIMATION.md` |
| MIP-09 | Estimation budgétaire par scénario MCU | ELEC | 8h | 2026-06-08 | 2026-06-11 | MIP-08 | [ ] | Impact du MCU sur le budget |
| MIP-10 | Estimation de l'effort et calendrier | ÉQUIPE | 8h | 2026-06-08 | 2026-06-11 | — | [ ] | **Ce document** alimente MIP-10 |
| MIP-11 | Ressources financières et matérielles | ÉQUIPE | 4h | 2026-06-08 | 2026-06-11 | MIP-09 | [ ] | Budget ~500$ ventilé par bloc |
| MIP-12 | Risques principaux | ÉQUIPE | 6h | 2026-06-08 | 2026-06-11 | — | [ ] | HRTF, MCU, accessibilité IDE, ergonomie |
| MIP-13 | Stratégie de gestion retenue | ÉQUIPE | 4h | 2026-06-08 | 2026-06-11 | — | [ ] | Justifier (trad./agile/hybride) |
| MIP-14 | Conclusion et recommandations | ÉQUIPE | 4h | 2026-06-08 | 2026-06-11 | MIP-12 | [ ] | |
| MIP-15 | Références (sources complètes) | ÉQUIPE | 4h | 2026-06-08 | 2026-06-11 | — | [ ] | |
| MIP-16 | Contrat d'équipe (inclus au MIP) | ÉQUIPE | — | 2026-06-08 | 2026-06-11 | ADM-05 | [ ] | Voir ADM-05 |
| MIP-17 | Finalisation 90 % + **remise FORMATIVE** (Coaching #4) | ÉQUIPE | 12h | 2026-06-08 | 2026-06-11 | MIP-14 | [ ] | **Formative jeudi 11 juin** (≤ 20 p., TNR 12, interligne 1.5) |
| MIP-18 | **Dépôt FINAL du MIP** (canal Teams) | ÉQUIPE | 6h | 2026-06-15 | 2026-06-18 | MIP-17 | [ ] | **Jeudi 18 juin 23 h 59** |

> **À éviter :** expliquer la théorie du cadre logique ; remplir les catégories non pertinentes de l'Annexe P ; phrases creuses.

### 3A. Rédaction du RPC1 — *ateliers s8-13, remise fin de S6 (s15)*

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| RPC1-01 | Contexte, objectifs, requis, contraintes (MAJ MIP) | ÉQUIPE | 10h | 2026-06-22 | 2026-07-03 | MIP-18 | [ ] | Cadre logique à jour |
| RPC1-02 | Systèmes similaires et état de l'art | ÉQUIPE | 8h | 2026-06-22 | 2026-07-03 | MIP-06 | [ ] | Consoles access., jeux audio, HRTF |
| RPC1-03 | Concept global (schémas, blocs, images) | ÉQUIPE | 12h | 2026-06-22 | 2026-07-10 | MIP-07 | [ ] | Interfaces, PC vs embarqué |
| RPC1-04 | Description des modules (E/S, specs, tests) | ÉQUIPE | 16h | 2026-06-29 | 2026-07-17 | RPC1-03 | [ ] | Engine, Audio, HW, Jeu, μPython, IDE |
| RPC1-05 | Options évaluées et recommandation | ÉQUIPE | 10h | 2026-06-29 | 2026-07-17 | RPC1-04 | [ ] | Ex : MCU via benchmark. Lier aux ADR |
| RPC1-06 | Incertitudes et risques | ÉQUIPE | 8h | 2026-07-06 | 2026-07-24 | — | [ ] | |
| RPC1-07 | Critères de vérification (tests/module) | ÉQUIPE | 8h | 2026-07-06 | 2026-07-24 | RPC1-04 | [ ] | |
| RPC1-08 | WBS (2 niveaux dans le rapport) | ÉQUIPE | 8h | 2026-07-13 | 2026-07-24 | — | [ ] | Ou backlog si Agile |
| RPC1-09 | Planification temporelle (Gantt) | ÉQUIPE | 10h | 2026-07-13 | 2026-07-24 | MIP-10 | [ ] | **Ce document** = base du Gantt. S6→S8 |
| RPC1-10 | Interactions partenaire (fréquence, type) | ÉQUIPE | 3h | 2026-07-13 | 2026-07-24 | — | [ ] | |
| RPC1-11 | Livrables intermédiaires (dates) | ÉQUIPE | 3h | 2026-07-13 | 2026-07-24 | — | [ ] | Jalons de convergence (Partie 3) |
| RPC1-12 | Budget prévisionnel (± 10 %) | ÉQUIPE | 8h | 2026-07-13 | 2026-07-24 | MIP-11 | [ ] | Voir `ESTIMATION.md` |
| RPC1-13 | Analyse des risques (proba, impact, mitig.) | ÉQUIPE | 8h | 2026-07-13 | 2026-07-31 | RPC1-06 | [ ] | Inclure risques Expo |
| RPC1-14 | Sommaire et recommandations | ÉQUIPE | 4h | 2026-07-27 | 2026-08-07 | RPC1-13 | [ ] | |
| RPC1-15 | Références | ÉQUIPE | 4h | 2026-07-27 | 2026-08-07 | — | [ ] | |
| RPC1-16 | Relecture et mise en forme (max 35 p.) | ÉQUIPE | 16h | 2026-08-03 | 2026-08-12 | RPC1-14 | [ ] | Étudier le feedback MIP |
| RPC1-17 | **Dépôt du RPC1 + RAE** (canal Teams) | ÉQUIPE | 2h | 2026-08-13 | 2026-08-14 | RPC1-16 | [ ] | **Fin de S6 (s15)** — Annexe M |

### 3C. Activités d'évaluation S6

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| EVAL-01 | Coaching #1 (30 min) | ÉQUIPE | 2h | 2026-05-18 | 2026-05-22 | — | [x] | Fait (s3) |
| EVAL-02 | Coaching #2 (30 min) | ÉQUIPE | 2h | 2026-05-25 | 2026-05-28 | — | [x] | Fait — 28 mai (s4) |
| EVAL-03 | Coaching #3 (30 min) | ÉQUIPE | 2h | 2026-06-01 | 2026-06-05 | — | [x] | Fait (s5) |
| EVAL-04 | Coaching #4 — **évaluation formative du MIP** | ÉQUIPE | 2h | 2026-06-08 | 2026-06-11 | MIP-17 | [ ] | **11 juin (s6)** |
| EVAL-10 | FEPRAP (formulaire éval. préliminaire du risque) | ÉQUIPE | 2h | 2026-06-08 | 2026-06-12 | — | [ ] | Dû s4 (Annexe M) → **rattrapage s6**. Santé-sécurité |
| EVAL-05 | Rencontres suivi-technique (45 min × 6) | ÉQUIPE | 30h | 2026-06-22 | 2026-07-31 | — | [ ] | s8-13. Tableau de bord **jeudi avant 5 h 00** |
| EVAL-06 | Audit d'équipe S6 (1h, tous présentent) | ÉQUIPE | 24h | 2026-08-03 | 2026-08-07 | — | [ ] | **s14** (Annexe M). Annexe R |
| EVAL-09 | Audit numérique individuel S6 (vidéo 10 min) | INDIV | 20h | 2026-08-10 | 2026-08-14 | — | [ ] | **s15** (Annexe M, manquait). Annexe S |
| EVAL-07 | Évaluation par les pairs (PME × 3) | INDIV | 6h | 2026-06-08 | 2026-08-14 | — | [ ] | s6 / s11 / s15 (Annexe M). Module les notes |
| EVAL-08 | RAE (rapport d'auto-évaluation) | INDIV | 14h | 2026-08-10 | 2026-08-14 | — | [ ] | Avec RPC1 (s15). Annexe X |

> **Rencontres hebdomadaires (dès s8) :** tableau de bord (2-3 p. PDF) déposé dans Teams **le jeudi avant 5 h 00** — contenu détaillé en Partie 3.

## S7 — PMC760 (hiver 2027)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| S7-01 | Rencontres de suivi (30 min × 10) | ÉQUIPE | 20h | 2027-01-05 | 2027-04-30 | — | [ ] | Tableau de bord hebdo |
| S7-02 | Rencontres techniques (60 min × 10) | ÉQUIPE | 40h | 2027-01-05 | 2027-04-30 | — | [ ] | Présentation PowerPoint Teams |
| S7-03 | Audits d'équipe (× 2) | ÉQUIPE | 40h | 2027-02-22 | 2027-04-09 | — | [ ] | s8 et s15 (Annexe M). Annexe R |
| S7-04 | Audits numériques individuels (× 2, vidéo 10 min) | INDIV | 30h | 2027-02-09 | 2027-04-18 | — | [ ] | **×2** : s6 et s16 (Annexe M). Annexe S |
| S7-05 | Évaluations par les pairs (PME × 3) | INDIV | 6h | 2027-01-05 | 2027-04-30 | — | [ ] | s6 / s11 / s17 |
| S7-06 | RAE | INDIV | 14h | 2027-04-19 | 2027-04-30 | — | [ ] | Annexe X |
| S7-07 | **RPC2** (max 80 p. avec annexes) | ÉQUIPE | 200h | 2027-03-01 | 2027-04-26 | S7-T06 | [ ] | Annexe U — conception détaillée + plan d'essais. `git tag RPC2` |
| S7-08 | Page descriptive de projet (Annexe Z / Padlet) | ÉQUIPE | 4h | 2027-04-05 | 2027-04-23 | — | [ ] | **Manquait.** Publique, maintenue jusqu'à S8 ; responsable-éditeur désigné |
| S7-09 | FEPRAP (mise à jour) | ÉQUIPE | 2h | 2027-01-12 | 2027-01-16 | — | [ ] | s2 (Annexe M) |

> **RPC2 (Annexe U) :** (1) description technique (architecture, modules, choix, fabrication, validation) ; (2) suivi de gestion (finances, heures, écarts, projection S8) ; (3) annexes (code tag Git, plans, calculs).

## S8 — PMC860 (automne 2027)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| S8-01 | Rencontres suivi-technique (45 min × 10) | ÉQUIPE | 30h | 2027-08-30 | 2027-12-11 | — | [ ] | |
| S8-02 | Audit d'équipe (× 1) | ÉQUIPE | 24h | 2027-10-25 | 2027-10-31 | — | [ ] | s10 (Annexe M) |
| S8-03 | Audit numérique individuel (vidéo 10 min) | INDIV | 20h | 2027-09-27 | 2027-10-17 | — | [ ] | s5-7 (Annexe M) |
| S8-04 | Évaluations par les pairs (PME × 3) | INDIV | 6h | 2027-08-30 | 2027-12-11 | — | [ ] | s5 / s11 / s17 |
| S8-05 | RAE | INDIV | 14h | 2027-12-07 | 2027-12-18 | — | [ ] | |
| S8-06 | **RLP** (rapport de livraison de projet, max 40 p.) | ÉQUIPE | 80h | 2027-11-01 | 2027-12-11 | S8-T09 | [ ] | Annexe W |
| S8-07 | **Expo MégaGÉNIALE** (démo publique) | ÉQUIPE | 40h | 2027-11-27 | 2027-11-28 | S8-T13 | [ ] | ⚠️ **27-28 nov. à confirmer (comité/Teams ; patron jeu-ven-sam)**. Sondage info-projet ≤ 15 sept |
| S8-09 | FEPRAP (mise à jour) | ÉQUIPE | 2h | 2027-09-07 | 2027-09-11 | — | [ ] | s2 (Annexe M) |
| S8-08 | Avis de fin de projet (Annexe J) | ÉQUIPE | 4h | 2027-12-18 | 2027-12-23 | S8-T13 | [ ] | Avant midi dernier jour — IN si manquant |
| S8-10 | Mise en garde (Annexe I), signée par tous | INDIV | 2h | 2027-12-14 | 2027-12-18 | — | [ ] | **Manquait** — IN si manquant |
| S8-11 | Déclaration ressources institutionnelles (Annexe Y) | ÉQUIPE | 2h | 2027-12-14 | 2027-12-18 | — | [ ] | **Manquait** — à la livraison S8 |

---

# PARTIE 2 — Développement technique (par bloc)

> **Le technique démarre en semaine 8 (22 juin), après le MIP.** Stratégie S6 (décision d'équipe) : **≈ 7 personnes sur audio + game engine** (chemin critique vers le benchmark/MCU) + **1 personne sur le boîtier** (mockup). Le reste (PCB préliminaire, contenu de jeu) est **reporté au stage T4**.
> **Dépendances inter-blocs :** Boîtier(interne) → PCB → [benchmark Engine+Audio → MCU] ; Engine ↔ Audio (interface commune) ; Jeu → Engine+Audio ; IDE → indépendant (jusqu'à l'USB).

## Bloc 0 — Fondations & interfaces (transversal)

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-01 | Contrats d'interface (Input, Audio, Haptic, Storage, MiniGame) | ENG | 40h | 2026-06-22 | 2026-06-26 | — | [ ] | **Phase 0 — démarre après le MIP (s8).** Fondation de tout le technique |
| TECH-02 | **Gel des interfaces** (revue croisée) | TOUTES | 8h | 2026-06-26 | 2026-06-29 | TECH-01 | [ ] | Tout changement futur = accord des 2 équipes |
| TECH-03 | Achat manettes USB (2-3 PS4/Xbox) | ENG | 4h | 2026-06-22 | 2026-06-29 | — | [ ] | ~60$ |
| TECH-04 | Setup du repo (structure, build, conventions) | ENG | 16h | 2026-06-22 | 2026-06-29 | — | [ ] | Document de conventions |

## Bloc 1 — Game Engine (ENG) · *Flux A* — **blitz S6 (s8-15)**

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-05 | GamepadMapper (USB → InputState) | ENG | 40h | 2026-06-29 | 2026-07-10 | TECH-02,TECH-03 | [ ] | 1ʳᵉ implé. de l'interface Input |
| TECH-06 | StubAudio + StubHaptic (logs, sans HW) | ENG | 24h | 2026-06-29 | 2026-07-06 | TECH-02 | [ ] | Tester la logique sans son |
| TECH-09 | Système de scènes (create/load/unload/transition) | ENG | 40h | 2026-06-29 | 2026-07-17 | TECH-04 | [ ] | Sur PC |
| TECH-10 | Monde 2D+Z (grille, entités sonores) | ENG | 40h | 2026-07-06 | 2026-07-17 | TECH-09 | [ ] | Sur PC |
| TECH-11 | Déplacement joueur (joystick gauche) | ENG | 32h | 2026-07-13 | 2026-07-24 | TECH-05,TECH-10 | [ ] | |
| TECH-12 | Système de collisions (murs, obstacles) | ENG | 32h | 2026-07-13 | 2026-07-24 | TECH-10 | [ ] | |
| GE-01 | **Jeu V1 sur PC** (test d'engine jouable) | ENG | 48h | 2026-07-27 | 2026-08-14 | TECH-11,TECH-12,TECH-13 | [ ] | **Livrable « blitz » fin S6** — valide engine + audio de base |
| GE-02 | Raffinement engine + harness de benchmark | ENG | 60h | 2026-09-08 | 2026-12-18 | GE-01 | [ ] | **Stage T4** — prépare le benchmark de S7 |
| S7-T02 | Bâton d'aveugle (raycast + haptique directionnel) | ENG | 48h | 2027-01-05 | 2027-01-29 | TECH-12 | [ ] | |
| S7-T03 | Intégration PCAudio dans le game engine | ENG | 32h | 2027-01-15 | 2027-01-26 | S7-T01,TECH-09 | [ ] | Son spatial au casque |
| S7-T04 | **Benchmark du jeu sur PC** (CPU/RAM/sources/latence) | ENG+AUD | 40h | 2027-01-22 | 2027-01-29 | S7-T03,S7-T01,GE-02 | [ ] | **Clé du choix MCU** |
| S7-T05 | Estimation des besoins MCU (à partir du benchmark) | AUD+ENG | 16h | 2027-01-29 | 2027-02-02 | S7-T04 | [ ] | Comparer aux MCU candidats |
| S7-T06 | **◆ DÉCISION : choix du microcontrôleur ◆** | TOUTES | 16h | 2027-02-02 | 2027-02-08 | S7-T05,TECH-18,MIP-08 | [ ] | **Jalon pivot — convergence A+B+C.** Produit un ADR (justification quantitative) |
| S7-T11 | Intégration MicroPython (firmware) | ENG | 60h | 2027-02-08 | 2027-03-12 | S7-T06 | [ ] | Voir ADR-0005 |
| S7-T12 | Protocole USB CDC (spec + implé.) | ENG | 40h | 2027-02-08 | 2027-03-12 | — | [ ] | Alimente l'IDE (S7-T15) |
| S8-T04 | NathanMapper + NathanHaptic (manette réelle) | ENG | 48h | 2027-09-13 | 2027-10-22 | S8-T01 | [ ] | Swap d'implémentation Input/Haptic |
| S8-T05 | Intégration audio embarqué dans le game engine | ENG | 40h | 2027-09-27 | 2027-10-29 | S8-T02,S8-T04 | [ ] | |

## Bloc 2 — Audio HRTF (AUD) · *Flux B* — **blitz S6 (s8-15)**

> **Stratégie audio (2 temps) :** benchmark initial sur **librairies existantes** (I/O playback + spatialisation **de référence**) pour des chiffres rapides de dimensionnement MCU — **mais le livrable est NOTRE propre librairie de son spatial** (convolution HRTF maison, voir [ADR-0002]). Seul moyen d'avoir le contrôle requis pour le portage embarqué et l'option FPGA.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-07 | Recherche HRTF (datasets MIT KEMAR, CIPIC, SOFA) | AUD | 24h | 2026-06-22 | 2026-07-03 | — | [ ] | Tableau comparatif |
| TECH-08 | Choix lib audio PC : **I/O playback** + lib spatialisation **de référence** | AUD | 16h | 2026-06-22 | 2026-06-26 | — | [ ] | Lib existante = I/O + baseline benchmark ; **pas** la spatialisation finale |
| TECH-13 | **Notre lib de son spatial** — proto 1 source (convolution HRTF maison) | AUD | 40h | 2026-06-29 | 2026-07-17 | TECH-08,TECH-07 | [ ] | Son qui tourne au casque |
| TECH-14 | **Notre lib** — multi-sources (4-6 sur PC) | AUD | 60h | 2026-07-13 | 2026-08-07 | TECH-13 | [ ] | |
| AU-01 | Benchmark conso/perf — **lib de référence + notre proto** | AUD | 32h | 2026-08-03 | 2026-08-14 | TECH-14 | [ ] | **Blitz fin S6** — chiffres pour le MCU |
| AU-02 | Pré-décision : audio sur MCU vs module séparé | AUD | 16h | 2026-08-10 | 2026-08-14 | AU-01 | [ ] | **Orientation** (décision formelle = S7-T07) |
| AU-03 | Maturation de **notre lib** (multi-source robuste, interpolation, distance) | AUD | 80h | 2026-09-08 | 2026-12-18 | TECH-14 | [ ] | **Stage T4** — rend l'audio « benchmark-ready » |
| S7-T01 | **Notre librairie de son spatial — complète** (contrat SpatialAudioEngine) | AUD | 60h | 2027-01-05 | 2027-01-22 | AU-03 | [ ] | **Le vrai livrable audio.** Front-load pour S7-T04 |
| S7-T07 | **DÉCISION audio : software / DSP externe / FPGA-CPLD maison** | AUD+ELEC | 8h | 2027-02-08 | 2027-02-12 | S7-T06,AU-02 | [ ] | Critère = benchmark. Si MCU insuffisant → Bloc 2b (voir ADR-0004) |
| S8-T02 | Portage de **notre lib de son spatial** sur le MCU choisi | AUD | 100h | 2027-08-30 | 2027-10-09 | S7-T06,S7-T07,S8-T01 | [ ] | Le plus complexe. **Remplacé par le Bloc 2b si l'option FPGA est retenue** |

### Bloc 2b — Option conditionnelle : décharge audio matérielle (FPGA/CPLD)

> **⚠️ Option CONDITIONNELLE — repli ultime de `H-07`** (voir [ADR-0004]). À n'activer **que si** le benchmark (`S7-T04`/`S7-T05`) montre qu'**aucun MCU abordable ne suffit** (décision à `S7-T07`). Le FPGA/CPLD est un **banc de filtres FIR numérique reprogrammable** : si retenu, il est **dans le produit final** (proto devkit ~40 $, **production puce ~7-10 $**), pas seulement pour tester. 3ᵉ implémentation de `SpatialAudioEngine`. **Si activée, REMPLACE `S8-T02`.** Détails : `ESTIMATION.md` §2.6/§4.2.

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| AUDHW-01 | Étude de faisabilité : dimensionner le FIR HRTF en logique | AUD+ELEC | 40h | 2027-02-02 | 2027-02-08 | S7-T05 | [ ] | **Conditionnel** — alimente `S7-T07` |
| AUDHW-02 | Choix du composant : FPGA/CPLD (iCE40 UP5K…) vs DSP + BOM | ELEC | 16h | 2027-02-12 | 2027-02-19 | S7-T07 | [ ] | À trancher tôt pour que le schéma `S7-T17` intègre le FPGA |
| AUDHW-03 | Implémentation HDL du moteur HRTF (convolution parallèle) + simu | AUD+ELEC | 160h | 2027-02-22 | 2027-09-18 | S7-T01,AUDHW-02 | [ ] | **Effort principal.** yosys/nextpnr (`C-25`). S7 → T5 → début S8 |
| AUDHW-04 | Interface de streaming MCU → FPGA (protocole + DMA/I2S) | ENG+ELEC | 48h | 2027-08-30 | 2027-09-25 | AUDHW-02 | [ ] | **Nouvelle interface à geler** |
| AUDHW-05 | Intégration du module audio matériel sur le PCB + tests | ELEC | 40h | 2027-09-27 | 2027-10-15 | S8-T01,AUDHW-03,AUDHW-04 | [ ] | Impacte `S7-T17`/`S7-T18` |
| AUDHW-06 | Validation A/B : qualité/latence vs version logicielle | AUD+ENG | 24h | 2027-10-18 | 2027-10-29 | AUDHW-05 | [ ] | Critère : latence < 20 ms (`E5`) |

## Bloc 3 — PCB / Électronique (ELEC) · *Flux C (électronique)* — **reporté en T4**

> S6 = focus audio+engine+boîtier → le **PCB préliminaire se fait au stage T4** (travail indépendant du MCU). Le comparatif MCU pour le MIP, lui, est fait en s6 (`MIP-08`).

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| PCB-01 | Définition de l'interface des contrôles (E/S) | ELEC | 24h | 2026-09-08 | 2026-09-25 | TECH-01 | [ ] | **Stage T4** — indépendant du MCU |
| PCB-02 | Conception préliminaire du BMS (batterie + murale) | ELEC | 40h | 2026-09-08 | 2026-10-09 | — | [ ] | **Stage T4** — faisable avant le choix MCU |
| PCB-03 | Section alim. + connecteurs + lib. d'empreintes | ELEC | 40h | 2026-10-12 | 2026-12-18 | PCB-01,PCB-02 | [ ] | **Stage T4** — pré-travail indépendant du MCU |
| TECH-18 | Recensement complet MCU candidats (ESP32-S3, RP2350, STM32H7…) | ELEC | 24h | 2026-09-08 | 2026-10-02 | — | [ ] | **Stage T4** — alimente le choix MCU `S7-T06` |
| S7-T08 | Breadboard MCU (valider I2S, ADC, PWM, USB) | ELEC | 48h | 2027-02-08 | 2027-03-05 | S7-T06 | [ ] | |
| S7-T17 | Schéma KiCAD v2.0 complet | ELEC | 60h | 2027-02-15 | 2027-03-19 | S7-T06,S7-T08,PCB-03 | [ ] | |
| S7-T18 | Layout PCB + commande de fabrication | ELEC | 48h | 2027-03-08 | 2027-04-02 | S7-T17 | [ ] | |
| PCB-04 | Fabrication PCB (délai externe JLCPCB) | ELEC | 8h | 2027-03-29 | 2027-04-23 | S7-T18 | [ ] | **2-3 sem incompressibles** (`H-16`) — commander tôt |
| S8-T01 | Soudure PCB + tests électriques | ELEC | 40h | 2027-08-30 | 2027-09-18 | PCB-04 | [ ] | |

## Bloc 4 — Boîtier (ELEC / méca) · *Flux C (mécanique)* — **1 personne, S6 (s8-14)**

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| BOI-01 | Mockup CAD de la coque (extérieur + ergonomie) | ELEC | 40h | 2026-06-22 | 2026-07-17 | — | [ ] | **S6** (1 pers.). Aucune dépendance (extérieur seulement) |
| BOI-02 | Itérations d'impression de la coque (sans interne) | ELEC | 32h | 2026-07-13 | 2026-08-07 | BOI-01 | [ ] | **S6** — itérer l'ergonomie de la main |
| BOI-03 | Polish ergonomie + consultations DV | ELEC | 24h | 2026-09-08 | 2026-12-18 | BOI-02,COM-05 | [ ] | **Stage T4** — retours DV (après recrutement) |
| BOI-04 | Conception interne (supports PCB/batterie/moteurs) | ELEC | 40h | 2027-03-08 | 2027-04-09 | S7-T18 | [ ] | **Dépend du PCB** (dimensions/positions) |
| S8-T03 | Impression 3D finale + assemblage complet | ELEC | 32h | 2027-09-13 | 2027-10-01 | S8-T01,BOI-04 | [ ] | |

## Bloc 5 — Jeu & Contenu (JEU) · *Flux D* — **reporté en T4**

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| JEU-01 | Conception papier du jeu complet (sprites/scènes/map/mini-jeux/sons) | JEU | 40h | 2026-09-08 | 2026-09-25 | — | [ ] | **Stage T4** — permet le dev des zones dès S7 |
| TECH-15 | Design de la carte (plan coté 2D) | JEU | 24h | 2026-09-08 | 2026-09-25 | JEU-01 | [ ] | Dimensions, positions des murs |
| TECH-16 | Liste des sons (inventaire exhaustif) | JEU | 16h | 2026-09-22 | 2026-10-02 | JEU-01 | [ ] | |
| TECH-17 | Banque de sons (production interne + CC0) | JEU | 120h | 2026-09-29 | 2027-08-13 | TECH-16 | [ ] | Long, parallélisable — T4 → S7 → T5 |
| S7-T09 | Développement des zones (Salon, Cuisine, Chambre, Musique) | JEU | 120h | 2027-01-05 | 2027-03-12 | TECH-09,TECH-12,S7-T01 | [ ] | Avec GamepadMapper + PCAudio |
| S7-T10 | Narration audio (enregistrement des voix) | JEU | 40h | 2027-01-25 | 2027-02-26 | JEU-01 | [ ] | |
| S8-T06 | École + mini-jeux d'exemple (zone extérieure) | JEU | 48h | 2027-09-13 | 2027-10-22 | S7-T11,S7-T09 | [ ] | |
| S8-T10 | Test utilisateur DV (protocole CER approuvé) | JEU | 24h | 2027-10-18 | 2027-10-29 | S8-T09,ETH-05 | [ ] | Groupe recruté via l'APHVE |

## Bloc 6 — IDE accessible (ENG) · *Flux E* — **S7** (voir [ADR-0006])

| ID | Tâche | Rôle | Est. | Début | Fin | Dépend de | Statut | Notes |
|----|-------|------|------|-------|-----|-----------|--------|-------|
| TECH-19 | Choix du stack (Electron/React, Tauri…) | ENG | 24h | 2027-01-05 | 2027-01-15 | — | [ ] | Produit un ADR. Critère : accessibilité |
| IDE-01 | Mockups interface (avec AI) | ENG | 24h | 2027-01-05 | 2027-01-22 | — | [ ] | |
| IDE-02 | TTS/STT + test isolé des fonctionnalités AI | ENG | 48h | 2027-01-18 | 2027-02-12 | IDE-01 | [ ] | Codage vocal : entrée STT, retour TTS |
| IDE-03 | Estimation des coûts (services AI cloud) | ENG | 8h | 2027-01-18 | 2027-01-29 | IDE-02 | [ ] | |
| IDE-04 | Résolution dépendance backend/frontend | ENG | 16h | 2027-01-25 | 2027-02-12 | TECH-19 | [ ] | |
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
| S8-T13 | Préparation Expo MégaGÉNIALE (kiosque, démo, protocole batterie) | TOUTES | 40h | 2027-11-01 | 2027-11-26 | S8-T11 | [ ] | Inclut le **protocole de démo batterie + autorisation comité (≥ 3 sem avant)** et nos propres écrans (Annexe V) |
| S7-T19 | Soumission au CER (formulaire d'avis) | ÉQUIPE | — | 2027-01-05 | 2027-01-23 | — | [ ] | = ETH-02. ≥ 4 sem avant test DV |
| S7-T20 | Soumission du protocole d'essai (superviseur) | ÉQUIPE | — | 2027-09-27 | 2027-10-02 | — | [ ] | = ETH-05. ≥ 2 sem avant test DV |

---

# PARTIE 3 — Chronologie, jalons et chemins critiques

## Réconciliation capacité ↔ charge planifiée

| Période | Capacité équipe | Charge planifiée (est.) | Lecture |
|---------|-----------------|-------------------------|---------|
| **S6** | 945 h (945 h nominal, mais ~630 h **restantes** s6-15) | **~750-850 h** | 🔴 **Sur-souscrite** : MIP (s6-7) + RPC1 (s8-15) + blitz audio/engine (s8-15) sur 10 sem. → débordement vers T4 |
| **T4** (stage) | ~420 h | **~450 h** | 🟠 **Plus chargé** : reçoit le PCB prélim, le contenu de jeu, la maturation audio/engine, le polish boîtier reportés de S6 |
| **S7** | 1890 h | ~1350 h | 🟢 Marge confortable (6 cr) |
| **T5** (stage) | ~420 h | ~300 h | 🟢 Finalisation contenu/sons + portage |
| **S8** | 945 h | ~650 h | 🟢 Intégration + tests + Expo + RLP |

> **🔴 S6 est le vrai goulot de capacité.** En démarrant le technique en s8 (après le MIP), il ne reste que ~10 semaines pour : MIP + RPC1 (2 livrables académiques) **et** le blitz audio+engine. **Leviers :** (1) IDE entièrement en S7 ; (2) PCB prélim + contenu de jeu **reportés en T4** ; (3) priorité absolue au **cœur audio+engine** (chemin critique vers le MCU) ; le boîtier mobilise 1 personne. **À surveiller :** T4 dépasse légèrement sa capacité nominale réduite — ajuster les heures de stage ou démarrer une partie du contenu en fin de S6 si bande passante.

## Jalons de convergence

| Jalon | Quand (date) | Ce qui converge | Ce qui est débloqué |
|-------|--------------|-----------------|---------------------|
| **MIP déposé** | 2026-06-18 (s7) | Identification du projet validée | Démarrage du technique + RPC1 + chaîne partenariat |
| **Interfaces gelées** | 2026-06-29 (s8) | Contrats des 5 interfaces | Développement parallèle des blocs |
| **Jeu V1 jouable sur PC** | 2026-08-14 (fin S6) | Engine + audio de base + GamepadMapper | Démos, premier benchmark, base T4 |
| **« Benchmark-ready »** | 2027-01-05 (S7 s1) | PCAudio mûr (T4) + engine raffiné (T4) | Benchmark formel immédiat |
| **◆ Choix du MCU ◆** | ~2027-02-08 (S7 s5) | Benchmark (A) + besoins audio (B) + analyse MCU (C) | Breadboard, schéma, PCB, portage |
| **Convention signée** | ~2026-09 (fin S6/T4) | APHVE + SARIC + équipe | **Recrutement DV** → consultations |
| **Manette NATHAN opérationnelle** | ~2027-10-09 (S8 s6) | PCB soudé + boîtier + NathanMapper/Haptic + audio embarqué | **Transition : on lâche la manette Xbox** |
| **Console complète** | ~2027-10-22 (S8 s8) | Manette + engine porté + jeu + IDE | Tests d'intégration, tests DV formels |
| **Expo MégaGÉNIALE** | 2027-11-27/28 *(à confirmer)* | Tout | Démonstration publique |

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

**Le game engine ne sait jamais s'il parle à une manette Xbox ou à la manette NATHAN.** C'est ce qui permet de développer le jeu complet sur PC avant d'avoir choisi le microcontrôleur (voir [ADR-0001]).

> L'interface `SpatialAudioEngine` admet une **3ᵉ implémentation conditionnelle** — `HardwareAudio` (FPGA/CPLD, **Bloc 2b**, [ADR-0004]) — à côté de `PCAudio` et `EmbeddedAudio`.

## Flux parallèles (S6 → T4 → S7 → T5 → S8)

```
        S6 (été 26)            T4 (stage)      S7 (hiver 27)        T5 (stage)    S8 (aut. 27)
        s6-7: MIP              ──────────      ─────────────        ──────────    ────────────
        s8-15: TECHNIQUE
ENG     interfaces(s8)         raffinement     bâton+benchmark      —             NathanMapper
        +mapper+engine+JeuV1   +harness        +intégration                       +audio embarqué
AUD     proto→multi-src        maturation      PCAudio complet      —             portage MCU
        +benchmark prél.       PCAudio         +DÉCISION audio
ELEC    (MIP-08 comparatif)    PCB prélim      breadboard→schéma    —             soudure
(PCB)                          +MCU recens.    →layout→fab
ELEC    mockup CAD (1 pers.)   polish +        conception interne   —             impression
(boît.) +impressions           consult. DV     (dépend PCB)                       +assemblage
JEU     —                      design+sons     zones+narration      finition      école+mini-jeux
                               production       (avec contenu T4)    sons          +tests DV
IDE     —                      —               stack+AI+TTS/STT      raffinement   intégration
                                               +accessibilité+USB                 +polish
DV      Discord+process        recrutement     consultations …………… (continu) ……  tests formels
                               +1ʳᵉ consult.
```

## Chemin critique (le plus long — hardware)

```
MIP déposé (2026-06-18)
 → Interfaces gelées (2026-06-29, s8)
   → Engine + Audio sur PC (blitz S6 s8-15 + maturation T4)
     → Benchmark PC (2027-01, S7 s3-4)
       → ◆ Choix MCU (2027-02-08, S7 s5)
         → Breadboard (s6-9) → Schéma KiCAD (s7-11) → Layout PCB (s10-13)
           → Fabrication PCB (2-3 sem, externe) → Soudure+tests (S8 s1-3)
             → NathanMapper/Haptic + audio embarqué (S8 s3-6)
               → ◆ Transition manette (S8 s6) → Intégration (S8 s8)
                 → Tests DV (S8 s8-9) → Expo (2027-11-27/28)
```

**Goulots non compressibles :** S6 (10 sem pour MIP+RPC1+blitz) · benchmark PC · choix MCU · fabrication PCB (`H-16`) · portage audio embarqué (`S8-T02`) · approbation CER (≥ 4 sem) · **convention de partenariat** (gèle le recrutement DV) · **[conditionnel]** décharge audio FPGA (`AUDHW-03/04/05`).

## Transition manette Xbox → NATHAN (S8, swap d'implémentation)

Conditions : PCB soudé (`S8-T01`) · NathanMapper/Haptic (`S8-T04`) · audio embarqué (`S8-T02`/`S8-T05`) · boîtier assemblé (`S8-T03`). **Incrémentale :** Input → Haptic → Audio → Storage.

---

## Pondérations des livrables (Annexe L)

- **PMC660 (S6) :** MIP **10 %** · RPC1 **15 %** · Audit d'équipe **25 %** · Rencontres techniques **30 %** · Rencontres gestion **15 %** · RAE **5 %**.
- **PMC760 (S7) :** RPC2 **25 %** · Audits d'équipe **~15 %** · Rencontres techniques **30 %** · Rencontres gestion **15 %** · RAE **5 %** *(détail exact : Annexe L)*.
- **PMC860 (S8) :** RLP **20 %** · Audit d'équipe **10 %** · Expo MégaGÉNIALE **10 %** · Rencontres techniques **30 %** · Rencontres gestion **15 %** · RAE **5 %**.

*(Les audits numériques comptent dans « Rencontres techniques » ; l'évaluation par les pairs module les notes d'équipe, Annexe L.)*

## Tableau de bord hebdomadaire (dès s8, **jeudi avant 5 h 00**)

Nom/date/photos+rôles · objectifs projet & session · ordre du jour · tâches faites/en cours/à venir · courbe en S ou burndown · heures/membre · taux d'atteinte · suivi des risques · protocoles d'essais · état des dépenses · problèmes · sujet rencontre technique.

## Checklist des livrables par session

**S6 :** Annexes A/D/E/H · FEPRAP · contrat d'équipe · modalités partenariat (SARIC) · MIP (≤ 20 p.) · RPC1 (≤ 35 p.) · RAE · audit d'équipe · audit numérique · tableaux de bord.
**S7 :** RPC2 (≤ 80 p.) · RAE · audits numériques (×2) · page descriptive (Annexe Z) · convention partenariat (si pas faite) · CER + protocole soumis · FEPRAP · code tagué (`git tag RPC2`).
**S8 :** RLP (≤ 40 p.) · RAE · audit numérique · avis de fin (Annexe J) · **mise en garde (Annexe I)** · **déclaration ressources (Annexe Y)** · FEPRAP · démo Expo · prototype fonctionnel.

---

## Notes de révision (à valider par l'équipe)

1. **Re-calage au 8 juin** : aucune tâche non terminée n'est datée avant aujourd'hui. Faits (`[x]`) : coachings #1-3, PART-01/02. *Corrige si d'autres tâches sont déjà faites.*
2. **Séquence S6** : MIP finalisé s6 → **formative 11 juin** (Coaching #4) → **remise finale 18 juin** → **technique à partir de s8 (22 juin)**. S6 utile = 10 semaines.
3. **Blitz S6** : ≈ 7 pers. sur audio+engine (chemin critique vers le MCU) + 1 sur le boîtier. **PCB préliminaire et contenu de jeu reportés en T4.**
4. **Partenariat → recrutement** : ouverture du dossier SARIC le 11 juin ; convention signée ~septembre (latences SARIC) ; **recrutement DV après la convention → T4** ; 1ʳᵉ consultation ~octobre. *(Contact informel DV possible avant si l'APHVE l'autorise — à ajouter au besoin.)*
5. **MCU avancé à ~S7 s5** (vs sem 8-9) — tient si `AU-03`/`GE-02` avancent en T4. Décision → ADR.
6. **Conformité ajoutée** (Annexe L/M) : FEPRAP (S6/S7/S8), audit numérique S6 (`EVAL-09`) et S7 ×2, page descriptive (`S7-08`), mise en garde (`S8-10`), déclaration ressources (`S8-11`), pondérations corrigées, tableau de bord jeudi 5 h 00, dépendance `MIP-08` rendue autonome.
7. **Capacité** : S6 sur-souscrite, T4 plus chargé — voir réconciliation. Estimations ± 20 %, à affiner par les responsables de bloc.
8. **Dates exactes (audits, ateliers, finaux)** : tirées de l'**Annexe M** (horaires-types, année exemple) → **à confirmer sur le SharePoint/Teams** pour E2026.
9. **Librairie de son spatial maison** = livrable clé ([ADR-0002]) ; **option FPGA/CPLD** = branche conditionnelle ([ADR-0004], Bloc 2b). `H-07` à synchroniser dans `HYPOTHESES.md`.
10. **Chevauchements de dates intra-bloc = parallélisme volontaire** (blitz ≈ 7 pers.) : ici « Dépend de » signifie « a besoin de », pas « strictement après ». Pour un import JIRA, **typer ces liens en *Start-to-Start*** (sinon l'import les lira en Fin→Début et générera des alertes). Le **chemin critique inter-blocs reste propre en Fin→Début** : interfaces → audio/engine → benchmark → MCU → PCB → soudure → intégration ; et convention → recrutement.

---

*Document vivant — à mettre à jour chaque semaine dans le tableau de bord. Décisions de conception tracées dans `docs/decisions/` (ADR). Prochaine étape : revue d'équipe (2 j) → import JIRA (CSV depuis ce fichier).*
