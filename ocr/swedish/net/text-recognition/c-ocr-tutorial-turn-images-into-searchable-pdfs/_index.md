---
category: general
date: 2026-01-12
description: c# ocr-handledning som visar hur du känner igen text i en bild, extraherar
  text från bild i c# och genererar en bild‑till‑pdf ocr‑fil med tillförlitlighetspoäng.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: sv
og_description: Lär dig en komplett C#‑OCR‑handledning för att känna igen text i bilder,
  extrahera text från bilder i C# och skapa ett bild‑till‑PDF OCR‑dokument med konfidenspoäng.
og_title: c# ocr handledning – Konvertera bilder till sökbara PDF-filer
tags:
- OCR
- C#
- PDF
title: c# OCR-handledning – Gör om bilder till sökbara PDF-filer
url: /sv/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Gör om bilder till sökbara PDF-filer

Har du någonsin undrat hur man **läser av text i bild**-filer i ett C#-projekt utan att leta efter tredjepartstjänster? Du är inte ensam. I många verkliga appar—tänk fakturaskannrar, kvittospårare eller flerspråkiga dokumentarkiv—behöver utvecklare en pålitlig, lokal OCR-motor som också ger ut förtroendesiffror.  

Denna **c# ocr tutorial** guidar dig genom allt du behöver: från att ladda en bild, välja språkmodeller, slå på GPU-acceleration, till att spara resultatet som en sökbar PDF. I slutet har du ett färdigt kodexempel som extraherar text, rapporterar OCR‑förtroende och eventuellt skapar en *image to pdf ocr*-fil—allt på under en minut kodning.

## Vad du kommer att bygga

- Läs in en flerspråkig bild (`sample_multi_lang.jpg` används som platshållare).  
- Välj språkmodellerna Arabiska, Hindi och Ryska (du kan lägga till fler).  
- Aktivera GPU‑bearbetning om din maskin stödjer det.  
- Hämta det råa OCR‑resultatet **med förtroendesiffror**.  
- Serialisera resultatet till vackert formaterad JSON **eller** skriv en sökbar PDF.  

Inga externa webbtjänster, ingen dold magi—bara Aspose.OCR för .NET, några rader C# och en tydlig förklaring av **varför** varje rad är viktig.

## Förutsättningar

- .NET 6.0 eller senare (koden kompileras på .NET Core och .NET Framework).  
- Visual Studio 2022 (eller någon IDE du föredrar).  
- En Aspose.OCR för .NET-licens (gratis provversion fungerar för testning).  
- Valfritt: ett CUDA‑kompatibelt GPU om du vill snabba upp igenkänning.

> **Proffstips:** Om du inte har ett GPU, sätt bara `UseGpu = false` så återgår motorn till CPU utan några kodändringar.

## Steg 1: Installera de nödvändiga NuGet‑paketen

Öppna **Package Manager Console** och kör:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Dessa tre paket ger dig OCR‑motorn, GPU‑acceleration och en bra JSON‑serializer för förtroende‑utdata.

## Steg 2: Ställ in projektstrukturen

Skapa ett nytt konsolprojekt (`dotnet new console -n AsposeOcrDemo`) och ersätt den genererade `Program.cs` med koden nedan.  
All logik finns i `Program`‑klassen; den enda extra typen är en liten extensionsmetod som formaterar OCR‑resultatet för JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Varför den här koden fungerar

1. **GPU‑växel** – `GpuOcrEngine` utnyttjar CUDA‑kärnor; ternära operatorn gör växlingen smidig.  
2. **Automatisk språknedladdning** – `AutoDownloadResources = true` säkerställer att Arabiska, Hindi‑ och Ryska‑modellerna hämtas första gången du kör appen.  
3. **Förtroendesiffror** – `result.Words` innehåller ett `Confidence` för varje igenkänt ord; extensionsmetoden formaterar dem till ett rent JSON‑objekt.  
4. **Sökbar PDF** – `result.Pdf` är redan en fullt sökbar PDF, så vi skriver bara byte‑arrayen till disk. Inga extra bibliotek behövs.

## Steg 6: Kör exempelkoden

Öppna en terminal, navigera till projektmappen och kör:

```bash
dotnet run
```

Om du valde **JSON**‑utdata kommer du att se något liknande:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Om du bytte till **PDF** skriver konsolen ut sökvägen och du hittar en sökbar PDF precis bredvid källbilden.

## Vanliga frågor & edge‑cases

- **Vad händer om en språkmodell inte är tillgänglig?**  
  OCR‑motorn kastar ett tydligt `ResourceNotFoundException`. Eftersom vi har `AutoDownloadResources = true` hämtas den saknade modellen automatiskt första gången, så undantaget dyker sällan upp i produktion.

- **Kan jag bearbeta en batch av bilder?**  
  Absolut. Lägg `engine.Recognize`‑anropet i en `foreach`‑loop över en katalog med filer. Samma `OcrResultExtensions` fungerar för varje bild.

- **Behöver jag en licens för GPU?**  
  Nej. Gratisprovversionen fungerar både för CPU och GPU. En full licens tar bort vattenstämpeln och lyfter begränsningarna för sidantal.

- **Hur exakta är förtroendesiffrorna?**  
  Siffrorna varierar från 0,0 (ingen förtroende) till 1,0 (perfekt förtroende). I praktiken är allt över 0,90 pålitligt för efterföljande bearbetning; du kan filtrera ord med lägre förtroende om du behöver striktare validering.

## Steg 7: Nästa steg (utöka ditt OCR‑verktygssats)

1. **Lägg till fler språk** – lägg bara till `LanguageModel.French` (eller någon annan stödjande modell) i `Languages`‑arrayen.  
2. **Kombinera OCR med PDF/A‑konvertering** – Aspose.PDF kan bädda in OCR‑lagret i ett PDF/A‑2b‑kompatibelt dokument för arkivering.  
3. **Integrera med Azure Functions** – paketera logiken i en serverlös endpoint för att bearbeta uppladdningar i realtid.  
4. **Finjustera förtroendetrösklar** – använd `result.Words.Where(w => w.Confidence < 0.85)` för att flagga osäkra ord för manuell granskning.

---

### TL;DR

Denna **c# ocr tutorial** visar dig hur du:

- Läs in en bild och välj flera språkmodeller.  
- Aktivera GPU‑acceleration med en enda boolesk flagga.  
- Hämta OCR‑resultat **med förtroendesiffror** och serialisera dem till JSON.  
- Eventuellt skriv en sökbar PDF (**image to pdf ocr**).  

Allt detta är möjligt med bara ett fåtal rader kod, en gratis Aspose.OCR‑provversion och koden ovan. Prova, justera språklistan, så har du en produktionsklar OCR‑pipeline på några minuter.

---

![c# ocr tutorial exempelbild](https://example.com/placeholder-image.jpg "c# ocr tutorial exempelbild")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}