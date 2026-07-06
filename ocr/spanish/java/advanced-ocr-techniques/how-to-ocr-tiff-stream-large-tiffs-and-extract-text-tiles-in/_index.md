---
category: general
date: 2026-04-29
description: Aprende a hacer OCR de archivos TIFF usando el modo de transmisión de
  Aspose OCR. Esta guía te muestra cómo extraer teselas de texto de imágenes TIFF
  con teselas de manera eficiente.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: es
og_description: cómo hacer OCR de TIFF usando Aspose OCR streaming. Código paso a
  paso para extraer fragmentos de texto de imágenes TIFF grandes.
og_title: cómo hacer OCR a TIFF – Guía completa de streaming
tags:
- OCR
- Java
- Aspose
- TIFF
title: cómo hacer OCR a TIFF – Transmitir TIFF grandes y extraer mosaicos de texto
  en Java
url: /es/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo hacer OCR a TIFF – Transmitir TIFF grandes y extraer fragmentos de texto en Java

¿Alguna vez te has preguntado **cómo hacer OCR a TIFF** archivos que son demasiado grandes para cargarlos en memoria de una sola vez? No eres el único. Muchos desarrolladores se topan con un obstáculo cuando sus imágenes TIFF se dividen en docenas de mosaicos, y la llamada habitual `ocrEngine.recognize()` simplemente falla.  

¿La buena noticia? El modo de transmisión de Aspose OCR te permite alimentar cada mosaico como un flujo separado, de modo que puedes **extraer fragmentos de texto** sin desbordar tu heap. En este tutorial recorreremos un ejemplo completo y listo‑para‑ejecutar en Java, explicaremos por qué cada línea es importante y señalaremos los errores comunes que querrás evitar.

> **Lo que obtendrás:** un programa ejecutable que une los TIFF en mosaico al vuelo, imprime el texto combinado y te muestra cómo adaptar el código a otros idiomas o formatos de imagen.

---

## Requisitos previos

- **Java 17** o superior (el código usa try‑with‑resources, por lo que JDK 8+ funciona, pero JDK 17 es la LTS actual).
- **Aspose.OCR for Java** biblioteca (v23.10 o posterior). Añádela mediante Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Una carpeta que contiene los mosaicos TIFF individuales (p. ej., `tile_0.tif`, `tile_1.tif`, …).  
- Opcional: un IDE como IntelliJ IDEA o VS Code, pero un editor de texto simple funciona bien.

---

## Paso 1 – Preparar las rutas de los mosaicos (por qué es importante)

Antes de que el motor OCR pueda hacer algo, necesita saber dónde se encuentra cada pieza de la imagen. Codificar las rutas de forma estática está bien para una demostración, pero en producción probablemente escanearías un directorio o leerías un archivo de manifiesto.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Consejo profesional:** mantén los mosaicos en orden léxico (0, 1, 2…) porque el motor concatenará el texto reconocido en la misma secuencia en que alimentas los flujos.

---

## Paso 2 – Habilitar el modo de transmisión en el motor OCR (palabra clave principal)

Ahora creamos la instancia `OcrEngine` y activamos la transmisión. Este es el núcleo de **cómo hacer OCR a TIFF** sin cargar la imagen completa en RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**¿Por qué transmisión?**  
Cuando se llama a `setEnableStreaming(true)`, el motor trata cada `ImageStream` entrante como una continuación del anterior. Construye un lienzo virtual interno, une los mosaicos de forma virtual y ejecuta OCR una sola vez al final. Esto evita el “OutOfMemoryError” que ocurriría si intentaras cargar un TIFF de varios gigabytes de una sola vez.

---

## Paso 3 – Añadir cada mosaico como un flujo de entrada (palabra clave secundaria)

Este es el bucle que alimenta cada mosaico al motor. El bloque `try‑with‑resources` garantiza que el manejador de archivo se cierre rápidamente, lo cual es crucial cuando se manejan docenas de archivos.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Observa que la frase **extraer fragmentos de texto** está integrada de forma natural: cada iteración *extrae* el texto de un mosaico y lo añade al conjunto de resultados en crecimiento.

