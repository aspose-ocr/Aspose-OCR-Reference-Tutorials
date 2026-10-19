---
category: general
date: 2026-02-14
description: Laad een afbeeldingsbestand en extraheer tekst van een bon met de Aspose
  OCR GPU‑engine. Leer hoe je het maximale GPU‑geheugen instelt, GPU‑geheugen configureert
  en OCR efficiënt op de afbeelding uitvoert.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: nl
og_description: Laad afbeeldingsbestand en extraheer tekst van bon met de Aspose OCR
  GPU-engine. Deze gids laat zien hoe je het maximale GPU-geheugen instelt en OCR
  op een afbeelding uitvoert in C#.
og_title: Afbeeldingsbestand laden & bontekst extraheren met GPU‑OCR in C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Afbeeldingsbestand laden & ontvangstbewijstekst extraheren met GPU‑OCR in C#
url: /nl/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afbeeldingsbestand laden & Tekst van bon extraheren met GPU OCR in C#

Heb je ooit **load image file** moeten gebruiken en de exacte tekst van een bon willen halen, maar liep je vast bij de OCR‑stap? Je bent niet de enige. In veel real‑world apps—uitgaven trackers, voorraad systemen, of zelfs eenvoudige receipt‑scanning bots—kan het snel kunnen lezen van een bonafbeelding een game‑changer zijn.  

Het goede nieuws? Met de GPU‑versnelde engine van Aspose.OCR kun je **load image file**, **set max GPU memory**, en **run OCR on image** allemaal in een paar nette regels C#. Hieronder lopen we het hele proces door, van het configureren van de GPU tot het afdrukken van de geëxtraheerde platte tekst.

## Wat je zult leren

In deze tutorial ontdek je hoe je:

* **Load image file** van schijf laden met Aspose’s `ImageStream`.
* **Configure GPU memory** zodat de engine nooit meer RAM verbruikt dan je toestaat.
* **Run OCR on image** en haal elk teken van een bon eruit.
* Veelvoorkomende valkuilen afhandelen—zoals out‑of‑memory fouten of wazige scans.
* De output verifiëren en instellingen aanpassen voor betere nauwkeurigheid.

Geen externe services, geen obscure trucjes—gewoon pure C# code die je in elk .NET 6+ project kunt plaatsen.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* .NET 6 SDK of later geïnstalleerd.
* Een geldige Aspose.OCR licentie (of je kunt de gratis evaluatiemodus gebruiken).
* De `Aspose.OCR` en `Aspose.OCR.Gpu` NuGet‑pakketten aan je project toegevoegd.
* Een voorbeeld bonafbeelding (`receipt.png`) klaar op schijf.

Als een van deze onbekend klinkt, pauzeer even en installeer de pakketten:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Dat is alles—geen extra native libraries nodig omdat de GPU‑ondersteuning rechtstreeks in het NuGet‑pakket is ingebouwd.

## Afbeeldingsbestand laden en GPU‑engine voorbereiden

Het eerste dat je moet doen is **load image file** in een `ImageStream`. Dit object abstraheert de details van het bestandssysteem en geeft de OCR‑engine een schone, in‑memory representatie.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Waarom dit belangrijk is:**  
*Loading the image file* via `ImageStream.FromFile` garandeert dat de engine de exacte pixeldata ziet, waarbij DPI en kleurdiepte behouden blijven. Deze stap overslaan of een corrupte stream voeren zal ertoe leiden dat de OCR tekens mist of uitzonderingen gooit.

> **Pro tip:** Als je te maken hebt met door gebruikers geüploade bestanden, wikkel dan de `FromFile`‑aanroep in een try‑catch‑blok en valideer eerst de bestandsgrootte. Grote afbeeldingen kunnen het GPU‑geheugen opslokken als je **configured GPU memory** niet correct hebt ingesteld.

## Max GPU‑geheugen instellen voor optimale prestaties

