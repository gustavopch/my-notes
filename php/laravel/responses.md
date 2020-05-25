# Responses

**String or array will be converted to full response:**

```php
Route::get('/', function () {
  return 'Hello World';
});

Route::get('/', function () {
  return [1, 2, 3];
});
```

**Creating full response manually:**

```php
return response('Hello World', 200)
               ->header('Content-Type', 'text/plain')
               ->header('X-Header-One', 'Foo');

return response('Hello World', 200)
               ->withHeaders([
                 'Content-Type' => 'text/plain',
                 'X-Header-One' => 'Foo',
               ]);
```

**Attaching cookies:**

```php
return response($content)
               ->cookie('name', 'value', $minutes);
```

**Redirecting:**

```php
return redirect()->route('profile', [$user]);

return redirect()->action('HomeController@index');

return redirect()->away('https://www.google.com');
```

**JSON:**

```php
return response()->json([
  'name' => 'Abigail',
  'state' => 'CA',
]);
```

**File downloads:**

```php
return response()->download($pathToFile);

return response()->download($pathToFile, $name, $headers);

return response()->download($pathToFile)->deleteFileAfterSend();
```

**Streamed downloads:**

```php
return response()->streamDownload(function () {
  echo GitHub::api('repo')
             ->contents()
             ->readme('laravel', 'laravel')['contents'];
}, 'laravel-readme.md');
```

**File response (without initiating a download):**

```php
return response()->file($pathToFile);
```

