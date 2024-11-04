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
 
### Ejemplos

```typescript showLineNumbers
let name: string = "Alexis"
let score: number = 98;

```
    
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDE0NjA1MTc4LC0zNTU1NzU4MywtMTc1Nz
cxNzM1MCw5NDUxMDQyMDUsMTg2MTcyMjI1NiwtMjA1OTMyNDU1
OV19
-->