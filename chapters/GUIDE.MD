# LOG8430 – Final · Méthodologies, Pièges, Décisions Rapides

## 1. SOLID – Principes de conception

### Méthodologies
Pour chaque classe/interface, pose-toi la question **« qui change et pourquoi ? »**. Si plus d'une raison de changer → SRP. Si tu modifies du code existant pour ajouter une fonctionnalité → OCP cassé (utilise héritage/interfaces). Si une sous-classe override pour « ne rien faire » → LSP violé. Si une classe implémente une méthode vide d'une interface → ISP violé. Si un module métier `import`e une classe concrète de bas niveau → DIP violé (injecte une abstraction).

### Pièges
- **ISP ≠ SRP** : ISP cible les *interfaces* (point de vue client), SRP cible les *classes* (cohésion interne).
- LSP ne se résume pas à « hériter sans erreur compilateur » : il faut que le **comportement** reste substituable (Autruche/Oiseau, Carré/Rectangle).
- DIP ≠ Dependency Injection. DIP = principe (dépendre d'abstractions), DI = technique d'implémentation.
- OCP ne veut pas dire « jamais toucher au code », mais « ne pas modifier les modules **stables et validés** ».

### Décisions rapides
- « Plusieurs interfaces simples > une grosse interface » → **ISP** (Q2.1 type).
- « Une seule raison de changer » → **SRP**.
- « Dépendre des abstractions » → **DIP**.
- « Sous-type substituable » → **LSP**.
- « Étendre sans modifier » → **OCP**.

### Tableau comparatif

| Principe | Cible | Mot-clé QCM | Violation typique |
|---|---|---|---|
| SRP | Classe | Une raison de changer | God Class |
| OCP | Module | Extension sans modif | `if/else` sur types |
| LSP | Hiérarchie | Substituabilité | Override → exception |
| ISP | Interface | Client-spécifique | Méthodes inutilisées |
| DIP | Dépendance | Abstraction | `new ConcreteClass()` dans logique métier |

---

## 2. Styles Architecturaux

### Méthodologies
1. Identifier la **contrainte dominante** : centralisation ? scalabilité ? découplage ? temps réel ?
2. Classer en **monolithique / modulaire / distribué**.
3. Si distribué : choisir entre centralisé (Client-Server, Primary-Secondary, Broker), décentralisé (P2P), réactif (EDA), ou orienté service (SOA).
4. Justifier en citant **2 avantages concrets** + **1 désavantage assumé**.

### Pièges
- L'examen 2023 interdit explicitement « modulaire / distribué / multitiered » comme réponse → il faut nommer un **style précis** (P2P, EDA, etc.).
- Confondre **Broker** et **SOA** : Broker = intermédiaire de routage, SOA = exposition de services.
- Pipe-Filter ≠ MVC : Pipe-Filter est unidirectionnel et non interactif.
- Blackboard a un **contrôleur** (souvent oublié), ce n'est pas juste un tableau partagé.

### Décisions rapides
- **Partage de fichiers sans serveur central, scalable** → **P2P** (Q4.1 type, ex : BitTorrent).
- **Capteurs IoT temps réel, découplage producteur/consommateur** → **Event-Driven (EDA)**.
- **Calcul parallèle big data** → **Primary-Secondary** (MapReduce).
- **Intégration de systèmes hétérogènes via registre de services** → **Broker** ou **SOA**.
- **Système legacy critique, sécurité maximale, équipe restreinte** → **Mainframe**.

### Tableau comparatif

| Style | Catégorie | Couplage | Point unique de défaillance | Cas typique |
|---|---|---|---|---|
| Mainframe | Monolithique | N/A | Tout le système | Banque legacy |
| Pipe-Filter | Modulaire | Faible | Non | Compilateur, pipe Unix |
| MVC | Modulaire | Moyen | Non | Web e-commerce |
| Blackboard | Modulaire | Moyen | Contrôleur | Reconnaissance vocale |
| Client-Server | Distribué | Fort | Serveur | App bancaire |
| Primary-Secondary | Distribué | Fort | Primary | MapReduce |
| **P2P** | Distribué | Faible | **Aucun** | **BitTorrent, Blockchain** |
| Broker | Distribué | Faible | Broker | API Gateway, CORBA |
| SOA | Distribué | Faible | Registre | Microservices, e-commerce |
| EDA | Distribué | Très faible | Bus | IoT, notifications |

---

## 3. Cadriciels, Plugiciels & Écosystèmes

### Méthodologies
Pour distinguer framework vs plugin vs librairie, pose-toi 2 questions :
1. **Qui appelle qui ?** Si le code te rappelle → framework (IoC). Si tu l'appelles → librairie. Si le système hôte fonctionne sans → plugin.
2. **Le système peut-il tourner sans ce composant ?** Oui → plugin. Non → framework.

### Pièges
- Une librairie n'est **pas** un framework (pas d'IoC).
- Plugin = SRP (mission unique), pas IoC.
- Frozen Spots = parties immuables, Hot Spots = points d'extension (pas l'inverse).
- AngularJS et Django sont des **frameworks**, pas des écosystèmes.
- Q3 examen 2023 demande **fonctionnalité + flux de contrôle** : insister sur l'IoC (Hollywood Principle).

