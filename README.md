## Hallazgos: Arquitectura Total con Flexbox

**1. ¿Por qué fue crucial `min-height: 100vh` y `flex-direction: column` en el contenedor global?**
`.app-layout` es un flex en columna que mide como mínimo el alto de la pantalla. Como `.main-wrapper` tiene `flex: 1`, absorbe todo el espacio libre y empuja el footer al fondo, incluso cuando hay poco contenido.

**2. ¿Cómo `gap` reemplazó los márgenes laterales en los menús?**
Con `gap` en `.nav__list` el espacio se aplica solo entre elementos, sin márgenes en cada `li`. Así no sobra espacio al final y se cambia en un solo lugar con `var(--espacio-mediano)`.

**3. ¿Cómo BEM, Custom Properties y Flexbox crean una tarjeta resistente a distintos textos?**
`.card` es un flex en columna y `.card__description` tiene `flex-grow: 1`, así que absorbe el espacio sobrante y el precio y el botón quedan siempre abajo. Las clases BEM mantienen cada regla en un solo lugar, y las variables mantienen colores y espacios consistentes.