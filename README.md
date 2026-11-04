# Catálogo de Productos – Simulador de Entrenamiento

## Estructura del proyecto

- `index.html`: maquetado semántico (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`).
- `style.css`: herencia, selectores combinados, modelo de caja y fondos.
- `banner.svg`: imagen de fondo del encabezado.
- `README.md`: documentación.

---

## Subactividad 1: Jerarquía de estilos

### Cálculo de puntos de especificidad

Valores:

- Etiqueta (a, ul, li) = 1 punto
- Clase (.btn-comprar) = 10 puntos
- ID (#btn-destacado) = 100 puntos

Ejemplos de mi código:

- header nav ul li a = 1+1+1+1+1 = 5 puntos
- aside ul li a = 1+1+1+1 = 4 puntos
- footer ul li a = 1+1+1+1 = 4 puntos
- .btn-comprar = 10 puntos
- .destacado = 10 puntos
- #btn-destacado = 100 puntos

### Conflicto de autoridad

Con `.btn-comprar` (10 pts) y `#btn-destacado` (100 pts) sobre el mismo enlace, el ID gana
aunque la clase esté escrita después, porque la especificidad pesa más que el orden.

### Refactorización

Se eliminaron las reglas con `#id` y se usó un sistema plano de etiquetas y clases.
`.btn-comprar` y `.destacado` valen 10 pts; al empatar gana la última escrita (cascada).
No se usó `!important`.

### Herencia

`font-family` y `color` se declaran solo en `body` y los demás elementos los heredan.

---

## Hallazgos: El Modelo de Caja

1. Margin y padding

El padding es el espacio de adentro de la tarjeta, o sea lo que separa el texto del borde. El
margin es el espacio de afuera, lo que separa una tarjeta de la otra. Cuando le puse padding a
los article el texto ya no quedaba pegado al borde, y con el margin las tarjetas dejaron de
estar juntas.

2. Por qué usar box-sizing: border-box

Sin eso, cuando le agrego padding o borde a una caja se hace más grande de lo que puse en el
width, y se puede salir de su contenedor. Con border-box el padding y el borde cuentan dentro
del ancho, entonces la caja se queda del tamaño que yo le dije.

3. Margen grande y elementos hermanos

Si le pongo un margen grande a un article, los que están al lado o debajo se mueven y queda más
espacio entre ellos. Probé subiéndole el margin a una tarjeta y las demás se corrieron.

**Auditoría con DevTools:** al inspeccionar un `<article>`, la pestaña Computed muestra
padding 20px, margin 15px y borde 1px, que coinciden con lo programado en `style.css`.


## Hallazgos: Centralización de Identidad Visual y Espaciado

En esta sección se documenta el proceso de estandarización aplicado a la hoja de estilos del catálogo deportivo, centralizando los valores clave mediante el uso de variables CSS en el selector `:root`.

### 1. Lista completa de variables declaradas

A nivel global se definieron las siguientes variables de color y espaciado para mantener la consistencia en todo el sitio web:

* **Colores:**
  * `--color-encabezado`: `rgb(240, 14, 93)` (Tono fucsia/rosado asignado a la barra de navegación y elementos de cabecera).
  * `--color-primario`: `rgb(10, 185, 220)` (Tono celeste cian utilizado para los títulos principales, tipografía base del cuerpo y bordes de las tarjetas de productos).
  * `--color-terciario`: `rgb(0, 0, 0)` (Color negro puro para el texto principal del contenido y enlaces secundarios).
  * `--color-botan-compra`: `rgb(1, 131, 1)` (Tono verde corporativo destinado a destacar los botones de compra).

* **Espaciados:**
  * `--espacio-pequeno`: `8px` (Margen o relleno compacto).
  * `--espacio-mediano`: `16px` (Espaciado estándar para paddings internos de contenedores).
  * `--espacio-grande`: `24px` (Espaciado amplio para separación entre bloques, márgenes de secciones, headers, main, aside y footer).

### 2. Ventaja de reutilizar medidas de margen y relleno frente a valores arbitrarios

Reutilizar las variables de espaciado (`--espacio-pequeno`, `--espacio-mediano`, `--espacio-grande`) en lugar de escribir valores numéricos aleatorios o inventados en cada selector aporta importantes ventajas:
* **Consistencia visual:** Garantiza que los márgenes y rellenos guarden una proporción armónica y matemática en toda la página, evitando desalineaciones visuales.
* **Mantenimiento simplificado:** Si en el futuro se requiere ajustar el espaciado global del sitio, solo es necesario modificar el valor en el bloque `:root` en lugar de buscar y cambiar cada selector de forma manual.
* **Legibilidad del código:** El código CSS se vuelve más semántico y fácil de comprender, ya que los nombres de las variables indican claramente la intención del espacio.

### 3. Prevención de colisiones visuales mediante la centralización en `:root`

La centralización de valores en el pseudo-elemento `:root` actúa como una única fuente de verdad (*Single Source of Truth*) para la hoja de estilos. A medida que el proyecto web crece y se agregan más componentes (como nuevas páginas, secciones, tarjetas de productos o paneles laterales):
* Se evitan conflictos de especificidad y duplicidad de reglas que puedan causar sobreescrituras imprevistas o "colisiones visuales" (como elementos encimados, desbordamientos de contenedores o inconsistencias de color).
* Permite escalar el desarrollo de manera ordenada y estructurada, asegurando que cualquier componente nuevo herede automáticamente la identidad visual y los patrones de diseño definidos.