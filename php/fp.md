# Functional programming

PHP supports first-class functions: a function can be assigned to a variable.

## Closures

```php
<?php

$add = function ($x) {
    // Note that the "use" keyword determines what will be
    // acessible by the inner function.
    return function ($y) use ($x) {
        return $x + $y;
    };
};

$addOne = $add(1);

echo $addOne(2); // => 3
```

## Filtering an array

```php
<?php

$input = [1, 2, 3, 4, 5, 6];

$filterEven = function ($item) {
    return ($item % 2) === 0;
};

$output = array_filter($input, $filterEven);
```

