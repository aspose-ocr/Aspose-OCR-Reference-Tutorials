---
category: general
date: 2026-09-13
description: Lär dig hur du konverterar en skannad sida till PDF i C# med Aspose OCR.
  Den här guiden visar förbehandling, Korean‑textigenkänning och hur du skapar en
  sökbar PDF.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Lär dig hur du konverterar en skannad sida till PDF i C# med Aspose
  OCR. Handledningen täcker bildförbehandling, GPU‑accelererad OCR för Korean‑text
  och att generera en sökbar PDF på några minuter.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Så här konverterar du en skannad sida till PDF i C# med OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Så här konverterar du en skannad sida till PDF i C# med OCR
url: /sv/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du konverterar en skannad sida till PDF i C# med OCR

Om du behöver **konvertera en skannad sida till PDF** samtidigt som du behåller texten sökbar, är du på rätt plats. Denna handledning guidar dig genom att använda Aspose OCR för att **förbehandla bild för OCR**, **igenkänna koreansk textbild**, och slutligen **skapa sökbar PDF-bild** – allt från en enkel C#-konsolapplikation.

## Snabba svar
- **Vilket bibliotek hanterar OCR?** Aspose.OCR for .NET  
- **Kan jag använda GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Behöver jag ett koreanskt språkpaket?** It downloads automatically on first use  
- **Kommer utdata att vara sökbara?** The generated PDF contains an invisible text layer  
- **Vilka .NET-versioner stöds?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Krav

- **.NET 6.0 eller senare** – fungerar på .NET Core, .NET Framework och .NET 5/6+  
- **Aspose.OCR för .NET** NuGet‑paket (`Aspose.OCR`) – provnycklar är gratis på Aspose‑sajten  
- En exempelbild med koreanska tecken, t.ex. `korean_book_page.jpg`  
- Din favorit‑IDE (Visual Studio 2022, VS Code, Rider osv.)

> **Proffstips:** Spara bilder i en `Resources/`‑mapp så att sökvägarna förblir konsekventa på olika maskiner.

## Översikt av processen

1. Initiera OCR‑motorn med GPU‑stöd.  
2. Lägg till **preprocess image for OCR**‑filter såsom deskew och denoise.  
3. Ladda ner och ladda den koreanska språkmodellen (hanteras automatiskt).  
4. Kör OCR på bilden.  
5. Exportera resultatet med **SearchablePdfExporter** för att **create searchable PDF image**.  
6. (Valfritt) Serialisera OCR‑utdata till JSON för efterföljande pipelines.

Nedan utvecklar vi varje steg, förklarar *varför* det är viktigt, och ger dig den exakta koden du kan kopiera‑klistra.

## Hur fungerar konvertering av skannad sida till PDF?

`OcrEngine` är huvudklassen i Aspose.OCR som utför optisk teckenigenkänning på bilder.  
`SearchablePdfExporter` skapar en PDF som innehåller originalbilden och ett osynligt textlager för sökning.  
`RecognitionResult` innehåller texten och förtroendedata som returneras av OCR‑motorn.

Läs in din bild med `new OcrEngine()` och anropa `engine.Recognize("korean_book_page.jpg")`, skicka sedan `RecognitionResult` till `SearchablePdfExporter.Export`. Detta tvåstegsflöde läser bitmapen, extraherar Unicode‑text och bäddar in båda i en enda PDF där textlagret är osynligt men sökbart. GPU‑acceleration halverar igenkänningstiden, medan deskew‑ och denoise‑filter ökar noggrannheten med upp till 15 % på brusiga skanningar.

## Konvertera bild till PDF – komplett arbetsflöde

Följande kodsnutt är det *kompletta* programmet. Skapa ett nytt konsolprojekt (`dotnet new console -n OcrPdfDemo`) och ersätt den autogenererade `Program.cs` med koden som visas i platshållaren.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Varför detta fungerar

- **GPU‑acceleration** halverar igenkänningstiden ungefär jämfört med enbart CPU‑läge.  
- **Deskew** och **Denoise** är klassiska *preprocess image for OCR*-tekniker; de korrigerar vanliga skanningsfel som annars får motorn att missa tecken.  
- **Language model loading** är avgörande för **recognize Korean text image** – utan den koreanska modellen skulle motorn falla tillbaka på ett generiskt latinskt alfabet och producera skräp.  
- **SearchablePdfExporter** samlar den ursprungliga bitmapen och ett osynligt textöverlägg, vilket ger dig ett **create searchable pdf image**‑resultat som du kan indexera i vilken PDF‑visare som helst.

## Varför detta fungerar

