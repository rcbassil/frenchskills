---
name: git-commit-formatter
description: Formate les messages de commit git selon la spécification Conventional Commits. Utiliser lorsque l'utilisateur demande de commiter des changements ou d'écrire un message de commit.
---

# Compétence : Formateur de Messages de Commit Git

Lors de la rédaction d'un message de commit git, vous DEVEZ suivre la spécification Conventional Commits.

## Format

`<type>[portée optionnelle]: <description>`

## Types Autorisés

- **feat** : Une nouvelle fonctionnalité
- **fix** : La correction d'un bug
- **docs** : Modifications de la documentation uniquement
- **style** : Modifications n'affectant pas le sens du code (espaces, formatage, etc.)
- **refactor** : Une modification du code qui ne corrige pas un bug ni n'ajoute une fonctionnalité
- **perf** : Une modification du code qui améliore les performances
- **test** : Ajout de tests manquants ou correction de tests existants
- **chore** : Modifications du processus de build ou des outils et bibliothèques auxiliaires tels que la génération de documentation

## Instructions

1. Analyser les changements pour déterminer le `type` principal.
2. Identifier la `portée` si applicable (ex. : composant ou fichier spécifique).
3. Rédiger une `description` en français et concise à l'impératif (ex. : « ajouter une fonctionnalité » et non « a ajouté une fonctionnalité »).
4. En cas de changements majeurs incompatibles, ajouter un pied de page commençant par `BREAKING CHANGE:`.

## Exemple

`feat(auth): implémenter la connexion avec google`
