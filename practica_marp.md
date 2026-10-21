# Práctica guiada: Creación de presentaciones con Marp y Markdown

**Curso de especialización**
**Tipo de actividad:** Práctica guiada individual
**Herramientas:** Visual Studio Code, extensión *Marp for VS Code*, navegador web

---

## Índice

1. Objetivos de aprendizaje
2. Introducción: ¿qué es Marp y cómo funciona?
3. Preparación del entorno de trabajo
4. Fase 1 — Primera presentación
5. Fase 2 — Directivas globales y locales
6. Fase 3 — Imágenes, fondos y maquetación
7. Fase 4 — Estilos CSS dentro del documento
8. Fase 5 — Creación de un tema propio en un archivo externo
9. Fase 6 — Visualización y exportación desde VS Code
10. Ejercicio final y entregables
11. Criterios de evaluación
12. Anexo A — Referencia rápida
13. Anexo B — Resolución de problemas frecuentes

---

## 1. Objetivos de aprendizaje

Al finalizar esta práctica, el alumnado será capaz de:

- Comprender el funcionamiento de Marp y su relación con el lenguaje Markdown.
- Estructurar una presentación en diapositivas a partir de un único archivo `.md`.
- Aplicar directivas globales y locales para controlar la apariencia y el comportamiento de las diapositivas.
- Insertar y maquetar imágenes, incluidas imágenes de fondo y composiciones a dos columnas.
- Definir estilos CSS tanto dentro del documento como en un archivo de tema externo.
- Registrar y utilizar un tema personalizado en Visual Studio Code.
- Previsualizar la presentación en tiempo real y exportarla a formatos HTML, PDF y PPTX.

---

## 2. Introducción: ¿qué es Marp y cómo funciona?

### 2.1 Definición

**Marp** (*Markdown Presentation Ecosystem*) es un conjunto de herramientas de código abierto que permite crear presentaciones de diapositivas escribiendo exclusivamente texto en formato Markdown. El autor se concentra en el contenido, mientras que Marp se encarga de transformar ese texto en diapositivas con un diseño coherente.

### 2.2 Principio de funcionamiento

El proceso de trabajo con Marp se resume en tres etapas:

1. **Redacción:** se escribe un archivo `.md` con sintaxis Markdown estándar (títulos, listas, imágenes, tablas, bloques de código…).
2. **Interpretación:** Marp analiza el archivo, divide el contenido en diapositivas y aplica un **tema** (una hoja de estilos CSS).
3. **Renderizado y exportación:** el resultado se muestra como una presentación que puede exportarse a HTML, PDF, PowerPoint (PPTX) o imágenes.

Internamente, cada diapositiva se convierte en un elemento HTML `<section>`. Este dato es fundamental, ya que permite aplicar estilos CSS a las diapositivas como si se tratara de una página web.

### 2.3 Ventajas frente a las herramientas tradicionales

| Aspecto | Herramientas tradicionales (PowerPoint, Impress…) | Marp |
|---|---|---|
| Formato del archivo | Binario o XML complejo | Texto plano (`.md`) |
| Control de versiones (Git) | Difícil de comparar cambios | Totalmente compatible |
| Coherencia visual | Depende del cuidado del autor | Garantizada por el tema |
| Reutilización de estilos | Plantillas propietarias | Hojas de estilo CSS estándar |
| Edición | Requiere el programa específico | Cualquier editor de texto |

### 2.4 Componentes del ecosistema

- **Marpit:** el motor base que convierte Markdown en diapositivas.
- **Marp Core:** amplía Marpit con temas predefinidos, fórmulas matemáticas, emojis, etc.
- **Marp for VS Code:** extensión que integra la vista previa y la exportación en el editor. **Es la herramienta que se utilizará en esta práctica.**
- **Marp CLI:** herramienta de línea de comandos para convertir presentaciones de forma automatizada.

### 2.5 Elementos relevantes de un documento Marp

Antes de comenzar, conviene conocer los cuatro elementos sobre los que se construye cualquier presentación:

