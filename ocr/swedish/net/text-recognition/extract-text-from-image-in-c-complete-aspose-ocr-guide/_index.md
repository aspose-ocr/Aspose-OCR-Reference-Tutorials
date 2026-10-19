---
category: general
date: 2026-01-10
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du konverterar
  text från skannade dokument med batchbearbetning och sparar resultaten.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: sv
og_description: Extrahera text från bild med Aspose OCR i C#. Denna handledning visar
  hur man konverterar text i skannade dokument med batchbearbetning.
og_title: Extrahera text från bild i C# – Komplett Aspose OCR-guide
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahera text från bild i C# – Komplett Aspose OCR-guide
url: /sv/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild – Komplett Aspose OCR-guide

Har du någonsin behövt **extrahera text från bild** men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på den muren när de hanterar skannade PDF‑filer, fler‑sidiga TIFF‑filer eller foto‑baserade kvitton. Den goda nyheten är att med Aspose OCR kan du **konvertera skannad dokumenttext** på bara några få rader C#.

I den här handledningen går vi igenom ett verkligt scenario: att ta en fler‑sidig TIFF, köra batch‑OCR på varje sida och skriva en enda textfil som innehåller varje sidas innehåll. I slutet har du en färdig‑att‑köra konsolapp, förstår varför varje steg är viktigt och vet hur du kan justera flödet för kantfall som lösenordsskyddade bilder eller anpassade språkpaket.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar även med .NET Core och .NET Framework)  
- Visual Studio 2022 (eller någon annan editor du föredrar)  
- En Aspose OCR‑licensfil (eller så kan du använda gratis utvärderingsläge)  
- En fler‑sidig bildfil (t.ex. `multipage.tif`) placerad i en mapp du kan referera till  

Inga ytterligare NuGet‑paket krävs förutom `Aspose.OCR`; vi installerar det i första steget.

## Steg 1 – Installera Aspose  OCR och sätt upp projektet

För att börja, skapa ett nytt konsolprojekt och hämta Aspose  OCR‑biblioteket.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Proffstips:** Om du har en licensfil (`Aspose.OCR.lic`), kopiera den till projektets rot. Biblioteket kommer automatiskt att plocka upp den vid körning.

Varför detta steg? Att installera paketet ger dig åtkomst till `BatchProcessor`, `OcrEngine` och andra praktiska klasser som abstraherar bort låg‑nivå bildhantering. Det säkerställer också att du använder de senaste OCR‑algoritmerna som Aspose levererar.

## Steg 2 – Ladda den fler‑sidiga bilden med BatchProcessor

`BatchProcessor` är designad för exakt detta scenario: att iterera över varje sida i en fler‑sidig bild utan att du måste dela filerna manuellt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` läser alla sidor till minnet och exponerar dem via `batchProcessor.Pages`. Varje sidobjekt känner till sitt nummer (`ocrPage.Number`) som vi senare kommer att använda för tydliga rubriker.

## Steg 3 – Förbered en StringBuilder för att samla resultat

Vi vill ha en enda textfil som innehåller varje sidas OCR‑utdata, separerade med rubriker. `StringBuilder` är det mest effektiva sättet att sammanfoga strängar i en loop.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Varför en `StringBuilder`? Att concatenera strängar med `+` i en loop skulle allokera en ny sträng vid varje iteration, vilket försämrar prestandan—särskilt med stora dokument.

## Steg 4 – Iterera över varje sida, kör OCR och lägg till resultat

Nu är kärnan i handledningen: loopa genom varje sida, känna igen text och lagra den med en sidmarkör.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Varför en ny `OcrEngine` per sida?** Vissa utvecklare återanvänder en enda motor och ändrar dess `Image`‑egenskap, men det kan behålla språkinställningar eller tidigare resultat, vilket leder till subtila buggar. Att instansiera en ny motor garanterar en ren start.

### Hantera vanliga kantfall

- **Tomma sidor:** Om en sida inte innehåller någon igenkännbar text, kommer `ocrEngine.Text` att vara en tom sträng. Du kanske vill infoga en platshållare som “(No text detected)”.
- **Språkväljning:** Som standard använder Aspose OCR engelska. För att bearbeta tyska eller franska, sätt `ocrEngine.Language = Language.German;` innan du anropar `Recognize()`.
- **Prestandatips:** För enorma TIFF‑filer kan du aktivera `ocrEngine.UseParallelProcessing = true;` för att utnyttja flera kärnor.

## Steg 5 – Skriv det kombinerade resultatet till en textfil

Till sist, spara den samlade strängen till disk.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

Den resulterande `multipage_result.txt` kommer att se ut ungefär så här:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Du har nu **extraherat text från bild** och effektivt **konverterat skannad dokumenttext** till ett sökbart, redigerbart format.

## Bonus – Visuell översikt (Bild‑alt‑text)

Nedan är ett enkelt flödesdiagram som illustrerar processen.  
*Alt‑text:* “Diagram som visar hur man extraherar text från bild med Aspose OCR batch‑behandling i C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(Om du publicerar den här handledningen på en statisk webbplats, ersätt platshållaren med en faktisk SVG‑ eller PNG‑fil.)*

## Vanliga frågor

**Fungerar detta med PDF‑filer?**  
Ja, Aspose OCR kan läsa PDF‑sidor som bilder. Du behöver bara konvertera PDF‑filen till bilder först, eller använda `PdfDocument` från `Aspose.PDF` och skicka varje sidas rasteriserade bild till `OcrEngine`.

**Vad händer om min TIFF är lösenordsskyddad?**  
`BatchProcessor` hanterar inte kryptering direkt. Dekryptera filen med ett bibliotek som `Aspose.Imaging` innan du skickar den till OCR‑pipeline:n.

**Kan jag få ut JSON istället för vanlig text?**  
Absolut. Ersätt `StringBuilder`‑logiken med en JSON‑serializer (t.ex. `System.Text.Json`) och lagra varje sidas text under en nyckel `pageNumber`.

## Fullt fungerande exempel

Här är det kompletta programmet som du kan kopiera‑klistra in i `Program.cs`. Det inkluderar alla using‑direktiv, felhantering och kommentarer.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Kör programmet med:

```bash
dotnet run
```

Du bör se ett konsolmeddelande som bekräftar framgång, och utdatafilen kommer att innehålla de sammanslagna OCR‑resultaten.

## Slutsats

Vi har just demonstrerat ett praktiskt sätt att **extrahera text från bild** med Aspose OCR, och omvandla vilken fler‑sidig skannad fil som helst till vanlig, sökbar text. Genom att utnyttja `BatchProcessor` och en ren per‑sidig `OcrEngine`‑uppsättning kan du på ett pålitligt sätt **konvertera skannad dokumenttext** samtidigt som kodbasen hålls enkel och underhållbar.

Känn dig fri att experimentera: prova olika språk, byt till JSON‑utdata, eller integrera denna logik i ett webb‑API som bearbetar uppladdningar i realtid. Kärnmönstret förblir detsamma—ladda, känna igen, samla och spara.

Har du fler frågor om OCR, Aspose‑licensiering eller hantering av massiva dokumentbuntar? Lämna en kommentar nedan eller kolla in Asposes officiella dokumentation för djupare insikter. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}