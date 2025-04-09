---
title: ¿Cuál es la diferencia entre exportaciones por defecto y nombradas en JavaScript?
date: 2024-08-27T13:29:01.694Z
author: Yazdun Fadali
authorURL: https://www.freecodecamp.org/news/author/yazdun/
originalURL: https://www.freecodecamp.org/news/difference-between-default-and-named-exports-in-javascript/
posteditor: "jesaadev"
proofreader: ""
---

JavaScript es uno de los lenguajes de programación más populares entre los desarrolladores web. Y ofrece múltiples maneras de organizar y compartir código entre diferentes archivos.

<!-- more -->

Al trabajar con módulos, es posible que te encuentres con dos formas comunes de exportar: exportaciones por defecto y exportaciones nombradas.

Comprender la diferencia entre estos dos métodos es esencial para gestionar eficazmente tu base de código y hacerla más mantenible.

En este artículo, exploraremos las diferencias entre las exportaciones por defecto y las exportaciones nombradas en JavaScript. Resaltaremos sus casos de uso y las mejores prácticas para ayudarte a elegir el enfoque adecuado para tus proyectos.

## Tabla de Contenidos

-   [Lo que aprenderás][1]
-   [Como empezar][2]
-   [¿Qué son los módulos de JavaScript][3]?
-   [¿Qué es exactamente la palabra clave export en JavaScript][4]?
-   [¿Qué es la exportación por defecto en JavaScript][5]?
-   [¿Qué es la exportación nombrada en JavaScript][6]?
-   [Cómo crear una aplicación sencilla usando módulos de JavaScript][7]
-   [Conclusión][8]

## Lo que aprenderás

En este tutorial, primero aprenderás sobre los módulos de JavaScript y cómo hacen que la codificación sea mejor y más fácil de gestionar. Explorarás exportaciones por defecto y exportaciones nombradas, comprendiendo cuándo usar cada uno de ellos.

Para poner todo en práctica, crearás una simple aplicación de cambio de color que une todos los conceptos, haciendo que tu experiencia de aprendizaje sea práctica.

También he creado un video tutorial basado en este artículo. Puedes verlo [aquí en YouTube][9].

Aquí está la [Demostración en Vivo][10] de lo que estaremos creando:

