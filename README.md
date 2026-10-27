# Kopius - The Academy Cohort 05 - Clase 1 de NodeJS

<p align="center">
  <a href="https://nodejs.org/en" target="blank"><img src="https://user-images.githubusercontent.com/3438503/260495760-ca5d8c24-b382-43d9-8fbe-d905b4b208f0.png" width="300" alt="NodeJS Logo" /></a>
</p>

## Contenido

### Preguntas comunues sobre Node

1. ¿Qué es Node?

Node es básicamente un ambiente de ejecicuón para ejecutar JavaScript desligado del navegador web o mejor conocido como Runtime environment.

2. ¿Qué lo hace tan especial?

Código abierto con el motor V8 de Google Chrome y está diseñado para realizar tareas de E/S(I/O) junto con el manejo de archivo de computadora cliente/servido.

**Caracteristicas**

- Asincronía
- Módulos nativos y de terceros
- Gestión de paquetes con NPM
- Escalabilidad
- Múltiple plataforma

3. ¿Qué es No-Blocking I/O?

Es una caracteristica de Node que permite ejecutar instrucciones en paralelo que no bloquean todo el hilo, donde casi el 99% de las funciones de node se ejecutar en modo no bloqueando y esto lo logra a la libreria libuv.

**Blocking**
Básicamente cuando la ejecución del código debe de esperar a que se complete el proceso pero esta a su vez impide que se sigan ejecutando otras instrucciones en paralelo.

4. NPM vs. NPX

**NPM (Node package manager)** es el gestor de paquetes para node con mayor crecimiento en paquetes desplegados y ya viene instalado con Node.

<p></p>

**NPX (Node package execute)** es una herramienta del ecosistema de Node.js que permite ejecutar comandos de paquetes de npm sin necesidad de instalarlos globalmente.

Referencias

- https://nodejs.org/learn/asynchronous-work/overview-of-blocking-vs-non-blocking

### Instalaciones y entorno de desarrollo

**Instalaciones requeridas**

