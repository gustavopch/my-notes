# Variables

## Naming Rules

PHP variables must start with `$` (e.g. `$foo`, `$_foo`).

If it starts with `$$`, it's a dynamic variable.

## Scopes

```php
<?php

// This variable will be available in the global scope
$v = 'global';
// Which means it'll be available for included files too
include 'other-file.php';

function declareInLocalScope() {
    // This is a whole new variable, completely unrelated to the
    // one we declared in the global scope.
    $v = 'local';
}

function failToUseGlobalScope() {
    // This won't produce any output as there's no variable named
    // $v in the scope of this function. Unlike JavaScript,
    // functions don't inherit the outer scope.
    echo $v;
}

function useGlobalScope1() {
    // Bring the global-scoped $v to the function scope
    global $v;
    // Assign value to the global-scoped variable
    $v = 'new value';
    // Echo the global-scoped variable
    echo $v;
}

function useGlobalScope2() {
    // Assign value to the global-scoped variable
    $GLOBALS['v'] = 'new value';
    // Echo the global-scoped variable
    echo $GLOBALS['v'];
}
```

## Static Variables

```php
<?php

function test() {
    // The "static" keyword will make this variable be initialized
    // only on the first time this function is called. Next times,
    // the value will be remembered.
    static $a = 0;
    echo $a;
    $a++;
}
```

