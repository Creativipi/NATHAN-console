# Documentation NATHAN Console — Commencez ici

Bienvenue. Cette documentation est organisée pour qu'un **nouvel arrivant** (contributeur open-source ou nouveau membre d'équipe) puisse comprendre **quoi**, **pourquoi** et **quand**, dans cet ordre.

## Parcours de lecture recommandé

1. **[`/README.md`](../README.md)** — *quoi & pourquoi le projet existe* (l'histoire de NATHAN, la vision).
2. **[`architecture/`](./architecture/)** — *comment c'est construit* (diagrammes système et IDE).
3. **[`decisions/`](./decisions/README.md)** — *pourquoi c'est construit ainsi, et son évolution* (journal des ADR = la timeline des décisions).
4. **[`planning/TACHES.md`](./planning/TACHES.md)** — *quoi est fait / à faire et quand* (tâches, dates, dépendances, base du GANTT).
5. **[`specs/`](./specs/)** — *les exigences détaillées* (à consulter au besoin).

## Carte de la documentation

| Dossier | Contenu |
|---------|---------|
| [`decisions/`](./decisions/README.md) | **Journal des décisions (ADR)** — la traçabilité du *pourquoi* |
| [`planning/`](./planning/) | [`TACHES.md`](./planning/TACHES.md) (tâches/GANTT) · [`ESTIMATION.md`](./planning/ESTIMATION.md) (coûts, effort, 3 gammes MCU) |
| [`specs/`](./specs/) | [`CAHIER-DES-CHARGES.md`](./specs/CAHIER-DES-CHARGES.md) · [`REQUIS.md`](./specs/REQUIS.md) · [`BESOINS.md`](./specs/BESOINS.md) · [`CONTRAINTES.md`](./specs/CONTRAINTES.md) · [`HYPOTHESES.md`](./specs/HYPOTHESES.md) · [`CADRE-LOGIQUE.md`](./specs/CADRE-LOGIQUE.md) |
| [`architecture/`](./architecture/) | Diagrammes `.drawio` / `.mmd` (console et IDE) |

## Comment lire la « timeline et l'évolution »

- **Pourquoi (décisions) :** [`decisions/README.md`](./decisions/README.md) — index des ADR par date et statut. Une décision qui en remplace une autre est visible via les statuts *Remplace / Remplacé par*.
- **Livraisons (jalons) :** les **tags git** marquent les jalons (interfaces gelées, choix MCU, RPC1, RPC2, RLP). `git log --oneline --decorate` montre la chronologie.
- **Plan (futur) :** [`planning/TACHES.md`](./planning/TACHES.md) → Partie 3 (jalons de convergence, chemins critiques).
- **Détail d'un fichier :** `git log --follow <fichier>` (l'historique est préservé malgré la réorganisation).

## Traçabilité par identifiants

Tout est relié par des IDs stables :

```
Besoin → Requis (R-xx) / Contrainte (C-xx) / Hypothèse (H-xx)
       → Décision (ADR-xxxx)
       → Tâche (TACHES : ADM-/TECH-/S7-T/AUDHW-/…)
       → Code / PCB / diagramme
       → Commit (conventional commits) / tag de jalon
```

> Contribuer ? Voir **[`CONTRIBUTING.md`](../CONTRIBUTING.md)** — notamment « quand et comment écrire un ADR ».
