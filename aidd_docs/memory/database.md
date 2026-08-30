---
title: Base de données
status: draft
updated: 2026-08-30
owner: bryan
---

# Base de données

Aucun schéma n'est écrit.
Le choix du moteur est explicitement laissé ouvert.

## ⚙️ Mise en place

- SQLite locale, fichier `claudit.db`. Tout reste sur la machine, il n'y a pas de serveur.
- Adaptateur mince dans `src/main/db/`, qui isole le moteur du reste du code.
- Volume de référence : 210 k enregistrements, pire agrégat mesuré à 85 ms.

## ⚖️ Le moteur reste à trancher

Aucune des deux options n'est confortable.
L'arbitrage se fera au premier jet d'implémentation, sur une mesure du corpus réel.

| | `node:sqlite` | `better-sqlite3@13` |
| --- | --- | --- |
| Binaire natif | Aucun | N-API, 8 prébuilds, 27 Mo installés |
| Maturité | Release candidate depuis deux ans, jamais stabilisée | Passé en N-API le 2026-07-21 |
| Mesuré sous charge | Non | Oui — 6,5 s sur 1,6 Go |

Les deux API sont proches : `node:sqlite` a été modelée sur `better-sqlite3`.
C'est ce qui rend l'adaptateur peu coûteux, et c'est la raison pour laquelle la décision peut attendre.

> [!WARNING]
> `better-sqlite3@13` segfault sous Node 20. Node ≥ 22 est un prérequis, pas un confort.

## 🧰 Réglages d'ingestion

Ces quatre réglages sont décidés, pas négociables, et conditionnent la tenue de la première indexation.

| Réglage | Raison |
| --- | --- |
| `journal_mode=WAL` | Lecture concurrente pendant l'ingestion |
| `synchronous=NORMAL` | Débit d'écriture, sur une base locale reconstructible |
| Transactions par lots | Une transaction par enregistrement effondre le débit |
| Index créés après ingestion | Les maintenir pendant l'insertion coûte plus qu'un rebuild |

La base est reconstructible depuis les transcripts : sa perte n'est pas une perte de données.
