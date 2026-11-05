---
category: general
date: 2026-01-13
description: cómo enderezar una imagen y eliminar el ruido de la imagen en C# – aprende
  a aumentar el contraste de la imagen, preprocesar OCR de imágenes y aplicar múltiples
  filtros de imagen.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: es
og_description: cómo enderezar una imagen y eliminar el ruido de la imagen en C# –
  aprende a aumentar el contraste de la imagen, preprocesar OCR de imágenes y aplicar
  múltiples filtros de imagen.
og_title: Cómo corregir la inclinación de una imagen – Guía completa de preprocesamiento
  en C# para OCR
tags:
- OCR
- C#
- Image Processing
title: Cómo corregir la inclinación de una imagen – Guía completa de preprocesamiento
  en C# para OCR
url: /es/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo enderezar una imagen – Guía completa de pre‑procesamiento en C# para OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** antes de enviarla a un motor OCR? No estás solo. En muchos escenarios reales—contratos escaneados, recibos o fotocopias antiguas—el texto está ligeramente inclinado, la foto se ve granulada y el contraste es irregular. ¿La buena noticia? Unas pocas líneas de código C# pueden corregir esa inclinación, eliminar el ruido de la imagen y mejorar el contraste, proporcionando una base sólida para tu OCR.

En este tutorial recorreremos un **ejemplo completo y ejecutable** que muestra exactamente cómo enderezar una imagen, eliminar el ruido, aumentar el contraste y luego ejecutar OCR con Aspose.OCR. Al final tendrás una canalización reutilizable que aplica **múltiples filtros de imagen** en una única llamada fluida—sin conjeturas.

## Qué necesitarás

- **.NET 6+** (o cualquier versión reciente de .NET; la API funciona igual)
- **Aspose.OCR for .NET** paquete NuGet (`Aspose.OCR` y `Aspose.OCR.Filters`)
- Una imagen escaneada de ejemplo (p. ej., `skewed_noisy.png`) que presente inclinación, ruido y bajo contraste
- Tu IDE favorito (Visual Studio, Rider, VS Code—elige el que prefieras)

Si ya tienes un proyecto configurado, solo agrega la referencia NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Consejo profesional:** Aspose ofrece una prueba gratuita con un número limitado de páginas—perfecta para probar el código a continuación.

## Paso 1: Crear la instancia del motor OCR

Lo primero que hacemos es iniciar un `OcrEngine`. Piensa en él como el cerebro que más tarde leerá el texto. No hay nada sofisticado aquí, pero es la base de todo lo que sigue.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Por qué importa:** Inicializar el motor una sola vez y reutilizarlo para muchas imágenes evita la sobrecarga de cargar los datos de idioma repetidamente.

## Paso 2: Cargar la imagen escaneada sin procesar

A continuación extraemos la imagen del disco. El método `OcrImage.FromFile` lee el archivo en un formato que Aspose puede manipular.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Caso límite:** Si tu imagen está en un formato no estándar (TIFF, BMP), Aspose aún la maneja, pero podrías convertirla a PNG primero para mayor consistencia.

## Paso 3: Construir una canalización de pre‑procesamiento (Enderezar → Eliminar ruido → Contraste)

Aquí respondemos a la pregunta central **cómo enderezar una imagen** mientras también **eliminamos el ruido** y **aumentamos el contraste**. La API fluida de Aspose nos permite encadenar filtros, haciendo que el código se lea como una frase.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### Qué hace cada filtro

| Filtro | Propósito | Impacto típico |
|--------|-----------|----------------|
| **DeskewFilter** | Detecta el ángulo de las líneas de texto y rota la imagen para que queden horizontales. | Elimina la inclinación que confunde al OCR, reduciendo frecuentemente la tasa de error entre un 30‑50 %. |
| **DenoiseFilter** | Aplica un algoritmo de suavizado que preserva los bordes mientras descarta el ruido aleatorio de píxeles. | Limpia recibos escaneados o fotos con poca luz, haciendo los caracteres más claros. |
| **ContrastFilter** | Extiende el histograma para que las áreas oscuras se vuelvan más oscuras y las claras más claras. | Mejora la distinción entre texto y fondo, especialmente útil para documentos descoloridos. |

> **¿Por qué encadenarlos?** Enderezar primero garantiza que el filtro de reducción de ruido actúe sobre una imagen correctamente orientada; aumentar el contraste al final hace que el texto limpio resalte para el motor OCR.

## Paso 4: Ejecutar OCR sobre la imagen procesada

Ahora que la imagen está recta, limpia y con alto contraste, la entregamos al motor OCR. Usaremos datos de idioma inglés, pero Aspose soporta más de 150 idiomas.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Si necesitas otro idioma, simplemente reemplaza `OcrLanguage.English` por el valor de enumeración correspondiente (p. ej., `OcrLanguage.Spanish`).

## Paso 5: Mostrar el texto reconocido

Finalmente, imprimimos el resultado en la consola. En una aplicación real podrías escribirlo en un archivo, una base de datos o alimentar el texto a pipelines de NLP posteriores.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Salida esperada

Ejecutar el programa completo contra un recibo típicamente inclinado produce algo como:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Si la salida se ve distorsionada, verifica la imagen original—un desenfoque excesivo o una oscuridad extrema podrían requerir pre‑procesamiento adicional (p. ej., un `SharpenFilter`).

![ejemplo de cómo enderezar una imagen](images/deskewed_example.png "cómo enderezar una imagen – antes y después del procesamiento")

*La imagen anterior muestra la escaneada original inclinada a la izquierda y la versión corregida, sin ruido y con alto contraste a la derecha.*

## Consejos adicionales y errores comunes

### 1. Cuando el ángulo de inclinación es extremo

Si el documento está inclinado más de 30°, el `DeskewFilter` puede tener dificultades. En ese caso, rota la imagen manualmente antes:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Manejo de imágenes en color

Los filtros trabajan internamente en escala de grises, pero puedes forzar una conversión:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Ajustar la fuerza de eliminación de ruido

`DenoiseFilter` acepta un parámetro opcional `strength` (0‑100). Valores más altos eliminan más ruido pero pueden difuminar detalles finos.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Usar múltiples filtros de imagen más allá de lo básico

Aspose incluye muchos más filtros: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter`, etc. Puedes combinarlos para crear una canalización personalizada que se ajuste a tu tipo de documento.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa entero, listo para colocar en un proyecto de consola.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Ejecuta el programa con `dotnet run`. Si todo está configurado correctamente, la consola mostrará texto limpio y legible extraído de tu imagen originalmente inclinada y ruidosa.

## Conclusión

Acabamos de cubrir **cómo enderezar una imagen** en C# mientras simultáneamente **eliminamos el ruido**, **aumentamos el contraste** y **preprocesamos la imagen para OCR** con una cadena de **múltiples filtros de imagen**. La lección clave es que una canalización de pre‑procesamiento bien ordenada puede mejorar drásticamente la precisión del OCR—convirtiendo a menudo un escaneo apenas legible en texto perfectamente legible.

¿Listo para el siguiente paso? Prueba a sustituir el `ContrastFilter` por un `BinarizeFilter` para ver cómo la conversión binaria (blanco y negro) afecta tus resultados, o experimenta con el `ResizeFilter` para proporcionar una imagen de mayor resolución al motor. El mismo patrón se aplica sin importar los filtros que elijas, por lo que ahora tienes una base flexible para todos tus futuros proyectos de OCR.

¿Tienes preguntas sobre el manejo de PDFs, OCR multilingüe o la integración en una API ASP.NET? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}