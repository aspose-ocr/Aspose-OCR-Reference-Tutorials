---
category: general
date: 2026-07-21
description: Extrae texto de una imagen usando Java OCR. Aprende cómo convertir PNG
  a texto, leer texto de PNG, cargar la imagen para OCR y realizar OCR en la imagen
  en solo unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: es
lastmod: 2026-07-21
og_description: Extraer texto de una imagen con Java. Esta guía muestra cómo convertir
  PNG a texto, leer texto de PNG, cargar la imagen para OCR y realizar OCR en la imagen
  de manera eficiente.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extraer texto de una imagen en Java – Tutorial de OCR paso a paso
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extraer texto de una imagen en Java – Guía completa de OCR
url: /es/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de una imagen en Java – Guía completa de OCR

¿Alguna vez necesitaste **extraer texto de una imagen** pero no estabas seguro de qué biblioteca Java elegir? No estás solo. Ya sea que estés digitalizando recibos, escaneando PDFs o creando un archivo searchable, extraer texto de un PNG es un problema diario para muchos desarrolladores.

En este tutorial recorreremos una solución práctica que te permite **convertir PNG a texto**, **leer texto de PNG**, **cargar imagen para OCR** y **realizar OCR en imagen**—todo con unas pocas líneas de código Java limpio. Al final tendrás un programa ejecutable que podrás incorporar en cualquier proyecto.

## Lo que construirás

1. Carga un archivo PNG desde el disco.  
2. Envía la imagen a un motor OCR (Tess4J, un wrapper Java para Tesseract).  
3. Imprime el texto reconocido en la consola.

Sin servicios externos, sin magia—solo Java puro y un motor OCR de código abierto.

## Requisitos previos

- **Java 17** o posterior (el código compila con versiones anteriores, pero Java 17 te brinda las últimas mejoras del lenguaje).  
- **Maven** o **Gradle** para la gestión de dependencias.  
- Un PNG de ejemplo llamado `sample.png` colocado en una carpeta que puedas referenciar (p.ej., `src/main/resources`).  
- Familiaridad básica con el método `main` de Java y el manejo de excepciones.

Si alguno de esos conceptos te resulta desconocido, no te preocupes—cada paso incluye un breve repaso.

## Paso 1: Configurar el proyecto y agregar la biblioteca OCR

Primero, crea un nuevo proyecto Maven (o Gradle si lo prefieres). Agrega la dependencia Tess4J, que incluye los binarios de Tesseract por ti.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Consejo profesional:** Si estás usando Gradle, la línea equivalente es `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Agregar esta biblioteca te brinda la clase `Tesseract`, que se encarga del trabajo pesado de **realizar OCR en imagen**.

## Paso 2: Cargar imagen para OCR

Ahora necesitamos **cargar imagen para OCR**. Tess4J funciona con `java.awt.image.BufferedImage`, así que leeremos el PNG usando `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

El método anterior aísla de forma limpia la lógica de **cargar imagen para OCR**, facilitando la prueba del resto del código. Observa el comentario—refleja el fragmento original mientras lo amplía para mayor claridad.

## Paso 3: Realizar OCR en imagen

Con la imagen en memoria, ahora podemos **realizar OCR en imagen**. La instancia `Tesseract` es nuestro motor; la configuraremos para usar los datos de idioma inglés predeterminados que vienen con Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Aquí hemos combinado los pasos originales “Step 1” y “Step 4” en un solo método, porque el objeto `Tesseract` es barato de crear y queremos que el código permanezca compacto. El comentario aún hace referencia a los pasos originales para trazabilidad.

## Paso 4: Unir todo – Método main

Finalmente, juntamos todo en `main`. Aquí **leerás texto de PNG** y verás el resultado impreso en la consola.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Cuando ejecutes `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (o el equivalente en Gradle), deberías ver algo como:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Esa salida demuestra que has **extraído texto de una imagen**, **convertido PNG a texto** y **leído texto de PNG** en un solo programa ordenado.

## Manejo de casos límite comunes

### Imágenes de baja calidad

Si el PNG está borroso o tiene bajo contraste, la precisión del OCR disminuye. Una solución rápida es pre‑procesar la imagen:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Soporte multilingüe

Tess4J puede manejar muchos idiomas. Simplemente descarga el archivo `.traineddata` apropiado y apunta `tesseract.setLanguage("spa")` para español, por ejemplo.

### PDFs grandes o imágenes multipágina

Si necesitas **extraer texto de una imagen** dentro de un PDF, divide cada página en PNGs primero (usando PDFBox) y luego alimenta cada PNG a la misma rutina OCR.

## Ejemplo completo (Todo el código en un solo lugar)

A continuación está la clase Java completa y lista para ejecutar. Copia‑pega en `src/main/java/com/example/ocrdemo/OcrDemo.java` y estarás listo para usar.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Ejecutar la clase imprime el resultado del OCR, confirmando que has **realizado OCR en imagen** y convertido tu PNG en texto editable.

## Recapitulación y próximos pasos

Comenzamos **extrayendo texto de una imagen** usando una configuración ligera de Java. Ahora sabes cómo **cargar imagen para OCR**, **realizar OCR en imagen** y **leer texto de PNG**—bloques de construcción esenciales para cualquier pipeline de digitalización de documentos.

¿Quieres ir más allá? Prueba estas ideas:

- **Procesamiento por lotes:** Recorrer un directorio de PNGs y escribir cada resultado en un archivo `.txt`.  
- **Integrar con una base de datos:** Almacenar las cadenas extraídas junto con metadatos para archivos searchable.  
- **Combinar con NLP:** Alimentar la salida del OCR a un modelo de análisis de sentimiento para obtener ideas rápidas.  

Cada una de esas extensiones se basa en los mismos conceptos centrales que cubrimos, así que estás listo para experimentar.

---

*¡Feliz codificación! Si encuentras algún problema

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen Java con Aspose.OCR modo detectar áreas](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [imagen a texto java: Convertir imagen a texto con Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Cómo hacer OCR de texto de imagen con idioma usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}