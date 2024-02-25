---
title: ES6
date: 
id: ES6
tags: 
  - Connaissances fondamentales
  - ES6
categories: 
  - Tech
  - JavaScript
no_toc: true
---

# ES6

> Info: Cette partie du contenu est remerciée pour l'aide apportée du cyber-ami "chargeur du front-end" (前端充电宝 en chinois), qui est l'ingénieur en développement front-end venant de la Hangzhou ville, en Chine. Son blog en chinois peut être consulté sur rubrique "liens utiles" .

### 1. Différences entre `let`, `const` et `var`

1. Portée du bloc
   
   La portée de bloc est délimitée par `{ }`, `let` et `const` ont une portée de bloc.
   
   `var` n'a pas de portée de bloc, c'est une portée de fonction. Les variables déclarées avec `var` dans une fonction seront détruites lorsque la fonction se termine.
   
   <!-- more -->
   
   La portée de bloc résout deux problèmes de l'ES5 :
   
   - Le risque de recouvrement des variables externes par des variables internes
   
   - Les variables de boucle utilisées pour le comptage peuvent fuir et devenir des variables globales

2. Hissage des variables (Hoisting variables)
   
   L'hissage des variables en JavaScript se réfère au déplacement de la déclaration des variables en haut de leur portée avant l'exécution du code. Cela signifie que vous pouvez utiliser une variable avant sa déclaration. Cependant, seul la déclaration est hissée, pas l'assignation.
   
   Toutes les déclarations de variables sont hissées, mais `var` est initialisée à `undefined` lors de l'hissage, tandis que les déclarations avec `const` et `let` ne sont pas initialisées, entraînant une zone morte temporaire (temporal dead zone) en cas d'accès avant l'assignation.
   
   Les variables déclarées avec `var` ont une portée sur toute la fonction, tandis que celles déclarées avec `let` et `const` ont une portée limitée à la zone avant leur déclaration.
   
   Voici quelques exemples :
   
   - Hissage avec `var` :
     
     ```js
     console.log(x); // undefined
     var x = 5;
     console.log(x); // 5
     ```
   
   - Hissage avec `let` ou `const`:
     
     ```js
     // console.log(y); // ReferenceError: y is not defined
     let y = 10;
     console.log(y); // 10
     ```
   
   En conclusion, comprendre l'hissage des variables aide à éviter les comportements inattendus liés à l'utilisation de variables avant leur déclaration. Dans le code, la meilleure pratique est de déclarer une variable avant de l'utiliser pour assurer un code plus clair et plus maintenable.

3. Ajout d'attributs globaux
   
   Dans le navigateur, l'objet global est `window`, tandis que dans Node, l'objet global est `global`
   
   Les variables déclarées avec `var` deviennent des variables globales et seront ajoutées comme propriétés de l'objet global. Cependant, cela n'est pas le cas avec `let` et `const`

4. Redéclaration
   
   Lorsqu'une variable est déclarée avec `var`, il est possible de la redéclarer, et la variable du même nom déclarée ultérieurement écrasera la précédente. Cependant, les déclarations avec `let` et `const` ne permettent pas la redéclaration

5. Zone morte temporaire
   
   Avant la déclaration d'une variable avec `let` ou `const`, celle-ci n'est pas accessible. Syntaxiquement, cela est appelé "zone morte temporaire"
   
   Les variables déclarées avec `var` ne sont pas sujettes à la zone morte temporaire

6. Initialisation des valeurs
   
   Lors de la déclaration de variables, `var` et `let` peuvent ne pas être initialisés immédiatement, mais une variable déclarée avec `const` doit être initialisée

7. Pointeurs
   
   `let` et `const` sont des syntaxes introduites par ES6 pour créer des variables.
   
   Les variables créées avec `let` peuvent avoir leur pointeur modifié, c'est-à-dire qu'elles peuvent être réaffectées. En revanche, les variables déclarées avec `const` ne peuvent pas être réaffectées
   
   | Différence                  | var | let | cont |
   |:---------------------------:|:---:|:---:|:----:|
   | Portée de bloc              | ✖   | ✔   | ✔    |
   | Hissage des variables       | ✔   | ✖   | ✖    |
   | Ajout de variables globales | ✔   | ✖   | ✖    |
   | Redéclaration des variables | ✔   | ✖   | ✖    |
   | Zone morte temporaire       | ✖   | ✔   | ✔    |
   | Initialisation des valeurs  | ✖   | ✖   | ✔    |
   | Changement de pointeur      | ✔   | ✔   | ✖    |

