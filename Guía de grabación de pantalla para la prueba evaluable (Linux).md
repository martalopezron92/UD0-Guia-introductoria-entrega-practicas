# Guía de grabación de pantalla para la prueba evaluable (Linux)

Esta guía explica cómo grabar la pantalla durante la **Parte B** de la prueba (90 minutos), cómo configurar la grabación para que el vídeo ocupe lo menos posible y cómo comprimirlo para subirlo a GitHub. Los comandos están pensados para **Ubuntu y derivadas** (Linux Mint, Pop!\_OS…); para otras distribuciones se indica la alternativa con Flatpak.

**Herramientas que vas a usar (ambas gratuitas):**

- **OBS Studio**, para grabar la pantalla.
- **7-Zip** (comando `7z`), para comprimir el vídeo en formato `.7z` y dividirlo en partes si fuera necesario.

> **Importante:** instala, configura y haz una **grabación de prueba antes del lunes**. El día de la prueba no habrá tiempo para resolver problemas de instalación.

## 1. Instalar OBS Studio

Abre una terminal (**Ctrl + Alt + T**).

**Opción A – Ubuntu y derivadas (repositorio oficial de OBS, recomendada):**

```
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install obs-studio
```

**Opción B – Cualquier distribución con Flatpak:**

```
flatpak install flathub com.obsproject.Studio
```

Al abrir OBS por primera vez puede aparecer el **Asistente de configuración automática**. Elige **Optimizar solo para grabación** o ciérralo: lo configuraremos a mano en el siguiente apartado.

## 2. Configurar OBS para que el vídeo ocupe poco

Abre **Archivo → Ajustes** y aplica la siguiente configuración. Al terminar, pulsa **Aplicar** y **Aceptar**.

### 2.1. Pestaña Salida

1. En **Modo de salida**, selecciona **Avanzado**.
2. Entra en la subpestaña **Grabación** y configura:

| Opción | Valor |
| --- | --- |
| Tipo | Estándar |
| Ruta de grabación | Una carpeta fácil de encontrar (por ejemplo, `~/Vídeos`) |
| Formato de grabación | **MKV** (si el ordenador se bloquea, el vídeo no se pierde) |
| Pista de audio | Marca **solo la 1** (OBS obliga a tener al menos una) |
| Codificador de vídeo | **x264** |
| Control de frecuencia | **CBR** |
| Tasa de bits | **150 Kbps** |
| Intervalo de fotogramas clave | **10 s** |
| Preset de uso de CPU | **veryfast** |

3. Entra en la subpestaña **Audio** y, en **Pista 1**, selecciona la **tasa de bits más baja** disponible.

### 2.2. Pestaña Vídeo

| Opción | Valor |
| --- | --- |
| Resolución base (lienzo) | La de tu pantalla (no la cambies) |
| Resolución de salida (escalada) | **1280x720** |
| Valores comunes de FPS | **10** |

Una pantalla con un editor de código cambia muy poco, así que con 10 fotogramas por segundo es más que suficiente y el archivo ocupa mucho menos.

### 2.3. Pestaña Audio

En **Dispositivos de audio globales**, pon **Desactivado** en **Audio del escritorio** y en **Micrófono/Audio auxiliar**. No necesitamos sonido y así la pista de audio queda en silencio.

### 2.4. Añadir la captura de pantalla

La fuente que debes añadir depende del tipo de sesión gráfica. Para saber cuál usas, ejecuta en la terminal:

```
echo $XDG_SESSION_TYPE
```

| Resultado | Fuente que debes añadir |
| --- | --- |
| `wayland` (lo habitual en Ubuntu reciente) | **Captura de pantalla (PipeWire)** |
| `x11` | **Captura de pantalla (XSHM)** |

1. En la ventana principal de OBS, en el panel **Fuentes**, pulsa **+**.
2. Elige la fuente indicada en la tabla y pulsa **Aceptar**.
3. **En Wayland**, el sistema mostrará una ventana preguntando qué quieres compartir: selecciona tu **pantalla completa** (el monitor en el que vas a trabajar) y pulsa **Compartir**.
4. **En X11**, selecciona el monitor en el que vas a trabajar.
5. En la vista previa debe aparecer tu escritorio completo.

## 3. Hacer una grabación de prueba (antes del lunes)

