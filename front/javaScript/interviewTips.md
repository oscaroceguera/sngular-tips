# Tips para entrevista

```javascript
var firstArray = [1, 2, 3, 4, 5, 6, 7, 8, 9];
```
## Operadores bit a bit o binarios

| Operador | Nombre               | Descripción |
|----------|----------------------|-------------|
|   &      |  AND                 |             |
|   &#124; |  OR                  |             |
|   ^      |  XOR                 |             |
|   ~      |  NOT                 |             |
|   <<     | Zero fill left shift |             |
|   >>     | Signed right shift   |             |
|   >>>    | Zero fill right shift|             |


| Operación | Resultado |             |      |
|-----------|-----------|-------------|------|
| 5 & 1     |    1      | 0101 & 0001 | 0001 |
| 5 &#124; 1     |    5      | 0101 &#124; 0001 | 0101 |
| ~ 5       |    10     | ~ 0101      | 1010 |
| 5 << 1    |    10     | 0101 << 1   | 1010 |
| 5 ^ 1     |    4      | 0101 ^ 0001 | 0100 |
| 5 >> 1    |    2      | 0101 >> 1   | 0010 |
| 5 >>> 1   |    2      | 0101 >>> 1  | 0010 |


## Como validar si un arreglo es un arreglo

```javascript
// opción 1
Array.isArray( firstArray ); // true

// opción 2
var myArray = [];
myArray instanceof Array; // true

// opción 3
var x = [];
x.constructor === Array // true

```
## Como concatenar arreglos

```javascript
// Método concat
var a= [ 1, 2, 3 ]
var b= [ 4, 5 ]

var c = a.concat( b ) // 1, 2, 3, 4, 5,

// Operador Spread
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);

// Método push ES5
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];

// Agregar todos los elementos de arr2 a arr1
Array.prototype.push.apply(arr1, arr2);

```

## Método para agregar elementos al final del arreglo

```javascript
firstArray.push( 0 )
```
## Método para agregar elementos al inicio del arreglo

```javascript
firstArray.unshift( 0 )
```

## Método para agregar nuevos elementos entre el elemento 4 y 5 del arreglo

```javascript
firstArray.splice( 4, 0, '12', '21' )
```

```javascript
// Ejemplo 2
// Remueve elementos de un arreglo y los reemplaza con nuevos.
var a = ['a', 'b', 'c'];
var r = a.splice(1, 1, 'ache', 'bug');
// a is ['a', 'ache', 'bug', 'c']
// r is ['b']
```
## Método para seleccionar una porción de un arreglo

```javascript
var a = ['a', 'b', 'c'];
var b = a.slice(0, 1); // b is ['a']
var c = a.slice(1); // c is ['b', 'c']
var d = a.slice(1, 2); // d is ['b']
```

## Obtener el promedio de un arreglo

```javascript
//opción 1
var sum = firstArray.reduce( function( curr, prev ){
	return curr + prev;
} )

var avg = sum / firstArray.length


// opción 2
var sum = firstArray.reduce( function( curr, prev, index, vector ){
	if( index === vector.length -1 ){
		return ( curr + prev ) / vector.length;
	}
	return curr + prev;
} )

```

## Obtener el cuadrado de cada número del arreglo

```javascript
var sq = firstArray.map( function( num ){
	return num * num;
} )
```

## Obtener números pares de un arreglo

```javascript
var even = [];
firstArray.map( function( num ){
	if( num % 2 === 0 )
		even.push( num );
} )

// o en ES6
var even = firstArray.filter( function( num ){
	return  num % 2 === 0;
} )


// con reduce
var even = firstArray.reduce( function( prev, num ){
	if( num % 2 === 0 ){
		prev.push( num )
	}
	return prev
}, [] )

```


## Invertir cadena

```javascript
var myStr = 'Hello';
myStr.myStr('').reverse().join(''); // 'olleH'

// why
myStr.myStr(''); // ["H", "e", "l", "l", "o"]
myStr.split('').reverse(); // ["o", "l", "l", "e", "H"]
myStr.myStr('').reverse().join(''); // 'olleH'
```


