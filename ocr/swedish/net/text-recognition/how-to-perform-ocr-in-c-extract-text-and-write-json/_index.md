---
category: general
date: 2026-02-09
description: Lär dig hur du utför OCR i C# för att extrahera text från en bild, känna
  igen text i PNG och snabbt skriva en JSON‑fil i C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: sv
og_description: Hur utför man OCR i C#? Följ den här steg‑för‑steg‑guiden för att
  extrahera text från bild, känna igen text från PNG och skriva JSON‑fil i C# effektivt.
og_title: Hur man utför OCR i C# – Extrahera text och skriv JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Hur man utför OCR i C# – Extrahera text och skriv JSON
url: /sv/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

Now "Sometimes OCR returns low confidence for noisy scans. You can filter symbols before exporting:" => translate.

Now "Large Files & Memory" => "Stora filer & minne".

Now "Processing a multi‑megabyte PNG can spike memory usage. Consider streaming the image in chunks or using `OcrEngine.RecognizeAsync` (available in newer Aspose versions) to keep the UI responsive." => translate.

Now "Step 5: Extend the Solution (Optional)" => "Steg 5: Utöka lösningen (valfritt)".

Now bullet points.

Now "All these extensions follow the same how to perform OCR pattern we established—initialize, recognize, export, and persist." => translate.

Now "Frequently Asked Questions" => "Vanliga frågor".

Now Q&A.

Now "Conclusion" => "Slutsats".

Now final paragraph.

Now ensure we keep shortcodes at start and end.

Now produce final content.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så utför du OCR i C# – Komplett guide

Att utföra OCR i C# är ett vanligt hinder när du behöver **extract text from image**‑filer. I den här guiden går vi igenom hur man känner igen text från PNG, exporterar det detaljerade resultatet till en JSON‑sträng och slutligen **write JSON file C#**‑stil. Har du någonsin stirrat på ett skannat formulär och undrat hur du förvandlar de där snirkliga linjerna till sökbar text? Du är inte ensam; många utvecklare stöter på detta problem tidigt.

Vi använder Aspose.OCR‑biblioteket eftersom det levererar per‑symbol‑förtroende direkt ur lådan och fungerar bra med .NET 6+‑projekt. När du är klar med den här tutorialen har du en färdigkörningskonsolapp som laddar en PNG, plockar ut varje tecken och sparar en prydlig JSON‑fil som du kan mata in i en databas eller en AI‑modell. Inga mystiska “se dokumentationen”‑genvägar—bara en självständig lösning.

## Vad du behöver

- **.NET 6 SDK** (eller senare) – den aktuella LTS‑versionen vid skrivtillfället.  
- **Aspose.OCR for .NET** NuGet‑paket – `Install-Package Aspose.OCR`.  
- En PNG‑bild du vill skanna (t.ex. `form.png`).  
- En IDE eller editor – Visual Studio, VS Code, Rider – vad du än föredrar.

Det är allt. Om du har dessa delar är du redo att köra.

![Exempel på hur man utför OCR](ocr-example.png "Hur man utför OCR i C#")

*Bildtext: illustration som visar hur man utför OCR med en C#‑konsolapp som bearbetar en PNG.*

## Steg 1: Ställ in projektet och lägg till beroenden

Först, skapa ett nytt konsolprojekt och hämta Aspose OCR‑biblioteket.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Proffstips:** Använd flaggan `--framework net6.0` om du vill låsa mål‑ramverket explicit.

Varför detta steg är viktigt: NuGet‑paketet innehåller klasserna `OcrEngine`, `ImageStream` och `JsonExporter` som vi kommer att förlita oss på. Utan dem har kompilatorn ingen aning om vad “OCR” ens betyder.

## Steg 2: Skriv den centrala OCR‑logiken

Öppna `Program.cs` (eller skapa en ny fil) och ersätt innehållet med följande. Varje avsnitt är kommenterat så att du kan se varför det finns där.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Varför varje del är viktig

