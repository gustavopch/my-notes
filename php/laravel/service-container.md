# Service container

## Binding

Within a service provider, you always have access to the container via the `$this->app` property.

**Simple binding:**

```php
$this->app->bind('HelpSpot\API', function ($app) {
  return new \HelpSpot\API($app->make('HttpClient'));
});
```

**Binding a singleton:**

```php
$this->app->singleton('HelpSpot\API', function ($app) {
  return new \HelpSpot\API($app->make('HttpClient'));
});
```

**Binding an existing instance:**

```php
$api = new \HelpSpot\API(new HttpClient);

$this->app->instance('HelpSpot\API', $api);
```

**Binding a primitive value:**

```php
$this->app->when('App\Http\Controllers\PurchaseController')
          ->needs('$reservationRadiusInMeters')
          ->give(5000);
```

**Binding an interface to a given implementation:**

```php
$this->app->bind(
  'App\Contracts\EventPusher',
  'App\Services\RedisEventPusher'
);
```

**Binding different implementations depending on the consumers:**

```php
$this->app->when(PhotoController::class)
          ->needs(Filesystem::class)
          ->give(function () {
            return Storage::disk('local');
          });

$this->app->when([VideoController:class, UploadController:class])
          ->needs(Filesystem::class)
          ->give(function () {
            return Storage::disk('s3');
          });
```

## Resolving

**Out of the container:**

```php
$api = $this->app->make('HelpSpot\API');
```

**Without access to the `$app` variable:**

```php
$api = resolve('HelpSpot\API');
```

**Not resolvable via the container:**

```php
$api = $this->app->makeWith('HelpSpot\API', ['id' => 1]);
```

**Automatically with type-hinting:**

```php
<?php

namespace App\Http\Controllers;

use App\Users\Repository as UserRepository;

class UserController extends Controller
{
  protected $users;
  
  public function __construct(UserRepository $users)
  {
    $this-> users = $users;
  }
}
```

**Obtaining the container with PSR-11 interface:**

```php
use Psr\Container\ContainerInterface;

Route::get('/', function (ContainerInterface $container) {
  $service = $container->get('Service');
});
```

