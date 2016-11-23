# Selectores CSS

* Selectores básicos: 

	- Selector universal `*` -> este selector se refiere a todos y cada uno de los 
	elementos del documento.
	
	- Selectores de tipo etiqueta ej: `p`, `h1`, `h2`, `span`, etc.
	
	- Selector descendente ej: `p span {}`, `h1 span {}` etc -> este selector se 
	refiere a los elementos que se encuentran dentro de otros elementos, un 
	elemento es descendente de otro cuando se encuentra contenido dentro de sus 
	etiquetas de apertura y cierre.
	
	- Selector descendente directo ej: `header > ul {}`, `div > p {}` etc -> este 
	selector se refiere a los elementos directamente descendentes de otro elemento,
	es decir aquel elemento que se encuentra en el primer nivel de descendencia.
	
	- Selector de clase ej: `.navegación`, `.contenedor`, etc -> el selector aplica 
	estilos a todos los elementos nombrados con dicha clase, un mismo nombre de 
	clase puede ser aplicado a varios elementos.
	
	- Selector de ID ej: `#menu`, `#barraLateral`, etc -> el selector se refiere al 
	elemento cuyo ID sea el indicado, los ID's son únicos e irrepetibles, no 
	pueden haber dos elementos con el mismo ID.

## Combinación de selectores básicos

* Aplicar estilos a varios elementos: 

	- `h1, h2, h3, h4 {}` -> al separar los elementos con una coma, se seleccionan 
	varios elementos para los cuales se aplicaran los mismos estilos, esto 
	aplica también para nombre de clase y ID's.

	- `header, .navegacion, .contenedor > h1 {}` -> pueden haber combinaciones
	entre los distintos tipos de selectores básicos, en este caso se están 
	aplicado estilos al elemento `header`, a los elementos con nombre de clase 
	`.navegacion` y al elemento `h1` que es directamente descendente del elemento 
	con nombre de clase `.contenedor`.

	- `div.contenedor {}` -> pueden haber combinaciones entre selectores de tipo
	etiqueta y nombre de clase, en este caso se esta refiriendo a la etiqueta de 
	tipo div que tenga nombre de clase `.contenedor`.

	- `div#navegacion {}` -> esta combinación es igual a la anterior pero con 
	los ID's.

## Selectores CSS3 avanzados:
	
* Selector de atributo 

	- `elemento[atributo="valor"] {}` -> selecciona los elementos que 
	disponen del atributo y cuyo valor es exactamente la cadena de texto 
	indicada.
	
	- `elemento[atributo^="valor"] {}` -> selecciona todos los elementos que 
	disponen de ese atributo y cuyo valor comienza exactamente por la cadena
	de texto indicada.
	
	- `elemento[atributo$="valor"] {}` -> selecciona todos los elementos que 
	disponen de ese atributo y cuyo valor termina exactamente por la cadena 
	de texto indicada.
	
	- `elemento[atributo*="valor"] {}` -> selecciona todos los elementos que 
	disponen de ese atributo y cuyo valor contiene la cadena de texto indicada.

	- Selector adyacente ej: `h1 + h2 {}` ->  seleccionar elementos que son 
	hermanos, en este caso el primer elemento `h2` inmediatamente después a un `h1`.

	- Selector general de hermanos ej: `h1 ~ h2 {}` ->  selecciona todos los 
	hermanos del tipo de elemento especificado.

* Pseudo-elementos:

	- `::first-line` -> selecciona la primera linea de texto de un elemento.

	- `::first-letter` -> selecciona la primera letra del texto de un elemento.

	- `::before` -> selecciona la parte anterior al contenido de un elemento 
	para insertar nuevo contenido generado.

	- `::after` -> selecciona la parte posterior al contenido de un elemento 
	para insertar nuevo contenido generado.

	- `::selection` -> selecciona el texto que ha seleccionado un usuario con 
	su ratón o teclado.

	- `elemento:nth-child(numero)` -> selecciona el elemento indicado pero con 
	la condición de que sea el hijo enésimo de su padre. Este selector es 
	útil para seleccionar el segundo párrafo de un elemento, el quinto 
	elemento de una lista, etc. Esta pseudo clase permite el uso de 
	expresiones complejas `li:nth-child(2n+1)` -> selecciona todos los 
	elementos impares de una lista.

	- `elemento:nth-last-child(numero)` -> idéntico al anterior pero el número 
	indicado se empieza a contar desde el último hijo.

	- `elemento:empy` -> selecciona el elemento indicado pero con la condición 
	de que no tenga ningún hijo. La condición implica que tampoco puede 
	tener ningún contenido de texto.

	- `elemento:first-child` y `elemento:last-child` -> seleccionan los 
	elementos indicados pero con la condición de que sean respectivamente los 
	primeros o últimos hijos de su elemento padre.

	- `elemento:nth-of-type(numero)` -> selecciona el elemento indicado pero con 
	la condición de que sea el enésimo elemento hermano de ese tipo, esta 
	pseudo clase también permite expresiones complejas.

	- `elemento:nth-last-of-type(numero)` -> idéntico al anterior pero el número 
	indicado se empieza a contar desde el último hijo.

	- `:not(elemento)` -> selecciona todos los elementos de la página que no 
	sean del tipo de elemento especificado 

		- ej: `:not(p) {}` -> selecciona todos los elementos de la página que 
		no sean párrafos.

		- ej: `:not(#especial) {}` -> selecciona cualquier elemento cuyo 
		atributo id no sea "especial".

## Referencias

* http://www.w3.org/TR/css3-selectors/
* http://www.w3schools.com/cssref/css_selectors.asp
* http://www.css3.info/selectors-test/
