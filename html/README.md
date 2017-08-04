# Preguntas para entrevistas de frontend
## HTML
### Preguntas
1. [x] [¿Qué hace un `doctype`  (`<!DOCTYPE html>`)?](#1)
1. [x] [¿Qué nuevos elementos componen HTML5?](#2)
1. [x] [¿Para que sirven los atributos `data-`?](#4)
1. [x] [¿Cuál es la diferencia entre `cookie` `localStorage`, `sessionStorage` e `indexedDB`?](#5)
1. [x] [¿Qué diferencias existen entre `<script>`, `<script async>` y `<script defer>`?](#6)
1. [x] [¿Puedo poner un tag `<link>` dentro del body? ¿Por qué no es recomendado?](#7)
1. [x] [¿Dónde es recomendado poner los tag `<script/>` después o antes del body? ¿Existen excepciones?](#8)
1. [x] [¿Qué es el Rendering Progresivo?](#9)
1. [x] [¿Qué son y cómo afectan al performance el `Reflow` y `Repaint`?](#10)
1. [x] [¿Qué estructura tiene el `DOM`?](#11)
1. [x] [¿Qué diferencia existe entre `DOM` y `HTML`?](#12)
1. [x] [¿Por qué usar tags como `<Section>` o `<Article>` pudiendo usar `<div />`?](#13)
1. [x] [Si tengo 3 tags estilados exactamente iguales (`<button />`, `<a />` y `<div />`) ¿Qué debería elegir para interactuar con un usuario y por qué?](#14)
1. [x] [¿Qué es un meta tag?](#17)
1. [x] [¿Qué es y cuáles son las ventajas del Shadow DOM?](#18)


### Respuestas
- #### [¿Qué hace un `doctype` (`<!DOCTYPE html>`)?](#1)
  <div id="1" />
  Es una declaración al comienzo de un documento HTML (previo al tag `<html>`). Consiste en una instrución que le deja saber al navegador en qué versión de HTML está el documento para interpretarlo correctamente.
  Definir `<!DOCTYPE html>` le dice al navegador que tiene que parsear el HTML basándose en el estandar HTML5.
  En el caso de navegadores más viejos, interpretarán el HTML en un modo "compatible con HTML5" pero ignorarán las funcionalidades que no soporten.
  `<!DOCTYPE html>` es mucho más simple que las definiciones de doctype anteriores, como por ejemplo:
  `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
  "http://www.w3.org/TR/html4/strict.dtd">
  `



- #### [¿Qué nuevos elementos componen "HTML5"?](#2)
  <div id="2" />
  - Semántica - Un marcado de texto (Text Markup) más semántico. Lo que agrega mejor accesibilidad, más herramientas para la descripción de el contenido web y mayor facilidad para el SEO.
    - `<footer>`
    - `<canvas>`
    - `<article>`
    - `<main>`
    - `<nav>`
    - `<aside>`
    - `<dialog>`
    - `<section>`
    - Etc...
    - Nuevos elementos de form:
      - `<datalist>`
      - `<keygen>`
      - `<output>`
  - Conectividad (Diferentes métodos de comunicación)
    - WebSockets
    - WebRTC
    - Eventos del Servidor (server-sent events)
  - Offline Web
    - Caché de aplicación
    - Web Workers
    - IndexedDB
    - Uso de archivos offline (File API / FileReader)
    - Detección de la conectividad (navigator.onLine)
  - Multimedia e interacción
    - `<Audio>` y `<Video>`
  - Trabajos gráficos
    - WebGL
    - Canvas
    - SVG
  - JavaScript/Integraciónes
    - Web Workers
    - History API
    - DragAndDrop
    - RequestAnimationFrame
    - FullScreenAPI
    - PointerLock
  - Acceso al dispositivo
    - Cámara
    - Eventos touch
    - Orientación del dispositivo
    - Geolocalización
    - Web Bluetooth
    - WebVR
  - CSS3



- #### [¿Para qué sirven los atributos `data-`?](#4)
  <div id="4" />
  Es un atributo de HTML, un estándar que permite adjuntar o guardar información extra en un elemento.

  ```html
  <div
    id="unDivCualquiera"
    data-usuario="fforres"
    data-usuario-correo="felipe.torressepulveda@gmail.com" >
  ```

  El acceso está estándarizado, puedes acceder a la data de la siguiente manera:

  ```javascript
    const article = document.getElementById('unDivCualquiera');
    article.dataset.usuario // "fforres"
    article.dataset.usuarioCorreo // "felipe.torressepulveda@gmail.com"
  ```

- #### [¿Cuál es la diferencia entre una `cookie`, `localStorage` y una `sessionStorage`?](#5)
  <div id="5" />
  - **Cookie:**
    Pequeño set de información enviada por un sitio web y almacenado en el navegador de un usuario.
    Se guarda en el disco, por lo que esta data es persistente.
    Es posible guardar y recuperar la data usando JS de la siguiente manera:

    ```javascript
    document.cookie = "username=fforres";
    /*O darle una fecha de expiración*/
    document.cookie = "username=fforres; expires=Thu, 19 Feb 2019 11:59:59 UTC";
    const cookie = document.cookie;
    ```

    Cada llamada a `document.cookie = "(...)"` crea una nueva cookie.
    Las cookies se guardan en texto plano.
    Pueden guardar poca data (4KB).
    Son enviadas en cada request.


  - **sessionStorage:**
    La propiedad `sessionStorage` permite acceder al objeto local `Storage` pero solo durante la sesión del usuario.

    Una sesión dura hasta que el navegador es cerrado.

    La data sobrevive a recargas de página.

    Una nueva "tab" o "ventana" genera una nueva sesión.

    ```javascript
    sessionStorage.setItem('usuario', 'fforres');
    /* guarda en la llave "usuario" el valor "fforres" */

    const usr = sessionStorage.getItem('usuario');  // usr retorna "fforres"

    sessionStorage.removeItem('usuario') // remueve la data guardada en esa llave

    sessionStorage.clear() //remueve toda la data de la sesión.
    ```
    ~5MB de storage por dominio


  - **localStorage:**
    La propiedad `localStorage` permite acceder al objeto local `Storage`

    La data no tiene una fecha de expiración y es accesible desde múltiples ventanas o tabs del mismo dominio y navegador.
    ```javascript
    const miStorage = localStorage;
    /* myStorage es ahora un objecto Storage */

    miStorage.setItem('usuario', 'fforres');
    /* guarda en la llave "usuario" el valor "fforres" */

    miStorage.usuario  // retorna "fforres"
    ```

    ~5MB de storage por dominio.

    Las propiedades del `localStorage` solo pueden ser accedidas por páginas con el mismo dominio que la página que definió (set o *seteó*) las propiedades. Por ejemplo, si una página como ejemplo.com *setea* algo en el `localStorage` puede ser accedida por ejemplo.com/xxxxx, ejemplo.com/yyyyy, ejemplo.com/xxxxx/zzzzz y así.


    **Como nota muy importante:** los datos guardados en `localStorage` y en `sessionStorage` son **específicos al protocolo de la página**. No es lo mismo http://ejemplo.com que https://ejemplo.com, los datos a los que acceden/escriben son distintos.


- #### [¿Qué diferencias existen entre `<script>`, `<script async>` y `<script defer>`?](#6)
  <div id="6" />
  - **script** -> Descarga el archivo y lo ejecuta, pero tanto la descarga como la ejecución se desarrollan secuencialmente y por lo mismo detienen el parseo del HTML.

  - **script async** -> Descarga el archivo paralelamente a la descarga/parseo del resto del documento/assets, pero al momento de ejecutarlo detiene el parseo del HTML.

  - **script defer** -> Descarga el archivo paralelamente a la descarga/parseo del resto del documento/assets, pero espera hasta que todo el HTML esté parseado antes de ejecutar el script.



- #### [¿Puedo poner un tag `<link>` dentro del body? ¿Por qué no es recomendado?](#7)
  <div id="7" />
  - Sí. No es recomendado, aunque posible.
  - Ejemplo de un proceso de descarga de un archivo HTML, un archivo CSS, una imagen y un archivo JS:
    - Descarga el "HTML".
    - Se parsea el HTML y ve que hay un archivo CSS, un archivo JS y una imagen.
    - Se inicia la descarga de la imagen.
    - El navegador decide que no puede mostrar la página sin antes descargar el CSS y JS.
      - Esta decisión se toma porque ambos archivos podrían alterar la visualización del DOM causando Reflow o Repaint si el CSS tuviese un `display: none` o el JS un `Node.remove()`, por ejemplo.
    - Descarga por orden de aparicion (CSS o JS).
    - Al descargar el CSS, lo lee, parsea, y se asegura que no llame nada más (un `@import` o `background:url('./imagen.jpg')`).
    - Al descargar el JS, lo lee, interpreta y ejecuta.
    - El navegador decide que ahora sí puede mostrar el DOM, por lo que empieza a pintar y estilar el DOM.

  En este ejemplo, en el caso de tener un segundo `<link />` dentro del body, el proceso se ejecuta normalmente hasta que se parsea el DOM, dentro del body se encuentra con el `<link />`, se detiene el parseo y pintado del DOM para descargar y parsear el CSS.

  Luego de eso vuelve a resumir el trabajo con el DOM y aplicar estilos de ser necesario.

  + Mas info sobre el Critical Rendering Path [acá](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/) y [acá](https://varvy.com/pagespeed/critical-render-path.html)




- #### [¿Dónde es recomendado poner los tag `<script/>` después o antes del body? ¿Existen excepciones?](#8)
  <div id="8" />
  - Depende mucho del contenido y acciones que ejecutarán dichos scripts. En antaño los `<script/>` se colocaban posterior al body para priorizar el mostrar la estructura del contenido (HTML), estilarlo (CSS) y después agregar la interactividad con los scripts. Pero actualmente existen los atributos `async` o `defer` que nos ayudan a definir descargas, parseos y ejecución diferidos.

- #### [¿Qué es el Rendering Progresivo?](#9)
  <div id="9" />
  - Un conjunto de técnicas y decisiones tomadas y aplicadas a fin de priorizar qué contenido o elemento se debería cargar primero (el contenido de una noticia, el landing en un sitio web) y despriorizar la carga de otras secciones (footer, banners, side-menus, etc).





- #### [¿Qué son y cómo afectan al performance el `Reflow` y `Paint`/`RePaint` ?](#10)
  <div id="10" />
  - `RePaint` es el nombre que se le da al proceso que ejecuta el navegador cuando realiza cambios visuales a un elemento, pero no cambia su `layout` (color de fondo, visibilidad, outline).

  - `Reflow` es el proceso que ejecuta el navegador cuando los cambios que realiza a un elemento, cambian su layout (posicion, tamaño, etc) que obligan a recalcular y posiblemente reposicionar otros elementos en el documento.

  Ambos procesos son críticos a la hora de analizar y optimizar la performance, donde `ReFlow` afecta de manera mucho mayor.

  - Al mover un elemento que cause `ReFlow`, es necesario recalcular **todos** los otros elementos del DOM que podrían verse afectados por este cambio.

  - `RePaint` necesita verificar la visibilidad de todos los otros nodos y como estos afectan a la visibilidad de el/los nodos iniciales.
    - Ejemplo:

      El cambiar el color de fondo de un `<div id="a" />` sobre el que hay un `<div id="b">` con una opacidad `0.5`, fuerza a recalcular el color de fondo y los efectos que tiene el `<div id="b">` sobre el A




- #### [¿Qué estructura tiene el `DOM`?](#11)
  <div id="11" />
  - Un árbol.
  - Un árbol imperfecto y desbalanceado.

  *Puede ser interesante tomarse de este tema para iniciar una conversacion sobre CS (Computer Science), estructuras de datos. El porqué usualmente los frontend engineers y frontend developers no buscan conocimientos de CS (Computer Science))*




- #### [¿Qué diferencia existe entre `DOM` y `HTML`?](#12)
  <div id="12" />
  - HTML - (Hyper Text Markup Language) Es un lenguaje de marcado (*markup*) que define una sintaxis específica para representar un cierto tipo de componentes que luego el navegador interpreta y transforma en el DOM.
  - DOM - (Document Object Model) - Es el modelo de la interpretación de un HTML. El DOM es (y expone) una API para un documento de HTML válido que permite interactuar y realizar acciones programáticas sobre él.
    Ejemplo:
      ```javascript
        if (a) {
          const texto = document.createTextNode(" Hola :-) ");
          document.body.appendChild(texto);
        }
      ```

  + Más información [acá (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) y [acá (w3.org)](https://www.w3.org/TR/DOM-Level-2-Core/introduction.html)





- #### [¿Por qué usar tags como `<Section>` o `<Article>` pudiendo usar `<div />`?](#13)
  <div id="13" />
  - En primera instancia, por accesibilidad. Utilizar elementos como `<article>`, `<details>`, `<footer>` o `<nav>` ayuda a los screenreaders a mapear e interpretar correctamente el DOM.
  - Tocando el tema de la accesibilidad, de nada sirve usar atributos como `role` o `aria-*` de manera conflictiva.
  ```html
    <!-- MAL! :( -->
    <button role="header"/>

    <!-- Mucho Mejor :) -->
    <header role="header"/>
  ```

  + Para conocer más de [Aria y document conformance, acá](https://www.w3.org/TR/html-aria/#docconformance)





- #### [Si tengo 3 tags estilados exactamente iguales (`<button />`, `<a />` y `<div />`) ¿Qué debería elegir para interactuar con un usuario y por qué?](#14)
  <div id="14" />
  - Una pregunta un poco capciosa, principalmente porque la decisión pasa por accesibilidad más que por otra cosa.

    La idea primaria es usar elementos concretos para las interacciones que se realizarán.
    Por ejemplo, si se busca hacer un submit a un formulario, es mejor usar un `<button />` que un `<span />` estilado.
    En el ejemplo anterior, aunque ambos realicen la acción mediante una función de JavaScript, screenreaders pueden considerar de manera distinta ambos elementos.

    Como caveat, es posible usar atributos como `role=""` o `aria-*` para especificar el rol de un elemento, pero no es bueno usarlos de manera conflictiva.


  + Para conocer más de [Aria y document conformance, acá](https://www.w3.org/TR/html-aria/#docconformance)





- #### [¿Qué es un meta tag?](#17)
  <div id="17" />
  - Son Elementos o Tags usados en HTML que proveen metadata del sitio o "Información sobre la información" (o del contenido) del mismo sitio.

  Ejemplo:

    Consideremos este meta tag:
    ```html
    <meta charset=“utf-8”>
    ```
    El tag no contiene información concreta del sitio como lo sería una noticia, un título, una imagen o un link, pero entrega información sobre el formato de encoding del sitio.

    ***Información sobre el contenido (o la información) del sitio.***




- #### [¿Qué es y cuáles son las ventajas del Shadow DOM?](#18)
  <div id="18" />
  El Shadow DOM es una funcionalidad que permite inyectar un sub-árbol de elementos DOM (un SUB-DOM) en el documento actualmente renderizado en el navegador.

  *(El Shadow DOM asocia un nuevo tipo de nodo asociado que se puede asociar con los elementos llamado el "Shadow Root", el elemento al que se le asocia este "Shadow Root" se le dice "Shadow Host")*

  La idea del Shadow DOM es crear elementos web con estilo y funcionalidades auto-contenidos (o encapsulados), por lo que reglas de estilo como `#contenedor { background: red; }` definidas dentro del Shadow DOM, no afectará elementos que cumplan con esa condición que estén fuera de él.

  Ejemplo:

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8">
      <script defer src="./index.js" charset="utf-8"></script>
      <style media="screen">
        #shadow {
          color: green;
        }
      </style>
    </head>
    <body>
      <h1 id="shadow">Hello Shadow DOM</h1>
    </body>
  </html>
  ```
  ```javascript
  const header = document.createElement('header');
  const shadowRoot = header.attachShadow({mode: 'open'});
  shadowRoot.innerHTML = `
    <style>
    #shadow {
      color: red;
    }
    </style>
    <h1 id="shadow">Hello Shadow DOM</h1>`; // Could also use appendChild().
  document.body.appendChild(header);
  ```

  Teniendo estos 2 elementos `<h1 id="shadow">Hello Shadow DOM</h1>`, uno siendo creado y estilado mediante el uso de Shadow DOM y el otro siendo creado por la interpretación del DOM, el navegador muestra lo siguiente:

  ![](./shadow_dom.png)
