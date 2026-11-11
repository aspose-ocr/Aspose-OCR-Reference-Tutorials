---
category: general
date: 2026-05-28
description: Koreansk språk‑OCR‑handledning med Aspose i C#. Lär dig hur du laddar
  en bild från en ström, extraherar vanlig text, konverterar bilden till PDF och exporterar
  en sökbar PDF.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: sv
og_description: Koreansk språk‑OCR i C# med Aspose. Steg‑för‑steg‑guide för att ladda
  bild från ström, extrahera vanlig text, konvertera bild till PDF och exportera sökbar
  PDF.
og_title: Koreanska språk OCR – Konvertera bild till PDF och extrahera text (C#‑guide)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Koreansk språk-OCR med Aspose: Konvertera bild till PDF och extrahera text
  i C#'
url: /sv/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Korean Language OCR med Aspose: Konvertera bild till PDF och extrahera text i C#

Har du någonsin undrat hur man kör **Korean Language OCR** på en bild utan att skicka något till molnet? Du är inte ensam. Oavsett om du digitaliserar gatunskyltar, bearbetar kvitton eller bygger ett flerspråkigt sökindex, kan möjligheten att känna igen koreanska tecken lokalt spara dig tid, pengar och integritetsproblem.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **laddar bild från ström**, **extraherar ren text**, **konverterar bild till PDF** och slutligen **exporterar sökbar PDF**—allt med Aspose.OCR och några rader C#. Inga externa tjänster, ingen dold magi—bara ren .NET‑kod som du kan klistra in i vilken konsolapp som helst.

## Vad du får med dig

- Ett fungerande konsolprogram som läser en JPEG‑fil via en filström.  
- Koreansk text extraherad som rena Unicode‑strängar.  
- En detaljerad JSON‑rapport av OCR‑körningen för felsökning eller analys.  
- En sökbar PDF som du kan öppna i vilken PDF‑läsare som helst och faktiskt markera de koreanska orden.  

**Förutsättningar**  
- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).  
- Aspose.OCR för .NET NuGet‑paket installerat (`Install-Package Aspose.OCR`).  
- En mapp som innehåller `korean_sign.jpg` och en skrivbar plats för utdatafilerna.  

Om du redan har dessa delar på plats, bra—låt oss sätta igång.

## Steg 1: Initiera OCR‑motorn för Korean Language OCR

Det första du behöver är en `OcrEngine`‑instans. Att aktivera GPU:n (om du har en) snabbar upp igenkänningen dramatiskt, och att stänga av automatisk resurshämtning tvingar biblioteket att använda de offline‑språkpaket du tillhandahåller.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Varför detta är viktigt:**  
> *GPU‑acceleration* kan minska behandlingstiden från sekunder till millisekunder för stora batcher. Att sätta `AutomaticResourceDownload` till `false` säkerställer att demonstrationen fungerar offline—ett avgörande krav för många företagsmiljöer.

## Steg 2: Ladda bild från ström

Att läsa bilden via en ström ger dig flexibilitet: du kan hämta filer från disk, nätverksdelningar eller till och med minnes‑cachade blobbar. Här öppnar vi en lokal JPEG‑fil, men samma mönster fungerar för vilken `Stream` som helst.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Proffstips:** Om du någonsin behöver bearbeta bilder som laddas upp via ett webb‑API, ersätt bara `File.OpenRead` med den inkommande `IFormFile.OpenReadStream()`—resten förblir identisk.

## Steg 3: Välj koreanskt språk och tillämpa förbehandlingsfilter

Aspose.OCR stöder ett fåtal förbehandlingssteg som rengör bilden innan igenkänning. För koreanska skyltar räcker vanligtvis deskewing och denoising.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Vad händer under huven?**  
> `Deskew`‑filtret räta upp roterad text, medan `Denoise` tar bort korn som kan förvirra teckenklassificeraren. Att hoppa över dessa steg leder ofta till förvrängd output, särskilt på lågupplösta foton.

## Steg 4: Extrahera ren text asynkront

