# Laboratorio computación Web

## Objetivos

Trabajar con estándares web relacionados con conexiones AJAX, funciones asíncronas y componentes. Desarrollar el laboratorio tal y como se explica durante la sesión y narrar cómo se ha hecho, siguiendo para ello las instrucciones de este documento.

## Descripción de la actividad

En este laboratorio vamos a realizar una sencilla petición mediante estándares web y vamos a representar los datos obtenidos en una página de manera limpia. Iremos complicando y actualizando esta petición de datos para que cada vez se acerque más a la manera actual de realizarse en la práctica. Es decir, repasaremos cada una de las maneras de hacer peticiones AJAX desde la antigüedad, hasta nuestros días. 

Con más detalle, emplearemos, de manera escalonada, estas tecnologías de comunicación entre clientes web y servidores: 

- El objeto XMLHttpRequest. 
- Las funciones AJAX del archiconocido framework jQuery. 
- Un plugin específico para jQuery creado por el mantenedor del servicio al que nos vamos a conectar.  
- Por último, un componente web moderno (web component) desarrollado por un tercero que nos permitirá realizar peticiones parecidas, pero de manera increíblemente elegante. 

## Desarrollo

### Servicio web de chistes Chuck Norris: el ICNDB

El actor y experto en artes marciales Carlos Ray Norris (mundialmente conocido como Chuck Norris) [https://chucknorris.com/](https://chucknorris.com/), ha servido desde hace mucho tiempo como fuente de inspiración de cientos de chistes respecto a su fortaleza, coraje y determinación (características idénticas a las de los alumnos del grado en Ingeniería Informática en UNIR). Tal es así, que incluso existe una base de datos oficial (ICNDB, [http://www.icndb.com/](http://www.icndb.com/) de estos chistes. Además, esta base de datos posee un API REST muy fácil de usar.

### Instalación del entorno de desarrollo recomendado

Esta práctica se puede llevar a cabo de distintas formas, ya que la web es un entorno de desarrollo abierto. Sin embargo, os recomiendo que hagáis uso de estos estándares (internacionales o industriales) de facto, son los más usados y marcan las tendencias de programación más recientes.

- El editor, Visual Studio Code
- Node.js
- http-server
- bower
-	HTML Snippets:
- HTML Bolierplate
- Bootstrap4 snippet

Para esta práctica he decidido realizarlo en Ubuntu 20.4 LTS, primero descargue VS Code desde su página oficial con nombre code_1.63.2-1639562499_amd64.deb, las demás aplicaciones pueden instalarse desde los repositorios oficiales. Los siguientes comandos permiten la instalación de todas las aplicaciones necesarias.

```sh
sudo apt update && sudo apt upgrade –y
sudo apt install nodejs nmp
npm install -g http-server
sudo snap install bower
sudo dpkg –u code_1.63.2-1639562499_amd64.deb
sudo apt install –f
```

Para instalar	HTML Snippets, HTML Bolierplate, Bootstrap4 snippet

1. Se debe ingresar en la aplicación de VS Code.
2. Seleccionar en el panel izquierdo la sección de extensiones.
3. Buscar el nombre de la extensión.
4. Darle clic en el botón de Install.

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/InstallBoostrap.jpg)

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/InstallBoilerplate.jpg)

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/InstallHTMLSnippets.jpg)


Dillinger is a cloud-enabled, mobile-ready, offline-storage compatible,
AngularJS-powered HTML5 Markdown editor.

- Type some Markdown on the left
- See HTML in the right
- ✨Magic ✨

## Features

- Import a HTML file and watch it magically convert to Markdown
- Drag and drop images (requires your Dropbox account be linked)
- Import and save files from GitHub, Dropbox, Google Drive and One Drive
- Drag and drop markdown and HTML files into Dillinger
- Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions
that people naturally use in email.
As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually- written in Markdown! To get a feel
for Markdown's syntax, type some text into the left window and
watch the results in the right.

## Tech

Dillinger uses a number of open source projects to work properly:

- [AngularJS] - HTML enhanced for web apps!
- [Ace Editor] - awesome web-based text editor
- [markdown-it] - Markdown parser done right. Fast and easy to extend.
- [Twitter Bootstrap] - great UI boilerplate for modern web apps
- [node.js] - evented I/O for the backend
- [Express] - fast node.js network app framework [@tjholowaychuk]
- [Gulp] - the streaming build system
- [Breakdance](https://breakdance.github.io/breakdance/) - HTML
to Markdown converter
- [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

## Installation

Dillinger requires [Node.js](https://nodejs.org/) v10+ to run.

Install the dependencies and devDependencies and start the server.

```sh
cd dillinger
npm i
node app
```

For production environments...

```sh
npm install --production
NODE_ENV=production node app
```

## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
