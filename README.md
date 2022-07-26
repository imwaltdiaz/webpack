# webpack🎲 

## ¿Qué es Webpack?

**Ideas/conceptos claves**
Module bundlers son herramientas de frontend que nos permiten usar archivos con módulos JavaScript, entre otras características y convertiros a un JavaScript el cual el navegador pueda entender

**Apuntes**
Webpack es una herramienta que nos permite preparar nuestro código para llevarlo a producción (module bundler)
Webpack nos permite trabajar con

- HTML
- CSS
- JavaScript
- Archivos estáticos
- Imágenes
- Fuentes

Tambien nos permite tener un modo en desarrollo para nuestros proyectos para hacer pruebas
Nacio en el 2012, desde ese entonces varias empresas lo usan como ser

- Twitter
- Instagram
- PayPal

También nos permite

- Gestionar dependencias
- Ejecutar tareas
- Conversión de archivos

Nos permite trabajar en módulos
Permitiéndonos tener un código separado en desarrollo, pero en producción en una fuente
Webpack permite tener módulos de JS en formato
AMD
Common JS
ES15
RESUMEN: Webpack es un module bundler que nos permite trabajar con una variedad de tecnologías web empezando desde HTML y terminando con JS. Además de tener soporte para archivos estáticos

## Tu primer build con webpack

webpack optimiza tu codigo en js.

Tu primer build con Webpack
Creamos una carpeta como le quieras llamar
(Bueno no! si eres de Windows te dejo este articulo cortito de los nombres de carpetas PROHIBIDOS )
La creamos desde la terminal con mkdir y luego entramos a ella con cd

mkdir curso-webpack
cd curso-webpack
una vez que entres a la carpeta inicializamos nuestro repositorio con git

git init
El paso que sigue es inicializar nuestro proyecto con npm y si no sabes de npm aqui esta el curso del profesor

npm init -y
o si les da error “Invalid Name” usen para personalizar la configuración

npm init
y para abrir el proyecto como flash es poner en la terminal y les abre el editor ( si usas VS CODE)

code .
La carpeta SRC es el source de todo el proyecto ( index.js , imágenes, utils, assets, helpers, database, etc).

**Instalación de Webpack**
si no quieres escribir ese comando también puedes usar este
la i de install

npm i webpack webpack-cli -D
o si usas yarn usa

yarn add webpack webpack-cli -D
Y luego ejecutamos webpack
npx lo que hace es ejecutar paquetes directamente de npm, este viene instalado de npm

npx webpack
Al hacer esto webpack creo una carpeta llamada dist, esto lo hace por defecto webpack sin preguntarnos.
Modo de desarrollo
Por defecto webpack al compilar nuestro proyecto setea el modo “production” implícitamente pero podemos definirle el modo explícitamente corriendo:

npx webpack --mode production
npx webpack --mode development
La diferencia radica que el modo development deja el código mas legible para los desarrolladores pero con comentarios, el modo production deja el código comprimido y mas limpio para usarse.

Estamos trabajando con git submodulos: https://www.youtube.com/watch?v=YVUkxt3Bvwg

