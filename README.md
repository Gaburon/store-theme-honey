# Estandarización de proyectos

En este repositorio reposa la documentación necesaria para la creacion de proyectos en IT Globers, bajo los estandares establecidos por la compañia, no cerrandonos a mejoras continuas y sugerencia por parte de nuestros desarrolladores.

## Historias de usuarios

Las historias de usuario son levantadas por parte de los PM, TL de IT Globers con lo PO (customer) del proyecto.

- Los requerimientos deben tener la mayor descripción tanto en funcionalidad como aspecto, es necesario especificar lo mayormente posible y no dejar ningun requerimiento a interpretacion **subjetiva**.
- Tiempo en las entregas, estos tiempos deben ser evaluados con el team técnico, PM y Líder técnico. Buscando la mayor acertividad en complejidad en el desarrollo del requerimiento planteado por el cliente
- Siempre debe existir componentes de guia o apoyo visual a lo que busca como resultado final al Cliente, (usuarios o dueño del producto).
- En caso de que se levanten nuevas Historias de usuario durante el desarrollo del proyecto, estas deben cumplir con las mismas especificaciónes anteriomente nombradas, y seguir la linea de la estandarización.
- Siempre aclarar al cliente que los tiempos de entrega podrian sufrir cambios si se agregan historias de Usuario adicionales.

### RFC (request for commits)

Documento donde se plasmara los componentes a usar dentro del proyecto, dando claridad de la ruta a seguir de cada componente o elemento.

- Nombre del proyecto
- Tecnologias/componentes a usar y por qué.
- Con una descripcion detallada del componente y la forma de implementarlo.

Ejemplo:
`Header`: se usara un `header-row` como contenedor general del header y ya cada sub-header sera con un `flex-layout.row` etc... Porque de esta manera sera mas practico al momento de darle styles etc...

## Tareas en Jira

Dentro de las tareas de Jira debe reposar la informacion de historias de usuario mas la documentación del RFC, para un facil abordaje por parte del desarrollador.

## Inicialización del proyecto

#### Solicitud de permisos a VTEX

El TL debe hacer la solicitud de los permisos de la siguiente aplicación:

```json
{vendor}.backend-services
Esta aplicación tendrá acceso a los builders
"graphql": "{version}.x",
 "node": "{version}.x"
```

