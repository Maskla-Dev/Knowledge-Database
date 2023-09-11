# Tipos de Datos

## Tipos escalares

| Longitud                       | Signo   | Sin signo | Tipo     |
| ------------------------------ | ------- | --------- | -------- |
| 8 bits                         | `i8`    | `u8`      | Entero   |
| 16 bits                        | `i16`   | `u16`     | Entero   |
| 32 bits                        | `i32`   | `u32`     | Entero   |
| 64 bits                        | `i64`   | `u64`     | Entero   |
| 128 bits                       | `i128`  | `u128`    | Entero         |
| Según arquitectura del sistema | `isize` | `usize`   | Entero   |
| 32 bits                        | `f32`   | No hay    | Flotante |
| 64 bits                        | `f64`   | No hay    | Flotante |

> [!warning]
> Al utilizar enteros, cuando ocurren [[Data Overflow|desbordamientos de memoria]] el comportamiento de los valores de las variables es predecible en tiempo de compilación cuando el binario fue compilado en modo `--release`, ya que las variables comenzarán de nuevo desde el valor más bajo. Para evitar este comportamiento y dar seguridad a las operaciones se recomienda el uso de los métodos `checked_*` (retorna `Option<T>`), `overflowing_*` (retorna una tupla `(T, bool)`) o `saturating_*` (si se alcanza el valor mínimo o máximo  permitido por el tipo de valor durante la operación, este mismo no cambiara, [ver concepto de saturación](https://es.wikipedia.org/wiki/Aritmética_de_saturación)).

### Literales y separadores

Las variables escalares pueden tener representación hexadecimal, octal, binaria y por byte. Adicionalmente cada una de esas representaciones, pueden agruparse y separarse dígitos que permita su legibilidad a excepción de la literal por byte.

```Rust
fn main(){
	let binary = 0b1111_0000;
	let decimal = 1234_1232;
	let hexadecimal = 0x1AF_12E;
	let octal = 0o1234_127;
	let byte = b'>';
}
```

### Boolean y Character

Los tipos `boolean` admiten solo dos posibles valores: `true` y `false`. 

```Rust
fn main(){
	let mut boolean_value = true;
	boolean_value = false;
}
```

El tipo character o `char` representa caracteres, este tipo de dato representa un [Unicode Scalar Value](https://www.unicode.org/glossary/#unicode_scalar_value) abarcando valores desde el U+0000 al U+D7FF y U+E000 al U+10FFFF. Este tipo acepta valores en representación entera, caracter y en literales.

```Rust
fn main(){
	let special_character = '@';
	let unicode_literal = '\u{D500}';
	let integer_character = 32;
}
```

> [!warning]
> Un caracter que no se encuentra en el rango causará que se inicie la secuencia de pánico, por ejemplo: `let panic_launch = '\u{DFFF}';`. Es posible evitar la secuencia de pánico si se marca como `unsafe` el bloque de código: `unsafe { let panic_launch = '\u{DFFF}'; }`. 

## Tipos compuestos

Los tipos compuestos son aquellos que agrupan otros datos en una estructura lineal estática, es decir, que no pueden cambiar de tamaño ni de composición en tiempo de ejecución y que la disposición de los datos es secuencial. El primer tipo de dato de este tipo son las tuplas, estas agrupan distintos tipos de datos en una sola estructura.

```Rust
fn main(){
	let implicit_tuple = ("string_type", 'c', 235);
	let explicit_tuple: (String, char, u32, f32) = ("string_type", 'c', 235,
													0.0);
}
```

Para acceder a su información existen 2 posibles notaciones.

```Rust
fn calc() -> (u32, i32){
	(32, -50)
}

fn main(){
	let full_tuple = calc();
	let (x, y) = calc();
	println!("{full_tuple.1}, {full_tuple.2}");
	println!("{x}, {y}");
}
```

La siguiente estructura son los arreglos, estos solamente agrupan datos de un solo tipo, se puede generar un arreglo si:
- Se especifican cada uno de los elementos que contiene.
- Se especifica una expresión de repetición `[expr; N]`, donde `N` es el numero de veces que la expresión `expr` va a repetirse en el arreglo. `expr` puede ser un valor o un tipo de dato.
```Rust
fn main(){
	let fixed_array = [1,2,3,4,5];
	let expression_array1: [i32: 5]; //Array with 5 entries of i32 length
	let expression_array2: [32: 5]; //Array with 5 entries where each entry
									//contains 32 value
}
```

> [!note]
> Es posible inicializar una tupla desde un arreglo si se conoce la longitud del arreglo:
> `let tuple_from_array: (w,x,y,z)=[1,2,3,4];`

> [!warning]
> Si se intenta acceder a una posición fuera de los limites de un arreglo o tupla, el programa compilara pero iniciará una secuencia de pánico en tiempo de ejecución.

>[!tip]
> `String` pasa a `&str` sin necesidad de realizar la conversión de manera explicita.

Los arreglos permiten [[Slicing|Slices]] e [[Iterators|Iteradores]].

## Strings

Hay dos tipos de cadenas de texto: `&str` (literal) y `String` (objeto). Las de tipo literal, se consideran referencias estáticas a los datos de la cadena de texto, dichas referencias serán mantenidas válidas durante la ejecución del programa (son alojadas en la memoria ***stack***) y estas mismas forman parte del conjunto de primitivas del lenguaje Rust. Las cadenas de tipo objeto no son primitivas y son flexibles en cuanto a su manipulación, por defecto tiene una codificación UTF-8 y se mantienen en la sección ***heap*** de la memoria.

```Rust
fn main(){
	let literal_str = "Hola Mundo";
	let object_empty_str = String::new();
	let initialized_obj_str = String::from(literal_str);
}
```

> [!note]
> Es posible convertir cadenas literales en objeto mediante el método `to_string()`. La mayoría de primitivas implementa este tipo de método.
> 
> De forma inversa, de objeto a literal con el método `as_str()`



# Mutabilidad e inmutabilidad
Las variables en Rust siguen la filosofía de seguridad del lenguaje, por lo que, cualquier variable escrita por defecto será del tipo inmutable, eso quiere decir que no puede ser modificada durante la [[Life Times|vida útil de esta]]. Para que una variable pueda ser inmutable, es necesario especificar que es mutable mediante **`mut`**.

```Rust
fn main(){
	let inmutable_variable = -4;
	let explicit_variable: u32 = 123;
	let mut mutable_variable = 0.324;
	const CONSTANT_INMUTABLE_VARIABLE: CustomType = { value: 32*420 };
}
```

> [!note]
> Los valores constantes son un comodín en cuanto a lectura de código, si bien siguen la lógica esperada (no admitir el uso de **mut**), se agrega el hecho que solo admiten valores que puedan ser computados en tiempo de compilación, además de requerir el tipo de dato que almacenarán de manera explicita.
> La vida útil de una variable constante dependerá del contexto en el que fue declarada (puede hacerse en el contexto global del programa).

