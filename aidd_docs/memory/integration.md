---
title: Intégrations
status: draft
updated: 2026-08-30
owner: bryan
---

# Intégrations

Les services extérieurs et leurs pièges.
La carte macro appartient à `ecosystem.md`.

## 🔌 Services externes

| Service | Sert à | Point d'intégration |
| --- | --- | --- |
| API Anthropic | Recommandations d'optimisation | `src/main/recommend/` |

L'API Anthropic est le seul service extérieur, et il est optionnel.

`~/.claude` n'est pas un service : c'est la source de données primaire, lue et écrite par `src/main/config/`.

## 🤖 API Anthropic

- Clé lue depuis une variable d'environnement, **optionnelle**.
- L'application doit démarrer et fonctionner sans elle : seul le pilier optimiser se désactive.
- Aucun appel hors ligne, sans exception.

## 🚫 Aucune base d'un outil tiers

`usage.db` a été envisagée comme accélérateur d'ingestion, puis écartée.
Le fichier appartient à Claude Usage, un tableau de bord tiers : ni Anthropic ni claudit n'en maîtrisent le schéma.

Les transcripts JSONL sont la seule source de consommation, et ils suffisent.

| Raison du retrait | Détail |
| --- | --- |
| Aucun gain | 1,6 Go ingérés en 6,46 s |
| Schéma non maîtrisé | `schema_meta` sans version, `agents` vide |
| Lecture faillible | `journal_mode` à `delete`, journal bloquant |

## 💶 Le coût se calcule sur sept dimensions

Un produit entrée fois prix, plus sortie fois prix, donne un chiffre faux.
Le champ `usage` d'une ligne `assistant` porte davantage.

| Dimension | Ce qu'elle change |
| --- | --- |
| Cache une heure | Tarif d'écriture propre |
| Cache cinq minutes | Tarif d'écriture différent du précédent |
| Lecture de cache | Tarif propre, distinct de l'entrée |
| Entrée | Tarif de base |
| Sortie | Tarif de base |
| Tokens de réflexion | Isolés, comptés à part |
| Requêtes d'outils serveur | Comptées séparément |

Le `service_tier` de la ligne conditionne la grille appliquée.
La grille est donc un modèle versionné dans le temps, puisque les tarifs évoluent : un enregistrement ancien se retarife avec la grille de sa date, jamais avec celle du jour.
