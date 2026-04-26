# LOG8430 - AIDE-MÉMOIRE : MAUVAISE CONCEPTION

# DÉFINITIONS CLÉS

## ANTIPATRON (Generique)
**Déf :** Une "mauvaise solution" à un problème courant. Semble efficace au début, mais cause des problèmes majeurs plus tard.
**Mots clés :** Solution à court terme, Dette technique, Piège, Contre-productif.

## ANTIPATRON ARCHITECTURAL
**Déf :** Erreur de structuration globale du système (haut niveau). Définit comment les gros composants interagissent.
**Mots clés :** Mauvais découpage, Couplage fort, Manque de vision globale, Monolithe rigide, Stovepipe.



## 1. ARCHITECTURE PAR IMPLICATION (Architecture by Implication)
**Déf :** Absence de planification architecturale explicite. On assume que les solutions passées s'appliquent sans analyse.
**Analogie :** Bâtir un château sur du sable car "on sait déjà bâtir des châteaux", sans vérifier le terrain.

### CAUSES
- Excès de confiance (gestionnaires/architectes).
- Dépendance aveugle aux expériences passées (contexte différent).
- Déficience en ingénierie système (enjeux non résolus).

### SYMPTÔMES & CONSÉQUENCES
- **S :** Manque de spécifications et de planification.
- **C :** Ignorance des nouvelles technos, risques cachés, complexité inattendue, échec imminent.

### REFACTORING
- **Modularisation en vues :** Séparer l'architecture en points de vue (Architecte, Développeur, Client).
- **Méthode GQA (Goal, Question, Answer) :** 1. **Objectifs (Goals) :** Définir ce que le système doit faire.
    2. **Questions :** Poser les questions critiques pour chaque objectif.
    3. **Réponses :** Fournir les vues/modèles qui répondent aux questions.

### EXCEPTIONS
- Différences entre projets minimes ou très localisées.
- Projets non critiques ou exploratoires (ex: Prototype/POC).


## 2. COUVRIR SES ARRIÈRES (Cover Your Assets)
**Déf :** Documentation excessive et hyper-détaillée qui tente de lister toutes les exceptions possibles pour éviter les critiques futures.
**Analogie :** Un manuel d'instruction de 1000 pages pour expliquer comment utiliser un marteau.

### CAUSES
- Peur des responsabilités ou des reproches.
- Culture d'entreprise bureaucratique.
- Manque de confiance envers les développeurs.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Documentation encombrante, complexe et illisible.
- **C :** Personne ne lit la doc, perte de temps massive, l'architecture réelle dévie de la doc papier.

### REFACTORING
- **Abstractions visuelles :** Remplacer les longs textes par des diagrammes et des tableaux.
- **Communication efficace :** Se concentrer sur l'essentiel pour que l'architecture soit comprise, pas juste "écrite".

### EXCEPTIONS
- Projets ultra-critiques (médical, spatial) où chaque détail doit être tracé légalement.

---

## 3. CONCEPTION PAR COMITÉ (Design by Committee)
**Déf :** Trop de décideurs sans direction claire. On essaie de satisfaire tout le monde en fusionnant toutes les idées.
**Citations clés :** "Un chameau est un cheval dessiné par un comité".

### CAUSES
- Rôles mal définis.
- Volonté de plaire à tout le monde.
- Réunions trop longues, fréquentes et mal organisées.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Conflits constants entre architectes/développeurs, doc contradictoire.
- **C :** Architecture incohérente, complexe inutilement, effort énorme pour interpréter le cahier des charges.

### REFACTORING
- **Rôles clairs :** Désigner un **Architecte Principal** (décideur final).
- **Priorisation :** Hiérarchiser les exigences au lieu de tout inclure.
- **Gestion de temps :** Réunions courtes avec objectifs précis ; diviser les équipes si nécessaire.

### EXCEPTIONS
- Très petites équipes où le consensus naturel est facile et rapide.

