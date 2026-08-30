---
title: Design
status: draft
updated: 2026-08-30
owner: bryan
---

# Design

Aucun langage visuel n'est arrêté : ni système de design, ni bibliothèque de composants, ni méthode de style.
Ce fichier ne porte donc que les contraintes que l'architecture impose déjà à l'interface.

## 🧩 Ce qui est décidé

- React et Vite, en SPA dans le renderer Electron.
- Un dossier par pilier sous `src/renderer/features/`, les composants partagés sous `src/renderer/components/`.

## ⏳ Toute vue doit tenir un état partiel

L'indexation tourne en arrière-plan et ne bloque jamais l'interface.
Une vue ne peut donc pas supposer que ses données sont complètes : l'état partiel est un état normal, pas une erreur à afficher.

C'est une contrainte de conception, pas une optimisation à ajouter plus tard.

## ❓ Reste à trancher

- Système de design : tokens maison, bibliothèque, ou ad hoc.
- Méthode de style.
- Barre d'accessibilité : contraste, focus, ARIA.

Ces choix se prendront au montage du renderer.
