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

## 3. L - Liskov Substitution Principle (Principio de Sustitución de Liskov)

Las subclases deben poder **sustituir** a sus clases base sin que el programa falle. En otras palabras, si una función espera una clase base, debería poder trabajar también con cualquier subclase sin comportarse de manera inesperada.

Aquí, `Penguin` no debería ser una subclase de `Bird` si no puede volar, ya que rompe el principio de Liskov. En este caso, podríamos crear una jerarquía diferente para representar aves que no vuelan.

```typescript
class Bird {
    fly(): string {
        return "Flying!";
    }
}

class Sparrow extends Bird {}
class Penguin extends Bird {
    fly(): string {
        throw new Error("Penguins can't fly!");
    }
}

function makeBirdFly(bird: Bird) {
    console.log(bird.fly());
}

const sparrow = new Sparrow();
makeBirdFly(sparrow); // OK

const penguin = new Penguin();
makeBirdFly(penguin); // Error: Penguins can't fly
```

## 4. I - Interface Segregation Principle (Principio de Segregación de Interfaces)

Las clases no deben estar forzadas a implementar interfaces que no usan. Es mejor tener varias interfaces pequeñas y específicas en lugar de una interfaz grande y general.

De esta forma, `Dog` solo implementa lo que realmente necesita (`Eater`), mientras que `Bird` puede implementar ambas (`Eater` y `Flyer`).

#### Ejemplo
```typescript
// Interfaz grande que viola el principio
interface Animal {
    eat(): void;
    fly(): void;
}

// Separando interfaces
interface Eater {
    eat(): void;
}

interface Flyer {
    fly(): void;
}

// Aplicando el principio
class Dog implements Eater {
    eat(): void { /* code to eat */ }
}

class Bird implements Eater, Flyer {
    eat(): void { /* code to eat */ }
    fly(): void { /* code to fly */ }
}
```

## 5. **D - Dependency Inversion Principle (Principio de Inversión de Dependencias)**

Las clases deben depender de **abstracciones (interfaces)** y no de implementaciones concretas. Esto significa que en lugar de crear dependencias directas, es mejor trabajar con interfaces para que el código sea más flexible.

Ahora, `Switch` puede trabajar con cualquier dispositivo que implemente la interfaz `Switchable`, no solo con `LightBulb`. Esto hace que el código sea más flexible y escalable.

```typescript
// Sin principio de inversión de dependencias
class LightBulb {
    turnOn() { /* code to turn on light bulb */ }
}

class Switch {
    private bulb: LightBulb = new LightBulb();
    toggle() {
        this.bulb.turnOn();
    }
}

// Con principio de inversión de dependencias
interface Switchable {
    turnOn(): void;
}

class LightBulb implements Switchable {
    turnOn() { /* code to turn on light bulb */ }
}

class Fan implements Switchable {
    turnOn() { /* code to turn on fan */ }
}

class Switch {
    constructor(private device: Switchable) {}
    toggle() {
        this.device.turnOn();
    }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzAzODY4MDg2XX0=
-->