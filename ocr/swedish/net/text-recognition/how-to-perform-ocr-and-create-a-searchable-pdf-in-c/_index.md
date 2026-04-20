---
category: general
date: 2026-02-14
description: Lär dig hur du utför OCR på en TIFF eller bild och konverterar PDF med
  OCR för att skapa en sökbar PDF—steg‑för‑steg C#‑guide.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: sv
og_description: Upptäck hur du utför OCR på bilder, konverterar PDF med OCR och skapar
  en sökbar PDF med Aspose OCR i en kortfattad C#‑handledning.
og_title: Hur man utför OCR och skapar en sökbar PDF i C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Hur man utför OCR och skapar en sökbar PDF i C#
url: /sv/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR och skapar en sökbar PDF i C#

Har du någonsin behövt **utföra OCR** på ett skannat dokument men varit osäker på hur du omvandlar resultatet till en sökbar PDF? Du är inte ensam – många utvecklare stöter på detta hinder när de arbetar med äldre TIFF‑arkiv eller PDF‑filer som bara innehåller bilder. Den goda nyheten? Med några rader C#‑kod och Aspose.OCR‑biblioteket kan du konvertera en TIFF eller någon annan bild till en fullt sökbar PDF på några sekunder.

I den här handledningen går vi igenom allt du behöver veta: från installation av biblioteket, inläsning av en flersidig TIFF, till att anropa `RecognizeToPdf` så att du kan **konvertera PDF med OCR** och **skapa sökbara PDF**‑filer som dina användare faktiskt kan söka i. I slutet har du en färdig konsolapp som producerar en sökbar PDF från en bildkälla.

## Förutsättningar

- **.NET 6.0** eller senare (koden fungerar även på .NET Framework 4.7+).
- En giltig **Aspose.OCR**‑licens eller en tillfällig utvärderingsnyckel (gratisprovversionen räcker för testning).
- Visual Studio 2022 (eller någon annan editor du föredrar) med **NuGet**‑pakethanteraren.
- En indatafil med namnet `input.tif` placerad i en mapp du kontrollerar – flersidiga TIFF‑filer fungerar direkt.

> **Proffstips:** Om du kör Windows, kopiera TIFF‑filen till samma mapp som den kompilerade `.exe`‑filen för att undvika problem med sökvägar.

## Steg 1: Installera Aspose.OCR NuGet‑paketet

Öppna projektmappen i en terminal och kör:

```bash
dotnet add package Aspose.OCR
```

Detta hämtar den senaste stabila versionen (från och med februari 2026 är det 23.10) och lägger till alla nödvändiga beroenden. När återställningen är klar ser du `Aspose.OCR` listad under **Dependencies** i Solution Explorer.

## Steg 2: Skapa en minimal konsolapplikation

Skapa ett nytt konsolprojekt om du inte redan har ett:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Byt ut den automatiskt genererade `Program.cs` mot den kompletta koden som visas i **Steg 3**. Programmet kommer att:

1. Instansiera OCR‑motorn.
2. Ladda källbilden (eller flersidig TIFF).
3. Köra OCR och skriva utdata direkt till en sökbar PDF.
4. Informera användaren om att processen lyckades.

## Steg 3: Fullständig fungerande kod – Från bild till sökbar PDF

Nedan är den **fullständiga** källfilen. Kopiera‑och‑klistra den i `Program.cs`. Kommentarer finns för att förklara de mindre uppenbara delarna.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Vad du kommer att se:** Efter att programmet har körts skapas en fil som heter `searchable.pdf` i mål‑mappen. Öppna den i Adobe Reader eller någon annan PDF‑läsare och försök söka efter ett ord som finns i den ursprungliga TIFF‑filen. Texten bör hittas omedelbart, vilket visar att du framgångsrikt **gjort en sökbar PDF** från en bild.

### Köra appen

```bash
dotnet run
```

Om allt är korrekt konfigurerat får du:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Öppna PDF‑filen, tryck `Ctrl+F`, skriv in ett ord från källan och se hur markeringen hoppar till rätt plats.

## Steg 4: Vanliga variationer och kantfall

### Konvertera en vanlig PDF (endast bild) till sökbar PDF

Om din källa är en PDF som innehåller skannade bilder snarare än text kan du fortfarande använda samma metod – byt bara ut `ImageStream`‑källan:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Det uppfyller scenariot **konvertera PDF med OCR** utan extra kod.

### Hantera stora flersidiga dokument

För dokument som överstiger några hundra sidor, överväg:

- **Öka minnesgränser** (`Engine.MemoryLimit = 2_000; // MB`).
- **Bearbeta i delar**: ladda en delmängd av sidor, skriv mellansteg‑PDF‑filer och slå sedan ihop dem med ett PDF‑bibliotek (t.ex. Aspose.PDF).

### Arbeta med språk som inte är engelska

Aspose.OCR stödjer många språk direkt. Ställ in språket före igenkänning:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Om du behöver **tiff till sökbar pdf** i ett icke‑latinskt skriftsystem, se till att rätt språkpaket är installerat.

### Vad gör man om den genererade PDF‑filen är tom?

- Kontrollera att indatafilen inte är skadad.
- Säkerställ att OCR‑motorn har en giltig licens – utvärderingsläge kan införa sidbegränsningar.
- Kontrollera att bildens upplösning är minst 300 dpi; lägre upplösning kan ge dålig igenkänning.

## Steg 5: Verifiera resultatet programatiskt (valfritt)

Ibland vill du bekräfta att PDF‑filen faktiskt innehåller ett textlager. Du kan använda Aspose.PDF för att extrahera text:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Om `extracted` inte är tomt har du framgångsrikt **gjort en sökbar pdf**.

## Slutsats

Vi har gått igenom **hur man utför OCR** på en TIFF (eller någon bild) och sömlöst **konverterar PDF med OCR** för att skapa en **sökbar PDF** som beter sig som ett inbyggt dokument. Nyckelstegen är:

1. Installera Aspose.OCR.  
2. Initiera `Engine`.  
3. Ladda bilden via `ImageStream`.  
4. Anropa `RecognizeToPdf`.  

Därefter kan du experimentera med språkinställningar, stor batch‑bearbetning eller kombinera utdata med andra PDF‑manipuleringsuppgifter. Samma mönster fungerar för **tiff till sökbar pdf**, **sökbar pdf från bild**, och även skannade PDF‑filer.

Klar för nästa utmaning? Prova att bädda in OCR i ett webb‑API så att användare kan ladda upp skanningar och få sökbara PDF‑filer direkt, eller utforska OCR på handskrivna anteckningar med `OcrEngine`‑s avancerade inställningar. Möjligheterna är oändliga – lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}