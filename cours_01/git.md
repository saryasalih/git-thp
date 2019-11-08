# **1.Introduction**
As-tu déjà travaillé en entreprise ou sur un projet étudiant ? Si oui, tu t'es peut-être déjà retrouvé dans mon cas avec un dossier qui ressemble à ça :
.

└── big_project
    
    ├── big_project_01.xls
    
    ├── big_project_03.xls
    
    ├── big_project_final_féfé.xls
    
    ├── big_project_final.xls
   
    ├── big_project.xls
   
    └── [WIP] big_project_fin.xls








En gros, c'est souvent le bordel dans le monde des moldus du code. Ces derniers passent leur temps à créer des milliers de fichiers, juste au cas où ils auraient besoin de revenir à une version précédente.

maintenant, imagine devoir travailler en équipe sur dossiers de code contenant des milliers de fichiers. Créer des index_VERSIONNUMBER.html à tire-larigot n'est clairemnt pas la mailleure solution. l'idéal serait d'avoir un logiciel capable de préciser pour chacune de ces sauvegardes la réponse aux 4 questions suivantes :

**°Quoi** : quels fichiers ont été modifiés dans cette photographie ?

**°Qui** : qui est responsable de cette modification ?

**°Quand** : de quand cette modification date ?

**°Pourquoi** : pourquoi cette modification existe-t-elle ?
  
  Avec un tel logiciel, fini le stress et les dossiers remplis de fichiers inutiles ! Bonne nouvelle : ce genre de logiciels existe et on les appelle des "gestionnaires de version" (version control software). J'aime bien ce schéma de GiTower qui explique bien à quoi ils servent :
  Comprends-tu maintenant pourquoi le gestionnaire de version appelé Git est un super logiciel, et pourquoi c'est un indispensable dans l'univers du code ? Dans cette ressource, nous verrons comment l'installer et s'en servir. Ensuite, nous verrons de quelle manière l'utiliser pour mettre ses dossiers en ligne avec GitHub (un équivalent de DropBox) pour te permettre de partager ton code et collaborer facilement avec d'autres devs.
  
  # **2.Contexte et historique**
  
  Tout comme il existe plusieurs explorateurs Internet (Firefox, Chrome, Safari, etc), il existe plein de logiciels de gestion de versions (SVN, BitKeeper, etc). Nous allons travailler avec Git pour ce cours car c'est de très très loin le plus connu et utilisé.

Git a été créé en 2005 par Linus Torvald, qui a (entre autres) créé le système d'exploitation Linux.

GitHub est un service de mise en ligne de projets "versionnés" via Git, créé en 2008. Il a été racheté par Microsoft en 2018 pour la modique somme de 7,5 milliards de dollars.

En gros, voici ce que font Git et GitHub :

**°Git** est un logiciel de gestion de versions. C'est à dire, un logiciel permettant de photographier à l'instant T les fichiers d'un dossier.

**°GitHub** est un service en ligne qui utilise Git, et qui permet entre autres de :

