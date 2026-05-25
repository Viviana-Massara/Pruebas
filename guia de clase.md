# Guía de clase — Repaso Front-End

`Tienda de productos` · 

---

## Estructura de la clase


## Bloque 1 — Git y GitHub 

📖 **Lectura antes de los comandos**  
[Git and GitHub Tutorial for Beginners](https://medium.com/@obaff/git-and-github-tutorial-for-beginners-9abae4a530d4) — Medium (octubre 2024)  
Cubre repositorios, commits, branches y el flujo de trabajo completo con ejemplos de comandos en el mismo orden en que se usan en clase.

### Tabla de referencia

| Zona | Comando | Qué hace |
|------|---------|----------|
| Working dir → Staging | `git add archivo` | Prepara el archivo |
| Staging → Local | `git commit -m "msg"` | Guarda el snapshot |
| Local → GitHub | `git push` | Lo sube al repositorio |
| Ver estado | `git status` | ¿Dónde estoy? |
| Ver historial | `git log --oneline` | Historial de commits |

### Comandos 

```bash
git init
git add .
git commit -m "init: estructura del proyecto"
git remote add origin <url-del-repo>
git push -u origin main
```

> A partir de este momento: cada vez que un bloque queda funcional, se hace un commit.

---

## Bloque 2 — HTML semántico

📖 **Lectura antes del código**  
[Semantic HTML Explained](https://youngmayor.medium.com/semantic-html-explained-57a61fb52ec0) — Medium  
Explica la diferencia entre elementos semánticos como `article`, `section` y `main` versus el uso genérico de `div`, con ejemplos de código concretos.

**Mostrar:** estructura HTML de una card de producto.

**Puntos a remarcar:**
- `<section class="productos">` agrupa todas las cards — es una sección temática de la página.
- `<article class="card">` representa un producto individual — tiene sentido por sí solo fuera de contexto.
- `<div>` no dice nada sobre su contenido — `<article>` sí. Eso importa para SEO y accesibilidad.
- La imagen va fuera de `.card-info` para que ocupe todo el ancho de la card.

```html
<section class="productos">

  <article class="card">
    <img src="imagen.jpg" alt="Nombre del producto">
    <div class="card-info">
      <h2>Nombre del producto</h2>
      <p>Descripción breve del producto.</p>
      <span class="precio">$99.99</span>
      <button>Agregar al carrito</button>
    </div>
  </article>

  <!-- Repetir article para cada producto -->

</section>
```

📦 **Commit:**
```bash
git add .
git commit -m "feat: estructura HTML de la card"
```

---

## Bloque 3 — CSS base

📖 **Lectura antes del código**  
[Box Model in CSS](https://medium.com/@Bharat2044/box-model-in-css-5b0993b52a40) — Medium (enero 2024)  
Explica el box model con un ejemplo de card — incluyendo `padding`, `border`, `margin` y `box-sizing: border-box`.

**Mostrar:** estilos base de la card.

**Puntos a remarcar:**
- `box-sizing: border-box` hace que el `padding` no agrande la card — el tamaño declarado es el tamaño final.
- `border-radius` redondea las esquinas — pequeño detalle visual que hace diferencia.
- `box-shadow` da profundidad sin usar imágenes.
- `:hover` en el botón da feedback visual al usuario — buena práctica desde el primer proyecto.
- La imagen con `width: 100%` se adapta al ancho de la card sin deformarse.

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: sans-serif;
  background-color: #f5f5f5;
  padding: 32px;
}

.card {
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  width: 280px;
}

.card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card-info {
  padding: 16px;
}

.card-info h2 {
  font-size: 1.1rem;
  margin-bottom: 8px;
}

.card-info p {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 12px;
}

.precio {
  display: block;
  font-size: 1.2rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 12px;
}

.card-info button {
  width: 100%;
  padding: 10px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

.card-info button:hover {
  background-color: #555;
}
```

📦 **Commit:**
```bash
git add .
git commit -m "feat: estilos base de la card"
```

---

## Bloque 4 — Flexbox

📖 **Lectura antes del código**  
[CSS Flexbox: Beginner's Guide to Layout Magic](https://eleftheriabatsou.medium.com/css-flexbox-beginners-guide-to-layout-magic-4cfd7102add2) — Medium (octubre 2024)  
Incluye un ejemplo directo de card layout con Flexbox — exactamente el caso de uso de la clase.

**Mostrar:** Flexbox aplicado dentro de `.card-info`.

**Puntos a remarcar:**
- Flexbox se usa **dentro de la card** — no para la grilla, eso es Grid.
- `flex-direction: column` apila los elementos verticalmente.
- `flex-grow: 1` en la descripción hace que empuje el precio y el botón hacia abajo — las cards quedan alineadas aunque tengan distinta cantidad de texto.
- Esta es la diferencia clave entre Flexbox (una dimensión) y Grid (dos dimensiones).

```css
.card-info {
  padding: 16px;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.card-info p {
  flex-grow: 1; /* empuja precio y botón al fondo */
}
```

📦 **Commit:**
```bash
git add .
git commit -m "feat: flexbox dentro de la card"
```

---

## Bloque 5 — Grid

📖 **Lectura antes del código**  
[CSS Grid 101: A Beginner's Guide](https://medium.com/@lonesahilnazir/css-grid-101-a-beginners-guide-9a4e106b256f) — Medium (enero 2024)  
Explica grid containers, `grid-template-columns`, la unidad `fr` y cómo usarlos para layouts responsivos.

**Mostrar:** duplicar la card hasta tener 6, aplicar Grid al contenedor.

**Puntos a remarcar:**
- `display: grid` se aplica al contenedor `.productos` — no a las cards.
- `repeat(3, 1fr)` crea 3 columnas que se reparten el espacio disponible en partes iguales.
- `gap` reemplaza los márgenes entre cards — más limpio y preciso.
- La unidad `fr` (fracción) es la clave de los layouts fluidos con Grid.

```css
.productos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  max-width: 1100px;
  margin: 0 auto;
}

.card {
  display: flex;
  flex-direction: column;
}
```

📦 **Commit:**
```bash
git add .
git commit -m "feat: grilla de cards con grid"
```

---

## Bloque 6 — Media Queries 

📖 **Lectura antes del código**  
[Responsive Design Essentials: A Guide to Media Queries](https://medium.com/@akxay/responsive-design-essentials-a-guide-to-media-queries-49109b76e404) — Medium (agosto 2024)  
Cubre breakpoints, sintaxis y ejemplos prácticos de adaptación de layouts a distintos tamaños de pantalla.

**Mostrar:** media queries para tablet y mobile. Abrir el inspector del navegador en vivo.

**Puntos a remarcar:**
- Las media queries no reescriben todo el CSS — solo modifican lo que cambia en ese breakpoint.
- 768px es el breakpoint estándar para tablet, 480px para mobile.
- Mostrar en el inspector cómo la grilla se adapta al redimensionar la ventana — ese momento visual es el más impactante de la clase.
- `meta viewport` en el HTML es obligatorio para que las media queries funcionen en dispositivos reales.

```css
/* Tablet — 2 columnas */
@media (max-width: 768px) {
  .productos {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Mobile — 1 columna */
@media (max-width: 480px) {
  .productos {
    grid-template-columns: 1fr;
  }
}
```

```html
<!-- Agregar dentro del <head> del HTML -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

📦 **Commit:**
```bash
git add .
git commit -m "feat: media queries responsive"
```

---

## Bloque 7 — Prueba

### Prueba 

1. Abrir el inspector del navegador.
2. Activar el modo responsive y probar distintos tamaños de pantalla.
3. Verificar que la grilla pasa de 3 → 2 → 1 columna.
4. Verificar que el botón de cada card tiene hover.
5. Verificar que las cards tienen la misma altura aunque el texto varíe.

### Push final (opcional — para llevar a casa)

```bash
git push origin main
```

### Conexión hacia adelante

| Hoy | Con JavaScript |
|-----|----------------|
| Cards estáticas en HTML | Cards generadas dinámicamente desde un array |
| Botón sin acción | Botón agrega el producto al carrito |
| Precio fijo en HTML | Precio calculado desde datos |
| 6 cards escritas a mano | N cards según los datos disponibles |

> El HTML y CSS que construyeron hoy en JavaScript se vuelve dinámico.