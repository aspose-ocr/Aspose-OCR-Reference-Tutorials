---
category: general
date: 2026-05-28
description: Tutorial de OCR de idioma coreano usando Aspose en C#. Aprende cómo cargar
  una imagen desde un flujo, extraer texto plano, convertir la imagen a PDF y exportar
  un PDF buscable.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: es
og_description: OCR de idioma coreano en C# usando Aspose. Guía paso a paso para cargar
  la imagen desde un flujo, extraer texto plano, convertir la imagen a PDF y exportar
  un PDF buscable.
og_title: OCR de idioma coreano – Convertir imagen a PDF y extraer texto (Guía C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR de idioma coreano con Aspose: Convertir imagen a PDF y extraer texto en
  C#'
url: /es/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de idioma coreano con Aspose: Convertir imagen a PDF y extraer texto en C#

¿Alguna vez te has preguntado cómo ejecutar **OCR de idioma coreano** en una foto sin enviar nada a la nube? No eres el único. Ya sea que estés digitalizando señales callejeras, procesando recibos o construyendo un índice de búsqueda multilingüe, poder reconocer caracteres coreanos localmente puede ahorrarte tiempo, dinero y dolores de cabeza relacionados con la privacidad.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra cómo **cargar una imagen desde un stream**, **extraer texto plano**, **convertir la imagen a PDF** y, finalmente, **exportar un PDF buscable**, todo con Aspose.OCR y unas pocas líneas de C#. Sin servicios externos, sin magia oculta, solo código .NET puro que puedes colocar en cualquier aplicación de consola.

## Qué obtendrás al final

- Un programa de consola funcional que lee un archivo JPEG a través de un flujo de archivo.  
- Texto coreano extraído como cadenas Unicode simples.  
- Un informe JSON detallado de la ejecución OCR para depuración o análisis.  
- Un PDF buscable que puedes abrir en cualquier lector de PDF y seleccionar realmente las palabras coreanas.  

**Prerequisitos**  
- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.7+).  
- Paquete NuGet Aspose.OCR for .NET instalado (`Install-Package Aspose.OCR`).  
- Una carpeta que contenga `korean_sign.jpg` y una ubicación con permisos de escritura para los archivos de salida.  

Si ya tienes esos componentes listos, genial—pongámonos manos a la obra.

## Paso 1: Inicializar el motor OCR para OCR de idioma coreano

Lo primero que necesitas es una instancia de `OcrEngine`. Habilitar la GPU (si dispones de una) acelera el reconocimiento de forma dramática, y desactivar la descarga automática de recursos obliga a la biblioteca a usar los paquetes de idioma offline que proporciones.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Por qué es importante:**  
> La *aceleración por GPU* puede reducir el tiempo de procesamiento de segundos a milisegundos para lotes grandes. Configurar `AutomaticResourceDownload` a `false` garantiza que la demo funcione sin conexión, un requisito crucial para muchos entornos empresariales.

## Paso 2: Cargar imagen desde un stream

