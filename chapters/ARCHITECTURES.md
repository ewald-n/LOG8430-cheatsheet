# Styles Architecturaux

## Diagramme des Styles Architecturaux

### MONOLITHIQUE
- **Mainframe**

### MODULAIRE
- **Pipe-Filter**
- **MVC**
- **Blackboard**

### DISTRIBUÉ
- **Client-Server**
- **Primary-Secondary**
- **Peer-to-Peer**
- **Broker**
- **SOA**
- **Event-Driven**

---

# STYLES MONOLITHIQUES

## 1. Mainframe (Monolithique)

**Analogie :** Château Fort. Tout à l'intérieur (données, logique, murs). Si pierre tombe → château vulnérable.

**Définition :** Architecture centralisée où traitement, logique et données fusionnés sur 1 unité calcul.

### Avantages
- Conception simple
- Contrôle total données
- Performance élevée (pas latence comm)
- Sécurité max contre attaques externes

### Désavantages
- Évolutivité nulle (impossible agrandir 1 partie)
- Maintenance coûteuse (code entrelacé)
- Point unique défaillance

### Cas d'usage
- **Systèmes bancaires legacy :** Millions transactions/jour, haute sécurité, aucune dépendance réseau
- **Inventaire industriel massif :** Équipe restreinte, contrôle absolu, frais exécution min

---

# STYLES MODULAIRES

## 2. Pipe-Filter (Modulaire)

**Analogie :** Chaîne Montage. Chaque poste (filtre) transforme produit et passe au suivant par tapis roulant (tuyau).

**Définition :** Flux données unidirectionnel où chaque Filtre transforme données reçues et transmet au suivant via Tuyau.

### Avantages
- Développement parallèle (plusieurs dev simultanément)
- Réutilisabilité composants
- Facilité ajout filtres
- Modules remplaçables

### Désavantages
- Surcharge performance (traversée chaque filtre)
- Perte efficacité (formatage données entre modules)
- Non interactif

### Cas d'usage
- **Pipeline compilation :** Transformations indépendantes, composants réutilisables
- **Traitement logs Unix :** cat|grep|sort, flexibilité, tuyaux = synchronisateurs

---

## 3. MVC – Model-View-Controller (Modulaire)

**Analogie :** Restaurant. Client (Vue) commande → Serveur (Contrôleur) transmet → Cuisine (Modèle) prépare → Serveur ramène plat → Client mange.

**Définition :** Séparation logique métier (Model), interface utilisateur (View), orchestration (Controller).

### Composants
- **Model :** Données + logique métier, notifie changements
- **View :** Affichage, écoute Model
- **Controller :** Reçoit input utilisateur, modifie Model/View

### Avantages
- Développement parallèle (équipes séparées UI/logique)
- Multiples vues même modèle
- Facilité tests unitaires
- Maintenabilité accrue

### Désavantages
- Complexité accrue (3 couches à gérer)
- Surcharge petits projets
- Couplage View-Controller parfois fort

### Cas d'usage
- **Application web e-commerce :** Plusieurs interfaces même données, équipes séparées, évolution UI fréquente
- **App mobile multiplateforme :** Logique partagée, vues iOS/Android distinctes

---

## 4. Blackboard (Modulaire)

**Analogie :** Tableau Noir Classe. Plusieurs experts écrivent hypothèses → Contrôleur lit → Choisit expert suivant → Répète jusqu'à solution.

**Définition :** Résolution problèmes complexes sans solution déterministe. Sources connaissances (experts) collaborent via espace partagé (blackboard).

### Composants
- **Blackboard :** Mémoire partagée, état problème
- **Sources Connaissances :** Modules experts indépendants
- **Contrôleur :** Orchestrateur, sélectionne expert selon état

### Avantages
- Flexibilité (ajout/retrait experts facile)
- Tolérance pannes (1 expert échoue ≠ système plante)
- Expérimentation (tester stratégies différentes)

### Désavantages
- Difficile tester/déboguer (comportement émergent)
- Pas de garantie solution
- Synchronisation blackboard = bottleneck
- Complexité contrôleur

### Cas d'usage
- **Reconnaissance vocale :** Phonétique + syntaxe + sémantique collaborent, pas d'algo unique
- **Diagnostic médical :** Symptômes → experts spécialisés proposent hypothèses, incertitude élevée

---

# STYLES DISTRIBUÉS

## 5. Client-Server (Distribué)

**Analogie :** Restaurant Drive-In. Client commande (requête) → Serveur prépare → Serveur livre (réponse).

**Définition :** Architecture 2 entités : Client (initie requêtes) et Serveur (fournit services/ressources). Communication réseau.

### Avantages
- Centralisation données (gestion simplifiée)
- Contrôle accès sécurisé
- Maintenance serveur sans toucher clients
- Scalabilité verticale (améliorer serveur)

### Désavantages
- Serveur = point unique défaillance
- Latence réseau
- Scalabilité limitée (serveur surchargé si trop clients)
- Coûts infrastructure serveur

