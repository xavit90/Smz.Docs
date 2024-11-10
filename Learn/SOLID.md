# Principios SOLID

Los principios **SOLID** son cinco reglas básicas para escribir código de calidad en programación orientada a objetos. Estos principios ayudan a que el código sea más fácil de entender, mantener y escalar.

Estas reglas ayudan a escribir código más limpio y manejable:

1. **S**: Mantén cada clase con una única responsabilidad.
2. **O**: Abre el código para extensiones y evita cambiar el código existente.
3. **L**: Las subclases deben ser capaces de sustituir a la clase base.
4. **I**: Crea interfaces pequeñas y específicas para evitar que las clases implementen cosas que no usan.
5. **D**: Trabaja con interfaces en lugar de dependencias directas para hacer el código más flexible.
Siguiendo estos principios, el código será más fácil de modificar, entender y reutilizar, facilitando su mantenimiento a largo plazo.

## 1. S - Single Responsibility Principle (Principio de Responsabilidad Única)

Cada clase o módulo debe tener una sola responsabilidad. Esto significa que debe hacer solo una cosa y hacerlo bien. Si tienes una clase que hace varias cosas, será difícil de mantener y entender.

Aquí, `UserRepository` solo maneja la lógica de guardar usuarios y `UserNotifier` solo maneja el envío de correos electrónicos. Así, cada clase tiene **una única responsabilidad**.

#### Ejemplo
```typescript
// Clase que viola el principio (hace dos cosas)
class User {
    saveUserToDatabase() { /* code to save user */ }
    sendEmailToUser() { /* code to send email */ }
}

// Aplicando el principio de responsabilidad única
class UserRepository {
    saveUserToDatabase() { /* code to save user */ }
}

class UserNotifier {
    sendEmailToUser() { /* code to send email */ }
}
```

## 2. O - Open/Closed Principle (Principio de Abierto/Cerrado)

Una clase debe estar **abierta para ser extendida, pero cerrada para ser modificada**. Esto significa que deberías poder añadir nuevas funcionalidades sin cambiar el código existente, evitando romper el código anterior.

En este caso, `Rectangle` puede ser extendido por `Circle` para añadir una nueva forma sin modificar el código existente en `Rectangle`.

#### Ejemplo
```typescript
// Clase original
class Rectangle {
    constructor(public width: number, public height: number) {}
    area(): number {
        return this.width * this.height;
    }
}

// Usando herencia para añadir nuevas formas sin cambiar Rectangle
class Circle extends Rectangle {
    constructor(public radius: number) {
        super(0, 0); // Pasamos 0 para ancho y alto porque no se usan aquí
    }
    area(): number {
        return Math.PI * this.radius * this.radius;
    }
}
```

# 3. L - Liskov Substitution Principle (Principio de Sustitución de Liskov)

Las subclases deben poder **sustituir** a sus clases base sin que el programa falle. En otras palabras, si una función espera una clase base, debería poder trabajar también con cualquier subclase sin comportarse de manera inesperada.
``
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODg3NjkzOTddfQ==
-->