# LOG8430 — Questions et réponses extraites des diapositives

> Compilation des questions / réponses (et quiz) trouvées dans les diapositives du cours.
> Pour chaque question, le contexte (extrait pertinent) et la réponse (lorsque présente dans les diapositives) sont reproduits.

---

## 1. Cadriciels (02b.Cadriciels-H26)

### Q1 — Vrai ou Faux ?
**Question :** Les frameworks nécessitent que les programmes soient écrits pour utiliser leurs fonctionnalités, tandis que les plugins étendent les fonctionnalités sans modifier le programme central.

**Réponse (Vrai) :**
- Les Framework fournissent des fonctionnalités que les programmes doivent être écrits pour utiliser.
- Les plugins étendent les fonctionnalités d'un autre élément, sans nécessiter de modifications du programme central qu'ils augmentent.
- Tandis que les cadriciels se concentrent sur l'amélioration de l'expérience du développeur, les plugins visent davantage à optimiser l'expérience de l'utilisateur.

---

### Q2 — Choix multiple
**Question :** Quel est l'objectif principal d'un plugin par rapport à un cadriciel ?

- A. Améliorer l'expérience du développeur
- B. Étendre les fonctionnalités d'un programme sans le modifier
- C. Fournir une structure pour écrire un programme
- D. Faciliter la gestion des dépendances

