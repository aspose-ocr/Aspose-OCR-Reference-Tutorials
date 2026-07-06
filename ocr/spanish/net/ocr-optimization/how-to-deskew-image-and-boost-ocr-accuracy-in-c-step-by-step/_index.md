---
category: general
date: 2026-04-17
description: Cómo enderezar una imagen rápidamente usando Aspose.OCR – aprende a cargar
  la imagen para OCR, preprocesar la imagen para OCR y reconocer texto en la imagen
  con alta precisión.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: es
og_description: Cómo corregir la inclinación de una imagen y mejorar la precisión
  del OCR en C#. Aprende a cargar imágenes para OCR, preprocesar imágenes para OCR
  y reconocer texto en imágenes con Aspose.OCR.
og_title: Cómo corregir la inclinación de una imagen – Tutorial completo de OCR en
  C#
tags:
- Aspose.OCR
- C#
- Image Processing
title: Cómo corregir la inclinación de una imagen y mejorar la precisión del OCR en
  C# – Guía paso a paso
url: /es/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen y mejorar la precisión del OCR en C#

**Cómo enderezar una imagen** es un obstáculo común siempre que necesites extraer texto de una foto que no está perfectamente alineada. En esta guía recorreremos la carga de la imagen, su preprocesado y, finalmente, **reconocer texto en la imagen** usando la potente cadena de filtros de Aspose.OCR.

Si alguna vez apuntaste la cámara del móvil a un recibo, un cartel o un formulario escaneado y terminaste con caracteres torcidos e ilegibles, sabes lo frustrante que puede ser. ¿La buena noticia? Unas pocas líneas de código C# pueden enderezar esa foto, eliminar el ruido y devolverte una cadena limpia que realmente puedas usar. También veremos cómo **mejorar la precisión del OCR** ajustando los pasos de preprocesado.

## Lo que necesitarás

- .NET 6.0 o posterior (el código también funciona con .NET Core)  
- Una licencia o copia de evaluación de **Aspose.OCR** (disponible vía NuGet)  
- Un archivo de imagen ligeramente rotado o ruidoso (p. ej., `skewed_photo.png`)  

No se requieren herramientas externas sofisticadas, solo la biblioteca Aspose.OCR y un poco de conocimiento de C#.

![Ejemplo de cómo enderezar una imagen](/images/deskew-demo.png "Cómo enderezar una imagen – original vs corregida")

---

## Paso 1 – Cargar la imagen OCR: Preparar el archivo fuente

Antes de poder enderezar algo, necesitamos cargar la foto en memoria. El método `OcrImage.FromFile` hace exactamente eso.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **Por qué es importante:** Cargar la imagen como un `OcrImage` le da al motor OCR acceso directo a los datos de píxeles, lo cual es esencial para los pasos posteriores de **preprocesado de imagen OCR**. Si la ruta del archivo es incorrecta, obtendrás una `FileNotFoundException`, así que verifica la ubicación.

## Paso 2 – Preprocesado de imagen OCR: Construir una cadena de filtros de enderezado

Ahora llega el corazón de **cómo enderezar una imagen**. Aspose.OCR incluye una colección de filtros que puedes apilar en cualquier orden. Para la mayoría de fotos reales querrás:

1. **Deskew** – corregir la rotación  
2. **Denoise** – eliminar los puntos de sal‑y‑pimienta  
3. **ContrastEnhance** – hacer que los caracteres tenues resalten

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **Consejo profesional:** Si tu imagen ya está bien expuesta, puedes omitir el `ContrastEnhanceFilter`. Menos procesamiento significa una ejecución más rápida.

### Casos límite

- **Rotación extrema (>45°):** El `DeskewFilter` funciona mejor hasta aproximadamente 30°. Para ángulos mayores quizás necesites rotar la imagen manualmente primero (`filteredImage.Rotate(…)`).
- **Fondos coloreados:** Convierte a escala de grises antes de eliminar el ruido para obtener mejores resultados (`filteredImage = filteredImage.ToGrayscale();`).

## Paso 3 – Reconocer texto en la imagen: Ejecutar el motor OCR

Con un bitmap limpio y enderezado, es hora de extraer los caracteres.

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **¿Qué ocurre tras bambalinas?** `OcrEngine` ejecuta un reconocedor basado en redes neuronales que espera una imagen casi vertical y de alto contraste. Por eso el paso previo de **preprocesado de imagen OCR** es crucial para **mejorar la precisión del OCR**.

### Salida esperada

Si la foto original contenía la línea “Invoice #12345 – Total $89.99”, la consola imprimirá algo como:

```
Invoice #12345 – Total $89.99
```

Si ves caracteres distorsionados, revisa la cadena de filtros—quizá la imagen necesite un afilado adicional (`new SharpenFilter()`).

## Paso 4 – Ajuste fino para mejorar la precisión del OCR

Incluso después de enderezar, el OCR puede tropezar con ciertas tipografías o escaneos de baja resolución. Aquí tienes algunos ajustes rápidos:

| Problema | Solución |
|----------|----------|
| Tamaño de fuente pequeño (<10 pt) | Escalar la imagen (`filteredImage = filteredImage.Resize(2.0);`) |
| Texto gris claro sobre blanco | Aumentar aún más el contraste (`new ContrastEnhanceFilter(1.5)`) |
| Texto multilingüe | Establecer `ocrEngine.Language = OcrLanguage.Multilingual;` |

Estos ajustes **mejoran la precisión del OCR** sin cambiar la estructura central del código.

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para ejecutar, que incorpora todos los pasos anteriores. Cópialo en un nuevo proyecto de consola y pulsa **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Ejecuta el programa y deberías ver el texto limpio y enderezado impreso en la consola.

## Preguntas frecuentes

**P: ¿Esto funciona con PDFs?**  
R: Sí. Convierte cada página del PDF a una imagen (p. ej., usando `Aspose.PDF`) y pasa el bitmap resultante a la misma cadena de filtros.

**P: ¿Qué pasa si mi imagen ya está perfectamente alineada?**  
R: El `DeskewFilter` detectará un ángulo cercano a cero y dejará la imagen sin cambios—no causa ningún daño.

**P: ¿Puedo procesar varias imágenes en lote?**  
R: Por supuesto. Envuelve el código en un bucle `foreach (var path in Directory.GetFiles(...))` y almacena cada `ocrResult.Text` en una lista o archivo.

---

## Conclusión

Hemos demostrado **cómo enderezar una imagen** programáticamente, recorrido el paso **cargar imagen OCR**, aplicado una robusta canalización de **preprocesado de imagen OCR**, y finalmente **reconocido texto en la imagen** con Aspose.OCR. Ajustando los filtros y, opcionalmente, escalando o afilando, puedes **mejorar la precisión del OCR** para una amplia gama de escenarios del mundo real.

¿Listo para el siguiente reto? Prueba integrar esta canalización en una API web, o experimenta con reconocimiento de notas manuscritas añadiendo `new BinarizationFilter()` antes del enderezado. Las posibilidades son infinitas—¡feliz codificación!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}