### Décisions rapides
- « Le système m'appelle » → **Framework**.
- « Ajout sans modification du noyau » → **Plugin** (architecture microkernel).
- « Mainteneur change l'API → milliers d'apps cassent » → problème de **breaking changes** dans un écosystème.

### Tableau comparatif

| Aspect | Framework | Plugin | Librairie |
|---|---|---|---|
| Flux de contrôle | **IoC** (cadre appelle) | Réagit à l'hôte | **Tu appelles** |
| Principe roi | OCP / DIP | **SRP** | Aucun spécifique |
| Indépendance | App ne tourne pas sans | Hôte tourne sans | Aucune |
| Extension | Hot Spots | Microkernel | Wrappers |
| Exemples | Django, Angular | AdBlock, Eclipse | Lodash, NumPy |

---

## 4. Big Data & NoSQL

### Méthodologies
1. Vérifier les **3V** : si au moins un dépasse les capacités SGBDR → Big Data.
2. Identifier la **forme** des données : clé simple ? document hétérogène ? colonnes massives ? relations complexes ?
3. Appliquer **CAP** : choisir 2 des 3 (souvent AP en NoSQL).
4. Si cohérence forte requise → **ACID** (SQL). Si haute dispo + scalabilité → **BASE** (NoSQL).

### Pièges
- **CAP : P ne se sacrifie pas** dans un système distribué (Q2.6 type) — si tu sacrifies P, ce n'est plus distribué.
- BASE ≠ ACID : BASE accepte la **consistance éventuelle**.
- MapReduce : l'input est **statique** (Q2.3 type — la phrase « input dynamic » est fausse).
- Document store ≠ relationnel : pas de JOIN côté serveur.
- « Reflète un changement immédiatement » → **ACID** (cohérence forte), pas BASE.

### Décisions rapides
- **Blog avec attributs variables, recherche texte/tags** (Q5 type) → **Document Store (MongoDB)**.
- **Sessions, paniers, cache** → **Clé-Valeur (Redis)**.
- **Logs massifs, séries temporelles** → **Wide-Column (Cassandra)**.
- **Réseau social, recommandations** → **Graphe (Neo4j)**.
- **Streaming d'événements** → **Kafka** (Q2.4 type).

### Tableau comparatif

| Modèle NoSQL | Structure | Cas d'usage | Techno phare |
|---|---|---|---|
| Clé-Valeur | Clé → valeur opaque | Cache, session | Redis, DynamoDB |
| **Document** | JSON/BSON imbriqué | **Blog, profils** | **MongoDB** |
| Wide-Column | Colonnes-familles | Logs, time-series | Cassandra, HBase |
| Graphe | Nœuds + arcs | Réseaux, fraude | Neo4j |

| Critère | SQL | NoSQL |
|---|---|---|
| Schéma | Rigide | Flexible |
| Scaling | Vertical (UP) | Horizontal (OUT) |
| Cohérence | ACID | BASE |
| JOIN | Oui | Non (en général) |

---

## 5. SOA & Mécanismes de Communication

### Méthodologies
1. Latence ? Si **minimale + appels directs** → RPC/gRPC.
2. Sécurité entreprise + transactions ? → **SOAP** (WS-Security).
3. Web public, scalable, cache ? → **REST**.
4. Frontend mobile flexible, sur-fetch à éviter ? → **GraphQL**.
5. Toujours préciser : **stub**, **interface**, **SLA**, **découvrabilité (UDDI)**.

