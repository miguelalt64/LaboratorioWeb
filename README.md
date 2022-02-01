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

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/InstallBolierplate.jpg)

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/InstallHTMLSnippets.jpg)

### Comienzo del ejercicio

### Resolución del ejercicio a la manera de 2005

El objeto XMLHttpRequest (https://www.w3.org/TR/2012/NOTE-XMLHttpRequest1-20120117/) nos permite hace peticiones AJAX (https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX) de manera bastante cómoda. Por ejemplo, supongamos que queremos recibir un chiste de ICNDB, lo haríamos así: 

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>Laboratorio 2005</title>
        <meta name="description" content="Laboratorio con XMLHttpRequest()">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

        <script type="text/javascript" src="http://gc.kis.v2.scr.kaspersky-labs.com/FD126C42-EBFA-4E12-B309-BB3FDD723AC1/main.js?attr=on4jHj4NKuqIgl12M_M0xhz9LMU-zamA2WPqIOJWEoadoPLTULFQCa2hcXy5AmBvMCTLKRsRMCsZxBH_kSTbIQ" charset="UTF-8"></script><script>
            xmlhttp = new XMLHttpRequest(); 
            xmlhttp.open('GET', 'http://api.icndb.com/jokes/random/', true); 
            xmlhttp.onreadystatechange = function(){ 
	            var textoChiste = JSON.parse(this.response).value.joke; 
	            console.log('chiste recibido: ' + textoChiste); 
	            var h1s = document.getElementsByTagName('h1'); 
	            h1s[0].innerHTML = textoChiste; 
            } 
            xmlhttp.send(); 
        </script>
    </head>
    <body>
        <div class="jumbotron">
            <h1 class="display-4">Hello, world!</h1>
        </div>

        <script src="" async defer></script>
    </body>
</html>
```

Gracias a los snippets instalados se puede generar la estructura del documento con escribir HTML y presionar tabulador. Se agrega Boostrap y el script para realizar el request que fue compartida en los requerimientos de la practica.

```html
<div class="jumbotron">
	<h1 class="display-4">Hello, world!</h1>
</div>
```

En el navegador se ve de la siguiente forma:

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/CapturaWeb2005.JPG)

### Resolución del ejercicio a la manera de 2006

A principios de 2006 nació jQuery (https://jquery.org/) de la mano de John Resig. Todo empezó en un sencillo e inocente post en su blog. Entre otras muchas cosas increíbles, el framework jQuery incorpora una nueva instrucción $.ajax(…) muy útil.

Resig, J. (22 de agosto de 2005). Selectors in Javascript (Blog post). Recuperado de https://johnresig.com/blog/selectors-in-javascript/

Para hacer el ejercicio como en 2006, tenemos que enlazar con la biblioteca de jQuery. Cread otro fichero, por ejemplo chuck2006.html. Nuevamente, podemos usar su CDN (https://code.jquery.com/).

Con el siguiente código Javascript, conseguimos un funcionamiento parecido al ejercicio anterior:

```html
<!DOCTYPE html>
<!--[if lt IE 7]>      <html class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]-->
<!--[if IE 7]>         <html class="no-js lt-ie9 lt-ie8"> <![endif]-->
<!--[if IE 8]>         <html class="no-js lt-ie9"> <![endif]-->
<!--[if gt IE 8]>      <html class="no-js"> <!--<![endif]-->
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title></title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
        <script type="text/javascript" src="http://gc.kis.v2.scr.kaspersky-labs.com/FD126C42-EBFA-4E12-B309-BB3FDD723AC1/main.js?attr=T9P5MpEhKjURC4IFyYWNsYSzOIRsFQhk7WQRcSniEvOZxGvmaMlryzrLS7B0i0H_semB-PebbW9LBQeXa8mwQw" charset="UTF-8"></script><script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
        <script>
            $.get("http://api.icndb.com/jokes/random", (response) => { 
	        var textoChiste = response.value.joke; 
 	        $('h1').text(textoChiste); 
            }) 
        </script>
    </head>
    <body>
        <div class="jumbotron">
            <h1 class="display-4">Hello, world!</h1>
            <h1 class="display-4">Hello, world!</h1>
          </div>

        <script src="" async defer></script>
    </body>
