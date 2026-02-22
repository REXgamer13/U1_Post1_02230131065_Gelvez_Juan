# U1_Post1_02230131065_Gelvez_Juan

- Nombre: Juan Sebastián Gelvez Botia
- Código: 02230131065
- Curso: PATRONES DISEÑO DE SOFTWARE - CUC13671A
## Objetivo
Desarrollar la capacidad de identificar violaciones de los principios SOLID en código Java existente y aplicar refactorizaciones sistemáticas para producir código más limpio, desacoplado y mantenible, utilizando interfaces, inyección de dependencias y separación de responsabilidades.
## Identificación de Violaciones a SOLID

Analice el código y documente en su README.md las violaciones que encuentre. Debe
***identificar al menos 4 violaciones.*** Considere qué responsabilidades tiene esta clase, de
qué depende directamente, y qué tan fácil sería agregar nueva funcionalidad.

1. Violación del Principio S de Responsabilidad Única (SRP)
    
    esta clase OrderManager{...} viola directamente porque tiene múltiples responsabilidades, como la gestión de pedidos, el cálculo de precios y la generación de informes, lo que hace que el código sea difícil de mantener y escalar.

2. Violación en el método de public void createOrder(String customer, String product, double price, int quantity) {...}
    
    en este bloque de código, el método acepta muchos parámetros por lo que en el 'Clean Code' se recomienda que los métodos no tengan más de 3 parámetros, lo que dificulta la legibilidad y el mantenimiento del código.
    
    además, el método también **viola el principio de O de Abierto/Cerrado (OCP)** Porque cualquier cambio en la lógica los descuentos requeriría modificar este método, lo que puede introducir errores y afectar otras partes del sistema.
    esta misma ocurre también en Calcular impuestos y generar reporte.
    ```
    // Calcular impuestos 
    public double calculateTax(String orderId) {
    for (String[] o : orders) {
    if (o[0].equals(orderId)) {
    double total = Double.parseDouble(o[3]);
    return total * 0.19;  // IVA 19%
    }
    }
    return 0;
    }
    // Generar reporte
    public String generateReport() {
    StringBuilder sb = new StringBuilder();
    sb.append("=== REPORTE DE PEDIDOS ===\n");
    double grandTotal = 0;
    for (String[] o : orders) {
    sb.append(o[0] + " | " + o[1] + " | $" + o[3] + "\n");
    grandTotal += Double.parseDouble(o[3]);
    }
    sb.append("TOTAL: $" + grandTotal);
    System.out.println(sb.toString());
    return sb.toString();
    }
    ```
    cualquier cambio en la lógica de cálculo de impuestos o generación de reportes requeriría modificar estos métodos, lo que puede introducir errores y afectar otras partes del sistema.

3. Violación en el bloque de código con la lógica de 'guardar archivo':

    ```
    // Guardar en archivo
    try {
    java.io.FileWriter fw = new java.io.FileWriter("orders.txt", true);
    fw.write(orderId + "," + customer + "," + total + "\n");
    fw.close();
    } catch (Exception e) { e.printStackTrace(); }
    ```
   Este bloque de código viola el principio de D de Dependency Inversion Principle (DIP) porque la lógica de guardar en un archivo está acoplada directamente a la clase OrderManager, lo que dificulta la reutilización y el mantenimiento del código. Si se quisiera cambiar la forma de almacenamiento (por ejemplo, a una base de datos), sería necesario modificar esta clase, lo que puede introducir errores y afectar otras partes del sistema.

4. Violación al principio I de Segregación de Interfaces (ISP)

    La clase OrderManager no implementa ninguna interfaz, lo que hace que esté acoplada directamente a su implementación. Esto dificulta la reutilización y el mantenimiento del código, ya que cualquier cambio en la lógica de gestión de pedidos requeriría modificar esta clase, lo que puede introducir errores y afectar otras partes del sistema. Además, al no tener interfaces, no se pueden crear implementaciones alternativas para diferentes tipos de pedidos o sistemas de almacenamiento, lo que limita la flexibilidad del código.
    las interfaces que se podrían implementar es en los bloques de código de:
    ```
       // Enviar notificación 
    System.out.println("EMAIL a " + customer +": Su pedido " + orderId + " ha sido creado.");
    

   ```
   ```
    // Generar reporte
    public String generateReport() {
    StringBuilder sb = new StringBuilder();
    sb.append("=== REPORTE DE PEDIDOS ===\n");
    double grandTotal = 0;
    for (String[] o : orders) {
    sb.append(o[0] + " | " + o[1] + " | $" + o[3] + "\n");
    grandTotal += Double.parseDouble(o[3]);
    }
    sb.append("TOTAL: $" + grandTotal);
    System.out.println(sb.toString());
    return sb.toString();
    }
    ```
   
5. Violación al principio de L de Sustitución de Liskov (LSP)

    indirectamente, La clase OrderManager no tiene una jerarquía de clases ni implementa ninguna interfaz, lo que hace que esté acoplada directamente a su implementación. Esto dificulta la reutilización y el mantenimiento del código, ya que cualquier cambio en la lógica de gestión de pedidos requeriría modificar esta clase, lo que puede introducir errores y afectar otras partes del sistema. Además, al no tener una jerarquía de clases o interfaces, no se pueden crear implementaciones alternativas para diferentes tipos de pedidos o sistemas de almacenamiento, lo que limita la flexibilidad del código o aplicar el principio de herencia.

