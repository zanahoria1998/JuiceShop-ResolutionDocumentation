<img width="334" height="142" alt="image" src="https://github.com/user-attachments/assets/5ed79f00-7670-4376-8708-be02b1c489af" />

Objetivo: Insertar un reproductor de SoundCloud mediante el buscador de Juice Shop. Se utiliza el mismo punto de entrada y procesamiento de HTML identificado en el Reto 1 — DOM XSS; la diferencia es el payload y el contenido que se incorpora a la página.

    <iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>

Conceptos previos:

<iframe>: Incrusta el reproductor dentro de la página.

src: Apunta al reproductor de SoundCloud y especifica la pista.

width y height: Establecen sus dimensiones.

allow="autoplay" y auto_play=true: Permiten y solicitan reproducción automática, sujeta a las restricciones del navegador.

Seguiremos los siguientes pasos, tomando como referencia el procedimiento ejecutado en el reto anterior:

1. Abrir el buscador utilizado en el Reto 1.
2. Introducir el nuevo payload y ejecutar la búsqueda.
3. Observar el reproductor e inspeccionar span#searchValue para identificar el iframe creado.

<img width="1114" height="701" alt="image" src="https://github.com/user-attachments/assets/a609a8ad-dde3-413b-83b1-2992a875834e" />

<img width="684" height="242" alt="image" src="https://github.com/user-attachments/assets/c636d07e-e8a5-4fa7-b7e8-d03b13e65c92" />

Al igual que en el reto anterior la aplicación interpreta nuevamente el término buscado como HTML. En este caso, el iframe carga un reproductor externo en lugar de ejecutar una URL javascript: para mostrar una alerta. Esto demuestra que el mismo punto vulnerable permite incorporar contenido externo a la interfaz.

Corrección/mitigación de vulnerabilidad

Para la mitigación se pueden aplicar las mismas medidas que en el reto anterior, que es mostrar la entrada cómo texto y aplicar una política CSP.

<img width="1076" height="612" alt="image" src="https://github.com/user-attachments/assets/3a456289-75a1-4612-8a02-01f0e836e9af" />

De esta manera ya no se ejecuta el iframe.
