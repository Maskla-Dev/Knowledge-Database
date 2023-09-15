# Ejecución asíncrona
Cuando una función es definida com `async`, se especifica la transformación del bloque de código en una máquina de estado que implementa el un trait llamado `future`. 
```Rust
async fn asynchronous_function(){}
```
Cuando se ejecuta una funcion `async`, se devuelve un valor del tipo `Future`  (`async` es un `Future`). Por instancia, una función `async` no puede ser ejecutada dentro de un flujo sincrono, sin embargo, se posible relegar el flujo de ejecución a una función asíncrona que permita la ejecución de otras funciones asíncronas. Para que esto ocurra, se requiere el uso de un **Executor**.
```Rust
// block_on bloquea el flujo principal de ejecución y ejecuta
// el future hasta que este ultimo termine
use futures::executor::block_on;
async fn hello_world(){
	println!("Hello world");
}

fn main(){
	let future = hello_world(); // hello_world no se ejecuta
	block_on(future);   //hello_world se ejecuta 
						//mediante la instancia future
}
```

Cualquier llamada de funciones asincronas y sincronas dentro de una funcion asincrona es valido, si se utiliza `.await` (cualquier `future` puede acceder a ello), se esperará a que termine la ejecución del `future` para pasar a la siguiente instrucción. `.await` no bloquea la ejecución del hilo (a diferencia de un *executor*).
```Rust
async fn learn_and_sing() {
    // Wait until the song has been learned before singing it.
    // We use `.await` here rather than `block_on` to prevent blocking the
    // thread, which makes it possible to `dance` at the same time.
    let song = learn_song().await;
    sing_song(song).await;
}

async fn async_main() {
    let f1 = learn_and_sing();
    let f2 = dance();

    // `join!` is like `.await` but can wait for multiple futures concurrently.
    // If we're temporarily blocked in the `learn_and_sing` future, the `dance`
    // future will take over the current thread. If `dance` becomes blocked,
    // `learn_and_sing` can take back over. If both futures are blocked, then
    // `async_main` is blocked and will yield to the executor.
    futures::join!(f1, f2);
}

fn main() {
    block_on(async_main());
}
```
# `Future` trait
Se designa como `Future` computaciones asíncronas que producen datos (incluyendo el dato vacío `()`). Los `Future` tienen una funcionalidad similar a las `Promises` de JavaScript, se define una función que será llamada una vez que la ejecución de la tarea principal haya terminado.
```Rust
trait SimpleFuture {
    type Output;
    fn poll(&mut self, wake: fn()) -> Poll<Self::Output>;
}

enum Poll<T> {
    Ready(T),
    Pending,
}

```
El código anterior describe un `Future`con lógica básica, `Outpuit`es el valor producido al finalizar el flujo del `Future` (definido mediante `async fn`), El valor devuelto por el `Future` es de tipo `Poll` el cual describe 2 de los estados: `Ready(T)` describe cuando el `Future` ha finalizado su ejecución, de este modo el dato de tipo `T` es el valor producido; y `Pending` que describe un `Future` que no ha terminado su ejecución. 