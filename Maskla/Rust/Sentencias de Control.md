# Condiciones
Estas condiciones son bloques que se ejecutan si la evaluación lógica se cumplen como verdadero. Ejemplo:

```Rust
if (a == b) || (b > a){
	//Ejecuta el bloque
}
```

# Ciclos
Los ciclos, ejecutan el bloque de instrucciones, el control de estas mismas se tiene mediante sentencias condicionales o indicando explícitamente el fin de la ejecución del ciclo con `break`. Adicionalmente se cuenta con `continue` para indicar que la iteración actual del bloque se interrumpirá para pasar a la siguiente iteración.

## Loop
Un `loop` es un ciclo que no tiene fin, debido a ello se hace necesario combinarlo con la sentencia `if` y alguna variable de cambio que permita romper el ciclo con la sentencia `break`. Los bloques `loop` pueden ser etiquetados para evitar ambigüedades en la legibilidad del código

```Rust
fn main(){
	let mut x = 1;
	'a: loop{
		if x == 10{
			break 'a;
		}
		x += 1;
	}
}
```

## While
Esta sentencia maneja el concepto anterior simplificándolo.

```Rust
fn main(){
	let mut x = 1;
	while x != 10 {
		x += 1;
	}
}
```

## For
`for` es un bloque cíclico que se repite según lo especificado por la expresión de iteración. Esta misma comienza y termina alcanzando cada uno de los términos especificados en la expresión, con una variable se puede tener registro del estado del ciclo.

```Rust
fn main(){
	for i in 1..10{
		if(i < 10){
			println!("For state: {}", i);
		}
	}
}
```

> [!info]
> La expresión del ciclo requiere ser un [[Slices#iteradores|iterador]]. 

 Para un arreglo, se puede obtener el iterador automáticamente desde colecciones como vectores o arreglos, ejemplo: 
```Rust
fn main(){
	let array = [1,2,3,4,5];
	for element in array {
		println!("Value in array: {element}");
	} 
} 
```
