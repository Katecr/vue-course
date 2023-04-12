<div align="center">
  <h1>VUE </h1>
  <h2>Introducción y Fundamentos</h2>
</div>
<div align="center" style="margin-top:20px;"> 
  <img src="img_readme/logo_vue.jpg" width="100%" title="logo_vue" alt="logo_vue">
</div>

<div style="margin-bottom:50px;"></div>

# Tabla de contenido
1. [Configuración del entorno](#configuración-del-entorno)
2. [Interpolación de datos](#interpolación-de-datos)
3. [Atributos reactivos](#atributos-reactivos)
4. [Eventos de usuario](#eventos-de-usuario)
5. [Inputs reactivos](#inputs-reactivos)
6. [Propiedades computadas](#propiedades-computadas)
7. [Watchers](#watchers)
8. [Estilos reactivos](#estilos-reactivos)
9. [Condicionales](#condicionales)
10. [Listas](#listas)
11. [Componentes](#componentes)
12. [Slots](#slots)
13. Comunicación de componentes
    - [Comunicación de componente padre a hijo ](#comunicación-de-componente-padre-a-hijo)
    - [Comunicación de componente hijo a padre](#comunicación-de-componente-hijo-a-padre)
14. [Custom v-model](#custom-v-model)
15. [Comunicación con componentes profundos](#comunicación-con-componentes-profundos)
16. [Instancias de componentes](#instancias-de-componentes)

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

<div style="margin-bottom:50px;"></div>

## Atributos reactivos
---

`v-bind:` es una directiva que se pone antes del atributo al cual su valor quiero cambiar dinamicamente. una conjugacion para "v-bind: " es " : "

Ejemplos:
```html
<img v-bind:src="link_img" alt="img_vue" title="img_vue" />
```
```html
<img :src="img" alt="img_vue" title="img_vue" />
```

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                attr:"src",
                link_img: "https://fastly.picsum.photos/id/25/200/300.jpg?hmac=ScdLbPfGd_kI3MUHvJUb12Fsg1meDQEaHY_mM613BVM"
            };
        },
        template: `<img v-bind:[attr]="link_img"/>`
    }).mount('#app');
    console.log(vm);
</script>
```

<div style="margin-bottom:50px;"></div>

## Eventos de usuario
---

Se puede realizar con vue todos los eventos de un formulario como clic, touch, submit, keyup etc.

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                counter: 0
            };
        },
        methods:{
            increment(){
                this.counter++;
            },

            decrement() {
                this.counter--;
            },

            reset() {
                this.counter = 0;
            }
        },
        template: `
            <button v-on:click="increment">+</button>
            <button v-on:click="decrement">-</button>
            <button v-on:click="reset">Reset</button>
            <p>{{counter}}</p>
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>


## Inputs reactivos
---

Como vue se encarga de sincronizar la vista con el modelo o viceversa.

1. Cuando se lea un cambio en un input
```javascript
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Hello vue!'
            };
        },
        methods:{
            input(e){
                this.text = e.target.value;
            }
        },
        template: `
            <p>{{ text }}</p>
            <input type="text" v-on:change="input" />
        `
    }).mount('#app');
</script>
```

2. Cuando se escriba en tiempo real
```javascript
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Hello vue!'
            };
        },
        methods:{
            input(e){
                this.text = e.target.value;
            }
        },
        template: `
            <p>{{ text }}</p>
            <input type="text" v-on:input="input" />
        `
    }).mount('#app');
</script>
```

> Para no copiar toda la sintaxis de eventos: v-on y atributos: v-bind, se puede resumir de la siguiente manera:
```v-on``` = @
```v-bind``` = :

```javascript
<input type="text" v-on:input="input" v-bind:value="text" />
<input type="text" @input="input" :value="text" />
```

3. La directiva v-model: ara crear bindings de datos bidireccionales (two-way binding) en elementos input, textarea y select de un formulario.

```javascript
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Hello vue!'
            };
        },
        template: `
            <p>{{ text }}</p>
            <input type="text" v-model='text' />
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>


## Propiedades computadas
---

Nos sirve para realizar lógica con nuestros datos

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                firstname: 'Kate',
                lastname: 'Castaño!',
                now: new Date()
            };
        },
        computed:{
            fullName(){
                return this.firstname + ' ' + this.lastname;
            },

            today(){
                return this.now.toLocaleDateString();
            }
        },
        template: `
            <div>{{ fullName }}</div>
            <div>{{ today }}</div>
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>


## Watchers
---

Un observador en Vue es una característica especial que nos permite observar algunos datos y realizar acciones específicas cuando cambian.

1. tiene como regla que debe ser el mismo nombre de la variable que se quiera escuchar

2. puedes obtener parametros, nuevo valor y viejo valor

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Hello vue!'
            };
        },
        watch: {
            text(value, old){
                console.log('Whatcher',value, old);
            }
        },
        template: `{{ text }}`
    }).mount('#app');
</script>
```

> Ejemplo abrir y cerrar puerta

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app"></div>
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Puerta cerrada',
                open: false
            };
        },
        watch: {
            //tiene como regla que debe ser el mismo nombre de la variable que se quiera escuchar
            open(value){
                if (value){
                    this.text = 'Puerta abierta';
                }else {
                    this.text = 'Puerta cerrada';
                }
            }
        },
        computed:{
            label(){
                this.open ? "Cerrar" : "Abrir";
            }
        },
        template: `<div>{{ text }}</div>
        <button @click="open = !open">{{ label }}</button>
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>


## Estilos reactivos
---

Para utilizar estilos en el template de vue, se pueden de dos maneras con style y con clases

1. ***style**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conexión CDN</title>
    <style>
        html,
        body {
            height: 100vh;
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
        }
    
        #app,
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 100%;
            height: 100%;
        }
    
        button {
            margin-top: 24px;
            border: none;
            background-color: white;
            padding: 8px 24px;
            border-radius: 12px;
        }
    </style>
</head>
<body>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <div id="app"></div>
    <script>
        const vm = Vue.createApp({
            data() {
                return {
                    text: 'Puerta cerrada',
                    open: false,
                    styles:{
                        backgroundColor: '#eca1a6'
                    }
                };
            },
            watch: {
                open(value) {
                    if (value) {
                        this.text = 'Puerta abierta';
                        this.styles.backgroundColor = "#b5e7a0";
                    } else {
                        this.text = 'Puerta cerrada';
                        this.styles.backgroundColor = "#eca1a6";
                    }
                }
            },
            computed: {
                label() {
                    this.open ? "Cerrar" : "Abrir";
                }
            },
            template: `
                <div class="container" :style="styles">
                    <h2>{{ text }}</h2>
                    <button @click="open = !open">{{ open ? "Cerrar" : "Abrir" }}</button>
                </div>
            `
        }).mount('#app');
    </script>
</body>
</html>
```

1. ***clases**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conexión CDN</title>
    <style>
        html,
        body {
            height: 100vh;
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
        }
    
        #app,
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 100%;
            height: 100%;
        }
    
        button {
            margin-top: 24px;
            border: none;
            background-color: white;
            padding: 8px 24px;
            border-radius: 12px;
        }
    
        .closed {
            background-color: #eca1a6;
        }
    
        .open {
            background-color: #b5e7a0;
        }
    </style>
</head>
<body>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <div id="app"></div>
    <script>
        const vm = Vue.createApp({
            data() {
                return {
                    text: 'Puerta cerrada',
                    open: false
                };
            },
            watch: {
                open(value) {
                    if (value) {
                        this.text = 'Puerta abierta';
                    } else {
                        this.text = 'Puerta cerrada';
                    }
                }
            },
            computed: {
                label() {
                    this.open ? "Cerrar" : "Abrir";
                },

                bgColor() {
                    return this.open ? 'open' : 'closed';
                },
            },
            template: `
                <div class="container" :class="bgColor">
                    <h2>{{ text }}</h2>
                    <button @click="open = !open">{{ open ? "Cerrar" : "Abrir" }}</button>
                </div>
            `
        }).mount('#app');
    </script>
</body>
</html>
```

<div style="margin-bottom:50px;"></div>

## Condicionales
--- 

Se pueden utilizar condicionales dentro de los templates, se utiliza las directivas:  ```v-if``` y ```v-else```
```javascript
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Acceder a tu cuenta',
                open: false,
                username: ""
            };
        },
        watch: {
            open(value) {
                if (value) {
                    this.text = 'Cerrar sesión';
                } else {
                    this.text = 'Acceder a tu cuenta';
                    this.username = "";
                }
            }
        },
        computed: {
            textButton() {
                return this.open ? 'Salir' : 'Acceder';
            },

            bgColor() {
                return this.open ? ['open'] : ['closed'];
            },
        },
        template: `
            <div class="container" :class="bgColor">
                <h2>{{ text }}</h2>
                <div v-if="open">
                    <p>Hola, {{ username }}</p>
                </div>
                <div v-else>
                    <div>Username</div>
                    <input type="text" v-model="username" />    
                </div>
                <button @click="open = !open">
                    <div v-if="!open">Acceder</div>
                    <div v-else>Salir</div> 
                </button>
            </div>
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>

## Listas
--- 

vue permite iterar una lista con la directiva ```v-for```

1. 
```javascript 

<div v-for="item in posts" class="item">
    <div class="title">{{ item.title }}</div>
    <p>{{ item.description }}</p>
</div>
```

2. Un id unico para cada item iterado
```javascript 
<div v-for="(item, i) in posts" :key="i" class="item">
    <div class="title">{{ item.title }}</div>
    <p>{{ item.description }}</p>
</div>
```

Ejemplo:

```javascript
<script>
    const vm = Vue.createApp({
        data() {
            return {
                text: 'Acceder a tu cuenta',
                open: false,
                username: "",
                posts: [{
                    title: "Titulo 1",
                    description: "Lorem ipsum..."
                }, {
                    title: "Titulo 2",
                    description: "Lorem ipsum..."
                }, {
                    title: "Titulo 3",
                    description: "Lorem ipsum..."
                }, {
                    title: "Titulo 4",
                    description: "Lorem ipsum..."
                }]
            };
        },
        watch: {
            open(value) {
                if (value) {
                    this.text = 'Cerrar sesión';
                } else {
                    this.text = 'Acceder a tu cuenta';
                    this.username = "";
                }
            }
        },
        computed: {
            textButton() {
                return this.open ? 'Salir' : 'Acceder';
            },

            bgColor() {
                return this.open ? ['open'] : ['closed'];
            },
        },
        template: `
            <div class="container" :class="bgColor">
                <h2>{{ text }}</h2>
                <div v-if="open">
                    <p>Hola, {{ username }}</p>
                    <div class="list">
                        <div v-for="(item, i) in posts" :key="i" class="item">
                            <div class="title">{{ item.title }}</div>
                            <p>{{ item.description }}</p>
                        </div>
                    </div>
                </div>
                <div v-else>
                    <div>Username</div>
                    <input type="text" v-model="username" />    
                </div>
                <button @click="open = !open">
                    <div v-if="!open">Acceder</div>
                    <div v-else>Salir</div> 
                </button>
            </div>
        `
    }).mount('#app');
</script>
```

<div style="margin-bottom:50px;"></div>

## Componentes
--- 

Reutilizar código por medio de componentes 

1. Separar en una variable el createApp
```javascript
const app = Vue.createApp({});
```

2. Guardar en otra variable el mount
```javascript
const vm = app.mount('#app');
```

3. Crear un componente, el primer atributo es el nombre del componente
```javascript
app.component('item', {
    props:['post'],
    template:`
        <div class="item">
            <div class="title">{{ post.title }}</div>
            <p>{{ post.description }}</p>
            <button @click="deletePost(i)">
                <div>Eliminar</div>
            </button>
        </div>
    `
});
```

4. Llamar el componente
```javascript
<div class="list">
    <item v-for="(item, i) in posts" :key="i" :post="item"  />
</div>
```


<div style="margin-bottom:50px;"></div>

## Slots
--- 

los slots sirven para aprovechar la sintaxis de HTML y definir un contenedor hijo independientemente de la etiqueta html

```javascript
<script>
    const app = Vue.createApp({
        template: `
        <div>
            <v-header>Titulos</v-header>
            <div>Lorem ipsum dolor </div>
        </div>
        `
    });
    app.component("v-header", {
        template:`<header><slot></slot></header>`
    })
    const vm = app.mount('#app');
</script>
```

Se pueden tener contenedores dentro de contendores así:
```javascript
app.component("v-layout", {
    template:`
        <header>
            <slot name="title"></slot>
        </header>
        <div>
            <slot name="content"></slot>
        </div>
    `
})
```

Cuando se utilizan mas de dos slot se deben nombrar y tener como identificarlo, su nombre inicial es default.
```javascript
<slot name="content"></slot>
```

La forma de asignarle el valor es con la etiqueta ```v-slot:nombre_del_slot```
```javascript
<template v-slot:title>Titulo</template>
```

Cuando se tienen dos o mas etiquetas en un mismo componente deben accederse a traves de template
```javascript
<v-layout>
    <template v-slot:title>Titulo</template>
    <template v-slot:content>Lorem lorem</template>
</v-layout>
```


<div style="margin-bottom:50px;"></div>

## Comunicación de componente padre a hijo
--- 

La sintaxis de props permite enviar datos de componentes padre a componentes hijo de forma reactiva, se utiliza como una variable local que viene desde una parte externa.

> Es una mala práctica cambiar el valor del prop sin avisar al componente padre


```javascript
app.component("v-item",{
    props: {
        text: {
            default: "Texto vacío"
        }
    },
    template:`
    <li>
        {{text}}
    </li>
    `
} )
```

> La sintaxis en props se puede simplificar a una lista, sin embargo se considera una buena práctica escribirlo como el ejemplo.

> https://vuejs.org/guide/components/props.html#prop-validation


<div style="margin-bottom:50px;"></div>

## Comunicación de componente hijo a padre
--- 

Para la comunicación de hijo a padre e pueden crear eventos que retornen valores y ejecuten código, en el ejemplo a continuación se crea un método en el componente hijo que es llamado al hacer click, el método dispara un evento que es escuchado desde el componente padre, se utiliza la sintaxis ```$emit```:

```javascript
<script>
    const app = Vue.createApp({
        data() {
            return {
                items: ["uno", "dos", "tres"]
            };
        },
        methods: {
            remove(i) {
                const items = this.items.filter((el, index) => index !== i);
                this.items = items;
            }
        },
        template: `
                <ul>
                    <v-item
                        v-for="(item, i) in items"
                        v-bind:text="item"
                        v-on:remove="remove(i)"
                    />
                </ul>
            `
    });

    app.component("v-item", {
        props: {
            text: String
        },
        methods: {
            rm() {
                this.$emit("remove");
            }
        },
        template: `<li v-on:click="rm">{{ text }}</li>`
    });

    const vm = app.mount("#app");
</script>
```

<div style="margin-bottom:50px;"></div>

## Custom v-model
--- 

Permite una comunicacion en dos sentidos entre el padre y el hijo, se debe especificar el prop del componente y la variable involucrada

```javascript
v-model:propValue="variableValue"
```

Ejemplo:
```javascript
<script>
    const app = Vue.createApp({
            data() {
                return {
                    text: "Hola Vue"
                };
            },
            template: `
            <div>
                <p>{{ text }}</p>
                <v-input v-model:value="text" />
            </div>
        `
        });

        app.component("v-input", {
            props: {
                value: String
            },
            methods: {
                input(e) {
                    this.$emit("update:value", e.target.value);
                }
            },
            template: `<input type="text" v-bind:value="value" v-on:input="input" />`
        });

    
    const vm = app.mount("#app");
</script>
```

<div style="margin-bottom:50px;"></div>

## Comunicación con componentes profundos
--- 

Un componente profundo es cuando un componente no es directamente hijo de un elemento padre

<div align="center" style="margin-top:20px;"> 
  <img src="img_readme/components_provide.png" width="100%" title="components" alt="components">
</div>

```javascript
<script>
    const app = Vue.createApp({
        data() {
            return {
                text: "Hola Vue"
            };
        },
        provide() {
            return {
                otroTexto: this.text
            };
        },
        template: `
                <div>{{ text }}</div>
                <otro />
            `
    });

    app.component("otro", {
        template: `<tercer />`
    });

    app.component("tercer", {
        inject: {
            otroTexto: {
                from: "otroTexto",
            }
        },
        template: `<div>{{ otroTexto }}</div>`
    });

    const vm = app.mount("#app");
</script>
```

<div style="margin-bottom:50px;"></div>

## Instancias de componentes
--- 

Una instancia es una copia de un componente de Vue. Estas instancias sirven para acceder a partes de DOM con vue

1. Usando ```vm.$root``` devuelve el objet raiz, el ue contiene todo el árbol de componentes de la aplicación
2. Usando ```vm.$el``` se accede al componente html de la aplicación
3. Para acceder a referencias especificas a un componente ```vm.$refs```.
4. Para props, ```vm.$props``` de esta forma se puede interactuar con Vue y JavaScript Vanila de forma progresiva.

> https://lenguajejs.com/vuejs/componentes/instancias-vue/