**Réponse :** **B. Étendre les fonctionnalités d'un programme sans le modifier**
(Justification donnée dans la diapositive suivante : « Les plugins étendent les fonctionnalités d'un autre élément, sans nécessiter de modifications du programme central. »)

---

## 2. Mégadonnées — Bases de données (06.MegadonneesBD-H26)

### Q3 — Modélisation conceptuelle
**Question :** On souhaite organiser l'information d'un système universitaire. Le système comprend :
- des étudiants (ID, nom, âge, nationalité)
- des professeurs (ID, nom, publications)
- des cours (suivis par les étudiants et enseignés par les professeurs).

Tâche : identifier les principaux concepts et lister les attributs pertinents, puis concevoir une représentation conceptuelle (p. ex. un diagramme E-R).

**Réponse (modèle E-R proposé) :**

| Student | Course | Professor |
|---|---|---|
| ID | ID | ID |
| Name | Name | Name |
| Age | studentID | publications |
| Nationality | professorID | |

Relations : Student `1..N — 0..N` Course ; Course `0..N — 1` Professor.

---

### Q4 — RDB suffisante ?
**Question :** Maintenant, ne parlons pas d'étudiants et de professeurs, mais d'étoiles, de planètes et de systèmes planétaires. Il y a des milliards d'objets, plus de types d'objets et des relations plus complexes. Est-il suffisant d'utiliser une base de données relationnelle (RDB) ?

**Réponse :** Non. Nous avons besoin d'une infrastructure plus puissante et plus flexible :
- Pour gérer le volume et la complexité des données.
- Pour intégrer de nouveaux types de données.

---

## 3. AOP — Programmation orientée aspects (11-AOP-H25)

### Q5 — Système bancaire en ligne
**Question :** Vous développez un système bancaire en ligne (transferts entre comptes). Est-ce suffisant pour un système bancaire en ligne ?
- Qu'en est-il de la sécurité ? (Est-ce que n'importe qui peut transférer de l'argent entre deux comptes ?)
- Qu'en est-il de l'intégrité ? (Peut-on toujours transférer de l'argent d'un compte ?)
- Qu'en est-il de la transparence et de la traçabilité ? (Les transactions doivent être enregistrées et récupérables pour fins de futures vérifications.)

**Réponse (Solution #2) :**
- Sécurité +
- Intégrité +
- Traçabilité +

Mais avons-nous terminé ? Si ces enjeux doivent être considérés dans chaque fonction (≈10 méthodes…), nous aurons beaucoup de répétitions ; toute modification de la politique impactera toutes les parties affectées (risque d'oubli ou d'incohérence). → Motivation pour AOP.

---

### Q6 — Mythes et réalités sur AOP

**Q :** Le flot de contrôle du programme est difficile à suivre.
**R :** Effectivement. Mais c'est ce qu'on souhaite ! On veut travailler à un niveau d'abstraction plus élevé. Et le polymorphisme ?

**Q :** AOP ne règle pas de nouveaux problèmes.
**R :** En effet. On ne cherche pas à résoudre de nouveaux problèmes, mais à résoudre les problèmes actuels de façon plus efficace.

**Q :** AOP encourage les mauvais designs.
**R :** Faux. AOP nous permet de corriger des problèmes difficilement corrigibles en OO, mais la bonne conception OO des classes issues du domaine du problème reste nécessaire.

**Q :** AOP peut être utile, mais la définition correcte d'interfaces est tout aussi efficace.
**R :** Faux. Pensez à l'exemple de « logfile » : l'utilisation d'une librairie pour enregistrer les traces d'exécution nécessite quand même une invocation dans chaque fonction dont on veut garder la trace.

**Q :** AOP ne fait que « patcher » la conception des classes du domaine.
**R :** Faux. AOP permet d'augmenter la modularité, la compréhensibilité et la traçabilité du code.

**Q :** AOP brise l'encapsulation.
**R :** Vrai, mais d'une façon systématique et contrôlée. On peut briser l'encapsulation d'une classe à partir d'un aspect. AOP est donc très puissant, mais ce pouvoir doit être utilisé correctement.

**Q :** AOP va remplacer l'OO.
**R :** Faux. Les concepts issus du domaine du problème continuent d'être modélisés avec des objets. AOP est utile pour modéliser les fonctions transversales qui, autrement, nécessiteraient des modifications à plusieurs classes du domaine.

**Q :** AOP n'est pas mature.
**R :** AspectJ en est à la version 1.9.23 (intégré à Eclipse, NetBeans, JBuilder, Emacs JDDE). AspectC++ 2.2 est disponible (intégré à Eclipse). AOP est disponible dans : Java, C#, C/C++, PHP, Haskell, JavaScript, Matlab, Perl, Prolog, Python, Ruby, XML.

---

# 11-Review (révision finale du cours)

> Le document 11-Review contient l'essentiel des questions/réponses utilisées comme révision pour l'examen.

## 4. Architecture vs. Conception

### Q7 — Architecture vs. Conception
**Question :** En quoi l'architecture logicielle diffère-t-elle de la conception logicielle en termes de types d'exigences qu'elles traitent ?

**Réponse :**
- L'architecture : gérer à la fois les exigences fonctionnelles **et** non fonctionnelles.
- La conception : traiter principalement les exigences fonctionnelles.

---

## 5. Patrons de conception et principes (SOLID)

### Q8 — Définitions à connaître
**Questions :**
- Que signifie SOLID ?
- Définir chaque principe.
- Comparer les principes entre eux.
- Identifier quel(s) principe(s) sont violé(s).
- Comment corriger ? Refactoring (remonter/descendre des méthodes ou des classes ; ajouter ou modifier la hiérarchie).

**Réponse — Principes SOLID :**

| Principe | Définition |
|---|---|
| Single Responsibility (SRP) | Une classe doit avoir une seule et unique responsabilité. |
| Open/Close (OCP) | Les composants logiciels doivent être ouverts à l'extension, mais fermés à la modification. |
| Liskov Substitution (LSP) | Les types dérivés doivent pouvoir être entièrement substitués à leurs types de base. |
| Interface Segregation (ISP) | Les clients ne doivent pas être forcés d'implémenter des méthodes inutiles qu'ils n'utiliseront pas. |
| Dependency Inversion (DIP) | Dépendez des abstractions, pas des implémentations concrètes. |

---

### Q9 — QCM SOLID
**Question :** Selon ce principe de conception SOLID, il est préférable de maintenir plusieurs interfaces simples plutôt qu'une seule interface grande et complexe.
- a) Principe de Ségrégation des Interfaces (ISP)
- b) Principe d'Inversion des Dépendances (DIP)
- c) Principe de Responsabilité Unique (SRP)

**Réponse :** **a) ISP — Principe de Ségrégation des Interfaces.**

---

## 6. Styles d'architecture

