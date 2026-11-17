---
category: general
date: 2026-11-17
description: Aprende cómo realizar OCR en una imagen con Java y extraer texto de fotos
  usando un ejemplo de código sencillo. Incluye consejos para leer imágenes en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: es
lastmod: 2026-11-17
og_description: Cómo realizar OCR en una imagen con Java y extraer texto rápidamente.
  Sigue esta guía para leer imágenes en Java y convertirlas a texto con un ejemplo
  listo para ejecutar.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Cómo realizar OCR en una imagen en Java – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Cómo realizar OCR en una imagen en Java – guía paso a paso
url: /es/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en una imagen con Java – guía paso a paso

Si necesitas **cómo realizar OCR** en una foto, este tutorial te muestra una solución completa y ejecutable en Java. Verás cómo leer un archivo de imagen, configurar un motor OCR y extraer el texto que el motor reconoce.

Trabajar con documentos escaneados, recibos o capturas de pantalla a menudo requiere convertir el contenido visual en texto buscable. Esta guía te acompaña en cada paso, desde cargar la imagen hasta imprimir el texto extraído, y también cubre problemas comunes como formatos de archivo no compatibles y resultados nulos.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java Development Kit (JDK) 8 o superior instalado.
* Una herramienta de compilación (Maven o Gradle) para obtener la biblioteca OCR.
* Un archivo de imagen (JPEG, PNG, BMP) que quieras procesar.

El código usa la **biblioteca OCR del paquete `com.asprise.ocr`** porque solo requiere un JAR y funciona en todas las plataformas principales. Reemplázala por otro proveedor (Tesseract, Google Vision, etc.) cambiando las sentencias de importación y el código de inicialización del motor.

## Paso 1: Añadir la dependencia OCR

Si usas Maven, agrega la siguiente dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Para Gradle, coloca esta línea en `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Estas líneas garantizan que el código **read image Java** pueda compilar y que el motor OCR esté disponible en tiempo de ejecución.

## Paso 2: Leer la imagen con Java

Leer un archivo de imagen es el primer paso concreto en cualquier flujo de **extract text image**. La clase incorporada `ImageIO` de Java maneja la mayoría de los formatos comunes.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Por qué es importante:** `ImageIO.read` devuelve `null` para formatos no compatibles o archivos corruptos. El método anterior registra el problema y devuelve `null` para que el siguiente paso pueda reaccionar de forma adecuada.

## Paso 3: Crear y configurar el motor OCR

El motor OCR debe saber qué idioma reconocer. Configurar el idioma mejora la precisión de forma drástica, especialmente para documentos que no están en inglés.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Por qué es importante:** Iniciar el motor es una operación relativamente pesada, por lo que deberías crearla una sola vez y reutilizarla para múltiples imágenes si tu aplicación procesa lotes.

## Paso 4: Realizar OCR y convertir la imagen a texto

Ahora que la imagen está cargada y el motor listo, puedes ejecutar el paso de reconocimiento. Este es el núcleo de **cómo realizar OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Manejo de casos límite:** Si la imagen es `null`, el método devuelve una cadena vacía en lugar de lanzar una `NullPointerException`. Esto hace que el código circundante sea más robusto al tratar con archivos suministrados por el usuario.

## Paso 5: Mostrar el texto extraído

Finalmente, imprime el resultado en la consola o envíalo a otro componente (p. ej., una base de datos o un widget de UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Cuando ejecutes el programa con `java OcrDemo sample.jpg`, la consola mostrará los caracteres reconocidos. Esto completa el ciclo **convert image to text**.

### Salida esperada

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Si la imagen no contiene caracteres legibles, el programa imprime `(no text detected)`.

## Variaciones comunes y cómo adaptarlas

| Variación | Qué cambia | Cuándo usar |
|-----------|------------|-------------|
| **Idioma diferente** | Reemplaza `"eng"` por `"spa"` para español, `"fra"` para francés, etc. | Documentos escritos en un idioma distinto al inglés |
| **Procesamiento por lotes** | Recorre una lista de rutas de archivo, reutiliza la misma instancia `Ocr`. | Grandes conjuntos de páginas escaneadas |
| **Mayor precisión** | Usa `Ocr.SPEED_SLOW` o habilita `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` para escaneos solo numéricos. | Cuando la calidad del OCR es crítica (p. ej., números de factura) |
| **Alternativa Tesseract** | Cambia la importación a `net.sourceforge.tess4j.Tesseract` y ajusta el código de inicialización. | Proyectos que ya dependen de Tesseract |

## Consejos profesionales

* **Redimensiona imágenes grandes** antes de enviarlas al motor; la velocidad del OCR escala con la cantidad de píxeles.
* **Pre‑procesa** la imagen (escala de grises, aumento de contraste) usando bibliotecas como OpenCV si la fuente es ruidosa.
* **Cachea el motor OCR** si lo llamas muchas veces en un corto período—iniciar y detener el motor genera sobrecarga.
* **Valida el resultado** con expresiones regulares cuando esperes un formato específico (p. ej., fechas, números de teléfono).

## Conclusión

Ahora sabes **cómo realizar OCR** en una imagen con Java, desde leer el archivo hasta mostrar el texto extraído. El tutorial cubrió técnicas de **read image Java**, **extract text image**, **convert image to text** y **image to text java**, y proporcionó consejos prácticos para escenarios del mundo real.  

A partir de aquí puedes:

* Integrar el paso OCR en un servicio web que reciba cargas.
* Combinar la salida con un índice de búsqueda para búsqueda de texto completo sobre documentos escaneados.
* Explorar opciones avanzadas de OCR como soporte multilingüe o conjuntos de caracteres personalizados.

¡Feliz codificación y disfruta convirtiendo imágenes en texto buscable!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar OCR en Java – Extraer texto de una imagen con corrección ortográfica](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convertir imagen a texto en Java usando Aspose OCR – Guía completa](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Cómo habilitar GPU para OCR en Java – Extraer texto de una imagen](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}