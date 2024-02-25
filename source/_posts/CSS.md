---
title: CSS
date: 2024-01-07 21:42:28
id: CSS
tags: 
  - Connaissances basiques
  - CSS
categories: 
  - Tech
no_toc: true
---

# CSS

### 1. Nouvelles fonctionnalités de CSS3

1. Nouveaux sélecteurs
   
   - :last-child correspond au dernier enfant de l'élément parent.
   
   - :nth-child(n) correspond au n-ième enfant de l'élément parent.
   
   <!-- more -->
   
   <!-- more -->

2. Caractéristiques de la bordure
   
   - border-radius: Bordure arrondie

3. Couleur et opacité
   
   - opacity: 0.5;
   
   - color: rgba(0, 0, 0, 0.5)

4. Ombres
   
   - text-shadow: Ombre du texte
   
   - box-shadow: Ombre de la boîte

5. Transformation
   
   - transform: rotate(9deg): Rotation
   
   - transform: scale(0.5) : Mise à l'échelle
   
   - transform: translate(100px, 100px): Déplacement

6. Transition et animation
   
   - transition: Transition
   
   - animation: Animation

7. Requête multimédia
   
   - @media Utilisé pour créer une mise en page réactive.

### 2. Modèle de boîte

1. Concept : Modèle de mise en page adopté par les éléments du DOM lors du rendu de la page peut être configuré via box-sizing.

2. Catégories :
   
   - content-box (Modèle de boîte standard du W3C)
     Lorsqu'une largeur (width) et une hauteur (height) sont définies pour un élément, cela modifie uniquement la largeur + hauteur.
   
   - border-box (Modèle de boîte IE)
     Lorsqu'une largeur (width) et une hauteur (height) sont définies pour un élément, cela modifie la largeur + hauteur + padding.
   
   - Autres non implémentés

### 3. BFC

1. Concept
   
   - BFC, également connu sous le nom de Contexte de Formatage en Bloc, se réfère à : une zone de rendu indépendante

2. Conditions de déclenchement (Activation du BFC)
   
   - Définir overflow, c'est-à-dire `hidden`, `auto`, `scroll`
   
   - Définir float, à l'exclusion `none`
   
   - Définir le positionnement, absolute ou fixed, etc.

3. Règles spécifiques
   
   - BFC est un élément bloc, et les éléments blocs sont disposés verticalement
   
   - BFC est un conteneur indépendant, ses éléments internes n'affectent pas les éléments externes au conteneur
   
   - Pour deux boîtes appartenant au même BFC, il peut y avoir un chevauchement des marges, et la marge maximale est prise
   
   - Lors du calcul de la hauteur de BFC, les éléments enfants flottants doivent également être inclus dans le calcul

4. Applications
   
   - Empêcher le chevauchement des marges
   
   - Effacer les flottants pour éviter l'effondrement de la hauteur
   
   - Empêcher que les éléments de flux standard soient recouverts par des éléments flottants

### 4. La pondération et la priorité des sélecteurs

- L'ordre de la pondération et de la priorité des sélecteurs：
  
  `!important > Style en ligne > #id > .class > balise > * > Héritage > Par défaut`

- Les navigateurs CSS analysent les sélecteurs **de droite à gauche**

### 5. Préprocesseur CSS

Les préprocesseurs CSS définissent un nouveau langage qui permet une maintenance et une gestion plus aisées du code CSS. Ils sont principalement:

- Sass

- Less

- Stylus

### 6. Flex

1. **Concept**
   
   - Flex est l'abréviation de "Flexible Box", ce qui signifie "layout flexible" et est utilisé pour fournir une flexibilité maximale au modèle de boîte.
   
   - Les éléments utilisant la mise en page Flex sont appelés conteneurs Flex (conteneur flex), abrégé en "conteneur". Tous ses sous-éléments deviennent automatiquement des membres du conteneur, appelés éléments Flex (élément flex), abrégé en "élément".
   
   - Le conteneur a par défaut deux axes : l'axe principal et l'axe transversal (également appelé axe secondaire). Par défaut, l'axe horizontal est l'axe principal et l'axe vertical est l'axe transversal.

2. Propriétés du conteneur (2 à 3)
   
   - `flex-direction` définit la direction de l'axe principal.
   
   - `flex-wrap` définit s'il faut passer à la ligne.
   
   - `flex-flow` est une forme abrégée des propriétés `flex-direction` et `flex-wrap`.
   
   - `justify-content` définit l'alignement des éléments le long de l'axe principal.
   
   - `align-items` définit l'alignement des éléments le long de l'axe transversal.
   
   - `align-content` définit l'alignement des éléments sur l'axe de croisement.

3. Propriétés des éléments (2 à 3)
   
   - `order` définit l'ordre d'arrangement des éléments. Plus le nombre est petit, plus l'élément est placé en avant. La valeur par défaut est 0.
   
   - `flex-grow` définit le facteur de croissance de l'élément. La valeur par défaut est 0, ce qui signifie qu'il ne se développera pas même s'il y a de l'espace supplémentaire.
   
   - `flex-shrink` définit le facteur de rétrécissement de l'élément. La valeur par défaut est 1, ce qui signifie qu'il se rétrécira en cas de manque d'espace.
   
   - `flex-basis` définit l'espace sur l'axe principal que l'élément occupe avant la distribution de l'espace supplémentaire. Sa valeur par défaut est "auto", correspondant à la taille originale de l'élément.
   
   - `flex` est une abréviation de `flex-grow`, `flex-shrink` et `flex-basis`, avec des valeurs par défaut de `0 1 auto`
   
   - `align-self` permet à un élément individuel d'avoir un alignement différent des autres éléments, pouvant remplacer la propriété `align-items`.

4. Compréhension
   
   - `flex-grow: 1` Si de l'espace supplémentaire est disponible, l'élément va se développer
   
   - `flex-shrink: 1` Si l'espace disponible est insuffisant, l'élément va se réduire
   
   - `flex-basis: 0%` Lorsque défini à 0%, cela signifie qu'il n'occupe pas d'espace sur l'axe principal. Cependant, en raison des paramètres de `flex-grow` et `flex-shrink`, l'élément se développera ou se réduira automatiquement

### 7. Méthodes de masquage des éléments de la page

1. `display: none` Ne prend pas de place. Ne déclenche pas les événements DOM
2. `opacity: 0` Occupe de la place, mais n'est pas visible. Déclenche les événements DOM
3. `visibility: hidden` Occupe de la place, mais n'est pas visible. Ne déclenche pas les événements DOM
4. `position: absolute; left: -10000px` Déplace l'élément hors de l'écran
5. `z-index: -1` Masque l'élément actuel derrière d'autres éléments positionnés

### 8. Centrer un élément horizontalement et verticalement

1. En utilisant la position absolue, avec les dimensions (largeur et hauteur) inconnues pour les sous-éléments
   
   ```css
   .father {
   position: relative;
   }
   .son {
   position: absolute;
   left: 50%;
   top: 50%;
   transform: translate(-50%, -50%);
   }
   ```

2. En utilisant la position absolue, les dimensions des sous-éléments doivent être explicitement définies
   
   ```css
   .father {
   position: relative;
   }
   .son {
   position: absolute;
   left: 50%;
   top: 50%;
   width: 200px;
   height: 200px;
   margin-left: -100px;
   margin-top: -100px;
   }
   ```

3. En utilisant Flex
   
   ```css
   .father {
   display: flex;
   justify-content: center;
   align-items: center;
   }
   ```
