---
category: general
date: 2026-04-04
description: Hoe GPU in Aspose OCR snel in te schakelen. Leer tekst uit een afbeelding
  te extraheren, afbeelding te laden voor OCR en tekst te herkennen met C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: nl
og_description: Hoe je GPU snel inschakelt in Aspose OCR. Volg deze tutorial om tekst
  uit een afbeelding te extraheren, een afbeelding te laden voor OCR, en tekst te
  herkennen met C#.
og_title: Hoe GPU voor OCR in C# in te schakelen – Complete gids
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Hoe GPU voor OCR in C# in te schakelen – Stapsgewijze gids
url: /nl/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe GPU in te schakelen voor OCR in C# – Complete Walkthrough

Heb je je ooit afgevraagd **hoe je GPU** kunt inschakelen bij het gebruik van Aspose OCR? Misschien loop je tegen een prestatie‑limiet aan bij het verwerken van honderden bonnetjes, en kan de CPU het simpelweg niet bijhouden. Het goede nieuws is dat het inschakelen van GPU‑versnelling een fluitje van een cent is, en zodra het aan staat zul je de OCR‑engine door afbeeldingen razendsnel laten gaan.

In deze tutorial laten we niet alleen de GPU‑schakelaar omzetten, maar ook hoe je **een afbeelding laadt voor OCR**, **tekst herkent**, en uiteindelijk **tekst uit een afbeelding haalt** met een helder C#‑voorbeeld. Aan het einde heb je een kant‑klaar programma dat platte tekst uit elke ondersteunde afbeelding haalt — zonder externe services.

## Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.7.2 en hoger).  
- Aspose.OCR for .NET, versie 24.2.0 of nieuwer (de GPU‑vlag werd in deze release toegevoegd).  
- Een GPU‑ingeschakelde machine met de juiste drivers (NVIDIA CUDA 11+ werkt uitstekend).  
- Een afbeeldingsbestand dat je wilt verwerken — denk aan een gescande bon, een gefotografeerde factuur, of een handgeschreven notitie.

Als je die al hebt, prima — laten we beginnen.

## Stap 1: Hoe GPU in te schakelen – Configureer de OCR‑engine

Het eerste wat je moet doen is Aspose OCR vertellen de GPU te gebruiken. Dit doe je door de `UseGpu`‑eigenschap op de `OcrEngine`‑instantie in te stellen. De eigenschap staat standaard op `false`, dus we schakelen hem expliciet in.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Waarom dit belangrijk is:** Wanneer `UseGpu` `true` is, besteedt de bibliotheek de zware matrixberekeningen uit aan de grafische processor. Op een bescheiden RTX 3060 merk je de latency dalen van enkele seconden per afbeelding naar een fractie van een seconde.

> **Pro tip:** Als je in een headless CI‑omgeving draait, zorg er dan voor dat de GPU‑driver geïnstalleerd is en dat het service‑account toestemming heeft om het apparaat te benaderen. Anders valt de engine stilletjes terug op CPU‑modus.

## Stap 2: Afbeelding laden voor OCR – Wijs de engine naar je bestand

Vervolgens moeten we **een afbeelding laden voor OCR**. Aspose OCR accepteert elk afbeeldingsformaat dat door System.Drawing wordt ondersteund (PNG, JPEG, BMP, TIFF, enz.). De helper `ImageStream.FromFile` verpakt het bestand in het vereiste stream‑object.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Als je liever laadt vanuit een `byte[]` (bijvoorbeeld wanneer de afbeelding uit een database komt), kun je in plaats daarvan `ImageStream.FromBytes(byteArray)` gebruiken — hetzelfde resultaat, alleen een andere bron.

## Stap 3: Hoe tekst te herkennen – Voer het OCR‑proces uit