---

## 4. SYSTÈME EN TUYAUX DE POÊLE (Stovepipe System)
**Déf :** Survient lors de la migration d'un système local vers un système distribué. Le code garde des hypothèses "locales" qui ne fonctionnent plus à distance.
**Principe brisé :** Brise le *Single Responsibility* et la *Dependency Inversion* (le métier dépend du système de fichiers).

### CAUSES
- Absence de vision globale lors de la distribution.
- Hypothèses fortes sur l'emplacement des fichiers ou l'accès mémoire local.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Sous-systèmes isolés, interfaces inappropriées pour le réseau.
- **C :** Impossible de faire communiquer les parties, bugs de localisation, système rigide.

### REFACTORING
- **Patron FAÇADE :** Créer une interface simplifiée qui cache la complexité et l'isolation des sous-systèmes.
- **Abstraction des interfaces :** Redéfinir les interfaces pour qu'elles soient réellement "distribuées".

### EXCEPTIONS
- Systèmes qui n'ont jamais besoin d'être scalables ou distribués (logiciels standalone simples).

## 5. LE FOUILLIS (Jumble)
**Déf :** Mélange chaotique des éléments horizontaux (couches MVC) et verticaux (services/implémentations).
**Principe brisé :** Violation du **DIP** (*Dependency Inversion Principle*). On dépend d'implémentations concrètes au lieu d'abstractions.

### CAUSES
- Manque de communication entre architectes et développeurs.
- Développement rapide sans respecter la séparation des responsabilités.

### SYMPTÔMES & CONSÉQUENCES
- **Exemple type :** Une Vue qui contient des requêtes SQL directes (court-circuite le Modèle).
- **Conséquences :** Stabilité réduite, code impossible à réutiliser.

### REFACTORING
- **Abstractions horizontales :** Définir les couches (Architecture) comme des interfaces abstraites.
- **Implémentations verticales :** Garder les détails (BD, Services) comme des implémentations concrètes qui se plient à l'architecture.

---

## 6. RÉINVENTER LA ROUE (Reinvent the Wheel)
**Déf :** Concevoir un système de zéro en ignorant les architectures ou standards existants.
**Principe brisé :** Violation de **OCP** (*Open/Closed Principle*). L'architecture est trop spécifique et fermée à l'extension.

