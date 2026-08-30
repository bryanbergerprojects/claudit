---
title: Navigation
status: draft
updated: 2026-08-30
owner: bryan
---

# Navigation

Aucun routeur n'est choisi.
La carte ci-dessous vient du découpage de `src/renderer/features/`, décidé dans `aidd_docs/INSTALL.md`.

## 🗺️ Les sections

Le diagramme montre les cinq zones de l'application, une par dossier de `features/`.

```mermaid
%%{init: {'theme':'base','themeVariables':{'fontFamily':'ui-sans-serif, system-ui, sans-serif','lineColor':'#94a3b8','primaryTextColor':'#334155'}}}%%
flowchart LR
    Dash(["dashboard"])
    Edit["editor"]
    Costs["costs"]
    Audit["audit"]
    Opti["optimize"]

    Dash --> Edit & Costs & Audit & Opti

    classDef neutre fill:#f8fafc,stroke:#94a3b8,color:#334155
    classDef bleu fill:#eff6ff,stroke:#3b82f6,color:#1e3a8a

    class Dash neutre
    class Edit,Costs,Audit,Opti bleu
```

`dashboard` est l'entrée ; les quatre autres sections portent chacune un pilier — éditer, mesurer, auditer, optimiser.

## 🔓 Routes protégées

Aucune. L'application est locale et mono-utilisateur, il n'y a pas d'authentification.

## ❓ Reste à trancher

Le routeur, et la façon dont une section s'affiche pendant que l'indexation est encore en cours.
