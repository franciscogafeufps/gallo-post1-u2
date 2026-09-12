# gallo-post1-u2
Post-contenido — Exportación de reportes académicos con patrones creacionales justificados

# Post-contenido Unidad 2: Patrones Creacionales

## Descripción
Repositorio del post-contenido de la Unidad 2 (Patrones de Diseño de Software). Proyecto Maven único (`exportador-reportes/`) que resuelve la exportación de reportes académicos en múltiples formatos garantizando la coherencia de familias (Parte 1) y la configuración compleja con validación de estados (Parte 2).

## Cómo ejecutar
\`\`\`bash
cd exportador-reportes
mvn compile
mvn exec:java -Dexec.mainClass="com.patrones.u2.Main"
\`\`\`

## Decisiones de diseño

### Decisión 1: Abstract Factory vs. Factory Method (Parte 1)
* **Patrón elegido:** Abstract Factory.
* **Justificación basada en el problema:** El sistema exige que el cuerpo del reporte y su encabezado/pie de página pertenezcan estrictamente al mismo formato de salida y no se mezclen de forma inconsistente (por ejemplo, evitar combinar un cuerpo Excel con un encabezado PDF). Dado que se trata de crear una familia completa de productos relacionados que deben permanecer coordinados, el patrón *Abstract Factory* es la decisión correcta. Se descartó *Factory Method* clásico porque este último se enfoca en instanciar un único producto aislado por subclase, lo que no garantiza por sí solo la consistencia entre múltiples piezas de una misma familia de exportación.

### Decisión 2: Mecanismo de extensibilidad de formatos (Parte 1)
* **Opción elegida:** Registro dinámico basado en `Map>` (`ReportFactoryRegistry`).
* **Justificación:** Se descartó el uso de una cadena de condicionales `switch` o `if/else` porque cada vez que el área de datos solicite incorporar un nuevo formato en el futuro (como el formato CSV planificado), obligaría a modificar el código fuente existente de la clase central, violando directamente el principio Open/Closed (OCP). El registro dinámico permite registrar nuevos proveedores mediante lambdas o referencias a métodos sin tocar las clases ya probadas y estables.