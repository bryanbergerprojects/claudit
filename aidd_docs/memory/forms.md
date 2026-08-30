---
title: Formulaires
status: draft
updated: 2026-08-30
owner: bryan
---

# Formulaires

Ni bibliothèque de formulaires ni bibliothèque de validation n'est choisie.

## 🎯 Ce que les formulaires devront faire

Le pilier éditer est un éditeur de configuration : ses formulaires écrivent des fichiers réels sous `~/.claude` et `~/.claude/plugins/`.

Deux exigences en découlent, et elles précèdent le choix d'outil.

| Exigence | Pourquoi |
| --- | --- |
| Validation avant écriture | Un fichier de configuration invalide casse Claude Code, pas seulement claudit |
| Écriture sur deux emplacements | La surface réelle dépasse `~/.claude` — voir `desktop.md` |

## ❓ Reste à trancher

Bibliothèque de formulaires, bibliothèque de validation, et emplacement de la logique partagée.
Ces choix se prendront au montage du pilier éditer.
