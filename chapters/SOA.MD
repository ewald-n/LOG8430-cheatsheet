# LOG8430 - AIDE-MÉMOIRE : ARCHITECTURES ORIENTÉES SERVICES (SOA)

# 1. FONDEMENTS ET DÉFINITIONS

## SOA (Service Oriented Architecture)
[cite_start]**Déf :** Style architectural permettant aux systèmes de collaborer de manière harmonieuse en structurant l'univers en **services**[cite: 1757, 1760]. [cite_start]Il repose sur la convergence de trois forces : la **modularité**, l' **interopérabilité** et l'infrastructure du **Web**[cite: 1751, 1752, 1756].

## LE SERVICE WEB
[cite_start]**Déf :** Composante logicielle atomique et publique qui expose une interface pour fournir une fonctionnalité ou des données[cite: 1898, 1901, 1902].
* [cite_start]**Indépendant :** N'exige aucun autre logiciel pour fonctionner[cite: 1899].
* [cite_start]**Atomique :** Produit des résultats complets[cite: 1900].
* [cite_start]**Boîte noire :** L'implémentation interne est cachée aux clients[cite: 1903].

---

# 2. CARACTÉRISTIQUES CLÉS (LES 8 PILIERS)

| Caractéristique | Description | Avantages | Défis / Limites |
| :--- | :--- | :--- | :--- |
| **1. Couplage Faible** | [cite_start]Dépendances minimales entre services[cite: 1794]. | [cite_start]Scalabilité et flexibilité accrues[cite: 1795]. | [cite_start]Tests et débogage plus complexes[cite: 1796]. |
| **2. Interfaces Abstraites** | [cite_start]Seule l'interface est exposée ; logique cachée[cite: 1797]. | [cite_start]Portabilité ; indépendance des plateformes[cite: 1798]. | [cite_start]Réduit la testabilité[cite: 1799]. |
| **3. Interopérabilité** | [cite_start]Communication entre langages/OS via protocoles standards[cite: 1804]. | [cite_start]Interaction facile de systèmes hétérogènes[cite: 1805]. | [cite_start]Gestion complexe des transformations de données[cite: 1805]. |
| **4. Réutilisabilité** | [cite_start]Composants modulaires pour divers contextes[cite: 1806]. | [cite_start]Réduit la duplication ; accélère le dev[cite: 1807]. | [cite_start]Exige une conception initiale très soignée[cite: 1807]. |
| **5. Découvrabilité** | [cite_start]Identifiables via registre ou APIs[cite: 1812]. | [cite_start]Encourage la réutilisation[cite: 1813]. | [cite_start]Gestion lourde des métadonnées[cite: 1814]. |
| **6. Contrats Standardisés** | [cite_start]Comportement garanti par des contrats (ex: WSDL)[cite: 1815]. | [cite_start]Améliore la prévisibilité[cite: 1816]. | [cite_start]Charge de gestion des versions de contrats[cite: 1816]. |
| **7. Autonomie** | [cite_start]Chaque service gère sa propre logique et ses données[cite: 1820]. | [cite_start]Tolérance aux pannes améliorée[cite: 1822]. | [cite_start]Complexité de coordination accrue[cite: 1823]. |
| **8. Absence d'État** | [cite_start]Aucun contexte client n'est stocké entre les requêtes[cite: 1824]. | [cite_start]Scalabilité maximale[cite: 1826]. | [cite_start]Le client doit gérer son propre état[cite: 1827]. |

---

# 3. COMPOSANTES ET ENTITÉS SOA

### [cite_start]LES ENTITÉS [cite: 1990]
* [cite_start]**Fournisseur :** Implémente le service, publie l'interface et garantit la qualité (SLA)[cite: 2003, 2005].
* [cite_start]**Client (Consommateur) :** Développe l'application-client, génère le **stub** et suit les termes du fournisseur[cite: 2009, 2012, 2013].
* **Réseau :** Infrastructure de communication. [cite_start]Les défaillances réseau incombent au fournisseur et affectent la SLA[cite: 2017, 2021].

### [cite_start]LES ARTEFACTS TECHNIQUES [cite: 1994]
* [cite_start]**Interface de service :** Document formel (XML/HTML) spécifiant les opérations, paramètres, types de retour et méta-informations (localisation, version)[cite: 2030, 2031, 2035, 2040].
* [cite_start]**Service Stub :** Code généré automatiquement permettant l'accès au réseau et la communication depuis le langage de l'application-client[cite: 2043, 2044, 2047].
* [cite_start]**UDDI :** Référentiel global pour la découverte et l'intégration des services[cite: 1935, 1937].

---

# 4. COMPOSITION DE SERVICES : ORCHESTRATION VS CHORÉGRAPHIE


