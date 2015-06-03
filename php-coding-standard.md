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

## Docblocks and Comments

* Dockblocks MUST use [phpDocumentor](http://www.phpdoc.org/) syntax
* All methods must have a docblock
* The docblock MUST be laid out in the following format: message, annotations, parameter definitions, return definition, exception definitions
```
/**
 * This method does something.
 * 
 * @Annotation()
 * @Annotation()
 *
 * @param Type $variable
 * @param Type $variable2
 *
 * @return Type1|Type2
 *
 * @throws InvalidArgumentException
 * @throws InvalidArgumentException
 * @throws SomeOtherException
 */
```
* The previously defined sections MUST be separated by a newline
* All method arguments MUST be documented
* All docblocks that are inherited should use `{@inheritdoc}`
* Redundant commentaries SHOULD be avoided
    * e.g: `This method gets something`, `method that adds something`
* Docblocks MUST use class alias for types, unless it is a root class
* Docblocks MUST declare each and every instance of all exceptions a method throws
* An inline docblock MUST be defined on the line prior to the variable
```
/* Type $variable */
$variable = ...;
```
* Object collection types MUST use the two brackets syntax
    * e.g: `DateTime[]`, `User[]`, etc.
* Inline comments MUST use double slashes
* To-do comments MUST be placed where it will be implemented/called

## Namespaces and Class Imports

* Code MUST use one use statement per line (i.e. MUST not use commas)
* Code MUST use aliases instead of full namespaces
* Namespaces SHOULD be singular

## Variables
* Variables should be descriptive (e.g. $userId not $key, $user not $value)

## Newlines
* A newline SHOULD be placed before and after a code block
* Prefixes/suffixes SHOULD be used in class names
* Methods or properties MUST NOT be declared as private, use protected instead
```
public function method()
{
    $var = false;

    if ($var === true) {
        $this->doSomething();
    }
    
    $this->doSomethingElse();
}
```
* A newline SHOULD be placed after declaring a variable and any business logic.
```
$var = new Something();

$var->doSomething();
$var->doSomethingElse();
```
* A newline MUST be placed between immediately unrelated business logic.
```
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

* The order of the class MUST be: traits, constants, properties, constructor, destructor, getters and setters, magic methods, business logic
* Getters and setters MUST be grouped by respective property
* Getters and setters MUST be declared in the order of their respective properties

```
class User
{
    const PASSWORD_EXPIRATION_LENGTH = 3;
    const TYPE_ADMIN = 'admin';
    
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
    
    /**
     * @param string $name
     * @param string $email
     * @param bool   $enabled
     */
    public function __construct($name, $email, $enabled = true)
    {
        $this->name = $name;
        $this->email = $email;
        $this->enabled = true;
    }
    
    public function __destruct()
    {
        // TODO: Implement __destruct()
    }
    
    /**
     * @return string
     */
    public function getName()
    {
        return $this->name;
    }
    
    /**
     * @param string $name
     */
    public function setName($name)
    {
        $this->name = $name;
    }
    
    /**
     * @return string
     */
    public function getEmail()
    {
        return $this->email;
    }
    
    /**
     * @param string $email
     */
    public function setEmail($email)
    {
        $this->email = $email;
    }
    
    /**
     * @return bool
     */
    public function isEnabled()
    {
        return $this->enabled;
    }
    
    /**
     * @param bool $enabled
     */
    public function setEnabled($enabled)
    {
        $this->enabled = $enabled;
    }
    
    /**
     * @return string
     */
    public function __toString()
    {
        return $this->name;
    }
    
    /**
     * @param string $attribute
     *
     * @return mixed
     */
    public function __get($attribute)
    {
        return isset($this->$attribute) ? $this->attribute : null;
    }
    
    /**
     * @param string $attribute
     * @param mixed $value
     */
    public function __set($attribute, $value)
    {
        $this->$attribute = $value;
    }
    
    public function something()
    {
        // TODO: Implement something()
    }
}
```

## Generic

* All tabs MUST be soft tabs using 4 spaces.
* You MUST not reuse already declared variables
* When not using scalars, type hints MUST be used in method arguments
* Code SHOULD NOT use fluent interfaces
* Method calls SHOULD be used as arguments only when they have no parameters or don't throw exceptions
* The default value of a property SHOULD be set in the property if it is scalar. If it's non-scalar, it MUST be placed in the class constructor. If the property is scalar and the argument is optional in the constructor, the default value must be in both places. ***
* When binding parameters in `PDO`, you MUST use named parameters instead of numbered ones
* `date()` function MUST NOT be used when manipulating dates, only outputting strings
* You SHOULD inject dependencies via the constructor EXCEPT when the majority of the class does not depend upon the majority of the dependencies.

## Symfony

* Routes SHOULD be named in RDNS syntax following the namespace of the controller, without controller in the name.
    * e.g. `Linio\Passport\Controller\Admin\User\ProfileController::updateAction` maps to `passport.admin.user.profile.update`
* Services MUST be declared using yaml configuration

## Database

* You MUST use plural words for table names
* You MUST use snake case for naming columns
