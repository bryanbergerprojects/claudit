---
title: Gestion de versions
status: draft
updated: 2026-08-30
owner: bryan
---

# Gestion de versions

Le dépôt existe : <https://github.com/bryanbergerprojects/claudit>, public, branche `main`.
Les conventions ci-dessous sont celles du projet `louise`, reprises à l'identique par décision.

## ⚙️ Mise en place

- Branche principale : `main`
- Plateforme : GitHub, dépôt `bryanbergerprojects/claudit`, **public dès la création**
- Licence : MIT, fichier `LICENSE` à la racine

La licence diffère de celle de `louise`, qui est en AGPL-3.0-or-later.
claudit est un outil que des tiers installent sur leur machine : la permissivité prime sur la réciprocité.

## 🗣️ Langue

Issues, corps des pull requests, threads de revue et documentation : français.
Messages de commit et titres de pull requests : anglais.

Seule exception dans un corps de PR rédigé en français : le mot-clé de fermeture, qui reste anglais.

## 🌿 Branches

- Format : `{type}/{issue_number}` — `feat/12`, `fix/34`, `docs/7`
- Types en usage : `feat`, `fix`, `chore`, `docs`, `refactor`, `test`

Toute branche part d'une issue : le numéro suffit à l'identifier, le titre de l'issue porte la description.
Pas d'issue, pas de branche — l'issue se crée d'abord.

## 💬 Commits

- Convention : Conventional Commits — <https://www.conventionalcommits.org>
- Format : `type(scope): description`
- Règles : impératif, minuscule, pas de point final

claudit n'est pas un monorepo : le `scope` suit les zones de `src/`, soit `core`, `ingest`, `main`, `preload`, `renderer`, `db`, `config`, `recommend`, `ipc`, plus `deps` et `ci`.
Le scope reste facultatif : un commit racine n'en a pas.

## 🤖 Stratégie de commit

L'IA commite d'elle-même : `after phase`.

## 🔀 Pull requests

Toute PR s'ouvre en `ready for review` et assignée à `BryanBerger98`, jamais en brouillon.

Le brouillon n'a aucun emploi sur un dépôt à un seul contributeur : il n'appelle ni revue ni fusion, il ne fait que retarder les deux.
L'assignation est le seul filtre qui remonte une PR dans `gh pr list --assignee @me` et dans le tableau de bord GitHub.

```bash
gh pr create --base main --title "…" --body-file … --assignee "@me"
```

`gh pr create` ouvre en `ready` par défaut : c'est `--draft` qu'il ne faut pas passer.
Le skill `aidd-vcs:02-pull-request` fait l'inverse et crée un brouillon — une ouverture ratée se rattrape avec `gh pr ready <n>`.

Le titre suit Conventional Commits, à l'identique d'un message de commit : `type(scope): description`.
La fusion est en squash seul, le titre de la PR devenant mot pour mot le message de commit sur `main` — d'où l'anglais, l'impératif, la minuscule et l'absence de point final.

Toute PR ouverte pour une issue la ferme explicitement : `Closes #<n>` dans le corps.

> [!WARNING]
> GitHub ne reconnaît que les mots-clés anglais — `close`, `fix`, `resolve` et leurs variantes.
> Un `Ferme #2` ne produit qu'une mention : l'issue reste ouverte après la fusion.

## 🧾 État de l'initialisation

Les réglages de `louise` ont été répliqués le 2026-08-30, avec deux écarts assumés.

| Élément | État |
| --- | --- |
| Protection de `main` | ✅ PR obligatoire, conversations à résoudre |
| Fusion en squash seule | ✅ `PR_TITLE` et `BLANK` |
| Labels thématiques | ✅ quinze labels, répliqués de `louise` |
| GitHub Project v2 | ✅ projet `claudit`, lié au dépôt |
| Contexte CI exigé sur `main` | ❌ écarté |
| Champs `Priority` et `Size` | ❌ non créés |
| Hooks git locaux | ⏳ non décidés |

Le contexte CI `verify` de `louise` a été écarté, faute de workflow de vérification ici.
GitHub Actions ne construit que les releases — voir `deployment.md` — donc un check requis ne tournerait jamais et bloquerait toute fusion définitivement.
Le réglage est à rebrancher le jour où un tel workflow existe.

`Priority` et `Size` existent sur `louise` sans aucune option, ce que l'API GraphQL refuse de créer.
Lefthook attend un `package.json`, qui n'existe pas encore.

> [!WARNING]
> `enforce_admins` est à `false`, comme sur `louise`.
> La protection documente donc la poussée directe sur `main` comme interdite, sans l'empêcher pour un administrateur du dépôt.
