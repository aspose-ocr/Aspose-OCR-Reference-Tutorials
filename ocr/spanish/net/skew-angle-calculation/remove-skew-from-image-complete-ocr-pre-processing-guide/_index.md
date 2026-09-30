---
category: general
date: 2026-02-14
description: Aprende cómo eliminar la inclinación de una imagen, preprocesar la imagen
  para OCR, reducir el ruido en la imagen y extraer texto de la imagen usando Aspose
  OCR en C#.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: es
og_description: Elimina la inclinación de la imagen, preprocesa la imagen para OCR
  y extrae texto de la imagen con un tutorial paso a paso en C# usando Aspose OCR.
og_title: Eliminar la inclinación de la imagen – Guía completa de preprocesamiento
  OCR
tags:
- OCR
- CSharp
- ImageProcessing
title: Eliminar la inclinación de la imagen – Guía completa de preprocesamiento OCR
url: /es/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eliminar la inclinación de la imagen – Guía completa de pre‑procesamiento OCR

¿Alguna vez necesitaste **eliminar la inclinación de la imagen** antes de enviarla a un motor OCR? No eres el único: documentos escaneados, fotos de recibos o capturas de pantalla a menudo llegan torcidos, y ese pequeño ángulo puede sabotear el reconocimiento de texto.  

¿La buena noticia? Con un puñado de filtros de Aspose OCR puedes enderezar, reducir ruido, aumentar el contraste y luego **extraer texto de la imagen** en una única y fluida canalización. En esta guía recorreremos todo el proceso, desde cargar una foto sesgada hasta **reconocer texto del documento** e imprimir el resultado.

---

## Lo que vas a construir

Al final de este tutorial tendrás una aplicación de consola C# lista para ejecutar que:

1. **Elimina la inclinación de la imagen** usando `DeskewFilter`.
2. **Reduce el ruido en la imagen** con `DenoiseFilter`.
3. **Preprocesa la imagen para OCR** aumentando el contraste.
4. **Reconoce texto del documento** mediante `Engine` de Aspose OCR.
5. **Extrae texto de la imagen** y lo muestra en la consola.

Sin servicios externos, solo el paquete NuGet Aspose OCR y unas cuantas líneas de código.

---

## Requisitos previos

- .NET 6.0 SDK o posterior (el código funciona también con .NET Core y .NET Framework).  
- Visual Studio 2022 o cualquier editor que prefieras.  
- Aspose.OCR para .NET instalado (`dotnet add package Aspose.OCR`).  
- Una imagen de ejemplo (`skewed_noisy.jpg`) ubicada en una carpeta a la que puedas referenciar.

Si ya tienes todo eso, vamos al grano.

---

## Paso 1: Cargar la imagen de origen

Lo primero que necesitamos es un `ImageStream` que apunte al archivo que queremos limpiar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Por qué es importante:** `ImageStream` abstrae el bitmap subyacente, permitiendo que los filtros de Aspose trabajen sin que tengas que gestionar datos de píxeles crudos.

---

## Paso 2: Construir una canalización de pre‑procesamiento (Eliminar inclinación y reducir ruido)

En lugar de llamar a cada filtro por separado, Aspose te permite encadenarlos en un `ImageProcessingPipeline`. Esto mantiene el código ordenado y asegura que las operaciones ocurran en el orden correcto.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### Por qué el orden es importante

1. **Deskew primero** – Enderezar la imagen antes de reducir ruido evita que el filtro de ruido trate los bordes inclinados como artefactos.  
2. **Denoise segundo** – Una vez la foto está nivelada, el algoritmo puede diferenciar mejor la señal del grano.  
3. **Aumento de contraste al final** – Mejorar el contraste después de que la imagen esté limpia maximiza la legibilidad para OCR sin amplificar el ruido.

---

## Paso 3: Aplicar la canalización y obtener una imagen limpia

Ahora ejecutamos la canalización contra el stream original.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

En este punto la imagen está enderezada, sin ruido y con mayor contraste—perfecta para OCR.

---

## Paso 4: Inicializar el motor OCR y reconocer texto

Con una imagen impecable en mano finalmente podemos pasarla a Aspose OCR.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Consejo:** Si necesitas ajustes específicos por idioma, `Engine` acepta una propiedad `Language` (p. ej., `ocrEngine.Language = Language.English;`). Para la mayoría de documentos basados en alfabeto latino el valor predeterminado funciona bien.

---

## Paso 5: Mostrar el texto extraído

Un rápido `Console.WriteLine` muestra el resultado.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

Al ejecutar el programa deberías ver el contenido textual de `skewed_noisy.jpg` impreso en la terminal—limpio, legible y listo para procesamiento posterior.

---

## Ejemplo completo funcional

A continuación tienes el programa completo, listo para copiar y pegar. Guárdalo como `Program.cs`, reemplaza `YOUR_DIRECTORY` con la ruta real y ejecuta `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Salida esperada** (ejemplo para un recibo sencillo):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

Si la salida se ve distorsionada, verifica que la ruta de la imagen sea correcta y que el archivo fuente realmente contenga texto legible.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si la imagen está rotada 90° en lugar de tener una ligera inclinación?

`DeskewFilter` maneja ángulos menores (±15°). Para rotaciones completas, llama a `new RotateFilter { Angle = 90 }` antes del paso de deskew.

### Mi imagen está en formato PNG—¿cambia algo?

No. `ImageStream.FromFile` detecta automáticamente el formato, así que PNG, JPEG, BMP o TIFF funcionan de la misma manera.

### ¿Cómo puedo ajustar la fuerza de reducción de ruido?

`DenoiseFilter` expone una propiedad `Strength` (0‑100). Valores más altos eliminan más grano pero pueden difuminar detalles finos. Experimenta con valores entre 30‑50 para documentos con mucho texto.

### Necesito procesar un lote de archivos—¿puedo reutilizar la canalización?

Claro. Crea `processingPipeline` una sola vez y luego itera sobre cada archivo:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

Reutilizar la misma instancia de `Engine` también mejora el rendimiento.

---

## Consejos profesionales para OCR listo para producción

- **Cachea la canalización**: Instanciar filtros repetidamente puede ser costoso en escenarios de alto rendimiento.  
- **Establece el idioma OCR**: `ocrEngine.Language = Language.Spanish;` para documentos que no sean en inglés.  
- **Maneja resultados vacíos**: Siempre verifica `ocrResult.Text?.Length > 0` antes de continuar.  
- **Registra imágenes intermedias**: Guardar `cleanedImage` en disco (`cleanedImage.Save("debug.png");`) te ayuda a afinar los parámetros de los filtros.

---

## Conclusión

Hemos demostrado cómo **eliminar la inclinación de la imagen**, **reducir el ruido en la imagen** y **preprocesar la imagen para OCR** usando la potente canalización de filtros de Aspose OCR, luego **reconocer texto del documento** y finalmente **extraer texto de la imagen**. Todo el flujo cabe en menos de 50 líneas de C# y es fácil de ampliar para procesamiento por lotes, modelos de idioma personalizados o filtros adicionales.

¿Listo para el siguiente paso? Prueba añadiendo un `BinarizeFilter` para forzar salida en blanco y negro, o experimenta con diferentes niveles de `ContrastBoostFilter` para ver cómo afectan la precisión del reconocimiento. Cuanto más juegues con la canalización, mejor entenderás cómo cada filtro contribuye a un resultado OCR limpio.

¡Feliz codificación, y que tus imágenes siempre permanezcan rectas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}