° Mettre en ligne ses dossiers Git (dans ce qu'on appelle "un repository").
° Collaborer à plusieurs sur un même dossier Git.

# **3. Le cours**
## **3.1. Git**

Nous allons maintenant voir :

**°** Comment installer Git sur ton ordinateur.

**°** Comment créer un dossier Git (repository).

**°** Comment faire une photographie (appelé "commit").

**°** Comment revenir à des versions précédentes.

## **3.1.1. Installation**

Pour installer Git, rien de plus simple : va sur le site du même nom dans la rubrique téléchargements, choisis ton OS, puis télécharge et installe le logiciel. Redémarre ton terminal, et voilà ! 

 ALERTE BONNE ASTUCE

Git est un logiciel **CLI** (Command Line Interface). Avec ce type de logiciels, tout passe par le terminal. Il s'oppose à **GUI**, Graphical _User Interface_.

Exemple : lorsque tu utilises la GUI de ton explorateur de fichiers, tu double-cliques sur un fichier pour l'ouvrir. Avec la CLI, tu tapes la commande $ open nom_du_fichier dans ton terminal. Autre exemple : pour créer un dossier en GUI, tu cliques droit -> nouveau dossier en GUI. En CLI, tu tapes $ mkdir nom_dossier dans ton terminal.

Bref, toutes les actions de ce cours traiteront de la CLI et passeront par le terminal avec les commandes que nous allons t'enseigner. Il existe des versions GUI pour Git, mais elles ne seront pas enseignées dans ce cours pour plusieurs raisons :

**°** Un peu comme Photoshop, la version GUI peut faire très peur avec ses milliers de boutons.

**°** Pas besoin d'avoir moult softwares installés : il suffit d'un terminal et à toi la gloire !

**°** Le but de cette semaine est de te donner les bases pour comprendre l'univers du développement. La version GUI n'étant pas utilisée par les devs, l'enseigner ne répond pas à notre vision : rendre l'univers du développement plus accessible.


Lance (ou relance) ton terminal, puis rentre la ligne suivante :

$ git --version

Le terminal devrait te renvoyer quelque chose comme : git version X.XX.X. S'il te renvoie un truc du genre command not found: git, c'est que tu n'as pas installé Git ou relancé ton terminal !

Pour se servir de Git, c'est simple : il suffit de rentrer dans le terminal les commandes $ git truc ou git machin pour lui faire exécuter truc ou machin. Voyons maintenant la commande permettant d'initialiser un dossier git.

## **3.1.2. Mise en place de ton dossier : git init et git status**

Avant de commencer, il faut dire au logiciel Git : "ceci est un dossier de travail correspondant à un projet. Initialise Git dans ce dossier stp". En gros, tu vas initialiser un _repository_ Git, ce qui te permettra de faire des photographies à l'instant T. Pour ceci, mets-toi dans un dossier de travail (avec la commande cd) et exécute la commande suivante :

$ git init
Initialized empty Git repository in /home/felix/Desktop/my_big_project/.git/

**ALERTE ERREUR COMMUNE**

Quand on débute dans le code, on a tendance à faire git init à la volée un peu partout. Il ne faut pas. Voici les types de dossiers dans lesquels tu dois initialiser des repository :

**°** Un dossier contenant le code de ton projet Google.

**°** Un dossier contenant le projet d'un site internet.

**°** Un dossier contenant un projet clair et défini.

Voici où **tu ne dois pas** faire git init :

**°** Le dossier qui contient tout ton ordinateur (exemple : exécuter git init en première ligne de commande de ton terminal).

**°** Ton dossier Desktop ou My Documents.

**°** Un dossier the_hacking_project contenant tous tes projets de THP.

**°** Un dossier qui contiendrait plusieurs dossiers de projets différents.

En général la _rule of thumbs_ est : un git init par projet. Si jamais tu as fait git init dans un dossier qui n'est pas bon, tu peux supprimer le dossier caché contenant toutes les informations de git en faisant :

$ rm -rf .git

Et maintenant, quelle est la commande la plus importante quand on manipule git ? Réponse : git status. Cette commande permet de te donner en un rien de temps l'état de ton projet git. Tu peux tester en entrant git status dans un repository git :

$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

Le logiciel git te dit actuellement qu'il n'y a rien dans ton dossier, et donc rien à photographier ("nothing to commit"). Voyons maintenant comment faire un commit, justement.

## **3.1.3. Faire un commit**

Un commit est une photographie à un instant T d'un projet. Pour faire court, tu vas prendre certains fichiers et les ajouter à la liste de ceux que tu veux photographier (cette liste peut aussi être vide). Ensuite, tu vas faire ta photographie en faisant git commit.

## **3.1.3.1. Ajouter un fichier avec git add**

Pour savoir quels fichiers git va prendre en photo, il faut les ajouter avec la commande git add :

$ git add nom_de_ton_fichier

Tu peux voir avec git status que ton fichier est bien ajouté.

## **3.1.3.2. Faire un commit avec git commit**

Maintenant que tu as ajouté tes fichiers à la liste, tu as juste à les prendre en photo avec la commande git commit :

$ git commit -m "I made a change this is a comment why I did it"

[master (root-commit) cfec956] change
 
 n files changed, m insertions(+), x deletions(-)
 create mode 100644 blabla

Et voilà comment marche le commit !

 **QUESTION RÉCURRENTE**

Mais dis-donc Jamy, pourquoi écrire git commit -m "mon commentaire" et pas git commit tout simplement ?
Excellente question. La commande git commit va ouvrir un fichier qui te demandera d'écrire un long message de commit avec Vim. Pas très pratique. Ainsi, comme l'option -l qui affiche les résultats de ls au format long, nous allons utiliser l'option -m qui permet d'écrire le message de commit directement dans la commande.

## **3.1.3.3. Exemple avec un petit projet**

Comme il n'est pas aisé d'expliquer les commits, je te propose un petit pas à pas pour t'aider à comprendre la notion de git ☺ Nous allons prendre l'exemple d'un site de restaurant.

Commence par créer un dossier restaurant_website, puis mets-toi dans le dossier avec ton terminal.

On commence toujours par initialiser son repository, donc entre la commande suivante :

$ git init

Initialized empty Git repository in /home/felix/ton_chemin/restaurant_website/.git/

Normalement, le dossier est vide et contient uniquement le dossier de configuration .git/ que tu n'as pas besoin de toucher (il s'affichera avec $ ls -a). Tu es fin prêt pour commencer ton projet.

