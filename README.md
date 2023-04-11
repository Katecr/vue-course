<div align="center">
  <h1>VUE </h1>
  <h2>Introducción y Fundamentos</h2>
</div>
<div align="center" style="margin-top:20px;"> 
  <img src="img_readme/logo_vue.jpg" width="100%" title="logo_fastapi" alt="logo_fastapi">
</div>

<div style="margin-bottom:50px;"></div>

## Configuración del entorno
---

1. Instalamos el cli de vue con el comando:

```bash
npm i -g vue-cli
```

2. Instalamos el complemento del navegador si deseamos

```bash
https://devtools.vuejs.org/guide/installation.html
```

3. Creamos la carpeta del proyecto

```bash
mkdir nombre_carpeta
```

4. Utilizar VUE por CDN

```bash
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

> Ejemplo:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conexión CDN</title>
</head>
<body>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <div id="app">{{ text }}</div>
    <script>
        Vue.createApp({
            data() {
                return {
                    text: 'Hello Word!'
                }
            }
        }).mount('#app')
    </script>
</body>
</html>
```

<div style="margin-bottom:50px;"></div>

## Interpolación de datos
---

La interpolación de datos hace referencia a la forma como se trabaja con variables dentro de los componentes Vue. Estas variables utilizan la sintaxis de doble llaves {{ text }}