GPU‑bronnen zijn kostbaar, vooral op gedeelde servers of laptops met beperkt VRAM. De `MaxDeviceMemory`‑eigenschap vertelt Aspose hoeveel van het GPU‑geheugen het veilig kan toewijzen.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Wanneer je **set max GPU memory** instelt, zal de engine automatisch terugschakelen naar CPU‑verwerking als het niet aan het verzoek kan voldoen—crashes voorkomen. Dit is de veiligste manier om **configure GPU memory** te doen zonder apparaat‑specifieke limieten hard‑coded.

**Wanneer aan te passen:**  
* Als je `OutOfMemoryException` opmerkt tijdens zware batchverwerking, verlaag dan de limiet.  
* Als je bonnen een hoge resolutie hebben (300 DPI+), verhoog het naar 2 GB om de snelheid hoog te houden.

## OCR uitvoeren op afbeelding om tekst van bon te extraheren

Nu het leuke deel—echt **run OCR on image** en haal de tekst van de bon. De `Recognize`‑methode retourneert een `OcrResult`‑object dat een `Text`‑eigenschap bevat met de platte‑tekst output.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

De console zal iets tonen als:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Waarom dit werkt:**  
De GPU‑engine draait een deep‑learning model dat getraind is op verschillende documentlay-outs. Door een schone, correct geladen afbeelding te voeren, geef je het model de beste kans om **extract text from receipt** nauwkeurig te extraheren.

## Verifieer de output en veelvoorkomende valkuilen

Zelfs met een krachtige engine is OCR geen magie. Hier zijn een paar dingen om op te letten:

| Issue | Cause | Fix |
|-------|-------|-----|
| Vervormde tekens | Lage contrast of wazige afbeelding | Pre‑process met Aspose’s `ImageProcessor` om het contrast te verhogen |
| Ontbrekende regels | Afbeelding te strak bijgesneden | Zorg ervoor dat de bon volledig binnen de afbeeldingsgrenzen past |
| Out‑of‑memory fouten | `MaxDeviceMemory` te laag voor afbeeldingsgrootte | Verhoog `MaxDeviceMemory` of schaal de afbeelding eerst kleiner |
| Verkeerde taal | Bon bevat niet‑Engelse tekst | Set `gpuEngine.Language = OcrLanguage.Spanish;` (of passend) |

Als je een van deze tegenkomt, is de snelle oplossing om de afbeelding te verkleinen tot onder 2000 px aan de langste zijde—dit vermindert de GPU‑belasting drastisch zonder de leesbaarheid van de meeste bonnen op te offeren.

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma, klaar om te compileren. Vervang het bestandspad door je eigen bonlocatie.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Verwachte console‑output** (je bon zal uiteraard verschillen):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Voer het programma uit met `dotnet run`. Als je de tekst ziet afgedrukt, gefeliciteerd—je hebt met succes **load image file**, **set max GPU memory**, en **run OCR on image** uitgevoerd om **extract text from receipt**.

## Veelgestelde vragen

**Q: Werkt dit op machines zonder een dedicated GPU?**  
A: Ja. Aspose.OCR schakelt elegant terug naar CPU‑modus als er geen compatibele GPU wordt gedetecteerd. Je kunt nog steeds **load image file** en **run OCR on image** uitvoeren, alleen iets langzamer.

**Q: Kan ik meerdere bonnen in één batch verwerken?**  
A: Absoluut. Plaats de herkenningscode in een `foreach`‑lus, maar onthoud om dezelfde `GpuEngine`‑instantie te hergebruiken—dit voorkomt het opnieuw initialiseren van GPU‑bronnen voor elk bestand.

**Q: Wat als mijn bon in een andere taal dan Engels is?**  
A: Stel de taal in vóór het aanroepen van `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

## Volgende stappen & gerelateerde onderwerpen

Nu je de basis onder de knie hebt, overweeg om te verkennen:

* **Fine‑tuning OCR accuracy** – experimenteer met `gpuEngine.RecognitionOptions` zoals `EnableDeskew` of `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}