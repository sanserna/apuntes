# Escribir Mejor AJAX

La forma estándar para hacer un llamado _Ajax_ usando _Jquery_ es bastante simple
por medio de la funcion `$.ajax()`

```js
$.ajax({
    data: someData,
    dataType: 'json',
    url: '/path/to/script',
    success: function(data, textStatus, jqXHR) {
        // When AJAX call is successfuly
        console.log('AJAX call successful.');
        console.log(data);
    },
    error: function(jqXHR, textStatus, errorThrown) {
        // When AJAX call has failed
        console.log('AJAX call failed.');
        console.log(textStatus + ': ' + errorThrown);
    },
    complete: function() {
        // When AJAX call is complete, will fire upon success or when error is thrown
        console.log('AJAX call completed');
    };
});
```

Desventajas del uso de este patrón:

1. **Anidamiento excesivo.** Las funciones y eventos dependientes de los datos
_AJAX_ devueltos tienen que ser envueltos en el manejador de éxito, ya que _AJAX_
es por naturaleza, asíncrono. Esto reduce la legibilidad del código.

2. **Dificultad para encadenar y combinar.** Es difícil y abrumadamente complejo
evaluar los resultados de múltiples solicitudes _AJAX_ - no podemos predecir
cuánto tiempo se tarda en que todas las solicitudes _AJAX_ (cada una corriendo
de forma asíncrona) devuelvan una respuesta.

### Promesas y objetos diferidos (deferred objects)

Las _promesas_ y los _objetos diferidos_ son implementados de forma nativa
en el metodo `$.ajax()`:

* `.done()` es el reemplazo de `.succes()`
* `.fail()` es el reemplazo de `.error()`
* `.always()` es el reemplazo de `.complete()`

Estos métodos se pueden ejecutar en cadena:

```js
$.ajax({
    data: someData,
    dataType: 'json',
    url: '/path/to/script'
}).done(function(data) {
    // If successful
   console.log(data);
}).fail(function(jqXHR, textStatus, errorThrown) {
    // If fail
    console.log(textStatus + ': ' + errorThrown);
});
```

Puede resultar mas efectivo asigar un llamado _AJAX_ a una variable, a la que se
le pueden encadenar _callbacks_ tambien. El metodo `$.ajax()` nos retorna una
promesa de forma nativa, la cual podemos usar para encadenamiento.

```js
var ajaxCall = $.ajax({
    context: $(element),
    data: someData,
    dataType: 'json',
    url: '/path/to/script'
});

ajaxCall.done(function(data) {
    console.log(data);
});
```

El `.done()` callback esta al mismo nivel del llamado a _AJAX_, esto ayuda a
mejorar la legibilidad del código y a mantener todo mucho mas organizado.

### Multiples llamados AJAX

El método `$.when()` permite encadenar varios llamados por medio de _AJAX_ y
realizar alguna acción cuando todos los llamados se resuelvan.

```js
var a1 = $.ajax({...}),
    a2 = $.ajax({...});

$.when(a1, a2).done(function(r1, r2) {
    // Each returned resolve has the following structure:
    // [data, textStatus, jqXHR]
    // e.g. To access returned data, access the array at index 0
    console.log(r1[0]);
    console.log(r2[0]);
});
```

### Cadena de dependencia en solicitudes AJAX

Se pueden encadenar múltiples llamados a _AJAX_, por ejemplo, cuando el segundo
llamado depende de los datos que retorne el primer llamado.

Digamos que la primera llamada recupera el ID de sesión de un usuario, y
necesitamos pasar ese valor a un segundo script. Recuerda que `$.then()`
devuelve una nueva promesa, la cual puede ser pasada posteriormente al método
`$.done()` o incluso otro `$.then()`.

```js
var a1 = $.ajax({
             url: '/path/to/file',
             dataType: 'json'
         }),
    a2 = a1.then(function(data) {
             // .then() returns a new promise
             return $.ajax({
                 url: '/path/to/another/file',
                 dataType: 'json',
                 data: data.sessionID
             });
         });

a2.done(function(data) {
    console.log(data);
});
```

#### Ejemplo de como encadenar llamados a AJAX

```js
function first() {
    return $.when('First');
}

function second(data) {
    message(data);
    return $.when(data + ' Second');
}

function third(data) {
    message(data);
    return $.when(data + ' Third');
}

function message(html) {
    $('<div/>').html(html).appendTo($('body'));
}

(function() {
    first().then(second).then(third).then(message);
}());

// Output:
// First
// First Second
// First Second Third
```
### Modularización de llamados a AJAX

Más a menudo que no, uno podría querer modularizar su código y delegar una sola
función para hacer solicitudes _AJAX_ dinámicas. ¿Cómo deberíamos invocar la
llamada AJAX individualmente, y acceder a la promesa devuelta, en este caso?
Resulta ser más que simple: simplemente devuelve el objeto _AJAX_ después de
hacer una solicitud.

```js
// Generic function to make an AJAX call
var fetchData = function(query, dataURL) {
    // Return the $.ajax promise
    return $.ajax({
        data: query,
        dataType: 'json',
        url: dataURL
    });
}

// Make AJAX calls
// 1. Get customer order
// 2  Get customer ID
var getOrder = fetchData(
    {
        'hash': '2528ce2ed5ff3891c71a07448a3003e5',
        'email': 'john.doe@gmail.com'
    }, '/path/to/url/1'),
    getCustomerID = fetchData(
    {
        'email': 'john.doe@gmail.com'
    }, '/path/to/url/2');

// Use $.when to check if both AJAX calls are successful
$.when(getOrder, getCustomerID).then(function(order, customer) {
    console.log(order.data);
    console.log(customer.data);
});
```

### Manejo de arreglos de objetos diferidos devueltos

A veces se desea usar `$.when()` en un arreglo de objetos diferidos. Una
situación de ejemplo sería: hacer una serie de llamadas _AJAX_, Y luego comprobar
cuando todos ellos están resueltos.

Simplemente usar el metodo `$.when.apply($, array)` para evaluar todas las llamadas
a _AJAX_ realizadas.

```js
// Let's say we have a click handler and fires off a series of AJAX request
$selector.click(function() {
    // Construct empty array
    var deferreds = [];

    // Loop using .each
    $(this).find('div').each(function() {
        var ajax = $.ajax({
            url: $(this).data('ajax-url'),
            method: 'get'
        });

        // Push promise to 'deferreds' array
        deferreds.push(ajax);
    });

    // Use .apply onto array from deferreds
    $.when.apply($, deferreds).then(function() {
        // Things to do when all is done
    });
});
```

```js
// Let's say we have a click handler and fires off a series of AJAX request
$selector.click(function() {
    // Map returned deferred objects
    var deferreds = $(this).find('div').map(function() {
        var ajax = $.ajax({
            url: $(this).data('ajax-url'),
            method: 'get'
        });

        return ajax;
    });

    // Use .apply onto array from deferreds
    // Remember to use .get()
    $.when.apply($, deferreds.get()).then(function() {
        // Things to do when all is done
    });
});
```