1. Pulsa **Iniciar grabación** y trabaja con normalidad durante **3 minutos** (abre tus apuntes, escribe en el editor…).
2. Pulsa **Detener grabación**.
3. Abre la carpeta de grabación y comprueba que el vídeo **se reproduce y se lee bien el texto**.
4. Mira el tamaño del archivo (o ejecuta `ls -lh ~/Vídeos`) y **multiplícalo por 30** para estimar lo que ocupará la grabación de 90 minutos. Por ejemplo, si 3 minutos ocupan 2,5 MB, la prueba completa ocupará unos 75 MB.

## 4. El día de la prueba

1. Abre OBS **antes de empezar** la Parte B.
2. Pulsa **Iniciar grabación** y comprueba que el contador de tiempo de la parte inferior avanza.
3. **No cierres OBS** hasta terminar. Puedes dejarlo en segundo plano.
4. Al terminar los ejercicios, pulsa **Detener grabación**.
5. Comprueba que el archivo de vídeo aparece en la carpeta de grabación.

## 5. Instalar 7-Zip

**Ubuntu y derivadas:**

```
sudo apt install p7zip-full
```

**Fedora:**

```
sudo dnf install p7zip p7zip-plugins
```

Comprueba que está instalado ejecutando `7z`: debe aparecer la ayuda del programa.

## 6. Comprimir el vídeo con 7-Zip

Abre una terminal en la carpeta donde está el vídeo (por ejemplo, `cd ~/Vídeos`) y ejecuta el comando que corresponda. Sustituye `grabacion.mkv` por el nombre real de tu archivo.

**Si el vídeo ocupa menos del límite de GitHub (ver apartado 7):**

```
7z a video.7z grabacion.mkv
```

**Si hay que dividirlo en fragmentos de 24 MB (para subir desde la web):**

```
7z a -v24m video.7z grabacion.mkv
```

**Si hay que dividirlo en fragmentos de 90 MB (para subir con `git push`):**

```
7z a -v90m video.7z grabacion.mkv
```

> **Consejo:** si tu nombre de archivo tiene espacios, escríbelo entre comillas, por ejemplo `"2026-11-09 16-50-12.mkv"`. También puedes escribir las primeras letras y pulsar **Tab** para que se autocomplete.

> **Nota:** 7-Zip apenas reduce el tamaño de un vídeo, porque el vídeo ya está comprimido. Lo que realmente hace que ocupe poco es la configuración de OBS del apartado 2.

## 7. Límites de GitHub y fragmentos

GitHub limita el tamaño de los archivos:

| Cómo subes el archivo | Tamaño máximo por archivo |
| --- | --- |
| Desde la web (Add file → Upload files) | **25 MB** |
| Con Git desde la terminal (`git push`) | **100 MB** |

Si has dividido el archivo, 7-Zip habrá generado varios archivos con nombres como `video.7z.001`, `video.7z.002`, etc. **Sube todos los fragmentos** al repositorio: sin uno solo de ellos el vídeo no se puede abrir.

## 8. Comprobación final antes de entregar

- [ ] El repositorio se llama `1DAW-BBDD-XXX-UD01-P01`.
- [ ] Contiene el archivo Markdown con los ejercicios resueltos.
- [ ] Contiene el vídeo comprimido en `.7z` (o **todos** sus fragmentos).
- [ ] Has entregado en Moodle el archivo de texto con la URL del repositorio.

## 9. Problemas frecuentes

- **La vista previa de OBS sale en negro:** casi siempre es porque has añadido la fuente equivocada. Comprueba tu tipo de sesión (apartado 2.4) y usa **PipeWire** en Wayland o **XSHM** en X11. Si sigue en negro, cierra sesión y, en la pantalla de inicio de sesión, elige **Ubuntu en Xorg** (icono de engranaje) antes de entrar.
- **No aparece la fuente "Captura de pantalla (PipeWire)":** actualiza el sistema (`sudo apt update && sudo apt upgrade`) o instala OBS con Flatpak (opción B del apartado 1).
- **El vídeo ocupa demasiado:** baja la tasa de bits a **100 Kbps** o los FPS a **5** y repite la grabación de prueba.
- **No se lee bien el texto en el vídeo:** sube la tasa de bits a **250 Kbps** y divide el archivo en fragmentos si es necesario.
- **El comando `7z` no se encuentra:** repite la instalación del apartado 5.

Recuerda: **si no se entrega el vídeo, la Parte B no se calificará** y tendrá una nota de 0.
