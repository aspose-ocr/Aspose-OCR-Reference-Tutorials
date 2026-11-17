---
category: general
date: 2026-09-10
description: Hur man använder OCR i C# för att extrahera kyrillisk text, förbehandla
  bilder och konvertera dem till PDF‑ eller HTML‑filer i ett enda körbart exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: sv
lastmod: 2026-09-10
og_description: Hur man använder OCR i C# för att extrahera kyrillisk text, förbehandla
  bilder och exportera resultaten som PDF eller HTML. Följ den här steg‑för‑steg‑guiden.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Hur man använder OCR i C# – extrahera kyrillisk text och konvertera bilder
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Hur man använder OCR i C# för att extrahera kyrillisk text
url: /sv/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du OCR i C# för att extrahera kyrillisk text

Om du behöver **how to use OCR** i C# för att extrahera kyrillisk text från skannade dokument, visar den här guiden en komplett, färdig‑att‑köra lösning. Du kommer också att lära dig hur du **preprocess image for OCR**, och hur du **convert image to PDF** eller **convert image to HTML** när texten har identifierats.

Projekt för dokumentdigitalisering stöter ofta på två problem: lågkvalitativa skanningar och behovet av att lagra resultat i flera format. Denna handledning löser båda genom att använda Aspose.OCR‑biblioteket, som automatiskt laddar ner saknade språkpaket, erbjuder inbyggda bildbehandlingshjälpmedel och kan exportera OCR‑resultatet till PDF eller HTML med ett enda anrop.

## Förutsättningar

* .NET 6.0 SDK eller senare (koden fungerar också med .NET Framework 4.7+).
* Visual Studio 2022 eller någon editor som stödjer C#‑projekt.
* **Aspose.OCR**‑paketet från NuGet. Installera det med:

```bash
dotnet add package Aspose.OCR
```

* En bildfil som innehåller kyrilliska tecken (t.ex. `sample_cyrillic.jpg`).  
  Placera filen i en mapp som du kan referera till som `YOUR_DIRECTORY`.

Biblioteket kommer att ladda ner det kyrilliska språkpaketet första gången du sätter `ocrEngine.Language = Language.Cyrillic;`, så ingen manuell nedladdning krävs.

## Steg 1 – Initiera OCR‑motorn (how to use OCR)

Att skapa en `OcrEngine`‑instans förbereder motorn för alla efterföljande operationer.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Varför detta är viktigt:** Motorn innehåller konfiguration som språk, bildbehandlingsinställningar och utskriftsalternativ. Att initiera den en gång håller resten av koden ren och trådsäker.

## Steg 2 – Välj det kyrilliska språket (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Varför detta är viktigt:** OCR‑noggrannheten beror starkt på rätt språkmodell. Genom att explicit välja `Language.Cyrillic` använder motorn tecken‑frekvenstabeller som passar ryska, ukrainska, bulgariska osv.

## Steg 3 – Förbehandla bilden för OCR

Lågkvalitativa skanningar innehåller snedvridning, fläckar eller ojämn belysning. Den inbyggda `ImageProcessor` kan förbättra igenkänningsgraden med bara två anrop.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Varför detta är viktigt:** Förbehandling minskar falska tecken och ökar förtroendescoret. Snedvriden text ger ofta förvrängd output; avsnedvridning räta upp den. Fläckborttagning eliminerar små artefakter som OCR‑motorn annars kan tolka som bokstäver.

> **Proffstips:** Om dina källbilder redan är rena kan du hoppa över dessa anrop. För kraftigt förnedrade skanningar, överväg ytterligare steg som `Binarize()` eller `ContrastStretch()`.

## Steg 4 – Utför OCR på inmatningsbilden

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Varför detta är viktigt:** `Process` kör igenkänningspipeline på den levererade bitmapen. Den returnerar `void`; den igenkända texten blir tillgänglig via egenskapen `Text`.

## Steg 5 – Hämta den igenkända texten och spara den till en fil

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Varför detta är viktigt:** Att lagra den råa texten möjliggör efterföljande bearbetning såsom sökning, indexering eller att skicka den till översättningstjänster.

## Steg 6 – Exportera OCR‑resultatet till andra format (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Varför detta är viktigt:** Att konvertera OCR‑resultatet till PDF eller HTML låter dig behålla den visuella kontexten av originalbilden samtidigt som du får sökbar text. Detta är särskilt värdefullt för juridiska eller arkiveringsarbetsflöden.

### Förväntat resultat

Att köra programmet med en tydlig kyrillisk skanning producerar tre filer:

* `result.txt` – vanlig Unicode‑text, t.ex. `Пример текста на кириллице`.
* `result.pdf` – en PDF som innehåller bilden med ett osynligt textlager för sökning.
* `result.html` – en HTML‑sida som visar bilden och valbar text.

Öppna någon av filerna för att verifiera att de kyrilliska tecknen har extraherats korrekt.

## Vanliga frågor och specialfall

| Fråga | Svar |
|----------|--------|
| **Vad händer om språkpaketet misslyckas att laddas ner?** | Se till att maskinen har internetåtkomst. Du kan också för‑ladda ner paketet från Asposes webbplats och placera det i `bin`‑mappen. |
| **Kan jag känna igen andra alfabet i samma körning?** | Ja. Anropa `ocrEngine.Language = Language.English;` (eller någon annan stödjande enum) innan `Process`. Du kan behöva köra `Process` separat för varje språk om bilden blandar skript. |
| **Min bild är en multi‑page TIFF – fungerar detta?** | `OcrEngine` bearbetar en bitmap åt gången. Ladda varje sida i en `Bitmap` och anropa `Process` i en loop, och sammanfoga resultaten. |
| **Hur ökar jag prestandan för stora batcher?** | Återanvänd en enda `OcrEngine`‑instans och sätt `ocrEngine.OptimizeMemory = true;`. Överväg också parallell bearbetning med separata motorinstanser per tråd. |

## Slutsats

Du vet nu **how to use OCR** i C# för att **extract Cyrillic text**, **preprocess image for OCR**, och **convert image to PDF** eller **convert image to HTML** i några koncisa steg. Det kompletta exemplet demonstrerar en produktions‑

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract OCR Text in C# – Complete Step‑by‑Step Guide](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}