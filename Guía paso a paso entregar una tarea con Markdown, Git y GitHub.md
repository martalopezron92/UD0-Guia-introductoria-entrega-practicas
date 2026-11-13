# Guía paso a paso: entregar una tarea con Markdown, Git y GitHub

Sigue los 10 pasos en orden: al terminar tendrás tu tarea en GitHub y el enlace entregado en Moodle. Trabajarás siempre con la carpeta abierta en Visual Studio Code y escribiendo los comandos de Git en su terminal. Usa primero la guía rápida; si no recuerdas cómo se hace algo, cada paso está explicado en detalle más abajo.

## Guía rápida

1. **Carpeta:** crea con el explorador de archivos una carpeta llamada `nombre-tarea` (fuera de cualquier otro repositorio) y ábrela en VS Code con *Archivo > Abrir carpeta*. Abre la terminal (*Terminal > Nuevo terminal*) y comprueba que `git status` responde `fatal: not a git repository`.
2. **GitHub:** crea un repositorio nuevo con el mismo nombre, **público** y **vacío** (sin README).
3. **Conectar:** en la terminal de VS Code: `git init`, `git branch -M main`, `git remote add origin https://github.com/TU_USUARIO/nombre-tarea.git`. Comprueba con `git remote -v`.
4. **Enunciado:** descarga el `.md` (de Moodle, o del repositorio de la profesora con el botón *Download raw file*) y guárdalo en la carpeta.
5. **Primer commit:** `git add .` y `git commit -m "Añado el enunciado de la tarea"`.
6. **Primer push:** `git push -u origin main`. Comprueba en GitHub que aparece el archivo.
7. **Trabajo:** completa la tarea en ese mismo archivo `.md`.
8. **Entrega en GitHub:** guarda (Control + S), `git add .`, `git commit -m "Completo la tarea"`, `git push`.
9. **Revisión:** recarga tu repositorio en GitHub y comprueba que se ven tus respuestas.
10. **Moodle:** botón verde *Code* > copia el enlace HTTPS > pégalo en un archivo `.txt` > adjúntalo en la tarea de Moodle.

---

# Explicación detallada de cada paso

## Antes de empezar

Necesitas tres cosas preparadas una sola vez (si ya las tienes de otras tareas, salta al Paso 1):

