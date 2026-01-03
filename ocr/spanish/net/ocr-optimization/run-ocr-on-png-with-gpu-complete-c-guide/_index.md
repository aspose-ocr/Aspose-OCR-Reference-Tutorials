---
category: general
date: 2026-01-02
description: Ejecute OCR en PNG rápidamente usando Aspose OCR y soporte GPU. Aprenda
  cómo reconocer texto de una imagen, extraer texto de una imagen y establecer el
  límite de memoria GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: es
og_description: Ejecute OCR en PNG de manera eficiente aprovechando Aspose OCR y la
  aceleración GPU. Este tutorial le muestra cómo reconocer texto a partir de una imagen,
  extraer texto de una imagen y controlar el uso de memoria de la GPU.
og_title: Ejecuta OCR en PNG con GPU – Guía completa de C#
tags:
- OCR
- C#
- GPU
title: Ejecuta OCR en PNG con GPU – Guía completa de C#
url: /es/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en PNG con GPU – Guía completa en C#

¿Alguna vez necesitaste **ejecutar OCR en PNG** pero te sentiste atrapado por el rendimiento? No eres el único. En muchas canalizaciones del mundo real, un solo PNG de alta resolución puede limitar un motor OCR solo de CPU, convirtiendo lo que debería ser una búsqueda rápida en una espera de varios minutos.  

La buena noticia es que Aspose OCR incluye extensiones GPU que te permiten **reconocer texto de imagen** en una fracción del tiempo. En este tutorial recorreremos un ejemplo práctico que muestra exactamente cómo **ejecutar OCR en PNG** usando C#, cómo **extraer texto de imagen**, e incluso cómo **establecer el límite de memoria GPU** para que te mantengas dentro del presupuesto de hardware.

También cubriremos el “cómo” y el “por qué” detrás de cada paso, de modo que salgas con un modelo mental sólido, no solo con un fragmento de código para copiar‑pegar.

## Qué aprenderás

- Los requisitos previos para usar el soporte GPU de Aspose OCR.  
- Cómo cargar un PNG en un `Bitmap` y pasarlo al motor OCR.  
- Cómo configurar `GpuDevice` y `GpuMemoryLimitMb` para un rendimiento óptimo.  
- Cómo **reconocer texto de imagen** y obtener el resultado en texto plano.  
- Consejos para manejar casos comunes como GPUs con poca memoria o PNGs multipágina.  

Al final de esta guía podrás **ejecutar OCR en PNG** a velocidad GPU y controlar con confianza la huella de memoria de tus trabajos OCR.

![Diagrama que muestra ejecutar OCR en PNG con aceleración GPU](run-ocr-on-png-diagram.png "ejemplo de ejecutar OCR en PNG")

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

1. .NET 6.0 o posterior (el código funciona también con .NET Core y .NET Framework).  
2. Una GPU NVIDIA con soporte CUDA (el ejemplo selecciona el dispositivo con índice 0).  
3. El paquete NuGet Aspose.OCR y sus extensiones GPU (`Aspose.OCR.Extensions`).  
4. Un PNG de ejemplo (`input.png`) colocado en una carpeta que puedas referenciar desde tu proyecto.  

Si alguno de estos te resulta desconocido, no te preocupes; indicaremos alternativas cuando sea pertinente.

---

## Paso 1 – Instalar Aspose OCR y Extensiones GPU

Lo primero. Sin las bibliotecas correctas el resto del código no compilará.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

El paquete `Aspose.OCR.Extensions` incluye los binarios nativos CUDA necesarios para la aceleración GPU.  
*Consejo:* Si trabajas en una máquina sin GPU, aún puedes compilar el proyecto; simplemente establece `PreferGpu = false` más adelante.

---

## Paso 2 – Cargar el PNG que deseas procesar

Ahora realmente **ejecutamos OCR en PNG** cargándolo en un `Bitmap`. Este paso es sencillo pero vale la pena una breve nota: `Bitmap` espera una ruta de archivo, así que asegúrate de que la ruta sea correcta respecto a tu ejecutable.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Si el PNG es inusualmente grande (por ejemplo, > 5000 px de lado), podrías querer reducirlo primero para evitar agotar la memoria GPU. Ahí es donde la opción **establecer límite de memoria GPU** resulta útil más adelante.