D'abord, créons notre fichier index.html et ajoutons quelques lignes de HTML à l'intérieur :

<!DOCTYPE html>

<html>

<head>
 <title>À la bonne table</title>

</head>

<body>
 <h1>Ce est le site de mon restaurant !</h1>

</body>

</html>

Si tu fais la commande git status, ton terminal te dira ceci :

$ git status

On branch master

No commits yet

Untracked files:
 
 (use "git add ..." to include in what will be committed)

  index.html

nothing added to commit but untracked files present (use "git add" to track)

Cela veut dire qu'il a vu qu'un fichier index.html existe, et que ce dernier est _untracked_ (c'est à dire que le photographe ne le prend pas en compte). Pour pouvoir le "track", il faut faire git add :

$ git add index.html

Tu verras que ce dernier est prêt avec git status :

$ git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached ..." to unstage)

  
  new file:   index.html

Là, git a bien compris que le fichier index.html doit être photographié. Il sera donc bien pris en compte dans le prochain commit. Faisons ce commit, justement :

git commit -m "first commit // adding index.html"

[master (root-commit) 279d87c] first commit // adding index.html
 1 file changed, 9 insertions(+)
 create mode 100644 index.html

Et voilà tu viens de faire ton premier commit ! Poursuivons ce "pas à pas" avec deux autres commits qui vont t'apprendre :

**°** À faire un commit avec deux fichiers.
**°** La puissance des commits.

Nous allons maintenant ajouter du CSS à notre site. On va mettre les h1 en rouge. Dans un fichier styles.css, ajoute les lignes suivantes :

h1 {
  color: red;
}

Puis, dans le fichier index.html, branche le fichier css :

<link rel="stylesheet" href="styles.css">

Voilà, tu as mis le titre en rouge, tu peux faire un commit ! Petit rappel : il te faut ajouter les fichiers modifiés, puis faire le commit. Voyons les fichiers avec git commit :

$ git commit

On branch master

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

  styles.css

no changes added to commit (use "git add" and/or "git commit -a")

Git est très malin : il te dit que le fichier index.html a été modifié depuis le dernier commit, et qu'il y a un nouveau fichier pas encore _tracked_. Pour faire un commit, il nous faut ajouter les deux fichiers avec git add puis faire le commit :

$ git add index.html
$ git add styles.css

Si tu fais git status, tu peux voir l'état des fichiers :

$ git status

On branch master

Changes to be committed:
  (use "git reset HEAD ..." to unstage)

  modified:   index.html
  
  new file:   styles.css

Parfait, git nous dit que ces fichiers seront pris en compte lors du prochain commit. Nous n'avons plus qu'à faire notre commit :

$ git commit -m "h1 in red"

[master d25c926] h1 in red
 2 files changed, 5 insertions(+), 1 deletion(-)
 create mode 100644 styles.css

Super ! Tu viens de faire ton deuxième commit. Nous allons maintenant faire le troisième pour te montrer la puissance des commits, et de git status notamment.

Prenons le cas où tu es en train de travailler sur le menu de ton restaurant. Tu hésites entre des ol et des ul. Pour le moment, ton fichier index.html ressemble à ceci :

<!DOCTYPE html>

<html>

<head>
  <title>À la bonne table</title>
  <link rel="stylesheet" href="styles.css">

</head>

<body>
  <h1>Ceci est le site de mon restaurant !</h1>
  <h2>Le menu</h2>
  <ul>
   
   <li>Harengs pommes à l'huile</li>
    <li>Blanquette de veau</li>
    <li>TODO : trouver un dessert</li>
  
  </ul>

</body>
</html>

En pleine hésitation, un collègue arrive et te demande de mettre les h1 en text-align: center; et de faire un commit. Tu t'exécutes et change le fichier style.css. Si tu fais git status tu as :

$ git status

On branch master

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   index.html
  modified:   styles.css

no changes added to commit (use "git add" and/or "git commit -a")

Git te dit que tu as modifié deux fichiers, mais tu ne veux en commit qu'un seul, car ce vilain "TODO : trouver un dessert" n'a pas vraiment sa place dans le menu. Pour ceci, il faut que tu _add_ uniquement ton fichier styles.css pour faire un commit ne contenant que ce fichier :

$ git add styles.css

Si tu fais git status tu auras :

$ git status

On branch master

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  modified:   styles.css

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   index.html

Si tu as à peu près compris, git te dit que styles.css correspond au fichier qui sera dans le commit tandis que index.html ne sera pas pris en photo. C'est exactement ce que tu veux. Il ne te reste plus qu'à faire le commit :

git commit -m "text align center for h1"

[master c94cb3d] text align center for h1
 1 file changed, 2 insertions(+), 1 deletion(-)

Puis si tu fais git status, git te dira que index.html a été modifié mais n'est toujours pas prévu dans le prochain commit :

$ git status

On branch master

Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git checkout -- ..." to discard changes in working directory)

  modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

À travers cet exemple, j'espère que tu as compris la puissance du commit. C'est un outil super pratique pour faire des sauvegardes à un instant T de ton projet, ce qui a deux gros avantages :

C'est extrêmement puissant pour collaborer à plusieurs sur un même dossier : on sait qui a fait quoi, quand et pourquoi.
La capacité à pouvoir facilement revenir en arrière (ce que nous allons étudier dans la partie suivante).

## **3.1.4. Revenir en arrière**

Comme nous l'avons vu, Git permet non seulement de faire des sauvegardes propres de ses projets, mais aussi de revenir en arrière facilement. Pour remonter le temps, ça se passe en deux étapes :

**°** Déterminer la sauvegarde où je veux revenir.
**°** Déterminer la raison du retour arrière :

**°** Est-ce à titre purement indicatif, juste pour regarder ce qui a été fait avant ?
**°** S'agit-il d'un retour en arrière définitif ?

## **3.1.4.1. Regarder l'historique des versions**

La commande git log permet de connaitre les commits faits sur le projet. Par exemple pour ton projet de restaurant, git log ressemblerait à ceci :

$ git log
commit c94cb3d84163a5877dec566a92ffbdc05661a64c (HEAD -> master)

Author: felhix

Date:   Tue Jun 4 18:36:08 2019 +0200

    text align center for h1

commit d25c9262c0b019a0090cf0fe2f5b9159f5511b5c

Author: felhix

Date:   Tue Jun 4 18:23:52 2019 +0200

    h1 in red

commit 279d87c30637bf4aea24e6765a428c65b44ec7ab

Author: felhix

Date:   Tue Jun 4 17:51:46 2019 +0200

    first commit // adding index.html

Pour quitter le log, il faut appuyer sur Q.

Tu peux voir la liste des commits contenant les informations importantes :

**°** Qui a fait le commit.
**°** Quand le commit a été fait.
**°** Pourquoi ? (avec le message)
**°** Qu'est-ce qui a été commité ? (grâce au code bizarre)

Le code 100d6f07dbf4cfb9103b3819e64432186750a1a2 est le SHA du commit. C'est son identifiant unique. C'est ce qui te servira pour le retour en arrière.

## **3.1.4.2. Revenir en arrière**

Il y a deux façons de revenir en arrière :

**°** La première est à titre purement indicatif, et te servira seulement à observer un état précédent
**°**La seconde est un retour définitif en mode "je veux revenir à tel endroit pour retravailler à partir de là"

## **3.7.1. Retour en arrière à titre purement indicatif**

Imaginons que tu veux juste jeter un oeil sur un fichier à un instant T. Pour ceci, tu rentrerais la commande :

$ git checkout SHA

(en remplaçant "SHA" par le code que tu as eu lors du git log)

Tu peux ainsi naviguer dans l'ancienne version pour consulter les fichiers à cet instant T. Pas plus compliqué ! Pour revenir à la version actuelle, tu n'as qu'à faire :

$ git checkout master

 **ALERTE ERREUR COMMUNE**

N'utilise pas cette commande si tu veux faire des modifications sur un fichier. Si jamais tu fais ça, tu auras droit à une erreur te faisant atterrir sur l'un des threads les plus célèbres de Stack Overflow. Si jamais tu veux revenir en arrière pour faire des modifications, passe à la section suivante.

**ALERTE ERREUR COMMUNE**

git checkout ne marche que si tu n'as aucune modification non sauvegardée. Si tu es entre deux commits, git checkout te renverra cette erreur :

$ git checkout 100d6f07dbf4cfb9103b3819e64432186750a1a2           

error: Your local changes to the following files would be overwritten by checkout:
  index.html

Please commit your changes or stash them before you switch branches.
Aborting

Dans ce cas, 2 possibilités . faire une sauvegarde (== faire un commit), ou tout effacer pour revenir au commit d'avant.

## **3.7.2. Revenir en arrière définitivement**

Tu peux revenir en arrière définitivement avec la commande git reset qui s'utilise comme ceci :

$ git reset --hard SHA

(en remplaçant "SHA" par le code reçu lors du git log)

 **ALERTE BONNE ASTUCE**

La commande git reset est aussi un bon moyen pour effacer son travail actuel et revenir au commit précédent. Imagine par exemple que tu es en train de travailler sur la diapo de Jean-Michel. En plein milieu, tu te dis que ton approche est mauvaise et tu as soudain envie d'effacer tout ce que tu as fait jusqu'à présent. Plutôt que de faire CTRL + Z plein de fois, tu peux rentrer la commande suivante :

$ git reset --hard

Et hop ! Tu reviens à ton dernier commit. Très pratique pour tester des concepts à la volée, ou quand tu n'as pas envie de commit les changements que tu viens de faire.

## **3.2. GitHub**

Maintenant que tu es un champion du commit, nous allons voir comment mettre son code en ligne pour en faire profiter la terre entière, et pouvoir collaborer à plusieurs sur un projet.

Grâce à git et GitHub, tu peux "push" ton code en ligne en quelques lignes de commandes à peine. Dans cette partie, nous verrons :

**°** Qu'est-ce que GitHub, et comment créer un repository.
**°** La notion de remote pour Git : comment lier ton repository local à un repository en ligne.
**°** les deux commandes maitresses : git pull et git push.

## **3.2.1. C'est quoi GitHub**

GitHub est une plateforme permettant deux choses très importantes dans l'univers du code :

**°** Pouvoir lier un repository Git local (sur ton ordinateur) à un repository que tu as créé en ligne sur la plateforme Github (un peu comme avec DropBox). Nous allons voir dans cette ressource comment le faire.
**°** Pouvoir travailler en équipe sur un même repository. Nous verrons ça plus tard.

Un grand nombre d'entreprises utilisent GitHub pour travailler, ainsi qu'une grosse majorité des projets OpenSource. Le code de ReactJS, Bootstrap, ou encore Ruby on Rails ont leur code sur GitHub et tout le monde peut y contribuer !

Va sur GitHub et créé un compte. Ensuite, va créer un repository, ce qui devrait te renvoyer à l'écran suivant :


Ok, décortiquons tout ça calmement :

**°** Le Repository name est le nom de ton repository.

**°** La Description est... sa description.

**°** Tu peux choisir de le mettre public ou privé.

°Petite astuce : la plupart des gens sont un peu méfiants et préfèrent tout mettre en privé. Sur GitHub, tu n'as pas vraiment à te faire de soucis avec les repository publics. Au contraire, avoir des jolis repository en ligne montre que tu es actif sur la plateforme ! Un peu comme un CV, en quelque sorte.

°Tu peux l'initialiser avec un README qui permet d'expliquer ce qu'est le projet et comment s'en servir. Pour ce premier projet, tu peux t'en passer.

Si tu as bien tout fait, tu devrais avoir cet écran :


Laisse-moi te traduire ces lignes bizarres en quelque chose de plus compréhensible : en gros, GitHub te dit que ton repository est prêt et qu'il est vide pour le moment. Il te donne même les commandes pour le lier à un repository local, à coup de git remote add origin git@github.com:username/le_nom_de_ton_projet.git. Nous allons voir ensemble la notion de remote dans la prochaine partie.

## **3.2.2. La notion de remote**

Qu'est-ce qu'un "remote repository" ? C'est une version à distance de ton repo Git, un peu comme une copie stockée ailleurs (souvent sur Internet). Tu peux facilement faire "local -> remote" ou de "remote -> local" avec Git.

Avec git remote, tu peux facilement ajouter des remotes, voir la liste des remotes, enlever des remotes.

Il en existe plusieurs types :

**°** GitHub, plateforme qui te propose d'avoir un repository à distance, te permet aussi de partager ton travail à d'autres et de disposer d'une sauvegarde en cas de coup dur.

**°**Heroku, qui te permet de lui envoyer le code d'une application Rails pour qu'il la transforme en serveur (= qu'il la publie sur Internet);

**°**GitLab, similaire à GitHub;

**°**Et bien d'autres !

Chaque remote aura un nom. Ce nom peut être par exemple "other_github", "origin", "heroku", ou "jetaime". Par convention, le repo en ligne principal s'appelle "origin", d'où la commande $ git remote add origin ton_url avec laquelle tu ajoutes un "remote repository" sur Github nommé "origin", avec "ton_url" en guise d'adresse.

Pour voir tous les "remote repository" associés à ton dossier git, tu peux faire : $ git remote -v. Cette commande est très pratique car faire de la superposition de remotes est une erreur classique quand on débute.

Continuons l'exemple de notre restaurant. Dans l'écran de ton repo vide (voir image précédente), récupère la commande ressemblant à git remote add origin git@github.com:username/le_nom_de_ton_projet.git. Ensuite, dans ton terminal, va dans le dossier de ton restaurant puis colle la commande précédente. Tu devrais pouvoir voir les remote en tapant git remote --v :

git remote --v                                               

origin  git@github.com:felhix/ton_super_nom.git (fetch)

origin  git@github.com:felhix/ton_super_nom.git (push)

## **3.2.3. Git push**

La commande git push va envoyer ton code stocké en local vers un remote de ton choix. Elle s'utilise en faisant : $ git push nom_du_remote nom_de_la_branche. Si tu veux push ta branche "master" vers la remote "origin", tu feras donc :

$ git push origin master

Ou alors, si tu veux push ta branche "other_branch" vers la remote "heroku" tu feras :

$ git push heroku other_branch

 **QUESTION RÉCURRENTE**

Mais dis donc Jamy, c'est quoi une branche ?

Ce n'est pas l'objet du cours, mais je vais faire un petit aparté à ce sujet. Une branche, grosso modo, est une bifurcation de ton projet sur laquelle tu vas travailler de manière indépendante. Grâce à cette fonctionnalité super pratique, tu peux travailler sur une version parallèle de ton projet et la re-fusionner plus tard, quand tu seras content des modifications apportées. Jusqu'à maintenant, tu as seulement fait des commits sur la branche Master. Mais tu verras, la plupart des fonctionnalités te demanderont de travailler sur une branche plutôt que de faire des commits directement sur Master, afin d'éviter d'exposer à tes utilisateurs des fonctionnalités non terminées.


Prenons l'exemple de notre site. Tu voudrais reprendre les couleurs du menu, ce qui représente plusieurs jours de travail. Pour ceci, tu voudrais créer une branche nommée new_design sur laquelle tu vas faire plusieurs commits, puis montrer le design à ton client. Quand tu seras content, tu n'auras plus qu'à fusionner la branche new_design avec la branche master et à toi la gloire !

Pour le moment, nous n'allons pas utiliser les branches. Sache juste que ce système existe, et que tu vas travailler sur la branche principale nommée master.

 **QUESTION RÉCURRENTE**

**Je viens d'initialiser un repo mais quand je push sur GitHub, certains dossiers de mon repo n'apparaissent pas (mais le reste si). Pourquoi?**

S’il n’y a aucun fichier dans un dossier, Git ne "push" pas le dossier. Ne t'étonne donc pas si un dossier vide sur ton ordi n'apparait pas dans GitHub : dès qu'un fichier (Ruby ou autre) y sera ajouté avec $ git add puis "commité" et pushed, cette fois le dossier apparaîtra bien, avec le fichier qu'il contient.

## **3.2.4. Git pull**

La commande git pull est le contraire de git push : elle remplace le code en local avec celui de la remote de ton choix. Elle s'utilise de la manière suivante : $ git pull nom_remote nom_branche. Ainsi, si tu veux pull ta branche "master" depuis la remote "origin" tu feras :

$ git pull origin master

## **3.3. Les messages d'erreur**

On ne va pas se leurrer, Git n'est pas facile à utiliser quand on débute... Avant de te précipiter et de maudire ton ordinateur, nous allons annoncer quelque chose : c'est normal d'avoir des erreurs, surtout quand on commence. C'est arrivé à TOUT le monde, et surtout à ceux qui sont à l'aise aujourd'hui ❤ Le secret, c'est de ne pas désespérer, et de résoudre tes soucis calmement, un à un. Comme tout développeur est passé par ce chemin, les réponses aux problèmes classiques pullulent sur Stack Overflow. Copie-colle ton message d'erreur, lis les réponses, essaie de les comprendre, et trouve la solution à ton problème.

 **EXEMPLE ILLUSTRÉ**

Prenons l'exemple d'une erreur que j'ai eue à mes débuts sur git. J'avais un repo git en local que j'avais déjà lié à une remote origin qui était un repo GitHub. Je n'étais pas content de mon repo GitHub, donc je l'ai supprimé, avant d'en re-créer un. Puis j'ai voulu lier mon repo local à ce nouveau repo GitHub en utilisant $ git remote add origin url_du_repo. Sauf que :

<$ git remote add origin url_repo

fatal: remote origin already exists.

Oh mon dieu, Fatal !! En général, les erreurs sont en mode "error bug". Mais là, s'il est écrit "fatal", ça doit être grave, non ? Non. Une petite recherche Google du message d'erreur, et tu pourras découvrir que c'est juste un problème de remote origin qui existe déjà.

Bref, je ne te le cache pas : les erreurs, tu en auras. La clé de succès de The Hacking Project est justement ta capacité à bien les analyser, et à faire les bonnes recherches Google qui résoudront ton problème.

# **4. Points importants à retenir**
## **4.1. Les commandes pratiques**

Voici un récap des commandes de base :

**°** $ git init : il faut TOUJOURS commencer par initialiser git avec cette commande. C'est elle qui transforme ton répertoire courant en repository git.
**°** $ git add ton_fichier : ajoute aux sauvegardes le fichier mentionné.
**°** $ git commit -m "ton commentaire" : crée un commit (commit = sauvegarde suivie d'un commentaire).
**°** $ git status : te donne le statut actuel de git.

## **4.2. Lire l'historique**

$ git log : permet de voir l'historique de tous les commits, qui sont rangés par :

**°** SHA : liste de chiffres et lettres qui identifient de façon unique le commit.
**°** Auteur
**°** Date
**°** Message fourni lors du commit, qui doit être clair et précis pour te permettre de savoir ce que faisait au moment de cette sauvegarde.. C'est peut-être pénible, mais tu te remercieras plus tard.

Pour quitter le log, il faut appuyer sur Q.

## **4.3. Se positionner sur un commit donné**

Imaginons que l'on veuille vérifier un truc sur un vieux commit. On va utiliser la commande $ git checkout, utilisée comme ceci :

**°** $ git checkout 45581cebdd2cae494f80f44010af9e4a86c9b8fa : dit à git de se positionner sur ce SHA précis. Attention à ne pas faire de modifications !
**°** $ git checkout master : une fois que l'on a fini de se balader, il faut revenir à la version présente de notre repository avec cette commande.

Si tu veux revenir en arrière définitivement, tu utiliseras $ git reset --hard SHA.

**°** $ git reset --hard 45581cebdd2cae494f80f44010af9e4a86c9b8fa : on dit à git de se positionner sur ce SHA précis.
**°** $ git reset --hard : efface tout pour revenir au dernier commit.

# **5. Pour aller plus loin**

Le cours de OpenClassrooms sur Git est une très bonne ressource pour aller plus loin. Il explique notamment la notion de branches et de fusions.

Voici également un cours sur Git de la Viking Code School. Il explique bien les bases de Git et fournit une bonne alternative au nôtre.

