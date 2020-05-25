# Requests

**Retrieving only the path**:

```php
$uri = $request->path();
// => 'foo/bar' given that we are at 'https://domain.com/foo/bar'
```

**Checking if the path matches a pattern:**

```php
if ($request->('admin/*')) {
  //
}
```

**Retrieving the URL:**

```php
$urlWithoutQueryString = $request->url();

$urlWithQueryString = $request->fullUrl();
```

**Retrieving the request method:**

```php
$method = $request->method();

$isPost = $request->isMethod('post');
```

**Retrieving input data:**

```php
$name = $request->input('name');

$name = $request->input('products.0.name');

$names = $request->input('products.*.name');

$archived = $request->boolean('archived');

// All as a simple array
$input = $request->all();

// All as an associative array
$input = $request->input();

// Portion
$input = $request->only('username', 'password');
$input = $request->only(['username', 'password']);
$input = $request->except('credit_card');
$input = $request->except(['credit_card']);
```

**Retrieving query string data:**

```php
$name = $request->query('name', 'Default Name');

// All as an associative array
$query = $request->query();
```

**Retrieving input via dynamic properties:**

```php
// Will first search in the request payload, then in the route parameters
$name = $request->name;
```

**Checking if input value is present:**

```php
$hasName = $request->has('name');

$hasNameAndEmail = $request->has(['name', 'email']);

$hasNameOrEmail = $request->hasAny(['name', 'email']);

$isNameFilled = $request->filled('name');

$isNameMissing = $request->missing('name');
```

**Uploaded files:**

```php
$photo = $request->file('photo');

$photo = $request->photo;

$hasPhoto = $request->hasFile('photo');

$isPhotoValid = $request->photo->isValid();

$path = $request->photo->path();

$extension = $request->photo->extension();

// Store with automatically generated name
$path = $request->photo->store('images', 's3');

// Store with explicit name
$path = $request->photo->storeAs('images', 'filename.jpg', 's3');
```

