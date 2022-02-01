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
