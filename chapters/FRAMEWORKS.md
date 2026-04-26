# AIDE-MÉMOIRE : ARCHITECTURE LOGICIELLE (MAJ Étude de Cas)

### 1. CADRICIELS (FRAMEWORKS)
- **Définition :** Architecture semi-implémentée, générique et agnostique. Squelette réutilisable.
- **Analogie :** Centre commercial (Structure fixe + espaces vides).
- **Composants :** - **Frozen Spots :** Modules concrets (fondations). Immuables.
    - **Hot Spots :** Modules abstraits (emplacements). À étendre par le dév.
- **Inversion de Contrôle (IoC) / Principe Hollywood :** "Ne nous appelez pas, on vous appellera". Le cadre dicte le flux.
- **Propriétés & Principes :**
    - **DIP / OCP :** Ouvert à l'extension, fermé à la modification.
    - **Standardisation :** Structure et flux uniformes.
- **Études de cas :**
    - **AngularJS (Web JS) :** Architecture **MV***. Automatise le *data-binding*. Très testable mais complexe.
    - **Django (Python) :** Architecture **MVT** (Model-View-Template). Focus sur la sécurité et le développement rapide (DRY).

---

### 2. PLUGICIELS (PLUGINS)
- **Définition :** Composant qui ajoute une fonction à un système hôte sans le modifier (**OCP**).
- **Architecture :** **Microkernel** (Noyau minimal). Le système de base est **atomique** (fonctionne seul).
- **Principes clés :**
    - **SRP (Single Responsibility) :** C'est le principe le plus pertinent. Une mission unique.
    - **Inversion de Dépendance :** Le système définit l'interface, le plugin l'implémente.
- **Désavantages :** Maintenabilité réduite (fragilité aux mises à jour du système) et conflits possibles.
- **Étude de cas :**
    - **Eclipse (IDE) :** Noyau minimal où tout est plugin. Priorise la **rétrocompatibilité** (supporter les vieilles versions), ce qui complexifie la maintenance du cœur.

---

### 3. ÉCOSYSTÈMES LOGICIELS & CHANGEMENTS DISRUPTIFS
- **Définition :** Collection de modules partageant un socle commun (Langage, Plateforme).
- **Propriétés :** Interdépendance, Maintenabilité (qualité variable car n'importe qui contribue), Effet de réseau.
- **Étude sur la gestion du changement (Breaking Changes) :**
    - **Le dilemme du coût :** Un petit changement chez le développeur (mainteneur) peut causer une charge de travail massive pour des milliers d'utilisateurs (développeurs tiers).
    - **Stratégies de négociation :**
        1. **Mainteneur assume le coût :** Limite les changements pour protéger les utilisateurs (Eclipse).
        2. **Utilisateur assume le coût :** Doit s'adapter rapidement aux ruptures (Node.js).
        3. **Coût partagé :** Collaboration via des volontaires et dépôts centralisés (R/CRAN).

- **Valeurs des communautés spécifiques :**
    - **Eclipse :** Priorité absolue à la **stabilité**. Facilite un accès rapide aux outils pour l'utilisateur final.
    - **R / CRAN :** Priorité au **partage et à la validation**. Dépôt distribué de paquets statistiques où la responsabilité est partagée.
    - **Node.js :** Priorité à la **vitesse de développement**. Écosystème géré par **npm** (très dynamique, changements fréquents).

- **Autre cas :**
    - **Android :** Hybride (OS + Cadriciel + Écosystème). Architecture **MVVM**. Modulaire et sécuritaire.

---

### COMPARISON GLOBALE (EXAMEN)

| Caractéristique | Cadriciel (Framework) | Plugiciel (Plugin) | Écosystème |
| :--- | :--- | :--- | :--- |
| **Rôle** | Squelette / Structure | Extension de fonction | Environnement global |
| **Principe Roi** | **IoC** (Inversion de Contrôle) | **SRP** (Responsabilité Unique) | **Effet de réseau** |
| **Indépendance** | L'app ne tourne pas sans lui | Le système hôte tourne sans lui | Modules interdépendants |
| **Gestion Changement** | Rigide (Frozen Spots) | Fragile (Microkernel) | Stratégies variables (Étude) |
| **Focus** | Productivité du Développeur | Expérience Utilisateur | Communauté & Marché |
| **Exemple** | Django, Angular | AdBlock, Plugin Eclipse | Android, npm, CRAN |