### Q10 — Étude de cas : application de partage de fichiers
**Question :** Vous êtes l'architecte principal chargé de concevoir une nouvelle application de partage de fichiers. Cette application doit permettre le partage direct de fichiers entre utilisateurs sans serveur central. La conception doit être scalable, capable de gérer un grand nombre d'utilisateurs simultanément, et minimiser la dépendance aux ressources centralisées (coût, goulets d'étranglement). Quel style architectural choisiriez-vous ? Justifiez votre réponse.

**Réponse :** Architecture **Pair-à-pair (P2P)** :
- Permet le partage direct de fichiers entre utilisateurs, sans serveur central.
- Naturellement scalable : chaque nouvel utilisateur apporte des ressources supplémentaires au réseau.
- Réduit les coûts liés à l'infrastructure centrale.
- Évite les goulets d'étranglement associés aux serveurs centralisés.

> Note de la prof : pour SOA / microservices, **toujours mentionner le type de communication** utilisé (SOAP, REST, RPC, GraphQL).
> « Modulaire » seul **n'est pas accepté** comme réponse → préciser : Pipe-Filter, Layered, MVC ou Blackboard.

---

## 7. Frameworks (Cadriciels)

### Q11 — Plugin vs Framework
**Question :** Expliquez en quoi un plugin et un framework diffèrent en termes de fonctionnalité au sein d'un système logiciel et de leur influence sur le flux de contrôle d'une application.

**Réponse :**

**Plugin :**
- Ajoute ou étend des fonctionnalités spécifiques dans une application sans modifier le code central.
- Introduit de nouvelles capacités ou intégrations, mais repose sur l'infrastructure de l'application hôte.
- Le flux de contrôle est déclenché par événements ; l'application hôte décide quand les fonctions du plugin sont exécutées.

**Framework :**
- Fournit un plan structuré pour le développement d'applications, avec des fonctionnalités prédéfinies que les développeurs peuvent étendre.
- Suit le principe de l'**inversion de contrôle (IoC)** : le framework gère le cycle de vie et le flux de contrôle ; les développeurs implémentent les détails spécifiques.

---

## 8. Mauvaise conception (Antipatrons)

### Q12 — QCM antipatron
**Question :** Quel anti-patron (antipattern) conduit à une interface excessivement complexe, prenant en charge de nombreux cas d'usage ?
- a) Cover your assets
- b) Swiss Army Knife
- c) Jumble

**Réponse :** **b) Swiss Army Knife** (Couteau suisse) — interface complexe qui expose de nombreuses fonctionnalités.

---

## 9. Mégadonnées — Entrée et analyse de données

### Q13 — QCM MapReduce
**Question :** Identifiez l'affirmation FAUSSE :
- a) Un job MapReduce divise généralement le jeu de données d'entrée en blocs indépendants, qui sont traités par les tâches map de manière entièrement parallèle.
- b) Le framework MapReduce fonctionne exclusivement sur des paires <clé, valeur>.
- c) Le jeu de données d'entrée de MapReduce est dynamique.

**Réponse :** **c)** est fausse — le jeu de données d'entrée est statique (pas dynamique).

---

### Q14 — QCM Streaming événementiel
**Question :** Ce framework de streaming traite les flux de données de manière orientée événements :
- Kafka
- Spark
- RabbitMQ

**Réponse :** **Kafka.**
(Rappel : « La définition des flux et l'entrée des données est basée sur le temps en Spark et sur les évènements en Kafka. »)

---

## 10. Mégadonnées — Bases de données et théorème CAP

### Q15 — Choix d'une BD NoSQL
**Question :** Vous développez une plateforme de blogs où chaque article peut avoir des attributs variables, et les utilisateurs doivent pouvoir rechercher des articles en fonction du contenu textuel et des tags. Quel type de base de données NoSQL est le plus approprié ? Justifiez votre réponse.

**Réponse :** **Base de données orientée documents** (ex. : MongoDB)
- Adaptée aux données semi-structurées, comme les articles de blog avec des attributs variables.
- Permet une recherche textuelle efficace grâce à des fonctionnalités d'indexation avancées.
- Convient parfaitement aux applications riches en contenu.
- Offre une flexibilité du schéma, idéale pour des données hétérogènes.

---

### Q16 — QCM ACID vs BASE
**Question :** Quel modèle de données est le plus adapté pour le cas d'usage suivant : « Un système doit refléter un changement immédiatement » ?
- a) BASE
- b) ACID

