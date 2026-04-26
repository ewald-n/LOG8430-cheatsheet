# 📊 LOG8430 - AIDE-MÉMOIRE : BIG DATA & NOSQL

## I. DÉFINITIONS ET CARACTÉRISTIQUES (LES 3V)

**Déf :** Un système est considéré "Big Data" s'il répond à au moins l'un des trois V à une échelle où les bases de données traditionnelles (SGBDR) échouent.

- **Volume :** Quantité massive de données (Téraoctets, Pétaoctets, Exaoctets).
- **Vélocité :** Vitesse de génération, de traitement et d'analyse (temps réel, flux de capteurs, marchés financiers).
- **Variété :** Diversité des types de données :
  - **Structurées :** BD relationnelles classiques.
  - **Semi-structurées :** Fichiers JSON, XML, logs.
  - **Non-structurées :** Texte libre, vidéo, images, audio.

---

## II. L'ÉCOSYSTÈME NOSQL (NOT ONLY SQL)

**Déf :** Systèmes de gestion de bases de données distribuées qui n'exposent ni interface SQL standard, ni interface normalisée.

### Caractéristiques Fondamentales

- **Scaling Out (Horizontal) :** Au lieu d'augmenter la puissance d'un serveur (Scaling Up), on distribue la charge sur de multiples serveurs bon marché.
- **Schéma Flexible :** Sans schéma (schemaless) ou avec schéma flexible pour gérer des données hétérogènes.
- **API Simples :** Utilisation d'API propres à chaque technologie (Get, Put, Delete) au lieu d'un langage standardisé.

### Théorème CAP (Le Compromis Inévitable)

Dans un système distribué, on ne peut garantir que 2 des 3 propriétés suivantes simultanément :

1. **Consistance (C) :** Tous les nœuds voient la même donnée au même moment.
2. **Disponibilité (A) :** Chaque requête reçoit une réponse (succès ou échec).
3. **Tolérance au partitionnement (P) :** Le système continue de fonctionner malgré la perte de messages ou d'un nœud.

> **Note :** La plupart des systèmes NoSQL choisissent **AP** (Disponibilité et Partitionnement) et acceptent la **Consistance Éventuelle**.

---

## III. LES 4 MODÈLES DE DONNÉES NOSQL

### 1. Clé-Valeur (Key-Value)

- **Déf :** Le modèle le plus simple. Une clé unique pointe vers une valeur (opaque pour la BD).
- **Propriétés :** Très efficace pour les applications simples ; stockage possible en mémoire vive pour une vitesse maximale.
- **Exemple :** Sessions utilisateurs, paniers d'achat, caches.
- **Technologies :** Redis, Riak, Amazon DynamoDB.

### 2. Document (Document Store)

- **Déf :** Stocke les données sous forme de documents (fichiers) encodés (JSON, XML, BSON).
- **Propriétés :** Les documents peuvent être de tailles et complexités diverses. Les données liées sont souvent imbriquées.
- **Exemple :** Profils utilisateurs complexes, catalogues de produits avec attributs variables.
- **Technologies :** MongoDB, CouchDB.

### 3. Colonnes (Wide-Column / Column-Family)

- **Déf :** Les données sont stockées par colonnes plutôt que par lignes.
- **Propriétés :** Permet de stocker des milliards de lignes avec des millions de colonnes. Très performant pour les agrégations de données massives.
- **Exemple :** Historiques de navigation, logs d'événements, séries temporelles.
- **Technologies :** Apache Cassandra, HBase.

### 4. Graphe (Graph Database)

- **Déf :** Utilise des structures de graphes avec des nœuds (entités) et des arcs (relations).
- **Propriétés :** Optimisé pour traverser les relations complexes. Les propriétés sont stockées sur les nœuds et les arcs.
- **Exemple :** Réseaux sociaux (amis de mes amis), systèmes de recommandation, détection de fraude.
- **Technologies :** Neo4j, InfiniteGraph.

---

## IV. ANALYSE ET PIPELINE DE DONNÉES

### Les Étapes de l'Analyse Big Data

1. **Acquisition :** Collecte depuis des sources variées (logs, réseaux sociaux, capteurs).
2. **Extraction & Nettoyage :** Transformer la donnée brute en format exploitable.
3. **Analyse & Modélisation :** Découvrir des patrons, faire des prédictions (Data Mining).
4. **Interprétation :** Visualisation et aide à la décision.

### Types d'Analyse

- **Analyse de Contenu :** Traitement de texte (NLP) pour identifier des thèmes ou sentiments.
- **Analyse de Graphe :** Mesurer la centralité, l'influence ou détecter des communautés dans un réseau.

---

## V. COMPARAISON RÉCAPITULATIVE : SQL VS NOSQL

| Caractéristique | **Bases Relationnelles (SQL)** | **Bases NoSQL** |
| :--- | :--- | :--- |
| **Structure** | Tableaux rigides, colonnes fixes. | Schéma flexible (Document, Graphe, etc.). |
| **Scaling** | Vertical (Scaling UP - Meilleur serveur). | Horizontal (Scaling OUT - Plus de serveurs). |
| **Normalisation** | Forte (évite la duplication). | Dénormalisation (on favorise la lecture rapide). |
| **Complexité** | Requêtes complexes avec JOIN (SQL). | API simples, JOIN souvent impossibles côté serveur. |
| **Consistance** | ACID (Atomique, Cohérent, Isolé, Durable). | BASE (Basic Availability, Soft state, Eventual consistency). |

> **Astuce Examen :** Si on te demande de migrer une application locale vers une version distribuée, attention à l'anti-patron **Stovepipe System** (vu au chapitre précédent) si tu gardes des accès fichiers locaux au lieu d'utiliser une base NoSQL distribuée !