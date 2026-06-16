---
category: general
date: 2026-06-16
description: El tutorial de cuadro delimitador OCR en Java muestra cómo extraer texto
  de una imagen, leer texto de una imagen y obtener la puntuación de confianza OCR
  para archivos JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: es
og_description: El cuadro delimitador OCR en Java le permite reconocer texto de archivos
  JPG, extraer texto de la imagen y ver las puntuaciones de confianza del OCR, todo
  en un sencillo ejemplo de código.
og_title: Caja delimitadora OCR en Java – Extraer texto de la imagen
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Caja delimitadora OCR en Java – Extraer texto de la imagen
url: /es/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Caja delimitadora OCR en Java – Extraer texto de una imagen

¿Alguna vez te has preguntado cómo obtener la **caja delimitadora OCR** para cada fragmento de texto en una imagen Java? En este tutorial te mostraremos cómo **extraer texto de una imagen**, **leer texto de una imagen**, y también ver la **puntuación de confianza OCR** mientras **reconoces texto de archivos jpg**. ¿La respuesta corta? Unas pocas líneas de código usando una biblioteca OCR moderna, más una breve explicación de por qué cada llamada es importante.

A continuación encontrarás un ejemplo completo, listo para ejecutar, un desglose paso a paso y varios consejos prácticos que puedes copiar directamente a tu propio proyecto. Al final, podrás generar una salida similar a:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Lo que necesitarás

- **Java 11** o superior (la sintaxis a continuación usa la palabra clave `var` por brevedad, pero puedes omitirla en JDKs más antiguos).  
- Una biblioteca OCR que ofrezca una API Java – para esta guía usaremos **[Tesseract4J](https://github.com/nguyenq/tess4j)**, un contenedor ligero alrededor del popular motor Tesseract.  
- Una imagen JPEG (`.jpg`) que contenga texto impreso claro.  
- Tu IDE favorito (IntelliJ IDEA, Eclipse, VS Code…) – cualquiera sirve.

Si te falta la biblioteca, simplemente agrega esta dependencia Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Ahora vamos a sumergirnos.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## Caja delimitadora OCR: Configurando el motor

Lo primero que debes hacer es crear una instancia del motor OCR. Piensa en ello como encender el escáner que luego leerá los píxeles.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Por qué es importante:**  
Sin establecer el `datapath`, Tesseract no sabrá dónde están sus paquetes de idioma y obtendrás un críptico error “Failed loading language”. La llamada `setLanguage` es opcional si solo necesitas el paquete inglés predeterminado, pero ser explícito hace que el código sea más claro para futuros lectores.

## Cargar la imagen que deseas procesar

A continuación, pasa al motor el JPEG que deseas analizar. La biblioteca acepta un `File` o un `BufferedImage`; usaremos un `File` por simplicidad.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Consejo profesional:**  
Si tu imagen está en recursos (p. ej., dentro de un JAR), usa `getResourceAsStream` y envuélvelo con `ImageIO.read`. Así el tutorial funciona tanto localmente como en una aplicación empaquetada.

## Realizar el reconocimiento OCR

Ahora le pedimos al motor que lea la imagen. El resultado es una cadena de texto plano, pero también queremos la **puntuación de confianza OCR** y la **caja delimitadora OCR** para cada línea.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Por qué usamos `getWords` en lugar de `doOCR` simple:**  
`doOCR` te da la cadena cruda pero descarta la información espacial. Al llamar a `getWords` con `RIL_WORD` (o `RIL_TEXTLINE` si prefieres cajas a nivel de línea), obtenemos una lista de objetos `Word` que cada uno lleva el texto, la confianza y el rectángulo delimitador. Ese es el corazón de la funcionalidad **caja delimitadora OCR**.

## Entendiendo la salida

Ejecutar el fragmento anterior contra un JPEG limpio produce una salida similar a:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – los caracteres reconocidos.  
- **Confidence** – un valor de punto flotante entre 0 y 1; cuanto más alto, mayor seguridad del motor.  
- **Box** – el rectángulo que encierra la palabra en coordenadas de píxel (x, y, ancho, alto).  

Ahora puedes **leer texto de una imagen** y también saber exactamente dónde se encuentra cada fragmento en el lienzo—perfecto para resaltar, recortar o alimentar a pipelines de NLP posteriores.

## Casos límite y errores comunes

| Situación | Qué vigilar | Solución / alternativa |
|-----------|-------------|------------------------|
| La imagen está borrosa o con bajo contraste | Las puntuaciones de confianza caen drásticamente (a menudo bajo 0.6). | Pre‑procesar con OpenCV: aumentar contraste, aplicar umbralado. |
| El JPEG contiene texto rotado | Las cajas delimitadoras aparecen sesgadas o faltan. | Usa `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` para que Tesseract detecte la orientación automáticamente. |
| Imágenes grandes provocan OutOfMemoryError | El heap de Java se llena al cargar imágenes grandes. | Reduce la escala de la imagen antes del OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Necesitas cajas a nivel de línea en lugar de palabra | `RIL_WORD` devuelve cajas por palabra. | Cambia a `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Los caracteres no ingleses aparecen como � | Datos de idioma no cargados. | Descarga el archivo `.traineddata` apropiado y apunta `setDatapath` a su carpeta. |

Abordar estos problemas temprano te ahorra horas de depuración más adelante.

## Ejemplo completo (todos los pasos en un solo archivo)

A continuación tienes una clase Java autosuficiente que puedes copiar‑pegar en una carpeta `src/main/java` y ejecutar con `mvn exec:java`. Reúne todo lo que hemos comentado.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}