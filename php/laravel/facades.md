# Facades

A facade is a class that provides access to an object from the container in a terse syntax.

For example, the `Cache` facade could be used like:

```php
Cache::get('user')
```

While it seems that we are calling a static `get` method from `Cache`, our call is actually handled by the magic `__callStatic` method on `Facade`. Our `Cache` class extends `Facade` and provided an implementation for `getFacadeAccessor`:

```php
class Cache extends Facade
{
  protected static function getFacadeAccessor() {
    return 'cache';
  }
}
```

## Real-time facades

To generate a real-time facade, prefix the namespace of the imported class with `Facades`:

```php
<?php

namespace App;

use Facades\App\Contracts\Publisher;
use Illuminate\Database\Eloquent\Model;

class Podcast extends Model
{
  public function publish()
  {
    $this->update(['publishing' => now()]);
    
    Publisher::publish($this);
  }
}
```

