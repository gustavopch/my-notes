# Service providers

**Service providers** bootstrap and configure every feature: databases, queue, validation, routing etc. They are configured in the `providers` array of the `config/app.php` file.

- First, each provider has its `register` method called;
- Once all providers are registered, the `boot` method of each one is called.

Note that many of the providers will only be loaded when needed by the request.

## Writing service providers

Within the `register` method, you should **only bind things into the service container** — you should never attempt to register any event listeners, routes, or any other piece of functionality, otherwise you may accidentally use a service that is provided by a service provider which is not loaded yet.

```sh
php artisan make:provider MyServiceProvider
```

**A basic service provider looks like:**

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Riak\Connection;

class MyServiceProvider extends ServiceProvider
{
  public function register()
  {
    $this->app->singleton(Connection::class, function ($app) {
      return new Connection(config('foo'));
    });
  }
}
```

**You may also use the `bindings` and `singletons` properties instead of manually registering stuff:**

```php
<?php

namespace App\Providers;

use App\Contracts\DowntimeNotifier;
use App\Contracts\ServerProvider;
use App\Services\DigitalOceanServerProvider;
use App\Services\PingdomDowntimeNotifier;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
  public $bindings = [
    ServerProvider::class => DigitalOceanServerProvider::class,
  ];
  
  public $singletons = [
    DowntimeNotifier::class => PingdomDowntimeNotifier::class,
    ServerToolsProvider::class => ServerToolsProvider::class,
  ],
}
```

**Deferred service provider:**

```php
<?php

namespace App\Providers;

use Illuminate\Contracts\Support\DeferrableProvider;
use Illuminate\Support\ServiceProvider;
use Riak\Connection;

class MyServiceProvider extends ServiceProvider implements DeferrableProvider
{
  public function register()
  {
    $this->app->singleton(Connection::class, function ($app) {
      return new Connection(config('foo'));
    });
  }
  
  public function provides()
  {
    // Must return the service container bindings registered by the provider.
    return [Connection::class];
  }
}
```

