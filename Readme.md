# Notes sur Symfony

### À propos

- Ce projet devra être composé de :
  - Un framework recréé avec la logique de Symfony pour me permettre d'avoir une meilleure idée du fonctionnement de Symfony.
  - Des notes sur des notions importantes à comprendre sur Symfony.

*Projet influencé par la série de vidéos de Lior CHAMLA : [On recrée Symfony](https://www.youtube.com/watch?v=RIZiOGjOsQI&list=PLpUhHhXoxrjdk6VgTUrunQNlVZizBU4WF)*\
*La documentation officielle Symfony [ici](https://symfony.com/doc/current/create_framework/index.html)*

## Chaînage d'un Projet Symfony 

- (À pousser bien plus tard)

## Notions Importantes de Symfony

### HTTP Foundation

- Centralise les requêtes et réponses HTTP.
- Une Request est composé d'un <u>tableau d'attributs </u> qui a pour vocation de stocker des éléments et est composé de $_GET, $_POST, $_SERVEUR etc...
  
- Méthodes courantes :
  - Requête : 
  	- GET &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: `$request->`<u>`query`</u>`->get('param');` 
	- POST &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: `$request->`<u>`request`</u>`->get('param');`
	- ATTRIBUTES : `$request->`<u>`attributes`</u>`->get('param');`
	
  - Réponse : `$response->headers->set('header', 'value')`, `$response->setContent('content')`, `$response->send()`

### Mise en Cache 

- Techniques de base et avancées (HTTP caching, ESI, cache applicatif).

### Front Controller PF

- Centralise le traitement des requêtes dans `index.php`.

### Serveur

- Options de serveur Symfony pour le développement local : `symfony server:start --port=8000`.
- Une option de base du serveur Symfony est notamment de renvoyer les requêtes vers le dossier `public` où se trouve notre `index.php`.

### `extract()`

- Utilisé pour extraire des variables à partir d'un tableau associatif.

### Symfony Routing 

- Définit des routes (dans symfony ça passe par `config/routes.yaml`).

### Méthode sans Symfony Routing

- On utilise `$request->getPathInfo()` pour déterminer la route actuelle :
	```php
	<?php
	$map = [ // on a nos différents chemins
		'/chemin1' => 'chemin1.php',
		'/chemin2' => 'chemin2.php'
	];

	// on vérifie l'URL de la requête
	$pathInfo = $request->getPathInfo();

	if (isset($map[$pathInfo])) { // si le fichier voulu existe, on le charge

		// ON CHOISIT DE COMMENCER ICI LA MISE EN CACHE
		ob_start();

		// ON INCLUDE NOTRE CONTENU VOULU
		include __DIR__ . '/../exemple_directory/' . $map[$pathInfo];

		// ON STOPPE LA MISE EN CACHE ET ON PRÉPARE LE CONTENU DANS NOTRE RÉPONSE
		$response->setContent(ob_get_clean());

	} else { // si le fichier n'existe pas, on renvoie une page erreur 404

		$response->setContent('La page demandée n\'existe pas');
		$response->setStatusCode(404);
	}

	// Puis on envoie la réponse
	$response->send();
	?> 
	```

	- ### Méthode avec symfony routing : PF

	```php
	<?php
	// CODE A RAJOUTER => COMMENTER EXPLICATION ROUTECOLLECTION, ADD(), RESSOURCENOTFOUNDEXDCEPTION, URLMATCHER, MATCH()...
	?> 
	```
	
### Callables / Controller PF

- C'est une pratique utilisé pour permetre à une chaine de caractère, un tableau et une classe de renvoyer vers une fonction ou une méthode.

	- On verra est alors qu'il est possible d'améliorer le système de routes pour renvoyer non le nom d'un fichier mais une méthode via un Callable, dans Symfony on parlera alors de <u>controller</u>  
	
	```php
	//CODE A RAJOUTER
	// $routes->add('chemin1')
	// var_dump($urlMatcher->match($request->getPathInfo()));
	
	// ON STOCK LA CLASSE ET LA METHOD VOULU DANS UNE VARIABLE
	$callable = [new NewClass, 'myMethod']

	// AVEC CES DEUX FACONS ON PEUT APPELLER LA METHOD ET PASSER UNE/DES VALEURS EN PARAMETRE
	// 1
	$callable('param');
	// 2
	call_user_func($callable, 'param');
	```

### Autoload PF

//...

### Resolver PF

//...
- Dépendance PHP
- Controller resolver : 
	-  Va permettre renvoyer vers une méthode à partir des attributs de `Request`
- Argument resolver : 
	- //.. fait de préciser le string et objet en paramètre pour obtenir les bons arguments (revoir 19:00 #5), (à pousser mais pas à trop comprendre en détail => c'est magique en gros)

### Configuration et Environnements PF

- Fichiers de configuration : `config/services.yaml`, `config/packages/*.yaml`.
- Gestion des environnements : `dev`, `prod`, `test`.

### Services et Dépendances F

- Conteneur de services pour la gestion des dépendances.
- Définition de services personnalisés.

### Sécurité PF

- Gestion de l'authentification et de l'autorisation.
- Configuration des rôles utilisateurs et des firewall.
 
### Tests PF

- Utilisation de PHPUnit pour les tests unitaires, fonctionnels et d'intégration.
- Outils Symfony pour faciliter les tests.
- (Comprendre plus tard l'utilité de faire des tests sur Symfony)