### Pièges
- **GraphQL ≠ RPC** : GraphQL est une *query language*, RPC = exécution distante (Q2.8 type).
- « SOAP = XML standardisé » → **vrai** (réponse correcte Q2.8).
- « REST URI uniques » → vrai, pas partagés (Q2.8).
- REST n'a **pas de contrat formel** standard (vs WSDL/SOAP).
- gRPC = HTTP/2 + Protobuf, pas REST.

### Décisions rapides
- **Télémédecine, appels directs synchrones, faible latence** (Q6.1 type) → **RPC** (ou gRPC) — appels de méthode directs, performance maximale.
- Web public + cache + scaling → **REST**.
- Banque, contrats stricts, sécurité → **SOAP**.
- Mobile, sur-fetch problématique → **GraphQL**.

### Tableau comparatif

| Protocole | Transport | Format | Forces | Faiblesses |
|---|---|---|---|---|
| RPC | TCP | Binaire | **Direct, rapide** | Couplage fort |
| SOAP | HTTP/SMTP | XML | Sécurité, contrats (WSDL) | Verbeux, lent |
| REST | HTTP | JSON | Scalable, cache, simple | Pas de contrat formel |
| GraphQL | HTTP | JSON | Client choisit, 1 endpoint | Cache complexe |
| gRPC | HTTP/2 | Protobuf | Streaming, ultra-rapide | Pas browser natif |

| Composition | Orchestration | Chorégraphie |
|---|---|---|
| Contrôle | Centralisé | Décentralisé |
| Outil | Camunda, Step Functions | Kafka, EventBridge |

---

## 6. EDA & Patrons de Concurrence / Event Handling