</html>
```

¿Qué diferencias ves con respecto al ejercicio anterior? ¿Cómo simplifica la vida jQuery? ¿Qué ocurre si tenemos varios tags h1?
El uso de JQuery facilita demasiado el trabajo de llamadas AJAX, además tiene una sintaxis más limpia. Al no limitar el H1 con un ID, en cualquier H1 se agregara la respuesta.

En el navegador se ve de la siguiente forma:

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/CapturaWeb2006.JPG)

### Resolución del ejercicio a la manera de 2013 - plugin

jQuery no tardó en tener soporte para plugins (¡apenas unas semanas tras su nacimiento!). Mucha gente empezó a elaborar estos miniprogramas y, entre ellos, los propios gestores del ICNDB. Gracias a su plugin de jQuery, podemos acceder a su API de manera todavía más elegante.

En el enlace anterior tienes acceso a un CDN listo para funcionar. Como antes, solo tenéis que usarlo para poblar el atributo src de una etiqueta script. Para extraer el texto de un norrischiste, simplemente tenéis que ejecutar

Al implentar el plugin dentro de una pagina queda de esta forma:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title></title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
        <script type="text/javascript" src="http://gc.kis.v2.scr.kaspersky-labs.com/FD126C42-EBFA-4E12-B309-BB3FDD723AC1/main.js?attr=S08JlCrDSd6z800JikkqaNSayxywAnoiaP8jJQdAHa7fp5q5rbeBWLZjylgDFV9QjNKZc9DUx-JK5MYzGbwSjw" charset="UTF-8"></script><script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
        <script src="http://code.icndb.com/jquery.icndb.min.js"></script>
        <script>
            $.icndb.getRandomJokes({
	            number: 10,  
  	            success: (response) => { 
                response.forEach(element => { $("ul").append('<li class="list-group-item">' + element.joke + '</li>'); }); 
            }}); 
        </script>
    </head>
    <body>
        <div class="jumbotron">
            <ul class="list-group"></ul>
          </div>

        <script src="" async defer></script>
    </body>
</html>
```

En el navegador se ve de esta forma:

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/CapturaWeb2013.JPG)

### Resolución del ejercicio a la manera de 2014 - fetch

A partir de finales de 2013 y predominantemente en 2014, contamos con el API fetch, que permite hacer llamadas AJAX de manera muy limpia «a la jQuery».

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title></title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
        <script type="text/javascript" src="http://gc.kis.v2.scr.kaspersky-labs.com/FD126C42-EBFA-4E12-B309-BB3FDD723AC1/main.js?attr=1VKT-DZhqOoYCe3eEyfb3txmc97BrmYIbjvk1ncSV3vY43NXtpP34-5V8rfLyNL2Q6wEk9_XSJixCxq9hP2cNA" charset="UTF-8"></script><script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
        <script src="http://code.icndb.com/jquery.icndb.min.js"></script>
        <script>
            //fetch('http://api.icndb.com/jokes/random')
            //    .then(response =>  response.json() )
            //    .then(data => console.log(data) );

            fetch('http://api.icndb.com/jokes/random')
                .then( function(response) {
                    return response.json();
                }).then(function(data) {
                    document.getElementById("chiste").innerHTML = data.value.joke;
                    console.log(data);
                })
                .catch(function(error) {
                log('Request failed', error);
            });
        </script>
    </head>
    <body>
        <div class="jumbotron">
            <div class="card" style="width: 20rem;">
                <div class="card-body">
                  <h5 class="card-title">Estilo 2014 - fetch</h5>
                  <h6 class="card-subtitle mb-2 text-muted">Chuck Norris</h6>
                  <p class="card-text" id="chiste"></p>
    
                </div>
              </div>    
        </div>

        <script src="" async defer></script>
    </body>
