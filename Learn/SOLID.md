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

```typescript

```

## 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3OTg5ODIxMTRdfQ==
-->