Hallazgos: Arquitectura BEM y Modularidad

1. ¿Qué significa BEM y cómo se escribe? BEM significa Block, Element, Modifier (Bloque, Elemento, Modificador). El bloque es el componente independiente (.card), el elemento es una parte que solo existe dentro del bloque y se escribe con doble guion bajo (.card__title), y el modificador es una variación y se escribe con doble guion medio (.card--destacada, .btn--secundario). Visualmente: bloque__elemento--modificador.

2. ¿Por qué dividir el CSS en varios archivos ayuda al trabajo colaborativo? Cada persona puede trabajar en un componente (tarjeta.css, botones.css, menu-lateral.css) sin editar el mismo archivo que otra, lo que reduce los conflictos al hacer merge en Git. Además es más fácil encontrar y corregir el código de un componente, y todo se une en style.css con @import.

3. ¿Cómo evita BEM la guerra de especificidad? Todos los selectores son una sola clase (peso 10, por ejemplo .card__title) en lugar de selectores anidados como main article h2 (peso 0-1-3). Como todos pesan lo mismo, la regla que gana es la que va después en el archivo, y no hace falta usar !important ni selectores cada vez más largos.