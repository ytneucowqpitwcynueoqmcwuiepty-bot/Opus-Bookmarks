# Toolkit OSINT / Pentest

Directorio de herramientas y recursos de OSINT y pentesting en **un único archivo HTML**: enlaces organizados por carpetas y subcategorías, con buscador, filtro de herramientas que requieren cuenta y exportación a marcadores del navegador.

Sin dependencias, sin build, sin servidor y sin peticiones externas: se abre con doble clic.

## Contenido

El contador de la cabecera indica cuántos enlaces hay en cada momento (y cuántos coinciden con la búsqueda activa).

| Carpeta | Qué incluye |
|---|---|
| Anonimato y privacidad | Identidades ficticias, email temporal y alias, SMS online, test de fugas y fingerprint, Tor y VPN, exploradores cripto |
| Personas y empresas | Emails, teléfonos, nombres de usuario, buscadores de personas, redes sociales, registros mercantiles y listas de sanciones (con recursos de España) |
| Buscadores | Buscadores generales, metabuscadores, archivo web, dorking, búsqueda de código |
| Geo y mapas | Mapas, satélite, street view, geolocalización, clima y desastres, sol y sombras, cartografía de España |
| Infraestructura y red | Whois y DNS, subdominios, Shodan y similares, análisis de webs, TLS y cabeceras, reputación de IPs |
| Malware y phishing | Análisis de muestras, ransomware, phishing |
| Pentest | CVEs y exploits, guías y chuletas, utilidades, labs y CTF, bug bounty |
| Para instalar | Herramientas de pentest, de OSINT y otras para instalar en local |
| Imágenes | Búsqueda inversa, metadatos, forense, reconocimiento facial, edición |
| Verificación y noticias | Fact-checking, sesgo mediático, noticias y datos, verificación de vídeo y foto |
| Vídeo y webcams | Buscadores de vídeo, análisis de vídeo, webcams |
| Transporte | Aviones, barcos, trenes, satélites |
| Leaks | Documentos filtrados, credenciales |
| Informes y gráficos | Diagramas y timelines, datos, informes de pentest |
| Otras recopilaciones | Directorios y listas OSINT |

## Cómo usarlo

### Abrirlo

1. Descarga o clona el repositorio.
2. Abre `index.html` en tu navegador.

Funciona desde un archivo local, también sin conexión (los enlaces, claro, necesitan red). Si activas GitHub Pages (*Settings → Pages*, rama `main`, carpeta `/ (root)`), también queda disponible en `https://<usuario>.github.io/<repositorio>/`.

### Navegar

- Cada **carpeta** es un desplegable, y dentro de ella hay **subcategorías**, también desplegables. El número entre paréntesis es la cantidad de enlaces que contiene.
- Un clic en un enlace lo abre en una pestaña nueva (con `noopener noreferrer`). Al pasar el ratón por encima se ve la URL completa.

### Buscar

Escribe en el cuadro de búsqueda de la cabecera. La búsqueda:

- No distingue mayúsculas de minúsculas.
- Busca coincidencias parciales en el **nombre** de la herramienta, en su **URL**, en el nombre de la **subcategoría** y en el de la **carpeta**.
- Abre automáticamente todas las carpetas y subcategorías con resultados y oculta las que no tienen ninguno.
- Actualiza el contador con el número de enlaces encontrados.

Ejemplos:

| Búsqueda | Qué encuentra |
|---|---|
| `shodan` | Toda la subcategoría *Shodan y parecidos* (Shodan, Censys, FOFA…), porque el nombre de la subcategoría también cuenta |
| `github.com` | Todas las herramientas alojadas en GitHub |
| `telegram` | Las herramientas con «Telegram» en el nombre (Telemetr, TGStat, Lyzem) |
| `[cuenta]` | Todas las que requieren registro |
| `dns` | Nombres, URLs y subcategorías con "dns" (p. ej. *Whois y DNS*) |

Para volver a la vista normal, borra el texto del cuadro.

### Filtrar las que requieren cuenta

La casilla **«Ocultar las que requieren cuenta»** esconde las entradas marcadas con la etiqueta `[cuenta]` en su nombre. Se combina con la búsqueda y actualiza el contador.

