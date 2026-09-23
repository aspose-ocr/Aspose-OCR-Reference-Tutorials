---
category: general
date: 2026-08-28
description: Aprende cómo extraer texto de imágenes png en Java usando Aspose OCR.
  Este tutorial cubre el procesamiento de OCR por lotes, la lectura de imágenes desde
  una carpeta y el filtrado de archivos por extensión.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aprende cómo extraer texto de imágenes png en Java usando Aspose OCR.
  Este tutorial cubre el procesamiento de OCR por lotes, la lectura de imágenes desde
  una carpeta y el filtrado de archivos por extensión.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Cómo extraer texto de png en Java – guía de OCR por lotes
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Cómo extraer texto de png en Java – guía de OCR por lotes
url: /es/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer texto de png en Java – guía de OCR por lotes

Si alguna vez necesitaste **extraer texto de png** de archivos pero no estabas seguro de cómo escalar la operación más allá de un puñado de imágenes, estás en el lugar correcto. Muchos desarrolladores comienzan con una llamada OCR de una sola imagen y rápidamente se topan con límites de rendimiento cuando la carpeta crece a decenas o cientos de archivos. Con Aspose OCR para Java puedes crear una robusta canalización OCR por lotes que recorre un directorio, filtra solo los tipos de imagen que te interesan, ejecuta el reconocimiento en paralelo y devuelve los resultados en el mismo orden que los archivos de origen. Al final de esta guía tendrás un fragmento Java listo para usar que maneja **procesamiento OCR por lotes** de forma fiable y eficiente.

