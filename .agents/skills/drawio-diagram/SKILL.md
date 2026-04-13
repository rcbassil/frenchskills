---
name: drawio
description: Toujours utiliser quand l'utilisateur demande de créer, générer, dessiner ou concevoir un diagramme, organigramme, diagramme d'architecture, diagramme ER, diagramme de séquence, diagramme de classes, diagramme réseau, maquette, wireframe ou esquisse d'interface, ou mentionne draw.io, drawio, drawoi, des fichiers .drawio, ou l'export de diagrammes en PNG/SVG/PDF.
---

# Compétence Diagramme Draw.io

Générez des diagrammes draw.io sous forme de fichiers `.drawio` natifs. Exportation optionnelle en PNG, SVG ou PDF avec le XML du diagramme intégré (le fichier exporté reste ainsi modifiable dans draw.io).

## Comment créer un diagramme

1. **Générer le XML draw.io** au format mxGraphModel pour le diagramme demandé
2. **Écrire le XML** dans un fichier `.drawio` dans le répertoire de travail courant via l'outil Write
3. **Post-traitement du routage des arêtes** (optionnel) : Si `npx @drawio/postprocess` est disponible, l'exécuter sur le fichier `.drawio` pour optimiser le routage des arêtes (simplifier les points de passage, corriger les collisions arête-sommet, redresser les angles d'approche). Ignorer silencieusement si non disponible — ne pas l'installer ni en informer l'utilisateur
4. **Si l'utilisateur demande un format d'export** (png, svg, pdf), localiser la CLI draw.io (voir ci-dessous), exporter avec `--embed-diagram`, puis supprimer le fichier source `.drawio`. Si la CLI est introuvable, conserver le fichier `.drawio` et indiquer à l'utilisateur qu'il peut installer l'application draw.io pour activer l'export, ou ouvrir le fichier `.drawio` directement
5. **Ouvrir le résultat** — le fichier exporté si exporté, ou le fichier `.drawio` sinon. Si la commande d'ouverture échoue, afficher le chemin du fichier pour que l'utilisateur puisse l'ouvrir manuellement

## Choisir le format de sortie

Vérifier la préférence de format dans la demande de l'utilisateur. Exemples :

- `/drawio créer un organigramme` → `organigramme.drawio`
- `/drawio png flowchart de connexion` → `login-flow.drawio.png`
- `/drawio svg : diagramme ER` → `er-diagram.drawio.svg`
- `/drawio pdf vue d'ensemble architecture` → `architecture-overview.drawio.pdf`

Si aucun format n'est mentionné, écrire simplement le fichier `.drawio` et l'ouvrir dans draw.io. L'utilisateur peut toujours demander un export ultérieurement.

### Formats d'export pris en charge

| Format | XML intégré | Notes |
|--------|-------------|-------|
| `png` | Oui (`-e`) | Lisible partout, modifiable dans draw.io |
| `svg` | Oui (`-e`) | Vectoriel, modifiable dans draw.io |
| `pdf` | Oui (`-e`) | Imprimable, modifiable dans draw.io |
| `jpg` | Non | Avec perte, pas de support XML intégré |

PNG, SVG et PDF supportent tous `--embed-diagram` — le fichier exporté contient le XML complet du diagramme, permettant de récupérer le diagramme modifiable en l'ouvrant dans draw.io.

## CLI draw.io

L'application draw.io inclut une interface en ligne de commande pour l'export.

### Localiser la CLI

D'abord détecter l'environnement, puis localiser la CLI en conséquence :

#### WSL2 (Sous-système Windows pour Linux)

WSL2 est détecté quand `/proc/version` contient `microsoft` ou `WSL` :

```bash
grep -qi microsoft /proc/version 2>/dev/null && echo "WSL2"
```

Sous WSL2, utiliser l'exécutable draw.io Desktop Windows via `/mnt/c/...` :

```bash
DRAWIO_CMD=`/mnt/c/Program Files/draw.io/draw.io.exe`
```

Les guillemets inverses sont nécessaires pour gérer l'espace dans `Program Files` en bash.

Si draw.io est installé dans un emplacement non standard, vérifier les alternatives courantes :

```bash
# Chemin d'installation par défaut
`/mnt/c/Program Files/draw.io/draw.io.exe`

# Installation par utilisateur (si ce qui précède n'existe pas)
`/mnt/c/Users/$WIN_USER/AppData/Local/Programs/draw.io/draw.io.exe`
```

#### macOS

```bash
/Applications/draw.io.app/Contents/MacOS/draw.io
```

#### Linux (natif)

```bash
drawio   # généralement dans le PATH via snap/apt/flatpak
```

#### Windows (natif, hors WSL2)

```
"C:\Program Files\draw.io\draw.io.exe"
```

Utiliser `which drawio` (ou `where drawio` sous Windows) pour vérifier s'il est dans le PATH avant de revenir au chemin spécifique à la plateforme.

### Commande d'export

```bash
drawio -x -f <format> -e -b 10 -o <sortie> <entrée.drawio>
```

**Exemple WSL2 :**

