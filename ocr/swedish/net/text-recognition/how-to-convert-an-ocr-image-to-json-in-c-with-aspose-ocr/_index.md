---
category: general
date: 2026-09-06
description: ocr‑bild till json‑konvertering i C# med Aspose.OCR – steg‑för‑steg‑guide
  för att extrahera text från bild och få JSON‑utdata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: sv
lastmod: 2026-09-06
og_description: ocr-bild till json i C# med Aspose.OCR. Lär dig hur du laddar en bild
  för OCR, känner igen text från ett foto och konverterar resultatet till JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Konvertera en OCR-bild till JSON i C# – komplett Aspose.OCR-guide
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Hur man konverterar en OCR-bild till JSON i C# med Aspose.OCR
url: /sv/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man konverterar en OCR-bild till JSON i C# med Aspose.OCR

Om du behöver **ocr image to json** i en .NET-applikation visar den här guiden hur du gör det med Aspose.OCR. Vi går igenom hur du laddar en bild för OCR, känner igen text från ett foto och konverterar resultatet till JSON så att du kan använda data i API:er eller databaser.

Att extrahera text från bildfiler är ett vanligt krav för fakturabehandling, kvittoskanning och arkiveringsprojekt. I slutet av den här tutorialen kommer du att kunna **convert image to text**, hämta resultatet som ren text och generera en strukturerad JSON‑payload som bevarar layoutinformation.

## Förutsättningar

- .NET 6.0 SDK eller senare installerat  
- Visual Studio 2022 (eller någon editor som stödjer .NET)  
- Ett Aspose.OCR NuGet‑paket (`Aspose.OCR`) tillagt i ditt projekt  
- En exempelbild (`input.jpg`) placerad i en mapp som du kan referera till från kod  

Du behöver inga ytterligare OCR‑motorer; Aspose.OCR sköter det tunga arbetet internt.

## Steg 1: Installera Aspose.OCR NuGet‑paketet

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Paketet innehåller klassen `Aspose.OCR.OcrEngine`, som tillhandahåller metoder för **load image for ocr**, språkval och export av resultat.

## Steg 2: Skapa ett nytt C#‑konsolprojekt

Om du ännu inte har ett projekt, skapa ett:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Lägg till de `using`‑direktiv som du kommer att behöva:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Steg 3: Ladda bilden och konfigurera OCR‑motorn

Följande kod visar hur du **load image for ocr**, ställer in språket och förbereder motorn för bearbetning. I det här exemplet använder vi kyrilliska, men du kan byta till `OcrLanguage.English`, `OcrLanguage.French` osv., beroende på källspråket.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Varför detta är viktigt:** Att ställa in rätt språk förbättrar avsevärt noggrannheten när du **recognize text from photo**. Motorn använder språk‑specifika ordböcker och teckenuppsättningar.

## Steg 4: Kör OCR‑processen och hämta resultat

Kör nu OCR‑motorn. Om processen lyckas kan du **extract text from image** som ren text, HTML eller JSON. Aspose.OCR tillhandahåller en `SaveJson`‑metod som skriver det strukturerade resultatet till en fil.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Förväntad JSON‑struktur

En typisk `output.json`‑fil ser ut så här (formaterad för läsbarhet):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

JSON‑payloaden innehåller varje rads text, ett förtroendescore och rektangeln som omger raden i det ursprungliga fotot. Detta gör det enkelt att mappa OCR‑resultatet tillbaka till UI‑element eller databasfält.

## Steg 5: Fullständig källkod för demonstrationen

Nedan är det kompletta, färdiga programmet som utför **ocr image to json**‑arbetsflödet. Kopiera det till `Program.cs` och kör `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Köra exemplet

1. Placera en bild med namnet `input.jpg` i projektets rot.  
2. Kör `dotnet run`.  
3. Observera konsolutdata och öppna `output.json` för att se den strukturerade datan.

## Pro‑tips och vanliga fallgropar

| Situation | Recommendation |
|-----------|----------------|
| **Låglösta foton** | Öka DPI innan bearbetning eller använd `ocrEngine.Image = ImageStream.FromFile(path, 300)` för att tvinga 300 DPI. |
| **Blandade språk** | Ställ in `ocrEngine.Language = OcrLanguage.Multilingual` och ange eventuellt en språklista via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Stora dokument** | Bearbeta en sida i taget för att hålla minnesanvändningen låg; motorn stödjer flersidiga TIFF‑filer. |
| **Felaktiga tecken** | Verifiera att rätt `OcrLanguage` är vald; att använda fel språk minskar noggrannheten när du **convert image to text**. |
| **JSON saknar fält** | Se till att du använder Aspose.OCR version 23.6 eller senare; äldre versioner exponerade inte `SaveJson`‑metoden. |

## Vanliga frågor

**Q: Kan jag få OCR‑resultatet som en byte‑array istället för en fil?**  
A: Ja. Använd `ocrEngine.SaveJson(Stream)` för att skriva direkt till en `MemoryStream`, och anropa sedan `stream.ToArray()`.

**Q: Stöder motorn PDF‑inmatning?**  
A: Aspose.OCR kan ta emot PDF‑sidor konverterade till bilder via Aspose.PDF, men OCR‑motorn själv arbetar på rasterbilder. Konvertera PDF‑filer till bilder först, och sedan **load image for ocr**.

**Q: Hur hanterar jag skript som skrivs från höger till vänster, som arabiska?**  
A: Ställ in `ocrEngine.Language = OcrLanguage.Arabic`. JSON‑filen innehåller korrekt textriktning, vilket du kan rendera i UI‑ramverk som stödjer RTL.

## Slutsats

Du har nu en komplett lösning för **ocr image to json** i C#. Genom att ladda en bild, konfigurera språket, köra OCR‑motorn och exportera resultatet som JSON kan du **extract text from image**, **convert image to text** och **recognize text from photo** i ett enda, strömlinjeformat arbetsflöde.  

Härifrån kan du utforska:

- Integrera JSON‑utdata med ett Web‑API (`ASP.NET Core`)  
- Lagra resultatet i en NoSQL‑databas som MongoDB  
- Lägga till efterbehandling för att korrigera vanliga OCR‑fel  

Känn dig fri att experimentera med olika språk, bildformat och utdataalternativ för att passa ditt projekts behov. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [känna igen text från bild i C# – Komplett guide till OCR och JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Konvertera bild till text i C# med Aspose OCR – Steg‑för‑steg‑guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Hur man extraherar text från bild med Aspose.OCR för .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}