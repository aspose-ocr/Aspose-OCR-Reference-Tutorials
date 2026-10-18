---
category: general
date: 2026-03-05
description: Convertir TIFF a texto en C# con Aspose OCR—extrae rápidamente texto
  de archivos de imágenes escaneadas y aprende cómo cargar un archivo de imagen en
  C# para el procesamiento OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: es
og_description: Convertir TIFF a texto en C# usando Aspose OCR. Aprende el flujo de
  trabajo completo para extraer texto de imágenes escaneadas y cargar archivos de
  imagen de manera eficiente.
og_title: Convertir TIFF a Texto en C# – Extraer Texto de Imagen Escaneada
tags:
- OCR
- C#
- Aspose
title: Convertir TIFF a Texto en C# – Extraer Texto de Imagen Escaneada
url: /es/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir TIFF a Texto en C# – Extraer Texto de Imágenes Escaneadas

¿Necesitas **convertir TIFF a texto en C#**? No eres el único luchando con imágenes escaneadas de varias páginas que se niegan obstinadamente a convertirse en cadenas buscables.  
En esta guía recorreremos una solución completa, lista‑para‑ejecutar que toma un archivo TIFF, lo envía a Aspose OCR y genera texto plano—sin servicios adicionales, sin magia oculta.

> **Consejo profesional:** Si trabajas con escaneos de alta resolución, habilitar el procesamiento GPU puede ahorrar segundos en cada página.

También te mostraremos cómo **extraer texto de imágenes escaneadas** y la mejor manera de **cargar archivo de imagen C#** en el motor OCR, para que puedas integrar esta lógica en cualquier proyecto .NET hoy.

---

## Lo que Necesitarás

Antes de profundizar, asegúrate de tener lo siguiente en tu máquina:

| Requisito | Razón |
|-------------|--------|
| .NET 6.0+ (o .NET Framework 4.7.2+) | Entorno de ejecución moderno, soporta `Span<T>` y E/S asíncrona |
| Aspose.OCR for .NET (paquete NuGet `Aspose.OCR`) | El motor OCR que utilizaremos |
| Un archivo de licencia válido de Aspose OCR (`Aspose.OCR.lic`) | Sin ella alcanzarás los límites de evaluación |
| Un archivo TIFF (de una o varias páginas) para probar | Ejemplo usado: `scanned_multi_page.tif` |
| GPU con CUDA 11+ (opcional) | Acelera el reconocimiento cuando `EngineMode = Gpu` |

Si te falta alguno de estos, obtén el paquete NuGet ahora:

```bash
dotnet add package Aspose.OCR
```

---

## Paso 1: Configurar el Proyecto e Importar Namespaces

Crea una nueva aplicación de consola (o agrega el código a un proyecto existente). Lo primero que hacemos es importar las clases que necesitaremos.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Por qué es importante:** Importar `Aspose.OCR.Image` nos brinda la fábrica `ImageStream`, que puede leer archivos TIFF directamente desde el disco o un flujo. Omitir este paso provocará un error de compilación.

---

## Paso 2: Inicializar el Motor OCR y Elegir el Modo de Procesamiento

El motor OCR debe configurarse **antes** de asignar cualquier imagen. Aquí decidimos si se ejecuta en la CPU o se aprovecha la GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Si estás en un servidor sin cabeza sin tarjeta gráfica, cambia `Gpu` a `Cpu` o `Auto`.*  
El modo del motor influye en la asignación de memoria y la velocidad; el modo GPU puede ser 2‑3× más rápido en TIFFs grandes y de alta resolución.

---

## Paso 3: Aplicar tu Licencia Aspose OCR

Ejecutar sin licencia te limita a unas pocas páginas y marcas de agua. Carga tu licencia temprano para que cada operación posterior no tenga restricciones.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Error común:** Colocar `SetLicense` después de `Recognize()` hará que el motor vuelva al modo de prueba para esa llamada.

---

## Paso 4: Cargar el Archivo TIFF – Manejo de Imágenes de una y Múltiples Páginas

Aspose OCR puede leer TIFFs de varias páginas directamente, pero necesitas proporcionar el flujo correcto. Aquí tienes un patrón robusto que funciona para ambos escenarios.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### ¿Por qué usar `ImageStream.FromFile`?

- Abstrae el `FileStream` subyacente, manejando la enumeración de páginas TIFF internamente.  
- También funciona con `MemoryStream`, por lo que puedes cargar imágenes desde una base de datos o una API web sin tocar el sistema de archivos.

### Caso límite: TIFFs muy grandes

Si tu TIFF supera los 200 MB, considera cargarlo página por página para evitar excepciones de falta de memoria:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Paso 5: Verificar la Salida

Al ejecutar el programa, deberías ver algo como:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Si el texto se ve desordenado, verifica:

1. **Resolución** – OCR funciona mejor con 300 dpi o más.  
2. **EngineMode** – Cambia a `Cpu` si el controlador GPU está desactualizado.  
3. **Licencia** – Asegúrate de que la ruta del archivo de licencia sea correcta y que el archivo sea legible.

---

## Preguntas Frecuentes (FAQ)

### ¿Funciona esto con otros formatos de imagen?

Absolutamente. `ImageStream.FromFile` soporta JPEG, PNG, BMP e incluso PDF (a través de Aspose.PDF). Simplemente reemplaza la extensión del archivo.

### ¿Qué pasa si necesito procesar imágenes almacenadas en una base de datos?

Lee el BLOB en un `MemoryStream` y pásalo a `ImageStream.FromStream(memoryStream)`. El motor OCR lo trata igual que un flujo basado en archivo.

### ¿Puedo ejecutar esto en Linux?

Sí—Aspose OCR es multiplataforma. Instala el runtime .NET apropiado y asegúrate de que las bibliotecas nativas requeridas para GPU (si se usan) estén disponibles.

---

## Ejemplo Completo Funcional (Listo para Copiar‑Pegar)

A continuación está el programa completo, listo para compilar. Reemplaza `YOUR_DIRECTORY` y la ruta del archivo de licencia con tus ubicaciones reales.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Guarda esto como `Program.cs`, ejecuta `dotnet run` y observa el texto

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}