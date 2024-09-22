Es una API que permite el acceso a las funcionalidades de la GPU. La arquitectura se puede apreciar con la figura, teniendo que el intermediario entre el SO y una aplicación es el adaptador, que es la representación física de la GPU, mediante este intermediario se pueden crear instancias a través de dispositivos lógicos en donde la aplicación puede solicitar las prestaciones de cálculo.

![[Pasted image 20240809215557.png]]
# Punto de partida
El dispositivo lógico puede ser creado a través de la clase `GPUDevice` y el adaptador mediante `GPUAdapter`. La instancia al adaptador se expone a través de la propiedad `navigator.gpu`, la propiedad `navigator` es el punto de partida al acceso a las distintas APIs del contexto del navegador, por lo tanto al acceder a `gpu` estamos obteniendo la instancia a la API de WebGPU (`GPU` es la clase que abstrae este punto de partida). Uno de los aspectos interesantes es el listado de las extensiones del WebGPU Shading Language, accesibles al listado en un objeto [[Set]] mediante el atributo `wgslLanguageFeatures`. Como métodos es importante conocer `getPreferredCanvasFormat()`, el cual nos permite obtener una cadena con la cual el `canvas` trabaja de manera óptima en el renderizado; encontramos también `requestAdapter()` quien nos proporcionará la instancia `GPUAdapter`.