![[maskladev_HomeDesktopWireframe.png]]
_Blockout de la página_

# Header
**Header** es un contenedor de los siguientes elementos:
- Logo
- Nav Buttons
- Selector de idioma

---
- [x] Contenedor del logo
- [x] Botones de navegacion
	- [x] Icono Portfolio
	- [x] Icono About Maskla
	- [x] Icono MindNet
- [x] Selector de idioma
	- [x] Input selector

> [!caution]
> TODOs Solo se trabajan como maqueta del frontend
## Logo
El logo contiene una imágen representativa del sitio, a su vez, es una referencia que direcciona a la página principal [[maskla.dev#Maskla - Home]].


## Nav Buttons
Los nav buttons son botones de navegación, son elementos interactuables que identifican cada una de las secciones del sitio al que el usuario puede acceder, por lo que solo existen 3 (portfolio, about maskla y mindnet). Cada uno al ser pulsado, cambiara el contenido del contenedor [[maskla.dev - Home#Fast Site-Travel Box]] según el caso.

### Fast Site-Travel Box
Es un contenedor dinámico, puede cerrarse o abrirse cuando el cursor no se encuentra en Nav Buttons o este mismo contenedor. Si se ha pulsado el boton Portfolio aparecera la referencia a la página [[maskla.dev - Portfolio]] y los 3 proyectos más destacados; al haber pulsado about maskla se redirecciona directamente a [[maskla.dev - About Maskla]]; finalmente, al pulsar MindNet se obtienen las temáticas y la referencia a la página [[maskla.dev - MindNet]]

## Selector de idioma
El selector de idioma es un input selector que registra los cambios, si se ha cambiado, se pedira al servidor la version correspondiente a dicho idioma y la devolverá para que se reemplacen los textos. Los idiomas soportados serán español e ingles por defecto, los demás dependerán del servicio de traducción.

# Main Content

# Aside content

# Footer
