---
category: general
date: 2026-01-10
description: Aprende a reconocer texto a partir de una imagen, extraer las coordenadas
  del texto y convertir un recibo a JSON usando Aspose OCR en C#. Tutorial paso a
  paso.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: es
og_description: Reconocer texto de una imagen en C# usando Aspose OCR. Esta guía muestra
  cómo extraer texto, obtener coordenadas y convertir el recibo a JSON.
og_title: reconocer texto de imagen – Tutorial completo de OCR en C#
tags:
- OCR
- C#
- Aspose
title: reconocer texto de una imagen en C# – Guía completa de OCR y JSON
url: /es/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconocer texto de imagen – Tutorial completo de OCR en C#

¿Alguna vez necesitaste reconocer texto de una imagen pero no estabas seguro de qué biblioteca elegir? No estás solo. En muchas aplicaciones del mundo real—seguidores de gastos, escáneres de recibos o archivadores de documentos—extraer texto de manera fiable es el primer obstáculo.  

En este tutorial recorreremos **cómo extraer texto**, obtendremos sus cajas delimitadoras y, finalmente, **convertir recibo a JSON** usando Aspose.OCR para .NET. Al final tendrás un proyecto C# autónomo que toma una foto de un recibo y genera un archivo JSON ordenado con puntuaciones de confianza y coordenadas.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener lo siguiente en tu máquina:

- **.NET 6.0 SDK** (o cualquier versión posterior). Los frameworks más antiguos también funcionan, pero .NET 6 es el punto óptimo para bibliotecas modernas.
- **Visual Studio 2022** o VS Code con la extensión C#.
- Paquete NuGet **Aspose.OCR for .NET** (`Aspose.OCR` y `Aspose.OCR.Output`). Puedes instalarlo a través de la consola del Administrador de paquetes:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Una imagen de recibo de muestra (p. ej., `receipt.jpg`) colocada en una carpeta que referenciarás más adelante.

Eso es todo—sin SDKs adicionales, sin binarios nativos, solo código administrado puro.

## Paso 1: Crear un nuevo proyecto de consola

Primero lo primero, crea una aplicación de consola. Es la forma más rápida de probar OCR sin la sobrecarga de una interfaz de usuario.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Consejo profesional:** Mantén la carpeta del proyecto ordenada; crea una subcarpeta llamada `Resources` y coloca `receipt.jpg` allí. Facilita el manejo de rutas.

## Paso 2: Cargar la imagen del recibo

Ahora realmente **reconocemos texto de la imagen**. El primer paso es apuntar el motor OCR al archivo.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

¿Por qué envolvemos la carga en una simple verificación de existencia? Porque en producción a menudo manejas cargas de usuarios que pueden estar ausentes o corruptas. Detectar el problema temprano te ahorra excepciones crípticas más adelante.

## Paso 3: Realizar OCR – **reconocer texto de la imagen**

Con la imagen en memoria, le pedimos a Aspose que **reconozca texto de la imagen**. Esta operación es sincrónica y devuelve un conjunto de resultados completo.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Detrás de escena, Aspose ejecuta una red neuronal entrenada con millones de caracteres. El motor llena `ocrEngine.Text`, `ocrEngine.RecognitionResult` y una colección de objetos `OcrRegion` que contienen coordenadas. Eso es exactamente lo que necesitamos para el siguiente paso.

## Paso 4: **Cómo extraer texto** – Obtener la cadena cruda

Si solo te importa el texto plano (quizá para una búsqueda rápida), puedes obtenerlo directamente del motor:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Notarás saltos de línea donde el OCR detectó límites de párrafo. En muchos escenarios de escaneo de recibos, la cadena cruda es suficiente para extraer totales, fechas o nombres de proveedores usando expresiones regulares simples.

## Paso 5: **extraer coordenadas de texto** – Cajas delimitadoras para cada palabra

A menudo necesitas saber *dónde* en la imagen se encuentra un fragmento de texto en particular—por ejemplo, para resaltar el importe total en una interfaz. Aspose nos brinda eso a través de objetos `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Observa que estamos iterando sobre **extraer coordenadas de texto** para cada segmento reconocido. Las coordenadas son relativas a la imagen original, por lo que puedes superponerlas en un lienzo gráfico o en un elemento HTML `<canvas>`.

## Paso 6: **convertir recibo a JSON** – Guardar resultados detallados

Ahora llega la parte que une todo: queremos una estructura legible por máquinas que incluya el texto, las puntuaciones de confianza y las cajas delimitadoras. Aspose incluye `JsonSaveOptions` que hacen esto muy sencillo.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

El archivo resultante se ve algo así (recortado por brevedad):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Ahora tienes un artefacto de **convertir recibo a JSON** que puede alimentarse a servicios posteriores—piensa en APIs de informes de gastos, canalizaciones de análisis o incluso una interfaz simple que dibuja rectángulos alrededor de cada palabra.

## Ejemplo completo en funcionamiento

Uniendo todas las piezas, aquí tienes el `Program.cs` completo que puedes copiar y pegar en tu proyecto:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Ejecuta el programa (`dotnet run`) y observa la salida de la consola. Abre `Resources/receipt.json` para verificar la estructura.

## Preguntas comunes y casos límite

- **¿Qué pasa si la imagen está borrosa?**  
  Aspose OCR funciona mejor con 300 dpi o más. Si obtienes puntuaciones de confianza bajas, considera aplicar un filtro de enfoque antes de pasar la imagen al motor.

- **¿Puedo reconocer varios idiomas?**  
  Sí. Configura `ocrEngine.Language = Language.English | Language.Spanish;` antes de llamar a `Recognize()`.

- **¿Cómo limito la salida solo a números (p. ej., totales)?**  
  Después de obtener el texto plano, ejecuta una expresión regular como `\d+\.\d{2}` sobre `ocrEngine.Text`. Como ya tenemos coordenadas, puedes mapear la cadena coincidente a su región para resaltado visual.

- **¿Es personalizable el formato JSON?**  
  La clase `JsonSaveOptions` expone un conjunto de banderas. Si necesitas un esquema completamente personalizado, puedes iterar sobre `ocrEngine.RecognitionResult.Regions` y serializar los objetos tú mismo con `System.Text.Json`.

## Conclusión

Acabamos de demostrar cómo **reconocer texto de una imagen** en C# usando Aspose.OCR, **cómo extraer texto**, obtener **extraer coordenadas de texto**, y finalmente **convertir recibo a JSON**. Todo el flujo vive en una única aplicación de consola fácil de ejecutar, lo que la hace perfecta para prototipos o como bloque de construcción en sistemas más grandes.

¿Próximos pasos? Intenta alimentar el JSON a un front‑end que dibuje las cajas delimitadoras, o conecta la salida a un servicio de informes de gastos. También puedes experimentar con diferentes formatos de imagen (PNG, TIFF) o procesar por lotes una carpeta de recibos.

¿Tienes más preguntas sobre OCR, Aspose o el manejo de JSON? Deja un comentario abajo, ¡y feliz codificación! 

![Ejemplo de imagen de recibo para reconocer texto de la imagen](receipt.jpg "Ejemplo de imagen de recibo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}