![Hay un botón en el centro de la pantalla, puede hacer clic en este botón y cambiar el color de fondo del elemento del cuerpo](https://www.freecodecamp.org/news/content/images/2023/08/ezgif-5-d38eb39cfc--1-.gif)

Aplicación de cambio de color

## Como empezar

Para comenzar con este tutorial, ya he preparado un proyecto de plantilla que contiene todas las dependencias necesarias. Esto elimina la necesidad de configurar tu proyecto desde cero.

Simplemente clona el [proyecto de plantilla][11] desde el repositorio de GitHub y luego sigue el tutorial. De esta manera, puedes centrarte en aprender e implementar los conceptos sin quedar atrapado en los detalles de configuración.

Código fuente en GitHub (por favor dale una estrella si disfrutas del tutorial ⭐️):

-   Plantilla Inicial: [Ver en GitHub][12]
-   Versión Final: [Ver en GitHub][13]

Una vez que hayas configurado la plantilla inicial y la hayas ejecutado exitosamente en tu máquina local, puedes pasar a la siguiente sección.

## ¿Qué son los módulos de JavaScript?

Imagina que tienes un proyecto grande y complejo en JavaScript, con muchos archivos y funciones diferentes. ¡Puede volverse desordenado y difícil de gestionar todo ese código!

Bueno, los módulos de JavaScript son como pequeños contenedores que te ayudan a organizar mejor tu código y hacerlo más fácil de usar y mantener.

Piensa en un módulo como una caja separada donde puedes poner código relacionado. Dentro de esta caja, puedes tener variables, funciones o incluso clases que trabajan juntas para realizar tareas específicas. Estos módulos actúan como pequeñas unidades autónomas que pueden ser reutilizadas fácilmente en diferentes partes de tu proyecto.

Una de las características esenciales de los módulos de JavaScript es que te permiten decidir qué partes del código quieres compartir con otras partes del proyecto. Puedes elegir exportar ciertas funciones o datos de un módulo, haciéndolos accesibles a otras partes de tu base de código.

Por otro lado, también puedes importar código de otros módulos cuando necesites utilizar su funcionalidad. Es como pedir herramientas prestadas de la caja de herramientas de un amigo cuando necesitas arreglar algo.

Los módulos de JavaScript nos ayudan a:

1.  **Organizar código**: Los módulos te permiten agrupar código relacionado en archivos separados, haciendo tu proyecto más organizado y manejable.
2.  **Encapsular código**: Cada módulo actúa como una unidad autónoma, por lo que puedes ocultar ciertas partes del código y solo exponer lo que quieres que otros usen.
3.  **Reutilizabilidad**: Puedes reutilizar módulos fácilmente en diferentes partes de nuestro proyecto, reduciendo la duplicación de código y promoviendo un proceso de desarrollo más eficiente.
4.  **Gestión de dependencias**: Los módulos te ayudan a manejar dependencias entre diferentes partes del proyecto, facilitando el seguimiento de cómo encaja todo.

Para comprender mejor este concepto, vamos a crear un juego sencillo y divertido. Crearemos una clase de JavaScript para una mascota virtual. Esta mascota tendrá un nombre y una especie, y podrás interactuar con ella jugando y alimentándola:

```javascript
// 📂 Pet.js

export class VirtualPet {
  constructor(name, species) {
    this.name = name;
    this.species = species;
    this.energy = 100;
  }

  // Jugar con la mascota
  play() {
    this.energy -= 10;
    this._checkStats();
  }

  // Alimentar a la mascota
  feed() {
    this.energy += 20;
    this._checkStats();
  }
```


```javascript
if (this.energy < 0) {
  this.energy = 0;
}
}

// Obtener el estado de la mascota
getStatus() {
  return `${this.name} el ${this.species} - Energía: ${this.energy}`;
}
}
```

La palabra clave `export` es una parte fundamental de este sistema de módulos, permitiéndote exponer partes específicas de tu código para ser usadas en otros archivos.

Al usar `export`, puedes hacer que tu clase `VirtualPet` esté disponible para otras partes de tu aplicación o incluso en archivos completamente separados.

Esto te permite encapsular el comportamiento de la mascota dentro de su propio módulo, promoviendo la modularidad del código y previniendo el acceso no deseado a funcionalidades internas.

Ahora, puedes importar la clase `VirtualPet` desde el módulo `pet.js` usando la declaración `import` en otro archivo:

```javascript
// 📂 Play.js

import { VirtualPet } from './pet.js';

const myPet = new VirtualPet("Fido", "Perro");

console.log(myPet.getStatus()); // Fido el Perro - Energía: 100

myPet.play();
console.log(myPet.getStatus()); // Fido el Perro - Energía: 90

myPet.feed();
console.log(myPet.getStatus()); // Fido el Perro - Energía: 100
```

¡Buen trabajo! Has creado exitosamente una mascota virtual usando módulos de JavaScript. 🎉

En esta sección, aprendiste sobre los módulos de JavaScript y cómo la palabra clave `export` te ayuda a organizar y compartir código de manera efectiva. En la próxima sección, aprenderás más sobre los diferentes métodos de exportar e importar módulos de JavaScript a través de varios archivos.

## ¿Qué es exactamente la palabra clave `export` en JavaScript?

En JavaScript, la declaración `export` se utiliza en módulos para exponer variables, funciones o clases de modo que puedan ser accesadas y usadas en otras partes de la aplicación o en archivos separados.

Al usar `export`, haces que ciertas partes de tu código sean accesibles fuera del módulo. Esto te permite reutilizar y promover una estructura de código modular y organizada.

En JavaScript, hay dos formas principales de exportar valores: exportaciones por defecto, utilizadas para un solo valor por archivo, y exportaciones nombradas, que permiten múltiples exportaciones por archivo.

## ¿Qué es la exportación por defecto en JavaScript?

En JavaScript, una exportación por defecto es una manera de compartir un único valor, función o clase como el principal elemento de un archivo con otras partes de tu código.

Cuando tienes un archivo que necesita ser utilizado en otras partes de tu aplicación, puedes marcar un elemento en ese archivo como la exportación por defecto usando la sintaxis `export default`.

Esto significa que cuando importas desde ese archivo en otra parte de tu código, no necesitas usar llaves `{}` alrededor de la declaración de importación. En su lugar, puedes darle cualquier nombre que quieras durante la importación, lo que lo hace más conveniente de usar.

```js
// 📂 math.js
const add = (a, b) => a + b;
export default add;

// 📂 main.js
import myAddFunction from './math.js';
const result = myAddFunction(5, 10); // Esto llamará a la función add de math.js y almacenará el resultado en la variable 'result'.
```

## ¿Qué es la exportación nombrada en JavaScript?

Las exportaciones nombradas en JavaScript te permiten exportar múltiples funciones, variables o clases de un solo archivo como entidades separadas. En lugar de exportar todo como una sola unidad, puedes nombrar y exportar cada parte individualmente.

Esto te da más control sobre qué partes del código quieres compartir con otros módulos. Cuando importas estas exportaciones nombradas en otros archivos, tienes que usar los nombres exactos que se usaron durante la exportación, asegurando que puedes acceder y usar las funcionalidades específicas que necesitas del archivo fuente.

```javascript
// 📂 math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// 📂 main.js
import { add, subtract } from './math.js';

const result1 = add(5, 3); // result1 será 8
const result2 = subtract(10, 4); // result2 será 6
```

En JavaScript, un archivo puede tener solo una exportación por defecto, pero puede tener tantas exportaciones nombradas como sea necesario.

Vamos a ver las diferencias entre las exportaciones nombradas y las exportaciones por defecto:

### Exportaciones Nombradas vs Exportaciones por Defecto:

Algunas características de las exportaciones nombradas son las siguientes:

-   Cuando usas exportaciones nombradas, puedes exportar múltiples valores, funciones o clases de un archivo, dando a cada uno de ellos un nombre específico.
-   Necesitas envolver los elementos que quieres exportar en llaves `{}` al importarlos en otro archivo, y debes usar los nombres exactos que se usaron durante la exportación.
-   Las exportaciones nombradas son excelentes cuando quieres compartir múltiples cosas de un archivo y darles nombres distintivos para usarlos en otras partes de tu código.
-   Un archivo puede tener tantas exportaciones nombradas como desees.

Algunas características de las exportaciones por defecto son las siguientes:

-   Las exportaciones por defecto son útiles cuando quieres exportar solo una cosa principal de un archivo. Es como marcar esa cosa como la más importante para compartir.
-   Al importar una exportación por defecto en otro archivo, puedes darle cualquier nombre que quieras durante la importación, y no necesitas usar llaves `{}`.
-   Un archivo puede tener solo una exportación por defecto.

### Cómo combinar exportaciones nombradas y por defecto:

Es importante notar que un archivo puede tener tanto exportaciones nombradas como por defecto juntas.

Esto significa que puedes exportar una cosa principal usando `export default`, mientras también exportas múltiples valores adicionales usando `export`.
```

## Cómo Crear una Aplicación Simple Usando Módulos de JavaScript

En esta sección final, crearás una genial aplicación de cambio de color usando módulos de JavaScript. Aprenderás cómo dividir tu código en archivos separados, haciéndolo reutilizable en toda tu aplicación y organizándolo de manera efectiva. Entremos en materia y divirtámonos construyendo esta aplicación juntos.

Si aún no lo has hecho, consulta la sección de [Introducción][14] para configurar el proyecto inicial antes de continuar. Esto te permitirá avanzar a lo largo del tutorial.

![image-24](https://www.freecodecamp.org/news/content/images/2023/08/image-24.png)

Una vez que ejecutes el proyecto inicial, podrás ver la siguiente página en tu navegador

Ahora vamos a empezar a codificar. Primero abre `./main.js` y podrás ver el siguiente código:

```javascript
//📂./main.js

import "./style.css";

document.querySelector("#app").innerHTML = `
  <div>
    <button id="flipper" type="button">Start Flipping</button>
  </div>
`;
```

Este código incluye un archivo CSS y establece el contenido del elemento con el ID "app" en un div que contiene un botón con el ID "flipper" y el texto "Start Flipping".

A continuación, agregarás la lógica de JavaScript para implementar la funcionalidad que cambia el color de fondo de la aplicación cuando se hace clic en el botón "Start Flipping".

Para cambiar el color de fondo, puedes usar un array de colores, que ya está preparado para ti dentro de `./colors.js`. Todo lo que tienes que hacer es exportar este array para que puedas usarlo en otros módulos de JavaScript dentro de tu aplicación:

```javascript
//📂./colors.js

const colors = [
  "#007bff",
  "#f1c40f",
  "#27ae60",
  "#e74c3c",
  "#8e44ad",
  "#3498db",
  "#f39c12",
];

export default colors;
```

Una vez que añades `export default colors` a este archivo, podrás acceder a esta variable en otros módulos importándola.

Ahora, importemos estos `colors` en `./utils.js` y procedamos a implementar una función que manejará el cambio del color de fondo de tu aplicación:

```javascript
//📂./utils.js

import colorsData from "./colors";

export function getRandomColor() {
  const randomIndex = Math.floor(Math.random() * colorsData.length);
  return colorsData[randomIndex];
}
```

Analicemos el código paso a paso:

1.  `import colorsData from "./colors"`: Esta línea importa los datos del archivo `./colors` en nuestro archivo actual. Los datos de `./colors` se asignan a una variable llamada `colorsData`, que ahora podemos usar en este archivo.
2.  `export function getRandomColor() { ... }`: Esta línea define una función llamada `getRandomColor()`. La función calcula un índice aleatorio del array `colorsData` y devuelve el color en ese índice.

Ahora hablemos de cómo funciona `export default`:

En el archivo `./colors`, hay una `exportación por defecto` del array `colors`. Al usar `export default`, podemos importar directamente el valor exportado sin necesidad de usar llaves `{}` alrededor al importarlo.

Por ejemplo, si fueras a importar múltiples valores del archivo `./colors`, usarías llaves `{}`. Pero como solo hay una exportación por defecto en el archivo `./colors`, puedes importarlo directamente sin la necesidad de llaves.

Además, puedes elegir cualquier nombre que desees al importar una exportación por defecto. En este caso, lo llamaste `colorsData`, pero podrías haber usado cualquier otro nombre y aún así funcionaría de la misma manera.

Para el siguiente paso, importemos la función `getRandomColor` que acabas de crear en el archivo `./main.js` y úsala para cambiar el color de fondo de tu aplicación:

```javascript
//📂./main.js

import "./style.css";
import { getRandomColor } from "./utils";

document.querySelector("#app").innerHTML = `
  <div>
    <button id="flipper" type="button">Start Flipping</button>
  </div>
`;

document.querySelector("#flipper").addEventListener("click", () => {
  const body = document.body;
  const randomColor = getRandomColor();
  body.style.backgroundColor = randomColor;
});
```

En este código, usaste importación por nombre para acceder a la función `getRandomColor` del archivo `./utils`. La declaración `import { getRandomColor } from "./utils"` te permite importar específicamente la función `getRandomColor` por su nombre exacto desde el módulo `./utils`.

Una vez que importas la función `getRandomColor`, puedes usarla directamente en tu código sin prefijo o modificación alguna. Por ejemplo, llamas a `getRandomColor()` sin necesidad de especificar el módulo del que proviene. Esto hace el código más limpio y directo.

Usar importaciones por nombre te permite elegir precisamente qué funciones, variables o constantes quieres importar de un módulo. Esto hace que sea fácil acceder solo a las partes específicas del código que necesitas en tu archivo actual. También ayuda a mantener tu código organizado y permite un mejor control sobre qué funcionalidades usas de diferentes módulos.

Ten en cuenta que con las importaciones por nombre, el nombre debe coincidir en ambos lados.

¡Gran trabajo hasta ahora! Aquí está el resultado actual:

![Este es un adelanto de la aplicación de cambio de color, hay un botón en el centro de la pantalla y una vez que haces clic en él, cambia el color de fondo del cuerpo del documento](https://www.freecodecamp.org/news/content/images/2023/08/ezgif-1-6b91c14ad7.gif)

Ahora, vamos a crear otra función de utilidad que cambiará el texto del botón para mostrar el valor hexadecimal del color actual:

```javascript
//📂./utils.js

import colorsData from "./colors";

export function getRandomColor() {
  const randomIndex = Math.floor(Math.random() * colorsData.length);
  return colorsData[randomIndex];
}

export function changeButtonText(text, element) {
  const button = document.querySelector(element);
  button.innerText = text;
}
```

`changeButtonText` te permitirá cambiar el texto que se muestra en un botón. Puedes llamar a esta función con dos parámetros: el `texto` que quieres mostrar en el botón y el `elemento` que representa el selector del botón. Una vez llamada, la función actualizará el texto del botón con el `texto` especificado.

Añadamos esto a `./main.js` y veamos cómo funciona en acción:

```javascript
//📂./main.js

import "./style.css";
import { getRandomColor, changeButtonText } from "./utils";

document.querySelector("#app").innerHTML = `
  <div>
    <button id="flipper" type="button">Start Flipping</button>
  </div>
`;

document.querySelector("#flipper").addEventListener("click", () => {
  const body = document.body;
  const randomColor = getRandomColor();
  changeButtonText(`Current Color is ${randomColor}`, "#flipper");
  body.style.backgroundColor = randomColor;
});
```

Has importado la función `changeButtonText` usando importación con nombre desde el archivo `./utils`. La función toma dos argumentos: el texto que queremos mostrar en el botón y el selector del botón que queremos actualizar. Cambia dinámicamente el texto del botón para mostrar el texto especificado con el valor del color actual.

Aquí está el resultado final:

![There is a button in the middle of the screen, you can click on this button and change the background color of the body element](https://www.freecodecamp.org/news/content/images/2023/08/ezgif-5-d38eb39cfc--1-.gif)

Resultado final

Eso es todo – ¡felicitaciones por construir tu aplicación de cambio de color utilizando módulos de JavaScript! 🎉

El enfoque modular te ayuda a organizar y reutilizar tu código de manera eficiente, haciendo que tu aplicación sea funcional y fácil de mantener. ¡Bien hecho!

## Conclusión

En conclusión, las exportaciones de JavaScript ofrecen herramientas poderosas para gestionar la organización del código y compartir funcionalidades entre diferentes partes de nuestras aplicaciones.

Exploramos las diferencias entre exportaciones con nombre, que permiten exportar múltiples entidades desde un archivo con nombres específicos, y exportaciones por defecto, que marcan una entidad principal como la exportación principal. Ambos mecanismos son esenciales para promover la modularidad y la reutilización del código.

Al entender estas técnicas de exportación, puedes crear estructuras de código más organizadas y eficientes, resultando en una mejor escalabilidad en tus proyectos de JavaScript.

¡Gracias por leer hasta el final! Puedes seguirme en [Twitter][15] donde comparto más consejos útiles sobre desarrollo web. ¡Feliz codificación!

[1]: #what-you-will-learn
[2]: #getting-started
[3]: #what-are-javascript-modules
[4]: #what-exactly-is-the-export-keyword-in-javascript
[5]: #what-is-the-default-export-in-javascript
[6]: #what-is-the-named-export-in-javascript
[7]: https://www.freecodecamp.org/news/p/a393357b-0fad-4f0d-8f01-d2a3e1d62854/how-to-create-a-simple-app-using-javascript-modules
[8]: https://www.freecodecamp.org/news/p/a393357b-0fad-4f0d-8f01-d2a3e1d62854/conclusion
[9]: https://youtu.be/YHRXgUeF1dA
[10]: https://fcc-javascript-modules.netlify.app/
[11]: https://github.com/Yazdun/fcc-javascript-modules/tree/starter
[12]: https://github.com/Yazdun/fcc-javascript-modules/tree/starter
[13]: https://github.com/Yazdun/fcc-javascript-modules
[14]: #getting-started
[15]: https://twitter.com/Yazdun

