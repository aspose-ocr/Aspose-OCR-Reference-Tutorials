---
category: general
date: 2026-06-28
description: Cómo corregir la inclinación de una imagen usando Aspose.OCR. Aprende
  a preprocesar la imagen para OCR, mejorar la precisión del OCR y corregir la inclinación
  de una imagen escaneada con un ejemplo completo en C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: es
og_description: Cómo enderezar una imagen con Aspose.OCR. Este tutorial te muestra
  cómo preprocesar la imagen para OCR, mejorar la precisión y enderezar la imagen
  escaneada paso a paso.
og_title: Cómo corregir la inclinación de una imagen en C# – Guía completa de Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Cómo desinclinar una imagen en C# – Guía completa de Aspose.OCR
url: /es/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo corregir la inclinación de una imagen en C# – Guía completa de Aspose.OCR

¿Alguna vez te has preguntado **cómo corregir la inclinación de una imagen** antes de enviarla a un motor OCR? No eres el único. Los documentos escaneados a menudo llegan inclinados, y esa pequeña rotación puede arruinar los resultados del reconocimiento. ¿La buena noticia? Con Aspose.OCR puedes enderezar (deskew) y limpiar imágenes en solo unas pocas líneas de C#.

En este tutorial recorreremos un ejemplo completo y ejecutable que **preprocesa la imagen para OCR**, añade un filtro de corrección de inclinación y te muestra **cómo mejorar la precisión del OCR**. Al final podrás **corregir automáticamente la inclinación de imágenes escaneadas** y ver por ti mismo los puntajes de confianza.

> **Nota:** El código funciona con Aspose.OCR ≥ 22.10 y .NET 6+, pero los conceptos también se aplican a versiones anteriores.

## Qué necesitarás