### CAUSES
- "Not Invented Here" syndrome (croire qu'on est les seuls à avoir ce problème).
- Connaissance insuffisante des solutions existantes ou des projets passés de la firme.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Application inutile de conceptions existantes (on refait ce qui existe déjà).
- **C :** Interopérabilité quasi-nulle, effort de développement démesuré, maintenance lourde.

### REFACTORING
- **Exploration :** Identifier les prototypes et architectures standards pertinents avant de coder.
- **Agilité :** Utiliser un processus en spirale/itératif pour raffiner les besoins.

### EXCEPTIONS
- Lorsque la communication est trop difficile ou coûteuse (frais de coordination) : repartir de zéro peut parfois être plus rapide à court terme pour une petite équipe isolée.

## 7. SPAGHETTI CODE
**Déf :** Logiciel manquant de structure et de cohérence.
**Principe brisé :** Modularité et abstraction quasi-invisibles.

### CAUSES
- Manque d'expérience en conception.
- Séparation des responsabilités inexistante.

### SYMPTÔMES & CONSÉQUENCES
- **Exemple type :** Code procédural, longues fonctions, aucune encapsulation.
- **Conséquences :** Compréhension et réutilisation difficiles, maintenance coûteuse.

### REFACTORING
- Appliquer les patrons de conception (Design Patterns) et les bonnes pratiques.
- Modulariser le code existant.

### EXCEPTIONS
- Tolérable si inévitable et temporaire, UNIQUEMENT dans l'implémentation (intérieur des fonctions) et non visible dans les interfaces publiques.

---

## 8. SWISS ARMY KNIFE
**Déf :** Interface trop complexe et polyvalente, essayant de couvrir trop de besoins différents.

### CONSÉQUENCES
- Interface chargée, difficile à utiliser et à maintenir.

### REFACTORING
- Diviser l'interface en plusieurs interfaces plus petites et cohérentes (Interface Segregation Principle).

---

## 9. VENDOR LOCK-IN
**Déf :** Dépendance directe et forte envers un fournisseur spécifique (logiciel ou matériel propriétaire).

### CAUSES
- Pas de standard ouvert respecté, format propriétaire.
- Choix économiques au détriment des techniques.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Mises à niveau fournisseurs pilotent la maintenance, délais induits.
- **C :** Portabilité réduite, violation de OCP et DIP.

### REFACTORING
- **Architecture multiniveau :** Séparer les couches pour isoler les détails de l'implémentation.
- **Abstractions :** Créer des interfaces pour ne pas dépendre de technos propriétaires.

---

## 10. STOVEPIPE SYSTEM
**Déf :** Intégration de sous-systèmes sans plan global, rendant chaque intégration unique et spéciale.

### CAUSES
- Manque d'abstraction. Interfaces uniques par système.
- Pas d'architecture centrale définie.

### SYMPTÔMES & CONSÉQUENCES
- **S :** Implémentation ne correspond pas à la documentation, complexité élevée.
- **C :** Maintenabilité et interopérabilité fortement diminuées.

### REFACTORING
- **Interface commune :** Mettre en place un service bus ou une API commune pour l'intégration.




## ANTIPATRON DE CONCEPTION (Design Smell)
**Déf :** Problèmes de conception au niveau des classes et objets (bas niveau). Rend le code difficile à lire, modifier ou tester.
**Mots clés :** Code smell, Spaghetti, classes trop grosses, Violation de principes SOLID, Manque de modularité.


# ANTIPATRONS DE CONCEPTION : ABSTRACTION

ABSTRACTION = Simplification des entités: Réduction et généralisation des composants pour les rendre plus simples, cohérents et réutilisables.


## 1. MANQUE D'ABSTRACTION (Missing Abstraction)
**Déf :** Utilisation de types primitifs ou de données brutes alors qu'une classe dédiée permettrait de regrouper la logique.
**Symptômes & Conséquences :**
- Violation du **SRP** (*Single Responsibility Principle*).
- Code répétitif et difficile à lire.
- Logique de validation éparpillée partout dans le code.
**Exemples :**
- Utiliser un `string` pour un numéro de téléphone au lieu d'une classe `Telephone` (qui gèrerait l'indicatif pays et la validation).
- Passer 5 variables (`rue`, `ville`, `cp`, etc.) au lieu d'un objet `Adresse`.
**Refactoring :** Extraire une classe (regrouper les champs liés dans un nouvel objet).

## 2. ABSTRACTION À MULTIFACETTES (Multifaceted Abstraction)
**Déf :** Une abstraction (classe ou interface) qui possède trop de responsabilités différentes.
**Symptômes & Conséquences :**
- Violation du **SRP**.
- Cohésion faible : l'abstraction n'a plus de sens clair.
- Difficile à réutiliser car elle en fait trop.
**Exemples :**
- Une interface `DatabaseManager` qui gère la connexion, les requêtes SQL, l'envoi de rapports par mail et l'archivage.
- Un `UserAccount` qui gère les infos de profil, le paiement et l'envoi de notifications SMS.
**Refactoring :** Extraire des classes ou des super-classes pour séparer chaque responsabilité.

