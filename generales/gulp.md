# Apuntes GULP

Gulp es básicamente un automatizador de tareas que nos permite hacer mas 
productivo nuestro flujo de trabajo, nos ahorra tiempo al momento de ejecutar 
tareas como compilar nuestro código css y html por medio de pre procesadores, 
minificar archivos y dejarlos listos para producción o incluso también comprimir 
imágenes para que tengan el peso correcto entre muchas otras.

## Flujo de trabajo de Gulp:

A continuación se muestra un flujo de trabajo común al momento de estar usando 
Gulp:

1. Empezamos por definir la tarea que quiero lograr.

2. Dentro de la tarea, se cargan los archivos que se desean procesar por 
medio de Gulp.

3. De forma opcional, una vez que los archivos se encuentran en
procesamiento, se puede elegir entre realizar una o mas modificaciones en el 
archivo.

4. Enviar los nuevos (posiblemente modificados) archivos a la carpeta de
destino.

## API de Gulp:

Usar Gulp es sencillo, no es necesario tener conocimientos avanzados sobre como 
funciona para poder realizar un trabajo mas productivo.

- gulp.task --> Define una tarea

- gulp.src --> Lee un archivo de entrada

- gulp.dest --> Especifica una ruta de destino

- gulp.watch --> Esta atento a los cambios realizados en el archivo

## Instalación

La instalación de Gulp se hace por medio de npm (node package manager), lo que 
quiere decir que es necesario que hayamos hecho la instalación previa de nodejs
y npm. Gulp como todos los otros paquetes de node puede ser instalado de forma 
local o global, se recomienda instalarlo de las dos formas al comento de usarlo.

- Instalación global:

```sh
$ npm install gulp -g
```

- Instalación Local:

```sh
$ cd my_project
$ npm install --save-dev gulp
```
Este comando instalara Gulp de forma local en el directorio de nuestro proyecto,
el argumento --save-dev le hace saber a npm que debe actualizar nuestro archivo 
package.json con un nuevo modulo en nuestras devDependencies.

## Usando GULP

La forma en la que nosotros usamos Gulp es por medio de un gulpfile, un gulpfile 
es un archivo que actuara como manifiesto para definir nuestras tareas, las 
tareas que nosotros queramos ejecutar estarán dentro de este archivo. Los 
gulpfiles están escritos en javascript por lo tanto deben llamarse gulpfile.js y 
deberá ser almacenado siempre en la raíz de nuestro proyecto.

Teniendo ya nuestro archivo gulpfile.js procedemos a probar que todo este 
funcionando por medio de una tarea sencilla:

```js
var gulp = require('gulp');

gulp.task('hello-world', function() {
	console.log('hello world!');
});
```

require es una función de node que añade referencias a los node modules que 
tenemos instalados. Una vez que hacemos referencia a un node module, podemos 
usarlo para crear una tarea, en el ejemplo anterior simplemente se creo una 
tarea que escribe un mensaje en consola, pero las tareas pueden llegar a ser 
tan complejas como se necesite.

Ejemplo de como compilar nuestro css por medio de Stylus estando atento a los 
cambios:

Este ejemplo requiere haber instalado el modulo `gulp-stylus` anteriormente por 
medio del comando: `$ npm install --save-dev gulp-stylus`

```js
var gulp = require('gulp');
var stylus = require('gulp-stylus');

gulp.task('build:css', function() {
	gulp.src('./src/styles/app.styl')
	.pipe(stylus())
	.pipe(gulp.dest('./build/css'))
});

gulp.task('watch', function() {
  gulp.watch('./src/styles/app.styl', ['build:css']);
});

gulp.task('default', ['build:css', 'watch']);
```

## Módulos de utilidad

- [borwser-sync](https://www.browsersync.io/docs/gulp/): realizar tareas para crear servidores y actualizar el browser 
cada vez que se realizan cambios en algun archivo.

- [gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin): comprime y procesa imágenes para que su peso sea el menor 
posible sin perder calidad.

- [gulp-jade](https://github.com/phated/gulp-jade): pre procesador de código para hacer la compilación a html.

- [gulp-stylus](https://github.com/stevelacy/gulp-stylus): pre procesador de código para hacer la compilación a css.

## Paginas de referencia:

- http://gulpjs.com/
- http://frontendlabs.io/1669--gulp-js-en-espanol-tutorial-basico-primeros-pasos-y-ejemplos
	