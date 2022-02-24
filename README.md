# App-Tiempo
#### En primer lugar hablaré de que trata mi proyecto, seguidamente explicaré lo que es una API y un pequeño resumen de como funciona.

## ¿De que trata mi proyecto?
El proyecto que he llevado a cabo muestra el tiempo en grados centígrados de la ciudad que quiera, una icono informativo de la situación meteorlógica que hace en el momento, el 
viento en km/h, un porcentaje de la probabilidad de precipitaciones y el nombre de la condición atmosférica.


## ¿Qué es una API?
API o *Application Programming Interfaces* es una abreviatura de Application Programming Interfaces, que en español significa interfaz de programación de aplicaciones. Es un 
conjunto de definiciones y protocolos que se utiliza para desarrollar e integrar el software de las aplicaciones y que permite comunicar aplicaciones de software entre ellas 
siguiendo unas determinadas reglas.


![Infografía del funcionamiento de una API](https://github.com/eSee3/App-Tiempo/blob/main/Tiempo/assets/API.PNG)
> Pablo Nevado | eSee3

## ¿Cómo Funciona una API?
Para entender el funcionamiento de una API hay que entender que no es un software que funciona independientemente, sino que es una extensión, que requiere de un sistema, una
aplicación o una plataforma en la cual agruparse. Las APIs deben integrarse a un sistema para funcionar.
Para usar una API, lo más probable es que necesites de una clave de API. Para saber si la API que deseas usar requiere este tipo de clave, puedes consultar la documentación para
conocer los requisitos de acceso del recurso que desees utilizar.
Casi todas las plataformas de desarrollo (Java, Node.js, PHP, JavaScript...) ofrecen una manera sencilla de utilizar las APIs Web, y también una forma, más o menos compleja según el caso, de crear APIs para permitir que otros se comuniquen con ellas.

La Aplicación que usé para la API es https://openweathermap.org/api

Mi código de JavaScript va embebido en el propio código HTML porque la informacón que nos muestre la API la pinto directamente en el resultado del HTML.

```JavaScript

	document.write('');
        window.onload = function(){
        document.querySelector("#city").addEventListener("change", consulta);
        }
	
    	function consulta(){
		// Nuestra API key
        	const apiKey = "e9cc819d23fb5a103ef0b878e7dd70ea";
		//Url en el que indicaremos la ciudad que nostros queramos en el input de ciudad
        	let url ="http://api.openweathermap.org/data/2.5/weather?";
        	let ciudad = document.querySelector("#city").value;
        	let recurso = url + "q=" + ciudad + "&APPID=" + apiKey + "&units=metric";
	
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function(){
            if (this.readyState == 4 && this.status == 200){
                let tiempo = JSON.parse(xhttp.responseText);
		//Aqui es donde pinto toda la información recogida
                document.getElementById("salida").innerHTML = 
                document.getElementById("salida").innerHTML = 
                    "<div class='infoName'> <h2>"
                    + tiempo.name 
                    + "</h2></div>"
                    + "<div class='infoData'> <div class='infoCont'><h3>"+ tiempo.main.temp + "  Cº </h3>"
                    + "<img src='http://openweathermap.org/img/wn/"  + tiempo.weather[0].icon  + "@2x.png' ></div>" 
                    + "<div class='infoCont'> Viento: " + tiempo.wind.speed +"   km/h <br>"
                    + "Humedad: " + tiempo.main.humidity  +"   %<br> <br> "
                    +  "<div class='infoDetail'>  "+tiempo.weather[0].description + "</div></div> </div>";
            }
        }
        xhttp.open("GET", recurso, true);
        xhttp.send();
    }
    document.write('</div>');
		
		```