**Réponse :** **b) ACID** (cohérence forte / immédiate).

---

### Q17 — QCM Théorème CAP
**Question :** Selon le théorème CAP, un système ne peut satisfaire qu'au maximum deux des trois garanties (Cohérence, Disponibilité, Tolérance aux partitions). Quelle garantie NE PEUT PAS être sacrifiée dans un système distribué ?
- a) Cohérence
- b) Tolérance aux partitions
- c) Disponibilité

**Réponse :** **a) Cohérence** ne peut pas être sacrifiée — *(réponse marquée « a. » dans la diapositive)*.
*(Remarque : dans un système distribué, on considère que la tolérance au partitionnement est garantie par défaut ; on choisit ensuite entre cohérence et disponibilité.)*

---

## 11. Blockchain

### Q18 — QCM PoW vs PoS
**Question :** Laquelle des affirmations suivantes distingue correctement le Proof of Work (PoW) du Proof of Stake (PoS) ?
- a) Le Proof of Work repose sur la puissance de calcul pour valider les transactions, tandis que le Proof of Stake repose sur la quantité de cryptomonnaie détenue par les validateurs.
- b) Le Proof of Stake consomme nettement plus d'énergie que le Proof of Work en raison de sa dépendance à la puissance de calcul.
- c) Le Proof of Work sélectionne les validateurs en fonction de leurs avoirs en cryptomonnaie, tandis que le Proof of Stake les sélectionne en fonction de leurs performances en minage.

**Réponse :** **a)** — PoW = puissance de calcul ; PoS = montant de cryptomonnaie détenue.

---

## 12. Architectures évènementielles & patrons de gestion d'événements

### Q19 — Étude de cas : choix d'un patron de gestion d'événements
**Question :** Vous êtes l'architecte principal chargé de concevoir une nouvelle application de partage de fichiers (P2P, scalable, sans serveur central, beaucoup d'utilisateurs simultanés, latence minimale). Sélectionnez un modèle de gestion d'événements parmi les options suivantes et justifiez votre choix :
- Reactor
- Proactor
- Asynchronous Completion Token
- Acceptor-Connector

**Réponse :** **Proactor.**
- Permet la gestion **asynchrone complète** des opérations d'entrée/sortie.
- Très performant pour les systèmes à forte concurrence, comme les applications P2P avec de nombreux transferts de fichiers simultanés.

---

## 13. SOA — Architectures orientées services

### Q20 — QCM Affirmation correcte
**Question :** Indiquez l'affirmation CORRECTE :
- a) GraphQL permet l'exécution distante d'une fonction dans un contexte différent.
- b) SOAP est un protocole de communication web hautement standardisé utilisant un format XML.
- c) En REST, les ressources peuvent partager des identifiants uniques (URI).

**Réponse :** **b) SOAP est un protocole de communication web hautement standardisé utilisant un format XML.**
*(a) décrit RPC, pas GraphQL ; (c) en REST, chaque ressource a un URI unique.)*

---

### Q21 — Étude de cas : plateforme de télémédecine
**Question :** Vous concevez l'architecture d'un système pour une plateforme de télémédecine. Communication temps réel entre divers modules (récupération des données patients, planification des rendez-vous, consultations directes). Le système exige des appels de méthode rapides, fiables et directs, des interactions synchrones, sécurisées, à latence minimale. Choisissez le mécanisme de communication SOA le plus adapté (SOAP, REST, RPC ou GraphQL) et justifiez votre choix.

**Réponse :** **RPC.**
- **Communication en temps réel** : interactions instantanées, cruciales pour des soins en temps voulu.
- **Appels de méthode directs** : simplifie les interactions entre modules.
- **Fiabilité** : tolérance aux pannes, livraison sécurisée des messages, accusés de réception.
- **Sécurité** : protège les données des patients (chiffrement, authentification).
- **Latence minimale** : conception légère.
- **Facilité d'intégration** : compatible avec divers langages et plateformes.

