---
title: Testing in Laravel
draft: false
tags:
---
 
###  1- Core Pest only (no plugin needed for unit tests)
```php
composer require pestphp/pest --dev -W
.\vendor\bin\pest --init
```
###  2- write the tester function
```php
<?php
uses(Tests\TestCase::class)->in(__DIR__);

test('generates valid slug', fn() => 
    expect(generate_slug('What is a "slug" in Laravel?'))->toBe('what-is-a-slug-in-laravel')
);

test('handles special chars', fn() => 
    expect(generate_slug('Hello World 123!'))->toBe('hello-world-123')
);
```

a note: there is difference between testing a class method and standalone function.

### 3- run the test
```php
.\vendor\bin\pest
```

### 4- to ignore the false positives 
```php
{
    "intelephense.diagnostics.undefinedTypes": false,
    "intelephense.diagnostics.undefinedFunctions": false
}
```


### note ! 
to test 
**Run**: `php artisan test` (PHPUnit) or `.\vendor\bin\pest` (both).