## 3. ABSTRACTION DUPLIQUÉE (Duplicate Abstraction)
**Déf :** Existence de deux abstractions identiques ou presque (clonage), que ce soit par le nom ou par le code.
**Symptômes & Conséquences :**
- Maintenance doublée (si on change un bug, il faut le faire deux fois).
- Confusion pour les développeurs sur quelle classe utiliser.
- Risque d'incohérence si les deux versions finissent par diverger.
**Exemples :**
- Deux classes `Client` identiques situées dans deux dossiers (packages) différents par erreur.
- Deux classes de calcul de taxes (`CalculTVA_V1` et `CalculTVA_Final`) qui ont exactement la même implémentation.
**Refactoring :** Supprimer le doublon ou extraire le code commun dans une classe partagée/super-classe.


# ANTIPATRONS DE CONCEPTION : ENCAPSULATION

ENCAPSULATION = “Séparation des préoccupations” et “Masquage de l’information”

## 4. ENCAPSULATION INSUFFISANTE (Deficient Encapsulation)
**Déf :** Lorsqu'une abstraction expose ses détails internes (attributs) plus qu'il n'est nécessaire.
**Symptômes & Conséquences :**
- Sécurité et maintenabilité réduites (n'importe quelle partie du code peut modifier l'état interne).
- Couplage fort entre les classes.
**Causes :** Pensée procédurale dans un contexte objet, ou facilité pour les tests unitaires.
**Exemple :** Une classe `CompteBancaire` où l'attribut `solde` est en `public`, permettant de le modifier sans passer par les méthodes `deposer()` ou `retirer()`.
**Refactoring :** Encapsuler les données (passer en `private` ou `protected`) et fournir des méthodes d'accès contrôlées (getters/setters ou méthodes métier).

