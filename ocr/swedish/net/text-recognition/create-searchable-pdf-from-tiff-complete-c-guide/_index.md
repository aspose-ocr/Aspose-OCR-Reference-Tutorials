---
category: general
date: 2025-12-30
description: Skapa sökbar PDF från en bild i C# – lär dig hur du konverterar TIFF
  till PDF, extraherar text från bilden och automatiserar PDF-skapande.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: sv
og_description: Skapa sökbar PDF från en bild med Aspose OCR i C#. Denna guide visar
  hur du konverterar TIFF till PDF, extraherar text och säkerställer PDF/A‑1b‑kompatibilitet.
og_title: Skapa sökbar PDF från TIFF – Steg‑för‑steg C#‑handledning
tags:
- Aspose OCR
- C#
- PDF generation
title: Skapa sökbar PDF från TIFF – Komplett C#‑guide
url: /sv/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från TIFF – Komplett C#‑guide

Har du någonsin behövt **skapa sökbar PDF** från en skannad TIFF men inte vetat var du ska börja? Du är inte ensam. Många utvecklare stöter på detta hinder när de behöver sökbara PDF‑filer för arkivering eller efterlevnad, och den goda nyheten är att lösningen är förvånansvärt enkel med Aspose OCR.

I den här handledningen går vi igenom hur du konverterar en bild till PDF, extraherar text från bilden och finputsar resultatet så att det uppfyller PDF/A‑1b‑standarder. När du är klar kan du **konvertera tiff till pdf**, **extrahera text från bild**, och du vet exakt **hur du skapar pdf**‑filer som både är sökbara och arkiveringsklara.

## Vad du behöver

- .NET 6 (eller någon nyare .NET‑version) – koden fungerar både på .NET Core och .NET Framework.  
- Aspose.OCR NuGet‑paket – installera det med `dotnet add package Aspose.OCR`.  
- En exempel‑TIFF‑fil (`input.tif`) som du vill omvandla till en sökbar PDF.  
- En utvecklingsmiljö (Visual Studio, VS Code, Rider… vilken som helst).

Det är allt. Inga extra SDK‑ar, inga externa tjänster och inga dolda konfigurationssteg.

![Skapa sökbar PDF‑exempel](image-placeholder.png "Förhandsgranskning av skapad sökbar PDF")

## Steg 1 – Initiera OCR‑motorn och ladda den engelska modellen

Innan vi kan omvandla en bild till sökbar text måste OCR‑motorn veta vilket språk den ska leta efter. Aspose OCR levereras med språkpaket som du kan ladda på begäran.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**Varför detta är viktigt:** Att ladda rätt språkmodell förbättrar igenkänningsnoggrannheten dramatiskt. Om du hoppar över detta steg faller motorn tillbaka på en generisk modell, vilket ofta ger förvrängd text – särskilt på lågupplösta TIFF‑filer.

## Steg 2 – Känn igen text från källbilden (valfritt men praktiskt)

När du kör OCR får du ett `OcrResult`‑objekt som du kan inspektera, logga eller till och med spara som vanlig text. Detta steg är valfritt om du bara bryr dig om den slutliga PDF‑en, men det är utmärkt för felsökning.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**Proffstips:** Om den extraherade texten ser felaktig ut, överväg att förbehandla bilden (räta upp, ta bort damm) innan du matar den till motorn. Aspose OCR erbjuder också bildförbättringsverktyg som du kan kedja här.

## Steg 3 – Ställ in exportören för sökbar PDF

Nu talar vi om för Aspose hur vi vill att den slutliga PDF‑en ska se ut. `SearchablePdfExporter` låter dig ange utsökväg, PDF/A‑kompatibilitet och några andra bekvämligheter.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**Varför PDF/A‑1b?** Många branscher (juridik, medicin, finans) kräver PDF‑filer som följer arkiveringsstandarder. Genom att sätta `PdfACompliance` säkerställer du att typsnitt inbäddas, färger är enhetsoberoende och filen klarar valideringsverktyg.

