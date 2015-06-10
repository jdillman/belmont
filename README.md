# Simple PHP web framework

Includes regex router, a 1-way data binding model and template-less templates

```php
<?php

require('Belmont.class.php');

// Configure the framework
$config = array(
  'tracking' => true,
  'stream' => false
);

// Set the routes
$routes = array(
  '/about' => 'AboutController',
  '/explore/([^/])+' => 'ProjectController',
  '/users/([0-9])+' => 'UserController',
  '/test' => function ($request) {
    return 'Inline Function Handler';
  },
  '/([^/]+)' => 'HomeController'
);

// Initialize the framework
$belmont = new Belmont($routes, $config);

// Handle the request
$response = $belmont->handleRequest();

// Send the response!
$response->send();
```

## Routes
Maps a url to a to a controller, use {} to tokenize values

```php

// Specify which controller and methods the route is for
$routes['/user/{id:[0-9]+}'] = array(
  'controller' => 'UserController',
  'methods' => 'GET|POST'
);

// Or specify the controller
$routes['/user/{id:[0-9]+}'] = 'UserController';

// Or use a callback
$routes['/user/{id:[0-9]+}'] = function ($request, $params) {
  return 'Inline handler';
};

$belmont->addRoute($routes)
```

## Controllers
Takes a request and generates a response

## Models
Data binding

## Templates
Just use PHP!

2 variables are available to templates, $html and $model;

$html is a helper class to build markup
$model is the data available to the template

```php`
// /belmont/templates header.html.tpl
echo '<h1>Header</h1>';
echo $html->p($model->get('name'));
echo $html->makeLink('/user/' . $model->get('uid'));
```

