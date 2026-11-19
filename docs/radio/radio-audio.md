<div class="ateca-hero" markdown>

![Entérate](../assets/img/hero/radio.jpg){ .ateca-hero__img .off-glb }

<div class="ateca-hero__texto">
<p class="ateca-hero__eyebrow">Radio y audio · Aula ATECA</p>
<h1>Radio <span>Entérate</span></h1>
<p>La emisora escolar del CIFP Villa de Agüimes: guion, grabación, edición y mezcla de programas con software libre.</p>
</div>
<p class="ateca-hero__credito">Foto: <a href="https://commons.wikimedia.org/wiki/File:Radio_WWOZ_New_Orleans_studio_October_2009_26.jpg" target="_blank" rel="noopener">Infrogmation of New Orleans</a> · CC BY-SA 4.0 · Wikimedia Commons</p>

</div>

<div class="video-botones">
<a class="video-boton" href="https://www.youtube.com/watch?v=l6cbUhjeLo4" target="_blank" rel="noopener" title="Cómo hacer un programa de radio (Educar Portal)"><span class="video-boton__play"></span><span class="video-boton__texto"><span class="video-boton__meta">Vídeo · 3 min</span><span class="video-boton__titulo">Cómo hacer un programa de radio</span><span class="video-boton__canal">Educar Portal</span></span></a>
<a class="video-boton" href="https://www.youtube.com/watch?v=A8APjp4g84U" target="_blank" rel="noopener" title="Audacity en 5 pasos (Tutoriales Youtuber)"><span class="video-boton__play"></span><span class="video-boton__texto"><span class="video-boton__meta">Vídeo · 8 min</span><span class="video-boton__titulo">Audacity en 5 pasos</span><span class="video-boton__canal">Tutoriales Youtuber</span></span></a>
<a class="video-boton" href="https://www.youtube.com/watch?v=z1S7Oyxe-rw" target="_blank" rel="noopener" title="Mixxx, software de DJ gratuito (TecnologiaDJ)"><span class="video-boton__play"></span><span class="video-boton__texto"><span class="video-boton__meta">Vídeo · 16 min</span><span class="video-boton__titulo">Mixxx, software de DJ gratuito</span><span class="video-boton__canal">TecnologiaDJ</span></span></a>
</div>

> El Aula ATECA da soporte a **Radio Entérate**, la emisora escolar del CIFP Villa de Agüimes, donde el alumnado produce programas educativos y divulgativos. Este manual cubre el flujo de trabajo de grabación/edición y las herramientas disponibles.

## 1. Radio Entérate { .seccion }

Proyecto de radio educativa gestionado por alumnado y profesorado del centro, orientado a desarrollar creatividad, comunicación oral y trabajo en equipo.

### 1.1 Flujo de un programa

![Flujo de producción de un programa de Radio Entérate](../assets/img/rad/radio-flujo.svg){ .diagrama .off-glb }

1. **Guion**: se prepara escaleta con bloques, tiempos y locutores. Reparte turnos de palabra por escrito para evitar solapamientos en la grabación.
2. **Grabación**: en el aula, con micrófono conectado al PC y **Audacity** abierto en una pista estéreo a 44.1 kHz. Haz una prueba de 10 segundos antes de grabar el programa completo para comprobar niveles.
3. **Edición**: cortes, ecualización básica, eliminación de ruido de fondo y normalización de volumen en Audacity.
4. **Música/efectos**: mezcla de cortinillas y música con **MIXXX** si el programa incluye tramos musicales en directo o pregrabados tipo DJ set.
5. **Exportación**: MP3 a 192 kbps (buen equilibrio calidad/peso) para publicación o retransmisión.

### 1.2 Buenas prácticas

- Graba siempre con auriculares puestos para detectar ruidos en directo (soplidos, sillas, móviles).
- Deja 2-3 segundos de silencio al inicio y final de cada grabación (margen para edición).
- Guarda el proyecto de Audacity (`.aup3`) además del MP3 exportado, por si hay que retocar algo más adelante.
- Archiva cada programa con un nombre consistente: `AAAAMMDD-titulo-programa.mp3`, para poder encontrarlo fácilmente en el histórico de la emisora.

## 2. Audacity { .seccion }

Software libre y gratuito, estándar de facto en educación para grabación y edición de audio multipista.

### 2.1 Configuración básica

1. En **Editar → Preferencias → Dispositivos**, selecciona el micrófono del aula como entrada y los altavoces/auriculares como salida.
2. Ajusta el proyecto a 44.1 kHz / estéreo (o mono si es solo voz, para reducir peso de archivo).
3. Usa **Efectos → Reducción de ruido**: primero capturas una muestra de "solo ruido" (2-3 segundos de silencio) y luego aplicas la reducción al resto de la pista.
4. **Efectos → Normalizar** al final para igualar volúmenes entre distintos locutores/tomas.

### 2.2 Atajos útiles

| Acción | Atajo |
|---|---|
| Grabar | R |
| Reproducir/Pausar | Espacio |
| Cortar silencio seleccionado | Ctrl + L |
| Deshacer | Ctrl + Z |
| Exportar como MP3 | Archivo → Exportar → Exportar como MP3 |

## 3. MIXXX { .seccion }

Herramienta libre para mezclar música en directo (crossfader, control de BPM, cue points), útil para separadores musicales del programa o proyectos de eventos del centro.

### 3.1 Uso básico

1. Carga las pistas en los dos *decks* (izquierda/derecha).
2. Sincroniza el BPM con el botón **Sync** antes de mezclar.
3. Usa el *crossfader* central para transicionar de una pista a otra.
4. Marca *cue points* (puntos de entrada) en los estribillos o momentos clave para no tener que buscar manualmente en directo.

## 📚 Recursos { .seccion }

- 📖 [Manual de Audacity (español)](https://manual.audacityteam.org/){target="_blank"}
- 🌐 [Audacity](https://audacity.es){target="_blank"}
- 🌐 [MIXXX](https://mixxx.org){target="_blank"}
- 🌐 Web del Aula ATECA (fuente de este manual): [Tecnologías | Aula AtecA](https://www3.gobiernodecanarias.org/medusa/proyecto/35014664-0006/aplicaciones/){target="_blank"}

> 📷 **Pendiente:** añadir fotos reales del set de radio del aula (mesa de mezclas, micrófonos, cabina) y una captura de un proyecto de Audacity ya editado.
