---
category: general
date: 2026-04-26
description: Skapa sökbar PDF från en skannad bild med Aspose OCR i C#. Lär dig hur
  du konverterar en skannad bild, extraherar text och snabbt genererar en sökbar PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: sv
og_description: Skapa sökbar PDF från en skannad bild med Aspose OCR. Steg‑för‑steg
  C#‑kod för att konvertera, extrahera text och generera en sökbar PDF.
og_title: Skapa sökbar PDF från skannad bild – C#‑guide
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Skapa sökbar PDF från skannad bild – C#‑guide
url: /sv/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från skannad bild – C#-guide

Har du någonsin behövt **skapa sökbara PDF**‑filer från papperskontrakt, kvitton eller gamla arkiv? Du är inte ensam – de flesta utvecklare stöter på detta hinder när en kund överlämnar en hög med TIFF‑skanningar och förväntar sig en sökbar PDF som slutleverans.  

I den här handledningen visar vi exakt **hur man OCR‑ar ett dokument** och omvandlar en skannad bild till en **sökbar PDF** med Aspose OCR för .NET. När du är klar kan du **konvertera skannade bild**‑filer, **extrahera text från bild**‑data och till och med hantera fler‑sidiga TIFF‑filer utan problem.

## Vad du behöver

Innan vi sätter igång, se till att du har:

* .NET 6.0 eller senare (API:et fungerar med .NET Core, .NET Framework och .NET 5+).  
* En giltig Aspose OCR‑licens eller så är du nöjd med utvärderingsvattentäcket.  
* NuGet‑paketet `Aspose.OCR` installerat (`dotnet add package Aspose.OCR`).  
* En exempel‑TIFF‑fil (t.ex. `contract_scan.tif`) som du vill omvandla till en sökbar PDF.

Det är allt – inga extra bibliotek, ingen galen konfiguration. Är du redo? Kör igång.

![Exempel på skapad sökbar PDF](create-searchable-pdf.png "exempel på skapad sökbar pdf")

## Steg 1 – Initiera OCR‑motorn (Create Searchable PDF)

Först och främst: du behöver en `OcrEngine`‑instans. Detta objekt är arbetshästen som läser bitmapen, identifierar tecken och ger dig tillbaka texten.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Varför ange språk?**  
Om du låter standardvärdet stå kommer Aspose att testa alla språkpaket, vilket saktar ner processen. Genom att specificera `Language.Latin` säger du åt motorn att fokusera på det latinska alfabetet, vilket ger dig snabbare prestanda och mer korrekta resultat för engelskspråkiga kontrakt.

## Steg 2 – Läs in din skannade bild (Convert Scanned Image)

Nu matar vi motorn med bilden vi vill bearbeta. Aspose kan läsa en filsökväg, en ström eller till och med en `byte[]`. För enkelhetens skull använder vi `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Om du någon gång behöver **konvertera TIFF till PDF** senare, tänk på att fler‑sidiga TIFF‑filer hanteras automatiskt – varje ram blir en separat PDF‑sida.

## Steg 3 – Kör OCR och hämta texten (Extract Text From Image)

Att köra OCR är lika enkelt som att anropa `Recognize`. Motorn returnerar ett `RecognitionResult` som innehåller ren text, förtroendescore och layoutinformation.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Proffstips:** Om du bara behöver texten (ingen PDF), kan du stanna här och skriva `extractedText` till en `.txt`‑fil. Men oftast är målet en sökbar PDF, så vi fortsätter.

## Steg 4 – Spara som en sökbar PDF (Create Searchable PDF)

Aspose gör sista steget trivialt: anropa bara `Save` med `SaveFormat.PdfSearchable`. Under huven bäddar biblioteket in den extraherade texten som ett osynligt lager samtidigt som det bevarar bildens ursprungliga utseende.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

När du öppnar `contract_searchable.pdf` i någon PDF‑visare kan du markera, kopiera och söka i texten – exakt vad en kund förväntar sig av en “sökbar PDF”.

## Hantera fler‑sidiga TIFF‑filer (Convert Tiff to PDF)

Om din källfil innehåller flera sidor behandlar Aspose varje ram som en separat sida automatiskt. Inga extra loopar behövs. Du kan dock vilja styra DPI eller bildkvalitet för varje sida:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Efter att du har ställt in dessa alternativ, upprepa **Steg 2** för varje ram, eller peka helt enkelt `ImageStream.FromFile` på den fler‑sidiga TIFF‑filen och låt Aspose göra det tunga lyftet.

## Vanliga fallgropar och hur du löser dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-------|
| Text är förvrängd eller saknas | Fel språk inställt | Ställ in `ocrEngine.Language` till rätt språkpaket (t.ex. `Language.German`). |
| PDF är enorm (10 MB för en enkel‑sidig skanning) | Standardkomprimeringen för bild är låg | Justera `ocrEngine.ImageProcessingOptions.Compression` till `Jpeg` och sätt ett rimligt `Quality`‑värde (0‑100). |
| OCR kör väldigt långsamt | Använder standard‑`Auto` språkdetektering | Ange explicit det språk du förväntar dig. |
| Inget sökbart lager visas | Sparat med `SaveFormat.Pdf` istället för `PdfSearchable` | Använd `PdfSearchable`. |

## Fullt end‑to‑end‑exempel

Här är hela koden samlad till en körbar konsolapp som du kan kopiera och klistra in i Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Vad du kommer att se:**  
* Ett konsolfönster som skriver ut ett utdrag av den OCR‑ade texten.  
* En `contract_searchable.pdf`‑fil som ligger bredvid din ursprungliga TIFF. Öppna den, tryck **Ctrl + F**, och sök efter vilket ord som helst som fanns i den ursprungliga skanningen – voilà, det fungerar.

## Nästa steg & relaterade ämnen

* **Hur man OCR‑ar dokument** i batch – omslut koden ovan i en `foreach`‑loop och bearbeta en hel mapp.  
* **Konvertera skannade bild**‑format andra än TIFF (PNG, JPEG) – samma API fungerar; byt bara filändelsen.  
* **Extrahera text från bild** för vidare analys – skicka `result.Text` till en naturlig språk‑behandlingspipeline.  
* **Optimera PDF‑storlek** – utforska `PdfSaveOptions` för att komprimera bilder ytterligare eller bädda in typsnitt endast när det behövs.  

Experimentera med dessa idéer, så blir du snabbt go‑to‑personen för alla “omvandla den här skanningen till en sökbar PDF”‑förfrågningar.

---

### TL;DR

Du vet nu hur du **skapar sökbara PDF**‑filer från skannade bilder med Aspose OCR i C#. Processen är: initiera motorn, läs in bilden, kör OCR och spara med `PdfSearchable`. Justera språkinställningar, DPI och komprimering för att hantera kantfall, och du är redo att **konvertera skannad bild**, **extrahera text från bild** och till och med **konvertera TIFF till PDF** i skala. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}