- **Git instalado** en tu ordenador. En Windows instala [Git for Windows](https://git-scm.com/download/win), que incluye la terminal **Git Bash**.
- **Una cuenta en GitHub** ([github.com](https://github.com)) con la que hayas iniciado sesión.
- **Visual Studio Code** instalado ([code.visualstudio.com](https://code.visualstudio.com)).

**La terminal de VS Code.** Todos los comandos de esta guía se escriben en la terminal integrada de Visual Studio Code y se ejecutan pulsando Enter:

- Para abrirla: menú **Terminal > Nuevo terminal** (*Terminal > New Terminal*). Atajo: Control + ñ en teclado español (Control + \` en otros teclados).
- Aparece en la parte inferior de la ventana y se sitúa automáticamente en la carpeta que tengas abierta en VS Code.
- **En Windows, usa Git Bash dentro de VS Code:** en el panel de la terminal pulsa la flecha junto al botón **+** y elige **Git Bash**. Para que sea siempre la opción por defecto: Control + Shift + P, escribe `Terminal: Select Default Profile` y elige **Git Bash**. (En macOS y Linux no hay que cambiar nada.)

**Comprueba que Git funciona.** Abre VS Code, abre la terminal y escribe:

```bash
git --version
```

Debe aparecer algo como `git version 2.47.0`. Si aparece "command not found" o "no se reconoce", Git no está instalado (o hay que cerrar y volver a abrir VS Code después de instalarlo).

**Configura tu nombre y correo (solo la primera vez).** Usa el mismo correo de tu cuenta de GitHub:

```bash
git config --global user.name "Nombre Apellido"
git config --global user.email "tu_correo@ejemplo.com"
```

Comprueba que se ha guardado con `git config --global --list`.

> Convención de esta guía: donde ponga `nombre-tarea` escribe el nombre real de tu tarea (por ejemplo `practica-markdown-01`), y donde ponga `TU_USUARIO` escribe tu usuario de GitHub. Usa nombres sin espacios, sin tildes y sin ñ: separa las palabras con guiones.

## Paso 1. Crear la carpeta de la tarea y abrirla en VS Code

Crea una carpeta nueva con el nombre de la tarea, en un lugar que **no** esté dentro de otro repositorio de Git, y ábrela en Visual Studio Code.

1. **Crea la carpeta con el explorador de archivos** (Explorador de archivos en Windows, Finder en Mac):
   - Ve a la carpeta donde guardas tus trabajos, por ejemplo **Documentos**.
   - Clic derecho en un espacio vacío > **Nuevo > Carpeta** (en Mac: **Nueva carpeta**).
   - Llámala exactamente `nombre-tarea`.
   - No la crees dentro de la carpeta de otra práctica o tarea anterior: esas carpetas ya son repositorios de Git.
2. **Abre la carpeta en VS Code:**
   - Abre Visual Studio Code.
   - Menú **Archivo > Abrir carpeta...** (*File > Open Folder...*), busca `nombre-tarea`, selecciónala y pulsa **Seleccionar carpeta** (en Mac, **Abrir**).
   - Si VS Code pregunta si confías en los autores de los archivos, pulsa **Sí, confío en los autores**.
   - Comprueba que en el panel **Explorador** (barra lateral izquierda) aparece arriba el nombre `NOMBRE-TAREA` y que está vacío.

   > Atajo en Windows: clic derecho sobre la carpeta > **Abrir con Code**.
3. **Abre la terminal de VS Code:** menú **Terminal > Nuevo terminal**. Comprueba que la terminal está en tu carpeta escribiendo:

   ```bash
   pwd
   ```

   La ruta que aparece debe terminar en `/nombre-tarea`.
4. **Comprueba que la carpeta NO está dentro de otro repositorio de Git:**

   ```bash
   git status
   ```
   - Si aparece `fatal: not a git repository` (o "no es un repositorio git"): **correcto**, puedes seguir.
   - Si aparece `On branch ...` o una lista de archivos: la carpeta está dentro de un repositorio. Cierra la carpeta en VS Code (**Archivo > Cerrar carpeta**), borra la carpeta, créala en otro sitio (por ejemplo directamente en Documentos o en el Escritorio) y repite este paso.

   Comprobación visual extra: pulsa el icono de **Control de código fuente** en la barra lateral izquierda (Control + Shift + G). Si ves el botón **Inicializar repositorio**, la carpeta no es un repositorio: **no lo pulses**, lo haremos con un comando en el Paso 3. Si en cambio aparecen archivos o el nombre de un repositorio, estás dentro de otro repositorio.
5. **Comprueba que la carpeta está vacía:**

   ```bash
   ls -a
   ```

   Solo deben aparecer `.` y `..`. Si aparece una carpeta `.git`, algo ha ido mal: cierra la carpeta en VS Code, bórrala y vuelve a empezar este paso.

> A partir de aquí, trabaja siempre con esta carpeta abierta en VS Code. Si cierras VS Code, al volver abre otra vez la carpeta con **Archivo > Abrir carpeta** (o **Archivo > Abrir reciente**) antes de escribir ningún comando.

## Paso 2. Crear el repositorio en GitHub (remoto)

Crea en GitHub un repositorio **vacío** con exactamente el mismo nombre que tu carpeta local.

1. Entra en [github.com](https://github.com) e inicia sesión.
2. Arriba a la derecha pulsa el botón **+** y elige **New repository**.
3. Rellena el formulario:
   - **Repository name**: `nombre-tarea` (idéntico al de la carpeta del Paso 1).
   - **Description**: opcional.
   - **Visibility**: **Public**, para que la profesora pueda verlo (salvo que se indique otra cosa en la tarea).
   - **Add a README file**: **NO** lo marques.
   - **Add .gitignore**: deja "None".
   - **Choose a license**: deja "None".
4. Pulsa **Create repository**.
5. **Comprobación:** GitHub muestra una página titulada "Quick setup" con una dirección como esta:

   `https://github.com/TU_USUARIO/nombre-tarea.git`

   Deja esta página abierta: necesitarás esa dirección en el Paso 3.

> Importante: el repositorio debe crearse vacío (sin README, sin .gitignore y sin licencia). Si GitHub crea archivos por su cuenta, tu primer `git push` será rechazado porque el remoto tendrá contenido que tu ordenador no tiene.

## Paso 3. Inicializar Git en la carpeta y conectarla con GitHub

Convierte tu carpeta en un repositorio local y dile a Git cuál es su repositorio remoto en GitHub.

1. En la terminal de VS Code (Terminal > Nuevo terminal), asegúrate de estar **dentro** de la carpeta de la tarea:

   ```bash
   pwd
   ```

   Debe terminar en `/nombre-tarea`. Si no, entra con `cd ruta/a/nombre-tarea`.
2. Inicializa el repositorio local:

   ```bash
   git init
   ```

   Debe aparecer: `Initialized empty Git repository in .../nombre-tarea/.git/`
3. Pon a la rama principal el nombre `main` (el mismo que usa GitHub):

   ```bash
   git branch -M main
   ```
4. Conecta tu repositorio local con el de GitHub. Copia la dirección de la página "Quick setup" del Paso 2 (opción **HTTPS**) y escribe:

   ```bash
   git remote add origin https://github.com/TU_USUARIO/nombre-tarea.git
   ```

   `origin` es el nombre corto con el que Git recordará esa dirección.
5. **Comprobación:**

   ```bash
   git remote -v
   ```

   Deben aparecer dos líneas con tu dirección, una terminada en `(fetch)` y otra en `(push)`. Revisa que el usuario y el nombre del repositorio están bien escritos.

> Si te has equivocado al escribir la dirección, corrígela con: `git remote set-url origin https://github.com/TU_USUARIO/nombre-tarea.git`

## Paso 4. Descargar el enunciado y guardarlo en tu carpeta

El enunciado es siempre un archivo `.md`. Descárgalo de donde lo haya dejado la profesora y guárdalo **dentro** de la carpeta `nombre-tarea`.

### Opción A: el enunciado está en Moodle

1. Entra en la tarea de Moodle y pulsa sobre el archivo `.md` adjunto.
2. Si el navegador lo descarga, irá a tu carpeta **Descargas**. Si en lugar de descargarlo lo muestra como texto, haz clic derecho sobre el enlace y elige **Guardar enlace como...**.
3. Mueve (o guarda directamente) el archivo dentro de la carpeta `nombre-tarea`.

### Opción B: el enunciado está en el repositorio de GitHub de la profesora

1. Abre el enlace del repositorio que te ha pasado la profesora.
2. En la lista de archivos, haz clic sobre el archivo `.md` del enunciado. Se abrirá con el formato ya aplicado.
3. Arriba a la derecha del contenido del archivo verás una barra de botones: **Raw**, un icono de copiar y un icono de **descarga** (flecha hacia abajo, "Download raw file"). Pulsa el icono de descarga.
4. Mueve el archivo descargado desde **Descargas** a la carpeta `nombre-tarea`.

> Alternativa si no ves el icono de descarga: pulsa **Raw**, y en la página de texto plano que se abre pulsa Control + S (Cmd + S en Mac). Al guardar, comprueba que el nombre termina en `.md` y no en `.txt`.
>
> No uses el botón verde **Code > Download ZIP** ni copies la dirección del repositorio de la profesora con `git clone`: tu carpeta debe contener solo el archivo del enunciado.

> Truco: en vez de mover el archivo con el explorador, puedes arrastrarlo desde la carpeta Descargas y soltarlo en el panel **Explorador** de VS Code, sobre el nombre de tu carpeta.

### Comprobación (para las dos opciones)

El archivo debe aparecer en el panel Explorador de VS Code (barra lateral izquierda). También puedes comprobarlo en la terminal de VS Code:

```bash
ls
```

Debe aparecer el archivo, por ejemplo `enunciado.md`. Comprueba que:

- La extensión es `.md` (no `.md.txt` ni `.txt`). En Windows activa en el Explorador **Vista > Mostrar > Extensiones de nombre de archivo** para verla.
- El archivo no está vacío: ábrelo con tu editor y verifica que se ve el enunciado.

## Paso 5. Hacer el primer commit

Un commit es una "foto" guardada del estado de tus archivos. Se hace en dos movimientos: primero eliges qué archivos entran (`git add`) y después guardas la foto con un mensaje (`git commit`).

Escribe los comandos en la terminal de VS Code. Fíjate también en el panel **Explorador**: mientras Git no sigue el archivo, aparece en verde con una **U**; después del commit la letra desaparece.

1. Mira el estado del repositorio:

   ```bash
   git status
   ```

   El archivo del enunciado aparece en rojo bajo **Untracked files** (Git aún no lo sigue).
2. Añade el archivo al área de preparación (cambia `enunciado.md` por el nombre real):

   ```bash
   git add enunciado.md
   ```

   (También vale `git add .` para añadir todo lo que hay en la carpeta.)
3. Vuelve a comprobar:

   ```bash
   git status
   ```

   Ahora el archivo aparece en verde bajo **Changes to be committed**.
4. Haz el commit con un mensaje que explique lo que has hecho:

   ```bash
   git commit -m "Añado el enunciado de la tarea"
   ```
5. **Comprobación:**

   ```bash
   git log --oneline
   ```

   Debe aparecer una línea con un código y tu mensaje, por ejemplo `a1b2c3d (HEAD -> main) Añado el enunciado de la tarea`. Y `git status` debe decir `nothing to commit, working tree clean`.

> Si Git responde "Please tell me who you are", no configuraste tu nombre y correo: vuelve a "Antes de empezar" y repite el commit.

## Paso 6. Primera subida a GitHub y verificación

Sube tu commit al repositorio remoto. La primera vez se añade `-u` para que Git recuerde a dónde subir en adelante.

1. Escribe:

   ```bash
   git push -u origin main
   ```
2. **Si te pide identificarte:**
   - En Windows y macOS suele abrirse una ventana o el navegador para iniciar sesión en GitHub. Pulsa **Sign in with your browser** y autoriza.
   - Si la terminal pide usuario y contraseña: el usuario es tu usuario de GitHub, pero **la contraseña de tu cuenta no sirve**. Hay que usar un *token*: en GitHub ve a tu foto > **Settings > Developer settings > Personal access tokens > Tokens (classic) > Generate new token**, marca el permiso **repo**, genéralo, cópialo y pégalo como contraseña (al pegar no se ve nada en pantalla; es normal).
3. **Comprobación en la terminal.** El mensaje debe terminar con algo parecido a:

   ```text
   To https://github.com/TU_USUARIO/nombre-tarea.git
    * [new branch]      main -> main
   branch 'main' set up to track 'origin/main'.
   ```

   Si aparece `error` o `rejected`, no continúes: consulta los problemas frecuentes.
4. **Comprobación en GitHub.** Abre `https://github.com/TU_USUARIO/nombre-tarea` (o recarga la página del Paso 2) y verifica:
   - Ya no sale la página "Quick setup": ahora se ve la lista de archivos.
   - Aparece tu archivo `enunciado.md` y, al pulsarlo, se ve el enunciado con formato.
   - Encima de la lista aparece el mensaje de tu commit ("Añado el enunciado de la tarea").
   - La rama que aparece seleccionada es **main**.

## Paso 7. Completar la tarea en el mismo documento

Responde la tarea escribiendo directamente en el archivo `.md` que has descargado; no crees un archivo nuevo.

1. En el panel **Explorador** de VS Code, haz clic en el archivo `.md` para abrirlo en el editor.
2. Escribe tus respuestas debajo de cada pregunta o donde indique el enunciado, usando la sintaxis de Markdown (títulos con `#`, listas con `-`, negrita con `**texto**`, código entre comillas invertidas...).
3. Para ver cómo queda con formato, pulsa Control + Shift + V (Cmd + Shift + V en Mac), o Control + K y después V para verlo al lado mientras escribes.
4. Guarda a menudo con Control + S (Cmd + S en Mac).

> Consejo: si la tarea es larga, puedes hacer commits intermedios (repitiendo el Paso 8) cada vez que termines una parte. Así no pierdes trabajo y queda registro de tu avance.

## Paso 8. Guardar, hacer commit y subir la tarea terminada

Cuando hayas terminado, guarda, haz un commit con tus cambios y súbelo a GitHub.

1. Guarda el archivo en el editor: **Control + S** (Cmd + S en Mac). En VS Code, un punto blanco en la pestaña del archivo indica que hay cambios sin guardar.
2. En la terminal de VS Code, mira qué ha cambiado (en el Explorador el archivo aparece marcado con una M, de modificado):

   ```bash
   git status
   ```

   El archivo aparece en rojo como **modified**. Si dice `nothing to commit`, es que no has guardado: vuelve al punto 1.
3. Añade los cambios y haz el commit:

   ```bash
   git add enunciado.md
   git commit -m "Completo la tarea"
   ```
4. Sube los cambios. Como en el Paso 6 usaste `-u`, ahora basta con:

   ```bash
   git push
   ```
5. **Comprobación:**

   ```bash
   git status
   ```

   Debe decir `Your branch is up to date with 'origin/main'` y `nothing to commit, working tree clean`.

## Paso 9. Comprobar en GitHub que la entrega está correcta

Antes de entregar, revisa en la web que lo que hay en GitHub es tu versión final.

- [ ] Abre `https://github.com/TU_USUARIO/nombre-tarea` y recarga la página (F5).
- [ ] Encima de la lista de archivos aparece tu último mensaje de commit ("Completo la tarea") con una hora reciente.
- [ ] Al pulsar el archivo `.md` se ven **tus respuestas** con el formato correcto (títulos, listas, negritas...).
- [ ] Pulsando en **commits** (icono de reloj, junto al número de commits) aparecen al menos dos: el del enunciado y el de la tarea terminada.
- [ ] El repositorio es **Public**: cierra sesión o abre una ventana de incógnito, pega la dirección y comprueba que se ve. Si sale "404", la profesora tampoco podrá verlo (cámbialo en **Settings > General > Danger Zone > Change visibility**).

Si falta algo, corrígelo en tu ordenador y repite el Paso 8.

## Paso 10. Entregar el enlace en Moodle

La entrega en Moodle es un archivo de texto con el enlace de tu repositorio.

1. En la página principal de tu repositorio en GitHub, pulsa el botón verde **Code**.
2. En la pestaña **Local**, opción **HTTPS**, pulsa el icono de copiar que hay junto a la dirección. Se copia algo como:

   `https://github.com/TU_USUARIO/nombre-tarea.git`
3. Crea un archivo de texto plano (con el Bloc de notas, TextEdit en modo texto o tu editor) y pega el enlace dentro.
4. Guárdalo con un nombre claro, por ejemplo `Apellido_Nombre_nombre-tarea.txt`.
5. **Comprobación:** copia el enlace del archivo, pégalo en el navegador y verifica que abre tu repositorio.
6. Entra en la tarea de Moodle, pulsa **Agregar entrega**, adjunta el archivo `.txt` y pulsa **Guardar cambios** (y **Enviar tarea** si aparece ese botón).

> Guarda el `.txt` **fuera** de la carpeta de la tarea (por ejemplo en el Escritorio), para no mezclarlo con el repositorio.

## Resumen de comandos

| Paso | Dónde / comando | Para qué sirve |
| --- | --- | --- |
| 1 | Explorador de archivos > Nueva carpeta | Crear la carpeta de la tarea |
| 1 | VS Code > Archivo > Abrir carpeta | Abrir la carpeta en VS Code |
| 1 | VS Code > Terminal > Nuevo terminal | Abrir la terminal donde se escriben los comandos |
| 1 | `git status` | Comprobar que NO estás dentro de otro repositorio (debe salir `fatal`) |
| 3 | `git init` | Convertir la carpeta en repositorio local |
| 3 | `git branch -M main` | Llamar `main` a la rama principal |
| 3 | `git remote add origin URL` | Conectar con el repositorio de GitHub |
| 3 | `git remote -v` | Ver a qué repositorio remoto estás conectado |
| 5 y 8 | `git add archivo.md` | Preparar el archivo para el commit |
| 5 y 8 | `git commit -m "mensaje"` | Guardar una versión con un mensaje |
| 5 | `git log --oneline` | Ver la lista de commits |
| 6 | `git push -u origin main` | Primera subida a GitHub |
| 8 | `git push` | Siguientes subidas |

## Problemas frecuentes

| Mensaje o síntoma | Causa | Solución |
| --- | --- | --- |
| `fatal: not a git repository` al hacer `git add`, `commit` o `push` | VS Code tiene abierta otra carpeta, o no hiciste `git init` | Abre la carpeta de la tarea con *Archivo > Abrir carpeta*, abre un terminal nuevo y comprueba con `pwd`; si falta, haz el Paso 3 |
| En el Paso 1, `git status` NO da error | La carpeta está dentro de otro repositorio | Crea la carpeta en otro sitio (Paso 1, punto 4) |
| `ls -a` da error en Windows | La terminal de VS Code es PowerShell, no Git Bash | Cambia a Git Bash (ver "Antes de empezar") |
| `git` no se reconoce en la terminal de VS Code | Git no está instalado, o VS Code estaba abierto al instalarlo | Instala Git y cierra y vuelve a abrir VS Code |
| `error: remote origin already exists` | Ya añadiste el remoto antes | Comprueba con `git remote -v`; si está mal, `git remote set-url origin URL` |
| `error: src refspec main does not match any` | Aún no has hecho ningún commit, o la rama no se llama `main` | Haz el Paso 5 y después `git branch -M main` |
| `! [rejected] ... (fetch first)` | El repositorio de GitHub no estaba vacío (se creó con README) | Ejecuta `git pull origin main --allow-unrelated-histories`, guarda el mensaje que se abra y repite `git push` |
| `Authentication failed` o `Support for password authentication was removed` | Has puesto la contraseña de GitHub | Usa un token como contraseña (Paso 6, punto 2) |
| `Repository not found` | Dirección mal escrita o repositorio inexistente | Revisa `git remote -v` y corrígela con `git remote set-url origin URL` |
| `nothing to commit, working tree clean` y en GitHub no están tus cambios | No guardaste el archivo antes del commit | Control + S en VS Code y repite el Paso 8 |
| El archivo se llama `enunciado.md.txt` | Se guardó como texto | Renómbralo a `enunciado.md` (en VS Code: clic derecho sobre el archivo > Cambiar nombre) |
| GitHub muestra el archivo sin formato | La extensión no es `.md` | Renómbralo, haz commit y push |
| `Please tell me who you are` | Falta configurar nombre y correo | Ver "Antes de empezar" |
