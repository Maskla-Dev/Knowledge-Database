El acceso al lienzo requiere `<canvas>` en el DOM, solo admite como atributos `width` y `height`. El lienzo expone un contexto que permite manipularlo, para acceder a este mismo utilizar `getContext()`, si el navegador no es compatible, retornará `undefined`.

```javascript
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");
```

