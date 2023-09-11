# Shadowing and Scope
Scope is the concept for memory allocation context, every function call creates its own memory context or scope. It means that every data definition is wrapped and  associated to the function flow. Scope works with hierarchical rules, so if a nested function is called, everything in the nested function cannot be reached by the function that defined it.

When a function calls or use defined data, first it try to get the memory reference from its scope, if the data does not live in its scope, go to the next level in the hierarchy and repeats until memory reference (data) is found. By this way, defining data allocation with same identifiers in different scopes produces variable shadowing. Shadowing allows variable identifier recycle in different scopes, is possible to produce new data with the same identifier without lose previous allocated data, by this way, always get the allocated data nearest to the scope call.
# Closures
Functions does not remember data from, previous running, so, every function invocation/run requires a new chunk of memory context. When the function run ends, every data inside the context is deleted, returning data is the exception for this mechanism. With this in mind, is possible cached the function wrapping it inside as return value in another function
```javascript
function createFunction(){
	function multiplyBy2(num){
		return num * 2;
	}
	return multiplyBy2
}

const generatedFunction = createFunction();
const value = generatedFunction(2); //Output value: 4
```

With the previous code example, `multiplyBy2` is cached in the memory, it is never deallocated in the context where it is created (via `createFunction`), using scope rules data can be cached too. It is possible because surrounding data from it context (in other words, required data for its operativity) is attached in the returning function reference, this data references are optimized in space, so, unused references inside returning function reference are not attached.
```javascript
function outer(){
	let counter = 0;
	function incrementCounter(){
		counter++;
	}
	return incrementCounter
}

const increment = outer(); //Gets cached incrementCounter function
increment(); //counter equal 1 after call
increment(); //counter equal 2 after call
```

Many applications can serve this JavaScript feature, listed as follow:
- *Once* function: Functions that counts calls, if certain call count is reached, it close its functionality.
- *Memoize* function: Functions that requires remember generated data through function calls.
- Module Pattern: Encapsulate data without expose them to higher scopes.
- Asynchronous JavaScript: Persisten state for asynchronous functions.