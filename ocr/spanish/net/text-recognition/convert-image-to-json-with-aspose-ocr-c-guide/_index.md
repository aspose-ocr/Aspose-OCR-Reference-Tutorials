---
category: general
date: 2026-01-15
description: Convertir imagen a JSON usando Aspose OCR en C#. Aprende cómo extraer
  texto de la imagen, obtener los cuadros delimitadores en JSON y reconocer la imagen
  de un recibo.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: es
og_description: Convertir imagen a JSON usando Aspose OCR en C#. Guía paso a paso
  para extraer texto de la imagen, reconocer imágenes de recibos y obtener los cuadros
  delimitadores en JSON.
og_title: Convertir imagen a JSON con la guía de Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Convertir imagen a JSON con la guía de Aspose OCR C#
url: /es/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir Imagen a JSON con Aspose OCR C# Guía

¿Alguna vez necesitaste **convertir imagen a JSON** pero no estabas seguro de qué biblioteca podría proporcionarte tanto el texto sin procesar como las coordenadas exactas de cada palabra? No estás solo. Muchos desarrolladores se topan con este obstáculo cuando intentan extraer texto de archivos de imagen—especialmente recibos—y al mismo tiempo necesitan una carga útil JSON legible por máquinas para el procesamiento posterior.

En este tutorial recorreremos un **ejemplo completo de Aspose OCR C#** que muestra cómo extraer texto de una imagen, reconocer una imagen de recibo y generar **cajas delimitadoras JSON** para cada palabra. Al final tendrás una aplicación de consola lista para ejecutar que imprime una cadena JSON bien formateada que puedes enviar a cualquier API, base de datos o canal de análisis.

> **Lo que obtendrás**  
> • Un proyecto C# completamente funcional que **convierte imagen a JSON**  
> • Entendimiento de por qué habilitamos `IncludeBoundingBoxes` (es la clave para `json bounding boxes`)  
> • Consejos para manejar diferentes formatos de imagen y lenguajes  

¡Vamos a comenzar!

---

## Qué Necesitarás

Antes de sumergirnos en el código, asegúrate de tener instalados los siguientes requisitos:

- **.NET 6.0 SDK** (o cualquier versión posterior) – el código está dirigido a .NET 6 pero también funciona en .NET Framework 4.7+ .  
- **Aspose.OCR for .NET** paquete NuGet – puedes obtenerlo con `dotnet add package Aspose.OCR`.  
- Una imagen de muestra de recibo (`receipt.jpg`) colocada en una carpeta a la que puedas referenciar desde tu proyecto.  
- Visual Studio 2022, VS Code, o cualquier IDE que prefieras.

No se requieren otros servicios externos; todo se ejecuta localmente.

---

## Convertir Imagen a JSON – Visión General

La idea central es simple: cargar una imagen, indicar a Aspose OCR que reconozca inglés (o cualquier idioma soportado), solicitar que incluya cajas delimitadoras y, finalmente, pedir el resultado en formato **JSON**. La biblioteca se encarga de todo el trabajo pesado—OCR, análisis de diseño y serialización a JSON.

Aquí tienes un diagrama de alto nivel del flujo (imagina una pequeña ilustración):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Ese pequeño diagrama captura todo el pipeline que implementaremos.

---

## Paso 1: Configurar el Proyecto e Instalar Aspose OCR

Primero, crea un nuevo proyecto de consola e incorpora el paquete Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Consejo profesional:** Si usas Visual Studio, haz clic derecho en el proyecto → *Manage NuGet Packages* → busca **Aspose.OCR** e instala la versión estable más reciente (actualmente 23.12).

---

## Paso 2: Cargar la Imagen que Deseas Reconocer

Usaremos el método `OcrImage.FromFile` para leer la imagen del recibo. Asegúrate de que la ruta apunte a un archivo real; de lo contrario obtendrás una `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Si tu imagen está junto al `.csproj`, puedes simplemente usar `"receipt.jpg"`.

---

## Paso 3: Configurar Opciones OCR para Cajas Delimitadoras JSON

La magia ocurre cuando habilitamos `OutputFormat = OutputFormat.Json` **y** `IncludeBoundingBoxes = true`. El primero indica a Aspose que serialice el resultado como JSON, mientras que el segundo agrega `x`, `y`, `width` y `height` para cada palabra—exactamente lo que necesitas para `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