Nu kommer sanningsögonblicket—att be motorn att känna igen tecknen och ge oss en ren sträng. Att använda `RecognizeAsync` håller UI‑responsivt om du bäddar in detta i en desktop‑ eller webbapp.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

When you run the program, you should see something like:

```
OCR complete. Extracted text:
서울시청
```

> **Varför asynkront?**  
> OCR kan vara CPU‑intensivt. Asynkron körning förhindrar att din tråd blockeras, vilket är särskilt praktiskt i ASP.NET Core där trådstjärning är ett verkligt problem.

## Steg 5: Hämta ett detaljerat igenkänningsresultat och spara som JSON

Ibland behöver du mer än bara den råa strängen—kanske vill du ha förtroendescore, avgränsningsrutor eller den ursprungliga bilddatan. Metoden `RecognizeDetailed` returnerar ett `RecognitionResult`‑objekt som kan serialiseras till JSON för senare analys.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Opening `korean_ocr.json` will reveal a structure similar to:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **När ska du använda detta?**  
> Om du bygger ett sökindex låter förtroendevärdena dig filtrera bort lågkvalitativa resultat. Om du behöver markera text i ett UI är avgränsningsrutorna din karta.

## Steg 6: Konvertera bild till PDF och exportera sökbar PDF

Aspose gör övergången från raster till vektor enkel. Genom att sätta `OutputFormat` till `SearchablePdf` bäddar biblioteket in den ursprungliga bilden och lägger ett osynligt textlager med OCR‑output ovanpå. Den resulterande PDF‑filen kan sökas, kopieras och indexeras precis som vilken native PDF som helst.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Öppna `korean_searchable.pdf` i Adobe Reader eller någon PDF‑visare, tryck **Ctrl+F**, skriv ett koreanskt ord och se det hoppa till exakt rätt ställe på sidan. Det är kraften i en sökbar PDF.

> **Extra tips:** Om du bara behöver en visuell PDF utan det dolda textlagret, byt `OutputFormat` till `Pdf` istället.

## Fullt fungerande exempel

Nedan är det kompletta programmet—kopiera, klistra in, ersätt `YOUR_DIRECTORY` med en faktisk sökväg, och tryck **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Förväntad konsolutdata

```
OCR complete. Extracted text:
서울시청
```

Och du kommer att hitta tre nya filer bredvid din källbild:

- `korean_ocr.json` – fullständig igenkänningsdata.  
- `korean_searchable.pdf` – en PDF du kan söka i.  
- (valfritt) eventuella mellanstegsloggar du väljer att lägga till.

## Vanliga frågor & edge‑cases

**Vad händer om jag inte har en GPU?**  
Sätt `EnableGpu = false`; CPU‑fallbacken fungerar utmärkt för små batcher.

**Kan jag bearbeta flera bilder i en körning?**  
Absolut. Packa in kärnlogiken i en `foreach (var file in Directory.GetFiles(...))`‑loop och tilldela om `ocrEngine.Image` varje iteration.

**Hur hanterar jag andra språk tillsammans med koreanska?**  
Aspose.OCR låter dig sätta `Language = Language.AutoDetect` eller kombinera språk med bitvis OR‑operator (t.ex. `Language.Korean | Language.English`).

**Vad händer om OCR‑förtroendet är lågt?**  
Inspektera `detailedResult.Pages[0].Words` och filtrera bort poster med `Confidence < 0.7`. Du kan också justera förbehandlingsfilter—försök lägga till `PreprocessFilter.ContrastEnhancement`.

## Avslutning

Du har just sett hur man utför **Korean Language OCR** från början till slut, från **laddning av bild från ström** till **extrahering av ren text**, sedan **konvertering av bild till PDF** och slutligen **export av sökbar PDF**. Tillvägagångssättet är modulärt, så du kan byta bildkälla, ändra utdataformat eller ansluta JSON‑filen till någon efterföljande pipeline.

Vad blir nästa steg

## Relaterade handledningar

- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Känn igen text i bild med Aspose OCR för flera språk](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}