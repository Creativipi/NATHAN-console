# ADR-0007 — Adopter les ADR et la structure `docs/` pour la traçabilité

- **Statut :** Accepté
- **Date de la décision :** 2026-06-07
- **Décideurs :** ÉQUIPE
- **Contexte projet :** projet open-source sur 3 sessions + 2 stages
- **Liens :** [[README]] (docs/), `CONTRIBUTING.md`, toutes les tâches « DÉCISION » de [[planning/TACHES]]

## Contexte et problème

Le projet est **open-source** et s'étale sur **3 sessions + 2 stages** : un nouvel arrivant doit pouvoir **voir la timeline et l'évolution** des décisions de conception. Les revues de `TACHES.md` et `ESTIMATION.md` ont révélé des **décisions dupliquées et incohérentes** entre documents (jalons SYNC divergents, `H-07` non synchronisé, `OPTION-AUDIO-MATERIELLE.md` « flottant ») — symptôme d'une **absence de couche « décisions »**.

## Options envisagées

- **A — Continuer à disperser** les décisions dans les specs/planif. *Contre :* dérive et incohérences (constatées en revue).
- **B — Journal unique `DECISIONS.md`.** *Contre :* devient lourd, peu *diff-able* par décision.
- **C — GitHub Issues/Discussions.** *Contre :* hors-repo (un clone seul ne montre pas la timeline).
- **D — ADR + structure `docs/` (retenue) :** un fichier markdown immuable par décision, numéroté/daté/statué, indexé ; dossiers `specs/ planning/ decisions/ architecture/` ; traçabilité par IDs ; tags git aux jalons.

## Décision

Adopter les **ADR**, réorganiser la doc sous **`docs/`**, et instaurer la discipline **« toute décision d'architecture/conception = un ADR »** (voir `CONTRIBUTING.md`). L'**index** `docs/decisions/README.md` est la frise chronologique ; les **tags git** aux jalons (interfaces gelées, choix MCU, RPC1/RPC2/RLP) donnent la timeline des livraisons.

## Conséquences

- **+** Traçabilité bout-en-bout (besoin → requis → décision → tâche → code → commit/tag), onboarding facilité, **alimente directement RPC1/RPC2/RLP** (qui exigent « options évaluées + justification »).
- **−** Discipline à tenir : chaque décision doit produire un ADR ; les ADR sont **immuables** (un changement = nouvel ADR « Remplace ADR-XXXX »).

## Suivi / quand re-questionner

Réviser le processus si le rythme d'ADR ne suit pas les décisions réelles (signal de dérive à corriger en rétro d'équipe).
