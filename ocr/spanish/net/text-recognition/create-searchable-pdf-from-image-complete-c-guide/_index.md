---
category: general
date: 2026-03-23
description: Crea PDF buscable a partir de una imagen usando Aspose OCR. Aprende cómo
  convertir TIFF a PDF con alta compresión y reconocer el texto de la imagen en minutos.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: es
og_description: Crea PDF buscable a partir de una imagen con Aspose OCR. Este tutorial
  muestra cómo convertir TIFF a PDF, agregar una capa de texto buscable y aplicar
  alta compresión.
og_title: Crear PDF buscable a partir de una imagen – Guía completa de C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Crear PDF buscable a partir de una imagen – Guía completa de C#
url: /es/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable a partir de una imagen – Guía completa en C#

¿Alguna vez necesitaste **create searchable pdf** a partir de un documento escaneado pero no estabas seguro de por dónde comenzar? No eres el único—muchos desarrolladores se topan con el mismo obstáculo al convertir escaneos TIFF en PDFs buscables. ¿La buena noticia? Con Aspose OCR puedes **convert tiff to pdf**, añadir una capa de texto oculta encima, e incluso reducir el tamaño del archivo con opciones de **high compression pdf**, todo con unas pocas líneas de C#.

En este tutorial recorreremos todo el proceso: desde instalar los paquetes NuGet correctos, cargar una imagen TIFF, reconocer su texto y, finalmente, exportar un PDF buscable. Al final tendrás una aplicación de consola ejecutable que **recognize image text** y produce un PDF compacto y buscable listo para indexar. Sin herramientas extra, sin pasos manuales de OCR—solo código limpio y una breve explicación.

## Requisitos previos y lo que necesitarás

- **.NET 6+** (o .NET Framework 4.6+). La API funciona en ambos, pero .NET 6 te brinda las últimas mejoras del runtime.  
- **Visual Studio 2022** o cualquier IDE que prefieras.  
- Paquetes NuGet **Aspose.OCR** y **Aspose.OCR.Gpu** (el paquete GPU es opcional pero acelera el reconocimiento en hardware compatible).  
- Un archivo TIFF de ejemplo (p. ej., `invoice.tif`) colocado en una carpeta que controles.  

Si ya tienes estos elementos, genial—continúa. Si no, el paso de instalación a continuación cubrirá todo.

## Paso 1: Instalar paquetes Aspose OCR

Para comenzar, abre la carpeta de tu proyecto en una terminal y ejecuta:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Estos comandos descargan tanto el motor OCR central como la biblioteca de aceleración GPU. Esta última no es obligatoria; el motor volverá al modo CPU si no encuentra una GPU compatible.

> **Consejo profesional:** Al apuntar a un entorno de producción, bloquea las versiones de los paquetes en tu `csproj` para evitar cambios inesperados que rompan la funcionalidad.

## Paso 2: Configurar la estructura del proyecto

Crea una nueva aplicación de consola (si aún no tienes una):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Sustituye el `Program.cs` autogenerado por el código completo que se muestra más adelante. El programa:

1. Inicializará un `OcrEngine` con soporte GPU.  
2. Cargará la imagen TIFF.  
3. Ejecutará OCR y abortará de forma elegante en caso de fallo.  
4. Configurará **PdfExportOptions** para una capa buscable y **high compression**.  
5. Escribirá el archivo de salida.

## Paso 3: Escribir el código completo (Ejemplo completo)

A continuación está el archivo fuente *completo*. Copia‑y‑pega en `Program.cs`. Los comentarios explican el “por qué” detrás de cada línea, no solo el “qué”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Por qué funciona esto

- **GPU acceleration** puede reducir el tiempo de reconocimiento de segundos a milisegundos en tarjetas modernas—útil para procesamiento por lotes.  
- **IncludeTextLayer** incrusta el texto derivado del OCR de forma invisible, permitiendo que los visores de PDF busquen en el documento sin alterar su apariencia visual.  
- **High compression** utiliza compresión Flate (ZIP) en el flujo de la imagen, lo cual es sin pérdida pero reduce drásticamente el tamaño del archivo—ideal para archivar miles de facturas.

