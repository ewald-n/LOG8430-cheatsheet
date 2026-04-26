# Cheat Sheet : LOG8430 - Blockchain

## 1. Concepts Fondamentaux et Définition
[cite_start]La **Blockchain** est un registre numérique distribué, immuable et basé sur le consensus, utilisant un réseau Peer-to-Peer (P2P) pour sécuriser des données sans autorité centrale[cite: 2033, 2040].

### Propriétés Clés
* [cite_start]**Immuabilité** : Les données sont permanentes et inaltérables ; on ne peut qu'actualiser l'état du système via de nouvelles transactions[cite: 2035, 2047].
* [cite_start]**Transparence** : Registre public où toutes les données sont visibles par les participants[cite: 2039, 2069].
* [cite_start]**Décentralisation** : Copies du registre distribuées sur le réseau ; pas de point de défaillance unique[cite: 2039].
* [cite_start]**Consensus** : Mécanisme de vérification de la confiance pour valider l'état du système[cite: 2036].

---

## 2. Architecture et Fonctionnement

### Structure des Blocs et Transactions
* [cite_start]**Bloc** : Contient plusieurs transactions validées cryptographiquement[cite: 2099].
* [cite_start]**Liaison** : Chaque bloc contient le **Hash** du bloc précédent (chaînage), rendant toute modification rétroactive virtuellement impossible sans recalculer toute la chaîne[cite: 2074, 2228, 2460].
* **Processus d'ajout** : 
    1. [cite_start]Demande/Authentification d'une transaction[cite: 2079].
    2. [cite_start]Création d'un bloc de transaction[cite: 2088].
    3. [cite_start]Diffusion à chaque nœud du réseau[cite: 2087].
    4. [cite_start]Validation par les nœuds (Consensus)[cite: 2093].
    5. [cite_start]Ajout à la blockchain existante et distribution de la mise à jour[cite: 2092, 2084].

### Couches Fonctionnelles (Architecture Bitcoin)
| Couche | Description | Technologies/Exemples |
| :--- | :--- | :--- |
| **Application** | Services pour l'utilisateur final | [cite_start]Portefeuilles, DApps [cite: 2535] |
| **Consensus** | Règles de validation et accord | [cite_start]PoW, PoS [cite: 2535, 2539] |
| **Réseau** | Interactions entre nœuds pairs | [cite_start]Protocole P2P [cite: 2535, 2541] |
| **Données** | Persistance et sécurité des messages | [cite_start]Transactions, Hashes, Signatures [cite: 2535, 2542] |
| **Matérielle** | Infrastructure physique/virtuelle | [cite_start]Serveurs, VM, Nœuds [cite: 2535, 2544] |

---

## 3. Le Problème des Généraux Byzantins (BFT)
[cite_start]Problème de théorie des jeux : Comment des parties dispersées peuvent-elles atteindre un consensus sans autorité centrale, sachant que certains acteurs peuvent être des traîtres[cite: 2121, 2124]?

### Paramètres Critiques pour l'Examen
* [cite_start]**Condition de Victoire** : Nécessite que $2/3$ des généraux attaquent simultanément[cite: 2115].
* **Seuil de Tolérance ($3f+1$)** :
    * [cite_start]$f$ = nombre de traîtres[cite: 2163].
    * [cite_start]**Nombre minimum de généraux** nécessaires pour garantir le consensus : $3f + 1$[cite: 2164].
    * [cite_start]*Exemple* : Pour tolérer 1 traître, il faut au moins 4 généraux ($3(1)+1 = 4$)[cite: 2165].

---

## 4. Mécanismes de Consensus : PoW vs PoS

### Proof-of-Work (PoW) - "Minage"
* [cite_start]**Principe** : Résoudre une énigme computationnelle complexe (SHA-256)[cite: 2210, 2234].
* [cite_start]**Fonctionnement** : Trouver un **nonce** tel que le Hash du bloc soit $\leq$ à une valeur cible (Target)[cite: 2217, 2238].
* [cite_start]**Avantage** : Sécurité robuste, première implémentation réelle de la tolérance aux pannes byzantines à grande échelle[cite: 2269, 2357].
* [cite_start]**Inconvénients** : Énorme consommation électrique, faible scalabilité (ex: 7 TPS pour Bitcoin)[cite: 2267].

### Proof-of-Stake (PoS) - "Forgeage"
* [cite_start]**Principe** : Sélection des validateurs selon le montant de jetons "stakés" (verrouillés en garantie)[cite: 2318].
* [cite_start]**Avantages** : Efficacité énergétique, meilleure scalabilité[cite: 2331, 2359].
* [cite_start]**Vulnérabilité (Nothing-at-stake)** : Les validateurs peuvent voter sur plusieurs forks simultanément sans coût, affaiblissant la sécurité[cite: 2336, 2341].

