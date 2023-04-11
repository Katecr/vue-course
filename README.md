<div align="center">
  <h1>VUE </h1>
  <h2>Introducción y Fundamentos</h2>
</div>
<div align="center" style="margin-top:20px;"> 
  <img src="img_readme/logo_vue.jpg" width="100%" title="logo_fastapi" alt="logo_fastapi">
</div>

<div style="margin-bottom:50px;"></div>

# Tabla de contenido
1. [Configuración del entorno](#configuración-del-entorno)
2. [Interpolación de datos](#interpolación-de-datos)


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

4. Creamos un archivo .html

```bash
touch index.html
```

5. Utilizar VUE por CDN: conectamos el script en el achivo .html debajo de body

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

***Directivas:*** son atributos que se pueden agregar al html para añadir nueva funcionalidad a la plantilla estatica. 

> Generalmente las directivas de Vue.js empiezan con v-

> Para generar las comillas `` Alt + 96

> Ctrl + Shift + u, después, 60h para los usuarios de Unix

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Hello Word!'
            }
        },
        template: `<div v-once v-text="text"></div>` //Actualice el contenido de texto del elemento y no permite modificaciones
    }).mount('#app');
    console.log(vm);
</script>
```

> https://vuejs.org/api/built-in-directives.html#v-text

> Se pueden customizar directivas: https://vuejs.org/guide/reusability/custom-directives.html#directive-hooks

La directiva `v-html` permite usar html dentro de las variables, hay que tener cuidado para que no se pueda ejecutar código a través de por ejemplo un input de usuario. No se recomienda que los ingresos en html tengan que ver con ingresos de usuario.

```js
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: '<p>Hello Word!</p>'
            }
        },
        template: `<div v-html='text'><div/>`
    }).mount('#app');
    console.log(vm);
</script>
```

