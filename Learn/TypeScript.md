# TypeScript
> Nota: La siguiente documentación incluye algunos conceptos utilizados en TypeScript, para más información visite el sitio oficial o documentación adicional.

## Introducción

**TypeScript** es un lenguaje de programación desarrollado por **Microsoft** que se basa en **JavaScript**.

La principal característica es su sistema de **tipos estáticos**, lo que significa que puedes definir qué tipo de datos debe tener cada variable, función u objeto en tu código. Esto ayuda a identificar errores antes de ejecutar el programa, haciéndolo más seguro y predecible. También ofrece características avanzadas como **interfaces**, **clases** y **módulos**, mejorando la organización del código y facilitando el trabajo en proyectos grandes.

Al final, el código TypeScript se convierte en JavaScript, lenguaje que los navegadores y muchos servidores entienden. Entonces, usar TypeScript permite escribir código más ordenado y seguro, haciendo que sea más fácil de entender y menos propenso a errores.

## Tipos Estáticos

TypeScript es un *superset* de JavaScript que agrega tipos estáticos, declarar de qué tipo es cada variable, ayuda a prevenir errores antes de ejecutar el código. Los tipos básicos incluyen:

 - string, number, boolean
 - array (number[], string[])
 - tuple, enum, y any (cuando necesitas evitar restricciones de tipos)
 - union types (number | string para variables de múltiples tipos posibles)
 
#### Ejemplos

```typescript showLineNumbers
let name: string = "Samm"
let average: number = 98;
let isStudent: boolean = true;

/* array: para listas de valores de un mismo tipo */
let scores: number[] = [99, 98, 99];
let subjects: Array<string> = ["Math", "English", "History"];

/* tuple: para listas de un tamaño y tipos definidos */
let person: [string, number] = ["Samm", 98];

/* enum: para definir un conjunto de valores constantes */
enum Color { Red, Green, Blue }
let favoriteColor: Color = Color.Green;
```
Las variables de tipo **any** pueden contener cualquier tipo de valor. Este tipo es útil cuando no puedes determinar el tipo exacto de una variable, pero debe usarse con cuidado porque elimina el beneficio del tipado estático.
```typescript
let randomValue: any = "Hello";
randomValue = 10; // Esto es válido
```
## Interfaces

Una **interfaz** define las propiedades que el objeto debe tener y sus tipos, pero no los valores. Esto ayuda a asegurarse de que el objeto siempre tenga la misma estructura en todo el código, lo cual es muy útil para mantener el orden y evitar errores.

#### Ejemplo
```typescript
interface Student {
    name: string;
    age: number;
}
```
## Clases

Una **clase** es un plano para crear objetos con propiedades y métodos.
Las clases ayudan a organizar el código, especialmente cuando se trabaja con muchos objetos que tienen propiedades y comportamientos similares. Además, permiten reutilizar el mismo "molde" para crear múltiples objetos sin tener que repetir código.

#### Ejemplo
```typescript
class Person {
    name: string;
    age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet(): string {
        return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
    }
}

// Creando una instancia de la clase persona
let person1 = new Person("Samm", 30);
```
## Objetos

Un **objeto** es una estructura que agrupa datos relacionados y organiza la información en "pares clave-valor".

#### Ejemplo
```typescript
let student = {
    name: "Samm",
    age: 22
};
```
## Tipos de arreglos
Un **arreglo** es una lista de elementos ordenados que pueden ser de cualquier tipo: *números*, *texto*, *objetos*, etc.

TypeScript permite definir **arreglos de un tipo específico**, lo que significa que se puede definir qué tipo de datos va a tener cada elemento.

#### Ejemplo
```typescript
let subjects: string[] = ["Math", "English", "History"];
let scores: number[] = [99, 98, 99];
let nombres: Array<string> = ["Math", "English", "History"];
let scores: Array<number> = [99, 98, 99];
```
Si quieres que un arreglo pueda contener más de un tipo, puedes usar tipos múltiples (o "union types"). Por ejemplo, un arreglo que contenga tanto números como cadenas de texto:

#### Ejemplo
```typescript
let data: (number | string)[] = [1, "two", 3, "four"];
```
## Métodos Asíncronos & Promesas

Un **método asíncrono** es una función especial que permite realizar tareas que **toman tiempo** sin detener el resto del programa. Esto es útil para cosas como esperar una respuesta de un servidor, leer archivos, o hacer cualquier cosa que no ocurra de inmediato.

Una **promesa** es un objeto que representa el resultado eventual de una **operación asíncrona**. Este resultado puede ser exitoso (cumplido) o fallido (rechazado). Las promesas se usan para manejar tareas que toman tiempo, como llamadas a APIs, sin bloquear el flujo del programa.

#### Ejemplo
```typescript
async getData(): Promise<Data> {
	let response = await axios.get<Data>("https://api.example.com/data");
    console.log(response.data);
    }
```
## Desestructuración

