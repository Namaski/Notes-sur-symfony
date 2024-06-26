# Notes sur Symfony

## Chainage d'un Projet Symfony 

- (A pousser bien plus tard)

## Notions Importantes de Symfony

### HTTP Foundation

- Centralise les requêtes et réponses HTTP.
- Méthodes courantes :
  - Requête : `$request->query->get('param')`, `$request->request->get('param')`
  - Réponse : `$response->headers->set('header', 'value')`, `$response->setContent('content')`, `$response->send()`

### Mise en Cache

- Techniques de base et avancées (HTTP caching, ESI, cache applicatif).
- 

### Front Controller

- Centralise le traitement des requêtes dans `index.php`.

### Serveur

- Options de serveur Symfony pour le développement local : `symfony server:start --port=8000` .
- Une option de base du serveur symfony est nottament de renvoyer les rêquete vers le dossier `public` où se trouve notre `index.php`

### `extract()`

- Utilisé pour extraire des variables à partir d'un tableau associatif.

### Symfony Routing

- Définit des routes dans des fichiers de configuration (`config/routes.yaml`).

	- ### Méthode sans symfony routing :

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

	- ### Méthode avec symfony routing :

	```php
	<?php
	// CODE ICI
	?> 
	```
	
### Tests

- Utilisation de PHPUnit pour les tests unitaires, fonctionnels et d'intégration.
- Outils Symfony pour faciliter les tests.
- (Comprendre plus tard a quoi sert de faire des test sur Symfony)

### Configuration et Environnements

- Fichiers de configuration : `config/services.yaml`, `config/packages/*.yaml`.
- Gestion des environnements : `dev`, `prod`, `test`.

### Services et Dépendances

- Conteneur de services pour la gestion des dépendances.
- Définition de services personnalisés.

### Sécurité

- Gestion de l'authentification et de l'autorisation.
- Configuration des rôles utilisateurs et des firewall.

 


