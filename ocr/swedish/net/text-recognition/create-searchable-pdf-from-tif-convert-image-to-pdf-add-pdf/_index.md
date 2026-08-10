---
category: general
date: 2026-04-04
description: Skapa sökbar PDF från en TIF‑bild i C# – lär dig hur du konverterar bild
  till PDF, lägger till PDF‑metadata och genererar ett sökbart dokument med Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: sv
og_description: Skapa sökbar PDF från en TIF-fil med C#. Konvertera bild till PDF,
  lägg till PDF-metadata och producera ett sökbart dokument med Aspose.OCR.
og_title: Skapa sökbar PDF från TIF – Steg‑för‑steg‑guide
tags:
- Aspose.OCR
- C#
- PDF generation
title: Skapa sökbar PDF från TIF – Konvertera bild till PDF, lägg till PDF‑metadata
url: /sv/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från TIF – Fullständig C#‑genomgång

Har du någonsin behövt **skapa sökbar PDF** från en skannad faktura men varit osäker på hur du behåller texten sökbar och filmetadata organiserade? Du är inte ensam. I många automatiseringsprojekt måste PDF‑filen både vara maskinläsbar och korrekt märkt med information som titel, författare och förtroendegränser.  

I den här guiden går vi igenom en komplett lösning som **konverterar en bild till PDF**, injicerar **PDF‑metadata** och filtrerar OCR‑resultat med låg förtroendegrad — allt med Aspose.OCR‑biblioteket. I slutet har du ett färdigt kodexempel som du kan klistra in i vilket .NET‑projekt som helst, samt ett antal tips för att hantera kantfall.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+)  
- Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)  
- En TIF‑bild som du vill omvandla till en sökbar PDF (t.ex. `input.tif`)  
- Grundläggande kunskap om C# och Visual Studio (eller din föredragna IDE)

Inga andra externa tjänster krävs — hela processen körs lokalt.

## Steg 1 – Ställ in OCR‑motorn (Skapa sökbar PDF‑kärna)

Det första vi behöver är en `OcrEngine`‑instans som vet vilket språk som ska kännas igen. I de flesta affärsscenarier räcker engelska, men du kan byta `Language.English` mot vilket stödjande språk som helst.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Varför detta är viktigt:** OCR‑motorn utför det tunga arbetet med att omvandla raster‑pixlar till Unicode‑text. Att ställa in språket korrekt förbättrar noggrannheten och minskar antalet ord med låg förtroendegrad som senare filtreras bort.

> **Proffstips:** Om du bearbetar flerspråkiga dokument, skapa flera motorer eller använd `Language.Multilingual` så att Aspose hanterar språkdetection automatiskt.

## Steg 2 – Ladda TIF‑bilden (Skapa PDF från TIF)

Nu pekar vi motorn på källfilen. Hjälpmetoden `ImageStream.FromFile` läser bilden till en ström som OCR‑motorn kan konsumera.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Du kanske undrar, *“Kan jag använda en JPEG eller PNG istället?”* Absolut — Aspose.OCR stödjer de flesta rasterformat. Byt bara filändelsen så är du klar.

## Steg 3 – Konfigurera PDF‑alternativ (Lägg till metadata i PDF)

Innan konverteringen definierar vi ett `PdfOptions`‑objekt. Här **lägger vi till PDF‑metadata** som titel och författare, och vi instruerar även motorn att släppa ord vars förtroende ligger under en tröskel.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Vad händer här?**  
- `Title` och `Author` blir en del av PDF:ens dokumentinformationsordbok, vilket gör filen enklare att indexera i dokumenthanteringssystem.  
- `MinConfidence` är ett skydd: OCR läser ofta fel på svaga tecken; filtrering av dem håller det sökbara lagret rent och förbättrar efterföljande textutvinning.

Om du behöver anpassad metadata (t.ex. `Subject`, `Keywords`) kan du sätta dem via `PdfOptions.CustomProperties`.

