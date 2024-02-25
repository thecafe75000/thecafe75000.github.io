---
title: JavaScript
date: 2024-01-07 21:15:24
id: JavaScript
tags: 
  - Connaissances fondamentales
  - JavaScript
categories: 
  - Tech
  - JavaScript
no_toc: true
---

# JavaScript

### 1. Les types de données en JavaScript

Ils se divisent en types de données fondamentaux et types de données de référence

1. Types de données fondamentaux:
   
   - number (nombre)
   
   - string (chaîne de caractères)
   
   - boolean (booléen)
   
   - null (null)
   
   - undefined (non défini)
     
     <!-- more -->
   
   - symbol (symbole)
     
     - Utilisé pour attribuer une valeur unique à une variable
     - Utilisé pour attribuer un nom de propriété unique à un objet (le type de nom de propriété d'objet doit être soit string, soit symbol)
   
   - bigint (entier bigint)
     
     - Lorsque les calculs avec le type number dépassent la valeur maximale (Number.MAX_SAFE_INTEGER) ou tombent en dessous de la valeur minimale, des problèmes de calcul peuvent survenir. Dans ce cas, on peut utiliser bigint (rarement utilisé en développement pratique).

2. Types de données de référence:
   
   - object (objet)
   - function (fonction)
   - array 

### 2. Comment détecter les types de données en JavaScript

1. typeof
   
   La plupart des types peuvent être détectés, mais ne peut pas faire la distinction entre null, object et array

2. A instanceof B
   
   Compréhension simple : vérifie si A est une instance de B
   Compréhension approfondie : vérifie si le `__proto__` de A pointe vers le même objet que B.prototype
   
   Principalement utilisé pour détecter les types de données référencés

3. Object.prototype.toString.call(xxx).slice(8, -1)
   
   c'est la solution parfaite, il peut détecter tous les types de données
   
   En développement, utilisez la méthode `toString()` pour encapsuler des fonctions utilitaires afin de détecter les types

4. Array.isArray
   
   Vérifie s'il s'agit d'un type array

5. A === B
   
   Vérifie que les valeurs et les types de A et B sont identiques.

### 3. Méthodes courantes pour les array

1. Méthodes de mise à jour d'un array
   
   - `push()`: Ajoute un élément à la fin du array
   - `pop()`: Supprime le dernier élément du array
   - `unshift()`: Ajoute un élément au début du array
   - `shift()`: Supprime le premier élément du array
   - `splice()`: Supprime/ajoute un élément à un indice spécifique
   - `sort()`: Trie le array
   - `reverse()`: Inverse l'ordre des éléments dans le array

2. Méthodes de parcours des éléments
   
   - `forEach()`: Parcourt les éléments du array
   - `map()`: Retourne un nouveau array avec la même longueur que l'original, mais les valeurs internes changent souvent. (Longueur inchangée, valeurs modifiées)
     - Souvent utilisé pour mettre à jour une valeur dans les données React
   - `filter()`: Retourne un nouveau array avec une longueur généralement inférieure à celle de l'original, mais les valeurs internes restent les mêmes. (Longueur modifiée, valeurs inchangées)
     - Souvent utilisé pour supprimer une valeur des données React
   - `reduce()`: Communément utilisé pour des fonctions telles que le calcul statistique, l'accumulation et la sommation
     - Module du panier, calcul du prix total par exemple
   - `find()`: Recherche un élément, le renvoie s'il est trouvé, sinon renvoie undefined
   - `findIndex()`: Recherche l'indice d'un élément, le renvoie s'il est trouvé, sinon renvoie `-1`
   - `every()`: Renvoie true seulement si tous les éléments renvoient true, sinon renvoie `false`
   - `some()`: Renvoie true dès qu'un élément renvoie true, sinon renvoie `false`

3. Autres méthodes 
   
   - `slice()`: Coupe certains éléments du array
   - `concat()`: Concatène des array
   - `join()`: Joint les éléments du array en une chaîne de caractères d'une certaine manière
   - `includes()`: Vérifie si un élément est présent, renvoie true s'il est présent, sinon renvoie `false`
   - `indexOf()`: Vérifie si un élément est présent, renvoie son indice s'il est trouvé, sinon renvoie `-1`

### 4. Opérations courantes sur le DOM

1. Ajouter des éléments du DOM
   
   - `document.createElement()` crée des éléments DOM
   - `xxxDom.appendChild()` insère un élément DOM dans le xxxDom

2. Supprimer des éléments du DOM
   
   - `xxxDom.removeChild()` supprime un sous-élément du xxxDom
   - `xxxDom.remove()` supprime xxxDom lui-même

3. Modifier des éléments du DOM
   
   - `xxxDom.innerText / xxxDom.textContent` définissent le contenu texte de l'élément
   - `xxxDom.innerHTML` définit le contenu HTML de l'élément

4. Obtenir/Rechercher des éléments du DOM
   
   - `document.getElementById()` obtient un élément DOM en fonction de l'identifiant
   - `document.querySelector()` obtient le premier élément DOM trouvé en fonction de n'importe quel sélecteur
   - `document.querySelectorAll()` obtient tous les éléments DOM trouvés en fonction de n'importe quel sélecteur

### 5. Compréhension des fermetures en JavaScript

1. Concept
   
   En utilisant l'outil de développement de Chrome, on comprend que l'essence d'une fermeture (closure) est un conteneur dans une fonction interne (non objet JavaScript), contenant les variables locales référencées.

2. Origine de la fermeture
   
   - Imbrication de fonctions
   - La fonction interne fait référence aux variables locales de la fonction externe
   - La fermeture est créée lors de l'appel de la fonction externe

3. Cycle de vie d'une fermeture
   
   - Création : Lorsque la fonction interne est créée
   - Fin de vie : Lorsque la fonction interne n'a plus de références de variables et devient un objet inutile, elle sera automatiquement récupérée par le ramasse-miettes (GC - Garbage Collection).

4. Rôle des fermetures
   
   - Prolonger la durée de vie des variables locales (les garder en vie un peu plus longtemps)
   - Permettre à des fonctions externes de manipuler indirectement les données des variables locales de la fonction interne

5. Application des fermetures dans les projets
   
   - Dans React, elles sont sous forme de fonctions d'ordre supérieur afin de réutiliser des fonctions

### 6. La référence de "this"

Dans des situations normales, la référence de `this` dépend de la manière dont la fonction est appelée :

1. Appel direct (liaison par défaut) : `this` pointe vers la fenêtre (window), et dans le mode strict ('use strict'), `this` pointe vers `undefined`

2. Appel de fonction par un objet (liaison implicite) : `this` pointe vers l'objet appelant

3. Appel de fonction avec `call()/apply()/bind()` (liaison explicite) : `this` pointe vers le premier argument passé
   
   - Différences et liens des `call()/apply()/bind()` :
     
     - `call()/apply()` exécutent immédiatement la fonction, tandis que `bind()` renvoie une nouvelle fonction
     - Lors de l'exécution avec `call()/apply()`, `this` pointe vers le premier argument ; la nouvelle fonction retournée par `bind()` pointe également vers le premier argument, tandis que la fonction d'origine reste inchangée
     - La manière de passer les arguments à `call()/bind()` est la même et peut prendre plusieurs arguments, tandis qu'`apply()` ne prend que deux arguments, le second étant un array

4. Appel de fonction avec `new` : `this` pointe vers l'objet d'instance créé

**Cas particuliers :**

1. Fonctions fléchées : `this` pointe vers le `this` de la fonction externe la plus proche (elle pointe vers le `this` de la fonction parente)

2. Fonctions de rappel :
   
   - Fonction de rappel de minuterie : `this` pointe vers la fenêtre, et dans le mode strict, vers `undefined`
   - Fonction de rappel d'événement DOM : `this` pointe vers l'élément DOM lié à l'événement

### 7. Prototype et Chaîne de Prototype

1. Prototype
   
   - Ce que nous appelons prototype se réfère à deux propriétés de prototype : `__proto__` et `prototype`
   - `prototype` est appelé propriété de prototype explicite
   - `__proto__` est appelé propriété de prototype implicite
   - Chaque fonction a une propriété de prototype explicite, dont la valeur est un objet que nous appelons `objet prototype`
   - Par défaut, il y a une méthode constructeur sur cet objet prototype, pointant vers la fonction elle-même, et un attribut `__proto__`, pointant vers l'objet prototype d'Object.
   - Chaque instance a une propriété de prototype implicite, dont la valeur pointe vers l'objet prototype de la fonction constructeur correspondante
   
   **Cas particuliers :**
   
   - `Function.prototype === Function.__proto__` ; ils pointent vers le même objet
   - `Object.prototype.__proto__ === null` ; c'est la fin de la chaîne de prototype

2. Chaîne de Prototype
   
   - Concept : À partir de la propriété `__proto__` d'un objet, toutes les connexions entre les objets forment une structure appelée chaîne de prototype, également connue sous le nom de "chaîne de prototype implicite"
   
   - Utilité : Utilisée pour rechercher les propriétés d'un objet
   
   - Règles : Lors de la recherche de propriétés d'un objet ou de l'appel de méthodes d'un objet, la recherche commence d'abord sur l'objet lui-même
     
     Si la propriété n'est pas trouvée, la recherche se poursuit le long de la chaîne de prototype
     
     Si la propriété est trouvée, sa valeur est renvoyée
     
     Finalement, la recherche aboutit à `Object.prototype.__proto__` , si la propriété n'est toujours pas trouvée, `undefined `est renvoyé
   
   - Application : La chaîne de prototype est utilisée pour mettre en œuvre l'héritage

### 8. Le mécanisme de collecte des déchets de JavaScript

En JavaScript，la libération (collecte) des objets est gérée par le collecteur de déchets du navigateur

1. Collecteur de déchets
   
   - Le navigateur dispose d'un thread dédié qui s'exécute à intervalles très courts
   - Son travail principal consiste à déterminer si un objet est un objet inutile, si oui,  le collecteur de déchets va le nettoyer de ses données en mémoire et marquer la mémoire comme étant en état de disponibilité

2. Stratégies de collecte des déchets
   
   - Mécanisme : Algorithme de marquage et d'élagage (Mark-and-Sweep)
     
     - Description : 
       
       La phase de marquage consiste à marquer tous les objets actifs, tandis que la phase d'élagage détruit les objets non marqués (c'est-à-dire les objets inactifs)
     
     - Inconvénients :
       
       - Fragmentation de la mémoire, entraînant des blocs de mémoire non contigus, ce qui peut conduire à de nombreux blocs de mémoire inutilisés et à une difficulté de trouver un bloc adapté lors de l'allocation de mémoire pour de grands objets
       - La vitesse d'allocation est lente, même en utilisant la stratégie du meilleur ajustement (First-fit), car l'opération reste une opération O(n), dans le pire des cas, une traversée complète de la mémoire peut être nécessaire
     
     - Solution : 
       
       On peut utiliser l'algorithme de marquage et de compactage (Mark-Compact). Après la phase de marquage, cet algorithme déplace les objets vivants (c'est-à-dire ceux qui ne nécessitent pas d'être nettoyés) vers une extrémité de la mémoire, puis nettoie la mémoire à la frontière