---

## 14. Microservices

### Q22 — QCM Strangling the monolith
**Question :** L'objectif de ce processus est de remplacer progressivement les fonctionnalités principales d'une application monolithique par d'autres microservices :
- a) Étouffer le monolithe (Strangling the monolith)
- b) Composer le monolithe (Composing the monolith)
- c) Construire des microservices (Constructing microservices)

**Réponse :** **a) Étouffer le monolithe (Strangling the monolith).**

---

## 15. AOP — Révision finale

### Q23 — Concepts de base de l'AOP
**Questions :**
- Qu'est-ce qu'une préoccupation transversale (cross-cutting concern) ? Des exemples ?
- Pourquoi la programmation orientée aspects (AOP) est-elle utile ? Quels sont ses avantages ?
- Qu'est-ce qu'un aspect, un advice, un pointcut ?

*(Définitions à maîtriser ; pas de réponse explicite donnée — voir cours AOP.)*

---

### Q24 — QCM Aspect / Pointcut
**Question :** Complétez les blancs : Un _______ est une construction qui permet l'injection de préoccupations transversales (cross-cutting concerns). La méthode qui implémente les tâches transversales telles que la journalisation ou la mise en cache s'appelle **Advice**. Tandis que ______ est une expression de motif qui identifie les endroits où le Advice doit être invoqué.
- a) Aspect, Joinpoint
- b) Aspect, Pointcut
- c) Classe, Pointcut
- d) Classe, Joinpoint

**Réponse :** **b) Aspect, Pointcut.**

---

# Annexes utiles (rappels pédagogiques)

## A. Réponses NON acceptées dans les examens / quiz
- « Modulaire » seul n'est pas une réponse acceptée → préciser **Pipe-Filter / Layered / MVC / Blackboard**.
- « Distribué » seul n'est pas accepté → préciser **Client-Server / Multitier / Primary-Secondary / Peer-to-peer / Broker / SOA / EDA**.

## B. Hors-programme de l'examen final
- Semaine 3 : Qualité de la conception, attributs de qualité, métriques de qualité.
- Semaine 4 : code antipatterns (diapos 50 à la fin).

---

# Examen Final — LOG8430, Automne 2023 (corrections proposées)

> Les questions ci-dessous sont reproduites depuis le document `LOG8430_Final1_A2023_QS.pdf` (questions seulement).
> Les corrections sont **générées** à partir du contenu du cours et du document de révision.

## Section 2 — Choix multiples (2 pts/question, 20 pts au total)

### 2.1 — Principe SOLID
**Question :** According to this (SOLID) design principle, it is better to maintain several simple interfaces than one large and complex interface.
- ☐ Interface Segregation Principle (ISP)
- ☐ Dependency Inversion Principle (DIP)
- ☐ Single Responsibility Principle (SRP)

**Correction :** ☑ **Interface Segregation Principle (ISP)** — Les clients ne doivent pas être forcés d'implémenter des méthodes inutiles. ISP recommande plusieurs interfaces simples et spécifiques plutôt qu'une seule interface monolithique.

---

### 2.2 — Antipatron architectural
**Question :** The architectural antipattern results in an excessively complex interface that provides and supports various use cases.
- ☐ Cover your assets
- ☐ Swiss army knife
- ☐ Jumble

**Correction :** ☑ **Swiss Army Knife** — Une seule interface expose énormément de fonctionnalités au lieu d'être divisée en interfaces spécialisées (« Cover your assets » = documentation interminable ; « Jumble » = mélange éléments horizontaux/verticaux).

---

### 2.3 — Affirmation FAUSSE sur MapReduce
**Question :** Point out the WRONG statement.
- ☐ A MapReduce job usually splits the input dataset into independent chunks, which are processed by the map tasks in a completely parallel manner.
- ☐ The MapReduce framework operates exclusively on <key, value> pairs.
- ☐ The input data set of MapReduce is dynamic.

