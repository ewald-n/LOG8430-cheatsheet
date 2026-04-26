# LOG8430 : Architectures Événementielles (EDA) & Patrons de Concurrence

## 1. Fondamentaux de l'Architecture Orientée Événements (EDA)
### Définitions Clés
* [cite_start]**Événement** : Toute action pertinente au système (ex: clic GUI, changement de données) qui affecte l'état ou le comportement des objets[cite: 2895, 2896].
* [cite_start]**Message** : Notification suivant l'événement, produite par le système/producteur et destinée à l'auditeur[cite: 2903, 2905].
* [cite_start]**Bus d'événements** : Canal/tampon où les événements sont enregistrés, stockés temporairement et transmis[cite: 2908].

### Propriétés et Avantages
* [cite_start]**Parallélisation** : Capacité augmentée car le bus peut être partagé par plusieurs producteurs/consommateurs[cite: 2918, 2921].
* [cite_start]**Évolutivité (Scalability)** : Les consommateurs peuvent être répliqués pour paralléliser les tâches[cite: 2923, 2924].
* [cite_start]**Agnotisme Technologique** : Interfaces définissables pour différents langages ; base des architectures orientées services (SOA)[cite: 2925, 2926].
* [cite_start]**Réactivité** : Traitement asynchrone en temps réel, éliminant les traitements par lots (batch) et réduisant les goulots d'étranglement[cite: 2938, 2939].

### Les 4 Styles d'Interaction
| Style | Initiateur | Participants | Exemple de tâche |
| :--- | :--- | :--- | :--- |
| **Déclenché par le temps** | [cite_start]Horaire prévu [cite: 2839] | [cite_start]Systèmes prédéfinis [cite: 2839] | [cite_start]Sauvegardes, rapports horaires [cite: 2784, 2839] |
| **Déclenché par la demande** | [cite_start]Client (App mobile) [cite: 2800] | [cite_start]Client / Serveur [cite: 2839] | [cite_start]Appels API, requêtes BD [cite: 2839] |
| **Déclenché par événement** | [cite_start]Événement externe [cite: 2839] | [cite_start]Dynamique / Ouvert [cite: 2839] | [cite_start]Notification de pic de conso [cite: 2820] |
| **Basé sur les données** | [cite_start]Données entrantes [cite: 2826] | [cite_start]Systèmes / Sources de données [cite: 2839] | [cite_start]Optimisation IA via météo/prix [cite: 2827] |

---

## 2. Patrons d'Accès et de Configuration de Service
[cite_start]*Objectif : Gérer l'accès aux interfaces et l'évolution des composants sans recompilation statique[cite: 2951, 3196].*

### A. Wrapper Façade
* [cite_start]**Définition** : Encapsule des fonctions/données de bibliothèques existantes (souvent C non-OO) dans des interfaces OO concises et portables[cite: 3104, 3176].
* [cite_start]**Exemple** : Le **Hardware Abstraction Layer (HAL)** d'Android encapsulant le Kernel Linux[cite: 3114, 3136].
* [cite_start]**Avantages** : Maintenabilité, modularité, élimination des erreurs de programmation directe sur API bas niveau[cite: 3180, 3181].
* [cite_start]**Limites** : Perte potentielle de fonctionnalités de l'abstraction sous-jacente et légère réduction de performance[cite: 3183, 3187].

### B. Component Configurator (Configurateur de composant)
* [cite_start]**Définition** : Permet de lier/délier des implémentations au moment de l'exécution (runtime) sans redémarrer le processus[cite: 3196, 3197].
* [cite_start]**Analogie** : Un coach de football substituant des joueurs durant un match[cite: 3236, 3239].
* [cite_start]**Avantages** : Configuration dynamique, administration centralisée[cite: 3226, 3228].
* [cite_start]**Limites** : Incertitude accrue sur les interactions entre composants, sécurité réduite[cite: 3229, 3230].

### C. Interceptor (Intercepteur)
* [cite_start]**Définition** : Ajout transparent de services déclenchés automatiquement par des événements spécifiques[cite: 3257].
* [cite_start]**Exemple** : Réexpédition de courrier lors d'un changement d'adresse[cite: 3289].
* [cite_start]**Avantages** : Extensibilité, séparation des responsabilités (logging, sécurité)[cite: 3312, 3313, 3325].
* [cite_start]**Limites** : Point d'insertion de vulnérabilités, risque d'interceptions en cascade[cite: 3319].

### D. Extension Interface
* [cite_start]**Définition** : Un composant expose plusieurs interfaces pour respecter le principe de **ségrégation d'interface** et éviter l'encombrement[cite: 3331].
* [cite_start]**Mécanisme** : Utilisation d'une `Root Interface` avec `getExtension()` pour accéder aux fonctionnalités spécifiques[cite: 3350, 3351].

---

## 3. Patrons de Synchronisation
[cite_start]*Objectif : Minimiser le surcoût de verrouillage et prévenir l'auto-blocage (deadlock)[cite: 3008, 3484].*