---

## Paso 3 – Crear y Configurar el Motor OCR para Uso GPU

Este es el corazón del tutorial: configurar el motor OCR para **reconocer texto de imagen** usando la GPU. Dos propiedades son clave:

- `GpuDevice` – selecciona qué dispositivo CUDA usar.  
- `GpuMemoryLimitMb` – limita la cantidad de memoria GPU que el motor puede asignar.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**¿Por qué establecer un límite de memoria?** Algunas GPUs comparten memoria con la pantalla o ejecutan múltiples cargas de trabajo simultáneamente. Al limitar la asignación evitas fallos por falta de memoria, especialmente al procesar muchos PNGs en paralelo.

---

## Paso 4 – Definir Opciones de Reconocimiento (Idioma y Preferencia GPU)

El objeto `RecognitionOptions` indica al motor qué idioma buscar y si **preferir GPU** incluso para imágenes pequeñas. Para la mayoría de documentos en inglés esto es suficiente, pero puedes cambiar `Language.English` por otras configuraciones locales soportadas.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Si alguna vez necesitas **extraer texto de imagen** en un idioma distinto al inglés, simplemente cambia el enum `Language`. La biblioteca soporta docenas de idiomas de forma nativa.

---

## Paso 5 – Ejecutar el OCR y Obtener el Resultado

Con todo conectado, la llamada final es una sola línea que realmente **ejecuta OCR en PNG** y devuelve un objeto de resultado rico.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

El `OcrResult` contiene no solo el texto plano (`ocrResult.Text`) sino también puntuaciones de confianza, cuadros delimitadores e incluso la imagen original con palabras resaltadas—útil si necesitas depurar o visualizar la extracción.

**Salida esperada** (para un PNG de ejemplo que dice “Hello World”):

```
=== OCR Output ===
Hello World
```

Si el texto aparece distorsionado, verifica que el PNG no esté corrupto y que el límite de memoria GPU no sea demasiado bajo para el tamaño de la imagen.

---

## Paso 6 – Manejo de Casos Especiales y Buenas Prácticas

### GPUs con poca memoria

Si ves una excepción como `CudaException: out of memory`, reduce `GpuMemoryLimitMb` o divide el PNG en mosaicos antes de procesarlo. El mosaico se puede crear con `Graphics.DrawImage` sobre una copia del `Bitmap`.

### Múltiples PNGs en lote

Al procesar una carpeta de PNGs, reutiliza la misma instancia de `OcrEngine`; inicializarla una sola vez ahorra cambios de contexto GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Reversión a CPU

Si no hay GPU disponible, simplemente establece `PreferGpu = false`. El motor cambiará automáticamente a CPU sin necesidad de modificar el código.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Ejemplo completo

A continuación tienes el programa completo que puedes copiar‑pegar en un nuevo proyecto de consola. Incluye todos los pasos anteriores, más algunas comprobaciones de seguridad.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Guarda el archivo como `Program.cs`, ejecuta `dotnet run` y deberías ver el texto extraído impreso en la consola.

---

## Conclusión

Acabamos de demostrar cómo **ejecutar OCR en PNG** usando las extensiones GPU de Aspose OCR, cómo **reconocer texto de imagen** y cómo **extraer texto de imagen** mientras controlas el **establecer límite de memoria GPU**. Configurando `GpuDevice` y `GpuMemoryLimitMb` mantienes tu aplicación rápida y estable, incluso en GPUs modestos.

A partir de aquí podrías:

- Experimentar con otros idiomas (`Language.French`, `Language.Spanish`).  
- Integrar el paso OCR en una canalización de procesamiento de documentos más grande.  
- Añadir post‑procesamiento como corrección ortográfica o extracción de entidades para pulir el texto bruto.  

Recuerda, la clave no es solo el código sino entender por qué cada configuración importa. Cuando sabes cómo **establecer límite de memoria GPU** y cuándo volver a CPU, crearás soluciones OCR que escalan con elegancia.

¿Tienes preguntas sobre un tamaño PNG específico, TIFFs multipágina o errores de GPU? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}