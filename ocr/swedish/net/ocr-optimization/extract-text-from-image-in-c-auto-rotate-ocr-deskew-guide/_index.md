---
category: general
date: 2026-03-29
description: Extrahera text från en bild med Aspose OCR i C#. Lär dig automatisk rotation
  av OCR och hur du räta upp en skannad bild för perfekta resultat.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: sv
og_description: Extrahera text från en bild med Aspose OCR. Denna guide visar automatisk
  rotering av OCR och hur man räta upp en skannad bild i C#.
og_title: Extrahera text från bild i C# – Auto‑rotera OCR & räta upp
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahera text från bild i C# – Guide för automatisk rotation, OCR och korrigering
  av snedvridning
url: /sv/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i C# – Auto‑Rotate OCR & Deskew Guide

Har du någonsin behövt **extrahera text från bild** men filen kom in i en konstig vinkel? Det är ett vanligt huvudvärk—särskilt när du hanterar skannade fakturor, fotograferade kvitton eller sneda PDF-filer. Den goda nyheten är att du inte behöver skriva en egen rotationsalgoritm. Genom att använda Aspose OCR:s inbyggda *auto rotate OCR*-funktion kan du låta motorn räta upp bilden och sedan **extrahera text från bild** i ett smidigt steg.  

I den här handledningen går vi igenom ett komplett, färdigt C#‑program som:

* Initierar OCR‑motorn med automatisk orientering och deskew,
* Känner igen en roterad eller sned bild,
* Returnerar både den upptäckta rotationsvinkeln och den extraherade texten.

Inga externa tjänster, ingen krånglig matematik—bara några rader kod och en tydlig förklaring av *how to deskew scanned image* när det behövs.

## Vad du behöver

