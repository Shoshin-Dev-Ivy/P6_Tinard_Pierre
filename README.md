# P6_Hot Takes #

## Contexte: ##
Création d’une API sécurisée pour une pour une application d'évaluation de sauces.

## Etapes techniques: ##

### Étape 1 => Démarrer le serveur backend: ###
- Créer un projet vide pour démarrer le serveur Node.js ;

- Installer Express ;

- Installer Mongoose.

À partir de la version 4.16 d'Express, bodyparser est inclus.

Utilisez ( express.json() ) pour analyser le corps de la requête.

#### Les problèmes à connaître : ####
- Si le port 3000 est utilisé par un autre processus, redémarrez complètement
  l'ordinateur (pour permettre l'utilisation du port), ou changez le port utilisé
  dans l’application Express.

- Impossible de se connecter à MongoDB.

- Vérifier la chaîne de connexion, le nom d'utilisateur et le mot de passe de MongoDB.

- Vérifier que MongoDB Atlas (ou un service similaire) autorise toutes les adresses IP
  à se connecter au cluster.

### Étape 2 => Construire le parcours utilisateur: API ###
Créez les éléments suivants :

- Modèle d'utilisateur ;

- Parcours utilisateur ;

- Contrôleur d'utilisateur.

L'utilisateur est en mesure d'effectuer les opérations suivantes :

  - Créer un compte ;

  - Se connecter et disposer d'un token valide.

#### Les problèmes à connaître : ####
- hacher le mot de passe.

- Un utilisateur peut s'inscrire plusieurs fois avec la même adresse électronique

  => vérifier qu’une adresse électronique est unique.

### Étape 3 => Démarrer le middleware: API ###
- Ajout de multer pour les images.

- Ajout d’authorize pour la validation des tokens.

- Authorize doit être ajoutée avant de commencer à construire le parcours pour les sauces.

- L'authentification est nécessaire pour qu'un utilisateur puisse effectuer une action
  sur le parcours des sauces.

#### Les problèmes à connaître : ####
- Les images importées sont manquantes.

- Multer n'est pas correctement configuré.

- Le chemin statique n'a pas été ajouté à l'application pour fournir les images.

- Assurez-vous d'ajouter le chemin statique à l'application.

### Étape 4 => Construire la route Sauce de l’API: API ###
Créez les éléments suivants :

- Le Modèle Sauce ;

- La Route Sauce ;

- Le Contrôleur Sauce.

- Autorisez toutes les fonctions en utilisant middleware Authorize.

L'utilisateur est en mesure d'effectuer les opérations suivantes :

- Ajouter une nouvelle sauce ;

- Supprimer une sauce ;

- Voir toutes les sauces.

#### Les problèmes à connaître : ####
- Erreur 401 (l'utilisateur n'est pas autorisé).

- Multer ne sauvegarde pas les images.

- Les images ne sont pas affichées sur le frontend.

### Étape 5 => Terminer la route Sauce de l’API: API complété ###
Exécuter l'application en tant qu'utilisateur pour vérifier que toutes
les fonctions ont été correctement mises en œuvre, tester :

Les deux types de demandes :

- Avec un fichier présent ;

- Sans fichier.

Les trois scénarios de la fonction « like » (1, 0, -1) ;

- L’utilisateur peut liker ou ne pas aimer une sauce (ou aucun des deux)

- Seul le propriétaire de la sauce peut modifier ou supprimer une sauce existante.

#### Les problèmes à connaître : ####
- Erreur 401 (l'utilisateur n'est pas autorisé).

- Multer ne sauvegarde pas les images.

- Les images ne sont pas affichées sur le frontend.

- Les données ne sont pas modifiées lorsque l'utilisateur tente
  de modifier une sauce existante.

- La fonction « modifier » échoue lorsqu'une image est téléchargée
  ou modifiée.

- La fonction « like » échoue lorsque l'utilisateur essaie de liker
  ou de ne pas aimer une sauce plusieurs fois.

- Le propriétaire de la sauce ne peut pas voir les boutons « modifier »
  et « supprimer ».

- L'identifiant de la Sauce doit être valide et ne pas contenir de faute de frappe,
  car seul le propriétaire de la Sauce peut la modifier ou la supprimer.

## API Routes: ##
Toutes les routes sauce pour les sauces doivent disposer d’une autorisation,

