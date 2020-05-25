# Middleware

```php
<?php

namespace App\Http\Middleware;

use Closure;

class MyMiddleware
{
  public function handle($request, Closure $next)
  {
    // Perform some action when the request is coming in...
    
    $response = $next($request);
    
    // Perform some action when the response is going out...
    
    return $response;
  }
}
```

**Global middleware:** append the middleware to `$middleware` at `app/Http/Kernel.php`.

**Route-specific middleware:** append the middleware to `$routeMiddleware` at `app/Http/Kernel.php` and use it in the route:

```php
// Using the middleware name
Route::get('admin/profile', function () {
  //
})->middleware('foo', 'bar');

// Using the middleware fully qualified class name
Route::get('admin/profile', function () {
  //
})->middleware(Foo::class);
```

**Middleware groups:** append the middlewares list to `$middleware` at `app/Http/Kernel.php` and use it in the route:

```php
Route::get('/', function () {
  //
})->middleware('web');

Route::group(['middleware' => ['web']], function () {
  //
});

Route::middleware(['web', 'subscribed'])->group(function () {
  //
});
```

**Middleware parameters:** define the middleware:

```php
<?php

namespace App\Http\Middleware;

use Closure;

class CheckRole
{
  public function handle($request, Closure $next, $roles)
  {
    if (!$request->user()->hasRole($roles)) {
      // Redirect...
    }
    
    return $next($request);
  }
}
```

And use a `:` to separate the middleware name from the parameters:

```php
Route::get('/users', function () {
  //
})->middleware('role:admin,editor')
```

