Linio PHP Coding Standard
-------------------------

This guide extends and expands on [PSR-2], the PHP community coding standard.

The intent of this guide is to reduce cognitive friction when scanning code
from different authors. It does so by enumerating a shared set of rules and
expectations about how to format PHP code.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## References
* [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
* [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
* [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
* [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4.md)

## Docblocks

* Docblocks MUST use [phpDocumentor](http://www.phpdoc.org/) syntax
* All method arguments MUST be documented
* Annotations MUST come before normal docblocks
* Redundant commentaries SHOULD be avoided
    * e.g: `This method gets something`, `method that adds something`
* Docblocks MUST use class alias for types, unless it is a root class
* Docblocks MUST ensure new line before @return
* Docblocks MUST declare the exceptions which the method throws
* Magic methods/properties MUST be declared in class docblock
* When declaring the type of a single variable, it MUST be placed after it's declaration
* Object collection types MUST use the two brackets syntax
    * e.g: `DateTime[]`, `User[]`, etc.
* Inline comments MUST use double slashes
* To-do comments MUST be placed where it will be implemented/called

## Namespace imports

* Code MUST use one use statement per line, MUST not use commas
* Code MUST use aliases instead of full namespaces
* Namespaces SHOULD be imported in the following order: Vendor, Framework, Project

## Strings

* Strings MUST always use single quotes
* Concatenation MUST be done only by using the `sprintf()` function, unless the variable
is placed in the start or the end of the string
    * e.g: `'String interpolation: ' . $var
* All SQL queries MUST be written inside double quoted strings

## Arrays

* All declarations MUST use short syntax
* A comma MUST be inserted at the last element, unless it is an inline array

## Getters and setters

* MUST be grouped by respective property
* MUST be declared in the order of their respective properties
* MUST be placed at the end of the class

## Generic

* [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) SHOULD be used for autoloading
* Code MUST ensure a new line before the return statement
* Parenthesis MUST be used when creating an instance of a class
* You MUST not reuse already declared variables
* When not using scalars, type hints MUST be used in method arguments
* Prefixes/suffixes SHOULD be used in class names
* Methods or properties MUST NOT be declared as private, use protected instead
* Code MUST NOT use fluent interfaces, never return $this
* Method calls SHOULD be used as arguments only when they have no parameters or don't throw exceptions
* The default value of a property SHOULD be placed in the class constructor
* When binding parameters in `PDO`, you MUST use named parameters instead of numbered ones
* `date()` function MUST NOT be used when manipulating dates, only outputting strings

## Symfony

* Routes SHOULD be named by bundle, controller, action: `cart_index_update`
* URI SHOULD follow the bundle structure and use dashes for word separation: `cart/index/update-product`
* Services MUST be declared using yaml configuration

## Database

* Use plural words for table names
* Use snake case for naming columns