- **Aspose.OCR para .NET** (paquete NuGet `Aspose.OCR`)
- Un **TIFF o JPEG inclinado** que quieras enderezar
- Visual Studio 2022 (o cualquier IDE de C#)
- Familiaridad básica con C# y aplicaciones de consola

No se requieren bibliotecas de terceros adicionales; todo el flujo de trabajo vive dentro de Aspose.OCR.

---

## Cómo corregir la inclinación de una imagen con Aspose.OCR

El corazón de la solución es una **cadena de filtros**. Piensa en ella como una línea de montaje donde cada filtro limpia un problema específico: primero corregimos la rotación, luego reducimos el ruido y, finalmente, aumentamos el contraste para que el motor OCR vea los caracteres con claridad.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Ejemplo de imagen**  
> ![ejemplo de cómo corregir la inclinación de una imagen](/images/deskew-example.png "ejemplo de cómo corregir la inclinación de una imagen")

### ¿Por qué aplicar primero un filtro de corrección de inclinación?

Cuando un documento está rotado aunque sea unos pocos grados, el motor OCR interpreta mal las líneas base, lo que genera una salida confusa. El `DeskewFilter` estima automáticamente el ángulo de rotación (hasta `MaxAngle` grados) y rota el bitmap de vuelta a una línea base horizontal. El `DeskewConfidence` devuelto indica cuán seguro está el algoritmo sobre la corrección—útil para registros o estrategias de respaldo.

---

## Preprocesar la imagen para OCR – Construyendo la cadena de filtros

### 1️⃣ DeskewFilter (Paso principal)

- **Qué hace:** Detecta la dirección dominante de la línea de texto y rota la imagen.
- **Por qué importa:** Una línea base recta maximiza la precisión de segmentación de caracteres.
- **Consejo:** Si tus documentos nunca superan los 10°, establece `MaxAngle = 10` para acelerar la detección.

### 2️⃣ DenoiseFilter (Limpieza secundaria)

- **Qué hace:** Reduce el ruido aleatorio de píxeles que puede aparecer después del escaneo.
- **Por qué importa:** El ruido a menudo crea bordes falsos, confundiendo la segmentación del OCR.
- **Consejo:** Ajusta `Strength` entre 0.3 (ligero) y 0.8 (agresivo) según la calidad del escaneo.

### 3️⃣ ContrastBoostFilter (Pulido final)

- **Qué hace:** Aumenta la diferencia entre el texto en primer plano y el fondo.
- **Por qué importa:** Un bajo contraste puede hacer que los caracteres tenues sean invisibles para el motor de reconocimiento.
- **Consejo:** Un `Level` de 1.2 funciona para la mayoría de los escaneos en blanco y negro; para documentos en color, experimenta con valores hasta 2.0.

Al encadenar estos tres filtros, **preprocesas la imagen para OCR** de manera que aborda los puntos de dolor más comunes: inclinación, ruido y bajo contraste.

---

## Cómo mejorar la precisión del OCR con corrección de inclinación y reducción de ruido

Podrías preguntar: “Si ya tengo un filtro de corrección de inclinación, ¿por qué añadir reducción de ruido y aumento de contraste?” La respuesta está en la **mejora acumulativa**. Cada filtro aborda una falla diferente, y juntos elevan la confianza general.

#### Prueba en el mundo real

| Prueba | Precisión OCR original | Después de Deskew | Después de la cadena completa |
|--------|------------------------|-------------------|-------------------------------|
| Factura simple (inclinación 5°) | 78 % | 92 % | 96 % |
| Escaneo de periódico antiguo (inclinación 15°, granulado) | 61 % | 78 % | 88 % |
| Formulario de bajo contraste (sin inclinación) | 70 % | 71 % | 84 % |

*Los números son ilustrativos pero reflejan ganancias típicas reportadas por usuarios de Aspose.*

**Conclusión clave:** Incluso si tu objetivo principal es **corregir la inclinación de una imagen escaneada**, añadir pasos de reducción de ruido y aumento de contraste suele producir un salto notable en la calidad final del texto.

---

## Verificando los resultados de la corrección de inclinación

Después de ejecutar la cadena, recibes dos piezas de información útiles:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- La **confianza de corrección** (`result.DeskewConfidence`) es un porcentaje. Valores superiores al 90 % suelen indicar que la rotación se corrigió con precisión.
- El **texto reconocido** (`result.Text`) te permite verificar al instante si la salida tiene sentido.

Si la confianza es baja (< 70 %), considera:

1. **Aumentar `MaxAngle`** – tal vez el documento esté rotado más de lo esperado.
2. **Añadir un `BinarizationFilter`** antes del deskew para simplificar la imagen.
3. **Rotar manualmente** la imagen usando `OcrImage.Rotate(angle)` como solución alternativa.

---

## Ejemplo completo de extremo a extremo (listo para ejecutar)

A continuación tienes el **programa completo y autocontenido** que puedes copiar y pegar en un nuevo proyecto de aplicación de consola. Recuerda reemplazar `YOUR_DIRECTORY` con la carpeta que contiene tu TIFF inclinado.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Salida esperada** (asumiendo un escaneo razonablemente limpio):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Si ves caracteres confusos, revisa las intensidades de los filtros o añade un `BinarizationFilter` como se mencionó antes.

---

## Errores comunes y consejos profesionales

- **Error:** Usar un TIFF con varias páginas. `OcrImage.FromFile` solo lee el primer marco. Usa `OcrImage.FromMultiPageFile` si necesitas todas las páginas.
- **Error:** Olvidar liberar `OcrEngine`. Envuélvelo en un bloque `using` en código de producción para liberar recursos nativos.
- **Consejo profesional:** Cachea la cadena de filtros si procesas muchas imágenes con la misma configuración—reduce la sobrecarga.
- **Consejo profesional:** Registra `DeskewConfidence` en un sistema de monitoreo; caídas repentinas pueden indicar un cambio en la calibración del escáner.

---

## Próximos pasos – Extender el flujo de trabajo

Ahora que sabes **cómo corregir la inclinación de una imagen** y **preprocesar la imagen para OCR**, puedes explorar:

- **Procesamiento por lotes** – recorre una carpeta de PDFs escaneados, convierte cada página a imagen y aplica la misma cadena.
- **Soporte de idiomas** – establece `engine.Language = OcrLanguage.English;` u otros idiomas para mejorar el reconocimiento.
- **Post‑procesamiento personalizado** – usa expresiones regulares para limpiar errores comunes del OCR (p. ej., “0” vs “O”).

Cada uno de estos temas se relaciona naturalmente con las palabras clave secundarias **cómo mejorar OCR** y **corregir imagen escaneada**.

---

## Conclusión

Hemos cubierto todo lo que necesitas saber sobre **cómo corregir la inclinación de una imagen** usando Aspose.OCR, desde construir una cadena de filtros robusta hasta verificar los puntajes de confianza. Al **preprocesar la imagen para OCR** con deskew, denoise y contrast boost, observarás un aumento medible en los resultados de **cómo mejorar OCR**, especialmente en escaneos inclinados o ruidosos.

Pruébalo con tu propio conjunto de documentos, ajusta los parámetros de los filtros y observa cómo la precisión del OCR sube. ¿Tienes preguntas o un archivo complicado que se niega a enderezarse? Deja un comentario abajo—¡solucionemos juntos! Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques alternativos en tus propios proyectos.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}