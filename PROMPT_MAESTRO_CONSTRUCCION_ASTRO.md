# Prompt maestro — Construcción del sitio en Astro a partir de la documentación

> **Cuándo usar este prompt:** cuando ya generaste el paquete de seis documentos HTML con el prompt maestro de documentación y quieres que Claude Code construya el sitio siguiéndolos.
>
> **Cómo usarlo:** copia todo lo que está entre `---INICIO---` y `---FIN---`, sustituye los campos marcados entre corchetes, y pégalo como primer mensaje en Claude Code estando ubicado en la raíz de tu carpeta de trabajo.
>
> **Requisito previo:** los seis documentos HTML deben estar accesibles en el disco, junto con el logotipo y cualquier material de origen (catálogos, fotos, listas de precios).

---INICIO---

# Proyecto: construcción del sitio web de [NOMBRE_DE_LA_MARCA]

Eres el desarrollador de este proyecto. Vas a construir el sitio web completo y funcional de **[NOMBRE_DE_LA_MARCA]**, [descripción en una línea: qué vende, a quién y dónde opera].

## Regla número uno

**No escribas textos de relleno.** Nada de "Lorem ipsum", "descripción del producto aquí", "tu texto aquí" ni secciones vacías. Todo el copy debe ser final y publicable, en español, siguiendo el tono de voz definido en el manual de identidad. Si te falta un dato, no lo inventes: anótalo en `PENDIENTES.md` y sigue adelante con lo que sí puedes resolver.

---

## Paso 0 — Lee la documentación antes de escribir una línea de código

En `[RUTA_DE_LA_CARPETA_DE_DOCUMENTOS]` están los documentos que son la **especificación completa** de este proyecto. Léelos todos antes de empezar. Contienen decisiones ya tomadas y validadas por el cliente, no sugerencias.

| Archivo | Qué contiene | Prioridad |
|---|---|---|
| `index.html` | Portal índice, solo navegación | Ignorar |
| `0_Benchmark_*.html` | Contexto de mercado y objetivo del sitio | Leer para entender el porqué |
| `1_Manual_de_Identidad_*.html` | **Colores exactos, tipografías, escala tipográfica, tono de voz, tokens CSS** | Crítico |
| `2_Arquitectura_y_Wireframes_*.html` | **Mapa del sitio, URLs, wireframes de cada pantalla, componentes** | Crítico |
| `3_Plan_de_Contenidos_*.html` | **Artículos a escribir, con título y palabra clave** | Crítico |
| `4_Guia_SEO_y_Medicion_*.html` | **Requisitos SEO, datos estructurados, metadatos** | Crítico |

Los documentos 1, 2 y 4 mandan sobre cualquier criterio propio que tengas. Si el manual dice que un color no se usa como texto, no lo uses. Si el wireframe pone los filtros arriba, van arriba.

**Materiales de origen adicionales** (ajusta esta lista a lo que exista):
- `[CARPETA_CATÁLOGOS]` — catálogos en PDF con precios y descripciones
- `[CARPETA_IMÁGENES]` — fotografías de producto o servicio
- `[ARCHIVO_LOGOTIPO]` — logotipo en alta resolución
- `[ARCHIVO_LISTA]` — lista de precios o inventario

**No modifiques ninguno de estos archivos de origen.** Cópialos si los necesitas.

---

## Paso 1 — Reconcilia los datos antes de construir nada

Cuando la información de producto viene de varias fuentes (un PDF, una hoja de cálculo, la web actual), **casi siempre hay contradicciones**. Resuélvelas antes de construir el catálogo, no durante.

