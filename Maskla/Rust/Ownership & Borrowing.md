El concepto de pertenencia u _Ownership_, especifica que para evitar referencias de memoria inválidas, para las variables en la sección ***`heap`*** debe de existir una sola referencia directa para cada valor en la memoria. 

Con este mecanismo, el contexto de las variables tiene una relevancia vital, ya que al pasar argumentos a través de funciones, se realiza un proceso de transferencia de la propiedad del objeto. Cuando la ejecución de un bloque de instrucciones (definidos con `{}`), todas los objetos dentro del bloque son retiradas de la memoria del program, es por ello, que si la pertenencia del objeto no es devuelta, el objeto dejará de estar disponible.

```Rust
fn main(){
	let mut x: i32 = 24; //x lives here
	object_thief(x); //x doesn live here, it lives in object_thief scope
	//x doesn live anymore
}

fn object_thief(x: mut i32){
	//x lives here
	x += 1;
	//x will be deallocated at end
}
```

Los mismos mecanismos rigen la sección ***`stack`*** de la memoria, sin embargo, pueden crearse referencias del objeto para poder acceder a sus datos a lo largo del programa para disponer y hacer uso de él, este mecanismo se le conoce como préstamo o _Borrowing_, teniendo así 2 tipos de referencias: únicas y compartidas.
```Rust
// Shared references
let main(){
	let mut vector = vec![1,2,3];
	// Can exists many references as required if all of them are
	// points the reference as inmutable (&<data type>)
	// Unique references for the object are dissabled when shared references
	// is working
	let x: &i32 = &vector[2];
	let y: &i32 = &vector[1];
	let z: &i32 = &vector[0];
	let vector_ref1 = &vector;
	let vector_ref2 = &vector;
	println!("{} {} {}", x, y , z);
}
```

```Rust
// Unique references
// When a references is pointed as mutable, the reference 
// becomes a unique reference. It means that another reference of same type
// (for the pointed object ) is not allowed
let main(){
	let mut vector = vec![1,2,3];
	let x: &mut i32 = &mut vector[2];
	// If unique references are downgraded to shared references, unique
	// references are dissabled, eg.
	// let y: &i32 = &*x;
}
```

Estas características son de exclusión mutua, es decir que si se elige una, la otra no estará disponible. Ejemplos:

```Rust
fn main(){  
	let name = String::from("Nami"); //name lives in main  
	thief(&name); //main borrows name variable to thief using a reference  
	//name still living here
	println!("I am {}!", name);
}  
  
fn thief(name: &String){  
	println!("I cannot steal your name {}!", name);  
	//name belongs to main, thus, name will not be deallocated  
}
```

```Rust
fn main() {  
	let mut a = String::from("asdasd");  
	change(&mut a);  
	read(&a);  
}  
  
fn change(a: &mut String){  
	println!("a = {}", a);  
	a.push_str("bsbsbsb");  
}  
  
fn read(a: &String){  
	println!("a = {}", a);  
}
```

Por si misma, una referencia solo contiene eso, una referencia, por lo tanto se debe de especificar cuando se requiere acceder al valor que contiene, sin embargo, algunas estructuras de la librería estándar de Rust (como `String`), acceden al valor de manera automática ya que definen rutinas ([[Traits]]) que permiten realizar el proceso de manera implícita. Este mecanismo se llama de-referenciación o _dereferencing_. 

```Rust
fn main(){
	let t: i32 = 42;
	let x: &i32 = &t;
	let y = &x;
	println!("{}", **y); //prints "42"
}
```

```Rust
fn main() {  
	let mut a = String::from("asdasd");  
	change(&mut a);  
	read(&a);  
}  
  
fn change(a: &mut String){  
	println!("a = {}", a);  
	a.push_str("bsbsbsb");  
}  
  
fn read(a: &String){  
	println!("a = {}", a);  
}
```
