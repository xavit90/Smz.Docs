# TypeScript
> Nota: La siguiente documentación incluye algunos conceptos utilizados en TypeScript, para más información visite el sitio oficial o 

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

La **desestructuración** es una forma fácil y rápida de **extraer valores** de objetos o arreglos y asignarlos a variables. En lugar de acceder a cada propiedad o elemento uno por uno, puedes sacar varios valores de una sola vez. Es como abrir una caja y sacar lo que necesitas directamente, en lugar de tomar cada cosa por separado.

#### Ejemplo
```typescript
async getData(): Promise<Data> {
	let { data } = await axios.get<Data>("https://api.example.com/data");
    console.log(data);
    }
```
## Inyección de Dependencias
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTAyMTgyMzQ0LC0yMDQyMDAwMjM4LC0xMD
Y1MzU0ODQ4LC02MTc3Njk4NDMsLTQyOTQ4MDY4LC00OTg0NzM0
MjcsLTE1ODM1NDg0MTcsMTQ2NTEwNzgzOSwtMjQ4ODYwMzkxLD
EzNDAwMzg2OTgsLTQzOTc5OTg5NSwtMTM5OTg5NDU3NSwxMjMy
ODI1NTMxLDE1NzQwMTQyNzAsMTQzNTcxNzYzOCwtMzg3NzkxOT
IwLC0zNTU1NzU4MywtMTc1NzcxNzM1MCw5NDUxMDQyMDUsMTg2
MTcyMjI1Nl19
-->