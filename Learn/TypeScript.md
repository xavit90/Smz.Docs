# TypeScript

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
let name: string = "Alexis"
let average: number = 98;
let isStudent: boolean = true;

/* array: para listas de valores de un mismo tipo */
let scores: number[] = [99, 98, 99];
let subjects: Array<string> = ["Math", "English", "History"];

/* tuple: para listas de un tamaño y tipos definidos */
let person: [string, number] = ["Alexis", 98];

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
## Objetos

Un **objeto** es una estructura que agrupa datos relacionados y organiza la información en "pares clave-valor".

#### Ejemplo
```typescript
let persona = {
    nombre: "Ana",
    edad: 30,
    esEstudiante: true
};

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMTg1NDQyMjUsMTIzMjgyNTUzMSwxNT
c0MDE0MjcwLDE0MzU3MTc2MzgsLTM4Nzc5MTkyMCwtMzU1NTc1
ODMsLTE3NTc3MTczNTAsOTQ1MTA0MjA1LDE4NjE3MjIyNTYsLT
IwNTkzMjQ1NTldfQ==
-->