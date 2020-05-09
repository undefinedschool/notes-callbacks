# ![Callbacks](https://i.imgur.com/5dD9fD4.png)

<div align="center">  
  <p align="center">
  <sub>
    Estas notas fueron elaboradas por <a href="https://twitter.com/_nhsz" target="_blank" rel="noreferrer noopener">@_nhsz</a>, como parte del contenido de los cursos de <a href="https://undefinedschool.io/" target="_blank" rel="noreferrer noopener"><strong>undefined school</strong></a>, una escuela de <strong>Desarrollo Web Full Stack JavaScript</strong>, <a href="https://github.com/undefinedschool/" target="_blank" rel="noreferrer noopener">100% Open Source</a>, con <strong>mentorías personalizadas para grupos reducidos</strong> y el foco puesto en los <strong>fundamentos</strong> y <strong>conceptos avanzados</strong> ⚡
  </sub>
  </p>
  
  <p align="center">
  <sub>
    Si te resultaron útiles, te cuento que soy muy fan del café; si querés colaborar para que no me quede dormido y siga escribiendo guías, apuntes y más <strong>contenido Open Source en español</strong>, podés invitarme uno, gracias! ❤️
  </sub>
  </p>
  
  <h4 align="center">
  ☕
  <code> 
  <a mp-mode="dftl" href="https://www.mercadopago.com.ar/checkout/v1/redirect?pref_id=243772354-b32a750f-2505-41c1-8e5e-9dcdb4536593" name="MP-payButton" class='blue-ar-l-rn-none'>
    <strong>Invitame 1 café!</strong>
  </a>
  </code>
  </h4>
  <hr>
</div>

👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-callbacks#intro)
- [JS Asincrónico](https://github.com/undefinedschool/notes-callbacks#js-asincr%C3%B3nico)
- [Qué es un _callback_?](https://github.com/undefinedschool/notes-callbacks#ok-todo-muy-lindo-pero-qu%C3%A9-es-un-callback-)
- [Cómo funcionan los callbacks en JavaScript?](https://github.com/undefinedschool/notes-callbacks#c%C3%B3mo-funcionan-los-callbacks-en-javascript)

---

## Intro

- La mayor parte del código que escribimos se ejecuta _secuencialmente_. Llamamos a esto _**programación sincrónica**_
- A veces es beneficioso que el código se ejecute luego de que suceda algo determinado (un _evento_) y no secuencialmente. Llamamos a esto _**programación asincrónica**_

Los _callbacks_ nos permiten programar de forma _asincrónica_

## JS Asincrónico

- En un lenguaje _single-thread_, sólo una tarea puede ejecutarse a la vez
- Una tarea pasa a ejecutarse _sólo_ si la anterior fue completada (ej: esperar a que una función termine de ejecutarse y retorne el resultado)
- Si una operación tarda mucho en finalizar, _bloquea_ la ejecución del resto del programa (si tarda poco también, pero obviamente es más difícil de percibir)
- La ejecución _asincrónica_ de código nos permite esquivar este cuello de botella, al _delegar o poner en segundo plano_<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup> una tarea, para que podamos continuar con la ejecución del resto, sin esperar a que la anterior finalice y obtener el resultado de la primera cuando finalice, para poder utilizarlo

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

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup>Ver notas sobre el [_Event Loop_](https://github.com/undefinedschool/notes-event-loop).