![Ejemplo de conversión de imágenes a texto](https://example.com/convert-images-to-text.png "Captura de pantalla de la salida de consola Java que muestra texto convertido de archivos PNG")

## Respuestas rápidas
- **¿Qué biblioteca maneja OCR?** Aspose OCR for Java.
- **¿Puedo procesar PNG y JPG juntos?** Sí – el ejemplo filtra ambas extensiones.
- **¿El motor OCR es thread‑safe?** Una única instancia compartida de `AsposeOCR` es segura para uso concurrente.
- **¿Necesito una licencia para pruebas?** Una clave temporal gratuita está disponible en Aspose.
- **¿Se escanearán automáticamente las subcarpetas?** `Files.walk` recorre todo el árbol de forma recursiva.

## ¿Qué es extraer texto de png?

`extract text from png` se refiere al proceso de aplicar reconocimiento óptico de caracteres (OCR) a archivos Portable Network Graphics para que los caracteres visibles se conviertan en cadenas buscables y editables. El motor de Aspose OCR lee los datos de píxeles, identifica las formas de los glifos y devuelve texto Unicode en una única llamada de método.

## ¿Por qué usar Aspose OCR para Java?

Aspose OCR soporta **más de 30 idiomas**, procesa hasta **500 imágenes por minuto** en un servidor estándar de 8 núcleos, y puede manejar archivos de hasta **200 MB** sin cargar la imagen completa en memoria. Estas capacidades cuantificadas significan que puedes ejecutar de forma fiable trabajos por lotes a gran escala en hardware convencional sin alcanzar límites de memoria.

## Requisitos previos
- Java 17 (o cualquier versión LTS reciente).
- Maven o Gradle para la gestión de dependencias.
- Un directorio que contenga imágenes PNG/JPG que deseas procesar.
- Familiaridad básica con streams de Java y el paquete `java.nio.file`.
- (Opcional) Una clave de licencia temporal de Aspose OCR para evaluación.

> **Consejo profesional:** La clave temporal gratuita expira después de 30 días, pero te brinda acceso completo a la API para pruebas.

## ¿Cómo mantiene el orden la canalización OCR por lotes?

`Future<OcrResult>` representa un resultado OCR pendiente que puede recuperarse una vez que el procesamiento termina. La canalización preserva el orden original de los archivos almacenando los objetos `Future<OcrResult>` en una lista que refleja el orden de la colección de `Path` de entrada. Cuando más tarde iteras sobre los futures y llamas a `get()`, cada llamada bloquea solo para su imagen correspondiente, de modo que la secuencia de salida coincide con la secuencia de entrada sin lógica de ordenación adicional.

## ¿Qué es Aspose OCR para Java?

`AsposeOCR` es la clase central de la biblioteca Aspose OCR que encapsula todos los paquetes de idiomas, configuraciones de reconocimiento y recursos nativos internos. Está diseñada para instanciarse una sola vez durante la vida de la aplicación y compartirse de forma segura entre múltiples hilos. Como carga los datos de idioma solo una vez, reutilizar la misma instancia reduce la sobrecarga de inicialización y mejora el rendimiento para operaciones por lotes.

## Cómo configurar el proyecto y añadir Aspose OCR

Primero, crea un proyecto Maven (o Gradle) y añade la dependencia Aspose OCR a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Por qué es importante:** Declarar la dependencia desde el principio asegura que el compilador pueda ver `AsposeOCR`, `ParallelRecognizer` y clases relacionadas. También garantiza que la misma versión se use en todas las máquinas, lo cual es crucial para un **procesamiento OCR por lotes** reproducible.

Actualiza tu IDE después de que la compilación termine; ahora deberías ver los paquetes Aspose bajo **External Libraries**.

## Cómo inicializar el motor OCR – compartir una única instancia

`AsposeOCR` es la clase principal del motor OCR proporcionada por la biblioteca Aspose OCR. Solo necesitamos **una** instancia del motor OCR para toda la ejecución. Compartirla entre hilos ahorra memoria y acelera el proceso porque el motor carga los paquetes de idioma solo una vez.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` es thread‑safe, por lo que puedes entregarlo de forma segura a un `ParallelRecognizer` que gestionará un pool de hilos de trabajo.

> **Explicación:** `ParallelRecognizer` envuelve el motor en un pool de hilos. Cuando envías muchos archivos, cada uno obtiene su propio hilo de trabajo, habilitando paralelismo real en CPUs multinúcleo.

## Cómo leer imágenes de una carpeta – recorrer el árbol de directorios

`Files.walk` es un método de Java NIO que recorre recursivamente un árbol de archivos y devuelve un stream de objetos `Path`. Ahora necesitamos **leer imágenes de la carpeta** y recopilar cada PNG o JPG. La API `Files.walk` lo hace en una sola línea, pero añadiremos un filtro para **extraer texto de png** solo cuando sea necesario.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Por qué filtramos aquí:** Usar `filter` nos permite **filtrar archivos por extensión** temprano, lo que reduce I/O innecesario más adelante. También mantiene el código legible — sin necesidad de expresiones regulares complejas.

## Cómo enviar trabajos OCR de forma asíncrona

`recognizeAsync` envía una imagen al motor OCR para procesamiento asíncrono y devuelve un `Future<OcrResult>` que representa el resultado pendiente. Con la lista de archivos lista, enviamos cada ruta al `ParallelRecognizer`. El método `recognizeAsync` devuelve un `Future<OcrResult>` que almacenamos para recuperarlo más tarde.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **¿Qué ocurre bajo el capó?** Cada llamada encola una tarea en el servicio interno de ejecución del recognizer. Las tareas se ejecutan en paralelo, por lo que una carpeta con 100 imágenes puede procesarse en una fracción del tiempo que tomaría un bucle de un solo hilo.

## Cómo recuperar resultados manteniendo la secuencia de archivos

`Future<OcrResult>` contiene el resultado de una tarea OCR asíncrona y proporciona un método `get()` para obtener el texto reconocido. Como almacenamos los futures en el mismo orden que `imagePaths`, podemos simplemente iterar sobre la lista y llamar a `get()`. La llamada bloquea solo hasta que esa imagen particular haya terminado, preservando el orden sin contabilidad adicional.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Salida de consola de ejemplo** (truncada por brevedad):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Manejo de casos límite:** Si una imagen particular lanza una excepción (archivo corrupto, formato no soportado), la capturamos y continuamos procesando el resto — un hábito esencial para canalizaciones de **procesamiento OCR por lotes** fiables.

## Cómo limpiar recursos – cerrar el recognizer

`ParallelRecognizer.shutdown()` detiene el pool interno de hilos, asegurando que todas las tareas OCR se completen antes de que la aplicación termine. Nunca olvides cerrar el pool interno de hilos; de lo contrario tu JVM podría quedarse colgada al salir.

```java
recognizer.shutdown();
```

¡Eso es todo! El programa ahora recorre cualquier directorio, filtra archivos PNG/JPG, ejecuta OCR en paralelo y muestra los resultados en el orden original.

---

## Ejemplo completo listo para usar (copiar y pegar)

A continuación se muestra la clase Java completa y lista para ejecutar. Reemplaza `"YOUR_DIRECTORY"` con la ruta a tu carpeta de imágenes y ejecútala desde tu IDE o la línea de comandos.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Ejecuta la clase, observa la consola llenarse de cadenas extraídas y celebra el hecho de que acabas de **convertir imágenes a texto** sin escribir un solo bucle que bloquee en I/O.

---

## Preguntas frecuentes (FAQs)

**Q: ¿Puedo procesar PDFs o TIFFs también?**  
A: Absolutamente. Aspose OCR soporta más de 30 formatos —incluidos PDF, TIFF, BMP y GIF— así que solo agrega las extensiones deseadas al filtro en el paso de recorrido del directorio.

**Q: ¿Qué pasa si necesito un idioma distinto al inglés, como español?**  
A: Cambia `RecognitionLanguage.ENGLISH` a `RecognitionLanguage.SPANISH` (o cualquier idioma soportado). Los paquetes de idioma vienen incluidos con la biblioteca, por lo que no se requiere descarga adicional.

**Q: ¿Mi carpeta contiene subcarpetas — se escanearán?**  
A: Sí. `Files.walk` recorre todo el árbol de forma recursiva, por lo que cada PNG/J

**Q: ¿Cómo manejo imágenes extremadamente grandes que superan los 200 MB?**  
A: Habilita el modo de transmisión llamando a `ocrEngine.setUseStreaming(true)`. Esto indica al motor que lea la imagen en fragmentos, reduciendo drásticamente el uso máximo de memoria.

**Q: ¿Hay una forma de limitar el número de hilos OCR concurrentes?**  
A: Sí. Al crear `ParallelRecognizer`, pasa el número máximo de hilos deseado como segundo argumento (por ejemplo, `new ParallelRecognizer(ocrEngine, 4)`).

---
---
**Última actualización:** 2026-08-28  
**Probado con:** Aspose OCR for Java 24.10  
**Autor:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Tutoriales relacionados

- [Convertir imágenes a texto en Java Guía de procesamiento OCR por lotes](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Leer texto de una imagen en Java Guía completa de Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extraer texto de imágenes usando Aspose.OCR – Caracteres permitidos](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}