## Currying

Curry es poder llamar una función con menos parámetros de los que espera, esta devuelve una función que espera los parámetros restantes y retorna el resultado.
```javascript
function sum( num1 ){
    return function( num2 ){
        return num1 + num2;
    };
}

// Forma 1 de ejecutar la función
var curry = sum(1) ;
curry( 2 );

// Forma 2 de ejecutar la función
sum( 1 )( 2 );
```

## Deep copy y Shallow Copy

Shallow copy( copia superficial ): solo se asigna el mismo valor de la memoría.

```javascript
// Shallow copy
var obj = { test: 1 };
var obj2 = obj;

obj2.abc = 12; // Cuando agregamos una nueva propiedad a obj2 tambien se asigna a obj ya que apuntan al mismo espacio en memoria
obj.test = 2; // Cuando cambiamos una nueva propiedad de obj tambien se cambia obj2
```

Deep copy( copia profunda ): Crea una nueva copia de un objeto y un nuevo espacio de memoria

```javascript
// Shallow copy
var obj = { test: 1 };
var obj2 = Object.assign( {}, obj );

obj2.abc = 12;
// Si se agrega una nueva propiedad a obj2, esta no se ve reflejada en obj
// ya que estan en diferentes espacios de memoria


// Ejemplo con operador Spread
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 }; // Object { foo: "bar", x: 42 }
var mergedObj = { ...obj1, ...obj2 }; // Object { foo: "baz", x: 42, y: 13 }
```

## Hoisting

Comportamiento por default de Javascript para agregar variables hasta el top de un contexto.

```javascript
var result = 4;
function ejemplo (){
    console.log(result);
}
ejemplo() // 4

function ejemplo2 (){
    console.log(result);
    var result = 10;
}
ejemplo2() // undefined

function ejemplo3 (){
    var result = 10;
    console.log(result);
}
ejemplo3() // 10
```

## 'use strict';

Impide crear variables de ámbito global “accidentalmente”. Toda variable ha de estar previamente declarada, ejemplo: Si usas foo = "bar" sin definir foo primero, tu código va a fallar.

[Referencia sobre Use strict](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Modo_estricto)


## Coerción
Es la acción de forzar a que un objeto se comporte como si fuera de otro tipo.

```javascript
var var1, // -> undefined
    var2 = 9;

if (var1) { } // -> coerción a false
if (var2) { } // -> coerción a true
```

## Event loop

[Referencia 1](http://altitudelabs.com/blog/what-is-the-javascript-event-loop/)
[Referencia 2](http://latentflip.com/loupe/)
[Referencia 2](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
```javascript
 function print() {
   console.log(1);
   setTimeout(function() { console.log(2) }, 0);
   console.log(3);
}
print() // 1, 3, 2
```
## Promesas

Como generar una nueva promesa nativa.

```javascript
var promise = new Promise(function( resolve, reject ){
    // some Jquery request
    $.ajax({
    	url: '/roooooo',
	success: function( response ){
	    resolve( response )
	},
	error: function( err ){
	    reject( err )
	}
    })
});

```

Como ejecutar multiples promesas.


```javascript
// Ejemplo 1
var p1 = new Promise( function( resolve, reject ){} );
var p2 = new Promise( function( resolve, reject ){} );

Promise.all( [ p1, p2 ] ).then( function( array ){
} ).catch()

// Ejemplo 2
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 100, "foo");
});

Promise.all([p1, p2, p3])
    .then( function(values){
        console.log(values); // [3, 1337, "foo"]
    })
    .catch(function(){
    	// si una petición es rechazada, mamasteee...
    });
// catch
```

[Explicación de Promises.all](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Promise/all)

## Herencia de objetos con Prototype
Como heredar metodos de un objeto a otro.

```javascript
function Person(){
    this.myvar = 5;
}

Person.prototype.getName = function( name ){
    console.log( name )
}

function Doctor(){
    Person.call( this )  // Llama el constructor de Person
}

Doctor.prototype = Object.create( Person.prototype );

var example = new Doctor();
console.log( example.getName );
console.log( example instanceof Person )

```
