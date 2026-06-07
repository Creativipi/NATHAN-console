# Diagrammes d'architecture

Diagrammes versionnés dans le repo (source synchronisée depuis le OneDrive de l'équipe) pour que le dépôt soit **auto-suffisant** pour un contributeur externe.

| Fichier | Décrit |
|---------|--------|
| `console.drawio` / `console.drawio.png` / `console.mmd` | Architecture **système** de la console (game engine, interfaces, blocs matériels) |
| `ide.drawio` / `ide.drawio.png` / `ide.mmd` | Architecture de l'**IDE** accessible |

**Ouvrir / éditer :**
- `.drawio` → [draw.io](https://app.diagrams.net/) ou l'extension *Draw.io Integration* de VS Code (le `.png` est un aperçu rapide, sans outil).
- `.mmd` → [Mermaid](https://mermaid.live/) ou un aperçu Markdown compatible Mermaid.

> Le diagramme système matérialise l'architecture **en contrats d'interface** décidée en [ADR-0001](../decisions/0001-architecture-pc-first-interfaces.md) (le game engine est agnostique du matériel). Toute évolution majeure de l'architecture doit s'accompagner d'un ADR.
