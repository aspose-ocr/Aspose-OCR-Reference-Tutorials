---
category: general
date: 2026-03-20
description: Aprenda cómo enderezar la imagen y eliminar el ruido de la imagen con
  Aspose OCR. Esta guía paso a paso también muestra cómo preprocesar la imagen para
  OCR y mejorar la precisión del OCR.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: es
og_description: Aprende a enderezar imágenes y eliminar el ruido con Aspose OCR. Mejora
  la precisión de tu OCR en minutos.
og_title: Cómo corregir la inclinación de una imagen – Guía completa en C# para el
  preprocesamiento de OCR
tags:
- OCR
- C#
- Image Processing
title: Cómo corregir la inclinación de una imagen – Guía completa en C# para el preprocesamiento
  OCR
url: /es/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen – Guía completa en C# para el pre‑procesamiento OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** que salió de un escáner con un ángulo extraño? No eres el único; muchos desarrolladores se topan con ese problema al intentar alimentar una foto a un motor OCR. La buena noticia es que con unas pocas líneas de C# y Aspose OCR puedes alinear, eliminar ruido y aumentar el contraste en una única canalización ordenada—sin necesidad de Photoshop.

En este tutorial repasaremos todo lo que necesitas saber: desde cargar una foto sesgada, hasta **eliminar el ruido de la imagen**, **preprocesar la imagen para OCR**, y finalmente **reconocer texto de la imagen** con una alta puntuación de **mejorar la precisión OCR**. Al final tendrás una aplicación de consola lista para ejecutarse que convierte un escaneo desordenado en texto limpio y buscable.

## Lo que necesitarás

- .NET 6 o posterior (el código usa la sintaxis `using var`, compatible desde C# 8)
- Un paquete NuGet de Aspose OCR (`Aspose.OCR`) – instálalo con `dotnet add package Aspose.OCR`
- Una imagen de ejemplo que esté tanto sesgada como ruidosa (p. ej., `skewed_noisy.png`)
- Un IDE o editor de tu preferencia (Visual Studio, VS Code, Rider… tú eliges)

> **Consejo profesional:** Si no tienes un archivo de muestra, simplemente rota una captura de pantalla clara unos grados y añade algo de ruido “sal‑y‑pimienta” con un editor de imágenes. La canalización funciona de la misma manera.

## Paso 1: Cómo enderezar una imagen con un filtro Deskew

Lo primero que hacemos es corregir la rotación. Aspose proporciona un `DeskewFilter` que puede detectar automáticamente ángulos hasta un `MaxAngle` configurable. Establecerlo en **5°** es un valor predeterminado seguro para la mayoría de documentos escaneados.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Por qué es importante:**  
Si el texto está inclinado, el algoritmo OCR puede interpretar mal los caracteres—por ejemplo, una “l” convirtiéndose en “i”. Al **enderezar** primero, le das al motor un lienzo recto con el que trabajar.

## Paso 2: Eliminar el ruido de la imagen con Despeckle

Los escaneos de teléfonos baratos o escáneres antiguos a menudo contienen manchas que parecen puntos aleatorios. Esas manchas confunden al reconocedor de caracteres. El `DespeckleFilter` suaviza la imagen mientras preserva los bordes.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Si necesitas **eliminar el ruido de la imagen** de forma más agresiva, aumenta `Strength` a 3 o 4—pero vigila la pérdida de trazos finos.

## Paso 3: Preprocesar la imagen para OCR – Aumento de contraste

Los escaneos de bajo contraste (gris claro sobre papel blanco) pueden hacer que el OCR omita letras tenues. El `ContrastFilter` extiende el rango tonal, haciendo los píxeles oscuros más oscuros y los claros más claros.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Caso límite:** Si tu imagen de origen ya tiene alto contraste, aplicar este filtro puede lavar los detalles. En ese caso, establece `Level` en `1.0` (desactivándolo efectivamente).

## Paso 4: Cargar y limpiar la imagen de origen

Ahora realmente cargamos la foto y la pasamos por la canalización que acabamos de ensamblar.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Nota:** El método `Apply` devuelve un nuevo objeto `Image`; el original permanece intacto. Esto facilita comparar “antes” y “después” si deseas depurar el proceso.

## Paso 5: Reconocer texto de la imagen usando Aspose OCR

Con una foto recta, sin ruido y de alto contraste en mano, finalmente la entregamos al motor OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Lo que deberías ver:** La consola imprime el contenido textual del escaneo original, generalmente con muchas menos equivocaciones que si hubieras alimentado el archivo crudo directamente.

## Paso 6: Verificar y mejorar la precisión OCR

Incluso con una canalización sólida, algunos caracteres pueden seguir estando equivocados—sobre todo si la fuente original es poco común. Aquí tienes algunos trucos rápidos para **mejorar la precisión OCR**:

| Problema | Solución rápida |
|----------|-----------------|
| Falta puntuación pequeña | Añade un `BinaryThresholdFilter` antes del paso de contraste |
| Idioma mixto (p. ej., English + Spanish) | Configura `ocrEngine.Language = Language.English | Language.Spanish;` |
| Fondo muy oscuro | Invierte la imagen (`new InvertFilter()`) antes de enderezar |
| Documentos extensos | Procesa páginas en paralelo (`Parallel.ForEach`) para acelerar |

Experimenta con el orden de los filtros; a veces aplicar **contraste** antes del **despeckle** produce mejores resultados en escaneos de baja calidad.

## Ejemplo completo y funcional

A continuación tienes el programa completo que puedes copiar y pegar en un nuevo proyecto de consola. Incluye todas las piezas que discutimos, más un par de comprobaciones de seguridad.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Salida esperada** (suponiendo que la imagen de muestra contiene “Hello World!”):

```
=== OCR Output ===

Hello World!
```

Si ves caracteres distorsionados, verifica el orden de la canalización o incrementa `DespeckleFilter.Strength`.

## Conclusión

Hemos cubierto **cómo enderezar una imagen**, **eliminar el ruido de la imagen**, **preprocesar la imagen para OCR**, y finalmente **reconocer texto de la imagen** usando Aspose OCR—todo mientras nos enfocamos en **mejorar la precisión OCR**. El ejemplo completo y ejecutable muestra cada paso en contexto, de modo que puedes insertarlo en cualquier proyecto .NET y comenzar a extraer texto de inmediato.

¿Listo para el siguiente desafío? Prueba a extender la canalización para manejar PDFs multipágina, o experimenta con paquetes de idioma para documentos multilingües. Los mismos conceptos se aplican—solo cambia la bandera `Language` y quizá añade un `RotateFilter` para páginas que estén al revés.

¿Tienes preguntas o una imagen complicada que aún no coopera? Deja un comentario abajo y lo solucionaremos juntos. ¡Feliz codificación!

![ejemplo de cómo enderezar una imagen](/images/deskew-example.png "Ilustración de cómo enderezar una imagen usando Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}