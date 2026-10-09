---
category: general
date: 2026-03-07
description: Aprende a enderezar la imagen, mejorar el contraste y extraer texto de
  un escaneo usando Aspose OCR. Realiza OCR en una imagen con un ejemplo completo
  en C# y carga la imagen para OCR fácilmente.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: es
og_description: Aprende cómo enderezar una imagen, mejorar el contraste y extraer
  texto de un escaneo usando Aspose OCR en C#. Realiza OCR en una imagen con código
  paso a paso.
og_title: Cómo enderezar una imagen y ejecutar OCR en C# – Guía completa
tags:
- C#
- OCR
- Image Processing
title: Cómo enderezar la imagen y ejecutar OCR en C# – Guía completa
url: /es/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen y ejecutar OCR en C# – Guía completa

Si alguna vez te has preguntado **cómo enderezar una imagen** antes de ejecutar OCR, estás en el lugar correcto. En este tutorial te guiaremos paso a paso para mejorar el contraste, cargar una imagen para OCR y, finalmente, **extraer texto de un escaneo** con Aspose OCR.  

Ya sea que estés digitalizando recibos antiguos, limpiando contratos escaneados o simplemente necesites una forma fiable de leer texto de una foto torcida, los pasos a continuación cubren todo lo que necesitas. Sin rodeos—solo un ejemplo funcional que puedes copiar‑pegar en Visual Studio.  

## Lo que lograrás

Al final de esta guía podrás:

* Corregir la inclinación hasta 30° (esa es la parte de **cómo enderezar una imagen**).  
* Aumentar el contraste de la imagen para obtener bordes de caracteres más nítidos (**cómo mejorar el contraste**).  
* Cargar tu foto en el motor OCR (**cargar imagen para OCR**).  
* Ejecutar el proceso de reconocimiento y **extraer texto de un escaneo**.  

Todo esto funciona con la última versión del paquete NuGet Aspose.OCR .NET (v23.11 al momento de escribir).  

---

![Ejemplo de cómo enderezar una imagen](/images/deskew-example.png "cómo enderezar una imagen")

*La imagen de arriba muestra un documento escaneado antes y después de enderezarlo.*

## Requisitos previos

* .NET 6.0 o posterior (el código también funciona en .NET Framework 4.7+).  
* Visual Studio 2022 (o cualquier IDE de C# que prefieras).  
* Paquete NuGet Aspose.OCR – instálalo con `dotnet add package Aspose.OCR`.  

Eso es todo. Sin servicios externos, sin claves API.

---

## Cómo enderezar una imagen con Aspose OCR

Lo primero que hacemos es crear un **ImageProcessingPipeline** y añadir un `DeskewFilter`. El filtro detecta automáticamente el ángulo dominante de la línea de texto y rota la imagen de vuelta a la horizontal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Por qué es importante:**  
Un escaneo inclinado confunde al motor OCR porque los caracteres ya no están alineados con la línea base. El `DeskewFilter` analiza el histograma de la imagen, encuentra el ángulo y la rota, mejorando drásticamente la precisión del reconocimiento.

> **Consejo profesional:** Si sabes que tus documentos nunca superan una inclinación de 15°, establece `MaxAngle = 15` para acelerar el procesamiento.

---

## Cómo mejorar el contraste para un mejor reconocimiento

Después de enderezar, el siguiente paso es hacer que el texto destaque. El `ContrastBoostFilter` extiende el rango de intensidad de los píxeles, lo que es especialmente útil para impresiones descoloridas.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Por qué ayuda:**  
Los escaneos de bajo contraste producen caracteres grisáceos que el binarizador puede interpretar como fondo. Aumentar el contraste oscurece más los píxeles oscuros y aclara más los claros, proporcionando al `BinarizationFilter` un lienzo más limpio.

---

## Realizar OCR en la imagen – Cargando el archivo

Ahora que la imagen está pre‑procesada, necesitamos **cargar imagen para OCR**. Aspose ofrece un práctico asistente `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Si tu imagen está en un stream (por ejemplo, cargada mediante una API web), puedes usar `ImageStream.FromStream(yourStream)` en su lugar. El motor acepta BMP, JPEG, PNG, TIFF y muchos otros formatos.

---

## Ejecutar el proceso de reconocimiento y extraer texto del escaneo

Con todo conectado, invocar `Recognize()` realiza el trabajo pesado. Después de la llamada, el texto reconocido está disponible a través de `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Salida esperada** (ejemplo para una factura sencilla):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Si la salida se ve distorsionada, verifica el orden de la canalización: enderezar primero, luego eliminar ruido, mejorar contraste y finalmente binarizar. Cambiar ese orden puede degradar los resultados.

---

## Problemas comunes y casos límite

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Resultado vacío** | La imagen es demasiado oscura o demasiado clara para el método de binarización predeterminado. | Aumenta `ContrastBoostFilter.Strength` o cambia a `BinarizationMethod.Otsu`. |
| **Texto parcial faltante** | Queda ruido después de la eliminación de ruido. | Usa `DenoiseLevel.Medium` para imágenes más suaves, o añade un segundo `DenoiseFilter`. |
| **Dirección de rotación incorrecta** | El documento tiene orientación mixta (p. ej., una foto de una página girada). | Establece manualmente `DeskewFilter.MaxAngle` a un valor menor y pre‑rota la imagen con `ImageProcessor.Rotate`. |
| **Ralentización del rendimiento** | Gran lote de imágenes de alta resolución. | Reduce la escala de las imágenes (`ImageProcessor.Resize`) antes de la canalización, o procesa en paralelo (`Parallel.ForEach`). |

---

## Ejemplo completo (listo para copiar‑pegar)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Guarda esto como `Program.cs`, ejecuta `dotnet run` y observa cómo la consola muestra el resultado de **extraer texto del escaneo**.  

---

## Próximos pasos y temas relacionados

* **Procesamiento por lotes** – Envuelve la lógica anterior en un bucle para manejar docenas de archivos.  
* **Paquetes de idioma personalizados** – Si necesitas leer scripts no latinos, carga un modelo de idioma mediante `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **Salida PDF** – Combina Aspose.PDF con OCR para incrustar texto buscable directamente en un archivo PDF.  
* **Ajuste de rendimiento** – Experimenta con el orden de `ImageProcessingPipeline`; a veces eliminar ruido antes de enderezar produce resultados más rápidos en fotos ruidosas.  

Todos estos se basan en los conceptos centrales que cubrimos: **cómo enderezar una imagen**, **cómo mejorar el contraste**, **cargar imagen para OCR**, **realizar OCR en la imagen**, y finalmente **extraer texto del escaneo**.

---

## Conclusión

Acabamos de demostrar una forma completa y lista para producción de **cómo enderezar una imagen** y ejecutar OCR en C#. Al encadenar un filtro de enderezado, un paso de eliminación de ruido, un aumento de contraste y un binarizador, obtienes una entrada limpia que permite a Aspose OCR extraer texto de forma fiable de los escaneos.  

Prueba el código, ajusta los parámetros de los filtros para tus propios documentos y verás cuán rápido mejora la precisión del reconocimiento. ¿Tienes preguntas? Deja un comentario, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}