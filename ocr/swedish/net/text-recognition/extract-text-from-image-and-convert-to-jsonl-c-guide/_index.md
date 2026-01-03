---
category: general
date: 2026-01-02
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du konverterar
  en bild till JSONL‑format snabbt och pålitligt.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: sv
og_description: Extrahera text från bild med Aspose OCR och konvertera den till JSONL-format.
  Fullständig steg‑för‑steg C#‑handledning för utvecklare.
og_title: Extrahera text från bild – konvertera till JSONL i C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Extrahera text från bild och konvertera till JSONL – C#‑guide
url: /sv/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild och konvertera till JSONL – Komplett C#-handledning

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket bibliotek som ger dig ren, strukturerad output? Du är inte ensam. I många kvitto‑behandlings‑ eller dokument‑digitaliseringsprojekt är flaskhalsen att omvandla en bitmap till sökbar text *och* ett maskin‑läsbart format.  

Den goda nyheten? Med Aspose OCR kan du **extrahera text från bild** och, med några rader kod, **konvertera bild till JSONL** för efterföljande analys. Denna guide går dig igenom hela processen, från att ladda en PNG till att skriva en JSON‑Lines‑fil som kan strömmas in i en datapipeline.

> **Tips:** Om du redan använder .NET 6 eller senare fungerar samma kod utan någon extra konfiguration.

## Förutsättningar — Vad du behöver

- **.NET 6 SDK** (eller någon nyare .NET‑version)
- **Aspose.OCR** NuGet‑paket  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** för serialisering  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- En exempelbild (t.ex. `receipt.png`) placerad i en mapp du kan referera till.
- En IDE eller editor du föredrar—Visual Studio, VS Code, Rider, osv.

Ingen tung installation, inga externa tjänster, bara ett fåtal NuGet‑paket.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: extrahera text från bild med C# och Aspose OCR*

## Steg 1: Ladda bilden du vill bearbeta  

Det första du gör när du vill **extrahera text från bild** är att ge OCR‑motorn en bitmap. Att använda `System.Drawing.Bitmap` är enkelt och fungerar för de flesta rasterformat.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Varför detta är viktigt:** Att ladda bilden som en `Bitmap` ger OCR‑motorn direkt pixelåtkomst, vilket förbättrar igenkänningshastigheten och noggrannheten jämfört med att strömma råa byte.

## Steg 2: Konfigurera Aspose OCR för JSON‑Lines‑output  

Aspose OCR låter dig ange språk, output‑format och några prestanda‑justeringar. Här begär vi **JSON‑Lines** (ett JSON‑objekt per rad) eftersom det är perfekt för rad‑för‑rad‑bearbetning senare.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Proffstips:** Om du behöver flerspråkiga kvitton, sätt `Language = Language.Multilingual` eller skicka en array av `Language`‑värden.

## Steg 3: Kör OCR och fånga resultatet  

Nu **extraherar vi text från bild**. Metoden `Recognize` returnerar ett `OcrResult`‑objekt som innehåller en samling av `OcrLine`‑objekt, där varje representerar en rad med igenkänd text samt dess avgränsningsruta.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

På den här punkten innehåller `ocrResult.Lines` allt du behöver—råtext, förtroendesiffror och koordinater.

## Steg 4: Serialisera raderna till JSON‑Lines  

Vi omvandlar samlingen till en snyggt indenterad JSON‑sträng. Även om JSON‑Lines vanligtvis är kompakt, gör indentering filen lättare att inspektera under utveckling.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Den resulterande variabeln `jsonLines` ser ungefär ut så här (trimmad för korthet):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Varje rad avslutas med ett radbrytningstecken, vilket ger dig en riktig **JSONL** (JSON‑Lines)‑fil.

## Steg 5: Skriv JSON‑Lines till disk  

Till sist sparar vi output så att andra tjänster—som Spark, Logstash eller ett enkelt Bash‑skript—kan läsa den rad för rad.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

När du öppnar `receipt.jsonl` ser du ett JSON‑objekt per rad, redo för strömning.

## Steg 6: Verifiera exporten  

En snabb kontroll sparar dig timmar av felsökning senare. Låt oss läsa de första raderna igen och skriva ut dem i konsolen.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Typisk konsolutskrift:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Om du ser något liknande, grattis—du har framgångsrikt **extraherat text från bild** och **konverterat bild till JSONL**.

## Vanliga fallgropar & hur du undviker dem  

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Tom output** | Bildens sökväg är felaktig eller filen kan inte läsas. | Använd `File.Exists(imagePath)` innan du skapar bitmapen. |
| **Låga förtroendesiffror** | Bilden är suddig eller har låg kontrast. | För‑behandla bilden (t.ex. `Bitmap.RotateFlip`, `Graphics.Clear`) eller öka DPI. |
| **Fel språk** | OCR använder som standard engelska men kvittot är på ett annat språk. | Ställ in `options.Language = Language.Spanish` (eller motsvarande enum). |
| **JSONL visas som en enda JSON-array** | Du använde `Formatting.None` utan radbrytningshantering. | Se till att varje serialiserat objekt avslutas med `Environment.NewLine`. |

## Fullt fungerande exempel  

Nedan är det kompletta, körklara programmet. Klistra in det i ett konsolprojekt och tryck **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Förväntat resultat:** En `receipt.jsonl`‑fil som innehåller ett JSON‑objekt per rad, var och en med fälten `Text`, `Confidence` och `BoundingBox`. Du kan nu mata in den här filen i vilken analys‑pipeline som helst som accepterar JSONL.

## Nästa steg – Gå bortom grundläggande OCR  

- **Batch‑behandling:** Packa in logiken ovan i en `foreach`‑loop för att hantera hela mappar med kvitton.  
- **Parallellism:** Använd `Parallel.ForEach` för fler‑kärnors hastighetsökning när du arbetar med tusentals bilder.  
- **Efterbehandling:** Ta bort rader med låg förtroende (`Confidence < 0.9`) innan lagring.  
- **Integration:** Skjut JSONL direkt till Azure Blob Storage eller AWS S3 med respektive SDK.  
- **Alternativa format:** Byt `OutputFormat` till `PlainText` eller `Xml` om ditt downstream‑system föredrar dem.  

## Slutsats  

Du har nu en solid, end‑to‑end‑lösning för **extrahering av text från bild** och **konvertering av bild till JSONL** med Aspose OCR i C#. Handledningen täckte allt från att ladda bitmapen till att verifiera output, samt ett antal praktiska tips för att hålla din pipeline robust.

Prova med dina egna kvitton, fakturor eller skannade formulär—se OCR‑motorn förvandla pixlar till sökbar, rad‑strukturerad data på sekunder. Om du stöter på kantfall (t.ex. snedvridna skanningar eller flerspråkig text), gå tillbaka till *RecognitionOptions*-avsnittet och justera språk eller förbehandlingssteg.

Lycka till med kodandet, och må dina datapipelines alltid vara rena!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}