# Compétence Draw.io pour Claude Code

Une compétence Claude Code qui génère des fichiers `.drawio` natifs, avec export optionnel en PNG, SVG ou PDF (avec XML intégré pour que le fichier exporté reste modifiable dans draw.io). Aucune configuration MCP requise.

## Comment ça fonctionne

Lorsque vous demandez à Claude Code de créer un diagramme, il va :

1. Générer le XML draw.io pour le diagramme demandé
2. L'écrire dans un fichier `.drawio` dans votre répertoire courant
3. Si vous avez demandé un format d'export, exporter via la CLI draw.io desktop
4. Ouvrir le résultat

## Prérequis

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installé
- [draw.io Desktop](https://github.com/jgraph/drawio-desktop/releases) installé (requis pour l'export PNG/SVG/PDF)

## Utilisation

```
/drawio créer un organigramme pour la connexion utilisateur
```

Par défaut, cela écrit un fichier `.drawio` et l'ouvre dans draw.io. Pour exporter vers un format image, mentionnez le format dans votre demande :

```
/drawio png organigramme pour la connexion utilisateur    → login-flow.drawio.png
/drawio svg : diagramme ER pour e-commerce               → er-diagram.drawio.svg
/drawio pdf vue d'ensemble architecture                  → architecture-overview.drawio.pdf
```

Autres exemples :

```
/drawio diagramme de séquence pour l'authentification API
/drawio png diagramme de classes pour les modèles dans src/
```

## Formats d'export

| Format       | Extension     | Notes                                                       |
| ------------ | ------------- | ----------------------------------------------------------- |
| (par défaut) | `.drawio`     | XML natif, modifiable dans draw.io, CLI desktop non requise |
| `png`        | `.drawio.png` | Lisible partout, XML intégré, modifiable dans draw.io       |
| `svg`        | `.drawio.svg` | Vectoriel, XML intégré, modifiable dans draw.io             |
| `pdf`        | `.drawio.pdf` | Imprimable, XML intégré, modifiable dans draw.io            |

La double extension `.drawio.*` indique que le fichier contient du XML de diagramme intégré. Ouvrez n'importe lequel de ces fichiers dans draw.io pour récupérer et modifier le diagramme complet. Le fichier source `.drawio` intermédiaire est supprimé après l'export puisque le fichier exporté contient le diagramme complet.

## Référence XML

La compétence référence le guide de génération XML partagé (routage des arêtes, conteneurs, calques, balises, métadonnées, mode sombre, etc.) depuis GitHub lors de l'exécution :
[`shared/xml-reference.md`](../shared/xml-reference.md)

C'est la source de vérité unique pour toutes les invites draw.io MCP du dépôt. Aucun fichier supplémentaire n'est nécessaire lors de l'installation.

## Pourquoi XML uniquement ?

Un fichier `.drawio` n'est que du XML mxGraphModel. Les formats Mermaid et CSV nécessitent la conversion côté serveur de draw.io — ils ne peuvent pas être sauvegardés comme fichiers natifs. Claude génère du XML directement pour tous les types de diagrammes, ce qui signifie :

- Aucune dépendance serveur
- Aucune étape de conversion
- Les fichiers sont immédiatement modifiables dans draw.io
