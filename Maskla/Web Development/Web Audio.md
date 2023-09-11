La API para manejar el audio en web se basa en la generación y conexión de nodos, teniendo 3 tipos de nodos: generadores, efectos y destino. Los nodos destino son las terminales en donde el audio terminará; los nodos generadores son las fuentes de audio.

# Fuentes y conexiones
El manejo de estas rutas de audio se realizan mediante un `AudioContext`, como su nombre lo indica, permite encapsular y operar las rutas de manera aislada. Principalmente, se requiere especificar fuentes de sonido mediante nodos. Cada una tiene sus variantes de lectura de fuente:
- `Buffer`:  La fuente proviene de la codificación del audio almacenada directamente en la memoria, es una fuente que optimiza pequeñas muestras de audio (recomendado 45 segundos de duración). Se genera un nodo de una fuente buffer mediante  `createBufferSource()`
- `Constant`: Una fuente cuya salida es un sonido monoaural (un solo canal) y sus muestras siempre tienen el mismo valor. Utilizar `createConstantSource()` para obtener el nodo.
- `Media`: La fuente proviene de un archivo de audio, se caracteriza por requerir un medio de manipulación directa en el DOM mediante `<audio>` o `<video>`. Obtener su nodo con `createMediaElementSource()`. 
- `MediaStreamTrack`: Los dispositivos externos que puedan funcionar a modo de fuente de audio acceden a la interfaz mediante este tipo. Es necesario un nodo mediante `createMediaStreamTrackSource()`.
- `MediaStream`: Es la agrupación de todos las fuentes `MediaStreamTrack`. El nodo se crea con `createMediaStreamSource()`.

![[AudioAPI.png]]

Las fuentes descritas anteriormente, cuando son procesadas para ser utilizadas dentro de un `AudioContext`  son `AudioNode`, de manera ilustrativa se les da el nombre _AudioSourceNode_. Cada nodo puede ser anidado mediante su propia interfaz mediante `connect()`, de esta manera se direcciona la salida de datos, la cual puede verse como el "la instrucción cable que conecta a las terminales". La interfaz de audio expone el dispositivo que reproduce el audio a nivel SO mediante el atributo `destination`, el cual retorna un objeto `AudioDestinationNode` que representa el nodo final.

```javascript
const audio_context = new AudioContext();
const audio_media_container = document.createElement('audio');
audio.src = '/supported_audio.mp3';
const audio_source_node = audio_context.createMediaElementSource();
const gain_node = audio_context.createGain();
audio_source_node.connect(gain_node);
gain_node.connect(audio_context.destination);
```

Las conexiones no sólo se limitan a nodos, también pueden realizarse hacia `AudioParams`, estos mismos encapsulan el valor al que esta relacionado con un `AudioNode` de efecto, de esta manera se permite controlar el parámetro sin efectos indeseados (como saltos o interrupciones del audio).

# Tipos de nodos
- **GainNode**: Este tipo de nodo permite controlar la intensidad de la señal de audio, es decir, la altura de la onda del audio.
- 