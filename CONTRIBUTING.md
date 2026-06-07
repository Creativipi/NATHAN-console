# Contribuer à NATHAN Console

NATHAN est un projet **open-source** (console de jeu audio accessible aux personnes non-voyantes) réalisé dans le cadre du projet majeur de conception PMC660-760-860 (Université de Sherbrooke). Ce guide explique **comment le projet est organisé** et **comment tracer une décision** pour que quiconque arrive puisse suivre la timeline et l'évolution.

## Où trouver quoi

- **Commencer :** [`docs/README.md`](./docs/README.md) (parcours de lecture).
- **Pourquoi (décisions) :** [`docs/decisions/`](./docs/decisions/README.md) — le journal des ADR.
- **Plan & tâches :** [`docs/planning/TACHES.md`](./docs/planning/TACHES.md).
- **Exigences :** [`docs/specs/`](./docs/specs/).
- **Architecture :** [`docs/architecture/`](./docs/architecture/).

## Règle d'or : toute décision d'architecture ou de conception = un ADR

Un **ADR** (Architecture Decision Record) capte une décision **non triviale** : choix d'un composant, d'un protocole, d'une architecture, d'un arbitrage de conception, ou tout virage par rapport à une décision antérieure.

### Quand écrire un ADR
- Tu fais un choix qui sera coûteux à inverser, ou que quelqu'un d'autre pourrait remettre en question plus tard.
- Tu tranches une tâche **« DÉCISION »** de `TACHES.md` (p. ex. `S7-T06` choix MCU). **C'est une condition de « terminé ».**
- Tu **changes** une décision déjà actée → nouvel ADR qui *remplace* l'ancien (ne jamais réécrire un ADR accepté).

### Comment
1. Copier le gabarit ci-dessous dans `docs/decisions/NNNN-titre-court.md` (`NNNN` = prochain numéro libre).
2. Remplir ; statut initial `Proposé`.
3. Faire valider par les rôles concernés → passer à `Accepté`.
4. Ajouter la ligne dans l'index [`docs/decisions/README.md`](./docs/decisions/README.md).
5. Lier l'ADR depuis les tâches/specs concernées (par ID).

### Gabarit

```markdown
# ADR-NNNN — <titre de la décision>
- Statut : Proposé | Accepté | Remplacé par ADR-XXXX | Déprécié
- Date de la décision : AAAA-MM-JJ
- Décideurs : <rôles : ENG / AUD / ELEC / JEU / ÉQUIPE>
- Contexte projet : <session / jalon / tâche>
- Liens : <R- / C- / H- / E- / tâches / autres ADR>

## Contexte et problème
## Options envisagées        (A … pour/contre · B … pour/contre)
## Décision
## Conséquences              (positives · négatives · risques)
## Suivi / quand re-questionner
```

## Convention de commits

Le projet utilise les **Conventional Commits** : `feat:`, `fix:`, `docs:`, `refactor:`, `style:`, `test:`, `chore:`.
- Lier le commit aux IDs concernés quand pertinent (ex. `feat: GamepadMapper (TECH-05)`).
- Une décision est consignée **avec son ADR** dans le même commit/PR (`docs: ADR-0008 choix du MCU (S7-T06)`).

## Tags de jalons

Taguer les jalons clés pour matérialiser la timeline des livraisons :
`interfaces-gelees`, `jeu-v1-pc`, `choix-mcu`, `RPC1`, `RPC2`, `manette-operationnelle`, `RLP`.

## Traçabilité

Garde la chaîne intacte : **besoin → requis (`R-`) / contrainte (`C-`) / hypothèse (`H-`) → décision (`ADR-`) → tâche (`TACHES`) → code/PCB → commit/tag**. Une seule **source de vérité** par fait ; les autres documents y *renvoient* (par ID) plutôt que de la dupliquer.
