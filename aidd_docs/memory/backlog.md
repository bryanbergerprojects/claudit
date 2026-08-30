---
title: Backlog
status: draft
updated: 2026-08-30
owner: bryan
---

# Backlog

Ni le dépôt ni le projet GitHub n'existent encore.
Le processus est celui de `louise`, repris à l'identique par décision.

## 🧭 Supports

| Support | Autorité sur | Rôle |
| --- | --- | --- |
| GitHub Issues, dépôt `bryanbergerprojects/claudit` | type, titre, corps, relations | seul dépôt des éléments de backlog |
| GitHub Project v2 dédié à claudit | statut de cycle de vie | tableau de pilotage |
| `aidd_docs/tasks/<yyyy_mm>/<yyyy_mm_dd>_<slug>/` | détail d'exécution : plan, phases, critères | source citée, jamais recopiée |

Aucun artifact de backlog n'est écrit en Markdown sous `aidd_docs/backlog/`.
C'est la destination par défaut des skills `aidd-pm` ; ici l'autorité est GitHub, et un artifact n'existe jamais sur deux supports à la fois.

## 🧩 Structure

| Niveau | Contient | Convention |
| --- | --- | --- |
| Epic | plusieurs Tasks ou User Stories | un résultat qui demande plusieurs tranches |
| User Story | zéro ou plusieurs Tasks | un comportement livrable seul |
| Task | rien | travail borné, sans valeur utilisateur |
| Spike | rien | investigation bornée dans le temps |
| Defect | rien | écart constaté sur un comportement existant |

## 🏷️ Représentation

Les issue types natifs sont activés au niveau de l'organisation `bryanbergerprojects`, donc disponibles pour claudit dès la création du dépôt.
La nature d'un élément se lit dans son type, jamais dans un label.

| Artifact | Issue type natif |
| --- | --- |
| Epic | `Epic` |
| User Story | `Feature` |
| Task | `Task` |
| Spike | `Spike` |
| Defect | `Bug` |

Les labels sont thématiques et se répliquent depuis `bryanbergerprojects/louise` : `⬆️ CI/CD`, `📉 Tech debt`, `📘 Documentation`, `🔐 Security`, `❌ Blocked`, `❓Needs info` et les autres.
Aucun ne porte de type ni de statut.

## 🔄 Cycle de vie

Le champ `Status` du projet porte le cycle de vie complet.
L'état ouvert ou fermé de l'issue n'en distingue que deux points et ne suffit donc pas.

| Statut projet | Sens |
| --- | --- |
| `Backlog` | proposé, pas encore prêt |
| `Ready` | prêt, périmètre et critères arrêtés |
| `In Progress` | en cours |
| `In Review` | pull request ouverte, revue attendue |
| `Done` | terminé, critères vérifiés |

## 📐 Planification

- Priorité : aucune convention. Les champs `Priority` et `Size` existent sur le projet `louise` sans options définies.
- Ordre : porté par les dépendances, pas par un score.
- Itération et jalon : aucun.

## 🔗 Relations

| Relation | Représentation native |
| --- | --- |
| parent | sub-issue — `POST /repos/{owner}/{repo}/issues/{number}/sub_issues`, champ `sub_issue_id` |
| depends_on | `POST /repos/{owner}/{repo}/issues/{number}/dependencies/blocked_by`, champ `issue_id` |
| source | lien absolu vers le fichier sur `main`, dans le corps |

Une relation est stockée une seule fois, dans sa représentation native, jamais recopiée en texte : deux copies divergent.

Les deux endpoints attendent l'identifiant interne numérique de l'issue, pas son numéro visible.
Ils exigent `-F` dans `gh api`, qui envoie un entier ; `-f` envoie une chaîne et échoue sans message exploitable.

## ✍️ Corps d'issue

Corps en français, structuré en sections H2 à emoji sémantique, dans cet ordre.

| Section | Contenu |
| --- | --- |
| `## 🎯 Résultat attendu` | l'état visé, en une phrase |
| `## 📐 Périmètre` | deux blocs, **Inclut** et **Exclut** |
| `## ✅ Terminé quand` | cases à cocher, issues des critères |
| `## 🔍 Preuve de complétion` | ce qui atteste le résultat |
| `## 🔗 Relations` | table, dont une ligne `Source` |

Un Epic ajoute `## 💡 Contexte et valeur` en tête et `## ⚠️ Dépendances et inconnues` en fin.
