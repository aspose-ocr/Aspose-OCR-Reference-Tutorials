---
category: general
date: 2026-07-05
description: Comprime imágenes PDF mientras conviertes PNG a PDF usando Java. Aprende
  el preprocesamiento de imágenes para OCR, reconoce texto JPG y realiza OCR por lotes
  a PDF en un solo tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: es
og_description: Comprime imágenes PDF y convierte PNG a PDF usando Java. Esta guía
  cubre el preprocesamiento de imágenes para OCR, el reconocimiento de texto en JPG
  y el OCR por lotes a PDF.
og_title: Comprimir imágenes PDF con Java – Tutorial completo de OCR por lotes
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Comprimir imágenes PDF con Java – Guía completa de OCR por lotes a PDF
url: /es/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comprimir imágenes PDF con Java – Guía completa de OCR por lotes a PDF

¿Alguna vez necesitaste **comprimir imágenes PDF** mientras convertías una carpeta de PNGs en PDFs buscables? No eres el único. En muchos flujos de automatización el mayor dolor es equilibrar la calidad de la imagen, la precisión del OCR y el tamaño final del PDF, todo al mismo tiempo.  

En este tutorial recorreremos una solución práctica que **convierte PNG a PDF**, aplica **preprocesamiento de imágenes para OCR**, y finalmente **comprime imágenes PDF** para que la salida siga siendo ligera. Al final sabrás cómo **reconocer texto JPG**, configurar un flujo de trabajo **OCR por lotes a PDF**, y mantener tus PDFs ordenados.

## Lo que aprenderás

- Configurar Aspose OCR para Java y aplicar una licencia.
- Configurar el motor para multihilo, aceleración GPU y corrección ortográfica.
- Construir una canalización reutilizable de **preprocesamiento de imágenes para OCR** (eliminar ruido, contraste, binarizar).
- Usar **PdfSaveOptions** para **comprimir imágenes PDF** sin sacrificar la legibilidad.
- Recorrer un directorio para **convertir PNG a PDF** y **reconocer texto JPG** en bloque.
- Un programa Java completo, listo‑para‑ejecutar, que puedes incorporar a cualquier proyecto.

> **Requisitos previos**: Java 8+, Maven o Gradle, una licencia de Aspose OCR para Java y una carpeta de imágenes PNG/JPG que deseas procesar.

---

## Paso 1: Aplicar la licencia de Aspose OCR (Esencial para producción)

Antes de poder llamar a cualquier API de OCR debes cargar una licencia válida; de lo contrario estarás limitado a las restricciones de la versión de prueba.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Por qué es importante*: Un motor con licencia habilita el soporte GPU, mayor precisión y elimina marcas de agua que de otro modo inflarían tus archivos PDF.

---

## Paso 2: Configurar el motor OCR – Hilos, GPU y corrección ortográfica

Un motor OCR rápido es la columna vertebral de cualquier trabajo **OCR por lotes a PDF**. Crearemos tantos hilos como la CPU del host pueda manejar, habilitaremos la aceleración GPU (si tienes una tarjeta compatible) y ajustaremos la corrección ortográfica para limpiar los errores del OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Consejo profesional*: Si ejecutas en un servidor sin pantalla y sin GPU, simplemente establece `gpu.setEnabled(false)` – el código seguirá funcionando, solo será un poco más lento.

---

## Paso 3: Construir una canalización de preprocesamiento de imágenes

Los escaneos crudos a menudo sufren de ruido, bajo contraste o iluminación desigual. **El preprocesamiento de imágenes para OCR** mejora drásticamente las tasas de reconocimiento, especialmente en escenarios de **reconocer texto JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Por qué encadenamos estos pasos*: El denoise primero evita que el binarizador amplifique los puntos; el contraste luego asegura que los caracteres sobresalgan; finalmente, la binarización le brinda al motor OCR una imagen binaria limpia con la que trabajar.

---