### Cas d'usage
- **Application bancaire :** Sécurité centralisée, transactions cohérentes, clients légers
- **Serveur email :** Stockage centralisé, accès multi-appareils, gestion utilisateurs simplifiée

---

## 6. Primary-Secondary (Distribué)

**Analogie :** Chef Orchestre. Chef (Primary) distribue partitions → Musiciens (Secondary) jouent leur partie → Harmonie collective.

**Définition :** Primary décompose tâche et délègue aux Secondary (réplicas/workers). Coordination centralisée, exécution parallèle.

### Avantages
- Parallélisme (tâches simultanées)
- Tolérance pannes (si Secondary échoue, Primary réassigne)
- Scalabilité horizontale (ajout Secondary)
- Performance accrue

### Désavantages
- Primary = bottleneck
- Complexité synchronisation
- Surcharge communication Primary-Secondary
- Pas adapté si tâches interdépendantes

### Cas d'usage
- **Réplication base données :** Primary = écriture, Secondary = lecture, haute disponibilité
- **Calcul distribué :** Traitement big data, MapReduce, tâches indépendantes parallélisables

---

## 7. Peer-to-Peer / P2P (Distribué)

**Analogie :** Potluck Party. Chaque invité apporte plat (ressource) et mange chez autres (consomme). Pas d'hôte central. ⭐ **QCM ★**

**Définition :** Réseau décentralisé où chaque nœud (pair) = client ET serveur. Partage ressources direct sans autorité centrale.

### Avantages
- Scalabilité naturelle (+ pairs = + ressources)
- Résilience (pas de point unique défaillance)
- Coûts réduits (pas serveur central)
- Autonomie pairs

### Désavantages
- Sécurité complexe (pairs non fiables)
- Découverte pairs difficile
- Performance variable (dépend pairs disponibles)
- Synchronisation données ardue

### Cas d'usage
- **Partage fichiers :** BitTorrent, pas serveur central, scalabilité infinie
- **Blockchain :** Décentralisation, consensus distribué, résilience attaques

---

## 8. Broker (Distribué)

**Analogie :** Agent Immobilier. Acheteur cherche maison → Agent (Broker) trouve vendeurs → Met en contact → Transaction.

**Définition :** Intermédiaire coordonne communication entre composants distribués. Découverte services, routage requêtes, découplage client-serveur.

### Composants
- **Broker :** Registre services, routage
- **Client :** Demande service
- **Serveur :** Fournit service, s'enregistre au Broker

### Avantages
- Découplage fort (client ignore localisation serveur)
- Ajout/modif services dynamique
- Transparence localisation
- Load balancing possible

### Désavantages
- Broker = point unique défaillance
- Latence ajoutée (hop supplémentaire)
- Complexité gestion Broker
- Coût infrastructure Broker

### Cas d'usage
- **Middleware entreprise :** CORBA, intégration systèmes hétérogènes, découverte services
- **API Gateway :** Microservices, routage intelligent, authentification centralisée

---

## 9. SOA – Service-Oriented Architecture (Distribué)

**Analogie :** Centre Commercial. Chaque boutique (service) = spécialité. Client visite boutiques nécessaires. Indépendance totale boutiques.

**Définition :** Architecture où fonctionnalités exposées comme services indépendants, réutilisables, accessibles via réseau (SOAP/REST/RPC/GraphQL).

### Avantages
- Réutilisabilité services
- Interopérabilité (langages/plateformes différents)
- Scalabilité service par service
- Maintenance isolée
- Agilité métier

### Désavantages
- Complexité orchestration
- Latence réseau
- Gouvernance services difficile
- Coûts infrastructure
- Dépendances services = risque cascade pannes

### Cas d'usage
- **Plateforme e-commerce :** Services paiement, inventaire, expédition indépendants, réutilisables
- **Microservices modernes :** Déploiement indépendant, équipes autonomes, CI/CD

---

## 10. Event-Driven / EDA (Distribué)

**Analogie :** Système Alarme Incendie. Détecteur fumée (producteur) détecte → Alarme sonne (bus événements) → Pompiers réagissent (consommateurs). Découplage total.

**Définition :** Architecture réactive où composants communiquent via événements asynchrones. Producteurs émettent, consommateurs réagissent via bus d'événements.

### Composants
- **Producteur :** Émet événements
- **Bus Événements :** Message broker, ex: Kafka, RabbitMQ
- **Consommateur :** Écoute, réagit

### Avantages
- Découplage extrême (producteur ignore consommateurs)
- Scalabilité (ajout consommateurs facile)
- Réactivité temps réel
- Résilience (événements persistés)

### Désavantages
- Complexité débogage (flux asynchrone)
- Ordre événements difficile garantir
- Duplication événements possible
- Latence bus
- Gestion erreurs complexe

### Cas d'usage
- **IoT :** Capteurs émettent données → systèmes réagissent temps réel, scalabilité massive
- **Notifications utilisateur :** Action utilisateur → événement → emails/push/SMS, découplage services
