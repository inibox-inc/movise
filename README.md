# movise v2.0.1

**movise** es una plantilla de películas y series con diseño estilo aplicación nativa Android (Material Design Dark), creada para integrarse en **AppCreator24** utilizando **Blogger** como base de datos y gestor de contenidos (CMS) en tiempo real.

---

## Para qué sirve

Permite gestionar y publicar un catálogo completo de películas y series desde el panel de entradas de Blogger sin necesidad de servidores de bases de datos externos ni conocimientos avanzados de programación. La interfaz principal (`movise-template.html`) se conecta automáticamente a tu blog para mostrar:

- Catálogo separado por **Películas**, **Series** y **Favoritos** (guardados localmente).
- Filtrado instantáneo por géneros y países.
- Buscador en tiempo real por título principal y títulos alternativos.
- Portadas con indicadores automáticos de banderas de idioma (en vertical), calificación (rating) y año de estreno.
- Vista de detalles con fondo (backdrop), póster, títulos alternativos, géneros, año, duración, calificación, reproductor de tráiler, selector de temporadas y episodios con miniatura individual y sinopsis.
- Selector de múltiples servidores de video con indicador de idioma, bandera y tipo de servidor (Sin anuncios, Premium, Con anuncios) e integración de reproductor interno.
- Ajustes de usuario para alternar entre tamaño de portadas pequeñas o grandes.

---

## Tecnologías y código utilizado

El proyecto está construido con tecnologías web estándar sin dependencias pesadas:

- **HTML5**: Estructura semántica de la aplicación y vistas dinámicas en una sola página (SPA).
- **CSS3**: Diseño adaptable (Responsive Design) para móviles, tablets, ordenadores y televisores mediante CSS Grid, Flexbox y Variables CSS (`:root`).
- **JavaScript (Vanilla ES6+)**: Consumo de la API v3 de Blogger (`fetch`), evaluación dinámica de metadatos en entradas, gestión de estado, búsqueda local instantánea y persistencia con `localStorage`.
- **Blogger XML (Layout v3)**: Plantillas `blank.xml` y `theme@v1.1.0.xml` para limpiar y estructurar el blog contenedor.
- **Fuentes e Iconografía**: Google Fonts (`Roboto`) y Google Material Icons (`Material Icons Round`).

### Recursos y fuentes incluidas en el código

```html
<!-- Tipografía Roboto e Iconos Material Design Round -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons+Round" rel="stylesheet">
```

---

## Estructura de archivos del repositorio

```text
movise/
├── blank.xml                   # Plantilla XML para limpiar el código de Blogger
├── theme@v1.1.0.xml            # Plantilla XML base para el blog de Blogger
├── movise-template.html        # Plantilla principal para insertar en AppCreator24
└── posts/
    ├── pelicula.html           # Código base en JavaScript para entradas de películas
    └── serie.html              # Código base en JavaScript para entradas de series
```

---

## Instalación paso a paso

### Paso 1: Configurar el blog en Blogger