1. Extrae los datos de **todas** las fuentes disponibles por separado.
2. Compara elemento por elemento: nombre, precio por variante, descripción, categoría, disponibilidad.
3. Aplica esta regla de resolución:

   **Regla de precios: ante un conflicto, usa siempre el precio más alto.** La comparación se hace **variante por variante**, no eligiendo una fuente completa. Si una fuente dice tamaño A $80 / tamaño B $130 y otra dice A $70 / B $150, el resultado es **A $80 / B $150**. Es preferible que un precio publicado quede por encima y se ajuste a la baja en la conversación, a que quede por debajo y haya que subirlo frente a un cliente que ya vio otro número.

   **Regla de contenido descriptivo:** usa la fuente más reciente, normalmente el catálogo con fecha más nueva.

   **Regla de cobertura:** si un producto aparece en una fuente y no en otra, **inclúyelo**. Un catálogo incompleto es peor que uno con un elemento por validar.

4. Genera `CONFLICTOS_DE_DATOS.md` en la raíz del proyecto con una tabla: elemento, valor según cada fuente, valor final aplicado y regla usada. Marca las filas con conflicto con ⚠️.
5. Para elementos sin descripción en ninguna fuente, **redáctala tú** siguiendo el patrón y la extensión de las existentes, y márcalos en el archivo de conflictos como "redactado, requiere validación".
6. **Avísame al terminar este paso** para que confirme antes de que sigas.

---

## Paso 2 — Stack y estructura

Crea una carpeta nueva llamada `[nombre-marca]-web/` en la raíz y trabaja ahí dentro.

**Stack:**
- Astro, última versión estable
- Tailwind CSS
- pnpm
- TypeScript
- Sin framework de UI adicional. Astro puro; islas de React o similares solo si algo lo exige de verdad.

```bash
pnpm create astro@latest [nombre-marca]-web
cd [nombre-marca]-web
pnpm astro add tailwind
pnpm add -D @astrojs/sitemap
```

**Estructura base**, adáptala a lo que pida el documento 2:

```
[nombre-marca]-web/
├── public/
│   ├── images/{productos,blog,marca}/
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── layout/      Header, Footer, Nav, y el CTA persistente
│   │   ├── product/     Card, Grid, Filtros, selector de variante
│   │   ├── blog/        ArticleCard, InlineProduct, ArticleHeader
│   │   └── ui/          Button, Badge, TrustStrip, SectionHeading
│   ├── content/
│   │   ├── config.ts
│   │   └── blog/
│   ├── data/
│   │   └── [catalogo].ts
│   ├── layouts/
│   ├── pages/
│   ├── styles/global.css
│   └── utils/
├── astro.config.mjs
├── tailwind.config.mjs
└── README.md
```

---

## Paso 3 — Sistema de diseño

**Extrae los tokens del documento 1**, que trae un bloque de código con las variables CSS listas. Tradúcelas a `tailwind.config.mjs` bajo `theme.extend`. No inventes colores ni tipografías: si no están en el manual, pregúntame.

Reglas que debes respetar y que están en el manual de identidad:

1. La **proporción de uso de color** definida en el manual. Los colores de acento son acentos: no los conviertas en fondos dominantes.
2. Las **restricciones de contraste**. El manual incluye una tabla WCAG con combinaciones aprobadas y rechazadas. Si un color de marca no pasa como texto sobre fondo claro, úsalo solo en bordes, iconos y fondos de botón con texto oscuro encima.
3. La **escala tipográfica** por elemento y punto de ruptura, tal como está tabulada.
4. Los **elementos gráficos característicos** de la marca (marcos, patrones, formas). Son lo que hace que el sitio se vea como la marca y no como una plantilla.
5. Fuentes desde Google Fonts con `preconnect` y `display=swap`.

---

## Paso 4 — Modelo de datos

Crea un archivo de datos tipado en `src/data/` con el catálogo completo. Estructura orientativa, ajústala al negocio:

```ts
export interface Item {
  slug: string;              // 'nombre-marca', minúsculas, sin acentos
  nombre: string;
  categoria: string;
  descripcionCorta: string;  // el formato que use la marca
  descripcionLarga: string;  // 150-300 palabras ORIGINALES
  atributos: Record<string, string | string[]>;  // los ejes de filtrado del doc 2
  variantes: { etiqueta: string; precio: number }[];
  imagen: string;
  destacado: boolean;
}
```

