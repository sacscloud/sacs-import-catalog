# \<sacs-import-catalog\>

Necesito importar de forma sencilla mis catalogos en cada uno de los modulos para tener la informacion de mi sistema anterior en sacscloud y poder tener todo en un solo espacio.import 

## Criterios de aceptación

- Realizar una opcion en el data table que habilite un boton para realizar la importacion al data table correspondiente 
- Debe de haber un template de excel descargable de ese data table para que el usuario pueda copiar la estructura y poder subirlo
- El importador debe ser sencillo y abrirse en un modal en la misma pantalla mostrando de forma sencilla los pasos a seguir para que cualquier tipo de usuario pueda hacer este paso de forma sencilla. 
- Debe sersencillo para el implementador agregar este boton en los data table para que el usuario final pueda importar de forma sencilla 
- El importador debe tener todas las validaciones posibles para que el usuario no cometa erroes y tengamos un costo alto del servidor. 

## Example

imagen o gif de ejemplo


## PROCESO DE IMPORTACION SACSCLOUD

## Paso 1: 
Insertar un objeto en el nodo "/imports" en el la base de datos para que se lea el archivo y se obtengan los campos del archivo, ejemplo del json a insertar:

```
{
account: Id de la cuenta en la cual se importarán los datos ejem: sacspruebas2,
reference: Ruta del api del account donde se insertaran los datos ejem: articulos,
template: Id del template que se utilizara para esta importación en caso de tenerlo,
urlFile: Dirección del archivo en el firestorage ejem: ‘importsFiles/-Lb3gOHX9KM9aO54XhHC_Articulos.xlsx’”
}
```

una vez insertado el objeto se crea automáticamente el nodo map que es un JSONString que contiene la información de que campo va hacia qué propiedad en la pi que se va insertar ejem

```
{
name: Nombre de la columna en excel,
property:Propiedad de la api donde se va a insertar el campo, por default pone el mismo nombre de la columna de excel.
*type: Tipo de dato que se va a insertar en la api por default “isString”,
catalogApp: En caso que sea type: selectdynamic es un string de la app donde hace referencia el dato,
catalog: En caso que sea type: selectdynamic es un string de la api donde hace referencia el dato,
catalogProperty: En caso que sea type: selectdynamic es un string de la propiedad de la api donde hace referencia el dato,
notApply: Valor Booleano  que representa si la columna de excel debe no importarse
}
```

*valores type disponibles: num, number, isNumber, checkbox, isBoolean, datecreation, datemodification, isDate, datepicker, isDateString, selectdynamic(Cuando se selecciona este tipo de dato es cuando el campo hace referencia a otro objeto perteneciente a otra api de la cuenta)

## Paso 2 sin template: 
Se le permite a los usuarios editar la configuración de la importación, en la cual podrán editar los siguientes parámetros del objeto de importación:

```
{
conditionals : JSONString de un Array de las condiciones para filtrar datos de la importación por el momento no implementado default:”[]”,
*deleteNotInList : Valor booleano en el cual se establece que se deben borrar los registros que no estén en el archivo que se esta importando,
 firebaseObjectField : Cuando se hace una importación para actualizar datos, campo del excel que servirá como id para comparar los datos,
importObjectField : Cuando se hace una importación para actualizar datos, campo del api que servirá como id para comprar los datos,
 map : JSONString que representa la configuración de hacia donde van los campos del excel en la api,
querys : JSONString de un Array de las consultas para hacer antes de importar datos por el momento no implementado default:”[]”
 }
 ```
 
*El campo deleteNotInList cuando está en true borra los registros en la base de datos que no estén en el archivo de importación que se esta subiendo por lo que se debe tener cuidado al establecerlo en true, en caso de no querer esto se debe establecer en falso

## Paso 2 con template: 
Se obtiene la información del template que se encuentra en “accounts/{account}/sacsimportadortemplates/{template}” y se sustituye lo que hay en el nodo template de esta información  con excepción del campo “importId” y así se establece la configuración de la importación sin necesidad que lo haga el usuario, actualmente el front consulta el template y actualiza el objeto de importación

## Paso 3:
Se hace un POST con el parámetro “importId”  hacia https://us-central1-sacs3-da4a6.cloudfunctions.net/app/analizedImportData, esto iniciara un proceso en el cual se iniciara el análisis del archivo a importar de acuerdo a la configuración de importación del paso 2, el resultado final sera un archivo donde se guardaran los campos ya formateados listos para insertar o actualizar, así como la instrucciones de los campos a limitar en caso de ser necesario, mientras se realiza el análisis de la información el objeto de importación actualizara el nodo step, status y percent según el status del análisis, al terminar, automáticamente el objeto de importación quedara de la siguiente manera:

```
{
	step:2,
	status:”Análisis de información terminada”
	percent:100
} 
```

## Paso 4:
Se hace un POST con el parámetro “importId” hacia  https://us-central1-sacs3-da4a6.cloudfunctions.net/app/executeImportTask, eso ejecutara el archivo de importación generado tras el análisis realizado del objeto de importación esto también ira actualización los campos step, status y percent de acuerdo al status de la ejecución, al terminar, automáticamente el objeto de importación quedara de la siguiente manera:

```
{
	step:3,
	status:”Import Task Finished Succesful”
	percent:100
}
```

Si existe algún error el archivo quedará así:

```
{
	step: 3,
	status: "Import Task Finished with errors",
	percent: 100
}
```

## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your element locally.

## Install component

```
bower i --save sacscloud/sacs-import-catalog
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
