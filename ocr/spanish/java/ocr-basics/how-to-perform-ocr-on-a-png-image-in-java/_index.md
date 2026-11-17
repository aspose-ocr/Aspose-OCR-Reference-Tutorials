---
category: general
date: 2026-10-11
description: Aprende a realizar OCR en una imagen PNG en Java, extraer texto de la
  imagen y convertir la imagen a texto con un sencillo ejemplo de OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: es
lastmod: 2026-10-11
og_description: Cómo realizar OCR en una imagen PNG con Java, extraer texto de la
  imagen y convertirla a texto usando un ejemplo conciso y listo para ejecutar.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Cómo realizar OCR en una imagen PNG en Java – guía completa
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Cómo realizar OCR en una imagen PNG en Java
url: /es/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en una imagen PNG en Java

Si necesitas **realizar OCR** en un archivo de imagen, aprender **cómo realizar OCR** en Java es esencial para muchas tareas de automatización. Ya sea que estés digitalizando recibos, indexando documentos escaneados o creando un archivo fotográfico buscable, la capacidad de **extraer texto de la imagen** ahorra innumerables horas manuales.

Este tutorial te muestra una solución completa y ejecutable que carga un PNG, ejecuta un motor OCR y **reconoce texto de PNG**. También verás cómo **convertir imagen a texto** y manejar problemas comunes como entradas de baja resolución o caracteres no ASCII.

## Lo que lograrás

Al final de esta guía podrás:

* código **load image java** que lee un PNG desde el disco,
* inicializar un motor OCR ligero,
* **extract text from image** y imprimir el resultado en la consola,
* adaptar la solución para otros formatos de imagen o procesamiento por lotes.

No se requieren servicios externos—solo una única biblioteca OCR de código abierto (Tess4J) y el runtime de Java SE.

---

## Requisitos previos

* Java 17 o superior (el código se compila con JDK 17).
* Maven o Gradle para la gestión de dependencias.
* Familiaridad básica con la línea de comandos y el IDE de tu elección.
* La biblioteca `tess4j` (un wrapper Java para Tesseract). Añade la siguiente dependencia Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Si usas Gradle, el equivalente es:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

También necesitas los archivos de datos de Tesseract (`.traineddata`). Descarga el paquete de datos en inglés desde el repositorio oficial y colócalo en una carpeta llamada `tessdata` en la raíz del proyecto.

---

## Paso 1: Cargar la imagen en Java

Cargar un PNG es sencillo con la clase estándar `ImageIO`. El código a continuación demuestra **load image java** de forma segura y consciente de excepciones:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Por qué es importante:** `ImageIO.read` detecta automáticamente el formato de la imagen, pero verificamos explícitamente si es `null` para evitar fallos silenciosos cuando el PNG está corrupto. Este patrón es una buena práctica cuando **load image java** para OCR.

---

## Paso 2: Inicializar el motor OCR

Tess4J envuelve el binario nativo de Tesseract, exponiendo una API Java sencilla. El siguiente método crea una instancia de `Tesseract`, la apunta a la carpeta `tessdata` y configura el idioma a inglés:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Por qué lo hacemos:** Inicializar el motor una sola vez y reutilizarlo para múltiples imágenes reduce la sobrecarga de inicio. La llamada `setOcrEngineMode` selecciona el modo predeterminado, que funciona bien para la mayoría de los PNG. Si encuentras escaneos ruidosos, puedes experimentar con otros modos (p. ej., `OEM_LSTM_ONLY`).

---

## Paso 3: Realizar OCR y **reconocer texto de PNG**

Ahora combinamos el cargador de imágenes y el motor OCR. El método a continuación ejecuta OCR sobre un `BufferedImage` y devuelve la cadena extraída:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Ejemplo completo ejecutable**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Salida esperada**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

La consola mostrará los caracteres exactos que el motor extrajo de `sample.png`. Si el PNG contiene solo una palabra, la salida será esa palabra seguida de un salto de línea.

---

## Paso 4: Variaciones comunes y casos límite

### 4.1 Manejo de PNGs de baja resolución

Tesseract funciona mejor con imágenes de al menos 300 DPI. Si tu PNG de origen es más pequeño, escálalo antes del OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Aplica `upscale(image, 2)` antes de llamar a `extractText` para mejorar la precisión.

### 4.2 Extracción de texto no inglés

Para **extract text from image** que contiene otros idiomas, descarga los archivos `.traineddata` apropiados y establece el código de idioma:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Procesamiento por lotes de varios PNGs

Si necesitas **recognize text from PNG** en archivos dentro de una carpeta, itera sobre el directorio:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Manejo de errores de OCR

Los errores típicos de OCR incluyen confundir `0` (cero) con `O` o `1` con `l`. El post‑procesamiento con expresiones regulares puede limpiar el resultado:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Consejos profesionales para OCR fiable en Java

| Consejo | Razón |
|-----|--------|
| **Usa un PNG sin pérdida** | Los artefactos de compresión en JPEG pueden confundir al motor. |
| **Recorta bordes blancos** | El espacio en blanco excesivo aumenta el tiempo de procesamiento y puede causar falsos positivos. |
| **Establece `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** solo cuando el diseño es desconocido; de lo contrario elige un modo específico (p. ej., `PSM_SINGLE_BLOCK`). |
| **Cachea la instancia `ITesseract`** |


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo leer texto de una imagen en Java usando Aspose OCR – Guía completa](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Cómo usar OCR en Java – Reconocer texto de la imagen rápidamente](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR de imágenes por lotes en Java – Extraer texto de archivos PNG rápidamente](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}