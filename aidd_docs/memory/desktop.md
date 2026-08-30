---
title: Application de bureau
status: draft
updated: 2026-08-30
owner: bryan
---

# Application de bureau

## 🖥️ Cadre

Electron, choisi parce que TypeScript est le seul langage maîtrisé.
Rust étant exclu de fait, Tauri l'a été aussi.

Trois processus, pas deux.

| Processus | Fichier d'entrée | Rôle |
| --- | --- | --- |
| Principal | `src/main/index.ts` | Base, configuration, appels API, IPC |
| Utilitaire | `src/ingest/index.ts` | Scan et ingestion, hors du fil de l'interface |
| Renderer | `src/renderer/main.tsx` | React |

Le processus utilitaire n'est pas un confort : il sort l'API SQLite synchrone du fil de l'interface.
Un `worker_threads` aurait fait l'affaire, mais Vite ne sait pas encore empaqueter un worker Node — la PR amont est ouverte depuis novembre 2025.

## 🔓 Accès natif

| Accès | Zone | Portée |
| --- | --- | --- |
| Lecture-écriture de `~/.claude` | `src/main/config/` | Fichiers de configuration, deux emplacements |
| Lecture des transcripts JSONL | `src/ingest/` | Source primaire |
| Lecture d'`usage.db` | `src/ingest/` | Optionnelle, échec toléré |
| Réseau sortant | `src/main/recommend/` | API Anthropic seule, désactivée hors ligne |

`src/core/` n'accède à rien : il ne connaît ni `electron` ni `node:fs`.
Toute lecture disque passe donc par `main` ou `ingest`.

> [!IMPORTANT]
> La surface d'édition dépasse `~/.claude`.
> Chez l'auteur, `~/.claude/agents/`, `rules/` et `skills/` sont vides : les skills et agents réels vivent dans `~/.claude/plugins/`.
> Le pilier éditer doit couvrir les deux emplacements, sans quoi il n'affiche rien.

## ⏱️ Budget de démarrage

La coquille doit être interactive en moins de trois secondes, quoi qu'il arrive.
L'indexation tourne en arrière-plan sans jamais bloquer l'interface, et toute vue doit savoir s'afficher dans un état de données partielles.

## 📦 Empaquetage et mise à jour

Voir `deployment.md` : `electron-builder`, absence de signature, et ses conséquences sur macOS.