| Elemento | Función | Ejemplo |
|---|---|---|
| **Front-matter** | Bloque YAML inicial que activa Marp y define opciones globales | `marp: true` |
| **Separador de diapositivas** | Línea con tres guiones que marca el inicio de una nueva diapositiva | `---` |
| **Directivas** | Instrucciones que modifican el aspecto o comportamiento | `<!-- paginate: true -->` |
| **Temas y estilos** | Reglas CSS que definen el diseño visual | `theme: gaia` |

---

## 3. Preparación del entorno de trabajo

### 3.1 Instalación de Visual Studio Code

Si no se dispone de él, descargue e instale Visual Studio Code desde su web oficial (<https://code.visualstudio.com>).

### 3.2 Instalación de la extensión Marp for VS Code

1. Abra Visual Studio Code.
2. Acceda al panel de **Extensiones** (icono de cuadrados en la barra lateral, o `Ctrl + Shift + X`).
3. Busque **Marp for VS Code** (publicada por *Marp team*).
4. Pulse **Instalar**.

> **Nota:** para exportar a PDF y PPTX, la extensión necesita un navegador basado en Chromium (Google Chrome, Microsoft Edge) o Firefox instalado en el equipo.

### 3.3 Estructura de carpetas del proyecto

Cree una carpeta de trabajo llamada `practica-marp` con la siguiente estructura:

```
practica-marp/
├── presentacion.md
├── img/
│   └── (imágenes que utilizará en la presentación)
├── themes/
│   └── (archivos CSS de temas propios)
└── .vscode/
    └── settings.json
```

Abra la carpeta completa en VS Code mediante **Archivo → Abrir carpeta…**. Es importante abrir la carpeta, y no solo el archivo, para que la configuración del proyecto (`.vscode/settings.json`) se aplique correctamente.

**✅ Comprobación:** en el explorador de VS Code se muestra la estructura de carpetas indicada.

---

## 4. Fase 1 — Primera presentación

### 4.1 Activar Marp en el documento

Abra `presentacion.md` y escriba el siguiente contenido:

```markdown
---
marp: true
---

# Introducción a Marp

Presentación de prueba

---

## ¿Qué es Marp?

Una herramienta para crear presentaciones a partir de Markdown.

---

## Ventajas

- Texto plano
- Compatible con Git
- Diseño coherente
```

**Explicación:**

- El bloque delimitado por `---` al inicio del archivo es el **front-matter**. La línea `marp: true` es obligatoria: indica a la extensión que el documento debe tratarse como una presentación.
- Cada `---` posterior **separa una diapositiva** de la siguiente.
- El resto es Markdown convencional.

### 4.2 Abrir la vista previa

Pulse `Ctrl + K` y, a continuación, `V` (o el icono de vista previa en la esquina superior derecha del editor). Se abrirá un panel lateral con las diapositivas renderizadas que se actualiza automáticamente al escribir.

**✅ Comprobación:** la vista previa muestra tres diapositivas en lugar de un documento continuo. Si se muestra como texto normal, revise que `marp: true` esté escrito correctamente.

### 4.3 Elementos de Markdown admitidos

Añada una nueva diapositiva que incluya los siguientes elementos, para comprobar cómo los representa Marp:

````markdown
---

## Elementos de Markdown

Texto en **negrita**, en *cursiva* y `código en línea`.

| Lenguaje | Tipo |
|---|---|
| Python | Interpretado |
| C | Compilado |

```python
def saludar(nombre):
    return f"Hola, {nombre}"
```

> Esto es una cita destacada.
````

**✅ Comprobación:** la tabla, el bloque de código (con resaltado de sintaxis) y la cita se visualizan correctamente.

---

## 5. Fase 2 — Directivas globales y locales

Las **directivas** son instrucciones que controlan el aspecto y el comportamiento de las diapositivas. Existen dos tipos.

### 5.1 Directivas globales

Afectan a toda la presentación y se escriben en el front-matter. Modifique el inicio de su archivo:

```markdown
---
marp: true
theme: default
size: 16:9
paginate: true
header: 'Curso de especialización'
footer: 'Práctica de Marp'
---
```

| Directiva | Función | Valores habituales |
|---|---|---|
| `theme` | Tema visual | `default`, `gaia`, `uncover` o un tema propio |
| `size` | Proporción de la diapositiva | `16:9`, `4:3` |
| `paginate` | Muestra el número de diapositiva | `true`, `false` |
| `header` | Texto en la cabecera | Cualquier texto |
| `footer` | Texto en el pie | Cualquier texto |

**Actividad 5.1:** cambie el valor de `theme` entre `default`, `gaia` y `uncover`, y observe las diferencias en la vista previa. Anote cuál le parece más adecuado para una presentación académica y por qué.

### 5.2 Directivas locales

Se aplican desde la diapositiva en la que se escriben **en adelante**. Se escriben como comentarios HTML:

```markdown
---

<!-- backgroundColor: #1e1e2e -->
<!-- color: white -->

## Diapositiva con fondo oscuro
```

Observe que, a partir de esta diapositiva, **todas las siguientes** heredan el fondo oscuro.

### 5.3 Directivas de ámbito puntual (prefijo `_`)

Si se antepone un guion bajo al nombre de la directiva, esta afecta **únicamente a la diapositiva actual**:

```markdown
---

<!-- _backgroundColor: #e63946 -->
<!-- _color: white -->
<!-- _paginate: false -->

# Sección 2
```

**Actividad 5.2:** cree una diapositiva de "separador de sección" con fondo de color, sin numeración y sin cabecera (`<!-- _header: '' -->`), y compruebe que la diapositiva siguiente recupera el aspecto normal.

### 5.4 Notas del presentador

Cualquier comentario HTML que **no** sea una directiva se interpreta como nota del presentador. No aparece en la diapositiva, pero se conserva en la exportación HTML y PPTX:

```markdown
## Resultados

<!-- Recordar explicar la metodología antes de mostrar los datos. -->
```

**✅ Comprobación:** la presentación muestra numeración, cabecera y pie; las diapositivas de sección tienen un aspecto diferenciado.

---

## 6. Fase 3 — Imágenes, fondos y maquetación

Copie al menos dos imágenes en la carpeta `img/` antes de comenzar esta fase.

### 6.1 Redimensionar imágenes

Marp amplía la sintaxis de imágenes de Markdown mediante palabras clave en el texto alternativo:

```markdown
![width:400px](img/foto1.jpg)
![height:200px](img/foto1.jpg)
![w:300 h:200](img/foto1.jpg)
```

### 6.2 Imágenes de fondo

La palabra clave `bg` convierte una imagen en fondo de la diapositiva:

```markdown
---

![bg](img/foto1.jpg)

# Título sobre la imagen
```

Variantes de ajuste:

| Sintaxis | Efecto |
|---|---|
| `![bg cover](...)` | Cubre toda la diapositiva (valor por defecto) |
| `![bg contain](...)` | La imagen completa cabe dentro de la diapositiva |
| `![bg 50%](...)` | Escala la imagen al porcentaje indicado |

### 6.3 Filtros de imagen

Pueden añadirse filtros visuales, útiles para mejorar la legibilidad del texto superpuesto:

```markdown
![bg brightness:0.4](img/foto1.jpg)
![bg blur:3px](img/foto1.jpg)
![bg grayscale](img/foto1.jpg)
![bg sepia](img/foto1.jpg)
```

### 6.4 Composición a dos columnas (imagen y texto)

Una de las funciones más útiles de Marp es dividir la diapositiva colocando el fondo en un lateral:

```markdown
---

![bg left:40%](img/foto1.jpg)

## Imagen a la izquierda

- El texto ocupa el espacio restante.
- Ideal para explicar un concepto visual.
```

Sustituya `left` por `right` para invertir la disposición.

### 6.5 Varias imágenes de fondo

Si se incluyen varias imágenes `bg` en la misma diapositiva, se distribuyen en horizontal. Con la palabra clave `vertical` se apilan en vertical:

```markdown
![bg](img/foto1.jpg)
![bg](img/foto2.jpg)
```

**Actividad 6.1:** cree una diapositiva de portada con imagen de fondo oscurecida (`brightness`) y el título en color blanco, y otra diapositiva con la composición imagen-texto a dos columnas.

**✅ Comprobación:** las imágenes se cargan correctamente (las rutas son relativas al archivo `.md`) y el texto es legible.

---

## 7. Fase 4 — Estilos CSS dentro del documento

Como se indicó en la introducción, cada diapositiva es un elemento `<section>`. Por tanto, su apariencia puede modificarse con CSS estándar.

### 7.1 Estilos globales con la etiqueta `<style>`

Añada el siguiente bloque justo después del front-matter:

```markdown
<style>
section {
  font-family: 'Segoe UI', Arial, sans-serif;
  font-size: 28px;
}

h1 {
  color: #1d3557;
}

h2 {
  color: #457b9d;
  border-bottom: 3px solid #457b9d;
}

em {
  color: #e63946;
  font-style: normal;
}
</style>
```

Estos estilos se aplican a **todas** las diapositivas.

### 7.2 Correspondencia entre Markdown y etiquetas HTML

Para dar estilo a un elemento es necesario conocer la etiqueta HTML que genera:

| Markdown | Etiqueta HTML | Selector CSS |
|---|---|---|
| `# Título` | `<h1>` | `h1` |
| `*cursiva*` | `<em>` | `em` |
| `**negrita**` | `<strong>` | `strong` |
| `` `código` `` | `<code>` | `code` |
| `> cita` | `<blockquote>` | `blockquote` |
| `- elemento` | `<ul><li>` | `ul`, `li` |
| Tabla | `<table>` | `table`, `th`, `td` |
| Diapositiva | `<section>` | `section` |
| Cabecera / pie | `<header>` / `<footer>` | `header`, `footer` |

### 7.3 Estilos de una sola diapositiva con `<style scoped>`

El atributo `scoped` limita los estilos a la diapositiva en la que se encuentra el bloque:

```markdown
---

<style scoped>
h2 {
  color: #2a9d8f;
  text-align: center;
}
</style>

## Este título solo cambia aquí
```

### 7.4 Clases personalizadas

La directiva `class` asigna una clase CSS a la diapositiva, que después puede usarse como selector:

```markdown
<style>
section.destacada {
  background: #f1faee;
  text-align: center;
  justify-content: center;
}
</style>

---

<!-- _class: destacada -->

# Idea clave
```

**Actividad 7.1:** defina dos clases propias (por ejemplo, `portada` y `cierre`) y aplíquelas a la primera y a la última diapositiva.

**✅ Comprobación:** los estilos globales afectan a todas las diapositivas; los estilos `scoped` y las clases solo a las diapositivas indicadas.

---

## 8. Fase 5 — Creación de un tema propio en un archivo externo

Incluir el CSS dentro del documento es práctico para ajustes puntuales, pero cuando los estilos se quieren **reutilizar en varias presentaciones** lo adecuado es definirlos en un archivo independiente. En Marp, este archivo recibe el nombre de **tema**.

> **Importante:** en Marp no se enlaza un CSS externo mediante una etiqueta `<link>`, como en una página web. El archivo CSS se declara como tema y se registra en la configuración del editor.

### 8.1 Crear el archivo del tema

Cree el archivo `themes/curso.css` con el siguiente contenido:

```css
/* @theme curso */

@import 'default';

section {
  font-family: 'Segoe UI', Arial, sans-serif;
  background: #ffffff;
  color: #222222;
  padding: 60px;
}

h1 {
  color: #1d3557;
  font-size: 56px;
}

h2 {
  color: #457b9d;
  border-bottom: 3px solid #a8dadc;
  padding-bottom: 8px;
}

em {
  color: #e63946;
  font-style: normal;
}

header,
footer {
  color: #888888;
  font-size: 18px;
}

/* Numeración de página */
section::after {
  color: #457b9d;
  font-weight: bold;
}

/* Clase para la portada */
section.portada {
  background: #1d3557;
  color: #ffffff;
  justify-content: center;
}

section.portada h1 {
  color: #ffffff;
}

/* Clase para separadores de sección */
section.seccion {
  background: #457b9d;
  color: #ffffff;
  justify-content: center;
  text-align: center;
}

section.seccion h1 {
  color: #ffffff;
}
```

**Explicación de los elementos clave:**

- `/* @theme curso */` — **comentario obligatorio**. Define el nombre con el que se identificará el tema. Sin él, Marp no reconoce el archivo como tema.
- `@import 'default';` — hereda todos los estilos de un tema base (`default`, `gaia` o `uncover`), de forma que solo es necesario definir las diferencias.
- `section::after` — pseudo-elemento que Marp utiliza para mostrar el número de página.

### 8.2 Registrar el tema en VS Code

Cree o edite el archivo `.vscode/settings.json`:

```json
{
  "markdown.marp.themes": [
    "./themes/curso.css"
  ]
}
```

La ruta es relativa a la carpeta del proyecto. Pueden registrarse varios temas añadiendo más elementos a la lista.

> **Alternativa:** también puede configurarse desde **Archivo → Preferencias → Configuración**, buscando `marp themes`, preferiblemente en la pestaña **Área de trabajo** para que la configuración quede asociada al proyecto.

### 8.3 Aplicar el tema en la presentación

En el front-matter, indique el **nombre del tema** (el declarado en `@theme`), no la ruta del archivo:

```markdown
---
marp: true
theme: curso
paginate: true
---

<!-- _class: portada -->

# Introducción a Marp

Curso de especialización

---

<!-- _class: seccion -->

# 1. Conceptos básicos
```

**Actividad 8.1:** elimine el bloque `<style>` creado en la Fase 4 y traslade todos sus estilos al tema `curso.css`. Compruebe que la presentación mantiene el mismo aspecto.

**Actividad 8.2:** cree un segundo tema, `themes/oscuro.css`, basado en `@import 'gaia';`, regístrelo en `settings.json` y alterne entre ambos temas cambiando únicamente la directiva `theme`.

**✅ Comprobación:** al cambiar el valor de `theme` en el front-matter, la vista previa aplica el tema correspondiente. Si aparece un aviso indicando que el tema no se reconoce, consulte el Anexo B.

### 8.4 Combinación de tema externo y estilos locales

Ambos enfoques son compatibles: el tema externo define el diseño general y el bloque `<style>` del documento permite ajustes específicos de una presentación concreta. Los estilos del documento tienen prioridad sobre los del tema.

---

## 9. Fase 6 — Visualización y exportación desde VS Code

### 9.1 Vista previa

| Acción | Procedimiento |
|---|---|
| Abrir vista previa lateral | `Ctrl + K` y después `V` |
| Abrir vista previa en la misma pestaña | `Ctrl + Shift + V` |

La vista previa se actualiza en tiempo real al guardar o editar el archivo.

### 9.2 Exportar la presentación

1. Con `presentacion.md` abierto, pulse el **icono de Marp** situado en la parte superior derecha del editor.
2. Seleccione **Export Slide Deck…**
   (También puede accederse desde la paleta de comandos, `Ctrl + Shift + P`, escribiendo `Marp: Export Slide Deck`.)
3. Elija el formato y la ubicación del archivo.

| Formato | Uso recomendado |
|---|---|
| **HTML** | Presentar desde el navegador; conserva notas del presentador y navegación |
| **PDF** | Distribución y entrega de documentos; formato universal |
| **PPTX** | Compartir con usuarios de PowerPoint (las diapositivas se insertan como imágenes, por lo que el texto no es editable) |
| **PNG / JPEG** | Exportar diapositivas individuales como imagen |

### 9.3 Presentar desde el archivo HTML

Abra el archivo HTML exportado en el navegador. Puede navegar con las flechas del teclado y activar la pantalla completa con `F11`.

**Actividad 9.1:** exporte la presentación a HTML y a PDF. Compruebe que las imágenes, el tema personalizado y la numeración se conservan en ambos formatos.

**✅ Comprobación:** se dispone de los archivos `presentacion.html` y `presentacion.pdf` con el diseño correcto.

---

## 10. Ejercicio final y entregables

### 10.1 Enunciado

Elabore una presentación de **entre 5 y 8 diapositivas** sobre ti mismo (de donde vienes, que has hecho hasta llegar aquí, hobbies, intereses, anecdotas personales...). La presentación debe cumplir los siguientes requisitos:

1. Utilizar un **tema propio** definido en un archivo CSS externo y registrado en VS Code.
2. Incluir una **portada** y una **diapositiva de cierre** con clases CSS diferenciadas.
3. Incluir al menos **dos diapositivas de separación de sección**.
4. Mostrar **numeración** de página, **cabecera** y **pie**, ocultándolos donde no proceda (portada y separadores).
5. Incluir al menos **una imagen de fondo** con filtro y **una composición imagen-texto** a dos columnas.
6. Incluir al menos **una tabla** y **un bloque de código**.
7. Contener **notas del presentador** en, al menos, tres diapositivas.
8. Utilizar al menos **un bloque `<style scoped>`**.

### 10.2 Entregables

Crea un repositorio en github con el nombre CECIB-HE-XXX-UD0-marp. XXX hace referencia a las siglas de tu nombre y apellidos. El repositorio debe contener:

- `presentacion.md`
- La carpeta `themes/` con el tema o temas creados.
- La carpeta `img/` con las imágenes utilizadas.
- La carpeta `.vscode/` con el archivo `settings.json`.
- La presentación exportada en formato **PDF** y **HTML**.

---
---

## 12. Anexo A — Referencia rápida

### Estructura mínima

```markdown
---
marp: true
theme: default
paginate: true
---

# Diapositiva 1

---

# Diapositiva 2
```

### Directivas

| Directiva | Tipo | Ejemplo |
|---|---|---|
| `marp` | Global | `marp: true` |
| `theme` | Global | `theme: curso` |
| `size` | Global | `size: 16:9` |
| `paginate` | Local | `<!-- paginate: true -->` |
| `header` / `footer` | Local | `<!-- footer: 'Texto' -->` |
| `class` | Local | `<!-- _class: portada -->` |
| `backgroundColor` | Local | `<!-- _backgroundColor: #000 -->` |
| `color` | Local | `<!-- color: white -->` |
| `backgroundImage` | Local | `<!-- backgroundImage: url('img/fondo.jpg') -->` |

> Recordatorio: sin prefijo, la directiva local se aplica desde esa diapositiva en adelante; con el prefijo `_`, solo a la diapositiva actual.

### Imágenes

| Sintaxis | Resultado |
|---|---|
| `![width:300px](img.jpg)` | Ancho fijo |
| `![bg](img.jpg)` | Imagen de fondo |
| `![bg contain](img.jpg)` | Fondo completo sin recortar |
| `![bg left:40%](img.jpg)` | Fondo en el 40 % izquierdo |
| `![bg right](img.jpg)` | Fondo en la mitad derecha |
| `![bg brightness:0.5](img.jpg)` | Fondo oscurecido |
| `![bg blur:4px](img.jpg)` | Fondo desenfocado |

### Plantilla de tema

```css
/* @theme nombre-del-tema */

@import 'default';

section { }
h1 { }
h2 { }
section.portada { }
```

---

## 13. Anexo B — Resolución de problemas frecuentes

| Problema | Causa probable | Solución |
|---|---|---|
| La vista previa muestra un documento normal y no diapositivas | Falta `marp: true` o está mal escrito | Revise el front-matter |
| El tema propio no se aplica | El nombre en `theme:` no coincide con el de `/* @theme */` | Use exactamente el mismo nombre |
| El tema propio no se reconoce | El tema no está registrado o la ruta es incorrecta | Revise `markdown.marp.themes` en `.vscode/settings.json` y que la carpeta del proyecto esté abierta en VS Code |
| Los cambios en el CSS no se reflejan | La vista previa no se ha recargado | Guarde el CSS y cierre y vuelva a abrir la vista previa |
| Las imágenes no aparecen | Ruta incorrecta | Las rutas son relativas al archivo `.md`; compruebe mayúsculas y extensión |
| No se puede exportar a PDF o PPTX | No hay navegador compatible instalado | Instale Google Chrome, Microsoft Edge o Firefox |
| Una directiva afecta a más diapositivas de las deseadas | Falta el prefijo `_` | Use `<!-- _directiva: valor -->` |
| Aparece una diapositiva vacía al principio | Hay contenido o líneas en blanco antes del front-matter | El primer `---` debe estar en la primera línea del archivo |

---

*Documentación oficial de referencia: <https://marp.app> y <https://marpit.marp.app>*
