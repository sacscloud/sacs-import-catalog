# \<sacs-input-autocomplete\>

Necesito importar de forma sencilla mis catalogos en cada uno de los modulos para tener la informacion de mi sistema anterior en sacscloud y poder tener todo en un solo espacio.import 

## Criterios de aceptación

- Realizar una opcion en el data table que habilite un boton para realizar la importacion al data table correspondiente 
- Debe de haber un template de excel descargable de ese data table para que el usuario pueda copiar la estructura y poder subirlo
- El importador debe ser sencillo y abrirse en un modal en la misma pantalla mostrando de forma sencilla los pasos a seguir para que cualquier tipo de usuario pueda hacer este paso de forma sencilla. 
- Debe sersencillo para el implementador agregar este boton en los data table para que el usuario final pueda importar de forma sencilla 
- El importador debe tener todas las validaciones posibles para que el usuario no cometa erroes y tengamos un costo alto del servidor. 

## Example

imagen o gif de ejemplo

## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your element locally.

## Install component

```
bower i --save sacscloud/sacs-input-autocomplete
```

## Viewing Your Element

```
$ polymer serve
```

## Test of component

The component must have the test basic:

- The component exist
- The component is in the DOM

The component must have test for properties:

- The property exist
- The property is declareded
- The property not is undefined

The component must have test for functions:

- The function is declareded
- The function exist
- The function don't throw error

### Running Tests

```
$ polymer test
```

Your application is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run your application's test suite locally.


## Properties

Las propiedades descritas solo son la base pero se deben agregar todas las que sean necesarias.

Name | Type | Description | Default
-----|-------------|---------|--------
`example` | `Array` | array to data | `[]`



## Methods

Las metodos descritos solo son la base pero se deben agregar todos las que sean necesarios.

Method | Description | Parameters | Return
-----|-------------|---------|------------
`example` | description | param | no retorna nada


## Events

Este componente no lanza ningun evento.

## Dependencies

Este componente no usa dependencias de otros componentes

## Use

```
<sacs-import-catalog></sacs-import-catalog>
```

## Behaviour

Descripcion del comportamiento interno del componente.

## Styling

Las siguientes propiedades y mixins estan disponibles para styling.

Custom property | Description | Default
----------------|-------------|----------
`--sacs-import-catalog-color` | background color | `#fff`

## Versions

El componente debe ser tageado para cada nuevo commit:

```
git tag v1.0.0
```
y se debe subir al repositorio

```
git push origin master v1.0.0
```

La version en el bower json tambien debe ser actualizada