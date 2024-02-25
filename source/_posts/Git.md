---
title: Git
date: 2024-01-21 22:25:29
id: Git
tags:
  - Connaissances avancées
  - Git
  - Linux
  - Github
categories: 
  - Tech
  - Git 
  - Linux
  - Github
no_toc: true
---

# Git

### 1. Installation de Git

1. Téléchargement et installation
   
   Lien de téléchargement:  [https://git-scm.com/](https://git-scm.com/)

2. Invite de commandes
   
   - CMD: `CMD` est l'abréviation de command, c'est-à-dire l'invite de commandes 
   
   - Powershell: il peut être considéré comme une version améliorée ou une version complémentaire de `CMD`, et prend en charge la plupart des commandes Linux
     
     <!-- more -->
   
   - Git Bash: bash est une ligne de commande de style Linux, les chemins sont également de style Linux, et elle peut utiliser des commandes Windows et Linux. Lors de l'installation de Git, un environnement bash léger est également installé, puis en lançant `git bash`, la fenêtre de commande qui s'ouvre contient les variables d'environnement de cet environnement bash. 
     
     bash est une bibliothèque de commandes basée sur le `shell` et un script de commande sous `unix`

3. Variable d'environnement
   
   - Tout simplement, les variables d'environnement sont des moyens rapides d'ouvrir des fichiers
   
   - Lorsque tu souhaites exécuter un programme, le système le recherchera dans le répertoire actuel. S'il ne le trouve pas, il cherchera dans les variables d'environnement du chemin (PATH). S'il le trouve, il l'exécutera; sinon, cela risque de provoquer une erreur. En configurant les variables d'environnement, nous pouvons optimiser notre efficacité d'utilisation, économiser du temps
   
   - Configurer les variables d'environnement sur l'ordinateur : 
     
     **Panneau de configuration -> Système et sécurité -> Système -> Modifier les paramètres -> Avancé -> Variables d'environnement -> Path**

### 2. Configuration initiale de Git

Maintenant que Git est installé sur ton système, quelques étapes sont nécessaires pour personnaliser ton environnement Git. 

Cette configuration n'a besoin d'être effectuée qu'une fois par machine, car les informations de configuration sont conservées lors des mises à jour du programme. Tu as la possibilité de les modifier à tout moment en exécutant les commandes appropriées.

La configuration Git est une variable du client Git local et ne change pas avec le dépôt Git.

1. Configuration du nom d'utilisateur et de l'adresse email
   
   La première chose à faire après avoir installé Git est de configurer ton nom d'utilisateur et ton adresse email. C'est une étape cruciale car chaque commit Git utilise ces informations et les enregistre dans chaque contribution, de manière permanente et non modifiable
   
   ```shell
   # Configurer le nom d'utilisateur global
   git config --global user.name "username"   
   
   # Configurer le mot de passe global
   git config --global user.email "email"
   ```

2. Vérifier la configuration Git
   
   ```shell
   # Vérifier le nom d'utilisateur et l'adresse email globaux dans la configuration
   git config --global user.name
   git config --global user.email
   
   # Vérifier toutes les configurations globales de Git
   git config --global -l  
   ```

### 3. Initialiser un dépôt Git

Nous avons besoin de Git pour gérer le code source, donc nous devons également avoir un référentiel Git en local.

Il y a deux façons d'obtenir un dépôt avec Git :

1. Initialiser un dépôt Git et ajouter tous les fichiers du projet au dépôt Git
   
   > PS: actuellement, de nombreux générateurs de projet créent automatiquement un dépôt Git lors de la création du projet
   
   - Créer ou accéder au dossier, faire un clic droit dans la zone vide du dossier, puis cliquer sur `Git Bash Here` pour ouvrir la ligne de commande 
     
     > sur système MAC, ouvrez le terminal dans le dossier actuel
   
   ```shell
   git init  # Initialisation du dépôt
   ```
   
   <!-- more -->
   
   - Cette commande créera un sous-répertoire appelé .git, contenant tous les fichiers nécessaires de ton dépôt Git initialisé. Ces fichiers sont au core du dépôt Git
   
   - Cependant, à ce stade, tu vient seulement d'effectuer une opération d'initialisation, les fichiers de ton projet n'ont pas encore été suivis
   
   - Créez un dépôt appelé 'name' dans le répertoire actuel, utilisez la commande `cd name` pour accéder au dépôt et effectuer des opérations
     
     ```shell
     git init name  # Créer le dépôt 'name'
     ```

2. Cloner un dépôt Git déjà existant depuis un autre serveur 
   
   > PS: cette opération est généralement nécessaire le premier jour en arrivant  à l'entreprise
   
   ```shell
   # exemple
   git clone https://github.com/thecafe75000/myreactdemos.git
   ```

### 4. Trois zones

Git a trois états possibles pour vos fichiers :

1. Contribué (committed)

2. Modifié (modified)

3. Indexé (staged)

Cela introduit le concept des trois zones de travail dans un projet Git : le référentiel Git, le répertoire de travail et la zone de mise en index

- Espace de travail (zone d'édition de code) : représente l'endroit où le code de développement local est situé

- Zone de mise en index (zone de modifications en attente) : représente l'endroit où le code est temporairement stocké dans le dépôt local

- Zone du dépôt (zone de sauvegarde de code) : représente l'endroit où le code entre dans le contrôle de version local
  
  <img src="https://github.com/thecafe75000/ImagesForMyblog/raw/main/Git/stageofgit.png" />

### 5. Répertoire `.git`

- Le répertoire `hooks` contient des scripts d'accroche pour le client ou le serveur, qui s'exécutent automatiquement lors d'opérations spécifiques

- Le répertoire `info` contient un fichier d'exclusion global, permettant de configurer les fichiers à ignorer.

- Le répertoire `logs` enregistre les informations de journal.

- Le répertoire `objects` stocke l'ensemble du contenu des données, l'emplacement du référentiel local.

- Le répertoire `refs` stocke les pointeurs vers les objets de validation des données (branches).

- Le fichier `config` contient des options de configuration spécifiques au projet.

- Le fichier `description` est utilisé pour afficher des informations de description sur le référentiel.

- Le fichier `HEAD` indique la branche actuellement extraite.

- Le fichier `index` contient des données de la zone de transit.

- **N'oubliez pas : ne modifiez jamais manuellement le contenu du dossier `.git`**

### 6. Commandes courantes de Git

1. Opérations de validation avec Git
   
   - `git status` : Consultation de l'état de la version
     
     - Rouge: Indique que le fichier est dans la zone de travail (modifié, supprimé ou non suivi)
     
     - Vert : Indique que le fichier est dans la zone de staging
     
     - Non indiqué : Signifie que le fichier est dans la zone de version
   
   - `git add -A` ou ` git add .` ou `git add *` :  Suivre de nouveaux fichiers, mettre en staging les fichiers modifiés, etc
   
   - `git commit -m 'commentaire'` : Valider les modifications et ajouter un commentaire
   
   - Bien que l'utilisation de la zone de staging permette de préparer soigneusement les détails à soumettre, parfois cela peut sembler un peu lourd. 
     
     Git propose une méthode pour sauter l'utilisation de la zone de staging, il suffit d'ajouter l'option `-am` à `git commit` lors de la soumission. 
     
     Git va automatiquement mettre en staging tous les fichiers déjà suivis et les soumettre ensemble, contournant ainsi l'étape `git add`.

2. Opération d'annulation
   
   - En utilisant `git restore`, il est possible d'annuler les modifications dans le répertoire de travail.
     
     Mais pour les nouveaux fichiers, il est nécessaire d'utiliser `rm` pour les supprimer
   
   - En utilisant `git restore --staged <fichier>`, il est possible d'annuler la mise en staging

3. Opération de suppression
   
   - Utilisez `git rm fileName` pour supprimer le fichier de la zone de staging et du répertoire de travail.
   - Utilisez `git rm --cached fileName` pour supprimer le fichier de la zone de staging sans toucher au répertoire de travail.
   - Utilisez `git rm -f fileName` pour supprimer de force le fichier de la zone de staging et du répertoire de travail (nécessaire en cas de divergence entre les fichiers des deux zones).
   - **Remarque : La commande `git rm` ne peut supprimer que les fichiers gérés par le référentiel.**

4. Opérations de renommage et de déplacement
   
   - `git mv 01.txt 02.txt`: Renommer le fichier
   - `git mv 01.txt hello/`: Modifier le chemin du fichier
   - `git mv 01.txt hello/02.txt`: Modifier le chemin du fichier et renommer

5. Comparer les différences
   
   - Utiliser `git diff` pour voir les différences entre la zone de travail et la zone de staging (sans afficher les fichiers supprimés ou ajoutés), affichant les modifications effectuées
     
     ```shell
     // Interprétation des résultats
     lipeihuadeMacBook-Pro% git diff
         //comparaison concerne index.html avant la modification et index.html après la modification)
         diff --git a/index.html b/index.html
         // Représente les valeurs de hachage Git de deux versions
         index 16158b4..61045cd 100644
         //"---" représente la version précédente des modifications
         --- a/index.html
         //"+++" représente la version après des modifications
         +++ b/index.html
         // lignes 1 à 2 du fichier source présentent des différences avec les lignes 1 à 5 du fichier cible,
         // Ci-dessous se trouvent les détails spécifiques des différences
         @@ -1,2 +1,5 @@
         // -partie rouge représente la diminution, +partie verte représente l'ajout
          index.html 
         -no 1
         +
         +
         +
         + modification supplémentaire
         // La dernière ligne n'a pas de saut de ligne
         \ No newline at end of file
     ```
   
   - `git diff --cached` : Afficher les différences entre la zone de staging et le référentiel.
   
   - `git diff a b` : Comparer les différences entre deux versions.

6. Versions historiques et annulations dans Git
   
   - Voir les versions antérieures
     
     - `git log`
       
       > Par défaut, sans aucun paramètre, `git log` affiche toutes les mises à jour selon l'ordre chronologique des soumissions, les plus récentes en haut. Chaque soumission est identifiée par une somme de contrôle SHA-1, le nom et l'adresse e-mail de l'auteur, l'heure de la soumission, et enfin, un paragraphe indenté affiche le commentaire de la soumission
     
     - Une option couramment utilisée avec `git log` est `-p`, qui affiche les différences de contenu à chaque soumission. Tu peux également ajouter `-2` pour afficher uniquement les deux dernières soumissions.
       
       Si le contenu est trop long, utilisez les touches de direction pour faire défiler vers le haut et le bas, appuyez sur `q` pour quitter
     
     - `git log --oneline` Informations succinctes
   
   - Revenir à une version spécifique en utilisant le numéro de version
     
     Régression de version locale, n'affecte que localement, n'influence pas le contenu du dépôt Git
     
     - `git reset --hard/--mixed/--soft b815fd5a6ae655b521a31a9`
       
       - `--hard` : Déplacer le pointeur HEAD de la bibliothèque locale, réinitialiser la zone de staging, réinitialiser la zone de travail
       
       - `--mixed`: Déplacer le pointeur HEAD de la bibliothèque locale, réinitialiser la zone de staging, le code ajouté à la zone de staging lors de la dernière opération d'add est maintenant affiché en rouge, indiquant qu'aucune opération d'add n'a été effectuée
       
       - `--soft` : Seulement déplacer le pointeur HEAD de la bibliothèque locale, la zone de staging et ton code local n'ont subi aucun changement
     
     > Lors du retour à une version antérieure, il n'est pas nécessaire d'utiliser la chaîne de hachage complète, les sept premiers caractères suffisent. 
     > 
     > **Avant de changer de version, il faut soumettre l'état actuel du code dans le référentiel**
     
     - `git reflog`
     
     > Si après un retour en arrière tu souhaites revenir à une version antérieure, `git reflog` permet de consulter tous les enregistrements d'opérations sur toutes les branches (y compris les opérations commit et reset), y compris les enregistrements de commit déjà supprimés. `git log`, en revanche, ne permet pas de visualiser les enregistrements de commit supprimés
   
   - Autres annulations
     
     ```shell
     git reset --hard HEAD^     # Revenir à la version précédente
     git reset --hard HEAD^^    # Revenir à la version antérieure précédente
     git reset --hard HEAD~100  # Revenir aux 100 versions précédente
     ```

### 7. Configurer les fichiers ignorés par Git

Dans certains projets, il y a des fichiers qui ne doivent pas être inclus dans le référentiel de versions, tels que les configurations de l'éditeur.

Dans Git, il est nécessaire de créer un fichier `.gitignore`, généralement dans le même répertoire que `.gitignore`

```shell
# Ignorer tous les dossiers .idea
.idea

# Ignorer tous les fichiers se terminant par .test
*.test  

# Ignorer les fichiers et dossiers node_modules
/node_modules
```

### 8. Branches de Git

Quasiment tous les systèmes de contrôle de version prennent en charge les branches d'une manière ou d'une autre. L'utilisation de branches signifie que tu peux séparer ton travail de la ligne principale de développement, évitant ainsi d'impact sur la ligne principale. 

Dans de nombreux systèmes de contrôle de version, il s'agit d'un processus légèrement inefficace —— souvent, il est nécessaire de créer complètement une copie du répertoire du code source. Pour les projets importants, un tel processus peut prendre beaucoup de temps.

La gestion des branches par Git est incroyablement légère, la création d'une nouvelle branche peut être réalisée en un instant, et le passage entre différentes branches est tout aussi rapide. 

Contrairement à de nombreux autres systèmes de contrôle de version, Git encourage une utilisation fréquente des branches et des fusions dans le flux de travail, même plusieurs fois par jour.

1. GitFlow
   
   GitFlow est une meilleure pratique pour le développement d'équipe, qui divise le code en plusieurs branches :
   
   - Branche principale `Main`: elle ne contient que les versions officiellement publiées
   
   - Branche de correction des bugs en production (Hotfix): Une fois le développement terminé, il est nécessaire de fusionner avec les branches `Main` et `Develop`, tout en créant une balise (tag) sur la branche `Main`
   
   - Branche de fonctionnalité `Feather` : Lorsque vous développez une fonctionnalité, créez une branche distincte, puis fusionnez-la avec la branche dev une fois le développement terminé
   
   - Branche `Release` : Branche en attente de publication, créée à partir de la branche `Develop`. Les tests et les corrections de bogues(Bug) sont effectués sur cette branche Release.
   
   - Branche `Develop` : Branche de développement où tous les développeurs soumettent leur code

2. Opérations de branches
   
   - Créer une branche
     
     ```shell
     git branch name   //name est le nom de branche
     ```
   
   - Voir les branches
     
     ```shell
     git branch
     ```
   
   - Changer de branche
     
     ```shell
     git checkout name  //name est le nom de branche
     ```
     
     > Note : Avant de changer de branche, il faut soumettre les modifications actuelles de la branche en cours
   
   - Créer et basculer sur une branche
     
     ```shell
     // Crée et bascule sur une nouvelle branche
     git checkout -b name 
     
     // Crée et bascule sur une nouvelle branche, force l'écrasement si la branche actuelle existe déjà
     git checkout -B name 
     
     // Crée une nouvelle branche à partir d'un commit spécifique  
     git checkout -b name commitID 
     
     // Crée une branche orpheline
     // Une branche orpheline n'est pas différente des autres branches
     // just au début d'une branche orpheline, elle n'a pas d'historique de commits provenant d'une branche parente
     git checkout --orphan name 
     ```

     ```

- Supprimer une branche
  
  ```shell
  # "name" peut être remplacé par le nom réel de la branche que tu souhaites supprimer
  git branch -d name  // Supprimer une branche locale
  
  git branch -D name  // Supprimer de force une branche locale (en cas de modifications non fusionnées)
  
  git push origin --delete name  // Supprimer une branche distante
  ```

- Merge des branches
  
  ```shell
  // Fusionne le contenu d'une branche spécifique dans la branche actuelle
  git merge name 
  
  // Fusionne de force des branches avec des historiques non apparentés
  git merge --allow-unrelated-histories name 
  ```

- Conflit
  
  Lorsque plusieurs branches modifient le même fichier, des conflits peuvent survenir lors de la fusion des branches. 
  
  La résolution des conflits est assez simple : modifier le contenu pour obtenir le résultat final souhaité, puis continuer avec les commandes `git add` et `git commit`

### 9. Commandes couramment utilisées sous Linux

Linux est un système d'exploitation open source et gratuit. L'interaction avec le système se fait généralement par des commandes. 

Voici quelques commandes couramment utilisées :

- `ls` : Afficher les fichiers dans le répertoire actuel (abrégé de "list")

- `ls -al` ou `ls -a -l` pour afficher les fichiers cachés et les présenter verticalement

- `cd` : Entrer dans un répertoire (abrégé de "change directory")

- `cd ..` Pour remonter d'un niveau 

- La touche `tab` permet l'autocomplétion du code

- `clear` : Effacer l'écran

- `mkdir` : Créer un répertoire

- `touch test.html` : Créer un fichier

- `rm test.html` : Supprimer un fichier

- `rm -r dir` : Supprimer un répertoire

- `mv fichier_ou_dossier_origine fichier_ou_dossier_destination` : Déplacer un fichier

- `cat test.html` : Afficher le contenu d'un fichier

- `ctrl+c` : Annuler une commande

- Les touches de direction vers le haut et vers le bas du clavier (flèches haut et bas) permettent de consulter l'historique des commandes

### 10. Utilisation de GitHub

GitHub est un site de gestion de dépôts Git. Il permet de créer un référentiel central distant, facilitant ainsi la collaboration entre plusieurs personnes pour le développement.

1. **Son utilisation**
   
   L'utilisation du dépôt distant GitHub est relativement simple, avec principalement les scénarios suivants :
   
   - **Dépôt local existant**
     
     1. Créer un dépôt distant
     
     2. Obtenir l'adresse du dépôt
     
     3. Associer l'URL du dépôt distant au dépôt local (de cette manière, on sait quel dépôt distant à rechercher sur local)
        
        ```shell
        git remote add origin https://github.com/xxx/xxx.git
        ```
        
        L'association ne peut se faire qu'une seule fois. Si tu souhaites associer un autre dépôt, tu dois supprimer l'association avec le dépôt actuel
        
        ```shell
        git remote remove origin
        ```
     
     4. Commit local
        
        ```shell
        git add .
        git commit -m xxx
        ```
     
     5. Tout d'abord, pousser le contenu de la branche principale du dépôt local vers le dépôt distant.
        
        **la première branche poussée est considérée comme la branche principale, indépendamment de son nom**
        
        ```shell
        git push -u origin main
        ```
        
        - `push` : Pousser la  branche
        
        - `-u` : Associer avec dépôt distant , une fois ajouté, les futures soumissions peuvent être raccourcies en utilisant directement `git push`
        
        - `origin` : Alias du dépôt distant
        
        - `main` : Branche du dépôt local
     
     6. Créez ensuite une nouvelle branche de développement appelée `dev`
        
        ```shell
        git checkout -b dev
        ```
     
     7. La branche de développement ajoute ou modifie le code
     
     8. Effectuer des commits locaux sur la branche de développement
        
        ```shell
        git add .
        git commit -m "xxxxxx"
        ```
     
     9. Pousser la branche de développement vers le dépôt distant
        
        ```shell
        # il faut indiquer le nom de la branche correspondante en cas de soumettre une branche
        git push origin dev 
        ```
   
   - **Pas de dépôt local**
     
     1. Cloner un dépôt
        
        ```shell
        git clone https://github.com/xxxxx/xxxxx.git [name]
        //name correspond à la modification du nom du dépôt
        ```
     
     2. Accéder au dépôt
        
        ```shell
        cd xxxxx
        ```
     
     3. Si la branche de développement n'existe pas, tu dois la créer. 
        
        Si elle existe, tu dois tirer à nouveau la branche de développement distante et basculer dessus
        
        ```shell
        # créer une branche nouvelle
        git checkout -b dev  
        
        # la branche distante existe,besoin de la tirer 
        git fetch origin dev:dev
        git checkout dev
        ```
     
     4. La branche de développement ajoute ou modifie le code
     
     5. Effectuer des validations locales sur la branche de développement
        
        ```shell
        git add .
        git commit -m 'message'
        ```
     
     6. Pousser la branche vers le dépôt distant
        
        ```shell
        git push
        ```
        
        > Après le clonage du code, le dépôt local aura une configuration par défaut pour une adresse distante avec le nom `origin`

2. **Le développement du code étant terminé, il est nécessaire de fusionner les branches**
   
   - Passer à la branche principale `main`
     
     ```shell
     git checkout main
     ```
   
   - Fusionner le contenu de la branche `dev`
     
     ```shell
     git merge dev
     ```
   
   - Une fois la fusion terminée, pousser la branche `main` vers le dépôt distant
     
     ```shell
     git push
     ```
   
   > Peut-être qu'une erreur pourrait survenir lors du `push` sur `main`, indiquant des messages tels que `hint: "git pull" xxx`
   > 
   > Cela signifie que la version du code dans le dépôt local est en retard par rapport à la version dans le dépôt distant. Il faut donc tirer la dernière version du code depuis le dépôt distant vers le dépôt local avec la commande : `git pull origin main`
