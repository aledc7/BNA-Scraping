# Banco Nacion Argentina - Web Scraping
- [x] aledc.com
- [x] MIT License
- [x] Tested Code

###### El siguiente código captura los datos de cualquier página mediante web scraping. En este ejemplo se logra capturar la cotización del Dolar Oficial publicada en el sitio web del Banco Nacion Argentina. 
##### Luego de extraidos los datos, se puede guardar en variables separadas la cotización de su interés, para así poder utilizarla en cualquier ambiente.


###### Aquí el código, 100% funcional, con sus comentarios sobre cada linea.


```javascript
<html>
 <head>
  <title>Web Scraping BNA - AleDC</title>
 </head>
 <body>
<?php

function genera_dolar(){


// Esta funcion captura toda la página mediante curl y retorna una variable con todo el contenido
function captura_dolar($url) {
    // inicializo curl y le paso como parametro una variable que llevará la url que quiero capturar
    $aledc = curl_init($url); 
    curl_setopt($aledc, CURLOPT_RETURNTRANSFER, TRUE);
    //curl_setopt($aledc, CURLOPT_SSL_VERIFYPEER, FALSE);
    //guardo el resultado de la consulta en la varialble respuesta
    $respuesta = curl_exec($aledc); 
    curl_close($aledc);
    return $respuesta;

} // fin captura_dolar







// asigno a una variable la url que quiero capturar, en este caso será la tabla de dolares del BNA
$url = 'http://www.bna.com.ar/Cotizador/MonedasHistorico';

// capturo el contenido completo de lo que sea que haya en la $url, en este caso, estoy capturando la tabla completa que sale en la url del BNA.
$tabla_dolar = captura_dolar($url);

// para comprobar que lo que se ha capturado, descomentar la linea de abajo, debería dibujarse la tabla completa del BNA.
//echo $tabla_dolar;

// inicializo el objeto DOMDocument
$dom = new DOMDocument;
// capturo todos los objetos que haya en la variable $tabla_dolar  que recordemos que es la tabla completa.
$dom->loadHTML($tabla_dolar);
// capturo cada elemento que tenga la etiqueta td, y lo guardo en un array.
foreach($dom->getElementsByTagName('td') as $node)
{
    $array[] = $dom->saveHTML($node);
}
// para comprobar que se haya capturado el array completo, descomentar la linea de abajo.
//    print_r($array);

// $dolar_final = $array[2];
// $dolar_compra = $array[2];
return $array;

}// fin funcion genera_dolar


// Ahora en la variable $array_dolar tendré todos los valores de la tabla capturada.
// Para obtener valor por valor simplemente tengo que indicar el indice del array correspondiente.
// Abajo está la Tabla 1.0 la cual indica el indice del array capturado.
$array_dolar = genera_dolar($url);

echo 'Dolar Banco Nacion Compra: ' . $array_dolar['1'] . '<br>';
echo 'Dolar Banco Nacion Venta: ' . $array_dolar['2'];


/*  Tabla 1.0 - Indice Array
La siguiente lista detalla el array capturado, para obtener el valor deseado, simplemente colocar el indice correcto del array.

    [0] => Dolar U.S.A_____________________________ 
    [1] =>    Compra
    [2] =>    Venta
    [3] => Libra Esterlina_________________________ 
    [4] =>    Compra
    [5] =>    Venta
    [6] => Euro ___________________________________ 
    [7] =>    Compra
    [8] =>    Venta
    [9] => Franco Suizos (*)_______________________ 
    [10] =>    Compra
    [11] =>    Venta
    [12] => YENES (*)______________________________ 
    [13] =>    Compra
    [14] =>    Venta
    [15] =>  Dolares Canadienses (*)_______________
    [16] =>    Compra
    [17] =>    Venta
    [18] =>  Coronas Danesas (*)___________________
    [19] =>    Compra
    [20] =>    Venta
    [21] =>  Coronas Noruegas (*)__________________
    [22] =>    Compra
    [23] =>    Venta
    [24] =>  Coronas Suecas (*)____________________ 
    [25] =>    Compra
    [26] =>    Venta
    [FIN]__________________________________________

*/

echo "<p>Desarrollado por <b>Ale DC</b> &copy; " . date("Y") . "</p>";
?>
<a href="https://aledc.com" target="_blank">https://aledc.com</a>


 </body>
</html>
```


###### Eso es todo, saludos cordiales



