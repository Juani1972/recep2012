# recep2012 · Recetario de Cook

Recetas y catálogo de la compra que descarga la app **Cook**. La app los lee al abrirse, los guarda en el móvil y, sin conexión, usa la última copia descargada. Para añadir o cambiar recetas basta con editar el archivo aquí: no hace falta publicar una versión nueva de la app.

| Archivo | Mercado | Contenido |
|---|---|---|
| `recetas/es-ES.json` | España | 301 recetas con alérgenos y dietas · catálogo de 609 artículos |

Más adelante se añadirán otros mercados, cada uno adaptado a su país (por ejemplo `recetas/en-GB.json`).

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
- `ingredientes`: `"Nombre: cantidad unidad"` (g, kg, ml, l, ud, cda, dientes, latas…) o solo el nombre si no lleva cantidad. Las cantidades son para `raciones_base` personas (2); una receta puede llevar `"raciones": 4`. Escribe siempre igual el mismo ingrediente («Tomate», no «Tomates») para que se sume bien en la lista de la compra.
- `alergenos`: los 14 de declaración obligatoria en la UE (Reglamento 1169/2011): `gluten`, `crustaceos`, `huevo`, `pescado`, `cacahuete`, `soja`, `lacteos`, `frutos_cascara`, `apio`, `mostaza`, `sesamo`, `sulfitos`, `altramuces`, `moluscos`.
- `dieta`: `vegetariana`, `vegana`, `sin_gluten`, `sin_lactosa`, `sin_cerdo`.
- Si quitas `alergenos` y `dieta` de una receta, la app los calcula a partir de los ingredientes.

Los alérgenos y dietas se han calculado a partir de los ingredientes y son **orientativos**: dependen de los productos concretos (un caldo, un chorizo o una salsa pueden llevar gluten, lácteos o apio). La app lo indica junto a cada receta.

## Catálogo

`catalogo` agrupa los artículos de la compra por sección. Cada artículo es `"Nombre|icono"` (el icono es opcional), por ejemplo `"Pilas AA|🔋"`.

## Antes de guardar un cambio

Si el JSON tiene un error, la app lo ignora y sigue con las recetas que ya tenía. Comprueba el archivo en <https://jsonlint.com> si dudas. GitHub puede tardar unos minutos en servir la versión nueva.

## Quién puede modificarlo

El repositorio es público para que la app pueda leerlo sin claves, pero solo su propietario puede escribir en él: cualquiera puede verlo o copiarlo, nadie más puede cambiarlo. Las propuestas de otras personas (pull requests) solo se incorporan si el propietario las acepta.

© Juani1972. Todos los derechos reservados. Este contenido se publica solo para que lo use la app Cook; no se autoriza su reutilización.