| Concept | **Orchestration** | **Chorégraphie** |
| :--- | :--- | :--- |
| **Contrôle** | [cite_start]**Centralisé** : Un moteur décide de la séquence[cite: 1984, 1985]. | [cite_start]**Décentralisé** : Collaboration pilotée par les événements[cite: 1981, 1982]. |
| **Mécanisme** | [cite_start]Un médiateur appelle chaque service[cite: 1985]. | [cite_start]Les services réagissent aux événements des autres[cite: 1982]. |
| **Exemples / Outils** | [cite_start]Temporal, Camunda, AWS Step Functions[cite: 1986]. | [cite_start]Kafka, AWS EventBridge (Serverless)[cite: 1983]. |

---

# 5. PROTOCOLES ET MÉCANISMES DE COMMUNICATION

### [cite_start]RPC (Remote Procedure Call) [cite: 2095]
* [cite_start]**Fonctionnement :** Étend l'appel local au réseau[cite: 2097]. [cite_start]Le client sérialise les paramètres (Pack) -> Envoi -> Le serveur désérialise (Unpack) -> Exécution[cite: 2120, 2129].
* [cite_start]**Avantages :** Haute performance, interaction directe[cite: 2136, 2138].
* [cite_start]**Inconvénients :** Couplage étroit, faible découvrabilité[cite: 2140, 2141].

### [cite_start]SOAP (Simple Object Access Protocol) [cite: 2145]
* [cite_start]**Structure :** Enveloppe XML contenant un **Header** et un **Body**[cite: 2155, 2156, 2157].
* [cite_start]**WSDL :** Langage XML décrivant les Types, Messages, PortType (opérations), Binding et Service (adresse)[cite: 2163, 2164, 2166, 2168].
* [cite_start]**Forces :** Sécurité entreprise (WS-Security), transactions fiables, gestion d'erreurs normalisée[cite: 2173, 2174, 2175].
* [cite_start]**Faiblesses :** Très verbeux (XML), lent (parsing), courbe d'apprentissage abrupte[cite: 2183, 2184, 2188].

### [cite_start]REST (Representational State Transfer) [cite: 2191]
* [cite_start]**Style :** Basé sur les ressources et les méthodes HTTP standards[cite: 2192, 2193].
* [cite_start]**Méthodes :** **GET** (Lire), **POST** (Créer), **PUT** (Mettre à jour), **DELETE** (Supprimer)[cite: 2201].
* [cite_start]**Forces :** Très scalable, performance élevée (léger), supporte la mise en cache[cite: 2205, 2206, 2207].
* [cite_start]**Faiblesses :** Absence de normes formelles (contrats), difficile à composer/rechercher sans standard[cite: 2210].

### [cite_start]GRAPHQL [cite: 2229]
* [cite_start]**Concept :** Le client demande **exactement** les données requises via un seul point d'accès[cite: 2245, 2246].
* [cite_start]**Caractéristiques :** Schéma fortement typé, pas de versionnage (le schéma évolue), support du temps réel (subscriptions)[cite: 2247, 2248, 2261].
* [cite_start]**Inconvénient :** Mise en cache complexe, risque de sollicitation serveur sur requêtes complexes[cite: 2267, 2269].

### [cite_start]gRPC (Google RPC) [cite: 2273]
* [cite_start]**Technologie :** Basé sur **HTTP/2** et **Protobuf** (format binaire compact)[cite: 2276, 2277].
* [cite_start]**Forces :** Performance maximale (plus rapide que REST), streaming bidirectionnel, génération auto de stubs[cite: 2293, 2294, 2296].
* [cite_start]**Limites :** Non supporté nativement par les navigateurs, débogage difficile (binaire)[cite: 3201, 2302].

---

# [cite_start]6. FOCUS EXAMEN : SLA ET MÉTRIQUES [cite: 2049]

[cite_start]**SLA (Service Level Agreement) :** Entente contractuelle sur la qualité du service[cite: 2050].
* [cite_start]**Éléments spécifiés :** Types de services, méthodes de monitorage, délais de résolution et pénalités[cite: 2051, 2054, 2056, 2057].
* **Métriques de performance critiques :**
    1.  [cite_start]**Temps de réponse :** Latence pour une demande[cite: 2060].
    2.  [cite_start]**Débit (Throughput) :** Nombre de demandes par unité de temps[cite: 2061].
    3.  [cite_start]**Disponibilité :** Taux de temps de fonctionnement (Uptime)[cite: 2062].

---

# [cite_start]7. HISTOIRE ET ÉVOLUTION (CHRONOLOGIE) [cite: 2074]

* [cite_start]**1991 :** CORBA (Partage d'objets via ORB, mais trop complexe/lent)[cite: 1863, 1865, 1891].
* [cite_start]**1998/1999 :** XML-RPC / SOAP (Standardisation XML)[cite: 2089, 2076].
* [cite_start]**2000 :** REST (Simplification via HTTP)[cite: 2090].
* [cite_start]**2015/2016 :** GraphQL / gRPC (Optimisation moderne et performance)[cite: 2082, 2092].