### 2. Les propriétés d'un objet const peuvent-elles être modifiées ?

`const` ne garantit pas que la valeur d'une variable ne peut pas être modifiée, mais plutôt que l'adresse mémoire pointée par la variable ne peut pas être modifiée.

Pour les types de données de base (nombres, chaînes de caractères, valeurs booléennes), leur valeur est directement stockée à l'adresse mémoire pointée par la variable, ce qui équivaut à une constante.

Cependant, pour les types de données par référence (principalement les objets et les array), la variable pointe vers l'adresse mémoire des données. Une fois initialisée, tant que la variable n'est pas réaffectée (modifiant l'adresse mémoire), il est possible d'effectuer des opérations arbitraires sur ce type de référence.

### 3. Est-ce que les fonctions fléchées peuvent être créées avec le mot-clé 'new'?

Les fonctions fléchées n'ont pas de prototype, n'ont pas leur propre référence `this`, et ne peuvent pas utiliser le paramètre `arguments`. Par conséquent, il n'est pas possible d'utiliser 'new' pour créer une fonction fléchée.

### 4. Différences entre les fonctions fléchées et les fonctions traditionnelles

1. Les fonctions fléchées sont plus concises que les fonctions traditionnelles :
   
   - Si aucune argument n'est requis, il suffit d'écrire une paire de parenthèses vides
   
   - En présence d'un seul argument, les parenthèses autour de l'argument peuvent être omises
   
   - Pour plusieurs arguments, ils sont séparés par des virgules
   
   - Si le corps de la fonction renvoie une seule instruction, les accolades peuvent être omises
   
   - Si la fonction n'a pas besoin de renvoyer de valeur et ne comporte qu'une seule instruction, le mot-clé 'void' peut être ajouté devant cette instruction. 
     
     C'est couramment utilisé lors de l'appel d'une fonction, par exemple:
     
     ```js
     let fn = () => void doesNotReturn();
     ```

2. Les fonctions fléchées n'ont pas de référence `this` propre
   
   Les fonctions fléchées ne créent pas leur propre référence `this`, elles n'ont donc pas de `this`propre. Elles héritent plutôt du `this` de leur portée parente. Ainsi, la référence 'this' dans une fonction fléchée est déterminée lors de sa définition et ne change pas par la suite.

3. La référence `this` héritée par une fonction fléchée ne changera jamais: 
   
   ```js
   var id = 'GLOBAL';
   var obj = {
     id: 'OBJ',
     a: function(){
       console.log(this.id);
     },
     b: () => {
       console.log(this.id);
     }
   };
   obj.a();    // 'OBJ'
   obj.b();    // 'GLOBAL'
   new obj.a()  // undefined
   new obj.b()  // Uncaught TypeError: obj.b is not a constructor
   ```
   
   La méthode `b` de l'objet `obj` est définie à l'aide d'une fonction fléchée. Dans cette fonction, `this` pointe toujours vers le contexte d'exécution global où elle a été définie, même si la fonction est appelée en tant que méthode de l'objet `obj`. 
   
   Il est important de noter que les accolades `{}` définissant l'objet ne créent pas un environnement d'exécution distinct ; elles restent dans le contexte global.

4. Les méthodes telles que `call()`, `apply()`, `bind()` ne peuvent pas modifier la référence `this` dans une fonction fléchée:
   
   ```js
   var id = 'Global';
   let fun1 = () => {
       console.log(this.id)
   };
   fun1();                     // 'Global'
   fun1.call({id: 'Obj'});     // 'Global'
   fun1.apply({id: 'Obj'});    // 'Global'
   fun1.bind({id: 'Obj'})();   // 'Global'
   ```

5. Les fonctions fléchées ne peuvent pas être utilisées en tant que constructeurs
   
   Le processus de l'utilisation du mot-clé `new` pour les constructeurs a été expliqué précédemment. 
   
   En réalité, la deuxième étape consiste à lier le 'this' de la fonction à l'objet nouvellement créé. Cependant, étant donné que les fonctions fléchées n'ont pas de `this` propre, pointent vers l'environnement d'exécution externe, et ne peuvent pas changer leur référence `this`, elles ne peuvent donc pas être utilisées en tant que constructeurs.

6. Les fonctions fléchées n'ont pas leur propre parametres `arguments`
   
   Les fonctions fléchées n'ont pas leur propre objet `arguments`. 
   
   Lorsqu'on accède à `arguments` dans une fonction fléchée, on obtient en réalité la valeur de `arguments` de la fonction externe

7. Les fonctions fléchées n'ont pas de `prototype`

8. Les fonctions fléchées ne peuvent pas être utilisées en tant que fonctions génératrices et ne peuvent pas utiliser le mot-clé `yield`

### 5. À quoi pointe le `this` des fonctions fléchées ?

Les fonctions fléchées diffèrent des fonctions traditionnelles en JavaScript, elles n'ont pas de `this` propre, et leur `this` est capturé à partir du contexte dans lequel elles sont définies. 

Cela devient leur propre référence `this`, et étant donné qu'elles n'ont pas de `this` propre, elles ne peuvent pas être invoquées avec le mot-clé `new`. De plus, la référence `this` ainsi capturée ne sera pas modifiée.

### 6. Le rôle et les scénarios d'utilisation de l'opérateur de propagation

1. Opérateur de propagation pour les objets
   
   L'opérateur de propagation pour les objets (...) est utilisé pour extraire toutes les propriétés énumérables de l'objet paramètre et les copier dans l'objet actuel
   
   ```js
   let bar = { a: 1, b: 2 };
   let baz = { ...bar }; // { a: 1, b: 2 }
   ```
   
   La méthode ci-dessus est en réalité équivalente à :
   
   ```js
   let bar = { a: 1, b: 2 };
   let baz = Object.assign({}, bar); // { a: 1, b: 2 }
   ```
   
   La méthode `Object.assign` est utilisée pour fusionner les objets en copiant toutes les propriétés énumérables de l'objet source dans l'objet cible. 
   
   Le premier argument de la méthode `Object.assign` est l'objet cible, et les arguments suivants sont les objets sources. 
   
   Si l'objet cible et l'objet source ont des propriétés de même nom, ou si plusieurs objets sources ont des propriétés de même nom, les propriétés ultérieures écraseront les propriétés précédentes.
   
   De même, si des propriétés personnalisées de l'utilisateur sont placées après l'opérateur de propagation, les propriétés de même nom à l'intérieur de l'opérateur de propagation seront écrasées:
   
   ```js
   let bar = {a: 1, b: 2};
   let baz = {...bar, ...{a:2, b: 4}};  // {a: 2, b: 4}
   ```

2. Opérateur de propagation pour les array
   
   L'opérateur de propagation pour les array permet de convertir un array en une séquence de paramètres séparés par des virgules, et ne peut déplier qu'un seul niveau de array à chaque fois
   
   ```js
   console.log(...[1, 2, 3])
   // 1 2 3
   console.log(...[1, [2, 3, 4], 5])
   // 1 [2, 3, 4] 5
   ```
   
   Voici quelques exemples d'utilisation de l'opérateur de propagation pour les array:
   
   - **Convertir un array en une séquence de paramètres**
     
     ```js
     function add(x, y) {
       return x + y;
     }
     const numbers = [1, 2];
     add(...numbers) // 3
     ```
   
   - **Copier un array**
     
     ```js
     const arr1 = [1, 2];
     const arr2 = [...arr1];
     ```
     
     À retenir : **L'opérateur de propagation (...) est utilisé pour extraire toutes les propriétés énumérables de l'objet de paramètre et les copier dans l'objet actuel**, ici l'objet de paramètre est un array, et tous les objets à l'intérieur du array sont de types de données de base, copiant ainsi tous les types de données de base dans un nouveau array.
   
   - **Fusionner des array**
     
     Si on souhaite fusionner des array à l'intérieur d'un array, vous pouvez le faire de la manière suivante :
     
     ```js
     const arr1 = ['two', 'three'];
     const arr2 = ['one', ...arr1, 'four', 'five'];
     // ["one", "two", "three", "four", "five"]
     ```
   
   - **L'opérateur de propagation combiné avec la déstructuration est utilisé pour générer des array**
     
     ```js
     const [first, ...rest] = [1, 2, 3, 4, 5];
     first // 1
     rest  // [2, 3, 4, 5]
     ```
     
     À noter: **Si vous utilisez l'opérateur de propagation dans l'affectation d'un array, il doit être placé uniquement en dernière position des paramètres, sinon une erreur sera signalée**
     
     ```js
     const [...rest, last] = [1, 2, 3, 4, 5];         // erreur
     const [first, ...rest, last] = [1, 2, 3, 4, 5];  // erreur
     ```
   
   - **Convertir une chaîne de caractères en un array réel**
     
     ```js
     [...'hello'] // [ "h", "e", "l", "l", "o" ]
     ```
   
   - **Tout objet implémentant l'interface Iterator peut être converti en un array réel à l'aide de l'opérateur de propagation**
     
     Une application courante est la conversion de certaines structures de données en array : utilisée pour remplacer la syntaxe `Array.prototype.slice.call(arguments)` de l'ES5
     
     ```js
     // l'objet arguments
     function foo() {
       const args = [...arguments];
     }
     ```
   
   - Utiliser les fonctions `Math` pour obtenir des valeurs spécifiques dans un array
     
     ```js
     const numbers = [9, 4, 7, 1];
     Math.min(...numbers); // 1
     Math.max(...numbers); // 9  
     ```
   
   ### 7. Compréhension de la déstructuration des objets et des array
   
   La déconstruction est un nouveau modèle d'extraction de données proposé par ES6. 
   
   Ce modèle permet d'extraire sélectivement les valeurs souhaitées d'un objet ou d'un array.
   
   1. **Déconstruction des array**
      
      Lors de la déconstruction d'un array, l'extraction des données souhaitées se fait en fonction de la position des éléments :
      
      ```js
      const [a, b, c] = [1, 2, 3]
      ```
      
      Finalement, les valeurs des indices 0, 1 et 2 du array sont respectivement assignées aux variables a, b et c, c'est-à-dire `1, 2, 3`.
      
      Les valeurs des éléments aux indices 0, 1 et 2 du array sont précisément mappées aux variables de gauche aux indices 0, 1 et 2, c'est le mode de fonctionnement de la déconstruction d'arrays. 
      
      Il est également possible d'effectuer une extraction précise de certains éléments du array en attribuant des espaces réservés vides aux variables de gauche.
      
      ```js
      const [a,,c] = [1,2,3]
      ```
      
      En laissant des espaces vides au milieu, il est possible d'assigner facilement les valeurs de la première et de la dernière position du array aux variables a et c, c'est-à-dire `a=1 et c=3`
   
   2. Déconstruction des objets
      
      La déconstruction des objets est légèrement plus complexe que la déconstruction des array, mais elle est également plus puissante.
      
      Lors de la déconstruction des objets, c'est le nom des propriétés qui sert de critère de correspondance pour extraire les données souhaitées.
      
      Définissons maintenant un objet :
      
      ```js
      const stu = {
        name: 'Bob',
        age: 24
      }
      ```
      
      Si l'on souhaite déconstruire ses deux propriétés propres, on peut le faire ainsi :
      
      ```js
      const { name, age } = stu
      ```
      
      Nous obtenons deux variables de niveau égal à 'name' et 'age' : `name = 'Bob', age = 24`.
      
      Il est important de noter que la déconstruction des objets se base strictement sur le nom des propriétés en tant que critère de localisation. Par conséquent, même si on échange les positions de 'name' et 'age', le résultat reste le même :
      
      ```js
      const { age, name } = stu // age = 24 name = "Bob"
      ```
   
   ### 8. Comment extraire les propriétés spécifiques d'un objet fortement imbriqué?
   
   Il arrive parfois de rencontrer des objets fortement imbriqués:
   
   ```js
   const school = {
      classes: {
         stu: {
            name: 'Bob',
            age: 24,
         }
      }
   }
   ```
   
   Comme dans le cas de la variable 'name' ici, qui est imbriquée sur quatre niveaux, il est évident que tenter de l'extraire avec les méthodes traditionnelles ne fonctionnera pas:
   
   ```js
   const { name } = school // ne marche pas
   ```
   
   Parce que l'objet 'school' lui-même ne possède pas la propriété 'name', cette dernière se trouve à l'intérieur de l'objet 'fils du fils' de l'objet 'school'. 
   
   Pour extraire 'name', une méthode plutôt laborieuse consiste à déconstruire couche par couche :
   
   ```js
   const { classes } = school
   const { stu } = classes
   const { name } = stu
   name // 'Bob'
   ```
   
   Mais il existe une méthode plus standard pour résoudre ce problème en une seule ligne de code : l'on peut, du côté droit des noms de variables déconstruites, utiliser la forme `deux-points + {nom de la propriété cible}` pour poursuivre la déconstruction en continuant ainsi jusqu'à obtenir les données ciblées : 
   
   ```js
   const { classes: { stu: { name } }} = school
   
   console.log(name)  // 'Bob'
   ```

### 9. Compréhension du paramètre `rest`

Lorsque l'opérateur de spread est utilisé sur les paramètres d'une fonction, il peut également regrouper une séquence de paramètres distincts en un seul array :

```js
function mutiple(...args) {
  let result = 1;
  for (var val of args) {
    result *= val;
  }
  return result;
}
mutiple(1, 2, 3, 4) // 24
```

Ici, la fonction 'multiple' reçoit quatre paramètres distincts, mais si l'on essaie d'afficher la valeur de 'args' à l'intérieur de cette fonction, on constatera qu'il s'agit d'un array :

```js
function mutiple(...args) {
  console.log(args)
}
mutiple(1, 2, 3, 4) // [1, 2, 3, 4]
```

C'est là que réside la puissance de l'opérateur `...rest`. Il peut regrouper plusieurs arguments d'une fonction dans un array. 

Cela est souvent utilisé pour récupérer les paramètres excédentaires d'une fonction, ou pour traiter des situations où le nombre de paramètres de la fonction est incertain, comme dans l'exemple ci-dessus.

### 10. Syntaxe des modèles et le traitement des chaînes de caractères dans ES6

ES6 a introduit le concept de 'syntaxe des modèles'. Avant ES6, la concaténation de chaînes de caractères était une tâche laborieuse :

```js
var name = 'css'   
var career = 'coder' 
var hobby = ['coding', 'writing']
var finalString = 'my name is ' + name + ', I work as a ' + career + ', I love ' + hobby[0] + ' and ' + hobby[1]
```

Avec seulement quelques variables, écrire autant de signes plus et être constamment vigilant quant aux espaces et à la ponctuation à l'intérieur pouvait être furieux. 

L'introduction des chaînes de modèles a considérablement simplifié cette tâche : Les chaînes de caractères ne sont pas seulement plus faciles à concaténer, mais aussi plus faciles à lire, améliorant ainsi la qualité globale du code

```js
var name = 'css'   
var career = 'coder' 
var hobby = ['coding', 'writing']
var finalString = `my name is ${name}, I work as a ${career} I love ${hobby[0]} and ${hobby[1]}`
```

**Les avantages des chaînes de modèles :**

1. Permet l'incorporation de variables avec la syntaxe `${}`

2. Dans les chaînes de modèles, les espaces, les indentations et les sauts de ligne sont conservés

3. Les chaînes de modèles prennent en charge entièrement les expressions opérationnelles, permettant d'effectuer des calculs à l'intérieur de `${ }`

En se basant sur le premier point, il est possible d'écrire du code HTML directement et sans obstacles dans les chaînes de modèles :

```js
let list = `
    <ul>
        <li>Élément de liste 1</li>
        <li>Élément de liste 2</li>
    </ul>
`;
console.log(message); // Sortie correcte, aucune erreur n'est générée
```

En se basant sur le deuxième point, il est possible d'insérer des calculs simples et des appels de fonction directement dans `${}` :

```js
function add(a, b) {
  const finalString = `${a} + ${b} = ${a+b}`
  console.log(finalString)
}
add(1, 2) // Sort '1 + 2 = 3'
```

En plus de la syntaxe des modèles, ES6 a également introduit une série de méthodes de chaînes de caractères visant à améliorer l'efficacité du développement :

- **jugement d'existence**
  
  Par le passé, pour déterminer si un caractère/une chaîne de caractères était présent dans une autre chaîne, on utilisait uniquement `indexOf > -1`. Maintenant, en ES6, trois nouvelles méthodes sont disponibles : `includes`, `startsWith`, `endsWith`. Elles renvoient toutes une valeur booléenne pour indiquer si l'élément recherché existe.
  
  1. **includes**  Vérifie la relation d'inclusion entre une chaîne de caractères et une sous-chaîne :
     
     ```js
     const son = 'haha' 
     const father = 'xixi haha hehe'
     father.includes(son) // true
     ```
  
  2. **startsWith**  Vérifie si une chaîne de caractères commence par un certain caractère/une certaine séquence :
     
     ```js
     const father = 'xixi haha hehe'
     father.startsWith('haha') // false
     father.startsWith('xixi') // true
     ```
  
  3. **endsWith** Vérifie si une chaîne de caractères se termine par un certain caractère/une certaine séquence :
     
     ```js
     const father = 'xixi haha hehe'
     father.endsWith('hehe') // true
     ```

- **Répétition automatique** 
  
  On peut utiliser la méthode repeat pour reproduire plusieurs fois la même chaîne de caractères ( soit la copier de manière continue) :
  
  ```js
  const sourceCode = 'repeat for 3 times;'
  const repeated = sourceCode.repeat(3) 
  console.log(repeated) // repeat for 3 times;repeat for 3 times;repeat for 3 times;
  ```
