También conocido como ofuscación, es un mecanismo que permite reciclar el nombre de las variables. La ofuscación funciona por contexto de la variable, es decir, que el bloque en el que se encuentra determinará la vida útil de la variable sobre-escrita.

# RUST
Rust, el shadowing trabaja [[Life Times|según la vida útil]] de la variable. La restricción para esto es que las variables de tipo `const` no permiten utilizar este mecanismo y que las variables deben contener valores del mismo tipo.

```Rust
fn main(){
	let x = 20;
	let y = 40;
	let y = 50;
	{
		let x = 30; 
		//In this scope x is equal to 30
	}
	//In this scope x is equal to 20 and y is equal to 50
}
```