## Steg 4 – Exportera OCR‑resultatet direkt till en sökbar PDF

Med motorn och exportören redo är den tunga lyftningen bara en rad kod. Exportören bygger internt en PDF‑sida, lägger över den igenkända texten som ett osynligt lager och skriver filen.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**Vad händer under huven?**  
1. Den ursprungliga TIFF‑filen bäddas in som en rasterbild.  
2. Den OCR‑genererade texten placeras ovanpå, dold men valbar.  
3. Metadata (t.ex. språk) läggs till så att PDF‑läsare kan indexera texten.

## Steg 5 – Verifiera resultatet (manuell kontroll + programmatisk validering)

Det är alltid god praxis att bekräfta att PDF‑en verkligen är sökbar.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

Om du kan kopiera‑klistra texten från PDF‑visaren eller se den i konsolutskriften ovan, har du lyckats.

## Edge Cases & vanliga variationer

### Konvertera andra bildformat

Samma kod fungerar för PNG, JPEG, BMP – byt bara filändelsen i anropen till `Recognize` och `Export`. Ingen extra konfiguration behövs.

### Fler‑sidiga TIFF‑filer

Aspose OCR bearbetar automatiskt varje sida i en fler‑sidig TIFF och exportören staplar dem i en fler‑sidig PDF. Om du behöver hoppa över en sida, filtrera `ocrResult.Pages` innan export.

### Icke‑engelska språk

Byt `LanguageModel.English` mot `LanguageModel.Spanish`, `LanguageModel.French` osv., eller ladda ett eget språkpaket. Kom ihåg att justera PDF‑metadata om du riktar dig mot en specifik lokalisering.

### Minska PDF‑storlek

Om TIFF‑filerna har hög upplösning kan den resulterande PDF‑en bli skrymmande. Du kan nerprovsampling av bilden innan OCR:

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### Hantera lösenordsskyddade PDF‑filer

Om du behöver skydda utdata, omslut `SearchablePdfExporter` med Aspose.Pdf:s krypterings‑API efter export:

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som innehåller alla steg och valfria justeringar som diskuterats ovan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**Förväntat resultat:**  
- Konsolen skriver ut den råa OCR‑texten från TIFF‑filen.  
- En fil `output.pdf` dyker upp i `YOUR_DIRECTORY`.  
- När du öppnar `output.pdf` i Adobe Reader kan du markera och kopiera texten, vilket bekräftar att den är sökbar.

## Sammanfattning

Vi har gått igenom allt du behöver för att **skapa sökbar PDF** från TIFF‑bilder med Aspose OCR i C#. Från initiering av OCR‑motorn, extrahering av text, konfiguration av PDF/A‑kompatibilitet till verifiering av det slutliga dokumentet, har varje steg förklarats tydligt. Du vet nu hur du **konverterar bild till pdf**, **konverterar tiff till pdf**, **extraherar text från bild**, och det bredare svaret på **hur du skapar pdf** med sökbara lager.

## Vad du kan utforska härnäst

- **Batch‑behandling:** Lägg in logiken i en loop för att automatiskt hantera dussintals bilder.  
- **Anpassade typsnitt:** Bädda in företagets typsnitt för varumärkeskonsekvens.  
- **Molnintegration:** Spara PDF‑erna direkt i Azure Blob Storage eller AWS S3 efter skapandet.  
- **UI‑frontend:** Bygg en enkel WinForms/WPF‑app som låter användare dra‑och‑släppa bilder för omedelbar konvertering.

Känn dig fri att experimentera med olika språkmodeller, DPI‑inställningar och PDF/A‑nivåer. API‑et är tillräckligt flexibelt för att anpassas till nästan vilket arbetsflöde du kan föreställa dig.

---

*Lycklig kodning, och må dina PDF‑er alltid vara sökbara!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}