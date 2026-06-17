---
category: general
date: 2026-02-20
description: Aprende a leer recibos en C# extrayendo texto de una imagen y convirtiéndolo
  a JSON. Código paso a paso usando Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: es
og_description: Descubre cómo leer recibos en C# cargando un archivo de imagen, extrayendo
  texto con Aspose OCR y convirtiendo el resultado a JSON. Ejemplo de código completo.
og_title: Cómo leer recibos en C# – Extraer texto, convertir a JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Cómo leer recibos en C# – Guía completa para extraer texto de una imagen
url: /es/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo leer recibos en C# – Guía completa

¿Alguna vez te has preguntado **cómo leer recibos** de forma programática? Tal vez estés creando una aplicación de seguimiento de gastos y necesites extraer los ítems de una foto de un recibo de supermercado. En mi experiencia, el mayor dolor es convertir ese JPEG borroso en datos estructurados que realmente puedas usar. ¿La buena noticia? Con unas pocas líneas de C# y Aspose OCR puedes **extraer texto de la imagen**, luego **convertir la imagen a JSON** de una manera que parece casi mágica.

En este tutorial obtendrás una solución lista‑para‑ejecutar que **carga un archivo de imagen C#**, ejecuta OCR y genera una carga JSON detallada. Sin servicios externos, sin llamadas REST complicadas—solo código .NET puro que puedes insertar en cualquier proyecto de consola o ASP.NET. Al final entenderás por qué cada paso es importante, cómo manejar casos límite comunes (como tamaños de recibo no estándar) y cómo se ve realmente la salida JSON.

## Lo que necesitarás

- **.NET 6.0 o posterior** – el código usa `System.Drawing.Common`, que es compatible con Windows, Linux y macOS.  
- **Aspose.OCR para .NET** – puedes obtener un paquete NuGet de prueba gratuita (`Aspose.OCR`) o usar una copia con licencia si ya la tienes.  
- Una **imagen de recibo de ejemplo** (`receipt.jpg`) colocada en una ubicación que tu aplicación pueda leer.  
- Cualquier IDE que prefieras (Visual Studio, Rider, VS Code).  

Eso es todo. Sin configuraciones extra, sin claves API.

---

## Paso 1 – Cargar el archivo de imagen C# (Palabra clave principal en acción)

Antes de que el motor OCR haga su magia, debes cargar la foto en memoria. Este es el paso clásico de “cargar archivo de imagen C#” que muchos desarrolladores pasan por alto.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Por qué importa:**  
`Image.FromFile` lee el archivo *una sola vez* y mantiene un manejador abierto, lo que es perfecto para una pasada rápida de OCR. Si procesas muchos recibos en un bucle, considera usar `Image.FromStream` para evitar bloquear el archivo.

> **Consejo profesional:** Si te encuentras con una *FileNotFoundException*, verifica la ruta y asegúrate de que la imagen realmente exista. Las rutas relativas también funcionan (`"./receipt.jpg"`), pero las rutas absolutas son más seguras para entornos de producción.

---

## Paso 2 – Crear y configurar el motor OCR

Aspose OCR incluye un `OcrEngine` listo para usar. No necesitas entrenar un modelo; la biblioteca ya sabe leer texto impreso, que es exactamente lo que usan la mayoría de los recibos.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Por qué establecemos estas opciones:**  
`DetectOrientation` indica al motor que rote automáticamente la imagen si el recibo fue escaneado al revés. Definir el idioma reduce el conjunto de caracteres, lo que puede mejorar la precisión—especialmente cuando solo necesitas datos alfanuméricos en inglés.

---

## Paso 3 – Reconocer la imagen y convertir a JSON

Ahora viene la parte divertida: **extraer texto de la imagen** y **convertir la imagen a JSON** en una sola llamada.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

El método `RecognizeToJson` devuelve una estructura JSON rica que incluye:

- `Text`: el texto plano concatenado.  
- `Lines`: una matriz de objetos línea con coordenadas.  
- `Words`: cada palabra con su puntuación de confianza.  
- `Regions`: cajas delimitadoras para los bloques de texto detectados.

Puedes deserializar este JSON a un objeto C# si necesitas acceso tipado, pero para muchos escenarios imprimir el JSON crudo es suficiente.

---

## Paso 4 – Mostrar el JSON (o guardarlo)

Veamos la salida y discutamos qué hacer con ella.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Salida de ejemplo

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**¿Qué hacer después?**  
Analiza la matriz `Lines` para extraer el importe del `Total`, o envía el JSON a un servicio downstream que almacene entradas de gastos. Como el resultado ya está en JSON, puedes conectarlo directamente a cualquier base de datos NoSQL, Azure Function o flujo de Power Automate.

---

## Paso 5 – Manejo de casos límite comunes

Incluso los mejores motores OCR tropiezan con algunas cosas. A continuación se presentan escenarios que podrías encontrar mientras aprendes **cómo leer recibos** en imágenes.

| Situación | Solución / Recomendación |
|-----------|--------------------------|
| **Recibo de baja resolución (≤ 150 dpi)** | Escala la imagen primero usando `Bitmap` y `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Recibo rotado o sesgado** | Mantén `DetectOrientation = true`. Para sesgos severos, pre‑procesa con `Image.RotateFlip` o una biblioteca externa como OpenCV. |
| **Fondo coloreado (p. ej., recibo sobre una mesa)** | Convierte a escala de grises y aumenta el contraste antes del OCR (`ImageAttributes`). |
| **Múltiples recibos en una foto** | Recorta cada región de recibo manualmente o usa `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Archivos grandes que provocan OutOfMemory** | Usa sentencias `using` para disponer los objetos `Image` rápidamente, o procesa en fragmentos. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Paso 6 – Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa *completo* que puedes compilar ahora mismo. Incluye todos los pasos, directivas `using` correctas y manejo de errores elegante.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Ejecutarlo:**  
`dotnet run` desde la carpeta del proyecto. Si todo está configurado correctamente verás el JSON impreso en la consola y guardado junto a tu imagen de recibo.

---

## Conclusión

Acabamos de cubrir **cómo leer recibos** en C# de principio a fin. Al cargar la imagen, configurar Aspose OCR y llamar a `RecognizeToJson`, puedes **extraer texto de la imagen** y **convertir la imagen a JSON** con prácticamente ningún código repetitivo. El enfoque escala—from a single‑receipt demo to a batch processor that handles hundreds of receipts nightly.

Próximos pasos que podrías explorar:

- **Parsear el JSON** para extraer fechas, totales e ítems (usa `System.Text.Json` o `Newtonsoft.Json`).  
- **Integrar con una base de datos** (SQL, Cosmos DB) para almacenar registros de gastos automáticamente.  
- **Agregar una UI** (WinForms, WPF o Blazor) para que los usuarios arrastren y suelten recibos.  
- **Cambiar Aspose OCR** por otro motor (Tesseract, Microsoft Azure OCR) si la licencia es un problema—simplemente mantén el mismo patrón de “cargar archivo de imagen C#”.

Siéntete libre de experimentar, romper cosas y luego volver aquí para repasar. Si encuentras algún obstáculo, la comunidad (y los foros de Aspose) son excelentes lugares para preguntar. ¡Feliz codificación y disfruta convirtiendo esos recibos de papel en datos limpios y buscables!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}