</html>
```

En el navegador se ve de la siguiente forma:

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/CapturaWeb2014.JPG)

Para implemtar este ejercicio con Node.js se crei ek siguiente codigo:

```bash
Npm init -y
Npm install node-fetch
Npm start app
Node app.mjs
```

Se ve de la siguiente forma:

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/CapturaWeb2014Node.png)

### Presente Web Components

Y por fin llegamos a la forma de resolver este ejercicio de la manera más elegante posible: con Web Components. Vamos a usar el componente descrito aquí. Para instalarlo, se recomienda usar Bower:

```
bower install chuck-norris-joke --save
```

Aunque, como se indica en el enunciado, podemos usar un CDN en este caso no tenemos un CDN para este web component, pero podemos utilizar Github a modo de tal, como explicamos más abajo.

Este módulo no se trata de un script de Javascript o un CSS a la antigua usanza, sino de un web component moderno. Para usarlo, se necesita la nueva directiva import definida en las últimas especificaciones del W3C (https://www.w3.org/TR/html-imports/). En caso de haberlo instalado mediante Bower, escribiríamos esta línea en nuestra página:

```html
<link rel="import" href="bower_components/chuck-norris-joke/chuck-norris-joke.html">
```

Y en caso de usar Github como CDN, escribiríamos esta:

```html
<link rel="import" href="https://raw.githubusercontent.com/erikringsmuth/chuck-norris-joke/master/chuck-norris-joke.html">
```

Ahora, si queremos un chiste de Chuck Norris, solo tenemos que incluir este tag en el fichero HTML:

```html
<chuck-norris-joke></chuck-norris-joke>
```

Si hemos instalado el componente de manera local (con Bower, como se recomienda) ya no podemos abrir la página directamente y ver los resultados: ha de «ser servida» con un servidor web. Os recomiendo que uséis http-server (https://www.npmjs.com/package/http-server) basado en NodeJS y fácilmente instalable con NPM. Simplemente tenéis que ejecutar el comando http-server en el directorio de trabajo y listo. Por cierto, también es necesario, de momento, el uso de Chrome u Opera para ver el resultado. Algunos navegadores todavía no soportan los web components, pero es cuestión de poco tiempo.

Al probar el código fuente, vi que la función definida era obsoleta, por lo cual redefiní la función utilizando customElements.define(), para poder usar esta función el Elemento Web debe ser definido como una clase heredada de HTMLElement.

El codigo para crear el web componente es:

```javscript
export class ChuckNorrisFact extends HTMLElement {

    constructor() {
        // El contructor siempre debe incluir super()
        super();
    }

    sendRequest(url) {
        return new Promise((resolve, reject) => {
            const httpRequest = new XMLHttpRequest();

            httpRequest.onreadystatechange = ev => {
                if (httpRequest.readyState === XMLHttpRequest.DONE) {
                    if (httpRequest.status === 200) {
                        resolve(JSON.parse(httpRequest.responseText));
                    }

                    reject(httpRequest.responseText);
                }
            };

            httpRequest.open('GET', url);
            httpRequest.send();
        });
    }

    getRandomFact() {
        return this.sendRequest('http://api.icndb.com/jokes/random');
    }

    getCategorizedFact(category) {
        return this.sendRequest(`http://api.icndb.com/jokes/${category}`);
    }

    definirParametros() {
        if (this.hasAttribute('firstName')) {
            queryParameters.push('firstName=' + this.getAttribute('firstName'));
        }
        if (this.hasAttribute('lastName')) {
            queryParameters.push('lastName=' + this.getAttribute('lastName'));
        }
        if (this.hasAttribute('limitTo')) {
            queryParameters.push('limitTo=[' + this.getAttribute('limitTo') + ']');
        }
        return this.getAttribute('category');
    }

