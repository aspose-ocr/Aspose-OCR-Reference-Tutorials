---
category: general
date: 2026-04-01
description: Cómo convertir la salida de OCR a JSON y XML en C# – aprende a extraer
  texto de una imagen y a escribir un archivo JSON en C# usando Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: es
og_description: Cómo convertir los resultados de OCR en archivos JSON y XML estructurados
  con C#. Guía paso a paso para extraer texto de una imagen y escribir un archivo
  JSON en C#.
og_title: Cómo convertir OCR a JSON y XML en C# – Escribir archivo JSON
tags:
- OCR
- C#
- Aspose
title: Cómo convertir OCR a JSON y XML en C# – Escribir archivo JSON
url: /es/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo convertir OCR a JSON y XML en C# – Escribir archivo JSON

**Cómo convertir OCR** a algo que realmente puedas usar es una pregunta que muchos desarrolladores se hacen. En esta guía te mostraremos cómo extraer texto de una imagen, convertir ese resultado de OCR en JSON y XML con formato agradable, y luego escribir esos archivos en disco con C#.

Si alguna vez has mirado una cadena cruda de OCR y pensado: “Tiene que haber una forma mejor de almacenar esto”, estás en el lugar correcto. Al final tendrás un programa completo y ejecutable que no solo **extrae texto de archivos de imagen**, sino que también sabe **escribir archivo JSON C#** y **escribir archivo XML C#** sin sudar.

## Lo que necesitarás

- **.NET 6.0** o posterior (el código también funciona con .NET Framework 4.6+).  
- Paquete NuGet **Aspose.OCR** – instálalo con `dotnet add package Aspose.OCR`.  
- Una imagen que contenga texto (p. ej., `invoice.png`).  
- Cualquier IDE que prefieras – Visual Studio, Rider o VS Code sirven.

> **Consejo profesional:** Mantén tus archivos de imagen en una carpeta dedicada (p. ej., `Resources/`) para que las rutas queden ordenadas.

## Paso 1: Configurar el motor OCR – Cómo convertir OCR

Primero, creamos una instancia de `OcrEngine` y le indicamos qué idioma buscar. En la mayoría de los casos el inglés es suficiente, pero puedes sustituir `Language.English` por cualquier idioma soportado.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Por qué importa:** Inicializar el motor con el idioma correcto mejora drásticamente la precisión, especialmente para escrituras no latinas.

## Paso 2: Reconocer texto – Extraer texto de la imagen

Ahora alimentamos la imagen al motor. El método `Recognize` devuelve un objeto `OcrResult` que contiene el texto bruto así como los datos de ubicación.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Si la imagen no se encuentra, `Recognize` lanza una `FileNotFoundException`. Para mantener la demo simple asumiremos que la ruta es correcta, pero en producción querrías envolver esto en un bloque try‑catch.

## Paso 3: Convertir el resultado a JSON – Escribir archivo JSON C#

Aspose.OCR hace que la serialización sea muy fácil. El método `ToJson` acepta una bandera `indent` para producir una salida con formato legible, lo cual es perfecto cuando planeas abrir el archivo en un editor de texto.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Muestra de JSON esperado

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Cómo extraer texto:** La propiedad `Text` te brinda la cadena plana que puedes pasar a otros servicios (índices de búsqueda, bases de datos, etc.).

## Paso 4: Persistir el JSON – Escribir archivo JSON C# (Continuación)

Con la cadena JSON lista, simplemente la escribimos en un archivo usando `File.WriteAllText`. Esto garantiza codificación UTF‑8 por defecto.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Ahora tienes un `invoice.json` junto a tu imagen, listo para el procesamiento posterior.

## Paso 5: Convertir el resultado a XML – Escribir archivo XML C#

Si prefieres XML para sistemas heredados, el método `ToXml` hace el trabajo pesado. Al igual que `ToJson`, también soporta el formato legible.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Muestra de XML esperado

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Paso 6: Persistir el XML – Escribir archivo XML C# (Continuación)

Guardar el XML es idéntico al paso del JSON; solo apunta a una extensión `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Ejemplo completo y funcional

Juntando todo, aquí tienes el programa completo que puedes copiar y pegar en una aplicación de consola:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Ejecuta el programa y encontrarás dos archivos nuevos —`invoice.json` y `invoice.xml`— justo donde los especificaste. Ábrelos para verificar que la estructura coincide con los ejemplos anteriores.

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si la imagen contiene varios idiomas?** | Crea instancias separadas de `OcrEngine` para cada idioma o usa `Language.Multi` si está soportado. |
| **¿Puedo controlar el formato de salida (p. ej., excluir datos de región)?** | Sí. Tanto `ToJson` como `ToXml` aceptan parámetros opcionales para filtrar campos; revisa la documentación de Aspose.OCR para `ExportOptions`. |
| **¿Cómo manejo PDFs grandes con muchas páginas?** | Procesa cada página individualmente, agrega los resultados y luego serializa una sola vez. |
| **¿La salida es segura en UTF‑8?** | Absolutamente—Aspose.OCR usa Unicode internamente, y `File.WriteAllText` escribe en UTF‑8 por defecto. |
| **¿Qué hay del rendimiento?** | OCR es intensivo en CPU. Para trabajos por lotes considera paralelizar entre núcleos o usar la API cloud de Aspose. |

## Conclusión

Ahora sabes **cómo convertir OCR** a JSON y XML usando C#. Siguiendo los pasos anteriores puedes **extraer texto de imagen**, luego **escribir archivo JSON C#** y **escribir archivo XML C#** con solo unas cuantas líneas. Este enfoque es rápido, fiable y funciona con cualquier tipo de imagen que Aspose.OCR soporte.

¿Listo para el próximo desafío? Prueba alimentando el

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}