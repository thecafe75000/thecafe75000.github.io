---
title: Package Manager
date: 2024-01-27 22:23:07
id: Package_Manager
tags:
  - Package Manager
categories: 
  - Tech
  - Package Manager
no_toc: true
---

# Package Manager

### 1. Introduction

Un gestionnaire de paquets est un outil logiciel utilisé pour gérer les bibliothèques ou cadres tiers (appelés communément "paquets") nécessaires au développement d'un projet. 

Il peut automatiquement installer, mettre à jour, désinstaller et configurer des paquets, tout en gérant les dépendances entre les paquets afin d'assurer la compatibilité entre eux.

<!-- more -->

### 2. Les gestionnaires de paquets courants

- npm

- yarn

- pnpm

### 3. npm (Node Package Manager)

npm est le gestionnaire de paquets pour Node.js, il est également une application.

npm n'a pas besoin d'être installé séparément, il est automatiquement installé lorsque l'on installe Node.js. 

> Contrairement à d'autres gestionnaires de paquets qui nécessitent une installation distincte

**Son utilisation**

1. **Initialiser le fichier de description du paquet**
   
   Avant de télécharger un paquet, il est nécessaire d'avoir un fichier `package.json`, également appelé " fichier de description du paquet ", qui enregistre des informations sur le projet en cours et des informations sur les dépendances etc.
   
   On peux utiliser la commande suivante pour créer le fichier de description du paquet :
   
   ```shell
   npm init
   
   npm init -y
   ```
   
   ```shell
   // package.json
   {
     "name": "test",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "author": "",
     "license": "ISC"
   }
   ```
   
   - `name` : nom du paquet
   
   - `version`:  version du paquet
   
   - `description`:  description du paquet
   
   - `main`:  fichier principal du paquet
   
   - `scripts`: commande pour exécuter le paquet
   
   - ce qui  peut être exécuté avec `npm run xxx`, par exemple : `npm run test`
   
   - `author`: l'auteur du paquet
   
   - `license`:  la licence open source du paquet

2. **Télécharger le paquet**
   
   Le site officiel: [https://www.npmjs.com](https://www.npmjs.com)
   
   Ce site permet de rechercher des paquets
   
   - `npm install [package]`:  Installer le paquet en tant que dépendance de production
   
   - `npm install [package] -D`:  Installer le paquet en tant que dépendance de développement
     
     > - Dépendances de production : Les dépendances nécessaires à la rédaction du code source du projet sont considérées comme des dépendances de production
     > 
     > - Dépendances de développement : Les dépendances utilisées par les outils de construction et de packaging du projet sont considérées comme des dépendances de développement
   
   - `npm install [package] -g`
     
     - Les packages installés globalement sont utilisés en tant qu'outils, par exemple : nodemon
     
     - Afficher le chemin d'installation global des packages : `npm root -g`
   
   - `npm i` installe toutes les dépendances du fichier `package.json` du projet en cours (y compris les dépendances de développement et de production)
     
     > Installer un paquet installe par défaut la dernière version. Si vous souhaitez installer une version spécifique, utilisez la commande : `npm i vue@2` par exemple
     > 
     > Cela signifie qu'il installera la version majeure 2 de Vue.js, en utilisant les versions mineures et les patchs les plus récents correspondants

3. **Supprimer le paquet**
   
   - `npm uninstall [package]`: désinstaller le paquet
   
   - `npm uninstall [package] -g`:  désinstaller le paquet installé globalement

### 4. yarn

`yarn` est un nouveau gestionnaire de paquets open source développé par Facebook, qui peut être utilisé en remplacement de npm.

Il est généralement recommandé d'utiliser `yarn` pour la gestion des paquets dans les projets React.

**Son utilisation**

- Installation
  
  ```shell
  npm install -g yarn
  ```

- Initialiser le fichier de description du paquet
  
  ```shell
  yarn init
  ```

- Télécharger le paquet
  
  - `yarn add [package]`: Installer le paquet en tant que dépendance de production
  
  - `yarn add [package] --dev`: Installer le paquet en tant que dépendance de développement
  
  - `yarn global add [package]`: Installer le paquet globalement
  
  - `yarn` : Installer toutes les dépendances du fichier `package.json` du projet en cours, y compris les dépendances de développement et de production

- Supprimer le paquet
  
  - `yarn remove [package]` : désinstaller le paquet
  
  - `yarn global remove [package]`: désinstaller le paquet installé globalement

### 5. pnpm

pnpm est un gestionnaire de paquets qui offre une installation plus rapide et une utilisation plus efficace de l'espace disque.

Site officiel: [https://pnpm.io/](https://pnpm.io/)

1. **Pourquoi utiliser pnpm ?**
   
   - Économiser de l'espace disque
     
     Lors de l'utilisation de npm, chaque projet réinstalle les dépendances de manière répétée dans différents projets. En revanche, avec pnpm, les dépendances sont stockées dans un référentiel adressable, de sorte que :
     
     - Si différentes versions d'une même dépendance sont utilisées, seuls les fichiers présentant des différences entre les versions sont ajoutés au référentiel. Par exemple, si un paquet comprend 100 fichiers et que sa nouvelle version ne modifie qu'un seul fichier parmi eux, lors de la mise à jour avec pnpm, seul ce nouveau fichier sera ajouté au référentiel, sans avoir à copier l'intégralité du contenu du nouveau paquet.
     - Tous les fichiers sont stockés à un emplacement précis sur le disque dur. Lors de l'installation d'un paquet, les fichiers du paquet sont liés en tant que liens durs à cet emplacement, sans occuper d'espace disque supplémentaire. Cela permet de partager la même version de dépendances entre différents projets.
     
     Ainsi, une quantité importante d'espace disque est économisée, proportionnelle au nombre de projets et de dépendances, et l'installation est considérablement plus rapide !
   
   - Améliorer la vitesse d'installation
     
     - Résolution des dépendances : Toutes les dépendances qui ne sont pas présentes dans le référentiel sont identifiées et récupérées depuis le référentiel.
     
     - Calcul de la structure du répertoire : La structure du répertoire node_modules est calculée en fonction des dépendances.
     
     - Liaison des dépendances : Toutes les dépendances précédemment installées sont directement récupérées depuis le référentiel et liées à node_modules.
   
   Cette méthode est beaucoup plus rapide que le processus d'installation traditionnel en trois étapes (résolution, récupération et écriture de toutes les dépendances dans node_modules).

2. **Son utilisation**
   
   - Installation
     
     ```shell
     npm install pnpm -g
     ```
   
   - Initialiser le fichier de description du paquet
     
     ```shell
     pnpm init
     ```
   
   - Télécharger le paquet
     
     - `pnpm add [package]`: Installer le paquet en tant que dépendance de production
     
     - `pnpm add -D [package]`: Installer le paquet en tant que dépendance de développement
     
     - `pnpm add -g [package]`: Installer le paquet globalement
     
     - `pnpm install` : Installer toutes les dépendances du fichier `package.json` du projet en cours, y compris les dépendances de développement et de production
   
   - Supprimer le paquet
     
     - `pnpm remove [package]`: désinstaller le paquet
