# recep2012 · Contenido de la app Cook por país

La app **Cook** no lleva textos ni recetas escritos en su código: todo lo de cada país está en un archivo de esta carpeta. La app trae una copia de estos archivos para funcionar sin conexión desde el primer momento y, cuando hay conexión, descarga la versión más reciente. **Para cambiar textos, recetas o el catálogo basta con editar el archivo aquí**: no hace falta publicar una versión nueva de la app.

| Archivo | Para qué sirve |
|---|---|
| `paises/index.json` | Lista de países disponibles y país por defecto |
| `paises/es-ES.json` | España: textos de la app, 301 recetas, catálogo de 609 artículos, secciones, iconos, unidades, voz, alérgenos y dietas |

La app elige el país según el idioma y la región del móvil (por ejemplo `es-ES`); si no hay uno exacto, uno del mismo idioma; si tampoco, el país por defecto. El usuario puede cambiarlo en Ajustes.

## Qué hay en un archivo de país

| Campo | Contenido |
|---|---|
| `formato` | Versión del formato. No lo cambies: si la app no lo entiende, ignora el archivo |
| `version` | **Súbelo en 1 cada vez que publiques cambios** |
| `id`, `idioma`, `nombre` | `es-ES`, idioma de fechas y números, nombre que se ve en Ajustes |
| `textos` | Todos los textos de la app (botones, menús, avisos). `{n}`, `{x}`… se sustituyen por valores; las claves `_1` / `_n` son singular y plural |
| `recetas` | Las recetas (formato abajo) |
| `catalogo` | Secciones del catálogo de la compra; cada artículo es `"Nombre\|icono"` (icono opcional) |
| `catalogo_rapido` | Secciones con botón directo en la lista de la compra |
| `secciones` | Secciones de la lista de la compra, en el orden en que se muestran, con las palabras clave que colocan ahí lo que escribe el usuario |
| `orden_busqueda` | Orden en que se prueban esas palabras clave (de lo más concreto a lo más general) |
| `iconos` | `["🍅", "tomate", …]`: icono que se pone a un artículo según su nombre; gana el primero que coincida |
| `unidades` | Cómo se leen y se muestran las cantidades (kg, l, dientes…) |
| `voz` | Palabras del dictado: números («dos»), unidades («kilos») y separadores («y») |
| `alergenos` | Los 14 alérgenos de la UE con las palabras que los detectan en una receta creada por el usuario |
| `reglas_dieta`, `dietas` | Cómo se calculan y cómo se llaman las dietas |
| `emojis` | Iconos que se ofrecen al crear un ingrediente |

Palabras clave: `"^pollo"` = empieza una palabra; `"=sal"` = palabra exacta; el resto = contiene ese texto.

## Opciones para idiomas con otras reglas

Todo se ajusta en el propio archivo del país, sin tocar la app:

| Campo | Para qué | Ejemplo |
|---|---|---|
| `direccion` | Idiomas que se leen de derecha a izquierda (árabe, hebreo) | `"direccion": "rtl"` |
| `busqueda` | Buscar dentro de las palabras, para idiomas sin espacios (japonés, chino) | `"busqueda": "contiene"` |
| `unidades.espacio` | Sin espacio entre número y unidad | `false` → `200g` |
| `unidades.antes` | Unidades que van delante del número | `["大さじ", "小さじ"]` → `大さじ2` |
| `unidades.fracciones` | Unidades que se muestran con ¼ ½ ¾ y se redondean a cuartos | `["cup", "tsp", "tbsp"]` → `½ cup` |
| `unidades.mostrar.ud` | Contador para cantidades sin unidad | `"個"` → `3個` |
| `unidades.sufijo_plural` / `plurales` | Cómo se forma el plural de las unidades (vacío si el idioma no tiene) | `"plurales": {"clove": "cloves"}` |
| `textos` con `_one`, `_two`, `_few`, `_many`, `_other` | Plurales de idiomas con varias formas (árabe, ruso, polaco); si no están, se usan `_1` y `_n` | `"recetas_n_few": "…"` |
| `voz.sin_espacios` | Dictado en idiomas sin espacios | `true` |
| `voz.orden` | La cantidad va detrás del nombre al hablar | `"nombre_cantidad"` → «牛乳2本» |
| `voz.separadores_pegados` | Palabras que separan artículos sin espacios | `["と", "、"]` |
| `textos.dias` | Los días de la semana en el orden en que empieza la semana en ese país | `["Sunday", "Monday", …]` |

## Formato de una receta

```json
{
  "id": "garbanzos-con-espinacas",
  "nombre": "Garbanzos con espinacas",
  "tipo": "comida",
  "minutos": 25,
  "ingredientes": ["Garbanzos cocidos: 400 g", "Ajo: 2 dientes", "Pimentón dulce"],
  "pasos": "Fríe el ajo y el pan…",
  "alergenos": ["gluten"],
  "dieta": ["vegetariana", "vegana", "sin_cerdo", "sin_lactosa"]
}
```

- `id`: identificador fijo; no lo cambies aunque cambies el nombre. Para una receta nueva usa el nombre en minúsculas, sin tildes y con guiones.
- `tipo`: `comida`, `cena` o `ambas`.
- `ingredientes`: `"Nombre: cantidad unidad"` o solo el nombre. Las cantidades son para `raciones_base` personas (2); una receta puede llevar `"raciones": 4`. Escribe siempre igual el mismo ingrediente («Tomate», no «Tomates») para que se sume bien en la lista.
- `alergenos` (UE, Reglamento 1169/2011): `gluten`, `crustaceos`, `huevo`, `pescado`, `cacahuete`, `soja`, `lacteos`, `frutos_cascara`, `apio`, `mostaza`, `sesamo`, `sulfitos`, `altramuces`, `moluscos`.
- `dieta`: `vegetariana`, `vegana`, `sin_gluten`, `sin_lactosa`, `sin_cerdo`.
- Si quitas `alergenos` y `dieta`, la app los calcula a partir de los ingredientes.

Los alérgenos y dietas son **orientativos**: dependen de los productos concretos. La app lo indica junto a cada receta.

## Antes de guardar un cambio

1. Sube `version` en 1.
2. Comprueba que el JSON es válido (por ejemplo en <https://jsonlint.com>). Si tiene un error, la app lo ignora y sigue con la versión que ya tenía.
3. GitHub puede tardar unos minutos en servir la versión nueva.

## Añadir un país

Copia `es-ES.json` con el nuevo identificador (por ejemplo `es-MX.json`), adáptalo entero (textos, recetas, catálogo, palabras clave, unidades, voz y alérgenos de ese país), súbele la `version` y añádelo a `index.json`. Conviene que lo revise una persona nativa antes de publicarlo.

## Quién puede modificarlo

El repositorio es público para que la app pueda leerlo sin claves, pero solo su propietario puede escribir en él: cualquiera puede verlo o copiarlo, nadie más puede cambiarlo.

© Juani1972. Todos los derechos reservados. Este contenido se publica solo para que lo use la app Cook; no se autoriza su reutilización.
