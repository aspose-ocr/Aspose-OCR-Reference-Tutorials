---
category: general
date: 2026-03-15
description: Cómo usar Aspose OCR para extraer texto de imágenes y convertir la imagen
  a JSON en C#. Aprende a reconocer texto de PNG y obtener una salida estructurada
  rápidamente.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: es
og_description: Cómo usar Aspose OCR para extraer texto de imágenes y convertir la
  imagen a JSON en C#. Esta guía le muestra cómo reconocer texto de PNG y obtener
  una salida estructurada.
og_title: Cómo usar Aspose OCR para convertir una imagen a JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Cómo usar Aspose OCR para convertir una imagen a JSON
url: /es/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar Aspose OCR para convertir una imagen a JSON

Cómo usar Aspose OCR es una pregunta frecuente cuando los desarrolladores necesitan extraer texto de imágenes. Si buscas **convertir imagen a JSON** o **reconocer texto de PNG**, esta guía te cubre—sin rodeos, solo una solución práctica de extremo a extremo.

En los próximos minutos repasaremos todo lo que necesitas: instalar la biblioteca, configurar el motor para salida JSON, cargar un PNG de recibo, ejecutar OCR y, finalmente, escribir el resultado en un archivo `.json`. Al final podrás **extraer texto de imagen** con una sola llamada a método, y comprenderás por qué cada paso es importante.

> **Consejo profesional:** Aspose OCR funciona con una amplia gama de formatos de imagen (PNG, JPEG, BMP, TIFF). El mismo código a continuación los manejará a todos, así que no tendrás que escribir lógica específica para cada formato.

## Lo que necesitarás

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.6+).  
- Un paquete NuGet válido de Aspose.OCR (prueba gratuita o con licencia).  
- Un archivo de imagen que deseas procesar (p.ej., `receipt.png`).  
- Visual Studio, VS Code o cualquier editor de C# que prefieras.  

¡Eso es todo—sin dependencias extra, sin servicios externos! ¿Listo? Vamos a sumergirnos.

![cómo usar el motor OCR de aspose](image-placeholder.png "cómo usar el motor OCR de aspose")

## Cómo usar Aspose OCR – Configurar salida JSON

Lo primero que debes hacer cuando **cómo usar aspose** para OCR es crear una instancia de `OcrEngine` y decirle que emita JSON. Este pequeño interruptor de configuración te ahorra tener que serializar manualmente el resultado más tarde.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Por qué es importante:** Establecer `OutputFormat` a `Json` significa que el motor OCR ya estructura el texto en una jerarquía de páginas, líneas y palabras. No necesitas analizar cadenas crudas después, lo que hace que el procesamiento posterior—como alimentar datos a una base de datos—sea mucho más limpio.

## Convertir imagen a JSON con Aspose OCR

Ahora que el motor está configurado, hablemos con más detalle de la parte **convertir imagen a JSON**.

1. **Cargar la imagen** – `Image.FromFile` funciona para cualquier formato compatible. Si trabajas con un flujo (p.ej., un archivo subido), puedes usar `Image.FromStream` en su lugar.  
2. **Ejecutar `Recognize`** – este método devuelve un objeto `OcrResult`. Como configuramos la salida a JSON, `ocrResult.Text` ya contiene una cadena JSON.  
3. **Escribir el archivo** – `File.WriteAllText` es la forma más sencilla de persistir el JSON. Si necesitas almacenarlo en un bucket en la nube, simplemente sustituye esta línea por la llamada adecuada del SDK.

### Salida JSON esperada

Una carga JSON típica se ve así (recortada por brevedad):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Ahora puedes alimentar esta estructura a cualquier sistema posterior—ya sea una herramienta de informes, un modelo de aprendizaje automático o un simple archivo de registro.

## Extraer texto de una imagen usando Aspose OCR

Si solo necesitas la cadena cruda (es decir, no te importa el JSON), simplemente cambia el formato de salida a texto plano:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**¿Cuándo elegir texto plano?**  
- Depuración rápida o salida en consola.  
- Escenarios donde aplicarás post‑procesamiento personalizado (p.ej., extracción con expresiones regulares).  

Pero recuerda, **extraer texto de imagen** usando JSON te brinda datos posicionales—útiles para resaltar texto en una UI o alinear con campos de formulario.

## Reconocer texto de archivos PNG

PNG es un formato sin pérdida, lo que a menudo produce mejor precisión OCR comparado con JPEGs fuertemente comprimidos. Aquí tienes una lista de verificación rápida para asegurar los mejores resultados cuando **reconoces texto de PNG**:

| Elemento de la lista | Por qué ayuda |
|----------------------|---------------|
| Usar un DPI de 300+ | Mayor resolución brinda al motor más píxeles con los que trabajar. |
| Mantener la imagen en escala de grises | Reduce el ruido; Aspose OCR convierte automáticamente, pero el preprocesamiento puede acelerar el proceso. |
| Eliminar el desorden del fondo | Fondos limpios mejoran las puntuaciones de confianza. |

Si encuentras puntuaciones de confianza bajas, intenta aumentar el DPI o aplicar un filtro de umbral simple antes de pasar la imagen a Aspose.

## Cómo extraer resultados OCR programáticamente

Más allá de simplemente guardar el JSON, quizá quieras leer programáticamente campos específicos—por ejemplo, el total de un recibo. Como el JSON contiene una jerarquía, puedes deserializarlo a un objeto C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Ahora puedes consultar `ocrData` con LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Por qué funciona:** El JSON ya indica dónde vive cada palabra en la página, por lo que puedes localizar campos de forma fiable aunque el diseño cambie ligeramente.

## Casos límite y errores comunes

- **Resultado nulo:** Si `ocrEngine.Recognize` devuelve `null`, la imagen podría no ser compatible o estar corrupta. Siempre protege contra ello:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Archivos grandes:** Para imágenes de varios megabytes, considera transmitir la imagen o redimensionarla antes del OCR para evitar un uso excesivo de memoria.

- **Problemas de licencia:** La versión de prueba agrega una marca de agua al resultado. Asegúrate de cargar tu licencia al inicio del programa:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Scripts no latinos:** Aspose OCR soporta muchos idiomas, pero debes establecer la propiedad `Language` según corresponda (p.ej., `ocrEngine.Configuration.Language = Language.English;`).

## Ejemplo completo (listo para copiar y pegar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}