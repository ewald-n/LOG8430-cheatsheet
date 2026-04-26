# LOG8430 - AIDE-MÉMOIRE : PROGRAMMATION ORIENTÉE ASPECT (AOP)

# I. FONDAMENTAUX ET PARADIGME

## DÉFINITIONS CLÉS
* [cite_start]**AOP (Aspect-Oriented Programming) :** Paradigme de programmation visant à modéliser les fonctionnalités transversales sans affecter les classes du domaine[cite: 1958, 2083].
* [cite_start]**Fonctionnalité Transversale (Cross-cutting Concern - CCC) :** Logique qui s'éparpille dans plusieurs modules ou classes (ex: sécurité, logging)[cite: 2071, 2075].
* [cite_start]**Niveau d'abstraction :** L'AOP est plus abstrait que le paradigme Orienté Objet (OO), se situant au-dessus dans la hiérarchie des langages[cite: 2051, 2053].

## LES PROBLÈMES DE L'OO (POURQUOI L'AOP ?)
[cite_start]L'approche OO classique pour les CCC mène à[cite: 2070]:
* [cite_start]**Éparpillement (Code Scattering) :** Une même fonctionnalité est copiée dans plusieurs modules[cite: 2072].
* [cite_start]**Confusion (Code Tangling) :** Une classe contient plusieurs logiques mélangées (métier + technique), réduisant sa cohésion[cite: 2073, 2117].
* [cite_start]**Duplication (Code Cloning) :** Inévitable si on doit invoquer manuellement un service dans chaque fonction[cite: 2074, 2448].
* [cite_start]**Résultat :** Modules moins indépendants et réutilisabilité diminuée[cite: 2082].

---

# II. ÉLÉMENTS DU MODÈLE AOP

[cite_start]L'AOP introduit trois concepts fondamentaux pour isoler la logique[cite: 2212]:

| Élément | Définition | Analogie / Rôle |
| :--- | :--- | :--- |
| **Join Point** | [cite_start]Point précis dans le déroulement du programme (exécution d'une méthode, accès à un attribut)[cite: 2232]. | "Le moment où..." |
| **Pointcut** | [cite_start]Expression (motif) qui capture et identifie un ou plusieurs *Join Points* où l'aspect doit agir[cite: 2215, 2232]. | "La cible" |
| **Advice** | [cite_start]Code (méthode) qui implémente la tâche commune à exécuter lors de l'activation du Pointcut[cite: 2214]. | "L'action à faire" |
| **Aspect** | [cite_start]Module regroupant les Pointcuts et les Advices pour une fonctionnalité donnée[cite: 2124, 2216]. | "L'unité modulaire" |

## LE PROCESSUS DE TISSAGE (WEAVING)
[cite_start]Le **Code Weaving** est le processus convertissant les aspects en code compilable par un compilateur standard[cite: 2091].
* [cite_start]**Inputs :** Base Code (OO) + Aspect Code[cite: 2092, 2094].
* [cite_start]**Output :** Modified Base Code[cite: 2095].
* [cite_start]**Weaver :** Outil (ex: compilateur `ajc` pour AspectJ) qui injecte l'aspect dans le code source ou le bytecode[cite: 2105].

---

# III. TYPES DE CROSSCUTTING (FONCTIONNEMENT)

## 1. CROSSCUTTING DYNAMIQUE
[cite_start]Intercepte des événements lors de l'exécution du programme[cite: 2138, 2139].
* [cite_start]**Interceptions communes :** Avant/Après un appel, lors d'une exception[cite: 2141, 2142].
* **Types d'Advices :**
    * [cite_start]`before()` : S'exécute juste avant le join point[cite: 2237].
    * [cite_start]`after()` : S'exécute juste après le join point[cite: 2238].
    * [cite_start]`around()` : Enveloppe le join point; peut modifier les arguments ou empêcher l'exécution[cite: 2239].

## 2. CROSSCUTTING STATIQUE (INTRODUCTION)
[cite_start]Modifie la structure statique des classes au moment de la compilation[cite: 2145, 2146].
* [cite_start]**Ajout de membres :** Introduire de nouveaux attributs ou méthodes dans une classe existante via un aspect[cite: 2147, 2242].
* [cite_start]**Modification de hiérarchie :** Forcer une classe à implémenter une interface ou à dériver d'une autre classe (`declare parents`)[cite: 2148, 2261].
* [cite_start]**Contrôle de compilation :** Générer des erreurs ou avertissements personnalisés basés sur des motifs de code (`declare error` / `declare warning`)[cite: 2149, 2276].

---

# IV. DOMAINES D'APPLICATION ET CAS D'USAGE

* [cite_start]**Gestion technique :** Authentification, Logging, Audit, Mise en cache, Performance [cite: 2126-2131].
* [cite_start]**Validation :** Utiliser des annotations (ex: `@Required`) interceptées par un aspect pour valider les paramètres avant l'exécution [cite: 2496-2498].
* [cite_start]**Tests Unitaires :** Faciliter le **Mocking** en interceptant des méthodes via `@Mock` pour retourner des données factices sans modifier le code métier [cite: 2512-2515].
* [cite_start]**Conformité Architecturale :** Empêcher les appels interdits entre couches (ex: la logique métier ne peut pas appeler l'UI) en déclarant une `declare error` à la compilation[cite: 2546, 2601].
* [cite_start]**Design Patterns :** L'AOP améliore l'implémentation de 17/23 patrons du GoF (meilleure localité et réutilisation)[cite: 2532, 2534, 2535].

---

# V. ASPECTJ : RÉSUMÉ SYNTAXIQUE ET RÈGLES

## COMPARAISON ASPECT VS CLASSE
| Caractéristique | Aspect | Classe |
| :--- | :--- | :--- |
| **Attributs/Méthodes** | [cite_start]Oui [cite: 2197] | Oui |
| **Abstrait** | [cite_start]Oui [cite: 2199] | Oui |
| **Instanciation** | [cite_start]**Non** (géré par le runtime) [cite: 2207] | Oui |
| **Privilèges** | [cite_start]Peut accéder aux membres `private` (`privileged aspect`) [cite: 2209] | Non (encapsulation stricte) |
| **Héritage** | [cite_start]Ne peut pas dériver d'un aspect **concret** [cite: 2208] | Peut dériver d'une classe concrète |

## EXEMPLE DE CODE CRITIQUE (TRACAGE)
```java
public aspect AspectTrace {
    // Capture tout sauf l'aspect lui-même
    pointcut pointsATracer(): !within(AspectTrace); 

    before(): pointsATracer() {
        System.out.println("Entrée dans : " + thisJoinPoint);
    }
}