- **OcrEngine**: Tänk på den som hjärnan i operationen. Den laddar språkmodeller och sätter upp inferens‑pipeline:n.  
- **ImageStream.FromFile**: Hanterar alla PNG, JPEG, BMP osv. Den abstraherar bort fil‑I/O‑kuriosa.  
- **RecognitionResult**: Innehåller råtexten plus förtroendesiffror. Här får du den granulära data du behöver för efterföljande validering.  
- **JsonExporter**: Konverterar det rika `RecognitionResult` till en ren JSON‑payload, perfekt för API:er.  
- **File.WriteAllText**: Det enkla .NET‑sättet att **write JSON file C#** utan extra beroenden.

## Steg 3: Kör applikationen och verifiera output

Kompilera och kör programmet:

```bash
dotnet run
```

Du bör se ett konsolmeddelande liknande:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Öppna `form.json` – du hittar något liknande:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Steget **extract text from image** lyckades, och du har nu en maskinläsbar JSON‑representation av varje tecken.

## Steg 4: Hantera vanliga edge‑cases

### Saknade eller korrupta filer

Om PNG‑sökvägen är felaktig kastar `ImageStream.FromFile` ett `FileNotFoundException`. Omge laddningskoden med ett try‑catch‑block:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Låga förtroendepoäng

Ibland returnerar OCR låg förtroende för brusiga skanningar. Du kan filtrera symboler innan export:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Detta säkerställer att JSON‑filen bara innehåller rimligt pålitliga tecken—användbart när du matar data till efterföljande validerings‑pipelines.

### Stora filer & minne

Att bearbeta en multi‑megabyte PNG kan öka minnesanvändningen. Överväg att streama bilden i bitar eller använda `OcrEngine.RecognizeAsync` (tillgänglig i nyare Aspose‑versioner) för att hålla UI‑responsen.

## Steg 5: Utöka lösningen (valfritt)

- **Batch‑behandling**: Loopa igenom en katalog med PNG‑filer och generera en matchande JSON per fil.  
- **Databaslagring**: Sätt in JSON‑en i en SQL `NVARCHAR(MAX)`‑kolumn för senare analys.  
- **Språkväljare**: Sätt `ocrEngine.Language = OcrLanguage.Spanish;` om du behöver stöd för icke‑engelska språk.

Alla dessa utökningar följer samma **how to perform OCR**‑mönster vi etablerat—initiera, känna igen, exportera och persistera.

## Vanliga frågor

**Q: Fungerar detta med JPG eller TIFF?**  
A: Absolut. `ImageStream.FromFile` upptäcker automatiskt formatet, så du kan ersätta PNG med vilken stödjande rasterbild som helst.

**Q: Vad händer om jag behöver extrahera text från en PDF?**  
A: Konvertera varje PDF‑sida till en bild först (t.ex. med `Aspose.PDF`) och mata sedan PNG‑en in i OCR‑flödet som beskrivs här.

**Q: Kan jag få OCR‑resultatet som XML istället för JSON?**  
A: Ja. Aspose.OCR levereras också med en `XmlExporter`. Byt ut `JsonExporter` mot `XmlExporter` och justera filändelsen.

## Slutsats

Vi har gått igenom **how to perform OCR** i C# från början till slut, visat hur du **extract text from image**, **recognize text from PNG** och **write JSON file C#** utan problem. Det kompletta, körbara exemplet finns i kodsnuttarna ovan, och du förstår nu varför varje steg är viktigt—initiering av motorn, hantering av edge‑cases och persistering av resultat.

Nästa steg kan vara att utforska batch‑OCR‑pipelines, integrera JSON‑outputen med Azure Cognitive Search eller experimentera med egna språkmodeller. Himlen är gränsen när du har bemästrat grunderna i OCR i C#.

Om du stött på några **snags** eller har **idéer** för vidare utökningar, lämna en kommentar nedanför. Lycka till med kodandet, och njut av att förvandla pixeliga skanningar till ren, sökbar data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}