# Elementos que componen el diseño web

Es importante entender la estructura básica de una aplicación web, en este
documentos se explica brevemente los elementos que componen una pagina o
aplicación web.

## En la web existen basicamente tres perfiles:

1. **Frontend:** interacción directa con el usuario, HTML CSS y JavaScript.
HTML (hypertext markup language) es básicamente el lenguaje de modelado de la 
información, es importante tener en cuenta que HTML no es un lenguaje de 
programación. CSS (cascading stylesheet) es un lenguaje declarado usando estilos
en cascada para aplicarle diseño gráfico a el HTML, sirve también para darle
estilo a otras cosas, pero principalmente CSS se usa en el diseño web. JavaScript
es un lenguaje de programación y de hecho es el único lenguaje de programación 
en el mundo del frontend, existen algunos frameworks tales como jquery, prototype, 
angular, backbone y muchos otros que están basados o creados en JacaScript,
javascript NO ES JAVA.

2. **Backend:** backend es básicamente el proceso por el cual se accede, 
procesa y se modifica la información de una base de datos que se encuentra del 
lado del servidor implementando algún tipo de lenguaje de programación (php, java, 
ruby on rails, MySql, MongoDB) o algún framework como Django o Node.JS y se 
envía al frontend para que sea vista por el usuario.

3. **Bases de datos:** todo arranca con bases de datos, algunos ejemplos de bases 
de datos son MySql, Postgres, MongoDB; Las bases de datos son las encargadas
de almacenar la información que se va a mostrar al usuario en la aplicación
o pagina web, en la fase del backend se establece la comunicación entre la
interfaz de usuario y los datos que se encuentran almacenados en la base de datos
del servidor.

## HTML5 conceptos basicos y maquetacion

El codigo HTML esta compuesto básicamente por 3 etiquetas, `<html>`, `<head>` y 
`<body>`, aparte de estos tres existe un requerimiento que es mas importante aun
y es el `<!DOCTYPE html>` esto no es una etiqueta en si sino una declaración del
lenguaje que vamos a usar, con esto el navegador puede reconocer que lo que se
tiene en el documento es una pagina web HTML, en este caso HTML5. las etiquetas
en HTML funcionan básicamente como un árbol, en donde se parte de una rama
principal que se va desplegando en ramas mas pequeñas.

CSS: estas siglas significan cascading style sheets, y es el encargado de 
definir cual va a ser la apariencia de nuestra estructura HTML. el concepto de 
cascada define que en el momento que yo aplico un estilo a un elemento, todos 
sus hijos van a heredar dicha propiedad de ser posible.

* [reset.css](http://meyerweb.com/eric/tools/css/reset/)
* www.color-hex.com
* [normalize.css](https://necolas.github.io/normalize.css/)
* www.placehold.it