### Tableau Comparatif détaillé
| Caractéristique | Proof-of-Work (PoW) | Proof-of-Stake (PoS) |
| :--- | :--- | :--- |
| **Acteur clé** | [cite_start]Mineurs [cite: 2357] | [cite_start]Validateurs [cite: 2357] |
| **Ressource** | [cite_start]Équipement et Énergie [cite: 2357] | [cite_start]Pièces/Tokens détenus [cite: 2357] |
| **Sécurité** | [cite_start]Coût d'attaque prohibitif [cite: 2357] | [cite_start]Contrôle par la communauté [cite: 2357] |
| **Récompense** | [cite_start]Nouveaux blocs + Frais [cite: 2359] | [cite_start]Frais de transaction [cite: 2359] |
| **Vulnérabilité** | [cite_start]Attaque 51% (Hash rate) [cite: 2288] | [cite_start]Problème "Nothing-at-stake" [cite: 2359] |

---

## 5. Le Trilemme de la Blockchain
[cite_start]Un système distribué peine à satisfaire simultanément ces trois propriétés[cite: 2431]:
1.  [cite_start]**Sécurité** : Protection contre les attaques et intégrité[cite: 2405].
2.  [cite_start]**Décentralisation** : Absence d'autorité centrale[cite: 2415].
3.  [cite_start]**Scalabilité** : Capacité à traiter un grand volume de transactions[cite: 2422].
[cite_start]*Note : Augmenter l'une de ces propriétés affaiblit généralement l'une des deux autres[cite: 2432].*

---

## 6. Comparaison des Technologies (Bitcoin, Ethereum, Hyperledger)

| Critère | Bitcoin | Ethereum | Hyperledger Fabric |
| :--- | :--- | :--- | :--- |
| **Type** | [cite_start]Publique (Ouverte) [cite: 2518] | [cite_start]Publique [cite: 2518] | [cite_start]Privée (Permissionnée) [cite: 2520, 2618] |
| **Consensus** | [cite_start]PoW [cite: 2531] | [cite_start]PoS (auparavant PoW) [cite: 2549] | [cite_start]PBFT / RAFT [cite: 2711] |
| **Langage** | [cite_start]Script (limité) [cite: 2559] | [cite_start]Solidity (Turing complet) [cite: 2559] | [cite_start]Go, Java, JS [cite: 2635] |
| **Vitesse** | [cite_start]~7 TPS [cite: 2711] | [cite_start]~15-20 TPS [cite: 2711] | >[cite_start]3500 TPS [cite: 2711] |
| **Usage** | [cite_start]Monétaire (FIAT alternatif) [cite: 2529] | [cite_start]Usage général (EVM) [cite: 2553] | [cite_start]Affaires / B2B (ex: Walmart) [cite: 2633, 2713] |

---

## 7. Smart Contracts (Contrats Intelligents)
[cite_start]Morceau de code et de données déployé sur une blockchain qui applique automatiquement les termes d'un accord[cite: 2724, 2727].

### Caractéristiques Techniques
* [cite_start]**Déterministe** : Même entrée = même résultat pour tous les participants (cohérence du réseau)[cite: 2763, 2765].
* [cite_start]**Immuable** : Une fois déployé, ne peut être ni modifié ni supprimé[cite: 2767].
* [cite_start]**Vérifiable** : Possède une adresse unique sur la blockchain[cite: 2776].
* [cite_start]**Gas (Ethereum)** : Chaque instruction a un coût prédéterminé pour limiter l'utilisation des ressources[cite: 2562].

### Cycle d'Exécution
1.  [cite_start]**Contrat prédéfini** : Termes codés et immuables[cite: 2744].
2.  [cite_start]**Événement** : Déclencheur (ex: date, réception de données)[cite: 2748].
3.  [cite_start]**Exécution** : Transfert automatique de valeur[cite: 2751].
4.  [cite_start]**Règlement** : Paiement instantané et efficace[cite: 2756].

---

## 8. Sécurité et Attaques

### Attaque 51% (PoW)
* [cite_start]**Définition** : Un groupe de mineurs contrôle >50% de la puissance de hachage du réseau[cite: 2290].
* [cite_start]**Capacités de l'attaquant** : Double dépense (effacer une transaction), bloquer des transactions, réordonner les blocs récents[cite: 2297, 2299].
* [cite_start]**Limites** : Ne peut pas créer de nouvelles pièces, voler des pièces existantes ou altérer les très vieux blocs[cite: 2299].

### Signature Numérique
* [cite_start]**Expéditeur** : Hache la transaction + chiffre avec sa **clé privée**[cite: 2484].
* **Vérification** : Les nœuds utilisent la **clé publique** de l'expéditeur. [cite_start]Si le hash correspond, l'intégrité et l'identité sont prouvées[cite: 2501, 2506].