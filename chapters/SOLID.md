# SOLID – Principes de Conception

## Pourquoi SOLID ?
Réduction dette technique · maintenabilité accrue · testabilité. **Corriger :** Refactoring (remonter/descendre méthodes/classes · modifier hiérarchie).

---

## S – Single Responsibility (SRP)
**Principe :** 1 classe = 1 seule raison de changer (1 mission).

**Truc :** Si trop de choses → modifier risque tout casser (effet de bord).

**Impact :** Code + facile à comprendre, modifier, tester (unit tests simples).

**Cible : Classe (cohésion interne).**

---

## O – Open/Closed (OCP)
**Principe :** Ouvert extension, fermé modification.

**Analogie :** Legos (ajouter pièces par-dessus) vs fondre plastique existant.

**Méthode :** Héritage/interfaces pour ajouter comportement sans toucher code source validé.

---

## L – Liskov Substitution (LSP)
**Principe :** Enfant (sous-type) remplace parent (type base) sans planter/changer logique.

**Test :** Véhicule → Voiture, `.rouler()` se comporte comme attendu.

**Règle :** Jamais forcer sous-classe à implémenter méthode inutile (ex: Autruche hérite Oiseau mais ne peut `.voler()`).

---

## I – Interface Segregation (ISP)
**Principe :** Plusieurs petites interfaces ciblées > 1 interface géante.

**Règle :** Classe ne doit PAS implémenter méthodes inutilisées.

**Focus :** Découper pour le client (consommateur interface).

**Cible : Interface (réduire couplage).** ⭐ **QCM ★**

---

## D – Dependency Inversion (DIP)
**Principe :** Dépendre abstractions (Interfaces/Classes abstraites), PAS implémentations concrètes.

**Analogie :** "Boîte Noire" (on se fiche du comment, tant qu'on sait ce qui sort = contrat).

**But :** Découpler modules haut niveau des détails techniques (changer DB ne casse pas logique affaires).

---

## ⚠ Piège Examen
**ISP ≠ SRP**
- **ISP** = segmenter INTERFACES pour clients
- **SRP** = 1 classe = 1 responsabilité (cohésion)