- El filtro se basa únicamente en esa etiqueta. Lo marcado como `(de pago)` es solo informativo: si no lleva también `[cuenta]`, el filtro no lo oculta.

### Expandir y colapsar

Los botones **Expandir** y **Colapsar** abren o cierran de una vez todas las carpetas y subcategorías visibles.

La vista se vuelve a pintar cada vez que escribes en el buscador o cambias la casilla de cuentas, y al hacerlo los desplegables vuelven a su estado por defecto: todo abierto si hay texto de búsqueda, todo cerrado si no lo hay.

### Exportar marcadores

El botón **Exportar marcadores** descarga `marcadores-osint-pentest.html`, un archivo de marcadores en el formato estándar de Firefox y Chrome (Netscape Bookmark), que se puede importar tal cual.

- Se exporta **todo el catálogo**, no solo lo que se ve: la búsqueda y el filtro de cuentas no afectan al archivo.
- Conserva la jerarquía: `Toolkit OSINT Pentest` → carpeta → subcategoría → enlaces.
- Las etiquetas como `[cuenta]` se mantienen en el título del marcador.

Para importarlo:

- **Firefox:** *Marcadores → Administrar marcadores → Importar y copias de seguridad → Importar marcadores desde HTML*.
- **Chrome / Edge / Brave:** abre el administrador de marcadores, menú `⋮` → *Importar marcadores* y elige el archivo.

## Añadir o editar herramientas

Todo el contenido está en el objeto `datos`, dentro de la etiqueta `<script>` de `index.html`. La estructura es:

```js
const datos = {
  "Carpeta": {
    "Subcategoría": [
      ["Nombre de la herramienta", "https://ejemplo.com/"],
      ["Otra herramienta [cuenta]", "https://otra.com/"]
    ]
  }
};
```

- Cada herramienta es un par `["nombre", "URL"]`.
- Para marcar una herramienta que exige registro, añade `[cuenta]` al final del nombre. Es lo que usan el filtro y la búsqueda.
- Una subcategoría nueva es una clave nueva dentro de su carpeta, y una carpeta nueva es una clave nueva en el nivel superior.
- El orden en pantalla (y en la exportación) es el orden en que aparecen en el código.
- Si el nombre lleva comillas dobles, escápalas: `\"`. El resto de caracteres especiales (`&`, `<`, `>`) no dan problemas.
- Los contadores se recalculan solos.

### Cambiar los colores

Los colores son variables CSS al principio del archivo, en `:root`:

| Variable | Uso |
|---|---|
| `--fondo` | Fondo de la página y de la cabecera |
| `--caja` | Fondo de las carpetas, del buscador y de los botones |
| `--borde` | Bordes |
| `--texto` | Texto y enlaces |
| `--gris` | Contador y etiqueta de la casilla |
| `--azul` | Acento (subcategorías y enlaces al pasar el ratón) |

## Privacidad

La página no hace ninguna petición de red por sí misma, no usa cookies ni almacenamiento local y no guarda nada: al recargar vuelve al estado inicial. Solo se conecta a un servicio cuando haces clic en uno de sus enlaces.

## Compatibilidad

Cualquier navegador moderno con soporte de `<details>`, columnas CSS y JavaScript ES6.

## Aviso legal y uso responsable

Este repositorio es solo un directorio de enlaces a servicios y herramientas de terceros, con los que no tiene ninguna relación. Muchos de ellos (búsqueda de personas, reconocimiento facial, bases de credenciales filtradas, escáneres de infraestructura, etc.) tienen un uso legítimo en investigación, periodismo y seguridad ofensiva autorizada, pero también pueden usarse para dañar a otros.

- Usa las herramientas de pentesting únicamente sobre sistemas propios o con autorización expresa y por escrito.
- Respeta la legislación aplicable (por ejemplo, la normativa de protección de datos y la de acceso a sistemas informáticos) y los términos de servicio de cada plataforma.
- Quien use este toolkit es el único responsable de cómo lo usa.

Algunos enlaces pueden dejar de funcionar con el tiempo, cambiar de condiciones o pasar a ser de pago. Si encuentras uno caído, abre un issue o un pull request.
