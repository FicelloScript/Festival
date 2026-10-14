# Contribuer au projet Festival 026a

## Branches

| Branche | Rôle |
|---|---|
| `main` | Production. Protégée : aucun push direct, merge uniquement par PR approuvée. |
| `Preprod` | Pré-production, validée avant passage sur `main`. |
| `Dev` | Branche d'intégration. Toutes les branches de tâche partent de `Dev` et y reviennent. |

Les branches de tâche suivent le format `type/numero-issue-description` :

- `feature/` : nouvelle fonctionnalité ou nouvelle page (ex. `feature/6-page-accueil`)
- `fix/` : correction d'un bug (ex. `fix/12-lien-contact`)
- `hotfix/` : correction urgente sur `main` (ex. `hotfix/15-lien-menu-casse`)
- `docs/` : documentation (ex. `docs/1-readme`)
- `style/` : mise en forme CSS (ex. `style/5-feuille-de-base`)

Noms en minuscules, mots séparés par des tirets, sans accents.

## Commits

Format : `type: description courte`

- `feat:` ajout de contenu ou de fonctionnalité
- `fix:` correction de bug
- `style:` modification CSS ou de mise en forme
- `docs:` documentation
- `refactor:` réorganisation du code sans changement visible

Règles :
- un commit = un changement cohérent (commits atomiques) ;
- description en français, à l'infinitif ou au présent (ex. `feat: ajouter le formulaire de contact`) ;
- pas de messages vagues comme `modif`, `test` ou `update`.

## Démarche pour une tâche

1. Prendre une issue sur le tableau Projects, s'assigner et la passer en *In progress*.
2. Partir de la dernière version de `Dev` :
```bash
   git switch Dev
   git pull
   git switch -c feature/numero-description
```
3. Committer régulièrement, puis pousser la branche :
```bash
   git push -u origin feature/numero-description
```
4. Ouvrir une Pull Request vers `Dev`.

## Pull Requests

- Base : `Dev` (sauf hotfix : base `main`).
- La description explique **quoi** et **pourquoi**, et se termine par `Closes #numero` pour lier l'issue.
- Ajouter un reviewer, s'assigner, lier le projet, passer la carte en *In review*.

## Revue de code

- Une PR est relue et approuvée par **un autre membre que son auteur**. On ne merge jamais sa propre PR.
- Chaque membre relit **au moins 2 PR** et laisse au moins un commentaire utile.
- Les commentaires sont constructifs : ce qui ne va pas, pourquoi, et une proposition.
- L'auteur corrige suite aux remarques dans de nouveaux commits sur la même branche, puis répond aux commentaires.

## Conflits

1. Mettre à jour sa branche avec `Dev` :
```bash
   git switch Dev
   git pull
   git switch ma-branche
   git merge Dev
```
2. Résoudre les conflits dans VS Code en gardant les changements des deux côtés quand c'est pertinent, en accord avec l'autre personne concernée.
3. Committer la résolution, pousser, et documenter le conflit dans la PR (fichier concerné, cause, choix fait).

## Hotfix

1. Créer la branche depuis `main` : `git switch main`, `git pull`, `git switch -c hotfix/numero-description`.
2. Corriger, ouvrir une PR vers `main`, traitée en priorité.
3. Une fois mergée, reporter la correction sur `Preprod` et `Dev` via PR.

## Mise en production

`Dev` → `Preprod` → `main`, toujours par Pull Request approuvée.