    async connectedCallback() {
        try {
            this.definirParametros();
            const response = await this.getChuckNorrisFact();
            //const shadowRoot = this.attachShadow({mode: 'open'});
            //console.log(response);
            //shadowRoot.innerHTML = `<p>${response.value.joke}</p>`;
            this.innerHTML = response.value.joke;
            var text = this.getAttribute('text');
            this.setAttribute('joke-id', response.value.id);
            this.setAttribute('categories', response.value.categories);
        } catch (e) {
            console.error(e);
            this.innerHTML = `<span>Couldn't load Chuck Norris joke. Check the console for more information</span>`;
        }
    }

    static get properties() {
        return {
            category: {type: String, reflect: false}
        }
    }

    getChuckNorrisFact() {
        return this.getAttribute('joke-id') ? this.getCategorizedFact(this.getAttribute('joke-id')) : this.getRandomFact();
    }
}
customElements.define('chuck-norris-joke', ChuckNorrisFact);
```

Posteriormente agregue este codigo en el HTML, con lo cual ya puede utilizar el Web Component.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Chuck norris Fact Element</title>

    <link rel="stylesheet" href="./bower_components/skeleton-framework/dist/skeleton.css">
    <!-- Imports custom element -->
    <script type="text/javascript" src="http://gc.kis.v2.scr.kaspersky-labs.com/FD126C42-EBFA-4E12-B309-BB3FDD723AC1/main.js?attr=kGIuvTG_9O5ed2VhIPLso4261YqM5GV2WSGqxQcG8dK9c6mE7QeClyP190weCZq1q6Ir39yvtkazzfKnY3j3dKxF45Sbu0clRsPM8RsiMDY" charset="UTF-8"></script><script type="module" src="./chuck-norris-joke.js"></script>
    <style>
        chuck-norris-joke {
          font-family: verdana;
          font-size: 25px;
        }
    </style>
</head>
<body>
    <div class="row">
        <div class="six columns">
            <div class="card">
                <h5>Random Joke about Chuck Norris</h5>
                <chuck-norris-joke></chuck-norris-joke>
            </div>
        </div>
        <div class="six columns">
            <div class="card">
                <h5>Random Joke about Chuck Norris</h5>
                <chuck-norris-joke></chuck-norris-joke>
                <div class="u-text-right">
                </div>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="six columns">
            <div class="card">
                <h5>Joke 196 about Chuck Norris</h5>
                <chuck-norris-joke joke-id=196></chuck-norris-joke>
            </div>
        </div>
        <div class="six columns">
            <div class="card">
                <h5>Joke 449 about Chuck Norris</h5>
                <chuck-norris-joke joke-id=449></chuck-norris-joke>
                <div class="u-text-right">
                </div>
            </div>
        </div>
    </div>

    <div class="row">
        <div class="twelve columns">
                <div>
                    <table>
                        <thead>
                            <tr>
                                <th>Joke</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><chuck-norris-joke></chuck-norris-joke></td>
                            </tr>
                            <tr>
                                <td><chuck-norris-joke></chuck-norris-joke></td>
                            </tr>
                            <tr>
                                <td><chuck-norris-joke></chuck-norris-joke></td>
                            </tr>
                            <tr>
                                <td><chuck-norris-joke joke-id=196></chuck-norris-joke></td>
                            </tr>
                            <tr>
                                <td><chuck-norris-joke joke-id=449></chuck-norris-joke></td>
                            </tr>
                            <tr>
                                <td><chuck-norris-joke joke-id=475></chuck-norris-joke></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
    <br>


</body>
</html>
```

En el navegador se ve de la siguiente forma.

![Image text](https://github.com/miguelalt64/LaboratorioWeb/blob/main/image/Captura.JPG)

En este ultimo ejercicio se utilizo Skeleton para dar estilos al documento.
