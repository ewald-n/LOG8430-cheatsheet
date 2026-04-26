# LOG8430E : Architectures de Microservices

## 1. Définitions et Fondamentaux
### 1.1 Qu'est-ce qu'un Microservice ?
* [cite_start]**Définition Académique :** Une version plus petite de la SOA (Service-Oriented Architecture) où chaque service est un processus unique avec une **seule responsabilité** (Principe Unix)[cite: 2187, 2188].
* [cite_start]**Two Pizza Team (Amazon) :** Une équipe de microservices doit être suffisamment petite pour être nourrie par deux pizzas (environ une douzaine de personnes).
* [cite_start]**Relation avec DevOps :** Technologie fondamentale pour DevOps grâce aux conteneurs; ils promeuvent l'automatisation, l'évolution et la livraison continues[cite: 2196, 2197].

### 1.2 SOA vs Microservices
| Caractéristique | Architecture SOA | Architecture Microservices |
| :--- | :--- | :--- |
| **Portée** | [cite_start]Échelle de l'entreprise [cite: 2202] | [cite_start]Échelle de l'application [cite: 2203] |
| **Réutilisation** | [cite_start]Partage de composants [cite: 2218] | [cite_start]Réutilisation du code [cite: 2219] |
| **Données** | [cite_start]Source principale unique (Synchrone) [cite: 2221] | [cite_start]Accès local/décentralisé par service [cite: 2222] |
| **Communication** | [cite_start]Moyens "lourds" (ESB, SOAP) [cite: 2547] | [cite_start]Moyens simples (HTTP, Message Broker) [cite: 2551] |
| **Gouvernance** | Centralisée | [cite_start]Décentralisée (Polyglotte) [cite: 2557, 2560] |

---

## 2. Le Monolithe : Avantages et Désavantages
### 2.1 Propriétés
* [cite_start]**Processus unique :** Un monolithe n'est pas un seul programme, mais un processus unique en exécution (peut être modulaire, mais pas distribué)[cite: 2237, 2238].
* [cite_start]**Architecture 3 couches :** Client, Serveur, Base de données[cite: 2227].

### 2.2 Analyse Critique
* [cite_start]**Avantages :** Équipe unique productive, facile à tester/déployer (fichiers WAR), supporté nativement par les IDE, mise à l'échelle horizontale simple via équilibreur de charge[cite: 2269, 2274, 2276].
* [cite_start]**Inconvénients (Loi de la croissance) :** * Surcharge des conteneurs (Tomcat) et IDE[cite: 2285].
    * [cite_start]**Frontières floues :** Modularité facile à briser involontairement[cite: 2284].
    * [cite_start]**Verrouillage (Vendor Lock-in) :** Engagement long terme envers une pile technologique (ex: tout Java/Tomcat)[cite: 2290, 2291].
    * [cite_start]**Déploiement rigide :** Un seul changement force le redéploiement de *tout* le système[cite: 2288].

---

## 3. Caractéristiques des Microservices (9 Principes)

1.  [cite_start]**Composantes via services :** Unités remplaçables et évolutives indépendamment[cite: 2455].
2.  **Produits et non projets :** Mentalité "Vous le construisez, vous l'exécutez" (Amazon). [cite_start]L'équipe est responsable du logiciel en production[cite: 2535, 2536].
3.  [cite_start]**Points de terminaison intelligents / Tuyaux stupides :** La logique réside chez l'expéditeur/récepteur (HTTP/REST), pas dans le réseau (contrairement aux ESB de la SOA)[cite: 2551, 2552].
4.  [cite_start]**Gouvernance décentralisée :** Liberté du choix de la pile technologique par service[cite: 2558, 2561].
5.  **Gestion décentralisée des données :** Un domaine complexe est divisé en domaines délimités (**Bounded Contexts** - DDD). [cite_start]Chaque service possède sa propre BD[cite: 2569, 2576].
6.  [cite_start]**Automatisation de l'infrastructure :** Investissement massif dans les pipelines CI/CD (Testing et Déploiement "ennuyeux")[cite: 2580, 2583].
7.  **Concevoir pour l'échec :** Monitoring technique et commercial impératif. [cite_start]Si un service échoue, il doit le faire gracieusement[cite: 2598, 2602].
8.  [cite_start]**Conception évolutive :** Possibilité de remplacer un composant sans affecter le système[cite: 2614].
9.  [cite_start]**Loi de Conway :** La structure du logiciel reflète la structure de communication de l'organisation[cite: 2468, 2486].

