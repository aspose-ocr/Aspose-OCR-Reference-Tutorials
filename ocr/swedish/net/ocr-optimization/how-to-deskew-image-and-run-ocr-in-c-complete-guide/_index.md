---
category: general
date: 2026-03-07
description: Lär dig hur du räta upp en bild, ökar kontrasten och extraherar text
  från en skanning med Aspose OCR. Utför OCR på en bild med ett komplett C#‑exempel
  och ladda enkelt bilden för OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: sv
og_description: Lär dig hur du räta upp en bild, ökar kontrasten och extraherar text
  från en skanning med Aspose OCR i C#. Utför OCR på en bild med steg‑för‑steg‑kod.
og_title: Hur man räta upp bild och kör OCR i C# – Komplett guide
tags:
- C#
- OCR
- Image Processing
title: Hur man räta upp bild och kör OCR i C# – Komplett guide
url: /sv/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här räta upp bild och kör OCR i C# – Komplett guide

Om du någonsin har funderat på **how to deskew image** innan du kör OCR, så är du på rätt plats. I den här handledningen går vi igenom hur du ökar kontrasten, laddar en bild för OCR och slutligen **extract text from scan** med Aspose OCR.  

Oavsett om du digitaliserar gamla kvitton, rensar upp skannade kontrakt eller bara behöver ett pålitligt sätt att läsa text från ett snett foto, så täcker stegen nedan allt du behöver. Inga onödigheter—bara ett fungerande exempel som du kan kopiera‑klistra in i Visual Studio.  

## Vad du kommer att uppnå

* Korrigera snedvridning upp till 30° (det är **how to deskew image**‑delen).  
* Öka bildkontrast för skarpare teckenkanter (**how to boost contrast**).  
* Ladda din bild i OCR‑motorn (**load image for OCR**).  
* Kör igenkänningsprocessen och **extract text from scan**.  

Allt detta fungerar med det senaste Aspose.OCR .NET NuGet‑paketet (v23.11 vid tidpunkten för skrivandet).  

---

![Exempel på hur man räter upp bild](/images/deskew-example.png "hur man räter upp bild")

*Bilden ovan visar ett skannat dokument före och efter räta upp.*

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).  
* Visual Studio 2022 (eller någon C#‑IDE du föredrar).  
* Aspose.OCR NuGet‑paket – installera via `dotnet add package Aspose.OCR`.  

Det är allt. Inga externa tjänster, inga API‑nycklar.

---

## Så här räter du upp en bild med Aspose OCR

Det första vi gör är att skapa en **ImageProcessingPipeline** och lägga till ett `DeskewFilter`. Filtret upptäcker automatiskt den dominerande textlinjens vinkel och roterar bilden tillbaka till horisontell.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Varför detta är viktigt:**  
En sned skanning förvirrar OCR‑motorn eftersom tecknen inte längre är i linje med baslinjen. `DeskewFilter` analyserar bildens histogram, hittar vinkeln och roterar den, vilket dramatiskt förbättrar igenkänningsnoggrannheten.

> **Proffstips:** Om du vet att dina dokument aldrig överstiger en lutning på 15°, sätt `MaxAngle = 15` för att snabba upp bearbetningen.

---

## Så här ökar du kontrasten för bättre igenkänning

Efter räta upp är nästa steg att få texten att sticka ut. `ContrastBoostFilter` sträcker pixelintensitetsområdet, vilket är särskilt hjälpsamt för blekta utskrifter.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Varför det hjälper:**  
Lågkontrastskanningar ger gråaktiga tecken som binariseringen kan tolka som bakgrund. Att öka kontrasten gör mörka pixlar mörkare och ljusa pixlar ljusare, vilket ger den efterföljande `BinarizationFilter` en renare yta.

---

## Utför OCR på bild – Ladda filen

Nu när bilden är förbehandlad måste vi **load image for OCR**. Aspose erbjuder en bekväm `ImageStream.FromFile`‑hjälpmetod.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Om din bild finns i en ström (t.ex. uppladdad via ett webb‑API) kan du istället använda `ImageStream.FromStream(yourStream)`. Motorn accepterar BMP, JPEG, PNG, TIFF och många fler.

---

## Kör igenkänningsprocessen och extrahera text från skanning

När allt är kopplat, utför anropet `Recognize()` det tunga arbetet. Efter anropet är den igenkända texten tillgänglig via `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Förväntad output** (exempel för en enkel faktura):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Om resultatet ser förvrängt ut, dubbelkolla pipeline‑ordningen—räta upp först, sedan brusreducering, kontrastökning och slutligen binarisering. Att byta ordning kan försämra resultaten.

---

## Vanliga fallgropar och kantfall

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Tomt resultat** | Bilden är för mörk eller för ljus för standardmetoden för binarisering. | Öka `ContrastBoostFilter.Strength` eller byt till `BinarizationMethod.Otsu`. |
| **Delvis text saknas** | Brus kvarstår efter brusreducering. | Använd `DenoiseLevel.Medium` för mildare bilder, eller lägg till ett andra `DenoiseFilter`. |
| **Fel rotationsriktning** | Dokumentet har blandad orientering (t.ex. ett foto av en roterad sida). | Ställ manuellt `DeskewFilter.MaxAngle` lägre och förrotera bilden med `ImageProcessor.Rotate`. |
| **Prestandaavmattning** | Stort parti av högupplösta bilder. | Skala ner bilder (`ImageProcessor.Resize`) före pipeline, eller bearbeta parallellt (`Parallel.ForEach`). |

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Spara detta som `Program.cs`, kör `dotnet run` och se konsolen skriva ut resultatet för **extract text from scan**.  

---

## Nästa steg & relaterade ämnen

* **Batch processing** – Packa in ovanstående logik i en loop för att hantera dussintals filer.  
* **Custom language packs** – Om du behöver läsa icke‑latinska skript, ladda en språkmodell via `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF output** – Kombinera Aspose.PDF med OCR för att bädda in sökbar text direkt i en PDF‑fil.  
* **Performance tuning** – Experimentera med ordningen i `ImageProcessingPipeline`; ibland ger brusreducering före räta upp snabbare resultat på brusiga foton.  

Alla dessa bygger på de grundläggande koncept vi täckte: **how to deskew image**, **how to boost contrast**, **load image for OCR**, **perform OCR on image**, och slutligen **extract text from scan**.

---

## Sammanfattning

Vi har just demonstrerat ett komplett, produktionsklart sätt att **how to deskew image** och köra OCR i C#. Genom att kedja ett deskew‑filter, ett brusreduceringssteg, en kontrastökning och en binarisering får du en ren inmatning som låter Aspose OCR på ett pålitligt sätt **extract text from scan**.  

Kör koden, justera filterparametrarna för dina egna dokument, så kommer du snabbt se hur igenkänningsnoggrannheten förbättras. Har du frågor? Lämna en kommentar, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}