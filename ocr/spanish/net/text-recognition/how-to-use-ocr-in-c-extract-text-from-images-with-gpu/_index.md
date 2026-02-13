---
category: general
date: 2026-02-13
description: Aprende a usar OCR en C# para extraer texto de archivos de imagen, habilitar
  el procesamiento GPU y convertir escaneos a texto rápidamente.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: es
og_description: ¿Cómo usar OCR en C#? Esta guía te muestra cómo extraer texto de archivos
  de imagen, habilitar el procesamiento GPU y convertir escaneos a texto.
og_title: Cómo usar OCR en C# – Extraer texto de imágenes con GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Cómo usar OCR en C# – Extraer texto de imágenes con GPU
url: /es/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

many terms are English; we keep them.

Let's produce the translated content.

We need to keep the shortcodes at top and bottom unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en C# – Extraer texto de imágenes con GPU

¿Alguna vez te has preguntado **cómo usar OCR** para extraer texto de un documento escaneado sin complicaciones? No eres el único: los desarrolladores preguntan constantemente, “¿Cómo puedo extraer texto de archivos de imagen de manera eficiente?” La buena noticia es que con Aspose.OCR puedes hacer exactamente eso, e incluso **activar el procesamiento con GPU** para obtener un notable aumento de velocidad en hardware compatible.

En este tutorial recorreremos un ejemplo completo, de extremo a extremo, que muestra **cómo usar OCR**, cómo **extraer texto de una imagen**, cómo **convertir un escaneo a texto**, y qué hacer si la GPU no está disponible. Al final tendrás una aplicación de consola en C# lista para ejecutarse que imprime el texto reconocido y te indica si la GPU se utilizó realmente.

## Lo que necesitarás

- SDK .NET 6 o posterior (el código también funciona con .NET Core)  
- Visual Studio 2022 o cualquier editor que prefieras  
- Paquete Aspose.OCR para .NET (disponible vía NuGet)  
- Un archivo de imagen de alta resolución (p. ej., `highres_scan.tif`) para probar  

No se requiere una configuración complicada: solo unos pocos comandos NuGet y estarás listo.

## Paso 1: Instalar Aspose.OCR y preparar el proyecto

Lo primero es llevar la biblioteca OCR a tu proyecto. Abre una terminal en la carpeta de tu solución y ejecuta:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Esto crea un proyecto de consola nuevo llamado **OcrDemo** y agrega el paquete NuGet `Aspose.OCR`. La biblioteca contiene la clase `OcrEngine` que utilizaremos.

> **Consejo profesional:** Si trabajas en una máquina con GPU dedicada, asegúrate de que el controlador gráfico más reciente esté instalado; de lo contrario la biblioteca volverá automáticamente al modo CPU.

## Paso 2: Escribir el código OCR completo

Ahora abre `Program.cs` y reemplaza su contenido con lo siguiente. Cada línea está comentada para que puedas ver *por qué* hacemos lo que hacemos.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Por qué funciona

- **ProcessingMode = Gpu** indica al motor que intente usar la GPU primero. La biblioteca abstrae las llamadas de bajo nivel a CUDA/OpenCL, por lo que no necesitas gestionar contextos de dispositivo tú mismo.  
- **IsGpuEnabled** es un booleano que confirma si la ruta GPU tuvo éxito. Si ves `false`, el motor retrocedió a CPU automáticamente—no hay motivo de pánico.  
- **RecognizeImage** realiza todo el trabajo pesado: carga la imagen, ejecuta el modelo OCR y devuelve el resultado en texto plano. No es necesario pre‑procesar manualmente el bitmap a menos que tengas requisitos especiales (p. ej., corrección de inclinación).

## Paso 3: Ejecutar la aplicación y verificar la salida

Compila y ejecuta:

```bash
dotnet run
```

Si todo está configurado correctamente, verás algo como:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Si la GPU no está disponible, la primera línea mostrará `GPU used: False`, pero el texto extraído seguirá apareciendo—gracias al retroceso elegante.

> **Pregunta frecuente:** *¿Qué pasa si mi imagen es un JPEG en lugar de un TIFF?*  
> El método `RecognizeImage` acepta cualquier formato compatible con `System.Drawing` de .NET (JPEG, PNG, BMP, etc.). Simplemente cambia la extensión del archivo en `imagePath`.

## Paso 4: Opcional – Ajustar configuraciones para mayor precisión

Aspose.OCR ofrece algunas opciones que puedes modificar:

| Configuración | Qué hace | Cuándo usar |
|---------------|----------|-------------|
| `ocrEngine.Language` | Fuerza un idioma específico (p. ej., `OcrLanguage.English`) | Si conoces el idioma del documento |
| `ocrEngine.PageSegMode` | Controla cómo el motor divide la página en bloques | Para diseños de varias columnas |
| `ocrEngine.DetectOrientation` | Auto‑rota texto que no está vertical | Escaneos que pueden estar al revés |

Puedes establecer estas propiedades antes de llamar a `RecognizeImage`. Por ejemplo:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Paso 5: Visualizar el flujo (Imagen con texto alternativo)

A continuación se muestra un diagrama sencillo que ilustra **cómo usar OCR** con aceleración opcional de GPU. No es necesario para que el código funcione, pero ayuda a comprender el panorama general.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Texto alternativo:* *Diagrama que muestra cómo usar OCR con procesamiento GPU, resaltando el retroceso a CPU cuando es necesario.*

## Casos límite y solución de problemas

1. **Falta de memoria en GPU** – Imágenes muy grandes pueden exceder la memoria de la GPU. En ese caso, la biblioteca volverá a CPU automáticamente. Puedes pre‑escalar la imagen para mantener bajo el consumo de memoria.  
2. **Formato de imagen no compatible** – Si `RecognizeImage` lanza *NotSupportedException*, verifica la extensión del archivo y asegura que la imagen no esté corrupta. Convertir a PNG suele resolver el problema.  
3. **Bajas puntuaciones de confianza** – Cuando el resultado OCR contiene muchos caracteres ilegibles, considera pre‑procesar (binarización, eliminación de ruido) o usar un escaneo de mayor resolución.  

## Conclusión: Lo que logramos

Acabamos de cubrir **cómo usar OCR** en una aplicación de consola C#, demostramos cómo **extraer texto de archivos de imagen** y mostramos cómo **activar el procesamiento con GPU** para obtener resultados más rápidos. Ahora sabes cómo **convertir un escaneo a texto**, verificar si la GPU se utilizó realmente y ajustar algunas configuraciones para escenarios límite.

### Próximos pasos

- Prueba enviar la salida a un **índice de búsqueda** (p. ej., Elasticsearch) para que tus PDFs escaneados sean buscables.  
- Experimenta con **procesamiento por lotes**—recorre una carpeta de imágenes y escribe cada resultado en un archivo `.txt`.  
- Combina OCR con **APIs de traducción** para traducir automáticamente documentos escaneados en idiomas extranjeros.  

¿Tienes más preguntas? Deja un comentario, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}