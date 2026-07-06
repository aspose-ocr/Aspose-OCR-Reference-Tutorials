---
category: general
date: 2026-04-01
description: How to convert OCR output to JSON and XML in C# – learn to extract text
  from image and write JSON file C# using Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: en
og_description: How to convert OCR results into structured JSON and XML files with
  C#. Step‑by‑step guide to extract text from image and write JSON file C#.
og_title: How to Convert OCR to JSON & XML in C# – Write JSON File
tags:
- OCR
- C#
- Aspose
title: How to Convert OCR to JSON & XML in C# – Write JSON File
url: /net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Convert OCR to JSON & XML in C# – Write JSON File

**How to convert OCR** results into something you can actually use is a question many developers ask. In this guide we’ll show you how to extract text from an image, turn that OCR output into nicely formatted JSON and XML, and then write those files to disk with C#.

If you’ve ever stared at a raw OCR string and thought, “There’s got to be a better way to store this,” you’re in the right place. By the end you’ll have a complete, runnable program that not only **extracts text from image** files but also knows how to **write JSON file C#** and **write XML file C#** without breaking a sweat.

## What You’ll Need

- **.NET 6.0** or later (the code works with .NET Framework 4.6+ as well).  
- **Aspose.OCR** NuGet package – install it with `dotnet add package Aspose.OCR`.  
- An image containing text (e.g., `invoice.png`).  
- Any IDE you like – Visual Studio, Rider, or VS Code will do.

> **Pro tip:** Keep your image files in a dedicated folder (e.g., `Resources/`) so the paths stay tidy.

## Step 1: Set Up the OCR Engine – How to Convert OCR

First, we create an `OcrEngine` instance and tell it which language to look for. In most cases English is enough, but you can swap `Language.English` for any supported language.

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

> **Why this matters:** Initialising the engine with the correct language dramatically improves accuracy, especially for non‑Latin scripts.

## Step 2: Recognise Text – Extract Text from Image

Now we feed the image to the engine. The `Recognize` method returns an `OcrResult` object that contains the raw text as well as location data.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

If the image can’t be found, `Recognize` throws a `FileNotFoundException`. To keep the demo simple we’ll assume the path is correct, but in production you’d want to wrap this in a try‑catch block.

## Step 3: Convert the Result to JSON – Write JSON File C#

Aspose.OCR makes serialization a breeze. The `ToJson` method accepts an `indent` flag to produce pretty‑printed output, which is perfect when you plan to open the file in a text editor.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Expected JSON Sample

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

> **How to extract text**: The `Text` property gives you the plain string you can feed into other services (search indexes, databases, etc.).

## Step 4: Persist the JSON – Write JSON File C# (Continued)

With the JSON string ready, we simply write it to a file using `File.WriteAllText`. This ensures UTF‑8 encoding by default.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Now you have a `invoice.json` sitting next to your image, ready for downstream processing.

## Step 5: Convert the Result to XML – Write XML File C#

If you prefer XML for legacy systems, the `ToXml` method does the heavy lifting. Like `ToJson`, it also supports pretty‑printing.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Expected XML Sample

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

## Step 6: Persist the XML – Write XML File C# (Continued)

Saving the XML is identical to the JSON step; just point to a `.xml` extension.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Full Working Example

Putting it all together, here’s the complete program you can copy‑paste into a console app:

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

Run the program, and you’ll find two new files—`invoice.json` and `invoice.xml`—right where you specified. Open them to verify the structure matches the samples above.

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if the image contains multiple languages?** | Create separate `OcrEngine` instances for each language or use `Language.Multi` if supported. |
| **Can I control the output format (e.g., exclude region data)?** | Yes. Both `ToJson` and `ToXml` accept optional parameters to filter fields; check the Aspose.OCR docs for `ExportOptions`. |
| **How do I handle large PDFs with many pages?** | Process each page individually, aggregate the results, then serialize once. |
| **Is the output UTF‑8 safe?** | Absolutely—Aspose.OCR uses Unicode internally, and `File.WriteAllText` writes UTF‑8 by default. |
| **What about performance?** | OCR is CPU‑intensive. For batch jobs consider parallelising across cores or using Aspose’s cloud API. |

## Conclusion

You now know **how to convert OCR** results into both JSON and XML using C#. By following the steps above you can **extract text from image**, then **write JSON file C#** and **write XML file C#** with just a handful of lines. This approach is fast, reliable, and works with any image type that Aspose.OCR supports.

Ready for the next challenge? Try feeding the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}