**Correction :** ☑ **« The input data set of MapReduce is dynamic »** est FAUSSE. Le jeu de données d'entrée d'un job MapReduce est **statique** (immuable pendant l'exécution du job, traitement par lots). Les deux autres affirmations sont correctes.

---

### 2.4 — Streaming orienté événements
**Question :** This streaming framework processes streams of data in an event-based manner.
- ☐ Kafka
- ☐ Spark
- ☐ RabbitMQ

**Correction :** ☑ **Kafka** — En Kafka, les flux sont définis par les évènements ; en Spark, ils sont définis par le temps (micro-batches), ce qui en fait une « fausse » analyse en streaming. RabbitMQ est un broker de messages, pas un framework de streaming.

---

### 2.5 — ACID vs BASE
**Question :** Which data model is the best for the use case: "A system needs to reflect a change immediately".
- ☐ BASE
- ☐ ACID

**Correction :** ☑ **ACID** — ACID garantit la cohérence forte (Atomicity, Consistency, Isolation, Durability). BASE prône une cohérence éventuelle, incompatible avec « refléter un changement immédiatement ».

---

### 2.6 — Théorème CAP
**Question :** According to the CAP theorem, a system can satisfy at most two of three guarantees, Consistency, Availability, and Partition tolerance. Which guarantee CANNOT be sacrificed in a distributed system?
- ☐ Consistency
- ☐ Partition tolerance
- ☐ Availability

**Correction :** ☑ **Partition tolerance** — Le cours indique explicitement : « On considère que la tolérance au partitionnement est garantie par défaut » dans un système distribué. Les partitions réseau étant inévitables, on doit choisir entre Consistency et Availability mais **jamais sacrifier P**.
*(Remarque : la diapo de révision marque « a », à interpréter selon l'ordre des choix présenté — ici l'option correcte est bien Partition tolerance, conforme au théorème CAP standard et au contenu du cours.)*

---

### 2.7 — Trilemme Blockchain
**Question :** According to this theorem, Blockchain cannot guarantee all three of which properties at the same time?
- ☐ Partition tolerance, consistency, availability
- ☐ Atomicity, isolation, consistency, durability
- ☐ Security, Scalability, Decentralisation

**Correction :** ☑ **Security, Scalability, Decentralisation** — C'est le **trilemme de la Blockchain** : difficulté à optimiser une propriété tout en équilibrant les compromis entre sécurité, scalabilité et décentralisation. (CAP s'applique aux BD distribuées ; ACID est une propriété des transactions.)

---

### 2.8 — Affirmation CORRECTE
**Question :** Point out the CORRECT statement:
- ☐ GraphQL allows for the remote execution of a function in a different context.
- ☐ SOAP is an XML-formatted, highly standardized web communication protocol.
- ☐ In REST, resources can share unique identifiers (URI).

**Correction :** ☑ **SOAP is an XML-formatted, highly standardized web communication protocol.**
- (a) est faux — c'est RPC qui permet l'exécution distante d'une fonction.
- (c) est faux — en REST, **chaque ressource a un URI unique** (les ressources ne partagent pas leurs URI).

---

### 2.9 — Migration monolithe → microservices
**Question :** The goal of this process is to incrementally replace the core functionalities of a monolithic application with other microservices:
- ☐ Strangling the monolith
- ☐ Composing the monolith
- ☐ Constructing microservices

**Correction :** ☑ **Strangling the monolith** — Le « Strangler Pattern » remplace progressivement les fonctionnalités du monolithe par des microservices, jusqu'à ce que le monolithe soit complètement « étranglé ».

---

### 2.10 — AOP : Aspect / Pointcut
**Question :** Fill in the blanks. An _______ is a construct that allows the injection of cross-cutting concerns. The method which implements the cross-cutting tasks such as logging, or caching is called Advice. While ______ is a pattern expression that matches the places where the Advice should be invoked.
- ☐ Aspect, Joinpoint
- ☐ Aspect, Pointcut
- ☐ Class, Pointcut
- ☐ Class, Joinpoint

**Correction :** ☑ **Aspect, Pointcut** —
- Un **Aspect** est la construction qui regroupe les préoccupations transversales.
- Un **Pointcut** est une expression de motif qui sélectionne les **joinpoints** où l'**Advice** sera invoqué.
- (Un *Joinpoint* est un point individuel d'exécution ; un *Pointcut* est l'expression qui en sélectionne plusieurs.)

