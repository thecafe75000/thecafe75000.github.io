---
title: Less
date: 2024-02-03 21:27:04
id: Less
tags:
  - Connaissances avancées
  - Less
categories: 
  - Tech
  - Less
no_toc: true
---

# Less

### 1. Qu'est-ce que Less ?

Less est un langage de style dynamique appartenant à la catégorie des préprocesseurs CSS. 

Il étend les fonctionnalités du langage CSS en ajoutant des caractéristiques telles que les variables, les mixins, les fonctions, etc., facilitant ainsi la maintenance et l'extension des feuilles de style. 

Less peut être exécuté côté client et également côté serveur en utilisant Node.js.

<!-- more -->

- Styles dynamiques : Le CSS est un langage non programmable nécessitant la rédaction de nombreuses lignes de code sans logique, ce qui le rend difficile à entretenir, à étendre et peu propice à la réutilisation. 
  
  C'est pourquoi des outils et des frameworks ont été développés pour traiter le CSS.

- Préprocesseur : Un programme de traitement d'une syntaxe donnée avant la génération du CSS.

> Depuis sa création, le CSS n'a pas subi de changements fondamentaux au niveau de sa syntaxe de base et de son mécanisme central. Son développement s'est principalement concentré sur l'amélioration de son expressivité. À ses débuts, le rôle du CSS sur les pages web était simplement décoratif et accessoire, avec une demande majeure pour la simplicité et la facilité d'apprentissage. Cependant, avec la complexité croissante des sites web d'aujourd'hui, le CSS natif a atteint ses limites, laissant les développeurs parfois dépassés.
> 
> Lorsqu'une langue n'a pas les capacités nécessaires et que l'environnement d'exécution des utilisateurs ne prend pas en charge d'autres choix, cette langue devient une "langue cible de compilation". Les développeurs optent alors pour une langue plus avancée pour le développement, puis la compilent vers le langage de base pour une exécution réelle.
> 
> Ainsi, dans le domaine du développement frontal, les préprocesseurs CSS ont vu le jour. Cette vieille langue qu'est le CSS a "réadapté" les besoins du développement web d'une autre manière

