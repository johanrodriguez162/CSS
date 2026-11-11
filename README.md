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

Hallazgos: Pseudoclases y Pseudoelementos

En esta subactividad le di interactividad y detalles decorativos al Catálogo Deportivo usando solo CSS, sin modificar el HTML.

1. Diferencia funcional entre pseudoclase y pseudoelemento

Una pseudoclase (:hover, :active, :focus) selecciona un elemento que ya existe en el HTML cuando se encuentra en un estado determinado, por ejemplo cuando el usuario pasa el cursor, hace clic o llega a él con el teclado. Es decir, reacciona a eventos del usuario.

Un pseudoelemento (::before, ::after) en cambio crea contenido virtual que no está escrito en el HTML. En el proyecto lo usé para poner una cuadrito decorativo antes de cada categoría del <aside> y una línea decorativa debajo del título de cada producto. Entonces: la pseudoclase cambia cómo se ve algo según el estado, y el pseudoelemento inyecta contenido.

2. Importancia de :focus para la accesibilidad web

Hay personas que no usan el mouse: navegan con la tecla Tab, ya sea por limitaciones motrices, por usar lectores de pantalla o simplemente por preferencia. La pseudoclase :focus muestra un contorno visible (outline) en el enlace o botón activo, y así saben en qué parte de la página están. Sin ese indicador no podrían saber dónde están ubicados, y se incumplen las pautas de accesibilidad WCAG. Por eso personalicé el contorno con el color secundario en las categorías del <aside> y en los botones de compra, en lugar de quitarlo.

3. Por qué inyectar elementos decorativos desde CSS

Las líneas, viñetas e iconos decorativos no aportan significado al contenido. Si los pusiera en el HTML con etiquetas vacías (como <span></span>) ensuciaría el código, lo haría más difícil de mantener y un lector de pantalla podría leerlos como contenido real. Con ::before y ::after el HTML se mantiene limpio y semántico, y el diseño se puede cambiar desde un solo lugar (el CSS) sin tocar la estructura, por ejemplo, cambiar el color o el tamaño de la línea decorativa con una sola regla.

Auditoría con DevTools

Con las herramientas de desarrollador (F12 → Elements → Styles → :hov) activé los estados :hover, :active y :focus sobre las categorías y los botones de compra, y comprobé que el navegador aplica los estilos solo mientras el estado está activo. También verifiqué que los bloques ::before y ::after aparecen en el árbol del DOM virtual, aunque no existen en el archivo HTML.

Comandos usados
bash
git checkout -b feature/interactividad-css
git add .
git commit -m "feat(ui): implementar pseudoclases interactivas en aside y pseudoelementos en productos"
git push origin feature/interactividad-css