## Paso 4: Preparar opciones de guardado PDF – **Comprimir imágenes PDF** eficientemente

Aspose permite afinar la salida PDF. Activaremos la compresión de imágenes y estableceremos un nivel de calidad que equilibre tamaño y legibilidad.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Resultado*: Cada PDF buscable será notablemente más pequeño—ideal para archivado o envío por correo electrónico.

---

## Paso 5: Procesar la carpeta – **Convertir PNG a PDF** y **reconocer texto JPG** en un solo bucle

Ahora juntamos todo. El bucle recorre un directorio de entrada, ejecuta OCR en cada PNG o JPG, y escribe un PDF buscable en una carpeta de salida. El nombre del PDF refleja el nombre de la imagen origen.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Salida esperada

Ejecutar el programa imprime una línea por cada imagen, por ejemplo:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Abre cualquier PDF resultante en un visor y verás texto seleccionable y buscable mientras que el tamaño del archivo suele ser **un 30‑50 % menor** que su contraparte sin compresión.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si mi servidor no tiene GPU?
Simplemente establece `gpuSettings.setEnabled(false)`. El resto de la canalización permanece igual y aún obtienes procesamiento multihilo en CPU.

### Mis PDFs siguen siendo demasiado grandes—¿puedo bajar más la calidad?
Sí. Ajusta `options.setImageQuality(70)` o incluso `50`. Valores más bajos reducen el tamaño de forma más agresiva pero pueden difuminar glifos finos. Prueba con una muestra representativa.

### ¿Cómo manejo otros formatos de imagen (TIFF, BMP)?
Añade las extensiones al filtro lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

La misma canalización de preprocesamiento funciona para la mayoría de los formatos raster.

### ¿Puedo mantener las imágenes originales en color en lugar de binarizarlas?
Reemplaza `.addBinarize()` por `.addGrayscale()` en el constructor del preprocesador si necesitas conservar el color para análisis posteriores.

---

## Consejos profesionales para OCR por lotes listo para producción

- **Gestión de memoria**: Reutiliza una única instancia de `OcrEngine` (como se muestra) para evitar la sobrecarga de crear/destruir objetos por imagen.
- **Manejo de errores**: Envuelve el bloque por archivo en un `try/catch` para registrar fallos sin abortar todo el lote.
- **Registro (logging)**: Usa un framework de logging adecuado (SLF4J, Log4j) en lugar de `System.out.println` para soluciones escalables.
- **Paralelismo**: Para carpetas masivas, considera procesar sub‑directorios con streams paralelos, pero vigila la contención de la GPU.
- **Seguridad**: Almacena el archivo de licencia fuera del repositorio y protégelo con permisos del sistema de archivos.

---

## Conclusión

Acabamos de demostrar cómo **comprimir imágenes PDF** mientras realizamos una conversión **OCR por lotes a PDF** que **convierte PNG a PDF**, **reconoce texto JPG**, y aplica una robusta **canalización de preprocesamiento de imágenes para OCR**. El programa Java completo es autónomo, se ejecuta en cualquier JDK moderno y produce PDFs buscables y ligeros listos para archivado o análisis posterior.

¿Próximos pasos? Experimenta con diferentes parámetros de preprocesamiento, prueba idiomas de OCR distintos al inglés, o integra el flujo de trabajo en un microservicio Spring Boot que vigile una carpeta y procese archivos al vuelo. Los conceptos clave—carga de licencia, configuración del motor, preprocesamiento y compresión PDF—permanecen iguales, dándote una base sólida para cualquier proyecto impulsado por OCR.

¿Tienes preguntas o quieres compartir tus propios ajustes? Deja un comentario abajo, ¡y feliz codificación!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagrama del flujo de trabajo OCR por lotes que muestra imágenes de entrada, preprocesamiento, motor OCR y salida PDF comprimida")

## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Reconocer texto PDF – Operaciones OCR con Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [reconocer texto en imagen con Aspose OCR – Tutorial completo de OCR en Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convertir imagen a texto en Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}