1. Ingresa a [https://www.blogger.com](https://www.blogger.com) y crea un nuevo blog siguiendo los pasos (elige el título y el subdominio disponible).
2. En el menú izquierdo de Blogger, dirígete a la sección **Tema**.
3. Haz clic en la flecha desplegable junto al botón **Personalizar** y selecciona **Editar HTML**.
4. Selecciona todo el código existente con `Ctrl + A`, bórralo y pega el contenido completo del archivo `blank.xml`. Haz clic en el icono de **Guardar**. Esta plantilla elimina todo el código por defecto de Blogger para dejarlo completamente limpio.
5. Vuelve a entrar en **Editar HTML**, selecciona todo con `Ctrl + A`, pega el contenido completo del archivo `theme@v1.1.0.xml` y guarda los cambios.

### Paso 2: Instalar la plantilla en AppCreator24

1. Ingresa a [https://www.appcreator24.com](https://www.appcreator24.com) y selecciona tu aplicación.
2. En el menú lateral, dirígete a **Secciones** y haz clic en **Crear sección**.
3. Selecciona el tipo de sección **HTML**.
4. Se mostrarán dos opciones:
   - `Utilizar el editor HTML`
   - `Introducir directamente el código HTML (Avanzado)`
5. Elige la segunda opción: **Introducir directamente el código HTML (Avanzado)**.
6. En el campo **Título de la sección**, escribe `Home` (o el nombre que prefieras).
7. Copia todo el código del archivo `movise-template.html` y pégalo en el cuadro de código HTML.
8. Despliega el apartado **Opciones avanzadas** y configura los siguientes valores exactamente así:
   - **Referencia**: `home`
   - **Abrir enlaces fuera**: `Sí`
   - **Mostrar loader**: `No`
   - **Precargar al iniciar app**: `Sí`
9. Haz clic en **Guardar**.
10. De regreso en la lista de **Secciones**, asegúrate de colocar esta sección arriba del todo en **primera posición** para que se muestre al iniciar la aplicación (si es la primera sección que creas en la app, ya estará en primera posición por defecto).

---

## Configuración de `movise-template.html`

Antes o después de pegar el código en AppCreator24, puedes personalizar los siguientes apartados dentro de `movise-template.html`:

### 1. Cambiar la URL de tu blog de Blogger y API Key

Busca la función `loadContent()` en `movise-template.html` y reemplaza `https://movi-se.blogspot.com/` por la URL de tu propio blog:

```javascript
const apiKey = 'AIzaSyDr0Dt0pwLY9vgxVGK4exxxxxxxxxxxx';

// Reemplaza la URL por la dirección de tu blog de Blogger
const blogUrlRes = await fetch(`https://www.googleapis.com/blogger/v3/blogs/byurl?url=https://tu-blog.blogspot.com/&key=${apiKey}`);
```

### 2. Cambiar el título principal de la aplicación

Para modificar el título del documento y el texto inicial de la barra superior, edita estas líneas:

```html
<!-- Título del documento -->
<title>movise</title>

<!-- Título en la barra superior -->
<div class="app-title" id="appTitle">Películas</div>
```

### 3. Configurar el perfil, enlaces del menú lateral y versión

En la etiqueta `<aside class="sidebar" id="sidebar">` puedes cambiar la imagen de perfil, nombre, usuario, enlaces de Telegram, Facebook, enlace de otras aplicaciones y el texto de versión del pie del menú:

```html
<!-- Cabecera del menú lateral -->
<div class="sidebar-header" onclick="window.open('https://t.me/movise', '_blank')" style="cursor: pointer; display: flex; flex-direction: row; align-items: center; justify-content: flex-start; height: auto; padding: 24px 16px; background: linear-gradient(135deg, rgba(187, 134, 252, 0.15), rgba(0,0,0,0.5)); border-bottom: 1px solid rgba(255,255,255,0.1);">
    <img src="https://www.udrop.com/file/OppW/Nk_20260319_135610_0000.png" alt="movise" style="width: 56px; height: 56px; border-radius: 50%; object-fit: cover; margin-right: 16px; box-shadow: 0 4px 8px rgba(0,0,0,0.5);">
    <div class="user-info">
        <div class="user-name" style="font-size: 18px; font-weight: 700;">movise</div>
        <div class="user-email" style="font-size: 14px; margin-top: 4px; color: var(--text-secondary);">@movise</div>
    </div>
</div>
```

Para cambiar la URL que se abre al pulsar **Compartir app** en el menú de tres puntos superior:

```javascript
document.getElementById('shareAppBtn').addEventListener('click', () => {
    moreModal.classList.remove('active');
    window.open('https://play.google.com/store/apps/details?id=com.movise.app', '_blank');
});
```

### 4. Cómo ocultar opciones del menú lateral (Apartado APPS o Apartado Soporte)

Si deseas ocultar bloques del menú lateral como **Apartado APPS** o **Apartado Soporte**, tienes dos métodos:

#### Opción A: Ocultar mediante comentarios HTML

Envuelve el bloque que no quieras mostrar entre `<!--` y `-->`:

```html
<!--
<div class="sidebar-divider"></div>
<div class="sidebar-label">Apartado APPS</div>
<div class="nav-item" onclick="window.open('https://hydrakids.app', '_blank')">
    <i class="material-icons-round">child_care</i>
    <span>Hydra Kids</span>
</div>
-->

<!--
<div class="sidebar-divider"></div>
<div class="sidebar-label">Apartado Soporte</div>
<div class="nav-item" onclick="window.open('https://t.me/movise', '_blank')">
    <i class="material-icons-round">send</i>
    <span>Siguenos en Telegram</span>
</div>
<div class="nav-item" onclick="window.open('https://facebook.com/movise', '_blank')">
    <i class="material-icons-round">facebook</i>
    <span>Siguenos en Facebook</span>
</div>
-->
```

#### Opción B: Ocultar con `style="display: none;"`

También puedes agregar `style="display: none;"` directamente en el elemento que quieras ocultar sin borrarlo:

```html
<div class="sidebar-divider" style="display: none;"></div>
<div class="sidebar-label" style="display: none;">Apartado APPS</div>
<div class="nav-item" style="display: none;" onclick="window.open('https://hydrakids.app', '_blank')">
    <i class="material-icons-round">child_care</i>
    <span>Hydra Kids</span>
</div>
```

### 5. Configurar la barra de géneros (`#genresBar`)

Puedes añadir, cambiar o quitar botones de filtro en el contenedor `#genresBar`. El atributo `data-genre` debe coincidir (sin importar mayúsculas o minúsculas) con el género o etiqueta asignado a la película o serie:

```html
<div class="genres-bar" id="genresBar">
    <button class="genre-chip active" data-genre="">Todos</button>
    <button class="genre-chip" data-genre="Accion">Acción</button>
    <button class="genre-chip" data-genre="Drama">Drama</button>
    <button class="genre-chip" data-genre="Romance">Romance</button>
    <button class="genre-chip" data-genre="Comedia">Comedia</button>
    <button class="genre-chip" data-genre="Terror">Terror</button>
    <button class="genre-chip" data-genre="Corea">Corea</button>
    <button class="genre-chip" data-genre="Japon">Japón</button>
    <button class="genre-chip" data-genre="China">China</button>
</div>
```

### 6. Cómo añadir o eliminar idiomas y banderas

En `movise-template.html`, los idiomas se definen mediante códigos numéricos en el objeto `LANGUAGES`. Por defecto están configurados los códigos `1`, `2` y `3`:

```javascript
const LANGUAGES = {
    "1": {
        name: "Latino",
        flag: "https://www.worldometers.info/images/flags/w160/mx.webp"
    },
    "2": {
        name: "Castellano",
        flag: "https://www.worldometers.info/images/flags/w160/es.webp"
    },
    "3": {
        name: "English",
        flag: "https://www.worldometers.info/images/flags/w160/us.webp"
    }
};
```

Para **añadir más idiomas** (por ejemplo Coreano, Japonés o Francés), obtén la URL de la bandera desde el catálogo oficial de Worldometers:
[https://www.worldometers.info/geography/flags-of-the-world/](https://www.worldometers.info/geography/flags-of-the-world/)

Copia la dirección de la imagen de la bandera (formato `https://www.worldometers.info/images/flags/w160/CODIGO_PAIS.webp`) y agrega un nuevo número al objeto `LANGUAGES`:

```javascript
const LANGUAGES = {
    "1": {
        name: "Latino",
        flag: "https://www.worldometers.info/images/flags/w160/mx.webp"
    },
    "2": {
        name: "Castellano",
        flag: "https://www.worldometers.info/images/flags/w160/es.webp"
    },
    "3": {
        name: "English",
        flag: "https://www.worldometers.info/images/flags/w160/us.webp"
    },
    "4": {
        name: "Coreano",
        flag: "https://www.worldometers.info/images/flags/w160/ks.webp"
    },
    "5": {
        name: "Japonés",
        flag: "https://www.worldometers.info/images/flags/w160/ja.webp"
    }
};
```

Para **eliminar un idioma**, simplemente borra su bloque numérico correspondiente dentro de `LANGUAGES`.

---

## Cómo publicar Películas y Series desde Blogger

### Obtención de metadatos con TMDB

Para obtener toda la información oficial de una película o serie (título, títulos alternativos, sinopsis, duración, calificación, póster vertical, fondo horizontal e imágenes de cada episodio), utiliza **The Movie Database (TMDB)**:

- Sitio web: [https://www.themoviedb.org/](https://www.themoviedb.org/)

En TMDB puedes copiar directamente las direcciones de las imágenes:
- **Póster vertical**: `https://image.tmdb.org/t/p/w500/NOMBRE_ARCHIVO.jpg`
- **Fondo (Backdrop) principal**: `https://image.tmdb.org/t/p/original/NOMBRE_ARCHIVO.jpg`
- **Miniatura (Backdrop) de episodio**: `https://image.tmdb.org/t/p/w500/NOMBRE_ARCHIVO.jpg`

### Pasos para crear una entrada en Blogger

1. En el panel de Blogger, haz clic en **Nueva entrada**.
2. En el campo **Título** superior de la entrada, escribe el nombre de la película o serie.
3. Cambia el modo del editor de Blogger haciendo clic en el primer icono de la barra de herramientas (el icono de lápiz / `<>`) y selecciona **Vista HTML**.
4. En el panel derecho de la entrada, dentro de **Etiquetas**, añade las etiquetas separadas por comas:
   - **Etiqueta de tipo**: Pon `Peliculas` si es una película, o `Series` si es una serie.
   - **Etiqueta de año**: Pon el año de estreno en formato de 4 dígitos (por ejemplo: `2026`). Este año aparecerá en la esquina inferior izquierda de la portada en el inicio.
   - **Etiquetas de géneros / países (opcional)**: Puedes agregar etiquetas como `Accion, Drama, Romance, Corea`, además de definirlas en la variable `genres` dentro del código.
5. Pega en el cuerpo de la entrada (en **Vista HTML**) el código correspondiente de `posts/pelicula.html` o `posts/serie.html` con los datos rellenados y haz clic en **Publicar**.

---

### Plantilla para Películas (`posts/pelicula.html`)

Copia y pega este código en la **Vista HTML** de tu entrada de Blogger cuando publiques una película:

```javascript
/* ==========================================
   movise v2.0.1
   Copyright (c) 2026 movise. Todos los derechos reservados.
   Plantilla de entrada: Película
   ========================================== */

const title = "Título de la Película";
const alternative_titles = "Título Alternativo 1, Título Alternativo 2";
const sinopsis = "Escribe aquí la sinopsis o descripción completa de la película.";
const poster = "https://image.tmdb.org/t/p/w500/TU_POSTER.jpg";
const backdrop = "https://image.tmdb.org/t/p/original/TU_BACKDROP.jpg";
const duration = "1h 45m";
const genres = ["Accion", "Drama", "Romance"];
const category = "Película";
const rating = "8.5";
const trailer = "https://www.youtube.com/embed/TU_TRAILER";

const servers = [
    {
        server: "Streamwish",
        language: "1",
        type: "Sin anuncios",
        url: "https://tu-servidor.com/embed/video1"
    },
    {
        server: "Filemoon",
        language: "2",
        type: "Premium",
        url: "https://tu-servidor.com/embed/video2"
    },
    {
        server: "Voe",
        language: "3",
        type: "Con anuncios",
        url: "https://tu-servidor.com/embed/video3"
    }
];
```

---

### Plantilla para Series (`posts/serie.html`)

Copia y pega este código en la **Vista HTML** de tu entrada de Blogger cuando publiques una serie:

```javascript
/* ==========================================
   movise v2.0.1
   Copyright (c) 2026 movise. Todos los derechos reservados.
   Plantilla de entrada: Serie
   ========================================== */

const title = "Título de la Serie";
const alternative_titles = "Título Alternativo 1, Título Alternativo 2";
const sinopsis = "Escribe aquí la sinopsis o descripción completa de la serie.";
const poster = "https://image.tmdb.org/t/p/w500/TU_POSTER.jpg";
const backdrop = "https://image.tmdb.org/t/p/original/TU_BACKDROP.jpg";
const duration = "45m";
const genres = ["Drama", "Romance", "Corea"];
const category = "Serie";
const rating = "9.0";
const trailer = "https://www.youtube.com/embed/TU_TRAILER";

const seasons = [
    {
        season: 1,
        episodes: [
            {
                episode: 1,
                title: "Comienzo",
                backdrop: "https://image.tmdb.org/t/p/w500/TU_EP1_BACKDROP.jpg",
                servers: [
                    {
                        server: "Streamwish",
                        language: "1",
                        type: "Sin anuncios",
                        url: "https://tu-servidor.com/embed/t1-ep1-srv1"
                    },
                    {
                        server: "Filemoon",
                        language: "2",
                        type: "Premium",
                        url: "https://tu-servidor.com/embed/t1-ep1-srv2"
                    }
                ]
            },
            {
                episode: 2,
                title: "El encuentro",
                backdrop: "https://image.tmdb.org/t/p/w500/TU_EP2_BACKDROP.jpg",
                servers: [
                    {
                        server: "Streamwish",
                        language: "1",
                        type: "Sin anuncios",
                        url: "https://tu-servidor.com/embed/t1-ep2-srv1"
                    }
                ]
            }
        ]
    },
    {
        season: 2,
        episodes: [
            {
                episode: 1,
                title: "Nuevo ciclo",
                backdrop: "https://image.tmdb.org/t/p/w500/TU_T2_EP1_BACKDROP.jpg",
                servers: [
                    {
                        server: "Streamwish",
                        language: "3",
                        type: "Sin anuncios",
                        url: "https://tu-servidor.com/embed/t2-ep1-srv1"
                    }
                ]
            }
        ]
    }
];
```

---

### Cómo añadir más servidores, episodios o temporadas

#### Añadir un nuevo servidor

Dentro del arreglo `servers: [ ... ]` (tanto en una película como dentro de un episodio de serie), agrega un nuevo bloque separado por coma:

```javascript
{
    server: "NombreDelServidor",
    language: "1", // 1 = Latino, 2 = Castellano, 3 = English
    type: "Sin anuncios", // Ej: "Sin anuncios", "Premium", "Con anuncios"
    url: "https://tu-servidor.com/embed/codigo"
}
```

#### Añadir un nuevo episodio a una temporada

Dentro del arreglo `episodes: [ ... ]` de la temporada correspondiente, añade un nuevo objeto separado por coma:

```javascript
{
    episode: 3,
    title: "Título del episodio 3",
    backdrop: "https://image.tmdb.org/t/p/w500/TU_EP3_BACKDROP.jpg",
    servers: [
        {
            server: "Streamwish",
            language: "1",
            type: "Sin anuncios",
            url: "https://tu-servidor.com/embed/t1-ep3-srv1"
        }
    ]
}
```

#### Añadir una nueva temporada

Dentro del arreglo principal `const seasons = [ ... ]`, añade un nuevo bloque de temporada al final separado por coma:

```javascript
{
    season: 3,
    episodes: [
        {
            episode: 1,
            title: "Regreso",
            backdrop: "https://image.tmdb.org/t/p/w500/TU_T3_EP1_BACKDROP.jpg",
            servers: [
                {
                    server: "Streamwish",
                    language: "1",
                    type: "Sin anuncios",
                    url: "https://tu-servidor.com/embed/t3-ep1-srv1"
                }
            ]
        }
    ]
}
```

---

## Licencia y Copyright

Copyright (c) 2026 **movise v2.0.1**. Todos los derechos reservados.

