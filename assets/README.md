# Gráficos de CRUISING

Todo el arte del juego vive en estos ficheros PNG. Puedes abrirlos con cualquier
editor de pixel art (Aseprite, Piskel, Photoshop, GIMP...) y modificarlos —
el juego los carga tal cual, sin ningún paso de compilación.

**Regla importante:** no cambies el tamaño del lienzo (ancho/alto en píxeles)
de ningún fichero, ni muevas los elementos a otra celda de la rejilla. El
código busca cada sprite por su posición exacta dentro de la hoja. Puedes
repintar libremente el contenido de cada celda, cambiar colores, formas,
añadir detalles, etc. — mientras cada celda mida lo mismo y esté en el mismo
sitio, todo seguirá funcionando.

Todas las hojas usan fondo transparente. Las celdas vacías deben seguir siendo
transparentes (no las rellenes de un color sólido) para que el sprite no se
vea con una caja rectangular alrededor.

## Ficheros y su rejilla

### `tiles.png` — 96×16 px, 6 celdas de 16×16 px
El terreno del mapa. Cada celda es una casilla completa (opaca, sin transparencia).

| Celda (de izquierda a derecha) | Contenido |
|---|---|
| 1 | Césped, variante 1 |
| 2 | Césped, variante 2 |
| 3 | Césped, variante 3 |
| 4 | Césped, variante 4 |
| 5 | Arbusto (sólido: el jugador no puede atravesarlo) |
| 6 | Árbol (sólido) |

El juego elige entre las 4 variantes de césped según la posición de cada
casilla en el mapa, para que no se vea todo repetido igual.

### `player.png` y `player_naked.png` — 128×18 px, 8 celdas de 16×18 px
El personaje jugable. `player_naked.png` es la variante "en pelotas" (cuando
el Sado te desnuda). Cada fila lógica son 2 celdas (2 fotogramas de caminar)
por dirección, en este orden:

| Celdas | Dirección |
|---|---|
| 1-2 | Arriba (de espaldas) |
| 3-4 | Derecha |
| 5-6 | Abajo (de frente) |
| 7-8 | Izquierda |

Dentro de cada pareja, la celda 1 y la celda 2 son los dos fotogramas de la
animación al caminar (alternan al moverse).

### `cop.png` y `sado.png` — 32×18 px, 2 celdas de 16×18 px
El policía y el Sado. No tienen sprites por dirección (siempre miran de
frente); las 2 celdas son los 2 fotogramas de caminar.

### `npcs.png` — 64×18 px, 4 celdas de 16×18 px
Los personajes con los que puedes hacer "match". Una celda por color, en
este orden: **rojo, azul, verde, amarillo**. No tienen animación de caminar
(están quietos esperando).

### `items.png` — 96×16 px, 6 celdas de 16×16 px

| Celda | Contenido |
|---|---|
| 1 | Condón rojo |
| 2 | Condón azul |
| 3 | Condón verde |
| 4 | Condón amarillo |
| 5 | Pastilla (cura la peste) |
| 6 | Camiseta (para vestirte tras quedarte en pelotas) |

## Efectos que NO están en las imágenes (se dibujan por código)

Algunos efectos siguen siendo dinámicos a propósito, porque cambian de
tamaño/color/opacidad en tiempo real y no tendría sentido "hornearlos" en
una imagen fija:
- El aura de colores detrás de los NPCs y el brillo de la pastilla/ropa.
- El tinte verde cuando el jugador tiene la peste.
- El parpadeo de ojos rojo/azul del policía cuando el jugador está infectado
  o desnudo, y el aviso "!" del Sado al perseguirte.
- El parpadeo del jugador tras ser atrapado (invulnerabilidad).

Si quieres cambiar esos efectos, hay que tocar el código en `index.html`
(busca los comentarios `runtime overlay` / `código` cerca de cada función
`draw...`), no las imágenes.
