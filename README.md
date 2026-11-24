# Know My Guitar

Juego web para aprender el diapasón de la guitarra tocando una guitarra real.
El juego escucha lo que tocas (micrófono o interfaz de audio USB), detecta la nota
y su octava, y comprueba si es correcta.

Todo está en un solo archivo: `index.html` (sin dependencias externas).

## Cómo abrirlo

El navegador solo permite usar el micrófono en **HTTPS** o en **localhost**:

```bash
python3 -m http.server 8000
```

Luego abre <http://localhost:8000>. Abriendo el archivo directamente (`file://`)
también puedes jugar en **modo sin audio** (clic en el diapasón).

## Modos

- **Encuentra la tónica**: toca la nota pedida en todas sus posiciones, cuerda por cuerda.
- Próximamente: una nota en todas las cuerdas, intervalos, escalas, arpegios.

## Estructura del código (dentro de `index.html`)

| Módulo | Función |
| --- | --- |
| `Music` | Nombres de notas, afinaciones (`TUNINGS`), cálculo de posiciones |
| `Settings` | Ajustes persistentes en `localStorage` |
| `PitchDetect` | Algoritmo YIN (70–1400 Hz) y `NoteTracker` (estabilidad, ataque, armónicos) |
| `AudioEngine` | Dispositivos, `getUserMedia` sin procesamiento de voz, canal, nivel |
| `NoteBus` | Eventos de notas aceptadas (audio real o clic simulado) |
| `Fretboard` | Diapasón SVG compartido (19–24 trastes, zurdos, marcas) |
| `MODES` | Registro de modos. Cada modo implementa `renderSetup()` y `start()` |

Para agregar un modo nuevo: crea un objeto como `TonicMode` y añádelo a `MODES`.
Para agregar una afinación: añade una entrada a `Music.TUNINGS`.
