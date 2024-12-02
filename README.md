# TCAntisèche

Le but de ce repo est de créer une compilation de fiches pour nous aider dans nos révisions, en passant par des outils rendant leur édition et la collaboration les plus intuitifs possibles.

## Get started

#### 0 - Condition préliminaire
Pour pouvoir partager vos notes, il faudra un accès en écriture au repo Git. Pour l'obtenir, envoyez moi un mail à [matheo.d91@gmail.com](mailto://matheo.d91@gmail.com). Sinon, vous pouvez vous contenter de consulter ces notes.
### Installation sur PC/Mac/Linux

#### 1 - Installer Obsidian 
En suivant [**> ce lien <**](https://obsidian.md/download), c'est un super éditeur de texte qui fait vraiment super bien son taf.

#### 2 - Cloner le repo
Clonez le repo n'importe où sur votre disque, peut importe le moyen (GitHub Desktop reste le moyen le plus simple)

#### 3 - Installation des plugins 
Ouvrez Obsidian et ouvrez le dossier du repo git en tant que vault. Rendez vous ensuite dans les paramètres, puis la la section `Community Plugins`, cliquez sur `Browse` puis cherchez et installez `Git`. Pensez à l'activer.

#### 4 - C'est parti !
L'icone du contrôle de source (Git) est apparu en bas de la barre d'outils à gauche. Cliquez dessus pour utiliser la collaboration.

### Installation sur un téléphone 

#### 1 - Création d’un PAT
Rendez vous sur le site de GitHub, dans vos paramètres ([à cette adresse](https://github.com/settings/tokens) - `paramètres développeurs` > `Personnal Access Token` > `fined-gained token`, et générez un token ayant accès seulement à ce repo, avec les permissions suivantes :
- code
- commits
- statuses
- merge queues
- pull requests 
- Metadata
- Custom properties (read only)
Mettez son expiration sur jamais (ou autre si vous savez ce que vous faites) et copiez le, en le gardant au chaud quelque part. 

#### 2 - Installation de Obsidian
Utilisez simplement votre magasin d’application habituel (AppStore ou PlayStore)

#### 3 - Récupération du repo dans Obsidian 
Lancez obsidian, et créez un Vault avec le nom de ce repo (`TCAntiseche`). 
Ouvrez ensuite le panneau de gauche pour accéder aux paramètres, allez dans l’onglet `Community Plugins` et activez les. 
Installez et activez le plugin `Git`.
Avec le bouton en bas à droite, ouvrez la barre d’outils puis la palette de commande et tapez `clone`.
Sélectionnez `Git: clone an existing repo`
Entrez l’URL, qui est `https://PAT@@github.com/PetchouDev/TCAntiseche`
Pour le chemin d’accès, laissez le champ vide et appuyez sur entrée. 
Si Obsidian vous demande si vous voulez cloner dans la racine du Vault, répondez `Yes`.
Si il vous demande si le repo a déjà un dossier `.obsidian`, répondez `NO`.
Enfin, garder la profondeur de clonage  par default en appuyant sur entrée. 

#### 5 - Configuration du plugin 
Pour pouvoir partager vos modifications, il faudra réaliser cette étape supplémentaire car contrairement à un ordinateur, votre téléphone n’a pas de Git system-wide. 

Pour cela, il faut chercher l’onglet de configuration spécifique du plugin dans les paramètres, et descendre dans la section `Authentification` et compléter avec les informations adaptées. 

Remplacez votre mot de passe par votre PAT. 
#### 4 - Let’s go !
Tout devrait être bon, envoyez moi un message ou un mail si vous avez du mal. 



## Utilisation du plugin Git

Le plugin est disponible depuis la palette de commande ou la barre d’outils (à gauche sur l’application de bureau, en cliquant sur la grille en bas à droite sur mobile)

#### Mettre à jour depuis le repo
Cliquez sur l'icone avec la flèche vers le bas (fetch) pour récupérer les dernières modifications du repo. 

#### Envoyer vos modifications
Dans la liste `Changes`, cochez les fichiers que vous voulez envoyer pour les placer dans la liste `Staged Changes`. 
Cliquez ensuite sur le bouton `Commit` (la coche) pour valider vos modifications. 
Enfin, cliquez sur le bouton `Push` (boutton avec la flèche vers le haut, devenu violet) pour envoyer vos modifications sur le repo.

#### Tout faire d’un coup
Le super bouton (flèche vers le haut dans un cercle) réalise toutes les opérations d’un coup. 
À savoir dans l’ordre  `Fetch`, `Pull`, `Commit` et `Push`.