La **desestructuración** es una forma fácil y rápida de **extraer valores** de objetos usando `{}` o arreglos usando `[]` y asignarlos a variables. En lugar de acceder a cada propiedad o elemento uno por uno, puedes sacar varios valores de una sola vez. Es como abrir una caja y sacar lo que necesitas directamente, en lugar de tomar cada cosa por separado.

#### Ejemplo
```typescript
async getData(): Promise<Data> {
	let { data } = await axios.get<Data>("https://api.example.com/data");
    console.log(data);
    }
```
## Inyección de Dependencias

La **inyección de dependencias** es una técnica que permite que un objeto o clase reciba las herramientas o datos que necesita para funcionar (llamadas “dependencias”) desde afuera, en lugar de crearlas él mismo. Esto hace que el código sea más flexible y fácil de probar, porque las dependencias se pueden cambiar o actualizar sin modificar la clase principal.

Imaginemos una clase `Car` que necesita un `Engine` para funcionar. Si `Car` crea su propio `Engine`, siempre dependerá de ese tipo específico de motor, lo cual no es flexible. Con la inyección de dependencias, `Car` recibe el `Engine` desde afuera, permitiendo que se use cualquier tipo de motor (por ejemplo, un motor eléctrico o de gasolina) sin cambiar la clase `Car`.

#### Ejemplo
Primero, se crean las dos clases que actúan como dependencias.
```typescript
class ElectricEngine {
	start(): string {
		return "Electric engine started.";
	}
}
 
class GasEngine {
    start(): string {
        return "Gas engine started.";
    }
}
```
Cada motor tiene un método *start* que devuelve un mensaje cuando el motor se enciende.
Posteriormente se crea la clase que se utilizara como dependencia. La clase *Car*, en lugar de crear su propio motor, *Car* recibirá un motor como parámetro cuando se cree un nuevo *Car*. Esto es la inyección de dependencias.
```typescript
class Car {
    private engine: { start(): string };

    constructor(engine: { start(): string }) {
        this.engine = engine;
    }
    
    startEngine(): void {
        console.log(this.engine.start());
    }
}
```
En este caso, *Car* tiene una propiedad *engine*, que es la dependencia.
Por último se pueden crear instancias de *Car* con diferentes tipos de motores.
```typescript
let electricCar = new Car(new ElectricEngine());
let gasCar = new Car(new GasEngine());

electricCar.startEngine();
gasCar.startEngine();
```
## Decoradores

Los **decoradores** son una forma de agregar comportamiento adicional a clases, métodos, propiedades, o parámetros sin modificar directamente el código original. Puedes pensar en ellos como "adornos" que añaden funcionalidades extra. Los decoradores permiten "envolver" algo en código adicional para realizar tareas como registro de datos (logging), autenticación, o validación sin alterar la lógica central.

Para crear un decorador básico, usamos `@` seguido del nombre del decorador justo antes de la clase o método que queremos modificar.

#### Ejemplo: Decorador de clase

Este decorador agrega un mensaje cuando se crea una instancia de la clase.

```typescript
function logClass(constructor: Function) {
  console.log(`Class ${constructor.name} has been created.`);
}

@logClass
class User {
  constructor(public name: string) {}
}

const user = new User("Alice");
// Output: "Class User has been created."
```

Aquí, el decorador `@logClass` envuelve a la clase `User` y registra un mensaje cuando se crea una instancia.

#### Ejemplo: Decorador de método

Este decorador registra cuándo se llama a un método.

```typescript
function logMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with arguments: ${args}`);
    return originalMethod.apply(this, args);
  };
}

class Calculator {
  @logMethod
  add(a: number, b: number) {
    return a + b;
  }
}

const calculator = new Calculator();
calculator.add(2, 3);
// Output: "Calling add with arguments: 2,3"
```

En este caso, el decorador `@logMethod` añade una funcionalidad para registrar los argumentos cada vez que se llama al método `add`.
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFR5cGVTY3JpcHRcbmF1dG
hvcjogU01vbnRlc1xudGFnczogJ3R5cGVzY3JpcHQsbmVzdCxq
YXZhc2NyaXB0J1xuc3RhdHVzOiBkcmFmZlxuZGF0ZTogJzIwMj
QtMTEtMDQnXG5jYXRlZ29yaWVzOiBEZXZlbG9wXG4iLCJoaXN0
b3J5IjpbMTA5MDg2NzI1MiwxODY1NzMyNTEwLC0xODU3OTU5Mj
kwLDE2NDQ3MDAzNDIsMTY1NTY5NzA3MCwtNTI3MjExMDc4LC0x
MTkwMTM1MzgsLTE0NTY5MjY5MjcsMTA3NTU3OTQ0OSw5MDIxOD
IzNDQsLTIwNDIwMDAyMzgsLTEwNjUzNTQ4NDgsLTYxNzc2OTg0
MywtNDI5NDgwNjgsLTQ5ODQ3MzQyNywtMTU4MzU0ODQxNywxND
Y1MTA3ODM5LC0yNDg4NjAzOTEsMTM0MDAzODY5OCwtNDM5Nzk5
ODk1XX0=
-->