- Site officiel: [http://lesscss.org](http://lesscss.org)

- Code source de Less:  https://github.com/cloudhead/less.js 

**Utilisation de Less**:

- Utilisation basique
  
  - `<style type="text/less">` : Le type de balise style doit être modifié en `less`
  
  - Selon le site officiel, nous avons besoin d'un fichier `less.js` pour la compilation Less, et il doit être  importé en bas de la page. Cela est nécessaire car il doit lire tous les fichiers Less liés à la page pour effectuer la compilation.
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <link rel="stylesheet/less" type="text/css" href="styles.less" />
        <style type="text/less">
            @num:200px;
            .box{
                border: 1px solid #000;
                .content{
                    width: @num;
                    height: @num;
                    background:red;
                }
            }
        </style>
    </head>
    
    <body>
        <div class="box">
            <div class="content"></div>
        </div>
        <script src="./less.min.js"></script>
    </body>
    
    </html>
    ```

- Compilation personnalisée de Less dans VSCode
  
  - Ouvrez l'éditeur VSCode, et installer l'extension `Easy LESS`.
  
  - Créer un nouveau fichier Less dans le dossier, puis enregistrer-le. Cela permettra de compiler le fichier CSS correspondant dans le même dossier.

- Installation globale de Less pour la compilation
  
  - Utiliser `npm i less -g` pour installer l'environnement Less global (il est nécessaire d'installer l'environnement Node, qui inclut automatiquement l'outil npm)
  
  - Utiliser la commande `lessc` pour effectuer la compilation
    
    ```less
    *{
        margin:0;
        padding:0;
    }
    .box{
        width: 100px;
        height: 100px;
        background-color: red;
        .content{
            width: 40px;
            height: 40px;
            background-color: pink;
        }
    }
    ```

### 2. La syntaxe de Less

1. **Les commentaires en Less**
   
   - Les commentaires commençant par `//` ne seront pas inclus dans le fichier CSS généré
   
   - Les commentaires enveloppés par `/* */` seront inclus dans le fichier CSS généré
   
   ```less
   //Il existe 2 types de commentaires, le 1er type de commentaires ne peut être vu que dans le fichier Less
   //Le deuxième type de commentaires sera compilé dans le fichier CSS
   .tab{
       width: 100px;
       height: 100px;
       /* Voici comment définir la couleur de fond */
       background-color: red;
   }
   ```

2. **Les variables en Less**
   
   Less nous permet de définir des variables pour gérer le CSS 
   
   > les variables doivent commencer par @
   
   Il est important de noter que dans Less, les variables sont considérées comme des `constantes` et ne peuvent être définies qu'une seule fois. Leur portée est locale et elles sont recherchées dans l'objet parent.
   
   - Les variables en tant que valeurs d'attributs normaux
     
     Utilisation comme valeur d'attribut normal : utiliser directement `@pink`
   
   - Utilisation en tant que sélecteur et nom de propriété
     
     - La forme du sélecteur `#@{valeur of the selector}`
     
     - `@{valeur of the selector} Nom de propriété`
   
   - Utilisation en tant qu'URL
     
     - `@url`
   
   - Chargement différé des variables
     
     Il charge la variable avant le chargement du style dans la portée actuelle, de l'intérieur vers l'extérieur. Il recherche d'abord les variables dans la portée actuelle, puis à l'extérieur de la portée si elles ne sont pas trouvées.
     
     ```less
     // Déclarer une variable représentant la couleur globale
     @mainColor:red;
     
     // Déclarer une variable représentant une valeur
     @zero:10px;
     
     // Déclarer une variable représentant le nom du sélecteur
     @a:outer;
     
     // Déclarer une variable représentant le nom de l'attribut
     @p:position;
     
     // Déclarer une variable pour enregistrer l'image
     @url1:"http://www.google.com/images/pic_new/logo.png";
     
     // Déclarer une variable pour sauvegarder l'image
     @url2:url("http://www.google.com/images/pic_new/logo.png");
     
     // variables peuvent contenir d'autres variables, mais elles doivent être précédées du symbole '@' complet
     @z:@zero;
     *{
         margin:@z;
         padding: @z;
     }
     // 2.Utilisation d'une variable en tant que sélecteur nécessite l'ajout de crochets
     .@{a}{
         //1.Utilisation d'une variable en tant que valeur d'attribut ordinaire nécessite l'ajout du symbole '@'
         border: 1px solid @mainColor;
         width: 400px;
         height: 400px;
         //3.Utilisation d'une variable en tant que nom d'attribut nécessite l'ajout de crochets
         @{p}: relative;
         .box{
             width: 100px;
             height: 100px;
             @{p}: absolute;
             left: @zero;
             top: @zero;
             right: @zero;
             bottom: @zero;
             margin: auto;
             background-color: @mainColor;
         }
         .logo{
             width: 200px;
             height: 100px;
             //4.Utilisation d'une variable en tant qu'adresse URL
             // background: url(@url1) 0 0 no-repeat;
             background: @url2 0 0 no-repeat;
         }
     }
     
     @var: 0;
     .class {
     @var: 1;
         .brass {
           @var: 2;
           three: @var;
           @var: 3;
         }
       one: @var;
     }
     ```

3. **Les règles de nesting en Less**
   
   - Nesting de base
     
     Lors de l'utilisation du CSS standard, il est nécessaire de définir les styles pour des éléments imbriqués sur plusieurs niveaux en utilisant soit des sélecteurs descendants pour définir l'imbrication de l'extérieur vers l'intérieur, soit en attribuant une classe ou un identifiant à cet élément. 
     
     Bien que cette méthode soit facile à comprendre, elle est peu pratique à maintenir, car elle ne permet pas de comprendre clairement les relations entre les styles.
     
     Dans Less, les règles d'imbrication résolvent ce problème. 
     
     Les règles d'imbrication permettent de nester un sélecteur dans un autre, facilitant la conception de code concis, avec une relation claire entre les styles.
   
   - Référence parentale
     
     L'utilisation de `&`: représente tous les éléments parents précédents, souvent utilisé dans les besoins de pseudo-éléments, pseudo-classes, structures CSS, etc.
     
     Le symbole `&` placé avant un sélecteur interne représente une référence au sélecteur parent. 
     
     Si aucun symbole `&` n'est présent avant un sélecteur interne, il est interprété comme un descendant du sélecteur parent ; s'il y a un symbole `&`, il est alors interprété comme un élément parent
   
   ```less
   #outer{
       border: 1px solid #000;
       .content{
           background-color: #ccc;
           padding: 30px;
           .nav{
               background-color: pink;
               border: 1px solid #000;
               list-style: none;
               li{
                   height: 40px;
                   line-height: 40px;
                   font-size: 28px;
                   color: royalblue;
                   // symbole & placé devant un sélecteur représente une référence au sélecteur parent
                   &:nth-child(3){
                       color:yellow;
                   }
                   &:hover{
                       color: green;
                   }
               }
               .active{
                   color:red;
               }
           }
       }
   
       .box{
           margin: 40px;
           background-color: yellowgreen;
           h2{
               font-size: 30px;
               text-align: center;
           }
           p{
               color: #ccc;
               font-size: 12px;
               border: 1px solid red;
           }
       }
   
       .clearFix{
           // css Hack
           *zoom:1;// Activer hasLayout dans les anciennes versions d'IE
           div{
               width: 100px;
               height: 100px;
               background-color: red;
               float: left;
               margin: 10px;
           }
           &:after{
               content:"\200B";
               height: 0;
               display: block;
               clear:both;
           }
       }
   }
   ```

4. **Opération en Less**
   
   - Toute valeur, couleur ou variable peut être opérée
   
   - Less calculera automatiquement l'unité pour vous, donc tu n'as pas besoin d'ajouter une unité à chaque élément, mais assurez-vous qu'au moins un élément a une unité
   
   - Les opérateurs doivent être séparés des valeurs par un espace, et lorsqu'il s'agit de priorités, utilisez des parenthèses () pour les calculs de priorité
   
   ```less
   @num1 : 30;
   .box{
       width: 30px * @num1;
       height: 1000px / 3;
       .con{
           // l'addition et la soustraction des valeurs 
           width: 100px - 30%;
           height: (100px + 10) * 20;
       }
       .inner{
           // manipulation des couleurs consiste à les convertir en valeurs rgba décimales, 
           // puis à effectuer le calcul, avant de les reconvertir en valeurs hexadécimales
           background-color: #fff-55;
       }
   }
   ```

5. **L'héritage dans Less (Extend)**
   
   Il permet à un sélecteur d'hériter du style d'un autre sélecteur. 
   
   L'héritage a deux formats de syntaxe :
   
   - `Sélecteur actuel:extend(sélecteur à hériter) {styles du sélecteur actuel}`
   
   - `Sélecteur actuel {&:extend(sélecteur à hériter);}`
   
   ```less
   // Sachant que .public est le sélecteur hérité, #box est le sélecteur actuel
   // Mode d'héritage N°1
   #box:extend(.public){
       color:red;
   }
   // Mode d'héritage N°2
   #box{
       &:extend(.public);
       color:red;
   }
   ```

6. **Mixin de Less**
   
   En LESS, nous pouvons définir un ensemble de propriétés génériques comme une classe, puis l'appeler dans une autre classe. 
   
   Le mélange consiste à introduire une série de propriétés d'une règle à une autre.
   
   - Mixin ordinaire
     
     - Définition du mixin : utilisez `.+nom_du_mixin+()+{ensemble_de_propriétés}`
     
     - Utilisation du mixin : `.+nom_du_mixin+();`
     
     - Lors de la définition et de l'appel d'un mixin, il est possible de ne pas ajouter des parenthèses (), mais pour faciliter la distinction entre le mixin et le style ordinaire, et aussi pour faciliter la transmission de paramètres, il est généralement conseillé d'ajouter des parenthèses ()
     
     ```less
     // Si une classe utilisée comme mixin n'a pas de parenthèses, elle peut être compilée
     // Si des parenthèses sont ajoutées, elle ne peut pas être compilée et peut seulement être appelée
     .mine(){
         border: 1px solid #000;
         border-radius: 10px;
         background-color: red;
     }
     
     .box{
         width: 100px;
         height: 100px;
         // 
         .mine();
     }
     .con{
         width: 100px;
         height: 100px;
         .mine;
     }
     ```
   
   - Mixin avec des paramètres
     
     Lors de la déclaration d'un mixin, il est possible de déclarer des paramètres formels entre parenthèses.
     
     Les paramètres sont définis par `@+nom_variable`.  
     
     Les arguments concrets peuvent être transmis lors de l'appel
     
     ```less
     // Les paramètres sont déclarés de la même manière que les variables lors de leur définition
     .center(@w,@h,@bg){
         width: @w;
         height: @h;
         background-color: @bg;
         position: absolute;
         left: 0;
         top: 0;
         bottom:0;
         right: 0;
         margin: auto;
     }
     
     .outer{
         // Transmettre les arguments
         .center(500px,500px,red);
         .inner{
            .center(300px,300px,green);
             .content{
                 .center(100px,100px,pink);
             }
         }
     }
     ```
   
   - Mixin de paramètres avec des valeurs par défaut
     
     Il est possible de définir directement des paramètres avec des valeurs par défaut lors de la déclaration d'un mixin, par exemple (@color: rouge).
     
     Lors de l'utilisation du mixin, si des arguments concrets sont transmis, les valeurs des arguments sont utilisées, sinon les valeurs par défaut des paramètres sont utilisées.
     
     ```less
     // Si l'utilisateur ne spécifie pas la largeur et la hauteur, 
     // les valeurs par défaut seront de 500 pixels. 
     // Cependant, en fournissant des arguments, les valeurs par défaut seront remplacées
     .center(@w:500px,@h:500px,@bg){
         width: @w;
         height: @h;
         background-color: @bg;
         position: absolute;
         left: 0;
         top: 0;
         bottom:0;
         right: 0;
         margin: auto;
     }
     
     .border(@w,@s,@c){
         // border:@w @s @c;
         // Dans un mixin, il est possible d'utiliser @arguments pour représenter les arguments fournis
         border:@arguments;
     }
     
     .outer{
         // Paramètres nommés : lors de la transmission des arguments, 
         // il est possible de spécifier des valeurs pour les paramètres correspondants
         .center(@bg:yellow,@h:600px);
         .inner{
            .center(300px,300px,green);
             .con{
                 .center(100px,100px,pink);
                 .border(10px,dotted,yellow)
             }
         }
     }
     ```
   
   - Paramètres nommés
     
     Lors de l'utilisation d'un mixin, si tu souhaites spécifier à quel paramètre formel correspond un argument donné, tu peux nommer les arguments
   
   - La variable `arguments`
     
     La variable `@arguments` représente l'ensemble de tous les paramètres. 
     
     Si tu ne souhaites pas traiter chaque paramètre individuellement, tu peux utiliser `@arguments` en remplacement. 
     
     ```less
     .border(@w:1px,@t:solid,@c:#333){
         border:@arguments;
     }
     ```

7. **Correspondance de motifs, surcharge et gardes**
   
   - correspondance de motif
     
     Dans Less, essayer d'utiliser la correspondance de motif à la place de if/else, dont le fonctionnement est similaire à switch/case. 
     
     Étant donné qu'un mixin peut avoir plusieurs formes, Less offre un mécanisme permettant de changer le comportement du mixin en fonction de la valeur des paramètres. 
     
     Lorsque les paramètres commencent par @_ , cela est obligatoire lors de l'appel de ce mixin.
     
     ```less
     //Lors de la correspondance de motifs, les mixins avec des paramètres commençant par @_ sont obligatoires
     .mine(@_){
         width: 300px;
         height: 100px;
     }
     // Autoriser à changer le comportement du mixin en fonction de la valeur des paramètres
     // Ce paramètre n'est pas utilisé pour transmettre des informations à l'intérieur du mixin, mais plutôt pour identifier les correspondances
     .mine(color1){
         background-color: red;
     }
     .mine(color2){
         background-color: pink;
     }
     
     .box{
         // La relation de correspondance est similaire à une déclaration switch
         .mine(color1);
     }
     ```
- surcharge 
  
  Le même mixin, des comportements différents, peuvent être sélectionnés en fonction du nombre d'arguments réels passés lors de l'appel
  
  ```less
  .mixin(@a,@b){
    background-color:@a;
    width: 1000px;
  }
  .mixin(@a){
    background-color: @a;
    width: 100px;
  }
  
  .box{
    border:1px solid #000;
    height: 100px;
    .mixin(pink,red);
  }
  ```

- gardes
  
  Sélectionner le comportement d'un mixin en fonction des conditions, similaire à if/else en JavaScript, en utilisant la syntaxe when. Les gardes (Guards) nous permettent d'utiliser les opérateurs >, >=, <, <=, =, le mot clé true (qui correspond uniquement au mot clé true, tout ce qui n'est pas true ne sera pas considéré comme une correspondance), ainsi que les opérations logiques and, not(), et nous pouvons également utiliser la virgule ',' pour séparer plusieurs gardes, ce qui signifie que dès que l'une d'entre elles est satisfaite, la condition est considérée comme vraie
  
  ```less
  .mixin(@q){ // sans gardes
    height: 100px;
  }
  .mixin(@q) when(@q>10){
    background-color: red;
  }
  .mixin(@q) when(@q<=10),(@q>100){
    background-color: black;
  }
  .box{
    border:1px solid #000;
    .mixin(99);
  }
  ```
8. **interpolation de chaîne de caractères**
9. 
