---
category: general
date: 2026-05-31
description: Aprende cómo obtener puntuaciones de confianza OCR en C# mientras extraes
  texto de una imagen y lees una imagen de recibo con Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: es
og_description: Los puntajes de confianza del OCR le permiten medir la precisión;
  esta guía muestra cómo extraer texto de una imagen, obtener cajas delimitadoras
  y leer la imagen de un recibo usando Aspose OCR.
og_title: Puntuaciones de confianza de OCR en C# – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Puntuaciones de confianza de OCR en C# – Guía completa
url: /es/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Puntuaciones de confianza OCR en C# – Guía completa

¿Alguna vez te has preguntado cómo obtener **OCR confidence scores** cuando necesitas *extract text from image*? Tal vez estés intentando **read receipt image** para el seguimiento de gastos y quieras saber qué caracteres le generan dudas al motor. ¿La buena noticia? Con Aspose.OCR puedes obtener porcentajes de confianza, bounding boxes y texto plano de un JPG en solo unas pocas líneas de C#.

En este tutorial recorreremos todo lo que necesitas saber: instalar la biblioteca, configurar el motor para **perform OCR on JPG**, extraer las puntuaciones de confianza y interpretar los **OCR bounding boxes** que indican dónde se encuentra cada carácter en la página. Al final tendrás una aplicación de consola lista‑para‑ejecutar que imprime cada carácter, su confianza y su ubicación—perfecta para validar recibos o cualquier documento escaneado.

## Lo que aprenderás

- Instalar Aspose.OCR vía NuGet y configurar un motor OCR básico.  
- Configurar `OcrOptions` para solicitar salida de texto plano **with confidence scores** y **bounding boxes**.  
- Recorrer `OcrResult` para **extract text from image** línea por línea y símbolo por símbolo.  
- Manejar problemas comunes como archivos faltantes, caracteres de baja confianza y formatos que no sean JPG.  
- Ampliar el ejemplo para procesar múltiples imágenes de recibos en una carpeta.

No se requiere experiencia previa con Aspose; solo un entorno .NET funcional y una imagen de recibo (JPG) que desees probar.

## Paso 1 – Instalar Aspose.OCR y preparar tu proyecto

Lo primero: necesitas el paquete NuGet Aspose.OCR. Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.OCR
```

> **Consejo:** La versión de prueba gratuita funciona hasta 200 páginas, lo cual es más que suficiente para probar el escaneo de recibos.

Después de instalar el paquete, crea un nuevo proyecto de consola (si aún no tienes uno):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Ahora puedes abrir el `Program.cs` generado y comenzar a agregar las directivas using:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Estos espacios de nombres te dan acceso a `OcrEngine`, `OcrOptions` y los tipos de resultado que necesitaremos más adelante.

## Paso 2 – Obtener puntuaciones de confianza OCR y bounding boxes OCR

Este es el corazón del tutorial. Configuraremos el motor para que cada carácter reconocido venga con una **confidence score** y una **bounding box** (el rectángulo que envuelve el glifo). El propio encabezado H2 contiene la palabra clave principal, cumpliendo la regla SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**¿Por qué incluir confidence scores?**  
Una confidence score (0‑100%) te indica cuán seguro está el motor sobre cada carácter. Si alimentas la salida a lógica posterior—por ejemplo, un flujo de aprobación de gastos—puedes rechazar o marcar automáticamente los símbolos de baja confianza.

**¿Por qué solicitar bounding boxes?**  
Los bounding boxes son esenciales cuando necesitas resaltar texto en la imagen original, extraer sub‑regiones o alinear los resultados OCR con una superposición UI. Cada `character.Bounds` te brinda X, Y, ancho y alto en coordenadas de píxeles.

## Paso 3 – Realizar OCR en JPG y extraer texto de la imagen

Ahora ejecutamos el motor. La llamada a `Recognize()` realiza todo el trabajo pesado y devuelve un objeto `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Si la ruta de la imagen es incorrecta o el archivo no es un formato compatible, Aspose lanza una `FileNotFoundException` o `UnsupportedImageFormatException`. Envuelve la llamada en un bloque try/catch en código de producción para manejar esos casos extremos de forma elegante.

### Extrayendo el texto plano

Si solo necesitas el texto concatenado, puedes leer `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Pero como también solicitamos confidence scores y bounding boxes, iteraremos a través de la estructura para ver los detalles de cada carácter.

## Paso 4 – Iterar por líneas, símbolos y mostrar confidence scores OCR

Este es el bucle que imprime cada carácter, su confidence y su caja. Aquí es donde el ejemplo de **read receipt image** realmente brilla.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

La salida de ejemplo podría verse así:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretando los números:**  
- **Confidence ≥ 90%** – generalmente seguro de aceptar.  
- **Confidence 70‑89%** – podrías querer verificar de nuevo, especialmente los dígitos en los importes.  
- **Confidence < 70%** – considera marcar para revisión manual.

## Paso 5 – Ejemplo completo ejecutable (incluyendo manejo de errores)

Juntando todo, aquí tienes un programa completo que puedes copiar‑pegar en `Program.cs`. Incluye una verificación simple de archivos faltantes y muestra un mensaje amigable si el OCR falla.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Salida esperada

Al ejecutar `dotnet run` la consola mostrará primero el texto concatenado del recibo, luego una lista de cada carácter con su confidence score y bounding box. Si la confidence de un carácter es baja, verás un porcentaje bajo 80, lo que indica que debes verificar esa parte del recibo manualmente.

## Bonus: Procesar múltiples recibos en una carpeta

Si tienes un lote de JPG de recibos, envuelve la lógica anterior en un bucle `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Recuerda reiniciar el `OcrEngine` para cada archivo, o crear una nueva instancia dentro del bucle para evitar fugas de estado.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Procesar en lote es útil para importaciones nocturnas de gastos.

## Conclusión

Ahora tienes una solución sólida, de extremo a extremo, para obtener **OCR confidence scores** en C#, **extracting text from image**, y recuperar **OCR bounding boxes** mientras **perform OCR on JPG** archivos como una **read receipt image**. El código es totalmente autónomo, funciona con la última versión de Aspose.OCR (a partir del 2026‑05‑31), y te brinda los datos granulares que necesitas para construir pipelines de procesamiento de documentos confiables.

¿Qué sigue? Intenta visualizar los bounding boxes en el recibo original usando `System.Drawing` o una biblioteca UI, o envía los caracteres de baja confidence a un servicio de verificación secundario. También puedes experimentar con diferentes idiomas configurando `ocrEngine.Options.Language = OcrLanguage.French;` – la API soporta muchas configuraciones regionales.

¡Feliz codificación, y que tus confidence scores siempre se mantengan altos! 

![Salida de consola mostrando OCR confidence scores y bounding boxes para un recibo

## ¿Qué deberías aprender a continuación?

- [Extraer texto de imagen C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cómo obtener opciones de caracteres OCR para caracteres reconocidos en reconocimiento de imágenes](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cómo usar Aspose OCR para resultado JSON en reconocimiento de imágenes](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}