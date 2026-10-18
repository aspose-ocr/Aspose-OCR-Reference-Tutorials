---
category: general
date: 2026-10-18
description: Compila un proyecto Java con Maven y ejecútalo desde la línea de comandos
  usando los comandos Maven clean, compile y exec. Aprende cómo construir y ejecutar
  una aplicación Java de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: es
lastmod: 2026-10-18
og_description: Compila un proyecto Java con Maven y ejecútalo desde la línea de comandos
  con una guía paso a paso. Domina maven clean compile run para construir y ejecutar
  una aplicación Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Compilar proyecto Java con Maven – ejecutar desde la línea de comandos
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Compilar proyecto Java con Maven y ejecutarlo desde la línea de comandos
url: /es/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compilar proyecto Java con Maven y ejecutar desde la línea de comandos

Si necesitas **compilar proyecto Java con Maven** y lanzar la clase resultante directamente desde una terminal, esta guía te muestra exactamente cómo. Al final del tutorial podrás limpiar artefactos antiguos, compilar el código fuente y **ejecutar clase Java desde la línea de comandos** usando una única cadena de comandos de Maven.

El tutorial cubre todo lo que necesitas saber para **construir y ejecutar una aplicación Java** con Maven, incluidos los plugins requeridos, los problemas comunes y consejos para shells basados en Windows y Unix. No se necesita documentación externa—simplemente sigue los pasos a continuación.

## Prerequisitos

* Java Development Kit (JDK) 8 o superior instalado y `JAVA_HOME` configurado.
* Apache Maven 3.6+ disponible en tu `PATH`.
* Un proyecto Maven que contenga un `pom.xml` y una clase Java con un método `public static void main(String[] args)` (para este ejemplo la clase es `com.aspose.ocr.examples.SimpleOcrDemo`).

## Compilar proyecto Java con Maven

El primer paso es eliminar cualquier clase compilada previamente y otros artefactos de construcción. Ejecutar `mvn clean` garantiza un inicio limpio y evita que bytecode obsoleto cause errores en tiempo de ejecución.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*¿Por qué limpiar?* Maven almacena las clases compiladas en `target/`. Si omites la fase de limpieza, los archivos `.class` antiguos pueden permanecer y ocultar problemas de compilación, especialmente después de refactorizar nombres de paquetes.

## Ejecutar clase Java desde la línea de comandos

Después de limpiar, compila los archivos fuente. La fase `compile` de Maven traduce todas las fuentes en `src/main/java` a bytecode y coloca los resultados en `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Ahora tienes una salida de **compilación de código fuente con Maven** lista para ejecutar. El siguiente comando ejecuta la clase compilada sin necesidad de un JAR separado.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

El objetivo `exec:java` del plugin **maven clean compile run** lanza la clase especificada directamente desde el directorio de salida compilado. Esta es la forma más rápida de **ejecutar clase Java desde la línea de comandos** durante el desarrollo.

### Salida esperada

Cuando la demostración se ejecuta correctamente deberías ver algo similar a:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Si recibes una `ClassNotFoundException`, verifica nuevamente el nombre de clase totalmente calificado y asegúrate de que se encuentre bajo `src/main/java`.

## Flujo de trabajo Maven clean compile run

Combinar los tres comandos produce un flujo de trabajo compacto y repetible:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*¿Por qué encadenarlos?* Combinar las fases elimina la necesidad de pulsar **Enter** tres veces y reduce la probabilidad de olvidar un paso. Maven ejecutará las fases en el orden en que aparecen, garantizando una compilación limpia antes de la ejecución.

### Consejos para un flujo de trabajo más fluido

| Consejo | Descripción |
|-----|-------------|
| **Usar un perfil** | Define un perfil Maven que agrupe `clean`, `compile` y `exec:java` para que puedas ejecutar `mvn demo` en lugar de escribir la cadena completa. |
| **Agregar opciones JVM** | Pasa `-Dexec.args="-Xmx512m"` para aumentar el tamaño del heap en aplicaciones que consumen mucha memoria. |
| **Multiplataforma** | En Windows usa `mvn.cmd` mientras que en shells Unix usa `mvn`. El mismo comando funciona en ambos entornos. |

## Construir y ejecutar aplicación Java con Maven

Si prefieres un artefacto distribuible, puedes dejar que Maven empaquete tus clases compiladas en un JAR ejecutable y luego ejecutarlo con el comando estándar `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Este enfoque es útil cuando necesitas **construir y ejecutar una aplicación Java** en un servidor donde Maven no está instalado. Sin embargo, para desarrollo rápido la secuencia **maven clean compile run** es más rápida porque omite el paso de empaquetado.

## Compilación de código fuente con Maven – problemas comunes

Aunque los comandos son sencillos, los desarrolladores a menudo encuentran los siguientes problemas:

1. **Falta `exec-maven-plugin`**  
   Si Maven no puede encontrar el objetivo `exec:java`, agrega el plugin a tu `pom.xml`:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Classpath incorrecto**  
   Maven compila en `target/classes`. Si mueves archivos manualmente o cambias el directorio de salida predeterminado, el objetivo `exec:java` puede no localizar tu clase. Mantén la estructura predeterminada a menos que tengas una razón específica para cambiarla.

3. **Usar la versión incorrecta de JDK**  
   Maven hereda el JDK de `JAVA_HOME`. Compilar código fuente con JDK 11 y ejecutarlo con JDK 8 provocará `UnsupportedClassVersionError`. Verifica la versión del JDK con `java -version` y `mvn -v`.

4. **Problemas de comillas en el shell**  
   En Unix, envuelve el valor de `-Dexec.mainClass` entre comillas simples si contiene caracteres especiales:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   En Windows, las comillas dobles funcionan sin problemas.

Al abordar estos puntos, podrás **ejecutar clase Java desde la línea de comandos** de manera fiable en cualquier entorno.

## Consejo profesional: automatizar con un script

Para equipos que reconstruyen la demostración con frecuencia, crea un pequeño script shell o batch:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Hazlo ejecutable (`chmod +x run-demo.sh`) y ejecuta `./run-demo.sh`. Esto elimina errores de escritura y asegura que cada desarrollador siga la secuencia exacta **maven clean compile run**.

## Conclusión

Ahora sabes cómo **compilar proyecto Java con Maven** y ejecutar instantáneamente **clase Java desde la línea de comandos** usando los objetivos clean, compile y exec de Maven. El flujo de trabajo paso a paso garantiza una compilación limpia, elimina artefactos obsoletos y te permite **construir y ejecutar una aplicación Java** con una sola línea de comandos.

A continuación, podrías explorar:

* Agregar el **shade plugin** para producir un uber‑JAR para despliegue.  
* Configurar perfiles Maven para diferentes entornos (dev, test, prod).  
* Integrar pruebas unitarias con `mvn test` antes del paso de compilación.

¡Experimenta con estas variaciones para adaptar el flujo de trabajo a tus propios proyectos, y tendrás una canalización de compilación robusta y repetible que funciona en Windows, macOS y Linux. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar OCR en Java – Guía completa paso a paso](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Ejecutar OCR en una imagen con Java – Guía completa de Aspose OCR](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Cómo realizar OCR con Aspose OCR en Java – Guía paso a paso](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}