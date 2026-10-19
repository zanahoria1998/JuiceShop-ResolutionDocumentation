  <img width="334" height="144" alt="image" src="https://github.com/user-attachments/assets/91713d1d-c319-4f78-a89e-dcd34864c8d5" />

Objetivo: Demostrar el ataque DOM XSS utilizando el payload proporcionado:
                             
                              <iframe src="javascript:alert(`xss`)">

Conceptos previos:

DOM: Estructura de elementos que el navegador mantiene para representar la página. Esta estructura/documento puede ir variando conforme interactuamos con ella. 

DOM XSS: Es una vulnerabilidad que surge cuando un JavaScript contiene variables/valores que pueden ser manipuladas por el atacante conocido origen y lo pasa a una función conocida como destino.

Payload: Código diseñado para explotar una vulnerabilidad. 

Input: Campo donde se escribe la búsqueda.

Span: Contenedor que, en este caso, muestra el término buscado dentro del encabezado.

Lo que hace el JavaScript proporcionado es generar un marco a través de <iframe>, su atributo "src" contiene una URL con el esquema URl "javascript:" este le indica al navegador que el texto que viene a continuación debe ejecutarse como código de JavaScript en lugar de cargar una página web o un archivo y "alert(`xss`)" muestra una ventana emergente.

Exploración inicial: Se identificó al buscador de la página cómo un posible punto de entrada; al buscar una palabra como "Hola", se observa que la página también la muestra en el encabezado "Search Results - Hola".

Nota: Que la palabra aparezca reflejada en pantalla no demuestra en sí el hallazgo de una vulnerabilidad. 

Troubleshooting:

En el estado inicial de la página no muestra "All products"

<img width="478" height="200" alt="image" src="https://github.com/user-attachments/assets/76a754da-52b2-4683-9d08-72c696fa687c" />

Realizamos una búsqueda de prueba, introducimos la palabra a buscar, en este caso "Hola". Posteriormente inspeccionamos el código desde el apartado "Elements" y observamos la siguiente estructura:

<img width="478" height="215" alt="image" src="https://github.com/user-attachments/assets/64786c68-d6f0-463b-a91c-f06748a43fd5" />

El primer <span> muestra el texto fijo y el segundo muestra el texto variable que corresponde a la búsqueda que se realiza. 

Una vez realizada esta prueba ingresamos el payload proporcionado dentro del buscador y ejecutamos la búsqueda. Lo que observamos es que aparece una ventana emergente con el mensaje "XSS"

<img width="663" height="322" alt="image" src="https://github.com/user-attachments/assets/676c4a15-fc6c-48bc-900d-be706a4c7b09" />

Al cerrar la ventana inspeccionamos el DOM en el apartado de <span> dónde aparece el texto variable y podemos darnos cuenta que ahora en lugar de texto contiene un <iframe>.

<img width="666" height="140" alt="image" src="https://github.com/user-attachments/assets/eca36d69-dd10-4a3b-b4d5-4c81cf1c2b0c" />

¿Por qué funciona? Antes de ejecutar la búsqueda el payload es únicamente texto, pero al momento de realizar la ejecución, la aplicación utiliza esa entrada para actualizar el encabezado, en este caso, el contenido se interpreta como HTML, por ello el navegador crea un <iframe> real dentro del <span> y al procesar el atributo src del iframe, se ejecuta el JavaScript y aparece la ventana emergente.

<img width="496" height="103" alt="image" src="https://github.com/user-attachments/assets/58cf9704-2144-4235-b7ad-bbbd9b569634" />

La causa es el uso de bypassSecurityTrustHtml sobre el término de búsqueda, que posteriormente se inserta como HTML en el DOM sin la sanitización habitual.

Corrección/Mitigación de vulnerabilidad

Mostrar la entrada cómo texto: para el buscador, retirar bypassSecurityTrustHtml y mostrar el término mediante interpolación de Angular ({{ searchValue }}) o textContent. Así el navegador no interpreta la entrada como HTML. Si la funcionalidad necesita aceptar HTML, utilizar un sanitizador que permita únicamente etiquetas y atributos seguros.

// searchValue debe conservar una cadena de texto.

                  this.searchValue = queryParam; (Dentro del HTML)

                  <span id="searchValue">{{ searchValue }}</span> (Dentro del DOM)

<img width="991" height="513" alt="image" src="https://github.com/user-attachments/assets/49186892-1be1-4309-9aad-c83963559b21" />

Otra opción es establecer una política de seguridad de contenido (CSP): configurar una política restrictiva que limite la ejecución de scripts y las fuentes permitidas para marcos mediante directivas como script-src y frame-src. Actúa como defensa adicional; no sustituye la corrección del procesamiento inseguro.