Leer la imagen a través de un stream te brinda flexibilidad: puedes obtener archivos del disco, de recursos compartidos en red o incluso de blobs almacenados en memoria. Aquí abrimos un archivo JPEG local, pero el mismo patrón funciona con cualquier `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Consejo profesional:** Si alguna vez necesitas procesar imágenes subidas mediante una API web, simplemente reemplaza `File.OpenRead` por `IFormFile.OpenReadStream()` entrante; el resto permanece idéntico.

## Paso 3: Seleccionar idioma coreano y aplicar filtros de pre‑procesamiento

Aspose.OCR admite un conjunto de pasos de preprocesamiento que limpian la imagen antes del reconocimiento. Para señales coreanas, la corrección de inclinación y la eliminación de ruido suelen ser suficientes.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **¿Qué ocurre bajo el capó?**  
> El filtro `Deskew` endereza el texto rotado, mientras que `Denoise` elimina el grano que puede confundir al clasificador de caracteres. Omitir estos pasos a menudo produce una salida distorsionada, sobre todo en fotos de baja resolución.

## Paso 4: Extraer texto plano de forma asíncrona

Ahora llega el momento de la verdad: pedir al motor que reconozca los caracteres y nos devuelva una cadena limpia. Usar `RecognizeAsync` mantiene la UI responsiva si lo integras en una aplicación de escritorio o web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Al ejecutar el programa, deberías ver algo como:

```
OCR complete. Extracted text:
서울시청
```

> **¿Por qué async?**  
> OCR puede ser intensivo en CPU. La ejecución asíncrona evita que tu hilo se bloquee, lo cual es especialmente útil en ASP.NET Core donde la escasez de hilos es una preocupación real.

## Paso 5: Obtener un resultado de reconocimiento detallado y guardarlo como JSON

A veces necesitas más que la cadena cruda—quizá quieras puntuaciones de confianza, cajas delimitadoras o los datos de la imagen original. El método `RecognizeDetailed` devuelve un objeto `RecognitionResult` que puede serializarse a JSON para análisis posterior.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Abrir `korean_ocr.json` revelará una estructura similar a:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **¿Cuándo usar esto?**  
> Si estás construyendo un índice de búsqueda, los valores de confianza te permiten filtrar resultados de baja calidad. Si necesitas resaltar texto en una UI, las cajas delimitadoras son tu mapa.

## Paso 6: Convertir imagen a PDF y exportar PDF buscable

Aspose hace que el salto de raster a vector sea sin esfuerzo. Al establecer `OutputFormat` a `SearchablePdf`, la biblioteca incrusta la imagen original y superpone una capa de texto invisible que contiene la salida OCR. El PDF resultante puede buscarse, copiarse e indexarse como cualquier PDF nativo.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Abre `korean_searchable.pdf` en Adobe Reader o cualquier visor de PDF, pulsa **Ctrl+F**, escribe una palabra coreana y observa cómo te lleva directamente al punto exacto de la página. Ese es el poder de un PDF buscable.

> **Consejo extra:** Si solo necesitas un PDF visual sin la capa de texto oculta, cambia `OutputFormat` a `Pdf` en su lugar.

## Ejemplo completo y funcional

A continuación tienes el programa completo—copia, pega, reemplaza `YOUR_DIRECTORY` por una ruta real y pulsa **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Salida esperada en la consola

```
OCR complete. Extracted text:
서울시청
```

Y encontrarás tres archivos nuevos junto a tu imagen fuente:

- `korean_ocr.json` – datos completos del reconocimiento.  
- `korean_searchable.pdf` – un PDF que puedes buscar.  
- (opcional) cualquier registro intermedio que decidas añadir.

## Preguntas frecuentes y casos límite

**¿Qué pasa si no tengo GPU?**  
Configura `EnableGpu = false`; el fallback a CPU es perfectamente aceptable para lotes pequeños.

**¿Puedo procesar varias imágenes en una sola ejecución?**  
Claro. Envuelve la lógica central en un bucle `foreach (var file in Directory.GetFiles(...))` y reasigna `ocrEngine.Image` en cada iteración.

**¿Cómo manejo otros idiomas junto con el coreano?**  
Aspose.OCR permite establecer `Language = Language.AutoDetect` o combinar idiomas con el operador OR a nivel de bits (p. ej., `Language.Korean | Language.English`).

**¿Qué hago si la confianza del OCR es baja?**  
Inspecciona `detailedResult.Pages[0].Words` y filtra las entradas con `Confidence < 0.7`. También puedes ajustar los filtros de preprocesamiento—prueba añadiendo `PreprocessFilter.ContrastEnhancement`.

## Conclusión

Acabas de ver cómo realizar **OCR de idioma coreano** de extremo a extremo, desde **cargar imagen desde un stream** hasta **extraer texto plano**, luego **convertir imagen a PDF** y finalmente **exportar PDF buscable**. El enfoque es modular, por lo que puedes cambiar la fuente de la imagen, modificar el formato de salida o conectar el JSON a cualquier canal posterior.

¿Qué sigue?

## Tutoriales relacionados

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}