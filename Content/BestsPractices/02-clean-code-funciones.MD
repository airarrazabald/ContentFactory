# Funciones

## Introducción:

La importancia de escribir funciones pequeñas, cohesivas y fáciles de entender. Las funciones bien diseñadas hacen que el código sea más legible, mantenible y reutilizable.

## Principios Clave:

- **Pequeñas:** Las funciones deben ser lo más pequeñas posible, idealmente con un máximo de 20-30 líneas de código.
- **Cohesivas:** Las funciones deben realizar una única tarea bien definida.
- **Entradas y salidas:** Las funciones deben tener un número limitado de entradas y salidas bien definidas.
- **Nombres significativos:** Los nombres de las funciones deben indicar claramente la acción que realizan.
- **Sin efectos secundarios:** Las funciones no deben modificar variables globales o el estado del sistema de forma inesperada.

## Ejemplo de Funciones en C#:

### Mala Práctica:

```csharp
public void CalcularTotalCompra(Cliente cliente, List<Producto> productos) {

  // Calcular el total sin impuestos

  decimal totalSinImpuestos = 0;
  foreach (Producto producto in productos) {
    totalSinImpuestos += producto.Precio;
  }

  // Calcular el impuesto

  decimal impuesto = totalSinImpuestos * 0.15m;

  // Calcular el total

  decimal total = totalSinImpuestos + impuesto;

  // Mostrar el total

  Console.WriteLine("Total: " + total);

}
```

### Beuna Práctica

```csharp
public decimal CalcularTotalSinImpuestos(List<Producto> productos) {

  decimal total = 0;
  foreach (Producto producto in productos) {
    total += producto.Precio;
  }

  return total;

}

public decimal CalcularImpuesto(decimal totalSinImpuestos) {
  return totalSinImpuestos * 0.15m;
}

public void MostrarTotal(Cliente cliente, decimal total) {
  Console.WriteLine("Cliente: " + cliente.Nombre);
  Console.WriteLine("Total: " + total);
}

public void CalcularTotalCompra(Cliente cliente, List<Producto> productos) {

  decimal totalSinImpuestos = CalcularTotalSinImpuestos(productos);
  decimal impuesto = CalcularImpuesto(totalSinImpuestos);
  decimal total = totalSinImpuestos + impuesto;

  MostrarTotal(cliente, total);

}
```

### En la buena práctica:

- Se han dividido las responsabilidades en funciones más pequeñas y cohesivas.
- Las funciones tienen nombres significativos que indican la acción que realizan.
- Las funciones no tienen efectos secundarios.

### En la mala práctica:

- La función CalcularTotalCompra es demasiado grande y compleja.
- La función realiza varias tareas diferentes, lo que la hace difícil de entender y mantener.
- La función modifica variables globales, lo que puede generar errores inesperados.
- Al escribir funciones pequeñas y cohesivas, el código se vuelve más legible, mantenible y reutilizable.

## Conclusión

Escribir funciones pequeñas, cohesivas y con nombres significativos es una práctica fundamental para escribir código limpio. Al seguir los principios y consejos mencionados, puedes mejorar la legibilidad, la mantenibilidad y la reutilizabilidad de tu código.