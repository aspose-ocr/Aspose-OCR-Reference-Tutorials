---
category: general
date: 2026-04-04
description: Lär dig hur du extraherar text från TIFF-filer med ett OCR-motorexempel
  i C#. Steg‑för‑steg‑guide med JSON- och XML-utdata.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: sv
og_description: Extrahera text från TIFF-filer med ett OCR-motorexempel i C#. Detaljerade
  steg, komplett kod och tips för JSON/XML‑utdata.
og_title: Extrahera text från TIFF med Aspose OCR-motor – Fullständig guide
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahera text från TIFF med Aspose OCR‑motorn – Komplett exempel
url: /sv/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från TIFF – Fullständigt OCR-motorexempel i C#

Har du någonsin behövt **extrahera text från TIFF**‑bilder men varit osäker på vilket bibliotek som kan hantera fler‑sidiga filer utan en massa kringgående lösningar? Du är inte ensam. I många äldre system kommer dokument som fler‑sidiga TIFF‑skanningar, och att hämta den råa texten är en nödvändig funktion för sökning, efterlevnad eller automatisering av datainmatning.

Den goda nyheten? Med Aspose OCR kan du göra det på några få rader—utan att pilla med låg‑nivå pixelbuffertar. Denna handledning guidar dig genom ett **fullständigt OCR‑motorexempel** som laddar en fler‑sidig TIFF, känner igen varje sida och skriver ut både snyggt formaterad JSON och valfri XML. I slutet har du en färdig‑att‑köra C#‑konsolapp som extraherar text från TIFF‑filer på sekunder.

## Vad du kommer att lära dig

- Hur du konfigurerar Aspose OCR‑motorn i ett .NET‑projekt.  
- Den exakta koden som behövs för att **extrahera text från TIFF**‑filer, inklusive hantering av fler‑sidiga filer.  
- Varför du kanske vill ha JSON istället för XML‑utdata och hur du genererar båda.  
- Tips för felsökning av vanliga fallgropar (t.ex. bild‑DPI, minnesanvändning).  

### Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar med .NET Core och .NET Framework).  
- En giltig Aspose OCR‑licens (eller en gratis provnyckel).  
- Visual Studio 2022 eller någon C#‑redigerare du föredrar.  
- En exempel‑fil med fler‑sidig TIFF (namngiven `multi-page.tiff` i exemplet).  

> **Proffstips:** Om du har en stram budget låter gratisprovet dig fortfarande extrahera text från upp till 100 sidor per månad—perfekt för testning.

---

## Steg 1 – Initiera OCR‑motorn (ocr engine example)

