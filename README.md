# Callbacks (WIP)

- La mayor parte del código que escribimos se ejecuta _secuencialmente_. Llamamos a esto _**programación sincrónica**_
- A veces es beneficioso que el código se ejecute luego de que suceda algo determinado (un _evento_) y no secuencialmente. Llamamos a esto _**programación asincrónica**_

Los _callbacks_ nos permiten programar de forma _asincrónica_

## JS Async

- En un lenguaje _single-thread_, sólo una tarea puede ejecutarse a la vez
- Una tarea pasa a ejecutarse _sólo_ si la anterior fue completada (ej: esperar a que una función termine de ejecutarse y retorne el resultado)
- Si una operación tarda mucho en finalizar, _bloquea_ la ejecución del resto del programa (si tarda poco también, pero obviamente es más difícil de percibir)
- La ejecución _asincrónica_ de código nos permite esquivar este cuello de botella, al _delegar o poner en segundo plano_ una tarea, para que podamos continuar con la ejecución del resto, sin esperar a que la anterior finalice y obtener el resultado de la primera cuando finalice, para poder utilizarlo

```js
const sync = () => {
  console.log('First');
  alert('Hello!');
  console.log('Third');
}
```

```js
// simulate server response latency
setTimeout(() => console.log('Response'), 5000);

// this function is executed after the other one, but finished first
console.log('Request');

// we can reduce latency to just 4ms and it'll still be executed after the 2nd function
setTimeout(() => console.log('Response'), 4);

// this function is executed after the other one, but finished first
console.log('Request');
```

## Ok todo muy lindo pero... qué es un callback? 🤔

Es una **función**. Se llama _callback_ porque [espera que alguien la llame](https://www.youtube.com/watch?v=StKVS0eI85I) para aparecer y ejecutarse. Se invoca sólo cuando pasa algo determinado. Es por esto último que decimos también que JavaScript es un lenguaje de programación orientado a eventos o [_event-driven_](https://en.wikipedia.org/wiki/Event-driven_programming).

Hay una _inversión del control_: en lugar de ser nosotras/os quienes decidimos cuándo va a ejecutarse una función (como lo hacemos normalmente, cuando codeamos secuencialmente), es otra función la que va a invocar a nuestro _callback_ en algún momento.

## ¿Cómo funcionan los _callbacks_ en JavaScript?

Recordemos que en JavaScript, las funciones son lo que llamamos [First-Class citizens](https://github.com/undefinedschool/notes-functions-first-class/) y esto nos permite tratarlas como cualquier otro valor, lo que incluye pasarlas por parámetro a otra función (y que esto a su vez es posible porque en JavaScript las funciones son _higher order functions_).

En el siguiente ejemplo, le pasamos una función (_callback_) `myCallback` por parámetro a otra función `foo`. La función _callback_ luego es invocada por `foo`

```js
// caller
function foo(callback) {
  callback('world');
}

// callback function
function myCallback(name) {
  console.log(`Hello ${name}`); // "hello world"
}

// pass callback to caller
foo(myCallback);
```

- Un _callback_ es sólo una forma de guardar cosas para hacer más tarde
- El orden en el que las cosas suceden no es lineal ni de arriba hacia abajo: va cambiando a medida que otras tareas se completan
