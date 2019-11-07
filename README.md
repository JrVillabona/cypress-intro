# Introducción a Cypress.io
Cypress.io es una herramienta de testeo de front-end de código abierto construida para la web moderna. Este framework “todo en uno” incluye librerías de aserciones, mocks y pruebas end-to-end automáticas sin utilizar Selenium.

Al contrario que Selenium, Cypress cuenta con una nueva arquitectura construida desde cero, que ejecuta los comandos en el mismo ciclo de ejecución.

No necesitamos instalar varias herramientas ni librerías separadas para poder ejecutar tests, ya que ejecutando únicamente una línea de comando tendríamos Cypress instalado.

## Instalación Cypress.io
Como único requisito necesitamos tener instalado una versión igual o superior a la **Node v6** en nuestro equipo.

Inicialmente creamos el directorio del proyecto en el que vamos a trabajar, y nos ubicamos en su ruta:
```
mkdir cypress-intro
cd cypress-intro
```
Creamos el package.json (donde estarán las dependencias):
```
npm init -y
```
Ubicados en la ruta del proyecto instalamos Cypress.io:
```
npm install --save-dev cypress
```
De esta forma Cypress se instalará en el directorio **./node_modules**

## Ejecución
El siguiente paso será abrir Cypress, lanzando el ejecutable que se encuentra en **./node_modules/.bin** podríamos ejecutarlo así desde la consola:
```
./node_modules/.bin/cypress open
```
Pero para que sea más sencillo, se agregarán los comandos de Cypress en la sección *scripts* dentro del archivo package.json situado en la raíz de nuestro proyecto.
```
{
  "scripts": {
    "cy:open": "./node_modules/.bin/cypress open",
    "cy:run": "./node_modules/.bin/cypress run"
  }
}
```
Ahora podemos invocar al comando de la siguiente forma:
```
npm run cy:open
```

## Aspectos generales
Al ejecutarlo por primera vez, se creará la carpeta **cypress**, que contiene la siguiente estructura de carpetas:

- `Fixtures`: Datos estáticos que pueden ser utilizados para los tests.
- `Integration`: Lugar donde colocaremos los tests. Por defecto contiene una carpeta de tests de ejemplo.
- `Plugins`: Permiten acceder, modificar o ampliar el comportamiento interno de Cypress. (Ej: Plugin de Cucumber)
- `Support`: Lugar para colocar comportamientos reutilizables, como comandos personalizados o anulaciones globales, que estarán disponibles para todos los tests.

## Escribamos nuestro primer test
Escribir tests en Cypress es muy sencillo. El objetivo de este primer test será navegar a la página oficial de **Cypress.io**, ir a la sección de **Support** y verificar que en la URL esté la ruta correspondiende a la página de **Support**. Para ello, en primer lugar crearémos un archivo Javascript dentro de la carpeta **Integration** lo podríamos llamar `support.spec.js` y dentro del archivo escribirémos el siguiente código:
```
describe('Test web oficial de cypress.io', () => {
  it('Visitar sección Support', ()=> {
    cy.visit('https://www.cypress.io/')
    cy.get(':nth-child(2) > :nth-child(1) > .header__NavLink-xi2ch0-6').click()
    cy.url().should('include', '/support')
  } )
} )
```
Analicemos línea a línea:
```
describe('Test web oficial de cypress.io', () => {
```
Esta línea define nuestro suite de tests, es importante darle un nombre descriptivo.
```
it('Visitar sección Support', ()=> {
```
Primera línea de un nuevo test dentro de nuestro suite de tests.
```
cy.visit('https://www.cypress.io/')
```
El comando **cy.visit** accede a la URL especificada.
```
cy.get(':nth-child(2) > :nth-child(1) > .header__NavLink-xi2ch0-6').click()
```
El comando **cy.contains** busca el elemento que contenga el texto que se le ha pasado como parámetro, y después hace click en él.
```
cy.url().should('include', '/support')
```
A través del comando **cy.url** nos aseguramos de que la ruta a la que accedemos es la correcta.

## Ejecutemos nuestro primer test
Ahora que tenemos nuestro primer test creado, ¡Ejecutémoslo!

Por defecto, los tests se ejecutarán en modo headless, es decir, mediante un navegador sin interfaz gráfica. Los navegadores con los que se ejecutarán los test son Chrome y Electron. No es necesario instalar Electron ya que es el navegador por defecto de Cypress.io.

El comando `run` ejecutará todos los tests que tengamos dentro de la carpeta **Integration**.
```
npm run cy:run
```
Si nuestro test fallase, podríamos ejecutarlo en **modo headed** para poder depurarlo más fácilmente.
```
npm run cy:run --headed
```
También podemos ejecutar los tests en modo interactivo utilizando el comando **open**.
```
npm run cy:open
```
Esto nos abrirá la consola de Cypress en la que podemos seleccionar el test que queramos ejecutar. Si el test pasa correctamente, el panel mostrará un check verde por cada test.

Podrémos también hacer click en cualquier paso del test, y la consola del navegador nos mostrará más información acerca del mismo.

## ¿Y ahora qué sigue?

Uno de los aspectos positivos para decidirse por Cypress para realizar nuestros tests E2E es sin duda su amplia documentación y su API. Aquí podremos encontrar una guía de uso bastante completa y un gran número de comandos que podremos utilizar en nuestros test.

- Cypress.io: https://www.cypress.io/
- Cypress Comandos: https://example.cypress.io/commands/querying