## 5. ENCAPSULATION INEXPLOITÉE (Unexploited Encapsulation)
**Déf :** Utilisation de vérifications de type explicites (`instanceof`, `if/else` sur les types) au lieu de profiter du polymorphisme.
**Symptômes & Conséquences :**
- Complexité augmentée par des structures de contrôle massives.
- Maintenabilité réduite : chaque nouveau sous-type demande de modifier tous les blocs `if/else`.
**Causes :** Pensée procédurale (on traite l'objet comme une structure de données plutôt que comme une entité intelligente).
**Exemple :** - **Mauvais :** Une boucle qui vérifie `if (animal instanceof Chien) { aboyer(); } else if (animal instanceof Chat) { miauler(); }`.
- **Bon (Polymorphisme) :** On appelle simplement `animal.emettreSon()` et chaque sous-classe gère sa propre implémentation.
**Refactoring :** Remplacer les vérifications de type par le polymorphisme (méthodes virtuelles/abstraites).



# ANTIPATRONS DE CONCEPTION : MODULARITÉ

# CONCEPT : MODULARITÉ
**Déf :** La capacité d'un système à être divisé en unités distinctes (modules) qui peuvent être créées et modifiées indépendamment. 
**Objectif :** Atteindre un **faible couplage** (dépendances minimales entre modules) et une **forte cohésion** (chaque module fait une seule chose de façon logique).

## 6. MODULARISATION BRISÉE (Broken Modularity)
**Déf :** Dispersion de données ou méthodes qui devraient être ensemble (similarité sémantique) à travers plusieurs abstractions.
**Symptômes & Conséquences :**
- Couplage fort et cohésion faible.
- "Effet domino" : une modification à un endroit casse tout le reste.
- Maintenabilité et performances réduites.
**Exemple :** Les données d'un `Utilisateur` sont dans une classe, mais ses méthodes de validation sont dans une autre, et ses préférences dans une troisième sans lien hiérarchique.
**Refactoring :** Regrouper les membres liés dans la même abstraction (encapsulation).

## 7. MODULARISATION INSUFFISANTE (Insufficient Modularity)
**Déf :** Une abstraction est trop vaste ("God Object") ou trop complexe, centralisant trop de membres publics ou de responsabilités.
**Symptômes & Conséquences :**
- Violation flagrante du **SRP** (Single Responsibility Principle).
- Difficulté à tester et à réutiliser une partie du code seulement.
**Exemple :** Une interface `IAllServices` qui force chaque classe à implémenter le logging, la base de données et l'authentification.
**Refactoring :** Extraire des méthodes, des classes ou des interfaces plus petites et spécialisées.

## 8. MODULARISATION CYCLIQUEMENT DÉPENDANTE (Cyclical Dependency)
**Déf :** Deux abstractions (ou plus) dépendent l'une de l'autre de manière directe ou indirecte.
**Symptômes & Conséquences :**
- Impossibilité de réutiliser une classe sans l'autre.
- Difficulté de compréhension (boucle infinie logique).
**Causes :** Mauvaise conception de l'abstraction, passage de pointeurs/références mal maîtrisé.
**Refactoring :** 1. Casser la boucle en extrayant le code commun dans une troisième classe.
2. Utiliser l'inversion de dépendance (interfaces).

---

# SOLUTIONS GÉNÉRALES DE MODULARITÉ (Page 29)

1.  **Déplacement (Move Method/Field) :** Relocaliser une méthode ou un attribut dans la classe où il est le plus utilisé pour améliorer la cohésion.
2.  **Extraction (Extract Class/Interface) :** Diviser une classe trop grosse en créant une nouvelle entité pour une responsabilité spécifique.
3.  **Inversion (Dependency Inversion) :** Faire dépendre les modules de haut niveau d'abstractions (interfaces) plutôt que de classes concrètes pour réduire le couplage.


## 1. Hiérarchie non factorisée
**Définition :** Il existe une duplication de code entre les classes dérivées (sœurs) ou entre les classes dérivées et la classe de base.


## 1. Hiérarchie non factorisée
**Définition :** Il existe une duplication de code entre les classes dérivées (sœurs) ou entre les classes dérivées et la classe de base.

* **Symptôme :** Maintenabilité réduite (si on change une logique, il faut la changer à trois endroits).
* **Cause :** Copier-coller rapide lors de la création de nouvelles classes.
* **Exemple :**
    * Classes : `Voiture`, `Moto`, `Camion`.
    * Problème : Les trois classes ont exactement le même code pour la méthode `calculerTaxe()`.
* **Refactoring :**
    * **Extraire une super-classe :** Créer une classe mère commune si elle n'existe pas.
    * **Remonter les méthodes/attributs (Pull up) :** Déplacer le code dupliqué des classes filles vers la classe mère.

## 2. Hiérarchie cyclique
**Définition :** Une classe de base possède une association directe (dépendance) avec une ou plusieurs de ses classes dérivées.

* **Symptôme :** Couplage très fort. Impossible de réutiliser la classe mère sans emmener toutes les classes filles avec elle.
* **Cause :** Mauvaise conception de l'héritage. La classe mère essaie de gérer des cas spécifiques qui appartiennent aux enfants.
* **Exemple (Le Garage et ses Clés) :**
    * La classe `Vehicule` (Mère) contient une méthode qui appelle spécifiquement `ClesVoiture` ou `ClesMoto` pour démarrer.
* **Refactoring :**
    * **Inversion de dépendance :** Utiliser une **Interface**. La classe mère dépend d'une interface, et les filles implémentent cette interface.
    * **Patron Stratégie (Strategy Pattern) :** Sortir la logique spécifique dans des classes à part pour rendre le comportement interchangeable.
    * **Imbriquer des classes :** Si une classe fille est minuscule et n'existe que pour la mère, elle peut parfois être intégrée.

## 3. Hiérarchie brisée
**Définition :** L'héritage est utilisé uniquement pour récupérer du code existant (réutilisation technique) et non parce qu'il existe un lien logique "EST UN" entre les classes.

* **Symptôme :** La classe fille hérite de méthodes dont elle n'a pas besoin ou qui n'ont pas de sens pour elle.
* **Exemple (Stack et Vector) :**
    * `Stack` (Pile) hérite de `Vector`.
    * **Problème :** Un `Vector` permet d'insérer un élément n'importe où (index 2, 5, etc.). Un `Stack` ne devrait permettre que `push` (ajouter en haut) et `pop` (retirer du haut). En héritant de `Vector`, le `Stack` "casse" sa propre logique.
* **Refactoring :**
    * **Remplacer l'héritage par la délégation :** La classe `Stack` ne doit plus hériter de `Vector`. Elle doit contenir un objet `Vector` privé à l'intérieur d'elle.
    * **Inverser la relation :** Repenser si la hiérarchie ne devrait pas être dans l'autre sens ou si une interface commune est préférable.

    # 📝 Aide-Mémoire Complet : Qualité Logicielle & Refactoring

## I. Comparaison : Anti-patrons de Code vs. Conception

| Caractéristique | **Anti-patrons de Code (Code Smells)** | **Anti-patrons de Conception** |
| :--- | :--- | :--- |
| **Niveau d'impact** | Local (méthode, classe). | Structurel (système, architecture). |
| **Nature** | Symptômes visibles, "odeurs" de code. | Causes racines, défauts de modularité. |
| **Exemples types** | Méthode longue, Code dupliqué, Feature Envy. | Blob (Classe Dieu), Spaghetti Code, Marteau d'Or. |
| **Complexité** | Souvent facile à repérer et à corriger. | Nécessite un remaniement architectural majeur. |
| **Abstraction** | Manque de propreté technique. | Mauvaise utilisation des principes (SOLID, etc.). |

---

## II. Catalogue des Code Smells & Refactoring

### 1. Code Dupliqué (Duplicated Code)
* **Définition :** La même structure de code se retrouve à plus d'un endroit. C'est l'ennemi numéro 1 de la maintenance.
* **Refactoring :** *Extract Method* (Extraire la méthode) ou *Pull Up Field/Method* (Remonter vers la classe mère).

```java
// AVANT : Logique de formatage répétée
void imprimerFacture() {
    System.out.println("--- " + titre.toUpperCase() + " ---");
}
void imprimerRecu() {
    System.out.println("--- " + titre.toUpperCase() + " ---");
}

// APRÈS : Une seule source de vérité
void imprimerEntete() {
    System.out.println("--- " + titre.toUpperCase() + " ---");
}
```

### 2. Méthode Longue (Long Method)
* **Définition :** Une méthode qui essaie de trop en faire (souvent > 20-30 lignes). Plus elle est longue, plus elle est difficile à comprendre et à tester.
* **Refactoring :** *Extract Method*. Cherche les commentaires internes; ils indiquent souvent un bloc qui mérite sa propre méthode.

### 3. Longue Liste de Paramètres (Long Parameter List)
* **Définition :** Une méthode qui prend plus de 3 ou 4 paramètres. Difficile à lire et risque d'erreur dans l'ordre des arguments.
* **Refactoring :** *Introduce Parameter Object* (Introduire un objet de paramètres).

```java
// AVANT
void creerUtilisateur(String nom, String prenom, String rue, String ville, String cp, String pays) { ... }

// APRÈS
void creerUtilisateur(String nom, String prenom, Adresse adresse) { ... }
```

### 4. Feature Envy (Envie de fonctionnalités)
* **Définition :** Une méthode qui utilise plus de membres d'une autre classe que de la classe à laquelle elle appartient.
* **Refactoring :** *Move Method* (Déplacer la méthode) vers la classe la plus utilisée.

```java
// AVANT (La méthode calculerRemise utilise tout de 'Produit')
class Commande {
    public double calculerRemise(Produit p) {
        return p.getPrixBase() * p.getFacteurTaxe() * 0.10;
    }
}

// APRÈS (La logique est déplacée dans Produit)
class Produit {
    private double prixBase;
    private double facteurTaxe;
    public double calculerRemise() {
        return this.prixBase * this.facteurTaxe * 0.10;
    }
}
```

### 5. Switch Statements (Énoncés conditionnels complexes)
* **Définition :** Présence de `switch` ou de `if/else` massifs basés sur des types de données.
* **Refactoring :** Remplacer les vérifications de type par du **Polymorphisme** ou le patron **Stratégie / État**.

```java
// AVANT : Vérifications de type manuelles
void emettreSon(String typeAnimal) {
    if (typeAnimal.equals("Chien")) System.out.println("Woof");
    else if (typeAnimal.equals("Chat")) System.out.println("Meow");
}

// APRÈS : Utilisation du Polymorphisme
abstract class Animal { abstract void crier(); }
class Chien extends Animal { void crier() { System.out.println("Woof"); } }
class Chat extends Animal { void crier() { System.out.println("Meow"); } }
```

### 6. Message Chain (Chaîne de messages)
* **Définition :** Un client demande un objet à un autre, qui en demande un autre en cascade (`a.getB().getC().doSomething()`).
* **Refactoring :** *Hide Delegate* (Cacher la délégation).

```java
// AVANT : Couplage fort avec toute la chaîne
client.getDepartement().getGestionnaire().getNom();

// APRÈS : La classe intermédiaire cache la complexité
client.getNomGestionnaire();
```

### 7. Inappropriate Intimacy (Intimité inappropriée)
* **Définition :** Une classe accède de manière excessive aux membres privés ou détails internes d'une autre classe.
* **Refactoring :** Déplacer des méthodes, extraire des classes ou cacher les délégations.

```java
// AVANT : Voiture manipule directement les internes du Moteur
class Voiture {
    void accelerer(Moteur m) {
        m.pressionHuile += 5;
        m.temperature += 10;
    }
}

// APRÈS : Le moteur gère sa propre logique interne
class Moteur {
    private int pressionHuile;
    private double temperature;
    public void monterEnRegime() {
        this.pressionHuile += 5;
        this.temperature += 10;
    }
}
```

### 8. Changement Divergent (Divergent Change)
* **Définition :** Tu dois modifier une seule classe pour plusieurs raisons différentes (ex: changer la DB *et* changer l'UI dans le même fichier).
* **Refactoring :** *Extract Class*. Sépare les responsabilités (Principe de Responsabilité Unique - SRP).

### 9. Chirurgie au Shotgun (Shotgun Surgery)
* **Définition :** L'inverse du divergent : pour faire une seule modification, tu dois modifier 10 classes différentes.
* **Refactoring :** *Move Method* ou *Move Field* pour regrouper la logique dispersée.

---

## III. Tableau Comparatif : Divergent Change vs Shotgun Surgery

| Odeur | Symptôme | Relation | Solution |
| :--- | :--- | :--- | :--- |
| **Divergent Change** | 1 Classe → Plusieurs changements différents. | 1 à N | Extraire des classes. |
| **Shotgun Surgery** | 1 Changement → Plusieurs classes impactées. | N à 1 | Regrouper dans une seule classe. |

> **Note Examen :** Si on te dit : *"Je veux changer le format de ma base de données et je dois toucher à 12 fichiers différents"*, la réponse est **Shotgun Surgery**.

---

## IV. Métriques & Qualité (Dernières Slides)

### 1. Complexité Cyclomatique ($V(G)$)
* **Calcul :** $V(G) = \text{Nombre de décisions} + 1$.
* **Interprétation :** Un score > 10 indique une méthode trop complexe qui nécessite un refactoring.

### 2. Métriques de Produit vs Processus
* **Produit :** Mesure le logiciel (Lignes de code, complexité, couplage CBO, cohésion LCOM).
* **Processus :** Mesure le cycle de développement (Nombre de bugs corrigés, temps par tâche).

### 3. Points Critiques
* **Cohésion :** Force du lien interne. On veut une cohésion **forte**.
* **Couplage :** Interdépendance entre les classes. On veut un couplage **faible**.
* **Qualité :** Les métriques servent à prédire la maintenabilité et à identifier les zones "à risque".