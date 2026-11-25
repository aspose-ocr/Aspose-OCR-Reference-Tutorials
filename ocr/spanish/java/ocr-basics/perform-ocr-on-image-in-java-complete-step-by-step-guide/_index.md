---
category: general
date: 2026-06-16
description: Aprende cómo realizar OCR en archivos de imagen en Java. Este tutorial
  cubre el reconocimiento de texto a partir de PNG, la extracción de texto de la imagen,
  la conversión de imagen a texto y la carga de la imagen para OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: es
og_description: Realiza OCR en una imagen usando Java. Esta guía muestra cómo reconocer
  texto de un PNG, extraer texto de una imagen y convertir una imagen a texto con
  un ejemplo listo para ejecutar.
og_title: Realiza OCR en una imagen con Java – Tutorial completo de programación
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Realizar OCR en una imagen en Java – Guía completa paso a paso
url: /es/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en Imagen con Java – Guía Completa Paso a Paso

¿Alguna vez necesitaste **perform OCR on image** en archivos pero no estabas seguro de qué biblioteca Java elegir? No estás solo. Ya sea que estés construyendo un escáner de recibos, un archivador de documentos o simplemente tengas curiosidad por convertir fotos en texto buscable, aprender a **perform OCR on image** con Java es una habilidad muy útil.

En este tutorial recorreremos todo lo que necesitas para **perform OCR on image** en archivos: cargar la imagen, configurar el motor, reconocer el texto y, finalmente, imprimir el resultado. Al final podrás **recognize text from PNG**, **extract text from image** y **convert image to text** con solo unas pocas líneas de código.

## Requisitos previos

- Java 17 o superior (el código compila con cualquier JDK reciente)
- Maven instalado (o tu herramienta de compilación favorita)
- Familiaridad básica con la sintaxis de Java
- Un archivo PNG que quieras probar (lo llamaremos `hello.png`)

> **Consejo profesional:** Si no tienes un PNG a mano, crea uno tomando una captura de pantalla de cualquier texto y guárdalo como `hello.png` en una carpeta llamada `resources`.

## Qué construiremos

Una pequeña aplicación de consola llamada `OcrDemo` que:

1. **Loads image for OCR** – lee un PNG del disco.
2. **Performs OCR on image** – usa el motor Tesseract a través de Tess4J.
3. **Extracts text from image** – devuelve un `String` con el contenido reconocido.
4. Imprime el resultado en la consola.

Vamos a sumergirnos.

## Paso 1: Configurar el proyecto y añadir Tess4J

Primero, crea un nuevo proyecto Maven (o Gradle si lo prefieres). Añade la dependencia Tess4J, que envuelve el popular motor Tesseract OCR.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **¿Por qué Tess4J?** Está activamente mantenido, funciona en todas las plataformas y te brinda una API Java limpia para tareas de **perform OCR on image**.

## Paso 2: Preparar la lógica de carga de imágenes

Ahora escribiremos un método auxiliar que **load image for OCR**. El método usa `ImageIO` de Java para leer un PNG en un `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Observa que el nombre del método refleja claramente la intención de **load image for OCR**, lo que hace que el código sea auto‑documentado.

## Paso 3: Configurar el motor OCR para **Perform OCR on Image**

Con la imagen en mano, creamos una instancia de `Tesseract`, habilitamos la detección automática de idioma y llamamos a `doOCR`. Este es el núcleo de cómo **perform OCR on image** los datos.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **¿Por qué habilitar la detección automática?** Permite que el motor elija el mejor modelo de idioma para la imagen, lo cual es especialmente útil cuando **convert image to text** a partir de fuentes que combinan inglés y otros scripts.

## Paso 4: Juntar todo – La aplicación principal

Aquí está el punto de entrada que **recognize text from PNG**, **extract text from image**, y finalmente imprime el resultado. Este es el ejemplo completo y ejecutable.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Salida esperada

Si `hello.png` contiene la frase “Hello, OCR world!”, la consola mostrará algo como:

```
=== Recognized Text ===
Hello, OCR world!
```

La salida exacta puede variar ligeramente según la calidad de la imagen, pero deberías ver el texto que colocaste en el PNG.

## Paso 5: Manejo de casos comunes

### 5.1 Tratar imágenes de baja resolución

Si el PNG de origen está borroso, la precisión del OCR disminuye. Una solución rápida es escalar la imagen antes de enviarla al motor:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Llama a `upscale(image, 2)` antes de `engine.recognize(image)` para mejorar los resultados.

### 5.2 Documentos multilingües

Si esperas texto en francés o alemán, simplemente añade los códigos de idioma a `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

El motor intentará entonces **extract text from image** usando los modelos de idioma combinados.

### 5.3 Omitir páginas vacías

A veces una página escaneada de PDF se renderiza como un PNG en blanco. Detectar una imagen vacía ahorra tiempo de procesamiento:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Paso 6: Empaquetar y ejecutar la aplicación

1. **Compilar:** `mvn clean compile`
2. **Ejecutar:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Asegúrate de que la carpeta `tessdata` (que contiene los archivos de idioma) esté junto al JAR compilado o especifica su ruta absoluta en `OcrEngine`.

## Conclusión

Ahora tienes un patrón sólido y listo para producción para **perform OCR on image** usando Java. Desde **loading image for OCR** hasta **recognize text from PNG**, cubrimos cómo **extract text from image**, **convert image to text**, y cómo manejar escenarios complicados como escaneos de baja resolución o contenido multilingüe.

A continuación, podrías explorar:

- **Procesamiento por lotes** – recorrer un directorio de PNGs y escribir cada resultado en un archivo `.txt`.
- **Generación de PDF** – incrustar el texto extraído de nuevo en PDFs buscables.
- **Servicios OCR en la nube** – comparar el rendimiento local de Tesseract con APIs como Google Vision o Azure Cognitive Services.

Siéntete libre de experimentar, ajustar los parámetros y compartir tus hallazgos. ¡Feliz codificación, y que tus imágenes siempre se conviertan en texto limpio y buscable!

![Diagrama que muestra el flujo de trabajo OCR para perform OCR on image](https://example.com/ocr-workflow.png "ejemplo de perform OCR on image")

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}