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

Comienzo del ejercicio

Resolución del ejercicio a la manera de 2005

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

