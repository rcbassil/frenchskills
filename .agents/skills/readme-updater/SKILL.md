---
name: readme-updater
description: Met à jour le fichier README.md du projet avec une documentation complète et à jour, incluant les descriptions, les instructions d'installation, les étapes d'exécution et des exemples. Utilisez cette compétence lorsque l'utilisateur demande à mettre à jour la documentation du projet ou les détails du README.
---

# Compétence : Mise à jour du README

Lorsque le projet subit des changements structurels ou fonctionnels, ou lorsque cela est explicitement demandé, vous DEVEZ vous assurer que le fichier `README.md` reflète fidèlement l'état actuel du projet.

## Instructions

1. **Analyser l'état du projet** : Commencez par examiner la structure des fichiers du projet, les fichiers de configuration et de dépendances (par ex. `pyproject.toml`, `requirements.txt`) ainsi que les points d'entrée principaux afin de comprendre le rôle du projet et les commandes qui le pilotent.
2. **Mise à jour du fichier** : Localisez ou créez le fichier `README.md` à la racine du projet.
3. **Maintenir les sections obligatoires** : Restructurez ou rédigez le `README.md` de sorte qu'il contienne toujours les sections suivantes, clairement définies :
   - **Titre et description** : Une explication claire et globale de l'objectif et des fonctionnalités du projet.
   - **Installation / Déploiement** : Instructions pas à pas pour installer les dépendances nécessaires ou déployer le projet de zéro. Inclure les prérequis si nécessaire.
   - **Lancement de l'application** : Instructions précises et commandes exactes pour exécuter le projet ou démarrer le serveur en local.
   - **Exemples d'utilisation & commandes** : Commandes terminal pratiques ou extraits de code illustrant comment les utilisateurs peuvent interagir avec les outils ou APIs fournis.
4. **Exactitude & contexte** : Vérifiez en croisant les scripts ou commandes terminal documentés pour vous assurer qu'ils existent bien dans le projet et sont entièrement corrects.

## Exemple de formatage

```markdown
# [Nom du projet]

[Brève description du projet détaillant le problème qu'il résout et ses principales fonctionnalités.]

## Prérequis

Listez les exigences système.
- Python 3.12+

## Installation & Déploiement

Instructions pour installer et préparer l'environnement.

\`\`\`bash
pip install -r requirements.txt
# ou
poetry install
\`\`\`

## Lancement de l'application

Pour exécuter l'application en local :

\`\`\`bash
python src/main.py
\`\`\`

## Exemples d'utilisation

Voici quelques exemples d'exécution de commandes spécifiques :

\`\`\`bash
# Exemple d'exécution du linter
flake8 .

# Exemple d'exécution des tests
pytest tests/
\`\`\`
```
