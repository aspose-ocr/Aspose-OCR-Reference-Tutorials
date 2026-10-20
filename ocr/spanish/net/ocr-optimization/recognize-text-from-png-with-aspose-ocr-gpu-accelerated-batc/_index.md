---
category: general
date: 2026-04-01
description: Aprende a reconocer texto de archivos PNG rápidamente configurando el
  ID del dispositivo GPU y habilitando la aceleración GPU en Aspose OCR. Guía paso
  a paso en C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: es
og_description: Reconoce texto de archivos PNG rápidamente configurando el ID del
  dispositivo GPU. Sigue esta guía completa de C# para habilitar la aceleración GPU
  con Aspose OCR.
og_title: reconocer texto de png – tutorial de OCR Aspose acelerado por GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: reconocer texto de png con Aspose OCR – demostración por lotes acelerada por
  GPU
url: /es/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconocer texto de png – Tutorial completo por lotes con GPU‑Accelerated en C#

¿Alguna vez necesitaste **recognize text from png** en imágenes pero encontraste el proceso dolorosamente lento? No estás solo. La mayoría de los desarrolladores comienzan con una llamada simple a OCR, y luego observan una consola que avanza como una babosa cuando una carpeta contiene docenas de capturas de pantalla.  

¿La buena noticia? Aspose OCR puede delegar el trabajo pesado a tu tarjeta gráfica, y con solo un par de líneas puedes **set gpu device id** para elegir la GPU exacta que deseas. En esta guía recorreremos un ejemplo completo y ejecutable que extrae cada PNG de una carpeta, activa la aceleración GPU, selecciona la primera GPU y muestra el recuento de caracteres de cada archivo.

Al final tendrás un programa autónomo que podrás insertar en cualquier proyecto .NET, y comprenderás por qué habilitar la GPU es importante, cómo manejar casos límite y qué ajustar para obtener un rendimiento aún mejor.

## Lo que necesitarás

- **.NET 6.0** o posterior (el código también se compila con .NET Core).  
- El paquete **Aspose.OCR** de NuGet – instálalo con `dotnet add package Aspose.OCR`.  
- Una máquina con una GPU compatible con CUDA (NVIDIA es la típica) y el controlador adecuado.  
- Una carpeta llena de imágenes **PNG** que deseas procesar.  

Si alguno de estos te resulta desconocido, no te alarmes. Los pasos a continuación incluyen los comandos exactos que necesitas, y también discutiremos qué hacer cuando no haya una GPU disponible.

## Paso 1: Inicializar el motor OCR y habilitar la aceleración GPU  

Lo primero que debes hacer es crear una instancia de `OcrEngine` y activar el soporte GPU. Esta bandera indica a Aspose que use las bibliotecas nativas CUDA bajo el capó.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Por qué es importante:** Sin `UseGpuAcceleration`, cada imagen se procesa en la CPU, lo que puede ser órdenes de magnitud más lento, especialmente para PNG de alta resolución. Habilitar la bandera también prepara al motor para aceptar un dispositivo GPU específico más adelante.

## Paso 2: Establecer el ID del dispositivo GPU (Opcional pero recomendado)  

Si tu estación de trabajo tiene más de una GPU, puedes decidir cuál usar. Los IDs de dispositivo comienzan en **0**, por lo que `0` elige la primera GPU, `1` la segunda, y así sucesivamente.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Consejo profesional:** Al ejecutar en un servidor compartido, establecer explícitamente el ID del dispositivo GPU puede evitar que tu tarea robe recursos de otros procesos. Si omites esta línea, Aspose seleccionará el dispositivo predeterminado, lo cual suele estar bien para una configuración de una sola GPU.

## Paso 3: Recopilar todos los archivos PNG de tu carpeta por lotes  

A continuación necesitamos localizar cada PNG en el que deseas ejecutar OCR. El método `Directory.GetFiles` hace el trabajo pesado.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Caso límite:** Si la carpeta está vacía, `imageFiles` será un arreglo vacío. Lo manejaremos más adelante con un mensaje amigable.

