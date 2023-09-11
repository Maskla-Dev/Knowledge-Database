PHP is a scripting language, requires an engine who interpret the language. A PHP script requires an open and close directive, PHP will read and process code inside these marks, outside of them will be process as plain text.
```php
<?php
	//Coding block
?>
```
*PHP minimal*

Basic output is handled with `echo` function, it returns a string response, `print` does someting similar, while `echo` can handle multiple arguments (as an array), `print` handle only one. `print_r`  response with an variable info, `var_dump` can handle the same operation but the last one exposes protected and private properties and the recursive structure.

Variable declaration starts with '**$**'  character, followed by the variable name. In PHP, shadowing is allowed (see [Shadowing](https://en.wikipedia.org/wiki/Variable_shadowing#:~:text=In%20computer%20programming%2C%20variable%20shadowing,is%20known%20as%20name%20masking.) ).

```php
<?php
//Will return something like "Hola Mundo\n"
echo "Hola", " Mundo", "<br>";  
//Will return "Nuevo Mundo"
print "Nuevo Mundo";
print "<br>";
//Array variable
$b = array('m' => 'monkey', 'foo' => 'bar', 'x' => array('x', 'y', 'z'));  
$results = print_r($b, true); // $results now contains output from print_r  
//String from 'b' variable
echo $results;  
print "<br>";
//Prints 'b' variable directly
print_r($b);
print "<br>";
//Prints data info about 'b' structure (is an array at this point) 
var_dump($b);
print "<br>";
//Prints data info about 'results' structure (is a string at this point) 
var_dump($results);
?>
```
*Output and variable declaration*

Constant variables should be handled with `define` and `const` keyword

```php
<?php
define("val_name", 2);
const const_name = "Constant";

echo const_name;
```
*Constant variables doesn't require '**$**' character to point the reference*

Data types are:
- Boolean
- Float
- Integer
- String
- Arrays
- Object
- NULL
- Resource
```php
<?php
class car{}

$boolean = true;
$float = 0.01;
$integer = 1;
$string = "String";
$array1 = [];
$array2 = array();
$object = new car();
$nulled = null;
?>
```
*Data types of PHP*

PHP is not a hard typed language, by this way, support the same operators as JavaScript. Although, PHP handle some JavaScript array and string functions with operators, instead function calls.

| Operator | Description                        | Example        |
| -------- | ---------------------------------- | -------------- |
| `.`        | String concatenation               | `$z = $x . $y` |
| `.=`       | String concatenation assignment    | `%x .= $y`     |
| `+`        | Array union                        | `$x + $y`      |
| `==`       | Array equality (same key/values)                    | `$x == $y`     |
| `===`      | Array identity with order checking | `%x === $y`    |
| `!= or <>`       | Array inequality                   | `$x != $y`     |
| `!==`      | Array identity with order checking | `%x !== $y`    |
*Some especial operators for PHP*

Conditional assignment introduces the NULL coalescing operator, it returns the first expression if is not NULL, otherwise returns the second expression.

```php
<?php
//...
$x = $y ?? $z //If $y is not null, $x would be $y, $z otherwise
?>
```
*Coalescing operator example*

More for string handling in [PHP Documentation](https://www.php.net/manual/en/book.strings.php).

Arrays can be handle by 2 ways, indexed and key/value. For key/value arrays, integer and string can be used as key and value allows all data types. For indexed arrays, stored values should be consistent.

```php
<?php
// Key/value array
$b = array('m' => 'monkey', 'foo' => 'bar', 'x' => array('x', 'y', 'z'));
// Indexed
$a = [1,2,3,4];
?>
```

```php
<?php
	$clients = array("JUAN", "Pedro", "Ramon");
	foreach($clients as $client){
	//Code stuff here
	}
	for($i = 0; $i < count($clients); ++$i):
		//Code stuff here
	endfor;
?>
```
*`foreach` and Alternative for loop syntax*

```php
<?php
$num = 1
if(1 > $num):
	echo "greater";
elseif(1 < $num):
	echo "lesser";
else:
	echo "equal";
endif;
?>
```
*Alternative if-else if-else syntax*

Destructuring syntax follows `[...$<value name>]` where `...$<value name>` is a list of variables where the target array values will be storage. In the same way, key/valued arrays works.
```php
$client = [
	"name" => "Marco",
	"price" => 233,
	"last" => "Utility" 
]
foreach($client as $key => $value){
	echo $key . " | " . $value;
}
```
*Destructuring*

PHP allows hard types usage, just enabling strict types.
```php
<?php
	declare(strict_types=1);

	string $string_var = "Variable"
?>
```
*Strict type enabling*

Strict type are useful when we want to crop variable validation layers
```php
<?php
	function isAuthUser(bool $is_auth) : string{
		if(is_auth){
			return "Success auth";
		}
		else{
			return "No auth";
		}
	}

	$login_state = isAuthUser(true);
	echo login_state;
?>
```
*Strict types*

For multiple variable types as parameters (a kind of templates), unions are required
```php
<?php
	function isAuthUser(bool $is_auth) : string | int{
		if(is_auth){
			return "Success auth";
		}
		else{
			return 400;
		}
	}

	$login_state = isAuthUser(true);
	echo login_state;
?>
```
*Unions for parameters*

Pointing function arguments is allowed with named parameters.
```php
<?php
	declare(strict_types=1)
	$num1 = 10;
	$result = sum(number1: $num1, number2: $num2);
	function sum(int $number1, int $number2) : int{
		return $number1 + $number2;
	}
?>
```
*Named parameters*

Using modules in PHP is easy, `include` (no fatal errors when something wrong), `require` (fatal errors), `require_once` (same as `require` but it loads module once at file) make it possible.
```php
<?php
	require_once './heading.php';
	require './main.php';
	include './footer.php';
?>
```

Decoding and encoding
```php
<?php
	$json = json_encode($object_to_encode);
	$object_to_encode = json_decode($json);
?>
```
# Frameworks
[[Laravel]]