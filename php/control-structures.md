# Control structures

## if/then/else

```php
<?php

$a = 1;
$b = '1';

// Type-insensitive compare
if ($a == $b) {
    // ...
} else {
    // ...
}

// Type-sensitive compare
if ($a === $b) {
    // ...
} else {
    // ...
}

// Alternative syntax
if ($a == $b):
    // ...
else:
    // ...
endif;
```

## while

```php
<?php

$length = 1;
$i = 0;

while ($i < $length) {
    $i++;
}

// Alternative syntax
while ($i < $length):
    $i++;
endwhile;
```

## for

```php
<?php

for ($i = 0; $i < 10; $i++) {
    // ...
}

// Alternative syntax
for ($i = 0; $i < 10; $i++):
    // ...
endfor;
```

## function

```php
<?php

function addOne($v) {
    return $v + 1;
}

echo addOne(2); // => 3

function recursivelyCount() {
    static $count = 0;

    $count++;
    if ($count < 10) {
        return recursivelyCount();
    }

    // Reset static variable
    $returnValue = $count;
    $count = null;

    return $returnValue;
}

echo recursivelyCount(); // => 10

// Nested function
function foo() {
    function bar() {
        echo "I don't exist until foo() is called.";
    }
}

// Can't call bar() as it doesn't exist yet
foo();

// Now we can call bar()
bar();
```