- [Visual Studio Code](https://code.visualstudio.com/)
- [Postman](https://www.postman.com/downloads/)
- [Table Plus](https://tableplus.com/)
- [Git](https://git-scm.com/)

```
git config --global user.name "Tu nombre"
git config --global user.email "Tu correo"
```

- [Node](https://nodejs.org/es/)
- [Google Chrome](https://www.google.com.mx/intl/es-419/chrome/?brand=CHBD&gclid=Cj0KCQiAtrnuBRDXARIsABiN-7AAMm13Ae3KDIib46Laxfe6tzD_w4yvDdpq5XsPw1eNlOkZ_0-3x3IaAvLEEALw_wcB&gclsrc=aw.ds)
- [Docker Desktop](https://www.docker.com/get-started)

Descargar imágenes de Docker - Opcional, pero llegaremos a necesitarlas después

```
docker pull postgres:16.15
```

**Instalaciones opcionales**

**Node Version Manager**

- Mac

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.8/install.sh | bash
```

- Windows

```
https://github.com/coreybutler/nvm-windows/releases/download/1.2.2/nvm-setup.exe
```

O

```bash
Invoke-WebRequest `
  -Uri "https://github.com/coreybutler/nvm-windows/releases/download/1.2.2/nvm-setup.exe" `
  -OutFile "$env:USERPROFILE\Downloads\nvm-setup.exe"
```

- Comandos utiles

```bash
# Verificar NVM
nvm version

# Instalar la última versión LTS de Node.js
nvm install lts

# Ver las versiones instaladas
nvm list

# Activar una versión específica
nvm use 24.11.1

# Verificar Node.js
node --version

# Verificar npm
npm --version
```

Referencias

- https://github.com/nvm-sh/nvm
- https://github.com/nvm-windows/nvm

### Primeros pasos con Node (Tarea)

1. Creamos en el directorio de trabajo creamos la carpeta `01-fundamentos`
2. Dentro creamos nuestro primer archivo app.js
3. Usando código JavaScript creamos dos variables
   i. una llamada `message` la inicializamos con el valor de tipo string 'Welcome'
   ii. la segunda `period` y la inicializamos con este código `new Date().getHours() < 12 ? "AM" : "PM";`
4. Necesitamos que escribi un saludo usando nuestra variable message donde si esta es de mañana asiganmos `Good Morninig` y si es de tarde `Good Afternoon`.
5. Al final imprimimos en la consola el resultado del valor de messge.

Ejecutar el programa desde la terminal por linea de comandos.

```bash
node app
```

### Leer y escribir archivos con Node (FileSystem)

El archivo con que vamos a trabajar hay que descargarlo desde:
https://github.com/aduartekopiustech/node-fullstack-clase-01/blob/main/README.md

```javascript
const fs = requiere("fs");

const data = fs.readFileSync("README.md", "utf8");

console.log(data);

fs.writeFileSync("README-COPY.md", data.replace(/Node/gi, "NodeJS"));
```

Tarea

1. Creamos un programa para leer el archivo README-COPY.md
2. Quiero saber cuantas palabras tiene el archivo.
3. Contar las ocurrencias de la palabra NodeJS, implementar case sentitive.

### Orden de ejecución, Event Loop y Node execution

<p align="center">
  <a href="https://nodejs.org/en" target="blank"><img src="https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F22911d4752a44b48a42c7fabae9a64ee?format=webp&width=2000" width="1000" alt="NodeJS Logo" /></a>
</p>

**Quien se ejecuta primero?**
No lo sabemos, es el `Event Loop` quien lo decide.

JavaScript es un lenguaje synchronous, blocking y single-threaded lo cual es un problema como por ejemplo un código asi;

```javascript
while (true) {
  // procedimiento
}
moreWork(); // nunca se ejecutará
```

Este es el problema que Node viene a resolver, por lo que le runtime de Node tiene estos 3 componentes.

<p align="center">
  <a href="https://nodejs.org/en" target="blank"><img src="https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F0adb9612e27a439e8bbe2a65b861bbb3?format=webp&width=2000" width="1000" alt="NodeJS Logo" /></a>
</p>

En esencia, el entorno de ejecución de Node está compuesto por tres componentes principales:

- Dependencias externas: como V8, libuv y crypto, que Node.js necesita para su funcionamiento.
- Funcionalidades de C++: que proporcionan capacidades como el acceso al sistema de archivos y la comunicación a través de redes.
- Una biblioteca de JavaScript: que proporciona funciones y utilidades para acceder a las funcionalidades implementadas en C++ directamente desde el código JavaScript.
  Aunque todos estos componentes son importantes, el componente fundamental para la programación asíncrona en Node.js es una dependencia externa llamada libuv.

### Libuv

Dentro del entorno de ejecución de Node.js, su función es proporcionar soporte para gestionar operaciones asíncronas.

[Asyncronous Code Execution in Node.js](https://cdn.builder.io/o/assets%2FYJIGb4i01jvw0SRdL5Bt%2Fd5131502a8e84dfcab11f1c3820101b7%2Fcompressed?apiKey=YJIGb4i01jvw0SRdL5Bt&token=d5131502a8e84dfcab11f1c3820101b7&alt=media&optimized=true)

Creamos otro archivo app.js y copiamos el siguiente código:

```javascript
console.log("Inicio de programa");

setTimeout(() => {
  console.log("Primer Timeout");
}, 3000);

setTimeout(() => {
  console.log("Segundo Timeout");
}, 0);

setTimeout(() => {
  console.log("Tercer Timeout");
}, 1);

console.log("Fin de programa");
```

- ¿Qué pasa si dos Timeouts terminan al mismo tiempo?
- ¿Qué pasa si una promesa termina al mismo tiempo que otro callback?
- ¿En qué orden se ejecutan

El event Loop es quien decide.

**¿Qué es el Event Loop?**

Técnicamente, el Event Loop es un programa escrito en lenguaje C. Sin embargo, podés entenderlo como un patrón de diseño que orquesta o coordina la ejecución de código síncrono y asíncrono en Node.js.
El Event Loop se ejecuta continuamente mientras tu aplicación Node.js esté en funcionamiento, gestionando múltiples operaciones que se ejecutan de manera concurrente.

En cada iteración del ciclo, existen seis colas diferentes, cada una de las cuales contiene una o más funciones callback que eventualmente deberán ejecutarse en la pila de llamadas (Call Stack).

<p align="center">
  <a href="https://nodejs.org/en" target="blank"><img src="https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F6b288555862049b4b5cd7f19e2ae909f?format=webp&width=2000" width="2000" alt="NodeJS Logo" /></a>
</p>

- Primero, está la cola de temporizadores (Timer Queue): técnicamente implementada como un min-heap (montículo mínimo), que contiene los callbacks asociados con setTimeout y setInterval.
- Segundo, está la cola de entrada/salida (I/O Queue): contiene los callbacks asociados con operaciones asíncronas, como las proporcionadas por los módulos fs (sistema de archivos) y http.
- Tercero, está la cola de verificación (Check Queue): almacena los callbacks asociados con la función setImmediate, que es específica de Node.js.
- Cuarto, está la cola de cierre (Close Queue): contiene los callbacks asociados con los eventos de cierre de una operación asíncrona.
  Finalmente, tenemos la cola de microtareas (Microtask Queue), que se divide en dos colas independientes:
- Cola nextTick (nextTick Queue): almacena los callbacks asociados con la función process.nextTick.
- Cola de Promesas (Promise Queue): contiene los callbacks asociados con las promesas nativas (Promise) de JavaScript.

**¿Cómo funciona el Event Loop?**

<p> Las flechas del diagrama ya nos dan una pista, pero es fácil confundirse, ya que el Event Loop ejecuta los callbacks siguiendo un orden específico.</p>

**Voy a explicar el orden de prioridad de las colas.**

<p>En primer lugar, es importante comprender que todo el código JavaScript síncrono escrito por el desarrollador tiene prioridad sobre el código asíncrono que el entorno de ejecución necesita procesar.</p>

Esto significa que el Event Loop solo puede comenzar a ejecutar callbacks cuando la pila de llamadas (Call Stack) está vacía.

Dentro del Event Loop, cada fase ejecuta los callbacks programados en su cola correspondiente. Sin embargo, existen varias reglas que debemos comprender, así que vamos a analizarlas una por una:

1. Se ejecutan los callbacks de las colas de microtareas (Microtask Queues). Primero se procesan las tareas de la cola nextTick y después las de la cola de promesas (Promise Queue).

2. Se ejecutan los callbacks de la cola de temporizadores (Timer Queue). Esta etapa se denomina Timers Phase y procesa los callbacks de temporizadores cuyo tiempo de espera ya ha finalizado.

3. Se ejecutan las microtareas pendientes después de cada callback de la cola de temporizadores. Primero las tareas de nextTick y luego las de la cola de promesas.

4. Se ejecutan los callbacks de la cola de entrada/salida (I/O Queue). Esta etapa corresponde al procesamiento de operaciones de entrada y salida (I/O Phase).

5. Se ejecutan las microtareas pendientes, comenzando por nextTick Queue y continuando con Promise Queue.

6. Se ejecutan los callbacks de la cola de verificación (Check Queue). Esta etapa se denomina Check Phase.

7. Se ejecutan las microtareas pendientes después de cada callback de la cola de verificación. Primero se procesan las tareas de nextTick y después las de la cola de promesas.

8. Se ejecutan los callbacks de la cola de cierre (Close Queue). Esta etapa se denomina Close Callbacks Phase.

9. Por última vez dentro de la misma iteración del ciclo, se ejecutan las microtareas pendientes. Primero las tareas de nextTick y luego las de la cola de promesas.

   Si todavía quedan callbacks por procesar, el Event Loop permanece activo durante una nueva iteración y se repiten los mismos pasos.
   Por el contrario, si todos los callbacks han sido ejecutados y no queda código ni ninguna operación activa que mantenga el proceso en funcionamiento, el Event Loop finaliza.
   Este es el papel que desempeña el Event Loop de libuv en la ejecución del código asíncrono de Node.js.

#### Algunas preguntas comunes que se puede responder tras entender como funciona el Event Loop.

**¿Cuando una tarea asíncrona finaliza en libuv, en qué momento Node.js decide ejecutar su callback en la Call Stack?**

- Respuesta:
  Las funciones callback se ejecutan únicamente cuando la pila de llamadas (Call Stack) está vacía.

**¿Node.js espera a que la Call Stack esté vacía antes de ejecutar un callback o interrumpe el flujo normal de ejecución para hacerlo?**

- Respuesta:
  El flujo normal de ejecución no se interrumpe para ejecutar una función callback.

**¿Qué sucede con otros métodos asíncronos, como setTimeout y setInterval, que también retrasan la ejecución de una función callback?**

- Respuesta:
  Los callbacks de setTimeout y setInterval reciben la primera prioridad.

**Si dos tareas asíncronas, como setTimeout y readFile, finalizan al mismo tiempo, ¿cómo decide Node.js qué callback ejecutar primero en la Call Stack? ¿Tiene alguno mayor prioridad?**

- Respuesta:
  Los callbacks de los temporizadores se ejecutan antes que los callbacks de entrada/salida (I/O), incluso si ambos están listos exactamente al mismo tiempo.

Referencias

- https://nodejs.org/learn/asynchronous-work/event-loop-timers-and-nexttick
- https://www.builder.io/blog/visual-guide-to-nodejs-event-loop

## Autor

- Ariel Duarte