## Steg 4 – Konvertera bilden till en sökbar PDF (Konvertera bild till PDF)

När motorn är förberedd och alternativen satta utför det sista anropet konverteringen. Det skriver en sökbar PDF till disk och bäddar in OCR‑textlagret under den ursprungliga bilden.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Efter att den här raden har körts innehåller `output.pdf`:
- Den ursprungliga TIF‑bilden som en visuell bakgrund  
- Ett osynligt textlager som sökmotorer och kopiera‑klistra‑operationer kan läsa  
- Den metadata vi definierade tidigare (titel, författare osv.)

### Förväntat resultat

Öppna den genererade PDF‑filen i Adobe Reader eller någon PDF‑visare och försök markera text. Du bör kunna kopiera meningar som matchar den ursprungliga skanningen. Dokumentets **Properties**‑dialog visar titeln “Invoice #12345” och författaren “MyCompany”.

## Steg 5 – Verifiera förtroendefiltrering (Varför MinConfidence hjälper)

Det är bra att bekräfta att ord med låg förtroendegrad faktiskt har tagits bort. Du kan inspektera PDF:ens dolda text med ett verktyg som `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Om ordet aldrig visas har `MinConfidence`‑filtret fungerat som avsett. Justera tröskeln (t.ex. `0.7f`) om du behöver ett mer aggressivt eller mer milt filter.

## Steg 6 – Hantera flera sidor (Skapa sökbar PDF från flersidig TIF)

Många fakturor kommer som flersidiga TIFF‑filer. Aspose.OCR behandlar varje ram som en separat sida automatiskt. Peka bara motorn på den flersidiga filen; samma `ConvertToSearchablePdf`‑anrop kommer att generera en flersidig sökbar PDF.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Kantfall:** Om en sida är tom kan OCR fortfarande generera ett tomt textlager, vilket är ofarligt. Du kan dock hoppa över tomma sidor genom att kontrollera `ocrEngine.HasText` innan konverteringen.

## Steg 7 – Paketera hela exemplet (Alla steg tillsammans)

Nedan är ett enda, färdigt‑att‑köra program som binder ihop allt. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen på din maskin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Kör programmet (`dotnet run` eller tryck **F5** i Visual Studio) så ser du bekräftelsemeddelandet. Den genererade PDF‑filen ligger bredvid din källbild, redo för indexering eller arkivering.

## Vanliga frågor & fallgropar

| Question | Answer |
|----------|--------|
| **Kan jag lägga till ett anpassat teckensnitt i det sökbara lagret?** | OCR‑lagret använder Unicode; den visuella framställningen styrs av den underliggande bilden, så ingen extra teckensnittsinbäddning krävs. |
| **Vad händer om min TIF är färgad?** | Aspose.OCR konverterar automatiskt färgbilder till gråskala för OCR, men du kan behålla originalfärgerna i PDF‑en genom att sätta `PdfOptions.PreserveColor = true`. |
| **Är biblioteket trådsäkert?** | Varje `OcrEngine`‑instans bör användas av en enda tråd. För parallell bearbetning, skapa en separat motor per tråd. |
| **Hur krypterar jag PDF‑en?** | Använd `PdfOptions.Security` för att sätta ett lösenord och behörigheter efter OCR‑konverteringen. |

## Nästa steg (Utöka ditt PDF‑verktygssats)

- **Batch‑bearbetning:** Loopa igenom en mapp med TIFF‑filer och generera en sökbar PDF för varje.  
- **Efterbehandling:** Använd Aspose.PDF för att slå samman de genererade PDF‑erna till ett enda huvud‑dokument.  
- **Avancerad metadata:** Fyll i anpassade XMP‑fält för bättre integration med SharePoint eller ECM‑system.  

Alla dessa tillägg bygger på det grundmönster vi just gått igenom: **skapa sökbar PDF**, **konvertera bild till PDF** och **lägga till PDF‑metadata**.

*Lycka till med kodandet! Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose.OCR‑dokumentationen för de senaste API‑uppdateringarna.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}