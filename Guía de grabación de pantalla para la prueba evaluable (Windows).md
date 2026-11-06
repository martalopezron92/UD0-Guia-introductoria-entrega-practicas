# Guía de grabación de pantalla para la prueba evaluable (Windows)

Esta guía explica cómo grabar la pantalla durante la **Parte B** de la prueba (90 minutos), cómo configurar la grabación para que el vídeo ocupe lo menos posible y cómo comprimirlo para subirlo a GitHub.

**Herramientas que vas a usar (ambas gratuitas):**

- **OBS Studio**, para grabar la pantalla.
- **7-Zip**, para comprimir el vídeo en formato `.7z` (y dividirlo en partes si fuera necesario).

> **Importante:** instala, configura y haz una **grabación de prueba antes del lunes**. El día de la prueba no habrá tiempo para resolver problemas de instalación.

## 1. Instalar OBS Studio

**Opción A – Desde la web oficial (recomendada):**

1. Entra en **https://obsproject.com**.
2. Pulsa el botón **Windows** para descargar el instalador.
3. Ejecuta el archivo descargado y pulsa **Siguiente** hasta terminar, dejando las opciones por defecto.
4. Al abrir OBS por primera vez puede aparecer el **Asistente de configuración automática**. Elige **Optimizar solo para grabación** o ciérralo: lo configuraremos a mano en el siguiente apartado.

**Opción B – Desde la terminal (PowerShell o Símbolo del sistema):**

```
winget install OBSProject.OBSStudio
```

## 2. Configurar OBS para que el vídeo ocupe poco

Abre **Archivo → Ajustes** y aplica la siguiente configuración. Al terminar, pulsa **Aplicar** y **Aceptar**.

### 2.1. Pestaña Salida

1. En **Modo de salida**, selecciona **Avanzado**.
2. Entra en la subpestaña **Grabación** y configura:

| Opción | Valor |
| --- | --- |
| Tipo | Estándar |
| Ruta de grabación | Una carpeta fácil de encontrar (por ejemplo, Escritorio) |
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

1. En la ventana principal de OBS, en el panel **Fuentes**, pulsa **+**.
2. Elige **Captura de pantalla** y pulsa **Aceptar**.
3. Si tienes varios monitores, selecciona el monitor en el que vas a trabajar y pulsa **Aceptar**.
4. En la vista previa debe aparecer tu escritorio completo.

## 3. Hacer una grabación de prueba (antes del lunes)

1. Pulsa **Iniciar grabación** y trabaja con normalidad durante **3 minutos** (abre tus apuntes, escribe en el editor…).
2. Pulsa **Detener grabación**.
3. Abre la carpeta de grabación y comprueba que el vídeo **se reproduce y se lee bien el texto**.
4. Mira el tamaño del archivo y **multiplícalo por 30** para estimar lo que ocupará la grabación de 90 minutos. Por ejemplo, si 3 minutos ocupan 2,5 MB, la prueba completa ocupará unos 75 MB.

## 4. El día de la prueba

1. Abre OBS **antes de empezar** la Parte B.
2. Pulsa **Iniciar grabación** y comprueba que el contador de tiempo de la parte inferior avanza.
3. **No minimices ni cierres OBS** hasta terminar. Puedes dejarlo en segundo plano.
4. Al terminar los ejercicios, pulsa **Detener grabación**.
5. Comprueba que el archivo de vídeo aparece en la carpeta de grabación.

## 5. Instalar 7-Zip

**Opción A – Desde la web oficial (recomendada):**

1. Entra en **https://www.7-zip.org**.
2. Descarga la versión **64-bit Windows x64** (la primera de la lista).
3. Ejecuta el instalador y pulsa **Install**.

**Opción B – Desde la terminal:**

```
winget install 7zip.7zip
```

## 6. Comprimir el vídeo con 7-Zip

1. Haz clic derecho sobre el archivo de vídeo. En **Windows 11**, pulsa primero **Mostrar más opciones**.
2. Selecciona **7-Zip → Añadir al archivo…**
3. Configura:
   - **Formato de archivo:** **7z**
   - **Nivel de compresión:** Normal
   - **Dividir en fragmentos (bytes):** déjalo vacío si el vídeo ocupa menos de lo indicado en el apartado 7; si no, consulta ese apartado.
4. Pulsa **Aceptar**. Se creará el archivo comprimido en la misma carpeta.

> **Nota:** 7-Zip apenas reduce el tamaño de un vídeo, porque el vídeo ya está comprimido. Lo que realmente hace que ocupe poco es la configuración de OBS del apartado 2.

## 7. Límites de GitHub y cómo dividir el archivo

GitHub limita el tamaño de los archivos:

| Cómo subes el archivo | Tamaño máximo por archivo |
| --- | --- |
| Desde la web (Add file → Upload files) | **25 MB** |
| Con Git desde la terminal (`git push`) | **100 MB** |

Si tu archivo `.7z` supera el límite, **divídelo en fragmentos** con 7-Zip (paso 3 del apartado 6), escribiendo en **Dividir en fragmentos (bytes)**:

- **`24M`** si vas a subirlo desde la web.
- **`90M`** si vas a subirlo con `git push`.

7-Zip generará varios archivos con nombres como `video.7z.001`, `video.7z.002`, etc. **Sube todos los fragmentos** al repositorio: sin uno solo de ellos el vídeo no se puede abrir.

## 8. Comprobación final antes de entregar

- [ ] El repositorio se llama `1DAW-BBDD-XXX-UD01-P01`.
- [ ] Contiene el archivo Markdown con los ejercicios resueltos.
- [ ] Contiene el vídeo comprimido en `.7z` (o **todos** sus fragmentos).
- [ ] Has entregado en Moodle el archivo de texto con la URL del repositorio.

## 9. Problemas frecuentes

- **La vista previa de OBS sale en negro (portátiles con dos tarjetas gráficas):** cierra OBS, ve a **Configuración de Windows → Sistema → Pantalla → Gráficos**, añade OBS y elige **Ahorro de energía**. Vuelve a abrir OBS.
- **El vídeo ocupa demasiado:** baja la tasa de bits a **100 Kbps** o los FPS a **5** y repite la grabación de prueba.
- **No se lee bien el texto en el vídeo:** sube la tasa de bits a **250 Kbps** y divide el archivo en fragmentos si es necesario.
- **No aparece "7-Zip" al hacer clic derecho:** en Windows 11 pulsa **Mostrar más opciones**; si sigue sin aparecer, reinstala 7-Zip.

Recuerda: **si no se entrega el vídeo, la Parte B no se calificará** y tendrá una nota de 0.
