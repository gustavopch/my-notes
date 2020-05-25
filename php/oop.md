# Object-oriented Programming

In PHP, objects are instances of classes. **Don't confuse them with associative arrays.**

## Acessing a property

```php
<?php

// Print the property "prop" of the object "obj"
echo $obj->prop;

// Does the same thing
$v = 'prop';
echo $obj->$v;

// Mistakes:
echo $obj.prop; // ERROR
echo $obj['prop']; // ERROR
```

## Property visibility

```php
<?php

class MyClass {
    // Public by default
    $publicProp;

    // Explicitly public
    public $otherPublicProp;
  
    // Available to this class and its subclasses
    protected $protectedProp;
  
    // Available to this class only
    private $privateProp;
}
```

## Inheritance

```php
<?php

class Dog extends Animal {
}
```

