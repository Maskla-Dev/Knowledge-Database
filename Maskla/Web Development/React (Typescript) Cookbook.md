# Dependencias
React se compone de 2 módulos: React-DOM y React. El primero contiene la lógica de renderizado, el segundo la interfaz de acceso al manejo de componentes.
# Componentes puros
Los componentes puros requieren una llamada explícita a la interfaz de creación de componentes mediante `React.createElement(<html element>,<props>,<Contain>)`. Para que un component sea renderizado se requiere obtener el contenedor y especificar el componente raíz de la aplicación (el componente que contiene a todos los demás componentes).

```TSX
ReactDOM.createRoot(document.getElementById('root')).render(
	<React.StrictMode>
		<App/>
	</React.StrictMode>
)
```
# StrictMode
Habilita verificación de los componentes al realizar un doble renderizado, con ello se logra identificar bugs como lo pueden ser componentes sueltos (componentes sin un ID mediante `key`) o mala lógica dentro de `useEffect`.
# Soporte `.tsx` y `.jsx`
El formato de archivos `.tsx` y `.jsx` abstrae 