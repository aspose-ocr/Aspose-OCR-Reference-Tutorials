---
category: general
date: 2026-04-29
description: Cómo enderezar una imagen y mejorar la precisión del OCR con Aspose OCR
  – aprende a eliminar el ruido, aumentar el contraste de la imagen y extraer texto
  de las imágenes.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: es
og_description: Cómo enderezar una imagen y mejorar la precisión del OCR. Este tutorial
  muestra cómo eliminar el ruido de la imagen, aumentar el contraste y extraer texto
  de la imagen usando Aspose OCR.
og_title: cómo enderezar una imagen – Guía completa de Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Cómo enderezar la imagen – Guía de preprocesamiento OCR de Aspose
url: /es/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo enderezar una imagen – Guía completa de Aspose OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** antes de enviarla a un motor OCR? No eres el único. Un escaneo torcido o una foto tomada en ángulo puede afectar el reconocimiento de texto, dejándote con una salida confusa.  

En este tutorial recorreremos una solución completa, de extremo a extremo, que no solo **cómo enderezar una imagen**, sino también **eliminar ruido de la imagen**, **mejorar el contraste de la imagen**, y, en última instancia, **extraer texto de la imagen** con Aspose OCR. Al final verás cómo **mejorar la precisión del OCR** sin tener que buscar en la documentación.

> **Lo que obtendrás:** una aplicación de consola C# lista para ejecutar, una explicación clara de cada paso de preprocesamiento y un puñado de consejos prácticos que puedes copiar y pegar en tus propios proyectos.

## Requisitos previos

- .NET 6.0 o posterior (el código funciona también con .NET Core y .NET Framework)  
- Paquete NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Una imagen de muestra que esté sesgada, ruidosa o de bajo contraste (p. ej., `skewed_noisy.jpg`)  
- Visual Studio, VS Code, o cualquier editor C# que prefieras  

No se requieren bibliotecas nativas adicionales – Aspose maneja todo en el proceso.

---

## Cómo enderezar una imagen con Aspose OCR

Lo primero que necesitamos es un filtro de enderezado que corrige el ángulo de rotación. Aspose OCR incluye `FilterDeskew`, que analiza las líneas base del texto y rota el mapa de bits en consecuencia.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Por qué empezamos con el enderezado:**  
Si las líneas de texto no son horizontales, el motor OCR intentará interpretar los caracteres inclinados como glifos diferentes, reduciendo drásticamente **la precisión del OCR**. El enderezado alinea las líneas base, proporcionando al reconocedor un lienzo limpio.

> *Consejo profesional:* Si conoces el ángulo de rotación de antemano (p. ej., todas las escaneos están a 90°), puedes omitir el filtro y rotar manualmente – es una pequeña mejora de rendimiento.

---

## Eliminar ruido de la imagen – Limpiar el escaneo

El ruido aparece como manchas negras o blancas aleatorias (el clásico patrón “sal‑y‑pimienta”) y puede confundir la segmentación de caracteres. `FilterDenoise` aplica un filtro mediano que suaviza estas manchas mientras preserva los bordes.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Cuándo ajustar la intensidad:**  
- **Strength = 1** – Grano ligero, procesamiento rápido.  
- **Strength = 3** – Escaneos muy ruidosos (p. ej., documentos fax).  

Aumentar demasiado la intensidad puede difuminar trazos finos, lo que podría *dañar* **la precisión del OCR**. Prueba un par de valores en una muestra representativa.

---

## Mejorar el contraste de la imagen – Resaltar caracteres tenues

Las imágenes de bajo contraste (p. ej., recibos descoloridos) a menudo hacen que el motor OCR no detecte glifos ligeros. `FilterContrastBoost` estira el histograma de modo que los píxeles oscuros se vuelvan más oscuros y los claros más claros.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Por qué el contraste es importante:**  
Un mayor contraste mejora la relación señal‑ruido, facilitando que el reconocedor neuronal de Aspose distinga “I” de “l”. Sin embargo, un exceso de aumento puede saturar la imagen, convirtiendo gradientes suaves en bordes duros que parecen artefactos. Busca un equilibrio; 1.5‑2.0 es un buen punto de partida.

---

## Extraer texto de la imagen – El paso final del OCR

Ahora que la imagen está recta, limpia y vívida, el motor OCR puede hacer su trabajo. El método `Recognize` devuelve un objeto `OcrResult` que contiene el texto sin procesar, puntuaciones de confianza e incluso cajas delimitadoras si las necesitas.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Salida de ejemplo** (suponiendo que la imagen fuente contiene “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Si ves caracteres faltantes, verifica nuevamente la cadena de preprocesamiento – quizás la imagen aún necesite un denoise más fuerte o un nivel de contraste diferente.  

> *Pregunta frecuente:* “¿Qué pasa si necesito reconocer un idioma diferente al inglés?”  
> Simplemente establece `ocrEngine.Language = Language.English;` a otro idioma soportado (p. ej., `Language.French`). Los pasos de preprocesamiento permanecen iguales.

---

## Mejorar la precisión del OCR – Ajustes extra

Incluso con una cadena perfecta, algunos ajustes adicionales pueden impulsar **la precisión del OCR** aún más:

| Consejo | Cuándo usar | Cómo |
|-----|--------------|-----|
| **Umbral binario** | Escaneos muy oscuros o muy claros | `processingPipeline.Add(new FilterBinarize());` |
| **Redimensionar imagen** | Fuentes pequeñas (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Especificar conjunto de caracteres** | Alfabeto conocido (solo dígitos, etc.) | `ocrEngine.Characters = "0123456789";` |
| **PDFs multipágina** | Procesamiento por lotes | Loop over each page and reuse the same pipeline. |

Recuerda: cada filtro adicional añade tiempo de procesamiento, así que habilita solo lo que realmente necesites.

---

## Ejemplo completo funcional (listo para copiar‑pegar)

A continuación está el programa completo, listo para compilar. Reemplaza `YOUR_DIRECTORY` con la carpeta que contiene `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Resultado esperado:** Texto limpio y enderezado impreso en la consola, con muchas menos errores de reconocimiento que al alimentar el archivo crudo directamente a `ocrEngine.Recognize`.

---

## Conclusión

Hemos cubierto **cómo enderezar una imagen**, cómo **eliminar ruido de la imagen**, cómo **mejorar el contraste de la imagen**, y finalmente cómo **extraer texto de la imagen** usando Aspose OCR. Al encadenar estos filtros verás un salto notable en **la precisión del OCR**, especialmente en escaneos de baja calidad.

¿Listo para el próximo desafío? Intenta alimentar un PDF multipágina en la misma cadena, o experimenta con umbrales personalizados para la binarización. Los mismos principios se aplican – endereza, limpia, ilumina y luego reconoce.

¿Tienes preguntas o un caso raro? Deja un comentario y solucionemos juntos. ¡Feliz codificación!  

![ejemplo de cómo enderezar una imagen](deskew-example.png "ejemplo de cómo enderezar una imagen")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}