- **GPU‑acceleration** halverar igenkänningstiden ungefär jämfört med enbart CPU‑läge.  
- **Deskew** och **Denoise** är klassiska *preprocess image for OCR*-tekniker; de korrigerar vanliga skanningsfel som annars får motorn att missa tecken.  
- **Language model loading** är avgörande för **recognize Korean text image** – utan den koreanska modellen skulle motorn falla tillbaka på ett generiskt latinskt alfabet och producera skräp.  
- **SearchablePdfExporter** samlar den ursprungliga bitmapen och ett osynligt textöverlägg, vilket ger dig ett **create searchable pdf image**‑resultat som du kan indexera i vilken PDF‑visare som helst.

## Förbehandla bild för OCR – tips & tricks

`DeskewFilter` korrigerar rotationen på skannade sidor.  
`ContrastFilter` justerar bildkontrasten för att förbättra OCR‑noggrannheten.  
`BinarizationFilter` konverterar bilden till svart‑vitt baserat på ett tröskelvärde, vilket minskar bakgrundsbrus.  
`OrientationFilter` upptäcker och korrigerar blandade porträtt‑/landskapsidor.

| Problem | Ytterligare filter | Hur man lägger till |
|-------|-------------------|------------|
| Låg kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Mycket bakgrundsbrus | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Blandad orientering (porträtt & landskap) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Obs:** Att lägga till för många filter kan sakta ner bearbetningen. Testa varje förändring på en enskild sida innan du skalar upp.

## Känn igen koreansk textbild – vanliga fallgropar

Koreanska skript innehåller Hangul‑stavelser som är visuellt täta. Om du märker förvrängd output:

1. **Se till att språkmodellen är helt nedladdad** – kontrollera konsolen för ett meddelande som “Downloading Korean model…”.  
2. **Öka `MaxAngle`** i `DeskewFilter` om dina skanningar är roterade mer än 12°.  
3. **Öka GPU‑minnet** genom att sätta `ocrEngine.GpuMemoryLimit = 2048;` (värde i MB).

`LanguageModel.Korean` laddar den koreanska språkdata för OCR, vilket möjliggör exakt Hangul‑igenkänning.  

Dessa justeringar påverkar direkt framgången för **recognize Korean text image**.

## Skapa sökbar PDF‑bild – verifiera resultatet

När programmet är klart, öppna `korean_page.pdf` i någon PDF‑läsare (Adobe Acrobat Reader, Foxit, till och med Chrome). Du bör kunna:

- **Markera text** med musen som om det vore en inbyggd PDF.  
- **Söka** efter koreanska ord med den inbyggda sökrutan.  

Om textlagret visas tomt, dubbelkolla att `Export`‑metoden fick rätt bildsökväg och att OCR‑resultatet innehåller icke‑tom `RecognitionResult.Text`.

## Full JSON‑output – vad du kan förvänta dig

Konsolen skriver ut en snyggt formaterad JSON‑payload. Ett trunkerat exempel ser ut så här:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Felsökning & FAQ

**Q: Min PDF är enorm jämfört med originalbilden.**  
A: Exportören bäddar in den ursprungliga bitmapen i dess ursprungliga upplösning. Om storlek är ett problem, skala ner bilden *innan* igenkänning:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR‑resultatet returnerar tomma strängar.**  
A: Verifiera att bildsökvägen är korrekt och att filen inte är korrupt. Se också till att GPU‑drivrutinen är uppdaterad; äldre drivrutiner kan orsaka tysta fel.

**Q: Kan jag bearbeta flera sidor i en loop?**  
A: Absolut. Omge steg 4‑6 i en `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))`‑loop och ändra PDF‑utgångssökvägen därefter.

## Slutsats

Vi har just **konverterat bild till PDF** samtidigt som vi bevarar sökbar text, allt tack vare Aspose OCR:s kraftfulla pipeline. Genom att **preprocess image for OCR** ökar du noggrannheten; genom att **recognize Korean text image** hanterar du komplexa skript; och genom att **create searchable pdf image** får du ett portabelt, indexerbart dokument.

Hämta koden, rikta den mot dina egna skanningar och experimentera med ytterligare filter eller språkmodeller. Samma mönster fungerar för kinesiska, japanska eller något latinskt språk – byt bara ut `LanguageModel.Korean` mot rätt enum.

Har du fler frågor? Lämna en kommentar, och lycka till med kodandet!

---

**Senast uppdaterad:** 2026-09-13  
**Testat med:** Aspose.OCR 24.11 för .NET  
**Författare:** Aspose

## Relaterade handledningar

- [Skapa sökbar PDF från skannade filer med Aspose OCR](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR‑förbehandlingspipeline – hur man känner igen text från bild](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Känn igen text från bild med Aspose OCR – komplett C‑guide](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}