### Méthodologies
1. Choisir le patron de **synchronisation** selon contexte : Singleton → Double-Checked Locking ; appels récursifs → Thread-Safe Interface.
2. Pour le **modèle de concurrence** : Active Object (asynchrone), Monitor (synchrone), Half-Sync/Half-Async (mixte), Leader/Followers (thread pool).
3. Pour le **handling d'événements** : Reactor (sync, app fait l'I/O), Proactor (async, OS fait l'I/O), ACT (token de contexte), Acceptor-Connector (séparation connexion/traitement).

### Pièges
- **Reactor vs Proactor** : Reactor = l'app fait l'I/O après notification ; Proactor = l'OS fait l'I/O et notifie à la fin.
- ACT = « cookie » pour retrouver le contexte dans une réponse asynchrone.
- Acceptor-Connector = essentiel pour **P2P orienté connexion**.
- Leader/Followers > Half-Sync/Half-Async en perf (pas de file d'attente entre threads).
- Scoped Locking seul + récursion = **deadlock** garanti.

### Décisions rapides
- **App P2P de partage de fichiers** (Q4.2 type) → **Acceptor-Connector** : sépare connexion (chaque pair = client + serveur) du traitement, parfait pour P2P.
- Beaucoup de connexions simultanées asynchrones → **Proactor**.
- Quelques connexions, traitement immédiat → **Reactor**.
- Réponse différée à corréler → **ACT**.

### Tableau comparatif

| Patron handling | Sync/Async | Qui fait l'I/O | Cas typique |
|---|---|---|---|
| **Reactor** | Synchrone | **Application** | Serveur web simple |
| **Proactor** | Asynchrone | **OS** | Haut débit, IOCP Windows |
| **ACT** | Asynchrone | Service | Corrélation requête/réponse |
| **Acceptor-Connector** | N/A (init) | N/A | **P2P, serveurs orientés connexion** |

| Concurrence | Caractéristique unique |
|---|---|
| Active Object | Thread propre à l'objet (Proxy + Scheduler + Servant) |
| Monitor Object | 1 méthode à la fois (`wait`/`notify`) |
| Half-Sync/Half-Async | File entre couches |
| Leader/Followers | Promotion de leader, pas de file |

---

## 7. Anti-patrons (Architecturaux + Conception + Code Smells)

### Méthodologies
1. **Niveau** : système → architectural ; classes → conception ; méthode → code smell.
2. **Identifier le principe brisé** (SOLID) pour orienter le refactoring.
3. **Refactoring patterns** : Extract Class/Method, Move Method, Introduce Parameter Object, Replace Conditional with Polymorphism, Hide Delegate.

### Pièges
- **Swiss Army Knife** = interface trop polyvalente (Q2.2 type, réponse correcte).
- **Jumble** = fusion horizontal/vertical (couches MVC + services), **pas** Swiss Army.
- **Cover Your Assets** = doc excessive, pas un anti-patron technique.
- **Stovepipe** = migration local→distribué ratée (typique de Q big data Q5).
- **Divergent Change** (1 classe, N changements) ≠ **Shotgun Surgery** (1 changement, N classes).

### Décisions rapides
- « Interface trop chargée, multi-usages » → **Swiss Army Knife**.
- « Vue qui contient du SQL direct » → **Jumble** (DIP cassé).
- « 12 fichiers à toucher pour 1 changement » → **Shotgun Surgery**.
- « Réinventer ce qui existe » → **Reinvent the Wheel** (NIH).
- « Système local migré sans abstraction » → **Stovepipe**.

### Tableau comparatif

| Anti-patron | Niveau | Principe brisé | Refactoring |
|---|---|---|---|
| Swiss Army Knife | Architectural | ISP | Diviser interfaces |
| Jumble | Architectural | DIP | Couches abstraites |
| Stovepipe | Architectural | SRP, DIP | Façade |
| Reinvent the Wheel | Architectural | OCP | Standards existants |
| Vendor Lock-in | Architectural | OCP, DIP | Abstractions multi-niveaux |
| Spaghetti Code | Conception | Modularité | Design patterns |
| God Object / Modularisation Insuffisante | Conception | SRP | Extract Class |
| Hiérarchie Brisée (Stack/Vector) | Conception | LSP | Délégation |
| Divergent Change | Code smell | SRP | Extract Class |
| Shotgun Surgery | Code smell | Cohésion | Move Method |
| Feature Envy | Code smell | Encapsulation | Move Method |
| Message Chain | Code smell | Loi de Demeter | Hide Delegate |

---

## 8. Blockchain

### Méthodologies
1. Vérifier les 4 propriétés : immuabilité, transparence, décentralisation, consensus.
2. Choisir le **consensus** : PoW (sécurité, énergie) vs PoS (efficacité) vs PBFT (privé).
3. Calcul du seuil byzantin : `n ≥ 3f + 1` pour tolérer `f` traîtres.
4. Identifier la chaîne : publique (Bitcoin/Ethereum) vs privée (Hyperledger).

### Pièges
- **Trilemme Blockchain** = Sécurité, Scalabilité, Décentralisation (Q2.7 type, réponse correcte).
- ≠ **CAP** (C, A, P) — qui est pour les BD distribuées.
- ≠ **ACID** (transactions BD).
- Attaque 51% : peut **réordonner / double-dépenser**, ne peut **pas** voler des coins existants.
- PoS vulnérabilité = **Nothing-at-stake**, pas 51%.

### Décisions rapides
- B2B contrôlé, haut TPS → **Hyperledger Fabric**.
- Smart contracts généraux → **Ethereum**.
- Monnaie pure → **Bitcoin**.
- Tolérer 1 traître → **minimum 4 nœuds**.

### Tableau comparatif

| Critère | Bitcoin | Ethereum | Hyperledger |
|---|---|---|---|
| Type | Public | Public | Privé |
| Consensus | PoW | PoS | PBFT/RAFT |
| Langage | Script | Solidity | Go/Java |
| TPS | ~7 | ~15-20 | >3500 |
| Usage | Monétaire | Général | B2B |

| Théorème | Trio | Domaine |
|---|---|---|
| **CAP** | Consistency, Availability, Partition | BD distribuées |
| **ACID** | Atomicity, Consistency, Isolation, Durability | Transactions SGBDR |
| **Trilemme Blockchain** | **Sécurité, Scalabilité, Décentralisation** | Blockchain |

---

## 9. Microservices

### Méthodologies
1. Identifier les **Bounded Contexts** (DDD) → 1 contexte = 1 service.
2. Appliquer **Two-Pizza Team** : équipe ≤ 12 personnes par service.
3. Pour migrer : **Strangler Application** — ne jamais réécrire en big-bang.
4. Choisir la **communication** : sync (HTTP/REST) pour requête-réponse, async (Kafka/RabbitMQ) pour découplage.

### Pièges
- **Strangling the Monolith** = remplacer **incrémentalement** (Q2.9 type, réponse correcte). Pas « composer », pas « construire ».
- Microservices ≠ SOA : Microservices = échelle app, BD par service ; SOA = échelle entreprise, BD partagée.
- **Kafka = streaming** (event-based), pas RabbitMQ (Q2.4 type).
- **RabbitMQ = MQ asynchrone**, pas streaming.
- **Nanoservices** = anti-patron (More the Merrier).
- Adopter sans CI/CD ni tests = **Trying to fly before walking**.

### Décisions rapides
- Goulot I/O sur S3, latence inter-service → **revenir au monolithe** (cas Amazon Prime Video).
- Échec d'un service ne doit pas tout casser → **Concevoir pour l'échec** + circuit breaker.
- Pile technologique partagée imposée → mauvaise foi (gouvernance décentralisée).

### Tableau comparatif

| Aspect | Monolithe | SOA | Microservices |
|---|---|---|---|
| Portée | App | Entreprise | App |
| BD | Partagée | Partagée | **Une par service** |
| Communication | Intra-process | ESB, SOAP | HTTP/REST, Kafka |
| Déploiement | Tout d'un coup | Couplé | **Indépendant** |
| Gouvernance | Centralisée | Centralisée | **Décentralisée** |

| Communication | Mécanisme | Techno |
|---|---|---|
| Synchrone | Req-rep | REST, gRPC |
| Async (MQ) | File | RabbitMQ |
| **Streaming** | **Append-only log** | **Kafka** |
| Pub-Sub | 1-à-N | Redis, SNS |

---

## 10. AOP – Programmation Orientée Aspects

### Méthodologies
1. Identifier les **CCC** (cross-cutting concerns) : logging, sécurité, transactions, cache, perf.
2. Définir un **Pointcut** = expression qui sélectionne des Join Points.
3. Écrire l'**Advice** = code à exécuter (Before/After/Around).
4. Encapsuler dans un **Aspect**.
5. Le **Weaver** tisse au compile-time, load-time ou runtime.

### Pièges
- **Q2.10 type** : « construct that allows injection of CCC » + « pattern expression » → réponse **Aspect, Pointcut**.
- **Joinpoint ≠ Pointcut** : Joinpoint = point d'exécution unique (un appel précis) ; Pointcut = expression qui matche **plusieurs** joinpoints.
- **Advice ≠ Aspect** : Advice = code ; Aspect = module qui contient Pointcut + Advice.
- Un Aspect **ne s'instancie pas** explicitement (géré par le runtime).
- Un Aspect concret **ne peut pas être hérité**.

### Décisions rapides
- « Logging dispersé partout » → AOP avec Pointcut sur toutes les méthodes publiques (homogène).
- « Validation différente par méthode » → crosscutting **hétérogène**.
- « Transaction auto avant/après méthode service » → Advice **Around**.

### Tableau comparatif

| Élément AOP | Rôle | Analogie |
|---|---|---|
| **Join Point** | Point d'exécution | Adresse précise |
| **Pointcut** | Expression de sélection | Pattern d'adresses |
| **Advice** | Code à injecter | Action à faire |
| **Aspect** | Module (Pointcut + Advice) | Plan complet |
| **Weaving** | Tissage dans le code | Couture |

| Aspect vs Classe | Aspect | Classe |
|---|---|---|
| Instanciation | **Non** (runtime) | Oui |
| Privilèges | Peut accéder `private` (privileged) | Non |
| Héritage concret | **Non** | Oui |

---

## Synthèse des réponses QCM types (examen 2023)

| Q | Sujet | Réponse |
|---|---|---|
| 2.1 | SOLID, plusieurs interfaces simples | **ISP** |
| 2.2 | Interface trop complexe | **Swiss Army Knife** |
| 2.3 | Affirmation FAUSSE MapReduce | **« Input dynamic »** |
| 2.4 | Streaming event-based | **Kafka** |
| 2.5 | Refléter un changement immédiatement | **ACID** |
| 2.6 | CAP, garantie non-sacrifiable | **Partition tolerance** |
| 2.7 | Trilemme Blockchain | **Sécurité, Scalabilité, Décentralisation** |
| 2.8 | Affirmation correcte | **SOAP = XML standardisé** |
| 2.9 | Remplacement incrémental | **Strangling the monolith** |
| 2.10 | AOP, blanks | **Aspect, Pointcut** |