# gallo-post1-u2
Post-contenido — Exportación de reportes académicos con patrones creacionales justificados

# Post-contenido Unidad 2: Patrones Creacionales

## Descripción
Repositorio del post-contenido de la Unidad 2 de Patrones de Diseño de Software - Sexto Semestre. Contiene un único proyecto Maven (`exportador-reportes/`) que resuelve la exportación de reportes académicos garantizando coherencia de familias (Parte 1) y la configuración compleja con validación de estados y análisis de Singleton (Parte 2).

## Cómo ejecutar
\`\`\`bash
cd exportador-reportes
mvn compile
mvn exec:java -Dexec.mainClass="com.patrones.u2.Main"
\`\`\`

## Decisiones de diseño

### Decisión 1: Abstract Factory vs. Factory Method (Parte 1)
* **Patrón elegido:** Abstract Factory.
* **Justificación:** El sistema exige que el cuerpo y el encabezado/pie pertenezcan estrictamente al mismo formato sin mezclarse de forma inconsistente. Abstract Factory garantiza la creación de familias completas de productos coordinados. Se descartó Factory Method clásico por enfocarse en productos aislados.

### Decisión 2: Mecanismo de extensibilidad de formatos (Parte 1)
* **Opción elegida:** Registro dinámico basado en `Map>` (`ReportFactoryRegistry`).
* **Justificación:** Se descartó el `switch` o `if/else` para cumplir con el principio Open/Closed (OCP), permitiendo registrar nuevos formatos (como el CSV planeado) sin modificar el código existente.

### Decisión 3: Builder vs. constructor telescópico vs. setters (Parte 2)
* **Opción elegida:** Patrón Builder con clase interna estática y validaciones en `build()`.
* **Justificación:** Se descartó un constructor con 9 parámetros (orden confuso de tipos repetidos), constructores sobrecargados (explosión combinatoria) y setters sueltos (objetos en estados inconsistentes a medio configurar). Builder permite una construcción fluida y valida reglas estrictas (como exigir una ruta de salida si se solicita compresión).

### Decisión 4: ¿ReportFactoryRegistry necesita ser Singleton? (Parte 2)
* **Conclusión:** NO.
* **Justificación:** El registro no requiere identidad de objeto ni polimorfismo de instancia, su inicialización no es costosa, el campo estático ya asegura una única fuente de verdad en la JVM, y un Singleton clásico bloquearía escenarios futuros *multi-tenant* donde distintas instituciones requieran registros independientes.

## Herramientas Utilizadas
* Java JDK 17
* Apache Maven 3.8+
* VS Code & Git / GitHub

## Conclusiones
El desarrollo de esta actividad permitió aplicar criterios objetivos de selección entre patrones creacionales complejos (como Abstract Factory y Builder) frente a alternativas simples, demostrando que la arquitectura de software debe responder a necesidades reales del problema y no a la aplicación dogmática de patrones por costumbre.