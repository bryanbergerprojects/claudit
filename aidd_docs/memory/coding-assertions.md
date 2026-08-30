---
title: Portes de validation
status: draft
updated: 2026-08-30
owner: bryan
---

# Portes de validation

## 🚧 État actuel

Aucune porte n'est câblée : il n'y a ni `package.json`, ni `biome.json`, ni `vitest.config.ts`.
Les outils sont arrêtés — Biome pour le lint et le format, Vitest pour les tests, `tsc` pour le typage — mais aucune commande listée ci-dessous n'est encore exécutable.

Ce fichier se réécrit au montage de la pile, avec les commandes réelles du `package.json`.

## ✅ Avant commit

La porte rapide, telle qu'elle est prévue.

| Ordre | Commande | Vérifie |
| --- | --- | --- |
| 1 | `biome check` | Format, lint, tri des imports, et la frontière du noyau |

La frontière du noyau n'est pas une convention à relire : c'est un `override` Biome sur `src/core/**` qui interdit l'import d'`electron`.
Elle doit être éprouvée par un import fautif volontaire au montage, sinon rien ne prouve que la règle mord.

## 🚀 Avant push

La porte lourde, telle qu'elle est prévue.

| Ordre | Commande | Vérifie |
| --- | --- | --- |
| 1 | `tsc --noEmit` | Typage |
| 2 | `vitest run` | Tests |

## 🤖 Comportement

Si un correctif est nécessaire, lancer un agent par assertion à réparer — typage, tests, règles violées par catégorie d'interface font trois agents.