---

## Section 3 — Plugin vs. Framework (6 pts)

**Question :** Explain how a plugin and a framework differ in terms of their functionality within a software system and their influence on the control flow of an application.

**Correction :**

**Plugin :**
- Ajoute ou étend des fonctionnalités spécifiques à une application sans modifier le code central.
- Repose sur l'infrastructure de l'application hôte (système de base atomique et indépendant).
- **Flux de contrôle** : déclenché par événements ; **c'est l'application hôte qui décide** quand les fonctions du plugin sont exécutées.
- Vise principalement l'expérience **utilisateur**.

**Framework (cadriciel) :**
- Architecture à moitié implémentée et générique : un **squelette** avec des fonctionnalités de base, destiné à être étendu.
- Fournit un plan structuré pour le développement d'applications.
- **Flux de contrôle** : suit le principe de l'**Inversion de Contrôle (IoC)** — c'est le **framework** qui gère le cycle de vie et appelle le code du développeur (« don't call us, we'll call you »).
- Vise principalement l'expérience **développeur**.

**Différence clé sur le flot de contrôle :** avec un plugin, le programme principal contrôle l'exécution et invoque le plugin ; avec un framework, le framework contrôle l'exécution et invoque le code du développeur.

---

## Section 4 — Application de partage de fichiers

### 4.1 — Style architectural (8 pts)
**Question :** What architectural style would you choose for this system? Justify your response. *Note: Answers like modular, distributed, layered, multitiered are not acceptable.*

**Correction :** Style **Pair-à-pair (Peer-to-Peer / P2P)**.

**Justification :**
- **Partage direct sans serveur central** : dans P2P, tous les pairs sont égaux ; pas de données centralisées. Cela répond exactement à l'exigence de partage direct entre utilisateurs.
- **Scalabilité naturelle** : chaque nouvel utilisateur ajoute des ressources (CPU, stockage, bande passante) au réseau au lieu d'en consommer auprès d'un serveur central → la capacité du système croît avec le nombre d'utilisateurs.
- **Réduction des coûts d'infrastructure** : pas besoin de payer/maintenir un serveur central de grande taille.
- **Élimination des goulets d'étranglement** : pas de point central de contention qui limite les performances ou crée un point de défaillance unique (SPOF).
- **Tolérance aux pannes** : la disparition d'un pair ne fait pas tomber le système (à comparer avec un client-serveur).

**Exemple :** applications de partage de fichiers comme BitTorrent.

---

### 4.2 — Patron de gestion d'événements (4 pts)
**Question :** Select one event handling pattern from: Reactor, Proactor, Asynchronous Completion Token, or Acceptor-Connector. Justify why it is the most suitable for this scenario.

**Correction :** **Proactor**.

**Justification :**
- Le Proactor **lance des opérations asynchrones et traite les résultats une fois terminés**, permettant une exécution simultanée sans attente bloquante.
- Idéal pour les **systèmes à forte concurrence** comme une application P2P avec **de nombreux transferts de fichiers simultanés**.
- Permet la **gestion asynchrone complète** des opérations d'I/O (lecture/écriture de gros fichiers, transferts réseau), ce qui maximise le débit et la réactivité.
- Comparé au Reactor (qui est synchrone côté traitement), le Proactor évite que le thread soit bloqué pendant les longues opérations d'I/O — crucial quand des centaines de pairs téléchargent/téléversent en parallèle.
- ACT et Acceptor-Connector sont des patrons complémentaires (corrélation des réponses, séparation connexion/traitement) mais ne sont pas en eux-mêmes des modèles de gestion d'événements asynchrones complets adaptés à ce besoin de scalabilité massive.

---

## Section 5 — Plateforme de blogs (7 pts)

**Question :** You are developing a blogging platform where each blog post can have varying attributes (title, content, author details, tags, comments, multimedia). Users need to search for posts based on text content and tags. Which NoSQL database type is most appropriate? Justify your answer.

**Correction :** **Base de données orientée documents** (ex. : MongoDB).

