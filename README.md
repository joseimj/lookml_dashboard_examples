# LookML Dashboard Examples

> Ejemplos de dashboards de Looker definidos como código (LookML), listos para copiar a un proyecto y adaptar a tu propio modelo.

![Looker](https://img.shields.io/badge/Looker-LookML-5F6CAF?logo=looker&logoColor=white)
![Dashboard as code](https://img.shields.io/badge/dashboard-as--code-1A73E8)
![License](https://img.shields.io/badge/license-MIT-green)

Colección de dashboards de Looker escritos en LookML (archivos `*.dashboard.lookml`). La idea es que sirvan como referencia de buenas prácticas: estructura limpia, KPIs claros, filtros reutilizables y descripciones que dan contexto a los agentes de Gemini en Looker.

## Vista previa

<!-- Sustituye esta imagen por una captura real del dashboard renderizado en Looker -->
![Vista previa del dashboard de Ventas E-commerce](assets/ventas_ecommerce.png)

> **Tip:** sube una captura del dashboard ya renderizado a `assets/` y actualiza la ruta de arriba. Una imagen es, de lejos, lo que más ayuda a que un repo de BI se vea profesional.

## Contenido

| Archivo | Descripción |
|---|---|
| [`ventas_ecommerce.dashboard`](ventas_ecommerce.dashboard) | Dashboard ejecutivo de ventas e-commerce: ingresos, pedidos, ticket promedio, tendencia mensual y top de productos/categorías. |

## Dashboard: Ventas E-commerce

Resumen ejecutivo de la operación de una tienda online. Usa layout `newspaper`, refresco automático cada 12 horas y filtros globales que se propagan a todos los tiles.

### Tiles

| # | Tile | Tipo | Qué muestra |
|---|---|---|---|
| 1 | Ingresos Totales | KPI (single value) | Ingresos netos del periodo (excluye pedidos cancelados) |
| 2 | Total de Pedidos | KPI (single value) | Número de pedidos del periodo |
| 3 | Ticket Promedio | KPI (single value) | Valor promedio por pedido (AOV) |
| 4 | Ingresos por Mes | Línea | Tendencia mensual de ingresos |
| 5 | Ventas por Categoría | Columnas | Ingresos por categoría de producto (top 10) |
| 6 | Top 10 Productos | Tabla | Productos con mayores ingresos |

### Filtros

- **Rango de Fechas** — sobre `orders.created_date` (por defecto, últimos 30 días).
- **País** — sobre `users.country`.

Ambos se conectan a cada tile mediante el parámetro `listen`.

## Requisitos

Este dashboard asume un modelo de Looker llamado `ecommerce` con un explore `orders` y los siguientes campos. Si tu modelo usa otros nombres, ajusta `model`, `explore` y los `fields` de cada tile.

| Vista | Campos usados |
|---|---|
| `orders` | `total_revenue`, `count`, `average_order_value`, `created_date`, `created_month`, `status` |
| `users` | `country` |
| `products` | `category`, `name` |

> El esquema coincide con el dataset de ejemplo de e-commerce de Looker (estilo *thelook*), así que es fácil de reproducir.

## Cómo usarlo

1. Copia el archivo del dashboard a tu proyecto de Looker, junto a tus archivos `.model.lkml` y `.view.lkml`.
2. Inclúyelo en el modelo correspondiente. Lo habitual es usar un comodín en el archivo `.model.lkml`:
   ```lookml
   include: "/dashboards/*.dashboard.lookml"
   ```
3. Ajusta `model`, `explore` y `fields` para que coincidan con tu modelo.
4. Guarda, previsualiza con **View Dashboard** y publica a producción. El dashboard aparecerá en la carpeta **LookML dashboards** del modelo.

Más detalle en la documentación oficial: [Building LookML dashboards](https://cloud.google.com/looker/docs/building-lookml-dashboards).

## Gemini / Conversational Analytics

El icono de chat de Gemini **no** se activa desde el YAML: se habilita a nivel de instancia en *Admin > Gemini in Looker*. Lo único que aporta el código son buenas `description` en el dashboard y en cada tile, que dan contexto al modelo. Los pasos exactos están comentados al inicio de [`ventas_ecommerce.dashboard`](ventas_ecommerce.dashboard).

## Estructura del repo

```
.
├── ventas_ecommerce.dashboard   # Dashboard de ventas e-commerce
├── assets/                      # Capturas de pantalla (añadir)
└── README.md
```

## Roadmap

- [ ] Captura de pantalla del dashboard renderizado
- [ ] Dashboard de retención / cohortes
- [ ] Dashboard de marketing (adquisición y canales)
- [ ] Incluir modelo y vistas de ejemplo para que sea reproducible de principio a fin

## Autor

**Jose Maldonado** — [@joseimj](https://github.com/joseimj)

## Licencia

Distribuido bajo licencia MIT. Consulta el archivo [`LICENSE`](LICENSE) para más información.
