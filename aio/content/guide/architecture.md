# Introducción a los conceptos de Angular

Angular es una plataforma y un framework para crear aplicaciones single-page en el lado del cliente usando HTML y TypeScript.
Angular está escrito en TypeScript.
Implementa la funcionalidad básica y opcional como un conjunto de bibliotecas TypeScript que importas en tus aplicaciones.

La arquitectura de una aplicación en Angular se basa en ciertos conceptos fundamentales.
Los building blocks básicos son *NgModules*, which provide a compilation context for *components*. NgModules collect related code into functional sets; una aplicación de Angular se define por un conjunto de NgModules. Una aplicación siempre tiene al menos un *módulo raíz* que permite el arranque y generalmente tiene muchos más *módulos de funcionalidad*.

* Los componentes definen *vistas*, que son conjuntos de screen elements que Angular puede elegir y modificar de acuerdo con la lógica y los datos de tu programa.

* Los componentes usan *servicios*, los cuales proporcionan una funcionalidad específica que no está directamente relacionada con las vistas. Los proveedores de servicios pueden *inyectarse* en componentes como *dependencias*, haciendo que tu código sea modular, reutilizable y eficiente.

Módulos, componentes y servicios son clases que usan *decoradores*. Estos decoradores indican su tipo y proporcionan metadatos que le indican a Angular cómo usarlos.

* Los metadatos para una clase de componente son asociados con una *plantilla* que define una vista. Una plantilla combina HTML ordinario con *directivas* de Angular y *binding markup* que permiten a Angular modificar el HTML antes de mostrarlo para su visualización.

* Los metadatos para una clase de servicio proporcionan la información que Angular necesita para que esté disponible para los componentes a través de la *Inyección de Dependencia (ID)*.

Los componentes de una aplicación suelen definir muchas vistas, ordenadas jerárquicamente. Angular proporciona el servicio `Router` para ayudarlo a definir rutas de navegación entre vistas. El enrutador proporciona capacidades de navegación sofisticadas en el navegador.

<div class="alert is-helpful">

  Visita el [Glosario de Angular](guide/glossary) para ver las definiciones básicas de términos importantes en Angular y su uso.

</div>

<div class="alert is-helpful">

  Para ver la aplicación de ejemplo que describe esta página, consulta el <live-example></live-example>.
</div>

## Módulos

Angular *NgModules* differ from and complement JavaScript (ES2015) modules. An NgModule declares a compilation context for a set of components that is dedicated to an application domain, a workflow, or a closely related set of capabilities. An NgModule can associate its components with related code, such as servicios, to form functional units.

Cada aplicación en Angular tiene un *módulo raíz*, convencionalmente nombrado `AppModule`, que proporciona el mecanismo de arranque que inicia la aplicación. Una aplicación generalmente contiene muchos módulos funcionales.

Como en los módulos de JavaScript, los NgModules puede importar funcionalidad de otros NgModules, y permiten que su propia funcionalidad sea exportada y utilizada por otros NgModules. Por ejemplo, para utilizar el servicio de enrutador en su aplicación, importa el NgModule `Router`.

Organizar su código en distintos módulos funcionales ayuda a gestionar el desarrollo de aplicaciones complejas, y en el diseño para su reutilización. In addition, this technique lets you take advantage of *lazy-loading*&mdash;that is, loading modules on demand&mdash;to minimize the amount of code that needs to be loaded at startup.

<div class="alert is-helpful">

  Para más detalles, visita [Introducción a los módulos](guide/architecture-modules).

</div>

## Componentes

Every Angular application has at least one component, the *root component* that connects a component hierarchy with the page document object model (DOM). Each component defines a class that contains application data and logic, and is associated with an HTML *template* that defines a view to be displayed in a target environment.

The `@Component()` decorator identifies the class immediately below it as a component, and provides the template and related component-specific metadata.

<div class="alert is-helpful">

   Decorators are functions that modify JavaScript classes. Angular defines a number of decorators that attach specific kinds of metadata to classes, so that the system knows what those classes mean and how they should work.

   <a href="https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841#.x5c2ndtx0">Learn more about decorators on the web.</a>

</div>

### Plantillas, directivas, y data binding

Una plantilla combina HTML con Angular markup que puede modificar elementos HTML antes de que se muestren.
Template *directives* proporcionan la lógica de programa y el *binding markup* conecta los datos de su aplicación y el DOM.
Hay dos tipos de enlace de datos:

* *Event binding* lets your app respond to user input in the target environment by actualizando los datos de su aplicación.
* *Property binding* te permite interpolar valores que se calculan a partir de los datos de tu aplicación en HTML.

Antes de mostrar una vista, Angular evalúa las directivas y resuelve la sintaxis de enlace en la plantilla para modificar los elementos HTML y el DOM, de acuerdo con los datos y la lógica de su programa. Angular soporta *two-way data binding*, lo que significa que los cambios en el DOM, como las elecciones del usuario, también se reflejan en los datos de su programa.

