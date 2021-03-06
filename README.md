[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/?branch=master)
[![Build Status](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/badges/build.png?b=master)](https://scrutinizer-ci.com/g/JanPietrzyk/php-version-transpiler/build-status/master)
|
[![Latest Stable Version](https://poser.pugx.org/janpiet/php-version-transpiler/v/stable)](https://packagist.org/packages/janpiet/php-version-transpiler)
[![Latest Unstable Version](https://poser.pugx.org/janpiet/php-version-transpiler/v/unstable)](https://packagist.org/packages/janpiet/php-version-transpiler)
[![License](https://poser.pugx.org/janpiet/php-version-transpiler/license)](https://packagist.org/packages/janpiet/php-version-transpiler)
[![Monthly Downloads](https://poser.pugx.org/janpiet/php-version-transpiler/d/monthly)](https://packagist.org/packages/janpiet/php-version-transpiler)


# PHP Version Transpiler

Remove PHP7 language features and add PHP 5.6 compatible syntax :)

Install:
```
composer require janpiet/php-version-transpiler
```



Usage:
```
_Bin_Path/_php-version-transpiler _PHP_7_Source_Directory_ _PHP_5_6_Target_Directory_
```

Run tests:

```
composer install
bin/phpunit
```

View the files it generates: 
* Input: `tests/_fixtures`
* Output: `tests/_out`

## Installation

requires composer & php7

````
composer install
bin/phpunit

````

## Support

As with every solution to such a problem there is no way to solve erverything, and there is no way to solve everything with one thing.
I suspect there will far more use cases for a Shim for many incompatibility between 5.6 and 7.0. Other stuff will be that hard to detect, that I am not sure it will be worth it.
Especially some of the more subtle additions to the language will not be emaulatable. But maybe they are not worth pursuing either?

#### From http://php.net/manual/de/migration70.new-features.php

| Feature                             | Supported     | Emulated   | Possible | SHIM     | Notes 
| ----------------------------------- |:-------------:| :---------:| :-------:| :-------:| :-------
| Scalar type declarations            | x             | -          | x        | -        |  
| Return type declarations            | x             | -          | x        | -        |
| Null coalescing operator            | x             | x          | x        | -        |
| Spaceship operator                  | x             | x          | ?        | -        |
| Constant arrays using define()      | -             | -          | x        | -        |
| Anonymous classes                   | x             | x          | x        | -        | But get_class() will now give something real back
| Unicode codepoint escape syntax     | -             | -          | partly?  | partly?  | Would need a shim
| Closure::call()                     | -             | -          | x        | -        |
| Filtered unserialize()              | -             | -          | x        | -        | Generally a very hard implementation for such a simple feature
| IntlChar                            | -             | -          | -        | x        |
| Expectations                        | -             | -          | -        | -        | It is backwards compatible
| Group use declarations              | -             | -          | x        | -        |
| Generator Return Expressions        | -             | -          | partly?  | partly?  | Would need a shim
| Generator delegation                | -             | -          | -        | -        |
| Integer division with intdiv()      | -             | -          | -        | x        | Should be much easier to do this by Shim 
| Session options                     | -             | -          | ?        | -        | maybe, but might be leaky
| preg_replace_callback_array()       | -             | -          | x        | -        | Can be very easily a Shim
| CSPRNG Functions                    | -             | -          | .        | -        | Can be very easily a Shim

#### From http://php.net/manual/de/migration70.incompatible.php

| Feature                                                                                            | Supported     | Emulated   | Possible | SHIM     | Notes 
| -------------------------------------------------------------------------------------------------- |:-------------:| :---------:| :-------:| :-------:| :-------
| Changes to error and exception handling                                                            | -             | -          | x        | -        | The docs contain a way out  
| Changes to the handling of indirect variables, properties, and methods                             | -             | -          | x        | -        |
| Changes to list() handling                                                                         | -             | -          | ?        | -        |
| Array ordering when elements are automatically created during by reference assignments has changed | -             | -          | -        | -        | And never will be....
| Parentheses around function parameters no longer affect behaviour                                  | -             | -          | x        | -        | Can be removed automatically
| foreach no longer changes the internal array pointer                                               | -             | -          | -        | -        | Therefore current() is essentially rendered useless here
| foreach by-value operates on a copy of the array                                                   | -             | -          | partly?  | partly?  | Would need support from a shim, might be hard to detect 
| foreach by-reference has improved iteration behaviour                                              | -             | -          | partly?  | partly?  | Would need support from a shim, might be hard to detect