```bash
`/mnt/c/Program Files/draw.io/draw.io.exe` -x -f png -e -b 10 -o diagram.drawio.png diagram.drawio
```

Options principales :
- `-x` / `--export` : mode export
- `-f` / `--format` : format de sortie (png, svg, pdf, jpg)
- `-e` / `--embed-diagram` : intégrer le XML du diagramme dans la sortie (PNG, SVG, PDF uniquement)
- `-o` / `--output` : chemin du fichier de sortie
- `-b` / `--border` : largeur de la bordure autour du diagramme (par défaut : 0)
- `-t` / `--transparent` : fond transparent (PNG uniquement)
- `-s` / `--scale` : mettre le diagramme à l'échelle
- `--width` / `--height` : adapter aux dimensions spécifiées (conserve le ratio)
- `-a` / `--all-pages` : exporter toutes les pages (PDF uniquement)
- `-p` / `--page-index` : sélectionner une page spécifique (base 1)

### Ouvrir le résultat

| Environnement | Commande |
|---------------|---------|
| macOS | `open <fichier>` |
| Linux (natif) | `xdg-open <fichier>` |
| WSL2 | `cmd.exe /c start "" "$(wslpath -w <fichier>)"` |
| Windows | `start <fichier>` |

**Notes WSL2 :**
- `wslpath -w <fichier>` convertit un chemin WSL2 (ex. `/home/user/diagram.drawio`) en chemin Windows (ex. `C:\Users\...`). Nécessaire car `cmd.exe` ne peut pas résoudre les chemins de type `/mnt/c/...`.
- La chaîne vide `""` après `start` est requise pour éviter que `start` n'interprète le nom de fichier comme un titre de fenêtre.

**Exemple WSL2 :**

```bash
cmd.exe /c start "" "$(wslpath -w diagram.drawio)"
```

## Nommage des fichiers

- Utiliser un nom de fichier descriptif basé sur le contenu du diagramme (ex. `login-flow`, `database-schema`)
- Utiliser des minuscules avec des tirets pour les noms composés
- Pour l'export, utiliser des doubles extensions : `nom.drawio.png`, `nom.drawio.svg`, `nom.drawio.pdf` — cela indique que le fichier contient du XML de diagramme intégré
- Après un export réussi, supprimer le fichier `.drawio` intermédiaire — le fichier exporté contient le diagramme complet

## Format XML

Un fichier `.drawio` est du XML mxGraphModel natif. Toujours générer le XML directement — les formats Mermaid et CSV nécessitent une conversion côté serveur et ne peuvent pas être sauvegardés comme fichiers natifs.

### Structure de base

Chaque diagramme doit avoir cette structure :

```xml
<mxGraphModel adaptiveColors="auto">
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>
    <!-- Les cellules du diagramme vont ici avec parent="1" -->
  </root>
</mxGraphModel>
```

- La cellule `id="0"` est le calque racine
- La cellule `id="1"` est le calque parent par défaut
- Tous les éléments du diagramme utilisent `parent="1"` sauf en cas de calques multiples

## Référence XML

Pour la référence XML draw.io complète incluant les styles courants, le routage des arêtes, les conteneurs, les calques, les balises, les métadonnées, les couleurs du mode sombre et les règles de conformité XML, récupérer et suivre les instructions à :
https://raw.githubusercontent.com/jgraph/drawio-mcp/main/shared/xml-reference.md

## Dépannage

| Problème | Cause | Solution |
|----------|-------|----------|
| CLI draw.io introuvable | Application desktop non installée ou absente du PATH | Conserver le fichier `.drawio` et indiquer à l'utilisateur d'installer l'application draw.io, ou d'ouvrir le fichier manuellement |
| L'export produit un fichier vide ou corrompu | XML invalide (ex. doubles tirets dans les commentaires, caractères spéciaux non échappés) | Valider la conformité XML avant l'écriture ; voir la section conformité XML ci-dessous |
| Le diagramme s'ouvre mais semble vide | Cellules racines `id="0"` et `id="1"` manquantes | S'assurer que la structure mxGraphModel de base est complète |
| Les arêtes ne s'affichent pas | La cellule mxCell d'arête est auto-fermante (sans élément mxGeometry enfant) | Chaque arête doit avoir `<mxGeometry relative="1" as="geometry" />` comme élément enfant |
| Le fichier ne s'ouvre pas après l'export | Chemin de fichier incorrect ou association de fichier manquante | Afficher le chemin absolu du fichier pour que l'utilisateur puisse l'ouvrir manuellement |

## CRITIQUE : Conformité XML

- **NE JAMAIS inclure de commentaires XML (`<!-- -->`) dans la sortie.** Les commentaires XML sont strictement interdits — ils gaspillent des tokens, peuvent causer des erreurs d'analyse et n'ont aucune utilité dans le XML de diagramme.
- Échapper les caractères spéciaux dans les valeurs d'attributs : `&amp;`, `&lt;`, `&gt;`, `&quot;`
- Toujours utiliser des valeurs `id` uniques pour chaque `mxCell`