---

## 4. Stratégies de Migration et Conception
### 4.1 Patron Strangler Application (Étouffement)
* **Mécanisme :** Le monolithe reste le cœur initial. Les nouvelles fonctionnalités sont ajoutées comme microservices. [cite_start]On remplace progressivement les fonctions de base du monolithe par des microservices jusqu'à disparition complète du monolithe[cite: 2627, 2634, 2640].
* [cite_start]**Règle Shotgun Surgery :** Si deux services sont modifiés ensemble de façon répétée, ils doivent probablement être fusionnés[cite: 2636, 2639].

### 4.2 Processus d'Assemblage (Chris Richardson)
1.  [cite_start]**Entrée :** User stories, exigences non fonctionnelles (SLA), Wireframes[cite: 2736, 2738, 2739].
2.  [cite_start]**Processus :** Définir les opérations système → Définir les sous-domaines → Grouper les sous-domaines en services → Concevoir les collaborations[cite: 2768, 2769, 2771].
3.  [cite_start]**Résultat :** Schémas d'architecture, contrats d'API, modèles de Bounded Contexts[cite: 2790, 2791].

---

## 5. Communication et Systèmes Distribués
### [cite_start]5.1 Les 8 Fallacies (Illusions) de l'informatique distribuée [cite: 2955]
* [cite_start]Le réseau est fiable, la latence est nulle, la bande passante est infinie, le réseau est sécurisé, la topologie ne change pas, il y a un seul administrateur, le coût de transport est nul, le réseau est homogène[cite: 2947, 2954].

### 5.2 Modèles de Communication
| Modèle | Mécanisme | Technologies | Avantages / Inconvénients |
| :--- | :--- | :--- | :--- |
| **Synchrone (Bloquant)** | [cite_start]Requête-réponse en temps réel [cite: 2964, 3032] | [cite_start]HTTP/REST, gRPC, GraphQL [cite: 3034, 3037, 3038] | Simple, mais crée un couplage temporel. |
| **Asynchrone (MQ)** | [cite_start]File d'attente (Buffer) [cite: 2969, 2970] | RabbitMQ, ActiveMQ | [cite_start]Découplé, tolérant aux pannes; difficile à tracer[cite: 2979]. |
| **Streaming** | [cite_start]Journal en ajout uniquement (Append-only) [cite: 3003] | Apache Kafka | [cite_start]Très scalable, gère gros volumes[cite: 3005]. |
| **Pub-Sub** | [cite_start]Diffusion un-à-plusieurs via un canal [cite: 3010, 3022] | Redis Pub/Sub, SNS | [cite_start]Faible couplage; duplication possible[cite: 3023, 3025]. |

---

## 6. Focus Examen : Antipatrons d'Adoption
* [cite_start]**Magic Pixie Dust :** Croire que les microservices résoudront tous les problèmes sans changer la culture (DevOps)[cite: 2806, 2810].
* [cite_start]**Microservices as the Goal :** Adopter l'architecture pour la technologie plutôt que pour régler un problème d'affaires[cite: 2825, 2828].
* [cite_start]**Scattershot Adoption :** Adoption sans stratégie centrale, chaque équipe fait ses propres choix (manque de coordination)[cite: 2860, 2864].
* [cite_start]**Trying to fly before walking :** Adopter les microservices sans maîtriser le code propre, les tests automatisés et le CI/CD[cite: 2877, 2879].
* [cite_start]**More the Merrier :** Créer des services trop petits (**Nanoservices**), ce qui explose la complexité de communication[cite: 2903, 2905].
* [cite_start]**Red Flag Law :** Utiliser des microservices avec des processus lents (Cascade, tests manuels)[cite: 2919, 2928].

---

## 7. Étude de cas : Amazon Prime Video (Retour au Monolithe)
* [cite_start]**Contexte :** Passage d'une architecture microservices distribuée (Lambda + Step Functions) à un monolithe en 2023[cite: 3047, 3048].
* [cite_start]**Problème :** Goulot d'étranglement dû aux transferts de données excessifs vers S3, latence élevée et coûts d'I/O[cite: 3113, 3120].
* [cite_start]**Solution :** Regroupement de tous les composants (détecteurs, convertisseurs) dans un seul processus (Amazon ECS)[cite: 3125, 3130, 3159].
* **Leçon :** Il n'y a pas de modèle universel. [cite_start]L'architecture doit être réévaluée à chaque ordre de grandeur de croissance[cite: 3167].