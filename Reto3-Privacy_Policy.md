<img width="334" height="144" alt="image" src="https://github.com/user-attachments/assets/406390b6-79d2-458c-bdf8-8cfc428fee9e" />

Objetivo: Localizar y consultar la política de privacidad de OWASP Juice Shop.

Conceptos previos:

Sources: Pestaña de las herramientas de desarrollo que permite consultar los archivos cargados por la página.

JavaScript: Lenguaje utilizado para implementar el comportamiento de la aplicación. En este caso, también contiene su configuración de navegación.

Path: Define el segmento de una ruta de navegación de Angular.

Children: Contiene las rutas hijas de una ruta principal.

Component: Indica el componente que Angular muestra al acceder a una ruta.

Exploración inicial: Se revisaron los archivos de la aplicación desde la pestaña Sources del navegador. Dentro del archivo JavaScript main.js, se buscaron coincidencias de la propiedad path para identificar las secciones disponibles y localizar la política de privacidad.

<img width="338" height="111" alt="image" src="https://github.com/user-attachments/assets/59e285d0-35be-4ced-8ede-8b62a43673d3" />

La sección "Privacy-Security" contiene una ruta hija llamada "Privacy-Policy", y esa fue la ruta ingresada dentro del navegador. 

<img width="1430" height="850" alt="image" src="https://github.com/user-attachments/assets/2764c24b-2bec-405e-b250-59956616399f" />

¿Por qué funciona?

Dentro de Angular se tiene una configuración de rutas para determinar qué componente debe mostrar según la dirección visitada. 

Esto corresponde a navegación dentro de la aplicación, no a una redirección ni a la modificación de su código.

La revisión de los archivos JavaScript desde Sources permite comprender cómo se organiza la navegación de una aplicación. Las propiedades path y children ayudan a identificar rutas principales y secundarias.
