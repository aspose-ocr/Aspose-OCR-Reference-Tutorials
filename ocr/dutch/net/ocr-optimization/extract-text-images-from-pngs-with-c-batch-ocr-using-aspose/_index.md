---
category: general
date: 2026-02-09
description: Haal snel tekst uit afbeeldingen met C# door maximale paralleliteit in
  te stellen voor batch‑OCR – leer gescande pagina’s converteren, meerdere afbeeldingen
  OCR‑verwerken en PNG‑tekst efficiënt lezen.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: nl
og_description: tekst uit afbeeldingen extraheren in C# door de maximale paralleliteit
  in te stellen. Deze tutorial laat zien hoe je gescande pagina's converteert, meerdere
  afbeeldingen OCR uitvoert en png-tekst leest met Aspose OCR.
og_title: tekst uit PNG's extraheren met C# – Complete batch‑OCR‑gids
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: tekstafbeeldingen extraheren uit PNG's met C# – Batch‑OCR met Aspose OCR
url: /nl/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit PNG's extraheren met C# – Batch OCR met Aspose OCR

Heb je ooit **tekst uit afbeeldingen** moeten **extraheren** uit een map met gescande PNG's, maar zat je vast bij de vraag “hoe maak ik het snel?”? Je bent niet de enige. In veel real‑world projecten moeten ontwikkelaars **maximale paralleliteit instellen** zodat tientallen pagina's in seconden in plaats van minuten worden verwerkt.  

In deze gids lopen we een compleet, uitvoerbaar voorbeeld door dat **gescande pagina's converteert**, **meerdere afbeelding‑OCR uitvoert**, en uiteindelijk **png‑tekst leest** zonder moeite. Geen vage “zie de docs” links—alleen code die je kunt copy‑paste, uitleg waarom elke regel belangrijk is, en tips om de gebruikelijke valkuilen te vermijden.

> **Pro tip:** Als je al ergens Aspose OCR gebruikt, zul je merken dat dezelfde `OcrEngine`‑klasse hier verschijnt, maar we passen de configuratie aan voor echte parallelle verwerking.

---

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.6+). De API werkt hetzelfde, maar nieuwere runtimes bieden betere thread‑afhandeling.  
- **Aspose.OCR for .NET** – installeer via NuGet: `Install-Package Aspose.OCR`.  
- Een map die een paar PNG‑scans bevat (`page1.png`, `page2.png`, …).  
- Een IDE of editor waar je je prettig bij voelt (Visual Studio, Rider, VS Code…).

Dat is alles. Geen extra services, geen cloud‑sleutels, alleen pure lokale verwerking.

---

## tekst uit afbeeldingen – Maximal Parallelisme Instellen voor Batch OCR

Wanneer je OCR start op meerdere bestanden, gebruikt de engine standaard één thread. Dat is veilig maar ontzettend traag. Door `MaxDegreeOfParallelism` te configureren, vertel je de engine hoeveel threads hij gelijktijdig mag starten.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Waarom 4?**  
Vier is een ideaal aantal op de meeste moderne laptops—genoeg cores om de CPU bezig te houden, maar niet zoveel dat andere processen verhongeren. Als je dit op een server met 16 cores draait, verhoog dan het aantal naar 12 of 14 voor een merkbare snelheidswinst.

---

## Gescande pagina's converteren – De Image Stream‑collectie opbouwen

Aspose verwacht elke afbeelding als een `ImageStream`. De `FromFile`‑helper leest het bestand, houdt het in het geheugen, en geeft het door aan de OCR‑engine. Je kunt ook een `MemoryStream` gebruiken als je afbeeldingen uit een database of een HTTP‑respons komen.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Randgeval:** Als een bestand ontbreekt of corrupt is, zal `FromFile` een `FileNotFoundException` gooien. Plaats de constructie in een `try/catch` als je onbetrouwbare invoer verwacht.

---

## meerdere afbeelding‑ocr – Batch OCR Uitvoeren

Nu gebeurt het zware werk. `RecognizeBatch` start tot het aantal threads dat je eerder hebt ingesteld, verwerkt elke afbeelding, en retourneert een lijst van `OcrResult`‑objecten.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Achter de schermen laadt elke thread zijn afbeelding, voert het neurale netwerk uit, en extraheert platte tekst. De volgorde van de resultaten komt overeen met de volgorde van de invoerlijst, zodat je veilig pagina 1 → resultaat 0 kunt koppelen, enzovoort.

---

## png‑tekst lezen – De Geëxtraheerde Inhoud Tonen

Tot slot lopen we door de resultaten en printen de platte tekst naar de console. Hier kun je de output naar een bestand, een database, of zelfs een downstream NLP‑service sturen.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Verwachte Console‑output

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Als je lege secties ziet, controleer dan of de PNG's geen volledig witte afbeeldingen zijn—OCR heeft contrast nodig.

---

## Praktische Tips & Veelvoorkomende Valkuilen

| Situatie | Wat te doen |
|-----------|------------|
| **Memory pressure** on large batches | Verwerk afbeeldingen in blokken van 10‑20 bestanden, roep daarna `GC.Collect()` aan als je pieken merkt. |
| **Incorrect language detection** | Stel `ocrEngine.Configuration.Language = OcrLanguage.English;` (of je doeltaal) in vóór het aanroepen van `RecognizeBatch`. |
| **Slow performance despite parallelism** | Controleer of je SSD geen I/O‑throttling heeft; lees eerst alle bestanden in het geheugen (zoals we doen met `ImageStream.FromFile`). |
| **Missing characters** | Verhoog `ocrEngine.Configuration.DPI = 300;` voor verwerking met hogere resolutie. |

---

## Voorbeeld Uitbreiden – Van PNG naar PDF of DOCX

Als je uiteindelijk **gescande pagina's** moet omzetten naar doorzoekbare PDF's, voer dan simpelweg dezelfde `ocrResults[i].PlainText` in een PDF‑bibliotheek (bijv. Aspose.PDF) en leg de tekst als een onzichtbare laag erover. Dezelfde parallelisme‑truc werkt daar ook.

---

## Volledige Broncode (Klaar om te Kopiëren‑Plakken)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Sla dit op als `BatchExample.cs`, voer `dotnet run` uit, en zie hoe je console vult met de tekst die eerder verborgen zat in die PNG‑scans.

---

## Visuele Samenvatting

![voorbeeld tekst uit afbeeldingen](images/ocr-batch.png){alt="voorbeeld tekst uit afbeeldingen"}

Het diagram toont de stroom: **PNG‑bestanden → ImageStream‑collectie → OcrEngine (max parallelisme) → OCR‑resultaten → Console / downstream opslag**.

---

## Conclusie

Je hebt nu een solide, end‑to‑end recept voor hoe je **tekst uit afbeeldingen** in C# kunt **maximale paralleliteit instellen**, **gescande pagina's converteren**, **meerdere afbeelding‑OCR** afhandelt, en **png‑tekst** efficiënt leest. De code is zelfstandig, de uitleg behandelt zowel het “hoe” als het “waarom”, en de tips voorkomen veelvoorkomende problemen.

Wat nu? Probeer de PNG‑lijst te vervangen door een dynamische `Directory.GetFiles`‑lus, experimenteer met verschillende thread‑aantallen, of voer de output in een doorzoekbare PDF. Hetzelfde patroon schaalt naar honderden pagina's met nauwelijks een extra regel code.

Heb je vragen of een lastig randgeval? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}