| Förutsättning | Varför det är viktigt |
|--------------|-----------------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR levereras som ett NuGet‑paket som riktar sig mot dessa runtime‑miljöer. |
| Visual Studio 2022 (or any C# editor) | Gör det enkelt att lägga till NuGet‑paket och köra konsol‑appen. |
| A sample image (`rotated_document.jpg`) | Filen bör vara en JPEG, PNG, BMP eller TIFF som inte är helt upprätt. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Tillhandahåller `OcrEngine`, `PreprocessingFilters` och relaterade typer. |

Om du har kryssat i dessa rutor är du redo att köra. Annars, hämta den senaste Aspose OCR från NuGet—det är en installation med ett klick.

---

## Steg 1 – Initiera OCR‑motorn (Primärt nyckelord i handling)

Det första vi gör är att skapa en `OcrEngine`‑instans och tala om för den att **auto rotate OCR** och **deskew** alla inkommande bilder. De två flaggorna kombineras med en bitvis OR (`|`) eftersom `PreprocessingFilters` är en enum med attributet `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Why this matters:**  
> *Auto‑rotate OCR* inspects the image’s text baseline, guesses the correct orientation, and rotates it internally before recognition.  *Auto‑deskew* does the same for slight slants that often appear in scanned documents.  By enabling both, you guarantee the best possible **extract text from image** results without manual image editing.

> **Varför detta är viktigt:**  
> *Auto‑rotate OCR* granskar bildens textrad, gissar rätt orientering och roterar den internt innan igenkänning. *Auto‑deskew* gör samma sak för små lutningar som ofta förekommer i skannade dokument. Genom att aktivera båda garanterar du bästa möjliga **extrahera text från bild**‑resultat utan manuell bildredigering.

---

## Steg 2 – Känn igen bilden och hämta resultatet

Nu ger vi motorn en filsökväg. Metoden `RecognizeImage` returnerar ett `OcrResult`‑objekt som innehåller den upptäckta rotationsvinkeln, förtroendescore och den rena texten.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** If you’re working with a stream (e.g., an uploaded file), use `ocrEngine.RecognizeImage(Stream)` instead.  The same preprocessing flags apply, so you still get **auto rotate OCR** benefits.

> **Tips:** Om du arbetar med en ström (t.ex. en uppladdad fil), använd `ocrEngine.RecognizeImage(Stream)` istället. Samma förbehandlingsflaggor gäller, så du får fortfarande fördelarna med **auto rotate OCR**.

---

## Steg 3 – Visa rotationsvinkeln och den extraherade texten

Till sist skriver vi ut två bitar information till konsolen: vinkeln motorn tror att bilden behövde roteras, och den faktiska texten den extraherade.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Förväntad output** (dina siffror kommer att skilja sig beroende på inmatningsbilden):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Om bilden redan var upprätt kommer rotationsvinkeln att vara `0°`, och du får fortfarande ren text tack vare *auto‑deskew*-algoritmen.

---

## Steg 4 – Förstå hur man deskewar skannad bild (Sekundärt nyckelord djupdykning)

Du kanske undrar *how to deskew scanned image* när OCR‑motorn rapporterar en icke‑noll rotation. Under huven använder Aspose OCR en **Hough transform** för att upptäcka den dominerande textradens orientering. Den roterar sedan bitmapen med den inversa vinkeln, vilket effektivt räta upp texten.

**När är det viktigt?**  
* Skannrar som matar in papper med en liten vinkel (vanligt på kontor).  
* Smartphone‑foton tagna för hand—horisonten är sällan perfekt.  

**Edge case handling:**  
Om resultatets `RotationAngle` är ovanligt stor (t.ex. > 45°) kan motorn ha missuppfattat bilden (kanske är det en logotyp eller en icke‑textgrafik). I så fall kan du:

1. Manuellt rotera bilden med `System.Drawing` innan du skickar den till motorn, eller  
2. Inaktivera `AutoRotate` och bara behålla `AutoDeskew` om du vet att dokumentet redan är upprätt.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Steg 5 – Vanliga fallgropar & Pro‑tips (E‑E‑A‑T i handling)

| Fallgrop | Varför det händer | Lösning |
|----------|-------------------|---------|
| **Blurry or low‑resolution images** | OCR accuracy drops dramatically; rotation detection may fail. | Use at least 300 dpi scans; apply a sharpening filter before OCR. |
| **Suddiga eller lågupplösta bilder** | OCR‑noggrannheten sjunker dramatiskt; rotationsdetektering kan misslyckas. | Använd minst 300 dpi‑skanningar; applicera ett skärpande filter innan OCR. |
| **Mixed languages** | The engine defaults to English; foreign characters become garbled. | Set `Language = Language.English | Language.Spanish` (or appropriate combination). |
| **Blandade språk** | Motorn använder som standard engelska; utländska tecken blir förvrängda. | Ställ in `Language = Language.English | Language.Spanish` (eller lämplig kombination). |
| **Large files (> 10 MB)** | Memory pressure can cause `OutOfMemoryException`. | Downscale the image first, or process in tiles using `OcrEngine.RecognizeRegion`. |
| **Stora filer (> 10 MB)** | Minnesbelastning kan orsaka `OutOfMemoryException`. | Skala ner bilden först, eller bearbeta i rutor med `OcrEngine.RecognizeRegion`. |
| **Incorrect file path** | `FileNotFoundException` stops the program. | Use `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` for robustness. |
| **Felaktig filsökväg** | `FileNotFoundException` stoppar programmet. | Använd `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` för robusthet. |

> **Pro tip:** Always log `ocrResult.RotationAngle` and `ocrResult.Confidence` (if available).  Those metrics help you decide whether a retry with different preprocessing settings is worth it.

> **Pro‑tips:** Logga alltid `ocrResult.RotationAngle` och `ocrResult.Confidence` (om tillgängligt). Dessa mått hjälper dig avgöra om ett nytt försök med andra förbehandlingsinställningar är värt det.

---

## Steg 6 – Utöka exemplet (Vad blir nästa?)

Nu när du kan **extrahera text från bild** med auto‑rotation och deskew, överväg följande nästa steg:

* **Batch processing** – Loopa igenom en mapp med bilder, lagra varje resultat i en databas, och flagga de med `RotationAngle > 5°` för manuell granskning.  
* **PDF conversion** – Kombinera den extraherade texten med originalbilden till en sökbar PDF med Aspose.PDF.  
* **Language detection** – Använd Aspose.OCR:s `AutoDetectLanguage`‑flagga för att låta motorn automatiskt välja bästa språk.  

Varje steg bygger på samma grundprincip: låt biblioteket hantera orienteringen, och du fokuserar på affärslogiken.

---

## Fullt fungerande exempel (Klar att kopiera och klistra in)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spara filen som `Program.cs`, kör `dotnet add package Aspose.OCR`, och sedan `dotnet run`. Du bör se vinkeln och den rena texten skriven till konsolen.

---

## Slutsats

Vi har just demonstrerat hur man **extraherar text från bild** i C# medan Aspose OCR tar hand om *auto rotate OCR* och det knepiga *how to deskew scanned image*-problemet. Genom att aktivera de två förbehandlingsflaggorna räta motorn automatiskt upp krokiga bilder, upptäcker korrekt orientering och levererar exakt text—utan manuell bildredigering.

Känn dig fri att experimentera med större batcher, olika språk eller till och med integrera resultatet i en sökbar PDF. Möjligheterna är oändliga när OCR‑motorn sköter det tunga lyftet åt dig.

**Redo att ta ditt dokumentflöde till nästa nivå?** Hämta koden, peka den mot dina egna skanningar, och se rotationsvinklarna försvinna. Om du stöter på problem, lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}