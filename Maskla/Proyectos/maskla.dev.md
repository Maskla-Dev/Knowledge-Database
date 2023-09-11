Sitio web, contiene conocimientos técnicos adquiridos, proyectos realizados e información acerca de Maskla. Opcionalmente, todo el sitio muestra información en cualquier idioma.

La organización de la página se muestra en el siguiente mapa del sitio:
![[mapsite_maskla.dev.drawio.png]]
# Mapa del sitio
- Index
	- Home
		- Portfolio
		- About Maskla
			- Donaciones
		- Mindnet
			- {Posts}
			- Request Review
			- FAQ
	- Admin - Login
		- Dashboard
			- Maskla - SiteMap
			- Log
			- Info
			- Form

## Maskla - Home
[[maskla.dev - Home]]
Es el punto de partida del sitio, contiene información una tarjeta de presentación del sitio, los post más recientes y relevantes de MindNet, publicaciones recientes de las redes sociales, links a redes sociales, los proyectos más relevantes creados hasta la fecha y monto en donaciones en caso de existir. El sitio puede direccionar directamente a las paginas:
- MindNet
- Portfolio
- Acerca de Maskla
Inicia con una pantalla de carga hasta que se obtiene la información.

### MindNet
La página contiene un índice donde se organizan los post introducidos, una barra de búsqueda y filtrado. De manera decorativa y de forma opcional se incorporará una vista en gráfo del sitio y sus relaciones.

#### Posts
Cada post esta separado temática y etiquetado por palabras clave; cada post puede ser editado o agregado desde [[maskla.dev#Form|la página del administrador]]. Cada post debe de contener una como cabecerá el nombre del post, la temática, las palabras clave, la última fecha en que fue modificado el post,  autor, agradecimientos especiales y un boton que direccione a [[maskla.dev#Request Review]] en caso de solicitar revisión; como contenido, solo el contenido a mostrar; por último, las referencias de donde fue obtenida la información. Si se requiere revisión, se coloca la información de origen en el redireccionamiento de la URL.

##### Referencias
Las referencias tendrán un formato simplificado al mostrarse. Cada referencia puede obtenerse mediante portapapeles según el formato deseado (APA o IEEE).

#### FAQ
Contiene información relevante respectiva a [[maskla.dev#MindNet]], principalmente contesta las preguntas:
- ¿Qué es MindNet?
- La información en mi idioma no tiene sentido
- ¿Cómo puedo asegurar que la información es véridica?
- Si hay información incierta o erronea ¿Cómo puedo puedo corregirla?
- Quisiera contribuir agregando más conocimiento ¿Cómo puedo hacerlo?
- ¿En que idiomas puedo visualizar la información?
- Me gustaría agradecerte por lo que has dado ¿Cómo puedo hacerlo?
- Ocurre un problema con la página ¿Qué puedo hacer?
- Hay información que no entiendo del todo ¿Hay asesorías personales?

Esta página tiene relación directa con [[maskla.dev#Donaciones]] mediante referencias en las preguntas contestadas. Requiere un índice para una navegación fluida.

## Portfolio
Portfolio contiene todos los proyectos trabajados por Maskla y detalles de los mismos. Tiene relación directa con [[maskla.dev#About Maskla]] y [[maskla.dev#Donaciones]].

## About Maskla
Contiene información de Maskla, quien esta detras del proyecto, semblanza, trayectoria y skills técnicas. Hay relación directa con [[maskla.dev#Portfolio]] y [[maskla.dev#Donaciones]].

## Request Review
Contiene un formulario para solicitar una revisión, requiere que el visitante llene información, requiere nombres, correo, motivo y descripción de la revisión. Debe de existir validación por captcha para mejorar la seguridad. Sugerir no colocar información sensible. Dar opcion de anonimato.

## Donaciones
Redirecciona a un flujo de pago con Stripe para hacer donaciones. Cuando sucede una donacion, enviar correo de agradecimiento.

## Admin Login
No se accede mediante una referencia directa, solo por URL, se recomienda uso de variables del entorno para definir su punto de acceso. Es una pantalla de inicio de sesión, que solicita usuario y contraseña para administrar el sitio. Redirecciona a [[maskla.dev#Dashboard]].

## Dashboard
Es el punto de partida para el direccionamiento a [[maskla.dev#Maskla - SiteMap]], [[maskla.dev#Log]] e [[maskla.dev#Info]]

### Maskla - SiteMap
Contiene y agrupa todos los puntos de entrada del sitio y sus datos asociados. Los grupos son esquemas de la estructura del sitio a excepcion de panel de administración o [[maskla.dev#Dashboard]]. Cada punto de entrada y dato puede ser editado, para ello se debe de redireccional al panel Form.

### Log
Contiene información de los eventos recientes de la página, principalmente donaciones y peticiones de revisión. Las peticiones de revisión redirigen a [[maskla.dev#Form]] para editar directamente. Algunas entradas de eventos pueden marcarse con un estado.

### Info
Contiene información de las métricas del sitio

### Form
Permite editar o agregar datos del sitio. Para facilitar la edición y diferenciación, existen las siguientes variantes:
- Proyecto
	- Título
	- Tecnologias
	- Descripcion breve
	- Imágenes descriptivas
	- Problemática
	- Propuesta de solución
	- Diagramas
	- Devlog
	- Referencia del proyecto
- Trayectoria
	- Fecha inicio
	- Fecha termino
	- Título
	- Descripción
- Tecnología
	- Icóno
	- Tecnología
- Temática
	- Nombre
- Posts (Gestionar por idioma)
	- Título
	- Temática
	- Etiquetas
	- Contenido (Gestionar por bloques)
		1. Contenido (formato, imágenes e insersión de código)
		2. Animaciones
	- Referencias

# Features

## Idioma
El servidor debe de ser capaz de reconocer la localización del visitante, mostrar la información en el idioma por default y realizar un efecto de reemplazado del texto con la localización correcta.