## Paso 4: Ejecutar la aplicación y verificar la salida

Abre una terminal dentro de la carpeta del proyecto y ejecuta:

```bash
dotnet run
```

Si todo está configurado correctamente, verás:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Abre `invoice.pdf` en cualquier lector de PDF (Adobe Acrobat, Edge o incluso un navegador). Intenta buscar una palabra que sepas que aparece en el TIFF original—p. ej., “Total”. El visor debería resaltar la palabra aunque forme parte de la imagen. Eso es la característica distintiva de un **searchable pdf**.

### Tamaño de archivo esperado

Una factura escaneada típica (≈300 KB TIFF) suele reducirse a **~80 KB** después de aplicar `PdfCompression.High`. El tamaño exacto depende de la complejidad de la imagen, pero notarás una reducción clara.

## Paso 5: Variaciones comunes y casos límite

| Situación | Qué ajustar | Por qué |
|-----------|-------------|--------|
| **No GPU available** | Cambia `new OcrEngine(GpuMode.Enabled)` a `new OcrEngine(GpuMode.Disabled)` | Evita que el motor intente inicializar la GPU, lo que puede causar una breve demora. |
| **Multiple pages (multi‑page TIFF)** | Establece `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Carga todos los fotogramas; Aspose procesará cada página y generará un PDF multipágina. |
| **Need OCR language other than English** | `ocrEngine.Language = Language.French;` (u otro idioma soportado) | Mejora la precisión para documentos que no están en inglés. |
| **Want a visible text overlay instead of hidden layer** | `pdfExportOptions.IncludeTextLayer = false;` y agrega manualmente objetos `TextFragment`. | Útil cuando deseas que el texto OCR aparezca como texto seleccionable sobre la imagen. |
| **Ultra‑small PDFs** | Combina `PdfCompression.High` con `ImageResolution = 150` DPI antes del reconocimiento. | Un DPI más bajo reduce los datos de la imagen, reduciendo aún más el PDF a costa de la fidelidad visual. |

> **Nota:** Siempre prueba los casos límite con una muestra pequeña antes de escalar a producción. La precisión del OCR puede variar según la calidad de la imagen, el ruido y el idioma.

## Paso 6: Consejos para implementaciones listas para producción

1. **Error Logging** – Reemplaza `Console.WriteLine` con un framework de registro adecuado (Serilog, NLog) para diagnósticos más fáciles.  
2. **Batch Processing** – Envuelve la lógica principal en un método que acepte rutas de entrada/salida, y luego itera sobre un directorio de archivos TIFF.  
3. **Async I/O** – Aunque Aspose OCR es sincrónico, la carga y guardado de archivos pueden ser asíncronos para mantener los hilos de UI responsivos.  
4. **Security** – Si expones esta funcionalidad a través de una API web, valida las rutas de archivo y limita los tamaños de archivo para prevenir abusos.  
5. **Version Pinning** – Usa números de versión exactos (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) para garantizar un comportamiento consistente entre compilaciones.

## Conclusión

Hemos creado una **complete, end‑to‑end solution** que **create searchable pdf** a partir de imágenes escaneadas, **convert tiff to pdf**, y lo hace con configuraciones de **high compression pdf** mientras **recognize image text** con precisión. El **searchable pdf from image** resultante es ligero, buscable y listo para flujos de trabajo posteriores como indexación, archivado o e‑discovery.

¿Tienes un lote de facturas? Inserta el método en un bucle, apunta a una carpeta y deja que Aspose OCR haga el trabajo pesado. ¿Quieres experimentar con diferentes niveles de compresión o paquetes de idioma? El código es lo suficientemente modular para cambiar esas opciones en segundos.

---

*¿Listo para subir de nivel?* Prueba añadiendo una marca de agua, incrustando metadatos, o incluso combinando varios PDFs procesados con OCR. La suite Aspose ofrece muchas extensiones—explora la documentación y mantén el impulso. ¡Feliz codificación!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}