# Exemples d'utilisation — Compétence Draw.io

Ce fichier présente des exemples concrets d'utilisation de la compétence Draw.io dans Claude Code, couvrant les types de diagrammes les plus courants et les différents formats d'export.

---

## 1. Organigramme (Flowchart)

**Cas d'usage :** Visualiser le flux de connexion d'un utilisateur.

**Commande :**
```
/drawio créer un organigramme pour le processus de connexion utilisateur
```

**Fichier généré :** `login-flow.drawio`

**Ce que Claude va faire :**
- Créer les étapes (Début, Saisie identifiants, Vérification, Accès accordé/refusé)
- Relier les étapes avec des flèches conditionnelles (Oui/Non)
- Ouvrir le fichier dans draw.io

---

## 2. Diagramme de séquence

**Cas d'usage :** Illustrer les échanges entre un client, une API et une base de données lors d'une authentification.

**Commande :**
```
/drawio diagramme de séquence pour l'authentification API avec JWT
```

**Fichier généré :** `api-auth-sequence.drawio`

**Ce que Claude va faire :**
- Créer les acteurs : Client, Serveur API, Base de données
- Représenter les messages échangés dans l'ordre chronologique (requête, validation, token JWT, réponse)
- Utiliser des flèches de retour pour les réponses

---

## 3. Diagramme ER (Entité-Relation)

**Cas d'usage :** Modéliser le schéma d'une base de données e-commerce.

**Commande :**
```
/drawio diagramme ER pour une base de données e-commerce avec clients, commandes et produits
```

**Fichier généré :** `ecommerce-er.drawio`

**Ce que Claude va faire :**
- Créer les entités : Client, Commande, Produit, LigneCommande
- Définir les attributs de chaque entité (id, nom, email, prix, etc.)
- Relier les entités avec les cardinalités (1-N, N-N)

---

## 4. Diagramme d'architecture système

**Cas d'usage :** Représenter l'architecture d'une application web en microservices.

**Commande :**
```
/drawio architecture microservices pour une application de gestion de tâches avec frontend, API gateway, services et base de données
```

**Fichier généré :** `microservices-architecture.drawio`

**Ce que Claude va faire :**
- Représenter les couches : Frontend, API Gateway, Services métiers, Base de données
- Grouper les composants dans des conteneurs (ex. Kubernetes cluster)
- Indiquer les protocoles de communication (REST, gRPC, etc.)

---

## 5. Diagramme de classes

**Cas d'usage :** Modéliser les classes d'un projet orienté objet.

**Commande :**
```
/drawio diagramme de classes pour les modèles dans src/models/
```

**Fichier généré :** `class-diagram.drawio`

**Ce que Claude va faire :**
- Créer une classe par modèle avec ses attributs et méthodes
- Représenter les relations d'héritage, composition et association
- Respecter la notation UML standard

---

## 6. Diagramme réseau

**Cas d'usage :** Schématiser l'infrastructure réseau d'une entreprise.

**Commande :**
```
/drawio diagramme réseau pour une infrastructure avec pare-feu, DMZ, serveurs web et base de données interne
```

**Fichier généré :** `network-diagram.drawio`

**Ce que Claude va faire :**
- Représenter les zones réseau (Internet, DMZ, LAN interne)
- Placer les équipements (routeur, pare-feu, switches, serveurs)
- Indiquer les flux autorisés entre zones

---

## 7. Wireframe / Maquette d'interface

**Cas d'usage :** Esquisser rapidement une page de tableau de bord.

**Commande :**
```
/drawio wireframe d'un tableau de bord avec barre latérale, graphiques et tableau de données
```

**Fichier généré :** `dashboard-wireframe.drawio`

**Ce que Claude va faire :**
- Créer une mise en page avec navigation latérale
- Ajouter des zones de contenu pour les graphiques et tableaux
- Utiliser des formes simples et des annotations pour indiquer les interactions

---

## 8. Export en PNG

**Cas d'usage :** Générer une image prête à être intégrée dans une présentation ou un document.

**Commande :**
```
/drawio png organigramme du processus d'onboarding employé
```

**Fichier généré :** `onboarding-flow.drawio.png`

**Ce que Claude va faire :**
- Créer le diagramme en XML draw.io
- Exporter via la CLI draw.io avec XML intégré (`-e`)
- Supprimer le fichier `.drawio` intermédiaire
- Ouvrir le PNG (réouvrable dans draw.io pour modification)

---

## 9. Export en SVG

**Cas d'usage :** Produire un diagramme vectoriel pour un site web ou une documentation technique.

**Commande :**
```
/drawio svg diagramme d'architecture pour la documentation du projet
```

**Fichier généré :** `architecture.drawio.svg`

**Ce que Claude va faire :**
- Générer le XML du diagramme
- Exporter en SVG avec le XML intégré
- Le fichier est utilisable dans un navigateur et reste modifiable dans draw.io

---

## 10. Export en PDF

**Cas d'usage :** Produire un livrable imprimable pour un client ou une réunion.

**Commande :**
```
/drawio pdf vue d'ensemble de l'architecture du système de paiement
```

**Fichier généré :** `payment-system-architecture.drawio.pdf`

**Ce que Claude va faire :**
- Créer le diagramme complet
- Exporter en PDF avec toutes les pages (`-a`) si nécessaire
- Le PDF contient le XML intégré pour une réédition future

---

## Récapitulatif des commandes

| Type de diagramme | Exemple de commande | Fichier de sortie |
|-------------------|--------------------|--------------------|
| Organigramme | `/drawio organigramme inscription utilisateur` | `user-signup-flow.drawio` |
| Séquence | `/drawio séquence paiement en ligne` | `online-payment-sequence.drawio` |
| ER / Base de données | `/drawio ER schéma blog` | `blog-er.drawio` |
| Architecture | `/drawio architecture application SaaS` | `saas-architecture.drawio` |
| Classes UML | `/drawio classes UML projet Python` | `python-class-diagram.drawio` |
| Réseau | `/drawio réseau infrastructure cloud` | `cloud-network.drawio` |
| Wireframe | `/drawio wireframe page de connexion` | `login-wireframe.drawio` |
| Export PNG | `/drawio png flux de validation commande` | `order-validation-flow.drawio.png` |
| Export SVG | `/drawio svg pipeline CI/CD` | `cicd-pipeline.drawio.svg` |
| Export PDF | `/drawio pdf architecture microservices` | `microservices-architecture.drawio.pdf` |

---

## Conseils

- **Soyez descriptif** : plus votre demande est précise, plus le diagramme sera détaillé et pertinent.
- **Mentionnez le format** si vous avez besoin d'un PNG, SVG ou PDF — sinon Claude produit un fichier `.drawio` natif.
- **Itérez facilement** : ouvrez le fichier `.drawio` dans draw.io pour ajuster manuellement, puis demandez à Claude d'exporter dans le format voulu.
- **Référencez votre code** : vous pouvez demander à Claude de générer un diagramme à partir de fichiers existants, ex. `/drawio diagramme de classes pour src/models/`.
