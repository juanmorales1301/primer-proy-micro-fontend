Aquí tienes el archivo `README` reorganizado y completado para hacerlo más claro y comprensible:

---

# Aplicación Microfrontend con Single-SPA

Una aplicación **microfrontend** permite integrar múltiples frameworks o bibliotecas en un solo proyecto, permitiendo utilizar diversas tecnologías, como React, Angular, Vue, etc. Para gestionar estos microfrontends, se utiliza **webpack** junto con la librería **single-spa**, que se encarga de configurar el entorno adecuado.

## ¿Qué es Single-SPA?

**single-spa** es una librería que facilita la creación de microfrontends, gestionando las aplicaciones y su carga en diferentes entornos.

## Comando para crear una aplicación microfrontend

```bash
npx create-single-spa
```

Este comando genera una aplicación con la configuración necesaria para trabajar con microfrontends.

### Tipos de aplicaciones en single-spa:
- **single-spa root config:** Contenedor principal que encapsula y coordina las demás aplicaciones.
- **single-spa application / parcel:** Subaplicaciones individuales que se ejecutan en el contenedor principal.
- **in-browser utility module (styleguide, api cache, etc.):** Módulos de utilidad para compartir recursos como estilos o caché entre las aplicaciones.

## Manejadores de paquetes

- **npm (Node Package Manager):** El manejador de paquetes predeterminado de Node.js, utilizado para gestionar dependencias y scripts del proyecto.
- **yarn:** Alternativa a npm, con características adicionales como bloqueo de versiones de dependencias.
- **pnpm:** Otro manejador de paquetes, eficiente en el uso del almacenamiento, al compartir dependencias comunes entre proyectos.

## ¿Desea utilizar TypeScript?

**TypeScript** es un superconjunto de JavaScript que añade tipado estático. Esto permite detectar errores en tiempo de desarrollo, pero requiere transpilación para convertir el código TypeScript a JavaScript.

## Single-SPA Layout Engine

El **Single-SPA Layout Engine** agiliza el proceso de carga de aplicaciones microfrontend, ya que permite definir el layout (disposición) de las aplicaciones en el DOM, cargando cada aplicación solo cuando es necesario.

## Inicialización del repositorio y estructura de carpetas

### Niveles de carpetas y archivos principales

1. **package.json:** Contiene las dependencias y scripts para ejecutar tareas en el proyecto. Por defecto, instala herramientas como webpack, babel, eslint, y otras:
   - **webpack:** Empaqueta y optimiza el código.
   - **babel:** Transpila el código JS moderno para compatibilidad.
   - **jest:** Realiza pruebas unitarias.
   - **eslint:** Linter para mantener la calidad del código.
   - **cross-env:** Configura variables de entorno en scripts de Node.
   - **prettier:** Formatea el código automáticamente.
   - **husky:** Gestiona hooks de git.
   - **pretty-quick:** Ejecuta prettier en los archivos modificados en un commit.

   Ejemplo de scripts en `package.json`:
   ```json
   "scripts": {
     "start": "webpack serve --port 9000 --env isLocal",
     "lint": "eslint src --ext js,ts,tsx",
     "test": "cross-env BABEL_ENV=test jest --passWithNoTests",
     "format": "prettier --write .",
     "check-format": "prettier --check .",
     "prepare": "husky install",
     "build": "concurrently npm:build:*",
     "build:webpack": "webpack --mode=production",
     "build:types": "tsc"
   }
   ```

2. **babel.config.json:** Configuración de Babel para la transpilación de código.
3. **.husky/pre-commit:** Hook de pre-commit que ejecuta tareas antes de realizar un commit.
4. **.eslintrc:** Configuración de ESLint para mantener la calidad del código.
5. **.prettierignore:** Archivos o carpetas que no deben ser formateados por Prettier.
6. **webpack.config.js:** Configuración de Webpack para empaquetar las aplicaciones.
7. **tsconfig.json:** Configuración de TypeScript.
8. **src/root-config.ts:** Archivo principal que gestiona el microfrontend en el proyecto.
9. **src/index.ejs:** Archivo de plantillas EJS para la aplicación principal.
10. **src/microfrontend-layout.html:** Define el layout de los microfrontends dentro de la aplicación.
11. **src/declarations.d.ts:** Declaraciones de tipos para TypeScript.

## Configuración de `microfrontend-layout.html`

Dentro del archivo `microfrontend-layout.html`, las aplicaciones microfrontend se registran en el contenedor principal utilizando etiquetas `<application>` dentro de un `<single-spa-router>`. Estas aplicaciones deben estar previamente definidas en el archivo `index.ejs`, utilizando el sistema **SystemJS** para gestionar las rutas y las dependencias.

### Ejemplo de configuración en `index.ejs`

En el `index.ejs`, la sección del script con el tipo `systemjs-importmap` define las aplicaciones disponibles en el microfrontend:

```json
{
  "imports": {
    "@single-spa/welcome": "https://unpkg.com/single-spa-welcome/dist/single-spa-welcome.js",
    "@primer-proyecto-mf/root-config": "//localhost:9000/primer-proyecto-mf-root-config.js"
  }
}
```

El nombre del parámetro dentro de `imports` debe coincidir con el nombre de la aplicación en el layout (`<application name="@single-spa/welcome">`), y el valor es la ruta al archivo compilado de la aplicación, que puede estar construida en diferentes tecnologías como React, Angular, Vue, o HTML/JS.

### Uso de `isLocal`

En la plantilla **EJS**, la variable `isLocal` permite cargar ciertas dependencias solo en entornos locales. Las etiquetas `<%` y `%>` son parte de la sintaxis EJS.

## Crear una nueva aplicación dentro del proyecto

Para integrar una nueva aplicación microfrontend dentro del proyecto existente, utiliza el siguiente comando:

```bash
npx create-single-spa
```

Al ejecutar este comando, puedes especificar una ruta personalizada para la nueva aplicación, como `micros/mf-product`. Si la carpeta está fuera de la raíz del proyecto, asegúrate de que exista antes de la creación. Luego, selecciona la opción **single-spa application / parcel** para generar la estructura básica de la aplicación frontend.

---

Este archivo `README` reorganizado te proporciona una mejor comprensión del uso de **single-spa** para la gestión de microfrontends, con una explicación clara de los conceptos clave y la estructura del proyecto.