**Justification :**
- **Attributs variables par article** : un schéma flexible est nécessaire (certains articles ont des images, d'autres des vidéos, des tags variables, etc.). Les BD documents associent chaque clé à une **structure de données complexe** (document JSON/BSON) sans imposer de schéma fixe — parfait pour des données semi-structurées et hétérogènes.
- **Recherche par contenu textuel et tags** : les BD documents (notamment MongoDB) offrent des **fonctionnalités d'indexation avancées**, dont l'indexation full-text et l'indexation sur les tableaux (idéal pour les tags).
- **Riche en contenu** : les BD documents sont conçues pour récupérer l'**ensemble du document** (l'article complet avec ses commentaires et métadonnées) en une seule requête — ce qui correspond exactement au cas d'usage d'affichage d'un article de blog.
- **Évolutivité du schéma** : on peut ajouter ou retirer des champs (nouveaux types de tags, nouvelles métadonnées) sans migration coûteuse, à mesure que la plateforme évolue.
- **Pourquoi pas les autres ?**
  - *Key-value* : trop simple, pas de recherche par contenu textuel.
  - *Graph* : surdimensionné, sauf si la plateforme tourne autour des relations sociales entre utilisateurs.
  - *Wide-column* : plutôt pour des données stables, peu modifiées, à très grand volume — pas optimal pour de la recherche textuelle riche.

**Exemple concret :** MongoDB est utilisé par de nombreuses plateformes de contenu (eBay, Forbes, etc.).

---

## Section 6 — Plateforme de télémédecine (10 pts)

**Question :** Select the most suitable SOA communication mechanism (SOAP, REST, RPC, or GraphQL) for the telemedicine scenario (real-time, quick/reliable/direct method invocations, synchronous, secure, low-latency). Justify your choice.

**Correction :** **RPC** (Remote Procedure Call).

**Justification détaillée par exigence :**

| Exigence du scénario | Comment RPC y répond |
|---|---|
| **Communication en temps réel** | RPC permet des **interactions instantanées** via des appels de procédure directs ; particulièrement adapté à des décisions médicales qui doivent être prises rapidement. |
| **Appels de méthode rapides et directs** | RPC abstrait l'appel réseau pour qu'il ressemble à un appel de fonction local, simplifiant les interactions entre les modules de santé (récupération données patients, planification, consultations). |
| **Interactions synchrones fluides** | RPC est intrinsèquement **synchrone et bloquant** par défaut (requête-réponse), assurant la cohérence des échanges entre modules. |
| **Fiabilité** | RPC garantit la tolérance aux pannes, la livraison sécurisée des messages et les accusés de réception. |
| **Sécurité** | RPC supporte le chiffrement et l'authentification (TLS, mTLS pour gRPC), critiques pour les données de santé (PHI/HIPAA). |
| **Latence minimale** | RPC a une **conception légère** (notamment gRPC avec Protobuf et HTTP/2), bien plus performant que SOAP/XML pour les communications inter-modules. |
| **Facilité d'intégration** | gRPC est compatible avec un grand nombre de langages et plateformes — utile pour intégrer des modules de santé hétérogènes (EHR, planification, etc.). |

**Pourquoi pas les autres ?**
- **SOAP** : très standardisé et sécurisé, mais le format XML est verbeux → latence et débit moins bons que RPC. Adapté aux systèmes financiers/legacy, pas à des communications temps réel.
- **REST** : architecture orientée ressources via HTTP, idéal pour les APIs publiques basées sur des ressources, mais moins adapté à des **invocations de méthodes directes** entre modules internes en temps réel ; surcoût HTTP/JSON par rapport à gRPC.
- **GraphQL** : excellent pour réduire l'over-fetching dans des applications mobiles ou des UIs complexes, mais ses requêtes sont conçues côté client et son évaluation côté serveur introduit du surcoût ; il n'est pas optimal pour des **appels de méthode directs synchrones** entre microservices internes à faible latence.

**Conclusion :** RPC (idéalement **gRPC**) est le mécanisme SOA le plus adapté à la télémédecine décrite : appels de méthode rapides, synchrones, sécurisés, à très faible latence, avec un excellent support multi-langage pour les différents modules.