(le token est envoyé par le front-end avec l'en-tête d’autorisation : « Bearer <token> »).

Avant que l'utilisateur puisse apporter des modifications à la route sauce,
le code doit vérifier si l'userId actuel correspond à l'userId de la sauce.

Si l'userId ne correspond pas, renvoyer « 403: unauthorized request. »

Cela permet de s'assurer que seul le propriétaire de la sauce peut apporter
des modifications à celle-ci.

## Data ModelsSauce: ##
- userId : String — l'identifiant MongoDB unique de l'utilisateur qui a créé
  la sauce

- name : String — nom de la sauce

- manufacturer : String — fabricant de la sauce

- description : String — description de la sauce

- mainPepper : String — le principal ingrédient épicé de la sauce

- imageUrl : String — l'URL de l'image de la sauce téléchargée par l'utilisateur

- heat : Number — nombre entre 1 et 10 décrivant la sauce

- likes : Number — nombre d'utilisateurs qui aiment (= likent) la sauce

- dislikes : Number — nombre d'utilisateurs qui n'aiment pas (= dislike)
  la sauce

- usersLiked : [ "String <userId>" ] — tableau des identifiants des utilisateurs
  qui ont aimé (= liked) la sauce

- usersDisliked : [ "String <userId>" ] — tableau des identifiants des utilisateurs
  qui n'ont pas aimé (= disliked) la sauce Utilisateur

### Utilisateur: ###
- email : String — adresse e-mail de l'utilisateur [unique]

- password : String — mot de passe de l'utilisateur haché

## Exigences de sécurité: ##
- Le mot de passe de l'utilisateur doit être haché.

- L'authentification doit être renforcée sur toutes les routes sauce requises.

- Les adresses électroniques dans la base de données sont uniques et un plugin Mongoose
  approprié est utilisé pour garantir leur unicité et signaler les erreurs.

- La sécurité de la base de données MongoDB (à partir d'un service tel que MongoDB Atlas)
  ne doit pas empêcher l'application de se lancer sur la machine d'un utilisateur.

- Un plugin Mongoose doit assurer la remontée des erreurs issues
  de la base de données.

- Les versions les plus récentes des logiciels sont utilisées avec des correctifs
  de sécurité actualisés.

- Le contenu du dossier images ne doit pas être téléchargé sur GitHub.

## Structure du projet: ##
/ backend   # Node.js, Express, MongoDB
/ frontend  # Angular 13

## Remarques / points particuliers: ##
- Le backend utilise Mongoose 7

- CORS gérés dans app.js

- Angular 13 pour le frontend, service Auth pour communiquer avec le backend

## Intallation du projet en local et lancement de la page Hot Takes: ##

### 1ère étape => cloner le projet en local: ###
Sur le repository P6_Tinard_Pierre, cliquez sur < > code => (copy url to clipboard):

https://github.com/Shoshin-Dev-Ivy/P6_Tinard_Pierre.git

Dans un éditeur de code, (exemple: VS CODE), ouvrez un terminal:

cd Documents: git clone https://github.com/Shoshin-Dev-Ivy/P6_Tinard_Pierre.git

Ensuite open folder => P6_Tinard_Pierre

### 2ème étape => création base de données Hot Takes: ###
Sur https://cloud.mongodb.com/:

Créer un projet P6 Hot Takes, (name et password) => créer un cluster, le nommer P6HotTakes:

- Sélectionner Free

- Cloud Provider & Region => AWS, Paris (eu-west-3)

- Cluster Capacity => 0 - 100 Ops/Sec, 512 MB Storage

- Additional Settings => MongoDB 8.0, No Backup

- Cluster Details => P6HotTakes

Cliquer sur `Connect` => `Drivers`

1) Connecting with MongoDB Driver => select Node.js

2) Install your driver => dans 

=> ~/Documents/Github/shoshin-dev-ivy/P6_Tinard_Pierre/back$ npm install mongodb

3) Add your connection string into your application code

Dans la partie backend, créer un fichier .env, et y ajouter les fichiers suivants:

=> MONGOOSE_KEY='mongodb+srv://ShoshinDevIvy:<password>@p6hottakes.xbqmiyp.mongodb.net/p6hottakes?retryWrites=true&w=majority&appName=P6HotTakes'

Changer <password> par le mot de passe créé pour accéder à MongoDB.

=> TOKEN_KEY='RANDOM_TOKEN_SECRET'

### 3ème étape => lancement du Back-end, appel à l'API: ###
- Dans un terminal, aller dans la partie back, et installer npm:

~/Documents/Github/shoshin-dev-ivy/P5_Tinard_Pierre/back $ npm install

- Lancer l'appel à l'API:

~/Documents/Github/shoshin-dev-ivy/P5_Tinard_Pierre/back $ npm start

Listening on port 3000: ✅ Connexion à MongoDB réussie !

### 4ème étape => lancement du Front-end, accès page Hot Takes: ###
- Dans un terminal, aller dans la partie frontend, et installer @angular/cli@13:

~/Documents/Github/shoshin-dev-ivy/P5_Tinard_Pierre/frontend $ npm install @angular/cli@13

~/Documents/Github/shoshin-dev-ivy/P5_Tinard_Pierre/frontend $ npm start

** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **

✔ Compiled successfully.

La page Hot Takes est accessible, lié au Backend du P6HotTakes.

- Vous pouvez créer plusieurs utilisateurs:

- Ils pourront créer des sauces, avec images, et mettre un like ou l'enlever sur toutes les sauces créees.