### A. Scoped Locking (Verrouillage de portée)
* [cite_start]**Mécanisme** : Le verrou est acquis à l'entrée d'un bloc et libéré automatiquement à la sortie (ex: destructeur en C++), même en cas d'exception[cite: 3396, 3409].
* [cite_start]**Technologie** : `std::lock_guard` en C++[cite: 3405].
* [cite_start]**Limite** : Risque d'interblocage en cas d'appels récursifs[cite: 3417].

### B. Strategized Locking (Verrouillage stratégique)
* [cite_start]**Mécanisme** : Paramétrer le mécanisme de synchronisation comme une stratégie pour s'adapter à diverses architectures sans changer le code métier[cite: 3426, 3427].
* [cite_start]**Avantage** : Réutilisabilité et personnalisation selon l'usage (lecture vs écriture)[cite: 3434, 3453].

### C. Thread-Safe Interface
* **Mécanisme** : 
    1. [cite_start]Les méthodes **publiques** (interface) acquièrent le verrou[cite: 3487].
    2. [cite_start]Les méthodes **privées** (implémentation) font confiance aux publiques et n'acquièrent pas de verrou[cite: 3488].
* [cite_start]**Avantage** : Évite l'auto-blocage lors d'appels intra-composants ou récursifs[cite: 3484].

### D. Double-Checked Locking Optimization
* [cite_start]**Objectif** : Réduire le surcoût quand une section critique ne doit s'exécuter qu'une seule fois (ex: Singleton)[cite: 3521, 3522].
* [cite_start]**Algorithme** : Vérifier un flag/pointeur -> Si nul, acquérir le verrou -> Re-vérifier (double check) -> Exécuter[cite: 3536, 3541].

---

## 4. Modèles de Concurrence
| Patron | Objectif | Caractéristique Unique |
| :--- | :--- | :--- |
| **Active Object** | [cite_start]Découpler l'invocation de l'exécution[cite: 3604]. | [cite_start]L'objet possède son propre thread de contrôle[cite: 3604]. [cite_start]Utilise `Proxy`, `Scheduler` et `Servant`[cite: 3611, 3613, 3614]. |
| **Monitor Object** | [cite_start]Synchroniser les méthodes concurrentes[cite: 3679]. | [cite_start]Garantit qu'une seule méthode s'exécute à la fois dans l'objet[cite: 3742]. [cite_start]Utilise `wait()` et `notify()`[cite: 3704]. |
| **Half-Sync / Half-Async** | [cite_start]Découpler traitements synchrones et asynchrones[cite: 3762]. | [cite_start]Utilise une file d'attente (`Queue`) entre la couche asynchrone (bas niveau) et synchrone (haut niveau)[cite: 3774, 3780]. |
| **Leader/Followers** | [cite_start]Modèle de thread pool efficace[cite: 3809]. | Un thread est "Leader" (attend l'event), les autres sont "Followers". [cite_start]Le leader promeut un nouveau leader avant de traiter l'event[cite: 3809, 3862]. |

---

## 5. Gestion des Événements (Event Handling)
### Reactor vs Proactor
* **Reactor (Réactif/Synchrone)** : L'application attend l'événement (via un démultiplexeur comme `select()`) et le traite immédiatement. [cite_start]Principe Hollywood : "Ne nous appelez pas, nous vous appellerons"[cite: 3905, 3931, 3972].
* **Proactor (Proactif/Asynchrone)** : L'application lance l'opération et continue. [cite_start]Le système (OS) exécute la tâche en arrière-plan et notifie l'application uniquement à la fin via un `Completion Handler`[cite: 3984, 3985, 4025].

### Patrons Complémentaires
* **Asynchronous Completion Token (ACT)** : Également appelé modèle **"Cookie"**. [cite_start]Permet à l'initiateur de passer un jeton au service, qui lui sera retourné inchangé pour identifier le contexte de la réponse[cite: 4084, 4091, 4093].
* **Acceptor-Connector** : Découple la connexion/initialisation (Acceptor/Connector) du traitement des données (Service Handler). [cite_start]Essentiel pour les systèmes P2P orientés connexion[cite: 4133, 4134, 4158].

---

## ⚡ Focus Examen : Points de vigilance
* **Reactor vs Proactor** : Dans le Reactor, c'est l'application qui fait l'I/O après notification. [cite_start]Dans le Proactor, c'est l'OS qui fait l'I/O et l'application reçoit le résultat[cite: 4067].
* [cite_start]**Synchronisation** : Ne jamais utiliser `Scoped Locking` seul dans une méthode récursive (risque de deadlock) ; combiner avec `Thread-Safe Interface`[cite: 3417, 3418].
* [cite_start]**Performance** : `Leader/Followers` est souvent plus performant que `Half-Sync/Half-Async` car il évite le passage de données entre threads (pas de file d'attente dynamique)[cite: 3871, 3873].