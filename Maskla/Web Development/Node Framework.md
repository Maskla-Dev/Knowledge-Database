Framework que permite la construcción de sistemas de nodos, provee de una interfaz que permite definir como se manipulan los datos entrantes y salientes de los nodos. Adicionalmente, se construye una interfaz que se adapta a los tipos de datos definidos.

Idealmente, la construcción de una aplicación utilizando el sistema de nodos sería
1. El programador registra tipos de datos de entrada y salida.
2. Se registran los tipos de nodos existentes, sus posibles entradas, salidas, las condiciones para procesar dichos datos y la manera en que se procesan los datos
3. Definido eso, una vez desplegada la aplicación, el sistema construirá una interfaz gráfica donde pueda manipular los nodos definidos y el flujo de datos.

En esencia, cada nodo representa un objeto, el nodo en la interfaz solo sirve para manipular sus datos y su procesamiento.

# Requerimientos
# Interfaz

![[NodeSystem_Blockout.png]]

- **Node editor viewport**: En la interfaz principal agrupa la interactividad de los nodos.
- **Node Options**: Agrupa todas las opciones de edición de parámetros de los nodos.
- **Editor Tools**: Proporciona herramientas que facilitan la manipulación del editor.
- **Wirepaths**: Enlista todos los nodos creados.
# Especificaciones
## Nodo
Un nodo tiene una capa externa y una interna. En la capa interna se encuentra un objeto, el objeto es una abstracción que sigue el marco de un paradigma orientado a objetos, es decir, el objeto proviene de alguna clase la cual tiene características y acciones especificas (atributos y métodos)