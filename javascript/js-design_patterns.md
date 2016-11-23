# JavaScript Design Patterns

## Patrón del Constructor

### Constructores Básicos

JavaScript por defecto no soporta la creación de clases de forma nativa, pero
si soporta funciones que actúan como constructores de objetos por medio del
prefijo `new`, de esta forma le decimos a **JavaScript** que queremos que dicha
función se comporte como un constructor e instancie un objeto nuevo con los
miembros definidos en esa función.

Dentro de un constructor la palabra clave _this_ hace referencia al nuevo
objeto que esta siendo creado.

```js
function Car (model, year, miles) {

    this.model = model;
    this.year = year;
    this.miles = miles;

    this.toString = function () {
        return this.model + " has done " + this.miles + " miles";
    };
}

// instancias del objeto car
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );

console.log(civic.toString());
console.log(mondeo.toString());
```

Las desventajas de este patrón es que dificulta la herencia y métodos como
`toString()` son re definidos para cada uno de los objetos que se creen usando
el constructor de `Car`.

### Constructores con Prototype

Las funciones, como casi todos los objetos en **JavaScript** contienen un objeto
`prototype`. Cuando se llamamos un constructor **JavaScript** para crear un
objeto, todas las propiedades del constructor `prototype` se ponen a disposición
del nuevo objeto.

```js
function Car (model, year, miles) {

    this.model = model;
    this.year = year;
    this.miles = miles;

}

Car.prototype.toString = function () {
    return this.model + " has done " + this.miles + " miles";
};

var civic = new Car( "Honda Civic", 2009, 20000 );

console.log(civic.toString());
```

Arriba, una sola instancia de `toString()` será compartida entre todos los
objetos Car.


## Módulos

Los módulos son una pieza integral de la arquitectura de cualquier aplicación
robusta y normalmente ayudan a mantener las unidades de código para un proyecto
separadas y organizadas de forma limpia.

### Object Literal

```js
var myObjectLiteral = {

    variableKey: variableValue,

    functionKey: function () {
        // ...
    }
};
```

Los _Object Literals_ no requieren que se instancien usando el operador `new`
pero no debe utilizarse al comienzo de una declaración ya que la apertura `{`
puede ser interpretada como el comienzo de un bloque. fuera del objeto, nuevos
miembros pueden ser añadidos de la siguiente manera:
`myModule.property = "someValue";`

A continuación podemos ver un ejemplo más completo de un módulo definido usando
la notación _Object Literal_

```js
var myModule = {

    myProperty: "someValue",

    // object literals can contain properties and methods.
    // e.g we can define a further object for module configuration:
    myConfig: {
        useCaching: true,
        language: "en"
    },

    // a very basic method
    saySomething: function() {
        console.log("Where in the world is Paul Irish today?");
    },

    // output a value based on the current configuration
    reportMyConfig: function() {
        console.log("Caching is: " + (this.myConfig.useCaching ? "enabled" : "disabled"));
    },

    // override the current configuration
    updateMyConfig: function(newConfig) {

        if (typeof newConfig === "object") {
            this.myConfig = newConfig;
            console.log(this.myConfig.language);
        }
    }
};

// Outputs: Where in the world is Paul Irish today?
myModule.saySomething();

// Outputs: Caching is: enabled
myModule.reportMyConfig();

// Outputs: fr
myModule.updateMyConfig({
    language: "fr",
    useCaching: false
});

// Outputs: Caching is: disabled
myModule.reportMyConfig();
```

### Patrón del Modulo

El patrón del módulo se definió originalmente como una forma de proporcionar
encapsulación tanto privada como pública para las clases.

#### Privacidad

El patrón del Módulo encapsula la "privacidad", el estado y la organización
usando cierres. Proporciona una forma de envolver una mezcla de métodos y
variables públicas y privadas, protegiendo las piezas de fugas en el ámbito
global y chocando accidentalmente con la interfaz de otro desarrollador. Con
este patrón, solo se devuelve una _API_ pública, manteniendo privada todo lo demás
dentro del cierre.

```js
var testModule = (function() {

    var counter = 0;

    return {

        incrementCounter: function() {
            return counter++;
        },

        resetCounter: function() {
            console.log("counter value prior to reset: " + counter);
            counter = 0;
        }
    };

})();

// Increment our counter
testModule.incrementCounter();

// Check the counter value and reset
// Outputs: counter value prior to reset: 1
testModule.resetCounter();
```
Aquí, otras partes del código no pueden leer directamente el valor de nuestro
`incrementoCounter ()` o `resetCounter ()`. La variable del contador está
totalmente protegida de nuestro ámbito global, por lo que actúa como una
variable privada, su existencia está limitada dentro del cierre del módulo, de
modo que el único código capaz de acceder a su ámbito son nuestras dos funciones.

### Variaciones del Patrón del Modulo

#### Import Mixins

Esta variación del patrón demuestra cómo los globales (por ejemplo, `jQuery`,
`Underscore`) se pueden pasar como argumentos a la función anónima de nuestro
módulo. Esto efectivamente nos permite importarlos y localmente usarlos como
deseamos.

```js
// Global module
var myModule = (function(jQ, _) {

    function privateMethod1() {
        jQ(".container").html("test");
    }

    function privateMethod2() {
        console.log(_.min([10, 5, 100, 2, 1000]));
    }

    return {
        publicMethod: function() {
            privateMethod1();
        }
    };

    // Pull in jQuery and Underscore
})(jQuery, _);

myModule.publicMethod();
```

#### Exports

Esta siguiente variación nos permite declarar globales sin consumirlos y
podría igualmente apoyar el concepto de importaciones globales visto en el
último ejemplo.

```js
// Global module
var myModule = (function() {

    // Module object
    var module = {},
        privateVariable = "Hello World";

    function privateMethod() {
        // ...
    }

    module.publicProperty = "Foobar";
    module.publicMethod = function() {
        console.log(privateVariable);
    };

    return module;

})();
´´´