También puedes ajustar `ocrOptions.Dpi` o `ocrOptions.Language` si necesitas mayor resolución o un idioma diferente.

---

## Paso 4: Realizar el Reconocimiento – Extraer Texto de la Imagen

Ahora llamamos a `Recognize`. El método devuelve un objeto `OcrResult` que contiene la cadena JSON, el texto sin procesar y más.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Si necesitas manejar otros idiomas, reemplaza `Language.English` por `Language.Spanish`, `Language.French`, etc. Aspose soporta más de 30 idiomas de forma nativa.

---

## Paso 5: Mostrar el Resultado – Tu Carga Útil JSON

Finalmente, imprimimos el JSON en la consola. En una aplicación real probablemente lo escribirías en un archivo o lo enviarías a un servicio.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Ejecutar el programa debería producir un documento JSON similar al fragmento a continuación.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Observa cómo cada palabra ahora lleva su **caja delimitadora JSON**—perfecta para alimentar una superposición UI o un parser posterior.

---

## Ejemplo Completo Funcional

A continuación tienes el programa completo, listo para copiar y pegar. Sin partes ocultas, sin llamadas externas—solo C# puro.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Cosas a vigilar:**  
> • **Errores de ruta de archivo** – verifica la ubicación de la imagen.  
> • **Paquete NuGet faltante** – asegura que `Aspose.OCR` esté referenciado.  
> • **Formatos de imagen no soportados** – utiliza JPEG, PNG, BMP o TIFF para obtener los mejores resultados.

---

## Preguntas Frecuentes y Casos Especiales

### ¿Puedo convertir una **página PDF** a JSON en lugar de un JPEG?

Sí. Convierte primero la página PDF a una imagen (por ejemplo, usando `Aspose.PDF`), luego alimenta esa imagen al mismo pipeline OCR. La salida JSON será idéntica porque el paso OCR solo necesita datos rasterizados.

### ¿Qué pasa si el recibo está borroso?

Aumenta el DPI en `ocrOptions`. Por ejemplo:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Un DPI mayor puede incrementar el uso de memoria, así que equilibra calidad y rendimiento.

### Necesito **múltiples idiomas** en el mismo recibo (p. ej., inglés + español).

Puedes pasar un arreglo de idiomas:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose intentará reconocer cada idioma en el orden especificado.

### ¿Cómo escribo el JSON en un archivo?

Simplemente reemplaza la línea `Console.WriteLine` con:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Así tendrás un archivo persistente que puedes enviar a otros servicios.

---

## Resumen Visual

![convert image to json example](convert-image-to-json.png "convert image to json example")

*La captura muestra la salida de consola del payload JSON después de ejecutar la demostración.*

---

## Conclusión

Acabamos de mostrarte cómo **convertir imagen a JSON** usando Aspose OCR en C#. Configurando `OutputFormat` y `IncludeBoundingBoxes`, puedes **extraer texto de la imagen**, **reconocer la imagen del recibo** y obtener **cajas delimitadoras JSON** precisas para cada palabra. El código completo y ejecutable está en el fragmento anterior, por lo que puedes insertarlo en cualquier proyecto .NET ahora mismo.

¿Qué sigue? Prueba a alimentar el JSON a un visor front‑end que resalte cada palabra, o envía los datos a un modelo de machine‑learning que clasifique los ítems de un recibo. También puedes experimentar con otros idiomas, configuraciones de DPI más altas o procesamiento por lotes de múltiples imágenes en un bucle.

Si encuentras algún problema, recuerda los consejos sobre rutas de archivo, DPI y arreglos de idiomas. No dudes en dejar un comentario o abrir un issue en el repositorio GitHub que crees para esta demo. ¡Feliz codificación y disfruta convirtiendo imágenes en JSON estructurado!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}