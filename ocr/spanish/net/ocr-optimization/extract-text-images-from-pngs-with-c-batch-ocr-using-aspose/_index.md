---
category: general
date: 2026-02-09
description: Extrae texto de imágenes rápidamente con C# configurando la paralelización
  máxima para OCR por lotes – aprende a convertir páginas escaneadas, manejar OCR
  de múltiples imágenes y leer texto PNG de manera eficiente.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: es
og_description: Extraer texto de imágenes en C# estableciendo paralelismo máximo.
  Este tutorial muestra cómo convertir páginas escaneadas, ejecutar OCR en múltiples
  imágenes y leer texto PNG con Aspose OCR.
og_title: extraer texto de imágenes PNG con C# – Guía completa de OCR por lotes
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Extraer texto de imágenes PNG con C# – OCR por lotes usando Aspose OCR
url: /es/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

with shortcodes unchanged.

Then heading "# extract text images from PNGs with C# – Batch OCR using Aspose OCR" translate to Spanish: "# extraer imágenes de texto de PNGs con C# – OCR por lotes usando Aspose OCR"

Proceed.

Paragraphs.

Let's translate.

I'll produce final markdown.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraer imágenes de texto de PNGs con C# – OCR por lotes usando Aspose OCR

¿Alguna vez necesitaste **extraer imágenes de texto** de una carpeta de PNG escaneados pero te quedaste atascado en la pregunta “¿cómo lo hago rápido?”? No estás solo. En muchos proyectos del mundo real, los desarrolladores deben **establecer la paralelización máxima** para que decenas de páginas se procesen en segundos en lugar de minutos.  

En esta guía recorreremos un ejemplo completo y ejecutable que **convierte páginas escaneadas**, ejecuta **OCR de múltiples imágenes**, y finalmente **lee texto PNG** sin sudar. No hay enlaces vagos de “ver la documentación”, solo código que puedes copiar‑pegar, explicaciones de por qué cada línea importa y consejos para evitar los problemas habituales.

> **Consejo profesional:** Si ya usas Aspose OCR en otro lugar, notarás que la misma clase `OcrEngine` aparece aquí, pero ajustaremos su configuración para un procesamiento verdaderamente paralelo.

---

## Qué necesitarás

- **.NET 6+** (o .NET Framework 4.6+). La API funciona igual, pero los entornos más recientes ofrecen mejor manejo de hilos.  
- **Aspose.OCR for .NET** – instala vía NuGet: `Install-Package Aspose.OCR`.  
- Una carpeta que contenga algunos escaneos PNG (`page1.png`, `page2.png`, …).  
- Un IDE o editor con el que te sientas cómodo (Visual Studio, Rider, VS Code…).

Eso es todo. Sin servicios extra, sin claves de nube, solo procesamiento local puro.

---

## extraer imágenes de texto – Configurando la paralelización máxima para OCR por lotes

Cuando lanzas OCR sobre varios archivos, el motor, por defecto, usa un solo hilo. Eso es seguro pero terriblemente lento. Configurando `MaxDegreeOfParallelism` le indicas al motor cuántos hilos puede crear simultáneamente.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**¿Por qué 4?**  
Cuatro es un punto óptimo en la mayoría de los portátiles modernos: suficientes núcleos para mantener la CPU ocupada, pero no tantos como para asfixiar otros procesos. Si lo ejecutas en un servidor con 16 núcleos, aumenta el número a 12 o 14 para notar una mejora de velocidad.

---

## convertir páginas escaneadas – Construyendo la colección de ImageStream

Aspose espera cada imagen como un `ImageStream`. El ayudante `FromFile` lee el archivo, lo mantiene en memoria y lo entrega al motor OCR. También puedes proporcionar un `MemoryStream` si tus imágenes provienen de una base de datos o de una respuesta HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Caso límite:** Si falta algún archivo o está corrupto, `FromFile` lanzará una `FileNotFoundException`. Envuelve la construcción en un `try/catch` si esperas entradas poco fiables.

---

## OCR de múltiples imágenes – Ejecutando OCR por lotes

Ahora ocurre el trabajo pesado. `RecognizeBatch` genera hasta el número de hilos que configuraste antes, procesa cada imagen y devuelve una lista de objetos `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Detrás de escena, cada hilo carga su imagen, ejecuta la red neuronal y extrae texto plano. El orden de los resultados coincide con el orden de la lista de entrada, de modo que puedes mapear página 1 → resultado 0, y así sucesivamente.

---

## leer texto PNG – Mostrando el contenido extraído

Finalmente iteramos sobre los resultados e imprimimos el texto plano en la consola. Aquí puedes redirigir la salida a un archivo, una base de datos o incluso a un servicio de NLP posterior.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Salida esperada en la consola

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Si ves secciones en blanco, verifica que los PNG no sean imágenes completamente blancas—OCR necesita algo de contraste.

---

## Consejos prácticos y errores comunes

| Situación | Qué hacer |
|-----------|-----------|
| **Presión de memoria** en lotes grandes | Procesa las imágenes en bloques de 10‑20 archivos, luego llama a `GC.Collect()` si notas picos. |
| **Detección de idioma incorrecta** | Establece `ocrEngine.Configuration.Language = OcrLanguage.English;` (o el idioma objetivo) antes de llamar a `RecognizeBatch`. |
| **Rendimiento lento a pesar de la paralelización** | Verifica que tu SSD no esté limitando I/O; lee todos los archivos a memoria primero (como hacemos con `ImageStream.FromFile`). |
| **Faltan caracteres** | Incrementa `ocrEngine.Configuration.DPI = 300;` para un procesamiento de mayor resolución. |

---

## Extender el ejemplo – De PNG a PDF o DOCX

Si eventualmente necesitas **convertir páginas escaneadas** en PDFs buscables, simplemente pasa el mismo `ocrResults[i].PlainText` a una biblioteca PDF (p. ej., Aspose.PDF) y superpone el texto como una capa invisible. El mismo truco de paralelismo funciona allí también.

---

## Código fuente completo (listo para copiar‑pegar)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Guarda esto como `BatchExample.cs`, ejecuta `dotnet run` y observa cómo tu consola se llena con el texto que antes estaba oculto dentro de esos escaneos PNG.

---

## Resumen visual

![extract text images example](images/ocr-batch.png){alt="ejemplo de extracción de imágenes de texto"}

El diagrama muestra el flujo: **archivos PNG → colección ImageStream → OcrEngine (paralelismo máximo) → resultados OCR → Consola / almacenamiento posterior**.

---

## Conclusión

Ahora tienes una receta sólida, de extremo a extremo, para **extraer imágenes de texto** en C# mientras **configuras la paralelización máxima**, **conviertes páginas escaneadas**, manejas **OCR de múltiples imágenes** y **lees texto PNG** de manera eficiente. El código es autónomo, las explicaciones cubren tanto el “cómo” como el “por qué”, y los consejos te evitan dolores de cabeza comunes.

¿Qué sigue? Prueba cambiar la lista de PNG por un bucle dinámico `Directory.GetFiles`, experimenta con diferentes conteos de hilos, o dirige la salida a un PDF buscable. El mismo patrón escala a cientos de páginas con apenas una línea de código adicional.

¿Tienes preguntas o un caso límite complicado? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}