---

## Paso 4 – Ejecutar el reconocimiento y mostrar el texto combinado (palabra clave principal)

Después de que todos los mosaicos están en cola, una única llamada realiza OCR sobre la imagen virtual. El resultado contiene el texto completo, como si tuvieras un único TIFF masivo.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Salida esperada** (suponiendo que los mosaicos contengan la frase “Hello World” dividida entre ellos):

```
=== OCR Output ===
Hello World
```

Si tus mosaicos contienen más líneas, aparecerán en el mismo orden en que los proporcionaste. También puedes escribir `ocrResult.getText()` a un archivo para procesamiento posterior.

---

## Paso 5 – Ejemplo completo y ejecutable (todos los pasos en un solo lugar)

A continuación tienes el programa completo que puedes copiar y pegar en `StreamingExample.java`. Incluye todas las importaciones, comentarios y manejo de errores.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Guarda, compila y ejecuta:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Deberías ver el texto OCR concatenado impreso en la consola.

---

## Consejos avanzados y errores comunes (por qué funciona esto)

| Problema | Por qué ocurre | Cómo arreglar / Optimizar |
|----------|----------------|---------------------------|
| **Errores de falta de memoria** | Cargar un TIFF de tamaño completo en un `BufferedImage` consume todo el heap. | Usa el modo de transmisión (`setEnableStreaming(true)`) – el motor nunca materializa la imagen completa. |
| **Desajuste de orden de mosaicos** | Los archivos se ordenan alfabéticamente en lugar de numéricamente (p. ej., `tile_10.tif` antes de `tile_2.tif`). | Rellena los números con ceros (`tile_00.tif`, `tile_01.tif`) o ordena programáticamente usando `Comparator`. |
| **Idioma incorrecto** | OCR por defecto está en inglés; el texto no inglés se vuelve ilegible. | Llama a `ocrEngine.getLanguageSettings().setLanguage("fr")` (o cualquier código ISO soportado). |
| **Fallos parciales** | Un mosaico corrupto detiene todo el proceso. | Captura `IOException` por mosaico, registra el error y decide si continuar o abortar. |
| **Cuello de botella de rendimiento** | La E/S de disco domina al leer muchos archivos pequeños. | Agrupa los mosaicos en un ZIP y transmite desde memoria, o usa un SSD rápido. |

---

## Cuándo usar transmisión vs. OCR de imagen única

- **Transmisión** es ideal para:
  - TIFF de varias páginas o escaneos gigapíxel.
  - Situaciones donde la memoria es limitada (p. ej., contenedores Docker, dispositivos móviles).
  - Pipelines que ya reciben fragmentos de imagen (p. ej., flujos de cámara).

- **OCR de imagen única** funciona bien para:
  - Archivos PNG/JPEG pequeños (< 5 MB).
  - Escaneos puntuales donde la simplicidad supera al rendimiento.

---

## Conclusión

Ahora tienes una comprensión sólida de **cómo hacer OCR a TIFF** usando las capacidades de transmisión de Aspose OCR, y sabes cómo **extraer fragmentos de texto** de manera eficiente. La solución completa—inicializar el motor, habilitar la transmisión, añadir cada mosaico y, finalmente, reconocer el lienzo virtual—cubre el “qué”, “por qué” y “cómo” que necesitas para un código listo para producción.

¿Próximos pasos? Prueba cambiar `"en"` por otro idioma, o experimenta con diferentes formatos de imagen (`.png`, `.jpg`). También podrías alimentar el resultado OCR directamente a un índice de búsqueda o a un generador de PDF. El patrón sigue siendo el mismo: transmitir, unir, reconocer.

¿Tienes preguntas sobre escalar a cientos de mosaicos, o necesitas ayuda con el manejo de errores? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}