Linio PHP Coding Standard
-------------------------

This guide extends and expands on [SYMFONY](http://symfony.com/doc/current/contributing/code/standards.html), which expands on [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md), the PHP community coding standard.

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
* [SYMFONY](http://symfony.com/doc/current/contributing/code/standards.html)
* [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design))

## Docblocks and Comments
* Docblocks MUST use [phpDocumentor](http://www.phpdoc.org/) syntax
* The docblock MUST be laid out in the following format: message, annotations, parameter definitions, exception definitions, return definition
```php
/**
 * This method does something.
 *
 * @Annotation()
 * @Annotation()
 *
 * @param Type $variable
 * @param Type $variable2
 *
 * @throws InvalidArgumentException
 * @throws InvalidArgumentException
 * @throws SomeOtherException
 *
 * @return Type1|Type2
 */
```
* The previously defined sections MUST be separated by a newline.
* Methods SHOULD NOT have a docblock, unless the following conditions are true.
    * The method does throw an exception
    * The method does has an annotation
    * A method parameter cannot be type hinted due to it being a union type or mixed
    * A method parameter needs a type override in the docblock such as overriding an array type with a class
* If such conditions are true, ONLY the conditions needed to be documented SHOULD be done.
* All properties MUST have a docblock.
* Redundant commentaries SHOULD be avoided.
    * e.g: `This method gets something`, `method that adds something`
* Docblocks MUST use imports for all classes.
* Docblocks SHOULD declare each and every instance of all exceptions a method throws.
* An inline docblock MUST be defined on the line prior to the variable.
```
/** Type $variable */
$variable = ...;
```
* Object collection types MUST use the two brackets syntax.
    * e.g: `DateTime[]`, `User[]`, etc.
* Inline comments MUST use double slashes.
* To-do comments MUST be placed where it will be implemented/called.

## Namespaces and Class Imports
* Code MUST use one use statement per line (i.e. do not use the use group syntax).
* Code MUST import all classes.
* Namespaces SHOULD be singular.

## Variables
* Variables SHOULD be descriptive (e.g. $userId not $key, $user not $value).

## Newlines
* A newline SHOULD be placed before and after a code block.
A newline between an assignment and a code block interacting with the variable is OPTIONAL.
```php
public function methodWithSpace()
{
    $var = false;

    if ($var === true) {
        $this->doSomething();
    }

    $this->doSomethingElse();
}
```
```php
public function methodWithoutSeperation()
{
    $var = false;
    if ($var === true) {
        $this->doSomething();
    }

    $this->doSomethingElse();
}
```
* A newline MAY be placed after declaring a variable and any business logic, but is OPTIONAL
```php
$var = new Something();

$var->doSomething();
$var->doSomethingElse();
```
```php
$var = new Something();
$var->doSomething();
$var->doSomethingElse();
```
* A newline MUST be placed between immediately unrelated business logic
```php
$this->handle(new Something());

$this->addFlash('success', 'Some Message');
```

## Strings
* Strings MUST always use single quotes
* Concatenation MUST be done only by using the `sprintf()` function, unless the variable
is placed in the start or the end of the string
    * e.g: `'String interpolation: ' . $var
* Newlines MUST be written with `PHP_EOL` instead of `\n`
* All SQL queries MUST be written inside single quotes

## Arrays
* All declarations MUST use short syntax
* A comma MUST be inserted at the last element, unless it is an inline array
* You MUST NOT align keys and values inside arrays (i.e. You MUST keep only one space before and one space after the arrow `=>` operator)

## Classes
* Prefixes/suffixes SHOULD NOT be used in class names, including traits and interfaces in most cases. Instead, try to use namespaces and descriptive class names. This helps to keep classes aligned with a single responsibility.
    * Examples:
        * `CompileUserPermissions` instead of `UserPermissionService`
        * `CastsToJson` instead of `JsonInterface`
    * Exceptions to this include exceptions, and also classes like repositories, where the class name cannot realistically be named to be understandable on it's own.
        * Exceptions MUST end in `Exception` (e.g. `InvalidArgumentException`)
    * Another exception are traits who's main purpose is to make dependency injection reusable, such as `SessionAware`.
* Constants MUST have visibility declared.
* Methods and property visibility SHOULD be declared as protected in libraries.
    * In your application specific code, it is up to the project lead to define the standard.
* The order of the class MUST be: traits, constants, properties, dependency injection setters, constructor, destructor, getters/setters, public methods, protected methods, private methods.
* Getters and setters MUST be grouped by respective property.
* Getters and setters MUST be declared in the order of their respective properties.
* All properties should have a sane default if one can be provided (E.g. a list should have an empty array).
* Dependency injection SHOULD primarily be done through a constructor. The exception to this rule is Symfony controllers.
* Having an unmaintainable constructor indicates the class is probably too complex, and does not follow SOLID principles.

```php
class User
{
    public const PASSWORD_EXPIRATION_LENGTH = 3;
    public const TYPE_ADMIN = 'admin';

    /**
     * @var string
     */
    private $type;

    /**
     * @var string
     */
    private $name;

    /**
     * @var string
     */
    private $email;

    /**
     * @var bool
     */
    private $enabled = true;

    public function __construct(string $name, string $email, bool $enabled = true)
    {
        $this->name = $name;
        $this->email = $email;
        $this->enabled = true;
    }

    public function __destruct()
    {
        // TODO: Implement __destruct()
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setName(string $name): void
    {
        $this->name = $name;
    }

    public function getEmail(): string
    {
        return $this->email;
    }

    public function setEmail(string $email): void
    {
        $this->email = $email;
    }

    public function isEnabled(): bool
    {
        return $this->enabled;
    }

    public function setEnabled(bool $enabled): void
    {
        $this->enabled = $enabled;
    }

    public function __toString(): string
    {
        return $this->name;
    }

    public function __get(string $attribute)
    {
        return $this->$attribute ?? null;
    }

    public function __set(string $attribute, $value): void
    {
        $this->$attribute = $value;
    }
    
    public function something()
    {
        // TODO: Implement something()
    }

}
```

## Methods & Functions
* Functions and methods MUST have type definitions for parameters, and return types.
This includes `void` for functions/methods with no return value.
    * Exceptions are only for mixed and union types.
* `return;` MUST ONLY be used for `void` returns.
* `return null;` MUST be used when returning `null`.
* Code SHOULD NOT use fluent interfaces.

## Generic
* All tabs MUST be soft tabs using 4 spaces.
* You MUST NOT reuse already declared variables.
* Method calls MAY be used as arguments only when they have no parameters or don't throw exceptions.
* When binding parameters in `PDO`, you MUST use named parameters instead of numbered ones.
* `date()` function MUST NOT be used when manipulating dates, only outputting strings.

## Symfony
* Routes SHOULD be named in RDNS syntax following the namespace of the controller, without controller in the name.
    * e.g. `Linio\Passport\Controller\Admin\User\ProfileController::updateAction` maps to `passport.admin.user.profile.update`
* Configuration must be done with YAML ONLY.

## Database
* You MUST use plural words for table names.
* You MUST use snake case for naming columns.