[Link form de solicitud](<[https://docs.google.com/forms/d/e/1FAIpQLSfhuhFxvezMhPEoFlN9yFEkUifGQlGP4HmJQgx6GP32WZchBw/viewform](https://docs.google.com/forms/d/e/1FAIpQLSfhuhFxvezMhPEoFlN9yFEkUifGQlGP4HmJQgx6GP32WZchBw/viewform?authuser=3)>)
En esta Aplicación se alojaran los servicios backend.
Por otro lado, se deberá configurar un repositorio dedicado a los componentes custom desde el lado front-end con la aplicación

```json
{account}.frontend-applications
```

Tambien la creación del/los ambientes necesarios y asignar permisos a los desarrolladores que estaran en el proyecto.

#### Configuración de Repositorios y WorkSpace

Crear los repositorios necesarios para el proyecto y gestionar los WorkSpace necesarios para las pruebas y views, además los WS de cada desarrollador (a criterio del líder técnico si lo hace el, o cada desarrollador )

#### Configuraciones Iniciales al Store Theme

En el archivo de styles.json `styles/configs/style.json` se puede configurar colores, fuentes, tamaños, espacios, etc. De manera directa al theme. Lo cual es el primer lugar que debemos adaptar a los requerimientos del proyecto.

<img src="assets/img/img-readme/img1.png">


## Estandarización de CSS

### Estructura Inicial
 
Para que los nuevos estándares y el proyecto funcionen correctamente, es necesario crear un nuevo archivo en la raíz de la Carpeta Global CSS, como sigue:

- Crea un nuevo archivo llamado ```vtex.store.css``` en la carpeta CSS

![VTEX Store CSS](https://user-images.githubusercontent.com/46954736/169902398-c0a21be5-9b5b-4924-9bb4-d520eb5732df.png)

- Y a continuación, añade las variables deseadas dentro del archivo

```
:global(.vtex-store__template) {
  --promotions-color: #ffed00;
  --green-offers: #289e36;
  --discounts: #7ac537;
  --dynamic-texts: #843a8d;
  --card-descriptions: #c47373;
  --promotion-flags: #525252;
}
```

Aquí podemos poner variables que necesitemos como colores, tamaños, fuentes, etc. que no se permitan configurar en el `styles.json` , el cual es mayormente usado para variables de colores. De esta forma, las variables quedan disponibles en toda la app para su uso.

_Como ``vtex-store__template`` es una clase global, podemos usar variables CSS para casos específicos y mejores personalizaciones de nuestros estilos_

## Estructura del Código

Para la implementación del código, utilizaremos la [Metodología BEM](https://en.bem.info/methodology/)

<p align="center">
  <img align="center" style="margin: 0 auto; width: 450px" src="https://user-images.githubusercontent.com/46954736/169904084-5512beb2-8850-4aed-b214-7295599d63c0.png" />
</p>

## Bloques y Nombres de Clases

Como ya estamos utilizando la Metodología BEM dentro de los bloques VTEX IO, esta es la forma que utilizaremos para implementar la metodología pero en las clases CSS. e,i:

Si un bloque nativo se llama ``"header-row#desktop__container-header"`` simplemente debemos nombrar la clase CSS basada en el alias del bloque. 

_bloque principal:_

```json
"header-row#desktop__container-header": {
    "children": [
      "image#header__contact--logo",
      "rich-text#header__contact--title"
    ]
  }
```
_bloque principal con clase css (``` "blockClass": "desktop__container-header"```):_

```json
"header-row#desktop__container-header": {
    "children": [
      "image#header__contact--logo",
      "rich-text#header__contact--title"
    ],
    "props": {
      "blockClass": "desktop__container-header"
    }
  }
```

_Nota: En el caso de que sea necesario utilizar más clases dentro del mismo bloque, puedes utilizar un array en la propiedad ``blockClass``, pero recuerda nombrar la clase utilizando la Metodología BEM:_

```json
"header-row#desktop__container-header": {
    "children": [
      "image#header__contact--logo",
      "rich-text#header__contact--title"
    ],
    "props": {
      "blockClass": [
        "desktop__container-header", 
        "example__example", 
        "example__example--example"
      ]
    }
  }
```

## Formato del Código


Así como es importante tener un estándar sólido en la estructura del código, también es importante que se vea bien y esté correctamente formateado a través de todos los cambios que el equipo hace.

Por esta razón, es necesario instalar [Formate: CSS/LESS/SCSS formatter](https://marketplace.visualstudio.com/items?itemName=MikeBovenlander.formate), un plugin de VSCode para formatear tus archivos CSS / LESS y SCSS que puede alinear verticalmente las propiedades.

<p align="center">
  <img 
    align="center" 
    style="margin: 0 auto; width: 450px !important;" 
    src="https://user-images.githubusercontent.com/46954736/169911661-66d35cde-0625-4b0b-8feb-60815d864bc3.gif" 
   />
</p>

![image](https://user-images.githubusercontent.com/46954736/169913102-0374e5c0-1cd2-4e3a-9883-9d8fd525ec4c.png)

De esta manera, podemos ver fácilmente nuestro código y hacer cambios a medida que aparecen nuevas características.


## Estructura de carpetas

Tener un ordenamiento simetrico y constante nos ayuda a mantener proyectos limpios y escalables, sobre todo a que otras personas lo puedan entender en un tiempo menor.

Por lo cual tenemos que pensar en los proyectos VTEX IO como un organismo que no muta si no que se extiende como las clases en POO.
Para ello debemos pensar en la construcción del esquema de los folders con 4 puntos de partida

1- Desktop
2- Mobile o phone (Según requiera)
3- Tablet
4- Global

Por qué desde estos cuatro puntos de partida?
Porque son las vistas generales en que el cliente ve nuestro producto, Global seria para los file que no se modifican según su vista.

<img src="assets/img/img-readme/Screenshot_1.png">

#### Estructura interna de cada carpeta.

Para las folders nombradas (Desktop, Mobile, Tablet y Global), se organizan de manera interna en 2 sub-Folders:

Desktop
=> Components: Contendra todos los componentes que pueda requerir la vista.
=> screen: Contiene los componentes principales que conforman páginas o la página en si misma.

En los folders componentes cada file debe ir con el nombre de su elemento padre, como se ve en la imagen `header-menu.jsonc` es el componente hijo de `header` asi podemos relacionar un componente con el su children.

<img src="assets/img/img-readme/Screenshot_2.png">

### Folder Global

En este folder iran todos los elementos que son igual para las vistas (phone, tablet, desktop), con las mismas dos carpetas internas, `components`, `screen`.
En el caso que se desee usar un componente global, pero se necesite hacer una extensión de estilos CSS, se agregará una clase adicional en un array del nuevo componente, agregando los estilos CSS adicionales requeridos.

```json

/.json - info card se usa en el home
{
    "flex-layout.row#global__info-card": {
        "children": [...],
        "props": {
            "blockClass": "global__info-card"
        }
    }
}

//vtex.flex-layout.css
.global__info-card {
    background-color: blue;
    color: white;
    font-size: 18px;
    width: 100%;
}

//.json - info card se usa en la página de producto pero tiene un cambio a su color de fondo

{
    "flex-layout.row#global__info-card--pdp": {
        "children": [...],
        "props": {
            "blockClass": ["global__info-card", "global__info-card--pdp"]
        }
    }
}

//vtex.flex-layout.css
.global__info-card--pdp {
    background-color: orange;
}
```

Por qué? porque asi evitamos chocar con las media querys nativas del navegador.

## Folders de css

Se crearan folders por componentes de el proyectos, es decir si tenemos en el home un slider-layout, tendriamos una carpeta que diga home en su interior uno con el nombre del slider-layout.
Ejemplo:

<img src="assets/img/img-readme/img3.png">

## Carpetas files y fonts

- Para los carpetas `files` y `fonts` no se requiere crear la estructura de las carpetas por vista ya contiene files unicos del proyecto y que sirven a todas las vistas. Pero sin cerrarse a que pueda existir esa discriminación por vista.
- Para `imagenes` se van a subir a arquivos. El nombramiento de cada imagen se llevará de la misma manera que los de componentes padres a hijos, ejemplo:
  `header__logo-marca.png`
  `header__icon-cart.png` etc.

* Para los `svg` se manejaran dentro de la carpeta assets del proyecto.

#### Hay dos "Principios o estándares" Para iniciar un proyecto:

a- Mobile first  
b- Desktop first

En ITGlobers si es un project responsive iniciamos con Mobile first, por qué? porque +70% del trafico en internet se hace desde un dispositivo mobile.

Para esto debemos usar el responsive layout, quien nos permetira manejar elementos diferentes en cada vista, ya sea que cambien el componente por completo o en su orden.

## Nombre a los archivos y clases.css de los proyecto con la metodologia BEM

`Block-element-modifier`

Por qué hacerlo con BEM?
Bueno BEM es una metodología usada en las hojas de styles para manejar mucho mejor la especificidad, lo cual aprovecharemos en IT Globers para nombrar componentes de VTEX IO y evitar que se repitan nombres o se pisen, igualmente para los file además de su uso en el CSS.

#### Nombrando bloques

Bloques de VTEX IO como `header-row`, `flex-layout.row`, `flex-layout.row`, `store.coustom`, `store.home` etc. Son nombres nativos en VTEX IO y les podemos agregar alias poniendo después de nombre por defecto un #, `flex-layout.row#{alias}`

Y aquí es donde pondremos en uso la metodología BEM para el nombramiento del alias.
Primero nombramos la vista (desktop, mobile, tablet o global) seguido de `__` nombre del component.

Si el bloque es un children vamos a manejar su nombre:

primero nombramos la vista `flex-layout.row#desktop` seguido de ' ** ' nombre del elemento padre `flex-layout.row#desktop**header`y por ultimo el del componente hijo que estás creando`flex-layout.row#desktop\_\_header--contact`

```json
 "header-row#desktop__container-header": {
	 "children": [
		 "flex-layout.row#desktop__header--contact",
		 "flex-layout.row#global__header--menu"// para cuando el componente esta en las 3 vistas, mobile, dekstop, tablet usamos "global"
	 ]
 },
```

Que pasa tiene muchos componentes anidados, para el 3er nivel de anidamiento se toma ya el elemento padre como principal y no la vista, ejemplo:

`flex-layout.row#desktop__header--contact` y este elemento tiene un children, seria asi:

```json
 "flex-layout.row#desktop__header--contact": {
	 "children": [
		 "ritch-text#header__contact--title",
		 "Image#header__contact--logo"// para cuando el componente esta en las 3 vistas, mobile, dekstop, tablet usamos "global"
	 ]
 },
```

#### Nombrando clases

Con las clases en los bloques es más práctico porque simple mente es ponerle el mismo alias del bloque como class en el css.

```json
 "header-row#desktop__container-header": {
	 "children": [
		 "flex-layout.row#desktop__header--contact",
		 "flex-layout.row#global__header--menu"// para cuando el componente esta en las 3 vistas, mobile, dekstop, tablet usamos "global"
	 ],
	 "props": {
		 "blockClass": "desktop__container-header",
		 "fullWidth": "true"
	 }
 },
```

Tambien tener en cuenta que en algunos proyectos es necesario reutilizar componentes con unas pequeñas variaciones en los styles, lo cual podemos hacer uso del array de classes que se puede manejar en Vtex.

```json
 "header-row#desktop__container-header": {
	 "children": [
		 "flex-layout.row#desktop__header--contact",
		 "flex-layout.row#global__header--menu"// para cuando el componente esta en las 3 vistas, mobile, dekstop, tablet usamos "global"
	 ],
	 "props": {
		 "blockClass": [
			 "desktop__container-header",
			 "Variante__uno",
			 "variante__dos"
			],
		 "fullWidth": "true"
	 }
 },
```

#### Nombrando files

El nombramiento de los file `.jsonc` es de igual manera simple y práctico, si hablamos de un bloque principal como `'header', 'footer', 'home', 'product-page'` etc. El nombre del file solo llevará el mismo nombre con la extensión 'header.jsonc', `'footer.jsonc', 'home.jsonc', 'product-page.jsonc'`, Si el file es un componente hijo como:

`header.jsonc` tiene un componente hijo que es el `menu`entonces el file del menú se llamara `header-menu.jsonc`.

# Nota:

- Todo elemento en el .jsonc debe llevar el `title` con el fin de facilitar el manejo del back office.
- Para los componentes que manejan mucha informacion de manera plana, como lo TyC, debemos manejar los archivos markdown.

## Commits, Pull Request and Merge

#### Estandar en los commits <a href="https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716">DOCS</a>

```json
	<type>(<scope>): <subject> <-- description -->

example:
		   <feat>(<header>): <create header with drop-down menu > <-- add drop-down menu for categories wite redirect -->
```

#### Pull request => que muestres que brach es la que entra y a cual elemplo:

```json

example:

**##feat<header-USA#342>:** create header with drop-down menu
|--> **description:**<!--add drop-down menu for categories with redirect.-->
|--> **How to test it?:** <!--- Don't forget to add a link to a Workspace where this branch is linked -->[Workspace](Link goes here!)
|--> **How does this PR make you feel?:**[:eslabón:](https://a.slack-edge.com/production-standard-emoji-assets/13.0/google-medium/1f517.png)****](**[http://giphy.com/](http://giphy.com/)**)
|--> **#### Screenshots or example usage:**<!--- Add some images or gifs to showcase changes in behaviour or layout. Example: before and after images, use only browser of GitHub-->
|--> **Does it depend on another component?:** <!---if depent of any apps-->								 |--> **url-custom-apps:** <!---link a apps donde los proyectos necesiten de ellas para	funcionar.-->
|--> **name-element-additional:** <!--mensaje-elemento-adicional
```

#### Merge

- Antes de cualquier merge el PR debe tener como minimo la revicion del TL.
- Para los mege de cada proyecto el responsable será el TL o quien a criterio del TL sea el encargado.

## Readme

Cada proyecto debe tener su readme.md al detalle de que hace su componente, elemento o aplicación. Con el fin de ayudar a los demas a entender su uso y comportamiento.

Elemplo:

#### CardsCatalogos

Es una app que recibe un script de tiendeo.com.co el cual contiene toda la informacion del catalogo de tiendas Jumbo.

```tsx
import React, { useEffect } from 'react';
const CardsCatalogos = () => {
  useEffect(() => {
    const script = document.createElement('script');
    script.src =
      'https://www.tiendeo.com.co/_integrations/slider.js?origin=jumbo';
    script.async = true;
    document.getElementById('tiendeo_container')?.appendChild(script);
    return () => {
      document.getElementById('tiendeo_container')?.removeChild(script);
      const where = document.getElementById('__tiendeoViewerContainer');
      if (where) {
        where.style.display = 'none';
      }
    };
  }, []);
  return <div id='tiendeo_container' />;
};
export default CardsCatalogos;
```

#### Configuration

<hr>
Importe _`tiendasjumboqaio.jumbo-general-apps`_ en las dependencias del tema _`manifest.json`_
```json
"dependencies": {
"tiendasjumboqaio.jumbo-general-apps"
}
```
Adicione el bloque de _`"cards-catalogos"`_ en cualquier plantilla de su tema.
```json
 "flex-layout.row#catalogos__body": {
 "children": ["cards-catalogos"]
 },
```

Del lado del cliente se rendieriza en un landing de catalogos disponibles.

| Prop name | Type | Description   | Default value |
| --------- | ---- | ------------- | ------------- |

### Handles

**CSS Handles**

- containerBanner
- containerTitle
- labelTitle
- spanTitle
- animateText
- imageBanner
- isBig

# Apps Custom

### Css de las app custom

Cada app custom debe mantener sus propios archivos de css de manera independiente al theme. con el fin de que sea reutilizable en diferentes proyectos.