Sobre `descripcionLarga`: escribe entre 150 y 300 palabras **originales** para cada elemento. **No copies las descripciones oficiales del fabricante o proveedor**: genera contenido duplicado y Google lo penaliza. Está explicado en el documento 4.

Los ejes de filtrado salen del documento 2, no de tu criterio.

---

## Paso 5 — Páginas

Construye **exactamente las páginas del mapa del sitio del documento 2**, con **exactamente la estructura de URLs** de su tabla. Las URLs no se improvisan: una vez indexadas, cambiarlas pierde el posicionamiento.

Para cada página, sigue su wireframe: el orden de los bloques, qué contiene cada uno y cuál es la acción principal. Los wireframes están dibujados, no descritos, así que se leen directo.

Presta atención especial a:

- **La página de listado**, que suele ser la más importante. Filtros acumulativos y buscador funcionando **sin recargar la página**, con JavaScript vanilla en el cliente. Contador de resultados visible. Estado vacío con salida hacia el canal de conversión.
- **Las URLs indexables por categoría**, generadas con `getStaticPaths`, además del filtrado dinámico.
- **La página de detalle**, donde el selector de variante debe **actualizar en vivo** el enlace o el mensaje de conversión.
- **Las páginas de apoyo** del mapa del sitio, con contenido real.
- **Una página 404** con salida hacia el listado.

---

## Paso 6 — Blog

Usa Content Collections de Astro.

- **Escribe completos los dos primeros artículos** del calendario del documento 3, con su título y palabra clave exactos, de 800 a 1,200 palabras cada uno, en el tono de la marca.
- Sigue la **anatomía de artículo en 7 pasos** que define el documento 3.
- **Inserta tarjetas de producto dentro del texto** cada vez que se menciona un elemento del catálogo. Es el mecanismo de conversión del blog; sin eso el blog no vende.
- Cada artículo cierra con llamada al canal de conversión.
- **Los artículos restantes del calendario** se crean como entradas con `proximamente: true`: aparecen en el índice del blog como tarjetas atenuadas con la etiqueta "Próximamente", sin página propia ni enlace.

---

## Paso 7 — Conversión

El documento 2 define cuál es el mecanismo de conversión del sitio. **Constrúyelo exactamente ese y no otro.** Si el documento dice que no hay carrito, no construyas carrito.

Si el mecanismo es **WhatsApp**, crea `src/utils/whatsapp.ts`:

```ts
const TELEFONO = '[NÚMERO o PENDIENTE]';

export function linkPedido(nombre: string, variante: string, precio: number) {
  const texto = `Hola, me interesa ${nombre} en ${variante} — $${precio}. ¿Está disponible?`;
  return `https://wa.me/${TELEFONO}?text=${encodeURIComponent(texto)}`;
}