## Paso 4: Procesar cada imagen y mostrar el recuento de caracteres reconocidos  

Ahora el bucle principal. Para cada PNG llamamos a `Recognize`, luego imprimimos el nombre del archivo y la longitud del texto extraído.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Lo que verás:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Si una imagen no contiene texto, el recuento será `0`. Eso es perfectamente normal para capturas de pantalla que son puramente gráficas.

## Paso 5: Ejecutar el programa y verificar el uso de la GPU  

Compila el archivo (`dotnet build`) y ejecútalo (`dotnet run`). Mientras la consola se desplaza, puedes abrir tu herramienta de monitoreo de GPU (como NVIDIA Smi) para ver el pico de utilización de la GPU brevemente por cada imagen. Si no ves ninguna actividad, verifica lo siguiente:

1. El controlador CUDA está instalado.  
2. `UseGpuAcceleration` está configurado en `true`.  
3. El `GpuDeviceId` correcto coincide con una GPU física.

Si la GPU no está disponible, Aspose volverá automáticamente a la CPU, pero perderás la ventaja de velocidad.

## Variaciones comunes y consejos  

| Situación | Qué cambiar |
|-----------|-------------|
| **Different image format** (e.g., JPEG) | Cambia el patrón de búsqueda a `*.jpg` o `*.*` y Aspose seguirá reconociendo el texto. |
| **Batch size is huge** (thousands of files) | Procesa en fragmentos para evitar presión de memoria: divide `imageFiles` en arreglos más pequeños. |
| **Need the actual text, not just length** | Reemplaza `ocrResult.Text.Length` por `ocrResult.Text` en el `WriteLine`. |
| **Running on a headless server** | Asegúrate de que el servidor tenga un controlador GPU; de lo contrario, establece `UseGpuAcceleration = false` para evitar errores innecesarios. |
| **Multiple GPUs, want to balance load** | Recorre `ocrEngine.GpuDeviceId = i % gpuCount` dentro del `foreach` para rotar los dispositivos. |

## Salida esperada y verificación  

Cuando todo funciona, la consola imprime cada nombre de archivo seguido del recuento de caracteres, como se mostró antes. Para verificar nuevamente la salida OCR real, puedes volcar temporalmente el texto:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Solo recuerda eliminar o comentar esa línea para lotes grandes; imprimir miles de líneas puede saturar tu terminal.

## Ejemplo completo funcional (listo para copiar y pegar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Guarda esto como `GpuBatchDemo.cs`, ejecuta `dotnet add package Aspose.OCR`, luego `dotnet run`. Deberías ver los recuentos de caracteres aparecer casi instantáneamente para cada PNG, gracias a la aceleración GPU.

## Conclusión  

Ahora sabes cómo **recognize text from png** archivos de manera eficiente habilitando la aceleración GPU y estableciendo explícitamente **set gpu device id** en Aspose OCR. El programa completo, listo para copiar y pegar, maneja el descubrimiento de carpetas, verifica casos límite y te brinda retroalimentación inmediata sobre el rendimiento del OCR.  

¿Próximos pasos? Prueba cambiar la llamada `Recognize` por `ocrEngine.RecognizeAsync` si necesitas procesamiento no bloqueante, o experimenta con diferentes opciones de preprocesamiento de imágenes (p. ej., binarización) que Aspose ofrece. También podrías canalizar los resultados OCR a una base de datos o a un índice de búsqueda para una solución de búsqueda de texto completo.  

¿Tienes preguntas sobre el manejo de PDFs multipágina, o quieres comparar Aspose OCR con Tesseract? Deja un comentario o explora nuestros otros tutoriales sobre **batch OCR C#**, **OCR performance tips**, y **GPU‑driven image processing**. ¡Feliz codificación!  

![Salida de consola mostrando recuentos de caracteres reconocidos para archivos PNG – reconocer texto de png usando aceleración GPU](image-placeholder.png "ejemplo de salida de reconocer texto de png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}