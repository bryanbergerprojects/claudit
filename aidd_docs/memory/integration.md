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
| Claude Usage (`usage.db`) | Accélérateur d'ingestion, optionnel | `src/ingest/` |

`~/.claude` n'est pas un service : c'est la source de données primaire, lue et écrite par `src/main/config/`.

## 🤖 API Anthropic

- Clé lue depuis une variable d'environnement, **optionnelle**.
- L'application doit démarrer et fonctionner sans elle : seul le pilier optimiser se désactive.
- Aucun appel hors ligne, sans exception.

## ⚠️ `usage.db` n'est jamais une source de vérité

Le fichier appartient à un outil tiers nommé Claude Usage.
Les transcripts JSONL restent la source primaire ; `usage.db` n'est qu'un accélérateur.

Trois défauts imposent la méfiance.

| Défaut | Conséquence |
| --- | --- |
| `schema_meta` sans numéro de version | Introspection `PRAGMA table_info` à chaque ouverture, jamais de schéma supposé |
| Table `agents` vide | Aucune donnée d'agent n'en vient |
| `journal_mode` à `delete` | Un journal chaud laissé par un plantage de l'autre outil empêche toute ouverture en lecture seule |

L'échec silencieux est toléré et attendu : l'ingestion continue sur les JSONL seuls.

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
