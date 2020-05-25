# Routing

**Basic usage:**

```php
Route::get('foo', function () {
  return 'Hello World';
});

Route::match(['get', 'post'], '/', function () {
  //
});

Route::any('/', function () {
  //
});
```

**Redirects:**

```php
Route::redirect('/here', '/there');

Route::permanentRedirect('/here', '/there');
```

**Views:**

```php
Route::view('/welcome', 'welcome');

Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

**Route parameters:**

```php
// Required parameter
Route::get('user/{id}', function ($id) {
  //
});

// Optional parameter
Route::get('user/{name?}', function ($id) {
  //
});

// Regex constraint
Route::get('user/{id}/{name}', function ($name) {
  //
})->where(['id' => '[0-9]+', 'name' => '[A-Za-z]+']);
```

**Global constraints:**

```php
class RouteServiceProvider extends ServiceProvider
{
  // ...
  
  public function boot()
  {
    Route::pattern('id', '[0-9]+');
    
    parent::boot();
  }
}
```

**Named routes:**

```php
Route::get('user/profile', 'UserProfileController@show')->name('profile');

// Generating URLs...
$url = route('profile');

// Generating redirects...
return redirect()->route('profile');

// Checking route...
if ($request->route()->named('profile')) {
  //
}
```

**Route prefixes:**

```php
Route::prefix('admin')->group(function () {
  Route::get('users', function () {
    // Matches "/admin/users"
  });
});
```

**Current route:**

```php
$route = Route::current();

$name = Route::currentRouteName();

$action = Route::currentRouteAction();
```

## Route binding

**Implicit binding:**

```php
Route::get('users/{user}', function (App\User $user) {
  return $user->email;
});
```

**Custom column:**

```php
Route::get('posts/{post:slug}', function (App\Post $post) {
  return $post;
});
```