Tus plantillas pueden usar *pipes* para mejorar la experiencia del usuario mediante la transformación de valores para mostrar.
Por ejemplo, usa pipes para mostrar fechas y valores de moneda que sean apropiados para la configuración regional de un usuario.
Angular proporciona pipes predefinidas para transformaciones comunes, y también puede definir sus propias pipes.

<div class="alert is-helpful">

  Para más detalles sobre estos conseptos, visita [Introducción a los componentes](guide/architecture-components).

</div>

{@a dependency-injection}


## Servicios e inyección de dependencias

Para los datos o la lógica que no están asociados con una vista específica y que desea compartir entre componentes, cree una clase *servicio*. A service class definition is immediately preceded by the `@Injectable()` decorator. The decorator provides the metadata that allows other providers to be **injected** as dependencies into your class.

 *Inyección de Dependecia* (ID) le permite mantener sus clases de componentes lean y eficientes. No obtienen datos del servidor, validan la entrada del usuario o inician sesión directamente en la consola; delegan tales tareas a los servicios.

<div class="alert is-helpful">

  Para más detalles, visita [Introducción a los servicios e ID](guide/architecture-services).

</div>

### Enrutamiento

El `Router` de Angular NgModule proporciona un servicio que le permite definir una ruta de navegación entre los diferentes estados de la aplicación y ver las jerarquías en su aplicación. It is modeled on the familiar browser navigation conventions:

* Ingresa una URL en la barra de direcciones para que el navegador vaya a la página correspondiente.

* Haz clic en los enlaces de la página para que el navegador vaya a una nueva página.

* Haz clic en los botones atrás y adelante del navegador para que el navegador vaya hacia atrás y hacia adelante a través del historial de páginas que has visto.

El enrutador asigna rutas similares a URL a vistas en lugar de páginas. Cuando un usuario realiza una acción, como hacer clic en un enlace, que cargaría una nueva página en el navegador, el enrutador intercepta el comportamiento del navegador y muestra u oculta las jerarquías de vista.

Si el enrutador determina que el estado actual de la aplicación requiere una funcionalidad particular, y el módulo que lo define no se ha cargado, el enrutador puede *lazy-load* el módulo bajo demanda.

El enrutador interpreta una URL de enlace de acuerdo con las reglas de navegación de visualización de la aplicación y el estado de los datos. Puedes navegar a las nuevas vistas cuando el usuario hace clic en un botón o selecciona desde un cuadro desplegable, o en respuesta a algún otro estímulo de cualquier fuente. El enrutador registra la actividad en el historial del navegador, por lo que los botones de retroceso y avance también funcionan.

Para definir reglas de navegación, asocie *rutas de navegación* con tus componentes. Una ruta utiliza una sintaxis similar a una URL que integra los datos de tu programa, de la misma manera que la sintaxis de la plantilla integra sus vistas con los datos de tu programa. Luego puedes aplicar la lógica del programa para elegir qué vistas mostrar u ocultar, en respuesta a la entrada del usuario y tus propias reglas de acceso.

 <div class="alert is-helpful">

   Para más detalles, visita [Enrutamiento y navegación](guide/router).

 </div>

<hr/>

## ¿Qué sigue?

Has aprendido los conceptos básicos sobre los building blocks de una aplicación en Angular. El siguiente diagrama muestra cómo se relacionan estas piezas básicas.

<div class="lightbox">
  <img src="generated/images/guide/architecture/overview2.png" alt="overview">
</div>

* Juntos, un componente y una plantilla definen una vista en Angular.
  * Un decorador en una clase de componente agrega los metadatos, incluido un puntero a la plantilla asociada.
  * Las directivas y el binding markup en la plantilla de un componente modifican las vistas basadas en los datos y la lógica del programa.
* El dependency injector proporciona servicios a un componente, como el servicio de router que le permite definir la navegación entre vistas.

Cada uno de estos temas se presenta con más detalle en las siguientes páginas.

* [Introducción a los Módulos](guide/architecture-modules)

* [Introducción a los Componentes](guide/architecture-components)

  * [Plantillas y Vistas](guide/architecture-components#templates-and-views)

  * [Metadatos de Componentes](guide/architecture-components#component-metadata)

  * [Data binding](guide/architecture-components#data-binding)

  * [Directivas](guide/architecture-components#directives)

  * [Pipes](guide/architecture-components#pipes)

* [Introducción a los Servicios e Inyección de Dependencias.](guide/architecture-services)

Cuando estés familiarizado con estos building blocks fundamentales, puedes explorarlos con más detalle en la documentación. Para saber más acerca de las herramientas y técnicas disponibles para ayudarte a crear y desplegar aplicaciones de Angular, visita [Próximos pasos: herramientas y técnicas.](guide/architecture-next-steps).
</div>
