# Arrays

## Associative arrays

```php
<?php

// 1st way:
$a['key1'] = 'value1';
$a['key2'] = 'value2';

// 2nd way:
$a = array(
  'key1' => 'value1',
  'key2' => 'value2'
);

// 3rd way (PHP v5.4 and beyond):
$a = [
  'key1' => 'value1',
  'key2' => 'value2'
];
```

## Indexed arrays

```php
<?php

// 1st way:
$a = array();
$a[] = 'position0';
$a[] = 'position1';

// 2nd way:
$a = array(
    'position0',
    'position1'
);

// 3rd way (PHP v5.4 and beyond):
$a = [
    'position0',
    'position1'
];
```

## Iterating

```php
<?php

$a = [
    'foo',
    'bar'
];

// Access only the value:
foreach ($matrix as $value) {
    echo $value;
}

// Access both key and value:
foreach ($a as $key => $value) {
    echo "$key: $value";
}
```

