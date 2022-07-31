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

## Configuración de webpack.config.js

⚙️ Configuración de webpack.config.js
<h4>Apuntes</h4>
El archivo de configuración nos va ayudar a poder establecer la configuración y elementos que vamos a utilizar
Para poder crear el archivo de configuración en la raíz del proyecto creamos un archivo llamado webpack.config.js
En el mismo debemos decir
El punto de entrada
Hacia a donde a enviar la configuración de nuestro proyecto
Las extensiones que vamos usar
const path = require('path');

```js
module.exports = {
  // Entry nos permite decir el punto de entrada de nuestra aplicación
  entry: "./src/index.js",
  // Output nos permite decir hacia dónde va enviar lo que va a preparar webpacks
  output: {
    // path es donde estará la carpeta donde se guardará los archivos
    // Con path.resolve podemos decir dónde va estar la carpeta y la ubicación del mismo
    path: path.resolve(__dirname, "dist"),
    // filename le pone el nombre al archivo final
    filename: "main.js"
  },
  resolve: {
    // Aqui ponemos las extensiones que tendremos en nuestro proyecto para webpack los lea
    extensions: [".js"]
  },
}
```

El flag —config indica donde estará nuestro archivo de configuración
npx webpack --mode production --config webpack.config.js
Para poder hacerlo más amigable el comando puedes crear un script en package.json
"scripts": {
		...
    "build": "webpack --mode production --config webpack.config.js"
  },
RESUMEN: Puedes crear un archivo webpack.config.js en el cual estarán las configuraciones con las cuales webpack trabajara, entre ellas están los puntos de entrada y salida, extensiones de archivos, entre otras características que se verán próximamente en él curso.



Para el que tenga dudas similares a las mias:

require(“path”)
require es una forma de importar módulos en node.
path es un objeto o clase que viene por defecto en node. Viene con varios métodos que podemos usar https://nodejs.org/api/path.html

__dirname
dirname lo incluye node también. Imprime el directorio actual en el que esta funcionando el proyecto de node, por ejemplo si usas node en /Tupc/fulanito/proyectos. Lo usamos porque si subimos este código a un servidor en la nube, el directorio en el que vamos a trabajar en esa máquina en la nube va a ser diferente al de nuestro pc https://nodejs.org/docs/latest/api/modules.html#__dirname

path.resolve()
Es un método de path. Sirve simplemente para concatenar direcciones. Si usamos path.resolve("/mipc", “/fulanito”), el resultado sería /mipc/fulanito https://nodejs.org/api/path.html#pathresolvepaths

```js
const path = require('path');

module.exports = {
    entry: './src/index.js', //Punto de entrada
    output: { // Hacia donde vamos a enviar lo que va a preparar webpack
        path: path.resolve(__dirname, 'dist'), // Nombre del directorio
        filename: 'main.js' // Nombre del archivo
    },
    resolve: {
        extensions: ['.js']
    }
}
```

Webpack config generator
Con esto puedes seleccionar los frameworks, preprocesadores, plugins, linternas, optimización, TODO (excepto pug :'v)
https://createapp.dev/webpack/no-library
aca tienen uno con muchas cosas seleccionadas

## Babel Loader para JavaScript

Babel es para que el proyecto sea compatible en todos los navegadores

💛 Babel Loader para JavaScript
Babel te permite hacer que tu código JavaScript sea compatible con todos los navegadores
Debes agregar a tu proyecto las siguientes dependencias
NPM

npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
Yarn

yarn add -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
babel-loader nos permite usar babel con webpack
@babel/core es babel en general
@babel/preset-env trae y te permite usar las ultimas características de JavaScript
@babel/plugin-transform-runtime te permite trabajar con todo el tema de asincronismo como ser async y await
Debes crear el archivo de configuración de babel el cual tiene como nombre .babelrc
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-transform-runtime"
  ]
}
Para comenzar a utilizar webpack debemos agregar la siguiente configuración en webpack.config.js
{
...,
module: {
    rules: [
      {
        // Test declara que extensión de archivos aplicara el loader
        test: /\.js$/,
        // Use es un arreglo u objeto donde dices que loader aplicaras
        use: {
          loader: "babel-loader"
        },
        // Exclude permite omitir archivos o carpetas especificas
        exclude: /node_modules/
      }
    ]
  }
}
RESUMEN: Babel te ayuda a transpilar el código JavaScript, a un resultado el cual todos los navegadores lo puedan entender y ejecutar. Trae “extensiones” o plugins las cuales nos permiten tener características más allá del JavaScript común

## HTML en Webpack

HtmlWebpackPlugin
Es un plugin para inyectar javascript, css, favicons, y nos facilita la tarea de enlazar los bundles a nuestro template HTML.

Instalación
npm

npm i html-webpack-plugin -D
yarn

yarn add html-webpack-plugin -D
Al webpack config queda asi

