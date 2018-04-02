Seminario Gráfica Computacional I 2018, Primer Semestre → Clase 3 → Viernes 6 de abril

# Seminario Gráfica Computacional I (v.2018)

### Visualización de datos

En la [clase recién pasada](https://github.com/profesorfaco/dgp502_2), cerramos la primera iteración. En esta clase corresponde abrir la segunda iteración, donde revisaremos: 

- [HTML5](https://developer.mozilla.org/es/docs/HTML/HTML5), [CSS3](https://developer.mozilla.org/es/docs/Web/CSS/CSS3) y [JavaScript](https://developer.mozilla.org/es/docs/Learn/Getting_started_with_the_web/JavaScript_basics) (con [Bootstrap](https://getbootstrap.com/))
- [JSON](https://www.json.org/json-es.html) y [GeoJSON](http://geojson.org/)
- [SVG](https://developer.mozilla.org/es/docs/Web/SVG) y [CANVAS](https://developer.mozilla.org/es/docs/Web/Guide/HTML/Canvas_tutorial)
- [D3.js](https://d3js.org/)

[D3.js (Data-Driven Documents)](https://d3js.org/) es una biblioteca de JavaScript, desarrollada por [Mike Bostock](https://bost.ocks.org/mike/), que nos permite crear visualizaciones de datos en el navegador web, **utilizando SVG, HTML y CSS**.

HTML y CSS ya son lenguajes conocidos. Lo nuevo es el SVG (Scalable Vector Graphics); [SVG](https://developer.mozilla.org/es/docs/Web/SVG) es un dialecto para la generación de gráficos, que provee elementos para definir posiciones, figuras básicas, paths, textos, transformaciones básicas, etc.

A continuación, un ejemplo de `<svg></svg>` que tendría que ir dentro de un `<body></body>` dentro de un `<html></html>`:

```
<svg width="200" height="200" style="background:#ddd;">
	<g transform="translate(0,0)">
		<circle cx="60" cy="60" r="43" fill="#f77"/>
		<text x="48" y="65" fill="white">¡Ay!</text>	
		<rect x="90" y="90" width="100" height="100" fill="#037"/>
		<text x="113" y="145" fill="white">Disculpe</text>
	</g>
</svg>
```

Como aprender SVG implica aprender un nuevo dialecto, [vamos a explorarlo un poco y de a poco](https://www.w3schools.com/graphics/svg_intro.asp) (nada más que lo justo y necesario).

Ahora volvamos a [D3.js](https://d3js.org/). Como otras bibliotecas de Javascript, necesita ver vinculada a nuestro documento HTML. En este caso, podemos vincularla agregando: 

```
<script src="https://d3js.org/d3.v5.min.js"></script>
```

Una vez haya sido vinculada, estamos listos para simplificar el trabajo con datos en JavaScript. 

Recordarán que si queríamos manipular, vía DOM, un elemento como el párrafo, teníamos que indicar algo como: 

```
document.getElementsByTagName("p")[0].style.setProperty("color", "red");
```

Esto afectaría únicamente al párrafo en primera posición (0). Y si queríamos afectar a todos los párrafos por igual, lo que corresponde hacer es algo como lo que sigue: 

```
var parrafos = document.getElementsByTagName("p");
for (var i = 0; i < parrafos.length; i++) {
	parrafos[i].style.setProperty("color", "red");
}
```

Pero, si ya estamos vinculando la biblioteca [D3.js](https://d3js.org/), podemos simplificar lo anterior tanto como lo que sigue:

```
d3.selectAll("p").style("color", "red");
```

Veamos otro ejemplo. Si queremos agregar ítems a una lista con identidad determinada, podríamos crear una función:

```
<ul id="astronautas"></ul>
<script>
var data = ["Anton Shkaplerov","Scott Tingle","Norishige Kanai","Oleg Artemyev","Andrew Feustel","Richard Arnold"]
var veces = data.length;
function repite(n) {
	var que = [];
	var donde = document.getElementById('astronautas');
	for (var x = 0; x < n; x++) {
		que[x] = document.createElement('li');
		que[x].textContent = data[x];
		donde.appendChild(que[x]);
	}
};
repite(veces);
</script>
```

Usando D3.js, el mismo resultado se obtendría mediante lo que sigue:

```
<ul id="astronautas"></ul>
<script src="https://d3js.org/d3.v5.min.js"></script>
<script>
var data = ["Anton Shkaplerov","Scott Tingle","Norishige Kanai","Oleg Artemyev","Andrew Feustel","Richard Arnold"]
d3.select("#astronautas")
.selectAll("li")
.data(data)
.enter()
.append("li")
.text(function(d) { return d + " "; });
</script>
```

- - - - 

[Avanzar a la siguiente clase](https://github.com/profesorfaco/dgp502_4/)
