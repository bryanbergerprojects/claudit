---
title: Tests
status: draft
updated: 2026-08-30
owner: bryan
---

# Tests

Aucun test n'existe et aucun exécuteur n'est installé.
Vitest est arrêté comme choix ; ce qui suit est la stratégie décidée, pas une pratique observée.

## 🎯 Stratégie

Le découpage suit la frontière du noyau, qui est ce qui rend le projet testable.

| Couche | Couvre | Coût |
| --- | --- | --- |
| Unitaire sur `src/core/` | Parsing, tarification, règles d'audit, scoring | Aucun Electron, aucun disque |
| Intégration sur `src/main/db/` | Schéma, migrations, adaptateur SQLite | Une base temporaire |
| Bout en bout | Non décidé | — |

`src/core/` n'important ni `electron` ni `node:fs`, ses tests tournent dans un simple processus Node.
C'est le bénéfice direct de la discipline de frontière, pas un effet secondaire.

## 🛠️ Outils

- Vitest, qui exige Vite ≥ 6 — c'est cette contrainte qui a écarté Electron Forge, voir `deployment.md`.

## ⚠️ Ce que les tests doivent couvrir en priorité

Deux zones concentrent le risque de résultat faux plutôt que de plantage.

| Zone | Pourquoi |
| --- | --- |
| Calcul de coût | Sept dimensions ; une erreur produit un chiffre plausible et faux |
| Lecture d'`usage.db` | Schéma tiers sans version, l'échec doit rester silencieux et sans perte |

## ▶️ Lancer

`vitest run` une fois la pile montée. La commande n'existe pas encore.