export function linkConsulta(contexto?: string) {
  const texto = contexto ? `Hola, tengo una duda sobre ${contexto}` : 'Hola, tengo una duda';
  return `https://wa.me/${TELEFONO}?text=${encodeURIComponent(texto)}`;
}
```

Implementa el CTA persistente en todas las páginas, el CTA por elemento que se actualiza al cambiar de variante, el cierre de cada artículo del blog y los enlaces del pie.

Si el mecanismo es un **formulario**, constrúyelo con validación en el cliente, estados de carga y error, y protección anti-spam. Si es **reserva de cita**, integra el servicio que indique el documento.

Cualquier credencial, número o endpoint que no tengas, déjalo como constante claramente marcada como pendiente y anótalo en `PENDIENTES.md`.

---

## Paso 8 — SEO

Implementa **todo** lo del documento 4. Como mínimo:

- `<title>` único por página, 50-60 caracteres, palabra clave al inicio
- Meta descripción única, 140-155 caracteres
- Open Graph y Twitter Card en todas las páginas
- Una sola `<h1>` por página
- URLs limpias, minúsculas, sin acentos
- `sitemap.xml` con `@astrojs/sitemap` y `robots.txt` enlazándolo
- Imágenes en WebP, `loading="lazy"`, texto alternativo descriptivo y específico
- **JSON-LD**: los bloques del documento 4 están listos para copiar. Aplica el de producto o servicio en cada detalle, el de negocio en inicio y contacto, y el de artículo en cada entrada del blog
- Canonical en todas las páginas
- Atributo de idioma correcto

Si el negocio es local, incluye las señales locales que indica el documento 4: ciudad en los títulos donde tenga sentido, mapa embebido en contacto y coherencia de datos con el perfil de Google Business.

---

## Paso 9 — Rendimiento y accesibilidad

- LCP por debajo de 2.5 segundos en móvil
- JavaScript al cliente solo el imprescindible: filtros y selector de variante
- Optimiza las imágenes con `astro:assets`, convierte a WebP, genera tamaños responsivos
- Áreas táctiles de 44 px mínimo
- Navegación completa por teclado con foco visible
- Contraste WCAG AA en todo el texto
- Móvil primero: diseña a 375 px y expande

---

## Paso 10 — Entregables

Al terminar genera:

1. **`README.md`**: instalación, desarrollo, compilación, cómo agregar un elemento al catálogo, cómo agregar un artículo al blog, cómo publicar.
2. **`CONFLICTOS_DE_DATOS.md`**: tabla de discrepancias, valor final y regla aplicada.
3. **`PENDIENTES.md`**: todo lo que necesitas del cliente, todo lo que asumiste y todo lo que quedó marcado como provisional.

Verifica que `pnpm build` compile **sin errores ni advertencias** antes de darlo por terminado.

---

## Cómo quiero que trabajes

Ve por fases y **detente al final de cada una para mostrarme el resultado** antes de seguir:

1. Lectura de documentos y reconciliación de datos → muéstrame el archivo de catálogo y el de conflictos
2. Setup y sistema de diseño → muéstrame la config de Tailwind y un componente de ejemplo
3. Componentes base y layout
4. Inicio y listado
5. Páginas de detalle
6. Blog con los dos artículos escritos
7. Páginas de apoyo, SEO y optimización

**Pregúntame siempre que:**
- La documentación se contradiga entre documentos
- Falte un dato que no puedas deducir con seguridad (número de contacto, dirección, credenciales)
- Un wireframe sea ambiguo sobre un comportamiento concreto
- Encuentres un conflicto de datos que la regla del precio más alto no resuelva
- Creas que una decisión de la documentación es un error técnico

Prefiero responder tres preguntas que corregir un sitio entero.

---FIN---

---

## Notas de uso

**Campos a sustituir antes de pegarlo:**

| Campo | Ejemplo |
|---|---|
| `[NOMBRE_DE_LA_MARCA]` | Decanto Selecto |
| Descripción de una línea | tienda de decants de perfumes originales en Pachuca |
| `[RUTA_DE_LA_CARPETA_DE_DOCUMENTOS]` | `propuesta web/` |
| `[CARPETA_CATÁLOGOS]`, `[CARPETA_IMÁGENES]`, etc. | ajusta o elimina las que no existan |
| `[nombre-marca]-web` | `decanto-selecto-web` |
| `[NÚMERO o PENDIENTE]` | el número real o déjalo como pendiente |

**Si el stack cambia.** Sustituye el paso 2 completo. El resto del prompt es independiente de la tecnología, salvo las referencias a Content Collections del paso 6 y a `astro:assets` del paso 9.

**Si no hay conflictos de datos** porque la fuente es única, el paso 1 se resuelve solo y el archivo de conflictos queda vacío. Déjalo de todas formas: sirve como constancia de que se revisó.

**Sobre la regla del precio más alto.** Protege contra el error caro, que es cobrar de menos. Pero si los precios más bajos venían de una rebaja intencional, publicar los altos sube precios sin querer. Por eso el paso 1 termina con una parada: revisa `CONFLICTOS_DE_DATOS.md` antes de dar luz verde.

**Encadenamiento completo del flujo:**

1. Prompt maestro de documentación + URL → seis documentos HTML
2. Este prompt + los documentos → sitio construido en Astro
3. Opcional: pedir a Claude Code un prompt de despliegue y analítica → sitio en producción con medición activa
