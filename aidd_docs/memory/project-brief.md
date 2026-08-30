---
title: Brief projet
status: draft
updated: 2026-08-30
owner: bryan
---

# Brief projet

## 🎯 Ce que c'est

claudit est une application de bureau locale qui rend la configuration de Claude Code visible, auditable et rentable.
Elle remplace l'édition manuelle des fichiers de `~/.claude` par une interface unique.

Side project personnel, open source, sans enjeu commercial.
Sa cible est son auteur, puis quelques développeurs amis.

## 💡 Pourquoi il existe

Trois manques, dont un qu'aucun outil ne traite.

| Manque | Ce que claudit apporte |
| --- | --- |
| La configuration s'édite à la main, fichier par fichier | Une interface unique sur `~/.claude` et `~/.claude/plugins/` |
| La consommation de tokens n'est pas convertie en coût | Une équivalence API, qui répond à la rentabilité d'un forfait face à la facturation à l'usage |
| La qualité des skills et agents n'est pas mesurée | Un audit contre les bonnes pratiques, croisé avec le coût |

## 🗣️ Vocabulaire du domaine

Ces termes viennent de Claude Code, pas du projet.
Un contributeur doit les connaître pour lire le code.

| Terme | Sens |
| --- | --- |
| transcript | Fichier JSONL d'une session, source primaire de la consommation |
| skill, agent, plugin | Unités de configuration éditables, réparties entre `~/.claude` et `~/.claude/plugins/` |
| `service_tier` | Champ d'une ligne `assistant` qui conditionne la grille tarifaire appliquée |
| tokens de réflexion | Tokens de raisonnement, comptés à part dans le champ `usage` |
| grille tarifaire | Modèle de prix versionné dans le temps, puisque les tarifs évoluent |
| pilier | Une des quatre fonctionnalités, chacune sa zone dans le renderer |

## 🧩 Les quatre piliers

| Pilier | Fait |
| --- | --- |
| Éditer | Lit et écrit la configuration, sur les deux emplacements |
| Mesurer | Convertit la consommation réelle en coût API équivalent |
| Auditer | Confronte skills, agents et prompts aux bonnes pratiques |
| Optimiser | Croise qualité et coût pour désigner ce qui mérite un effort |
