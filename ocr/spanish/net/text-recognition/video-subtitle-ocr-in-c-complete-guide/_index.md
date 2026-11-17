---
category: general
date: 2026-06-03
description: Tutorial de OCR de subtítulos de video que muestra cómo extraer fotogramas
  de un video y leer texto de archivos de video como MP4 usando Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: es
og_description: Aprende OCR de subtítulos de video con Aspose.OCR. Extrae fotogramas
  de video, lee texto del video y extrae texto de MP4 en pocos minutos.
og_title: OCR de subtítulos de video en C# – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR de subtítulos de video en C# – Guía completa
url: /es/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Guía completa de OCR de subtítulos de video en C#

¿Alguna vez necesitaste **video subtitle ocr** pero no sabías por dónde empezar? No estás solo. Ya sea que estés digitalizando grabaciones de conferencias, extrayendo subtítulos de videos de entrenamiento, o simplemente tengas curiosidad por leer texto de un video, este tutorial te muestra exactamente cómo hacerlo con C# y Aspose.OCR.  

En los próximos minutos extraeremos fotogramas del video, ejecutaremos OCR en esos fotogramas y, finalmente, mostraremos el texto de los subtítulos fotograma a fotograma. Al final podrás **leer texto de video** archivos —incluyendo MP4— sin buscar herramientas de terceros.

## Lo que construirás

Crearemos una pequeña aplicación de consola que:

1. Decodifica un MP4 (o cualquier formato compatible) en fotogramas `Bitmap` individuales.  
2. Limita la región de OCR a la banda de subtítulos para que el motor no se distraiga con toda la imagen.  
3. Procesa cada fotograma con `VideoOcrProcessor` de Aspose.  
4. Imprime el texto de subtítulos reconocido en la consola.

Sin rodeos, solo un ejemplo funcional de extremo a extremo que puedes incorporar en un proyecto real.

## Requisitos previos

- **.NET 6.0** o posterior (el código también funciona en .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – instalar vía NuGet: `Install-Package Aspose.OCR`.  
- Un archivo de video (MP4 funciona muy bien).  
- Una forma de decodificar fotogramas de video – la demo usa un método de marcador de posición, pero puedes conectar FFmpeg, OpenCV o cualquier biblioteca que devuelva objetos `Bitmap`.  

> Consejo profesional: Si estás en Windows, el paquete `System.Drawing.Common` funciona bien para `Bitmap`. En Linux/macOS necesitarás la dependencia nativa `libgdiplus`.

## Paso 1 – Extraer fotogramas del video

La primera barrera es convertir una imagen en movimiento en imágenes fijas. El método `GetVideoFrames` a continuación se deja deliberadamente vacío; reemplázalo con tu decodificador favorito. Aquí tienes un boceto rápido usando FFmpeg‑Core (solo para ilustrar la forma de los datos):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Por qué es importante:** Extraer fotogramas le brinda al motor OCR una imagen estática con la que trabajar, lo que mejora drásticamente la precisión en comparación con intentar leer directamente de una transmisión de video.

## Paso 2 – Configurar el VideoOcrProcessor

Ahora que tenemos una secuencia de objetos `Bitmap`, podemos entregarlos a Aspose.OCR. El `VideoOcrProcessor` nos permite definir una **Region of Interest (ROI)** – perfecta para subtítulos que normalmente se encuentran en la parte superior o inferior del fotograma.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **¿Por qué limitar la ROI?** Al ignorar el resto de la imagen reducimos el ruido, disminuimos el tiempo de procesamiento y evitamos falsos positivos provenientes de gráficos de fondo.

## Paso 3 – Ejecutar OCR en la secuencia de fotogramas

Con el procesador listo, alimentar los fotogramas es una sola línea. El método `Process` devuelve un enumerable de objetos `OcrResult`, cada uno con el texto reconocido para su fotograma correspondiente.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **¿Qué ocurre detrás de escena?** Aspose.OCR normaliza internamente cada bitmap, ejecuta un reconocedor basado en redes neuronales y luego post‑procesa la salida para mejorar la puntuación y los saltos de línea.

## Paso 4 – Mostrar el texto extraído

Finalmente, iteramos sobre los resultados e imprimimos cada línea de subtítulo. También podrías escribirlos en un archivo SRT, una base de datos o enviarlos a un servicio de traducción.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Ejemplo completo funcional

Al juntar todo, obtenemos un programa de consola autónomo:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Salida esperada (ejemplo)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Si el OCR tiene dificultades con un fotograma en particular, verás una cadena vacía – eso indica que debes ajustar la ROI o aumentar la tasa de extracción de fotogramas.

## Problemas comunes y cómo solucionarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Caracteres basura** | Fotogramas de baja resolución o compresión pesada | Extrae fotogramas a mayor bitrate, o aumenta la escala del bitmap antes del OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **No se devuelve texto** | La ROI no cubre realmente la banda de subtítulos | Verifica las coordenadas del rectángulo (usa una herramienta de captura de pantalla para medir). |
| **Cuello de botella de rendimiento** | Procesar cada fotograma a 30 fps es excesivo | Muestrea a 1‑2 fps para la mayoría de los flujos de subtítulos; aún puedes capturar cada cambio de subtítulo. |
| **FFmpeg no encontrado** | `ffmpeg.exe` no está en el `PATH` | Proporciona la ruta completa en `ProcessStartInfo.FileName` o instala FFmpeg globalmente. |

## Extender la solución

- **Exportar a SRT** – concatenar las marcas de tiempo con el texto OCR y escribir un archivo SubRip.  
- **Soporte multilingüe** – establecer `ocrProcessor.Language = OcrLanguage.Spanish` (o cualquier idioma compatible).  
- **Procesamiento en tiempo real** – canalizar los fotogramas directamente desde una transmisión en vivo en lugar de leer desde disco.  

Todas estas variaciones siguen girando en torno a las ideas principales de **extract frames from video**, **read text from video**, y **extract text from mp4**.

## Conclusión

Hemos recorrido un flujo de trabajo completo de **video subtitle ocr** en C#. Al extraer fotogramas del video, centrar el OCR en la banda de subtítulos e iterar sobre los resultados, puedes leer de forma fiable **read text from video** archivos como MP4. El código está listo para copiar y pegar, y el diseño modular te permite intercambiar cualquier decodificador de fotogramas que prefieras.

¿Próximos pasos? Intenta exportar los resultados a un archivo SRT, experimenta con diferentes tamaños de ROI, o envía los subtítulos a una API de traducción para subtítulos multilingües. El cielo es el límite una vez que domines los conceptos básicos de extracción de texto de video.

¡Feliz codificación, y que tus subtítulos siempre sean cristalinos!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}