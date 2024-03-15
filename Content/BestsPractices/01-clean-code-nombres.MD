# Nombres Significativos

## Introducción:

El capítulo 2 de "Clean Code" de Robert C. Martin se centra en la importancia de elegir nombres significativos para variables, funciones, clases y otros elementos del código. Los nombres significativos ayudan a comprender el código a simple vista, lo que facilita su mantenimiento y colaboración.

## Principios Clave:

- **Evitar nombres genéricos:** No usar nombres como `x, y, z, a1, b2, etc.,` ya que no dan información sobre el propósito del elemento.
- **Utilizar nombres descriptivos:** Elegir nombres que describan claramente lo que representa el elemento. Por ejemplo, nombreCliente es mejor que nombre.
- **Utilizar verbos para las funciones:** Los nombres de las funciones deben indicar la acción que se realiza. Por ejemplo, `calcularAreaTriangulo` es mejor - que `areaTriangulo`.
- **Utilizar sustantivos para las variables:** Los nombres de las variables deben indicar el tipo de dato que almacenan. Por ejemplo, `edadCliente` es mejor que `edad`.
- **Considerar el contexto:** El nombre debe tener sentido en el contexto del código en el que se utiliza.

## Ejemplo en C#:

### Mala práctica:

```csharp
public class MiClase { // Nombre genérico, no indica el propósito de la clase

  public void Calcular() { // Nombre genérico, no indica qué se calcula
    int num; // Nombre genérico, no indica qué tipo de dato almacena ni su propósito
    num = 10; // Asignación sin contexto
    if (num > 5) { // Condición sin contexto
      // ...
    }
  }
}
```

### Buena Práctica

```csharp
public class CalculadoraPrecioTotal { // Nombre descriptivo, indica el propósito de la clase

  public void CalcularPrecioTotal(Producto producto, int cantidad) { // Nombre descriptivo, indica la acción que realiza la función y sus parámetros

    decimal precioTotal = producto.Precio * cantidad; // Asignación con contexto
    if (precioTotal > 100) { // Condición con contexto
      // ...
    }
  }
}
```

## Conclusión:

Elegir nombres significativos es una práctica fundamental para escribir código limpio. Al seguir los principios y consejos mencionados, puedes mejorar la legibilidad, la mantenibilidad y la colaboración de tu código.