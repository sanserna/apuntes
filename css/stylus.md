# STYLUS

Stylus es un famoso pre-procesador de código que nos hace la vida mas fácil. Es
una herramienta indispensable que nos ayuda a optimizar y administrar fácilmente
nuestro código CSS. Con esta herramienta podemos realizar nuestro trabajo de una
manera mas rápida y ordenada, ahorrando tiempo y dando mejores resultados.

Su funcionamiento es muy simple, nosotros escribimos nuestro código CSS normal,
el de toda la vida en un archivo (generalmente CSS), los pre-procesadores lo que
hacen es optimizar ese código para generar un archivo CSS más liviano que aporta
de cara a la optimización de carga de un sitio web. Ese es todo el misterio no 
hay más. La sintaxis te Stylus permite ser usada de varias formas, la primera
de ellas nos da la posibilidad de no usar llaves de apertura y cierre `{}`, no
usar dos puntos al declarar una propiedad `:` y no usar punto y coma para
finalizar la declaración de una propiedad `;`. Sin embargo Stylus permite hacer
uso de la sintaxis CSS normal, simplemente hay que tener en cuenta que todo en
Stylus se basa en la indentación.

## Instalación de Stylus

Stylus necesita de node.js corriendo para poder funcionar por lo tanto el primer
paso será instalar node.js, para ello ingresamos al sitio oficial de [NodeJS](https://nodejs.org/en/) y le
damos al botón “Install”. Con ello nos descargará el instalador de nodejs.

Después de haber realizado la instalación de node.js podemos acceder al instalador
de paquetes de node llamado npm (node package manager). Para realizar la
instalación de Stylus de forma global ejecutamos el siguiente comando en nuestra
terminal de mac o en el CMD de windows:

```sh
$ npm install -g stylus
```

El flag `-g
- Variables: Hay dos formas de declarar una variable
	$nombreVariable = valor
	nombreVariable = valor

- Mixins ó funciones:
	nombreMixin(parametros->opcionales)
		propiedades

- Imports: una de las ventajas que ofrece u pre-procesador es que podemos tener 
nuestro codigo en diferentes archivos para que sea mas modular e importarlos en 
los archivos que queramos usarlos.

	@import 'styles/variables'
	@import 'normalize.css'
	@import 'styles/*'

- Built-in functions: Stylus por defecto nos ofrece un conjunto de funciones que 
podemos usar al memento de dar estilos.

	http://stylus-lang.com/docs/bifs.html

- Custom functions: Stylus también nos ofrece la posibilidad de crear nuestras 
propias funciones que retornaran un valor.

	add(a,b)
		a + b

	lo único que necesita una función es un valor de retorno, la función puede o 
	no recibir parámetros, y dichos parámetros pueden tener un valor por defecto 
	en caso de que no se de ningún valor, si se desea retornar múltiples valores
	se debe encapsular los valores en paréntesis (a b) o usar la palabra return.

- Interpolación: Stylus soporta interpolación usando los caracteres {} para 
encerrar una expresión que luego pasa a ser parte del identificador.

	-webkit-{'border' + 'radius'} pasa a ser -webkit-border-radius.

- Extensiones stylus: stylus permite utilizar extensiones que permiten darle una 
funcionalidad mas completa a stylus, como por ejemplo librerías de mixins o funciones.
	
	//-- nib --\\
	Es un conjunto de mixins para añadir prefijos a las propiedades CSS que los 
	requieren.

	* Lo primero que toca hacer para utilizar un plugin de stylus es instalarlo 
	por medio de la terminal, ya sea de forma global o local, en este caso 
	usaremos 'nib'.

		'npm install nib -g' -> se hace la instalacion de 'nib' de forma global, 
		en mac usar el comando sudo y en windows hacer la instalación con 
		permisos de administrador.

	* Una vez instalado el plugin hay que importarlo dentro de nuestro archivo 
	de stylus.

		@import 'nib'

	* Finalmente ejecutamos el comando de stylus en el terminal pero esta vez 
	indicándole que estamos haciendo uso de el plugin 'nib' -> para esto se usa 
	el flag '-u'.

		ej: 'stylus -u nib ./src/app.styl -w -o ./build'

	//-- Rupture --\\
	Es un plugin que nos permite añadir media queries de forma mas sencilla y 
	estandarizada.

	* Para utilizar este plugin por medio de la terminal, hay que instalarlo de 
	forma global.

		'npm install rupture -g' -> se hace la instalacion de 'rupture' de forma 
		global, en mac usar el comando sudo y en windows hacer la instalación 
		con permisos de administrador.

	* Rupture no requiere que hagamos un import en nuestro archivo de stylus, 
	simplemente debemos indicarle stylus en el comando que vamos a estar usando 
	rupture también.

		ej: 'stylus -u nib -u rupture app.styl'

	* https://github.com/jenius/rupture -> documentación del plugin.

	//-- Typographic --\\
	Plugin que permite hacer uso de las tipografias de forma responsive. El uso 
	de este plugin es recomendado para proyectos en los que se requiera el uso 
	de tipografias de forma agil y rapido.

		* Instalar por medio de la terminal de forma global o local.

			'npm install typographic'

		* Una vez instalado el plugin hay que importarlo dentro de nuestro 
		archivo de stylus.

			@import 'typographic'

		* Ejecutar el comando de stylus indicandole que se esta usando el plugin 
		de typographic.

			ej: 'stylus -u nib -u rupture -u typographic app.styl'

		* https://github.com/corysimmons/typographic -> documentación del plugin.
