---
category: general
date: 2026-10-11
description: Aprende cómo realizar OCR en imágenes en C# con Aspose.OCR, incluyendo
  la instalación de System.Drawing.Common y la extracción de texto de archivos JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: es
lastmod: 2026-10-11
og_description: Realiza OCR en una imagen en C# usando Aspose.OCR. Esta guía te muestra
  cómo instalar System.Drawing.Common, cargar una imagen para OCR y extraer texto
  de un JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Realizar OCR en una imagen con C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Cómo realizar OCR en una imagen en C# usando Aspose.OCR
url: /es/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en una imagen en C# usando Aspose.OCR

Si necesitas **perform OCR on image** archivos en una aplicación .NET, esta guía te muestra una solución completa. Usando Aspose.OCR puedes rápidamente **recognize text from picture** archivos como JPGs y mostrar el resultado en una ventana de consola.

Aprenderás a:

* **install System.Drawing.Common package** – la biblioteca que proporciona la clase `Image`,
* **load image for OCR** – leer un JPEG o PNG en memoria,
* configurar el modelo de idioma,
* **perform OCR on image** y, finalmente,
* **extract text from JPG** y mostrarlo.

Los pasos están escritos para .NET 6+, pero también funcionan con .NET Framework 4.6.1 o posterior.

---

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Proporciona el runtime para la aplicación de consola C#. |
| Visual Studio 2022 (or any IDE) | Facilita agregar paquetes NuGet y ejecutar el programa. |
| Internet connection (first run only) | Aspose.OCR descarga el módulo de idioma automáticamente. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Se usa para demostrar **extract text from JPG**. |

---

## Paso 1: Instalar el paquete System.Drawing.Common

El paquete NuGet `System.Drawing.Common` suministra la clase `Image` que usarás para **load image for OCR**. Abre la consola del Administrador de paquetes y ejecuta:

```powershell
Install-Package System.Drawing.Common
```

> **Consejo profesional:** Apunta a `net6.0-windows` o agrega `<UseWindowsForms>true</UseWindowsForms>` al archivo del proyecto si encuentras advertencias específicas de plataforma en Linux/macOS.

---

## Paso 2: Agregar el paquete NuGet Aspose.OCR

Aspose.OCR contiene el motor OCR y los modelos de idioma. Instálalo con:

```powershell
Install-Package Aspose.OCR
```

El paquete es liviano; los datos de idioma requeridos (p. ej., Cirílico) se descargan la primera vez que configuras `OcrEngine.Language`.

---

## Paso 3: Cómo cargar la imagen para OCR

Cargar la imagen es el primer paso concreto antes de que puedas **perform OCR on image**. El método `Image.FromFile` lee cualquier formato compatible con GDI+, incluyendo JPG, PNG, BMP y TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Si el archivo no existe, se lanza `FileNotFoundException`; envuelve la llamada en un bloque try/catch para código de producción.*

---

## Paso 4: Configurar el motor y **perform OCR on image**

Crea una instancia de `OcrEngine`, selecciona el modelo de idioma, asigna la imagen cargada y llama a `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

El método `Recognize()` devuelve un objeto `OcrResult` que contiene el texto extraído, puntuaciones de confianza y cajas delimitadoras. El módulo de idioma se descarga automáticamente en el primer uso, por lo que no se requieren archivos adicionales.

---

## Paso 5: **Extract text from JPG** y mostrarlo

Ahora puedes **recognize text from picture** y mostrar el resultado. La propiedad `Text` de `OcrResult` contiene la cadena simple.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Salida esperada de la consola

```
Recognized text:
Пример текста на кириллице
```

Si la imagen de origen contiene texto en inglés, la salida será la frase en inglés que colocaste en la imagen.

---

## Casos límite y consejos de mejores prácticas

| Situación | Recomendación |
|-----------|----------------|
| **Large images ( > 5 MB )** | Redimensiona la imagen a ≤ 2000 px en el lado más largo antes de OCR para reducir el uso de memoria y mejorar la velocidad. |
| **Multiple languages in one picture** | Llama a `ocrEngine.AddLanguage(OcrLanguage.English)` además de Cirílico, luego establece `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Aumenta el contraste con `System.Drawing.Graphics` antes de pasar el bitmap al motor. |
| **Running on Linux/macOS** | Asegúrate de que la dependencia nativa `libgdiplus` esté instalada (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Reutiliza la misma instancia de `OcrEngine` y solo reemplaza `ocrEngine.Image` para evitar cargar repetidamente el módulo. |

---

## Programa completo y ejecutable

A continuación se muestra la aplicación de consola completa que incorpora todos los pasos anteriores. Copia el código en un nuevo proyecto de consola C#, reemplaza la ruta de la imagen y ejecútalo.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ejecutar el programa** imprime la cadena reconocida en la consola, confirmando que has **performed OCR on image** y **extracted text from JPG** con éxito.

---

## Conclusión

Ahora sabes cómo **perform OCR on image** archivos en C# usando Aspose.OCR, desde instalar el necesario **System.Drawing.Common package** hasta **loading image for OCR**, seleccionar el idioma apropiado y finalmente **extracting text from JPG**. Este ejemplo de extremo a extremo te brinda una base sólida para crear pipelines de procesamiento de documentos más avanzados, como procesamiento por lotes de carpetas de imágenes o integrar OCR en una API web.

### ¿Qué sigue?

* Explora **recognize text from picture** en PDFs convirtiendo cada página a una imagen primero.
* Experimenta con las propiedades `Resolution`, `Threshold` y `MaxProcessingTime` de `OcrEngine` para afinar la precisión en escaneos ruidosos.
* Combina la salida OCR con una biblioteca de procesamiento de lenguaje natural para categorizar automáticamente el contenido extraído.

Siéntete libre de adaptar el código a otros formatos de imagen, agregar manejo de errores o integrarlo en aplicaciones más grandes. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}