const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'production', // LE INDICO EL MODO EXPLICITAMENTE
    entry: './src/index.js', // el punto de entrada de mi aplicación
    output: { // Esta es la salida de mi bundle
        path: path.resolve(__dirname, 'dist'),
        // resolve lo que hace es darnos la ruta absoluta de el S.O hasta nuestro archivo
        // para no tener conflictos entre Linux, Windows, etc
        filename: 'main.js', 
        // EL NOMBRE DEL ARCHIVO FINAL,
    },
    resolve: {
        extensions: ['.js'] // LOS ARCHIVOS QUE WEBPACK VA A LEER
    },
    module: {
        // REGLAS PARA TRABAJAR CON WEBPACK
        rules : [
            {
                test: /\.m?js$/, // LEE LOS ARCHIVOS CON EXTENSION .JS,
                exclude: /node_modules/, // IGNORA LOS MODULOS DE LA CARPETA
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    },
    // SECCION DE PLUGINS
    plugins: [
        new HtmlWebpackPlugin({ // CONFIGURACIÓN DEL PLUGIN
            inject: true, // INYECTA EL BUNDLE AL TEMPLATE HTML
            template: './public/index.html', // LA RUTA AL TEMPLATE HTML
            filename: './index.html' // NOMBRE FINAL DEL ARCHIVO
        })
    ]
}

## Loaders para CSS y preprocesadores de CSS

📘 Loaders para CSS y preprocesadores de CSS
<h4>Ideas/conceptos claves</h4>
Un preprocesador CSS es un programa que te permite generar CSS a partir de la syntax única del preprocesador. Existen varios preprocesadores CSS de los cuales escoger, sin embargo, la mayoría de preprocesadores CSS añadirán algunas características que no existen en CSS puro, como variable, mixins, selectores anidados, entre otros. Estas características hacen la estructura de CSS más legible y fácil de mantener.

post procesadores son herramientas que procesan el CSS y lo transforman en una nueva hoja de CSS que le permiten optimizar y automatizar los estilos para los navegadores actuales.

<h4>Apuntes</h4>
Para dar soporte a CSS en webpack debes instalar los siguientes paquetes
Con npm

npm i mini-css-extract-plugin css-loader -D
Con yarn

yarn add mini-css-extract-plugin css-loader -D
css-loader ⇒ Loader para reconocer CSS
mini-css-extract-plugin ⇒ Extrae el CSS en archivos
Para comenzar debemos agregar las configuraciones de webpack
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
	...,
	module: {
    rules: [
      {
        test: /\.(css|styl)$/i,
        use: [
          MiniCssExtractPlugin.loader,
          "css-loader",
        ]
      }
    ]
  },
  plugins: [
		...
    new MiniCssExtractPlugin(),
  ]
}
Si deseamos posteriormente podemos agregar herramientas poderosas de CSS como ser:
pre procesadores
Sass
Less
Stylus
post procesadores
Post CSS
RESUMEN: Puedes dar soporte a CSS en webpack mediante loaders y plugins, además que puedes dar superpoderes al mismo con las nuevas herramientas conocidas como pre procesadores y post procesadores

Para sass

npm i -D node-sass sass-loader
Añadimos el loader al arreglo de loaders y modificamos un poco la expresion regular

{
        test: /\.s?css$/,
        use: [MiniCssExtractPlugin.loader,
            "css-loader",
            "sass-loader"]
      },

Loaders
Fuera de contexto, webpack solamente entiende JavaScript y JSON. Los loaders nos permite procesar archivos de otros tipos para convertirnos en módulos válidos que serán consumidos por nuestras aplicaciones y agregadas como dependencias.

En alto nivel, los loaders poseen 2 configuraciones principales:

test - propiedad que identifica cuáles archivos deberán ser transformados
use - propiedad que identifica el loader que será usado para transformar a dichos archivos
Plugins
Mientras los loaders transforman ciertos tipos de módulos, los plugins _son utilizados para extender tareas específicas, como la optimización de paquetes, la gestión de activos y la inyección de variables de entorno.

Una vez importado el plugin, podemos desear el personalizarlos a través de opciones.

## Copia de archivos con Webpack

Si tienes la necesidad de mover un archivo o directorio a tu proyecto final podemos usar un plugin llamado “copy-webpack-plugin”
Para instalarlo debemos ejecutar el comando
Para npm

npm i copy-webpack-plugin -D
Para yarn

yarn add copy-webpack-plugin -D
Para poder comenzar a usarlo debemos agregar estas configuraciones a webpack.config.js
...
const CopyPlugin = require('copy-webpack-plugin');

module.exports = {
	...
  plugins: [
    new CopyPlugin({
      patterns: [
        {
          from: path.resolve(__dirname, "src", "assets/images"),
          to: "assets/images"
        }
      ]
    }),
  ]
}
Es importante las propiedades from y to
From ⇒ que recurso (archivo o directorio) deseamos copiar al directorio final
To ⇒ en que ruta dentro de la carpeta final terminara los recursos

Resolve o Join path
Cuando trabajamos en entorno de Node, habrán ocasiones que deberamos describir, mediante una dirección absoluta, el directorio de trabajo. En Node, tenemos una libreía nativa pathpara resolver este caso.

Abrán veces que necesitmeos resolver o unir directorios de trabajos. Donde, con una simple declaración, podriamos caer en un sencillo copy & paste sin entender sus efectos (que pudiesen ser similares).

Cuando deseen estructurar un directorio de trabajo a partir de una dirección absoluta, sin importar el SO, se utiliza path.resolve([...paths]) por ello, si queremos utilizar nuestro directorio de trabajo como una referencia, utilizamos __dirname y de ahí, resolverá el conjunto de paths que le anexemos:

/*
En nuestro ejemplo, resolverá nuestro path en /user/path/to/workdirectory/ + src + assets/images
quedando algo similar a /users/path/to/js-portfolio/src/assets/images
*/
path.resolve(__dirname, 'src', 'assets/images')
Se tendrá que ser cuidadoso en el proceso de construcción porque cada forma de escribir el path, generará en un path diferente:

path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif'

## Loaders de imágenes

