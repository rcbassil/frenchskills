# French Skills

French Skills est une collection de compétences (skills) personnalisées conçues pour les assistants IA, visant à automatiser des tâches courantes de développement, de documentation et de sécurité.

## Prérequis

- **Python 3.12+**
- **uv** (recommandé pour la gestion des dépendances et de l'environnement) : [Installation de uv](https://github.com/astral-sh/uv)

## Installation & Déploiement

Pour préparer l'environnement de développement :

```bash
# Avec uv
uv sync

# Ou avec pip
pip install .
```

## Structure du Projet

Le projet est organisé autour de fichiers de définition de compétences :

- `SKILL.md` (racine) : Contient la définition de la compétence **Analyseur de Vulnérabilités**.
- `.agents/skills/` : Dossier contenant d'autres compétences modulaires.
- `main.py` : Point d'entrée simple pour tester l'environnement Python.

## Skills Disponibles

### 1. Analyseur de Vulnérabilités (`vulnerability-scanner`)
Effectue des audits de sécurité complets :
- **SCA** : Détection de CVE (via `pip-audit`, `safety`).
- **SAST** : Analyse statique du code source (via `bandit`, `semgrep`).
- **IaC** : Vérification de la configuration d'infrastructure (via `trivy`, `checkov`).

### 2. Mise à jour du README (`readme-updater`)
Automatise la génération et la maintenance de la documentation du projet pour s'assurer qu'elle reste synchronisée avec l'évolution du code.

### 3. Formateur de Commits (`git-commit-formatter`)
Assure que tous les messages de commit respectent la spécification **Conventional Commits** (`feat`, `fix`, `docs`, etc.), facilitant ainsi la génération automatique de changelogs.

## Engagement de Sécurité

Le projet `frenchskills` suit des standards de sécurité rigoureux. Des audits automatisés de composition logicielle (SCA) et de tests statiques de sécurité (SAST) sont réalisés régulièrement pour garantir l'absence de vulnérabilités connues et de failles de configuration.

## Lancement de l'application

Pour exécuter le point d'entrée principal :

```bash
uv run main.py
```

## Exemples d'utilisation

### Lancer une analyse de sécurité (exemple via uv)
```bash
uv run --with pip-audit pip-audit
```

---
*Ce projet est maintenu pour assurer des standards élevés de développement et de sécurité via l'IA.*
