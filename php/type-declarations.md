# Type declarations

There are two flavors of type declarations in PHP:

- Coercive (default): will try to transform values to the declared type.
- Strict: will error out if types aren't as expected. `declare(strict_types=1)`

## Coercive

```php
function foo(string $v): string {
    return $v;
}

foo(123); // Returns the string "123"
```

## Strict

```php
declare(strict_types=1);

function bar(string $v): string {
    return $v;
}

foo(123); // Throws an error
```

## Scalar types

- `string`
- `int`
- `float`
- `bool`