3. Mécanisme de collecte des déchets du moteur V8 de JavaScript
   
   - Il utilise un algorithme basé sur le marquage et l'élagage, mais il a subi certaines optimisations
   - Pour la zone des objets récemment créés (nouveaux objets), une collecte parallèle est utilisée
   - Pour la zone des objets plus anciens, une approche d'augmentation de marquage et de nettoyage paresseux (incremental marking and lazy sweeping) est adoptée

### 9. Le mécanisme de la boucle d'événements en JavaScript

1. Concept : Mécanisme d'exécution du code asynchrone

2. Processus :
   
   - Le thread principal de JavaScript exécute séquentiellement tout le code. Lorsqu'il rencontre du code synchrone, il l'exécute séquentiellement. En revanche, lorsqu'il rencontre du code asynchrone, il le transmet au module de gestion correspondant (thread secondaire) :
     - Par exemple, en cas de rencontre d'une minuterie, elle est gérée par le module de gestion des minuteries. Ce module compte le temps, et lorsque le temps est écoulé, il ajoute automatiquement la fonction de rappel à la file d'attente des rappels (file d'attente des tâches macros)
     - De même, en cas de rencontre d'un événement DOM, il est géré par le module de gestion du DOM. Ce module lie l'événement, et lorsque l'événement se produit, il ajoute automatiquement la fonction de rappel à la file d'attente des rappels (file d'attente des tâches macros)
     - Lors de rencontres avec des requêtes ajax, elles sont gérées par le module de gestion des requêtes ajax. Ce module envoie la requête, et lorsqu'une réponse est reçue, il ajoute automatiquement la fonction de rappel à la file d'attente des rappels (file d'attente des tâches macros)
   - Le thread principal de JavaScript ne s'arrête pas et exécute séquentiellement le code suivant jusqu'à ce que tout le code soit exécuté. Ensuite, le thread principal de JavaScript lance la boucle d'événements
   - Le thread principal de JavaScript parcourt la file d'attente des rappels, récupère séquentiellement les fonctions de rappel et les exécute
     - La file d'attente des rappels se divise en deux types : file d'attente des tâches macros (macro-tâches) et file d'attente des microtâches (micro-tâches)
     - **File d'attente des tâches macros :** Fonctions de rappel pour les minuteries, les rappels ajax, les rappels d'événements DOM
     - **File d'attente des microtâches :** Promise.then/catch/finally, MutationObserver (fonctionnement de la méthode nextTick)
     - Il donne la priorité à l'exécution des fonctions de rappel de la file d'attente des microtâches jusqu'à ce qu'elles soient toutes exécutées
     - Après avoir exécuté la première fonction de rappel de la file d'attente des tâches macros, il exécute à nouveau les fonctions de rappel de la file d'attente des microtâches jusqu'à ce qu'elles soient toutes exécutées
     - Ensuite, il passe à l'exécution de la prochaine fonction de rappel de la file d'attente des tâches macros, puis répète le processus, et ainsi de suite