Nu de engine geconfigureerd is en de afbeelding geladen, is het tijd om **tekst te herkennen**. De `Recognize`‑methode doet al het zware werk en retourneert een `OcrResult`‑object dat de platte tekst, confidence‑scores en zelfs de begrenzings‑boxen bevat als je die later nodig hebt.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Je kunt ook de taal wijzigen door `ocrEngine.Language = OcrLanguage.French;` in te stellen vóór het aanroepen van `Recognize()`. De GPU‑versnelling werkt ongeacht het taalpakket dat je laadt.

## Stap 4: Hoe tekst uit afbeelding te extraheren – Geef het resultaat weer

Tot slot **extraheren we tekst uit de afbeelding** door de `Text`‑eigenschap van het result‑object uit te lezen. Voor demonstratiedoeleinden dumpen we het gewoon naar de console, maar je kunt het naar een bestand, een database, of een andere service sturen.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Verwachte output** (jouw eigen tekst zal verschillen afhankelijk van de afbeelding):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Als je de ruwe confidence‑waarden nodig hebt, kun je `ocrResult.Regions` itereren en elke `Region.Confidence` inspecteren.

## Volledig werkend voorbeeld – Eén bestand, klaar om te draaien

Hieronder staat het complete programma. Kopieer‑en‑plak het in een nieuw console‑project, herstel het Aspose.OCR‑NuGet‑pakket, en druk op **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Opmerking:** Vervang `YOUR_DIRECTORY/receipt.jpg` door het daadwerkelijke pad naar jouw afbeelding. Als het programma een `FileNotFoundException` gooit, controleer dan het pad en de bestandsrechten.

## Veelgestelde vragen & randgevallen

### Wat als de GPU niet wordt gedetecteerd?

Aspose OCR zal automatisch terugschakelen naar CPU‑modus en een waarschuwing loggen. Om te verifiëren welke modus actief is, inspecteer `ocrEngine.IsGpuEnabled` na constructie — het retourneert `true` alleen wanneer de GPU‑driver succesvol is geladen.

### Kan ik meerdere afbeeldingen in een lus verwerken?

Zeker. Plaats de regel `ocrEngine.Image = …` gewoon binnen een `foreach (var file in files)`‑lus. Houd dezelfde `OcrEngine`‑instantie aan; hergebruik bespaart de overhead van het telkens opnieuw toewijzen van GPU‑bronnen.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Hoe ga ik om met niet‑Engelse talen?

Stel de taal in vóór het aanroepen van `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

De GPU‑versnelling werkt op dezelfde manier; alleen het taalmodel verandert.

### Wat als ik grote, hoge‑resolutie foto’s heb?

Als je tegen out‑of‑memory‑fouten aanloopt, schaal de afbeelding dan eerst down. Aspose OCR biedt `ImageHelper.Resize` – een snelle manier om te verkleinen zonder al te veel detail te verliezen.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Conclusie

We hebben behandeld **hoe je GPU** inschakelt voor Aspose OCR, laten zien hoe je **een afbeelding laadt voor OCR**, stap voor stap **tekst herkent**, en **tekst uit een afbeelding haalt** met een beknopt, productie‑klaar C#‑programma. Door de `UseGpu`‑vlag te toggelen krijg je een merkbare snelheidsboost, vooral bij het verwerken van batches bonnen, facturen, of elke high‑volume documentstroom.

Klaar voor de volgende stap? Probeer deze OCR‑pipeline te koppelen aan een database om geëxtraheerde bonnen op te slaan, of voer de platte tekst in een natural‑language‑processing‑model voor uitgaven‑categorisatie. Je kunt ook de `OcrResult.Regions`‑collectie verkennen om begrenzings‑boxcoördinaten te krijgen en een UI te bouwen die elk woord op de originele foto markeert.

Happy coding, en geniet van de extra horsepower die GPU‑versnelling aan je OCR‑werkbelasting geeft! 

---

![hoe gpu in te schakelen illustratie](gpu-ocr-diagram.png "hoe gpu in te schakelen illustratie")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}