Innan vi kan **extrahera text från TIFF** behöver vi en instans av OCR‑motorn. Detta objekt innehåller all konfiguration du eventuellt kan justera senare (språk, upplösning osv.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Varför detta är viktigt:* `OcrEngine`‑klassen döljer det tunga arbetet. Att instansiera den en gång och återanvända den för flera bilder är mer minnes‑effektivt än att skapa en ny motor per sida.

---

## Steg 2 – Ladda den fler‑sidiga TIFF‑filen (extract text from TIFF)

Nu pekar vi motorn på vår källfil. `ImageStream.FromFile` stöder TIFF, JPEG, PNG och många andra, men i den här handledningen fokuserar vi på TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Obs:** Ersätt `YOUR_DIRECTORY` med den faktiska mappvägen på din maskin.  
> **Tips:** Om din TIFF har låg DPI (under 150), överväg att förbehandla den för att förbättra OCR‑noggrannheten.

---

## Steg 3 – Känn igen alla sidor

Att anropa `Recognize()` kör OCR‑algoritmen över **varje sida** i TIFF‑filen. Resultatobjektet innehåller den råa texten, förtroendescore och sid‑vis segmentering.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Vad du får tillbaka:* `ocrResult` innehåller en samling av `PageResult`‑objekt. Texten för varje sida kan nås via `ocrResult.Pages[i].Text`. Motorn levererar också förtroendenivåer, vilket kan vara användbart för kvalitetskontroller.

---

## Steg 4 – Spara resultat som JSON (och valfri XML)

De flesta moderna pipelines föredrar JSON, men äldre system hanterar fortfarande XML. Så här genererar du båda, snyggt formaterade.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Exempel på JSON‑utdata (avkortad)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON‑utdata är människoläsbar, vilket gör felsökning enkelt. XML speglar samma struktur om du behöver den.

---

## Steg 5 – Verifiera extraktionen (extract text from TIFF)

Efter att filerna har skrivits hjälper en snabb kontroll att säkerställa att inget gick fel.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Om du ser kodsnutten skrivas ut har du lyckats **extrahera text från TIFF** och sparat den. Därefter kan du mata JSON‑data till ett sökindex, en databas eller någon annan efterföljande tjänst.

---

## Varför använda Aspose OCR för att extrahera text från TIFF?

- **Fler‑sidigt stöd direkt ur lådan** – ingen behov av att dela upp TIFF‑filen manuellt.  
- **Hög noggrannhet** tack vare proprietära neurala nätverksmodeller.  
- **Plattformsoberoende** – fungerar på Windows, Linux och macOS .NET‑körmiljöer.  
- **Rika utdataformat** (JSON, XML, vanlig text) som passar både moderna och äldre stackar.  

Om du fortfarande är osäker, prova gratisprovet på ett exempel‑dokument. Du kommer märka hastigheten och enkelheten jämfört med öppen‑källkodsalternativ som ofta kräver extra bild‑förbehandling.

---

## Vanliga fallgropar & hur du undviker dem

| Issue | Symptom | Fix |
|-------|---------|-----|
| Låg‑upplöst TIFF | Saknade tecken, låg förtroendegrad | Skala upp bilden till ≥150 DPI före OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Fel språk | Slarviga ord, särskilt för icke‑engelsk text | Ställ in `ocrEngine.Language = Language.Spanish` (eller lämpligt) före `Recognize()` |
| Minnesbrist på stora filer | `OutOfMemoryException` | Bearbeta sidor i batcher: loopa igenom `ocrEngine.Image.Pages` och anropa `RecognizePage(i)` |
| Licens ej tillämpad | Vattenstämpel “Evaluation” i utdata | Registrera din licens: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Fullt fungerande exempel (Kopiera‑klistra redo)

Nedan är det kompletta programmet som du kan klistra in i ett nytt konsolprojekt. Det innehåller alla delar vi diskuterade—initiering, inläsning, igenkänning och sparning.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Spara filen som `Program.cs`, kör `dotnet run` och låt konsolen visa var JSON‑ och XML‑filerna hamnade. Klart—du har just slutfört ett **ocr engine‑exempel** som extraherar text från TIFF.

---

## Nästa steg & relaterade ämnen

- **Batch‑behandling:** Packa in logiken i en `foreach`‑loop för att automatiskt hantera dussintals TIFF‑filer.  
- **Sök‑integration:** Skicka JSON till Elasticsearch eller Azure Cognitive Search för att möjliggöra fulltextssökning över skannade dokument.  
- **Bild‑förbehandling:** Utforska Aspose’s `ImageProcessing`‑API för att räta upp, ta bort prickar eller justera kontrast före OCR.  
- **Alternativt utdata:** Använd `ocrResult.ToPlainText()` om du bara behöver råa strängar utan metadata.  

Om du är nyfiken på andra bildformat fungerar samma mönster för PDF‑filer (byt bara källfilen) eller PNG. Huvudpoängen är att när motorn är konfigurerad är resten en repeterbar pipeline.

## Slutsats

Vi har gått igenom ett **fullständigt OCR‑motorexempel** som låter dig **extrahera text från TIFF**‑filer med Aspose OCR, och levererar ren JSON och valfri XML för alla efterföljande arbetsflöden. Koden är självständig, förklaringarna täcker “varför” bakom varje steg

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}