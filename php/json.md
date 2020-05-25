# JSON

```php
<?php

// Get JSON string from a POST
$json = $_POST['json'];

// Turn the JSON string into an object
$obj = json_decode($json);

// Turn the JSON string into an associative array
$arr = json_decode($json, true);

// Turn an object into a JSON string
$obj = new Dog();
$json = json_encode($dog);
```

