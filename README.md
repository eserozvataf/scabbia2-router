# Scabbia2 Router Component

[This component](https://github.com/eserozvataf/scabbia2-router) is a simple routing dispatcher which resolves and dispatchs the routes to callbacks or controllers.

[![Build Status](https://travis-ci.org/eserozvataf/scabbia2-router.png?branch=master)](https://travis-ci.org/eserozvataf/scabbia2-router)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/eserozvataf/scabbia2-router/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/eserozvataf/scabbia2-router/?branch=master)
[![Total Downloads](https://poser.pugx.org/eserozvataf/scabbia2-router/downloads.png)](https://packagist.org/packages/eserozvataf/scabbia2-router)
[![Latest Stable Version](https://poser.pugx.org/eserozvataf/scabbia2-router/v/stable)](https://packagist.org/packages/eserozvataf/scabbia2-router)
[![Latest Unstable Version](https://poser.pugx.org/eserozvataf/scabbia2-router/v/unstable)](https://packagist.org/packages/eserozvataf/scabbia2-router)
[![Documentation Status](https://readthedocs.org/projects/scabbia2-documentation/badge/?version=latest)](https://readthedocs.org/projects/scabbia2-documentation)

## Usage

### Creating route definitions

```php
use Scabbia\Router\RouteCollection;

$routes = new RouteCollection();

// adding a static route
$routes->addRoute('GET', '/about', 'AboutController::IndexAction');

// adding a static route with multiple http methods
$routes->addRoute(['GET', 'POST'], '/about', 'AboutController::IndexAction');

// adding a dynamic route
$routes->addRoute('GET', '/users/profile/{id:[a-z]+}', 'UsersController::ProfileAction');

// adding a dynamic route with a routing name
$routes->addRoute('GET', '/users/posts/{id:[a-z]+}', 'UsersController::PostsAction', 'user/posts');
```

### Saving route definitions

```php
file_put_contents('routes.json', json_encode($routes->save()));
```

### Loading route definitions back

```php
$routes = json_decode(file_get_contents('routes.json'));
```

### Dispatching a route

```php
use Scabbia\Router\Router;

$router = new Router($routes); // initialize a new router with route definitions
$route = $router->dispatch('GET', '/about');

if ($route['status'] === Router::FOUND) {
  call_user_func($route['callback'], ...$route['parameters']);
}
```

### Reverse Routing with names

```php
use Scabbia\Router\Router;

$router = new Router($routes); // initialize a new router with route definitions

echo $router->path('users/posts', [ 'id' => 'eser' ]);
```

## Links
- [List of All Scabbia2 Components](https://github.com/eserozvataf/scabbia2)
- [Documentation](https://readthedocs.org/projects/scabbia2-documentation)
- [Twitter](https://twitter.com/eserozvataf)
- [Contributor List](contributors.md)
- License Information [I](LICENSE-Apache) [II](LICENSE-Flask)


## Contributing
It is publicly open for any contribution. Bugfixes, new features and extra modules are welcome. All contributions should be filed on the [eserozvataf/scabbia2-router](https://github.com/eserozvataf/scabbia2-router) repository.

* To contribute to code: Fork the repo, push your changes to your fork, and submit a pull request.
* To report a bug: If something does not work, please report it using GitHub issues.
* To support: [![Donate](https://img.shields.io/gratipay/eserozvataf.svg)](https://gratipay.com/eserozvataf/)
