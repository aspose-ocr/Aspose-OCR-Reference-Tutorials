---
category: general
date: 2026-03-21
description: Leer hoe je afbeeldingsbestanden kunt rechtzetten en tekstafbeeldingen
  kunt herkennen met Aspose OCR. Converteer jpg naar tekst en corrigeer de rotatie
  van afbeeldingen in een paar regels C#‑code.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: nl
og_description: Hoe je een afbeelding rechtzet en tekst uit JPEG's haalt met Aspose
  OCR. Volg deze stapsgewijze gids om jpg naar tekst te converteren en de rotatie
  van de afbeelding te corrigeren.
og_title: Hoe een afbeelding rechtzetten in C# – Snelle Aspose OCR‑tutorial
tags:
- OCR
- C#
- Aspose
title: Hoe een afbeelding rechtzetten in C# – Complete gids met Aspose OCR
url: /nl/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten in C# – Complete gids met Aspose OCR

Heb je je ooit afgevraagd **hoe je een afbeelding kunt rechtzetten** die uit een scanner kwam met een vreemde hoek? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze tekst uit bonnetjes, facturen of handgeschreven notities proberen te extraheren. Het goede nieuws is dat je met Aspose OCR de rotatie van de afbeelding kunt corrigeren en schone, doorzoekbare tekst kunt halen in slechts een handvol regels.

In deze tutorial lopen we het volledige proces door: van het installeren van de bibliotheek, het inschakelen van automatisch rechtzetten, tot het herkennen van tekst in een afbeelding en uiteindelijk het converteren van een JPG naar tekst. Aan het einde heb je een kant‑klaar console‑applicatie die **tekst jpg** bestanden herkent zonder ze eerst handmatig te roteren.

## Wat je nodig hebt

- **.NET 6.0** of later (de code werkt zowel op .NET Core als .NET Framework)  
- **Aspose.OCR for .NET** NuGet‑pakket – versie 23.12 of nieuwer wordt aanbevolen  
- Een voorbeeld **scheve JPEG** (bijv. `skewed_receipt.jpg`) geplaatst op een locatie die je app kan lezen  
- Visual Studio, VS Code, of elke C#‑editor die je verkiest  

Er zijn geen andere externe tools nodig. De bibliotheek behandelt het rechtzetten, OCR en zelfs taalherkenning intern.

![voorbeeld van afbeelding rechtzetten](/images/deskew-example.png "afbeelding rechtzetten met Aspose OCR")

## Stap 1: Het project opzetten en Aspose.OCR installeren

Om alles overzichtelijk te houden, start je een nieuw console‑project:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

De regel `dotnet add package` haalt de **Aspose.OCR**‑binaries plus alle native afhankelijkheden op. Als je op Windows werkt, krijg je de native DLL’s automatisch; op Linux/macOS heb je mogelijk het `libgdiplus`‑pakket nodig, maar dat is een eenmalige installatie.

## Stap 2: Automatisch rechtzetten inschakelen (Correcte afbeeldingrotatie)

Open nu `Program.cs` en vervang de inhoud door de onderstaande code. De sleutelregel hier is `ocrEngine.Settings.Deskew = true;` – dat is de vlag die de engine vertelt **hoe een afbeelding recht te zetten** automatisch.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Waarom rechtzetten inschakelen?

Wanneer een scanner een pagina onder een hoek binnenhaalt, is de tekstbasis scheef. Traditionele OCR‑engines zouden elk teken als een gekantelde versie lezen, waardoor de nauwkeurigheid sterk daalt. Door `Deskew = true` in te stellen, voert Aspose OCR een snelle Hough‑transformatie uit, draait de bitmap terug naar horizontaal en voert vervolgens de herkenning uit. Het resultaat is hetzelfde als wanneer je de afbeelding handmatig in Photoshop had geroteerd—alleen sneller en volledig geautomatiseerd.

## Stap 3: Tekst in afbeelding herkennen en JPG naar tekst converteren

De `Recognize`‑aanroep doet twee dingen tegelijk:

1. **Rechtzet** de afbeelding (omdat we de vlag hebben ingeschakeld).  
2. **Extraheert** de tekstinhoud, die wordt geretourneerd in een `OcrResult`‑object.

Je kunt `ocrResult.Text` behandelen als een gewone string, naar een bestand schrijven, of doorgeven aan downstream verwerkingspijplijnen. Als je de ruwe vertrouwensscores per woord nodig hebt, geeft `ocrResult.Words` je een collectie met `Confidence`‑waarden.

### Voorbeeldoutput

Als we aannemen dat `skewed_receipt.jpg` een eenvoudige bon bevat, zie je mogelijk iets als:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Let op hoe de cijfers netjes uitgelijnd zijn, ondanks dat de oorspronkelijke afbeelding ongeveer 7° is gedraaid. Dat is de magie van **correcte afbeeldingrotatie** ingebouwd in de bibliotheek.

## Stap 4: Het voorbeeld uitvoeren en resultaten verifiëren

Compileer en voer uit:

```bash
dotnet run
```

Als alles correct is ingesteld, zie je de geëxtraheerde tekst in de console afgedrukt. Als je een uitzondering krijgt zoals `FileNotFoundException`, controleer dan het pad naar je JPEG en zorg dat het bestand leesbaar is.

### Veelvoorkomende valkuilen & pro‑tips

- **Grote afbeeldingen** – Het geheugenverbruik van OCR groeit met de afbeeldingsafmetingen. Verklein te grote bestanden (bijv. > 3000 px breedte) voordat je ze aan de engine voert.  
- **Niet‑Latijnse scripts** – Standaard gaat de engine uit van Engels. Stel `ocrEngine.Settings.Language = OcrLanguage.French;` in (of een andere ondersteunde taal) als je **tekst in afbeelding** moet herkennen in andere alfabetten.  
- **Batchverwerking** – Voor veel bestanden, hergebruik dezelfde `OcrEngine`‑instantie; een nieuwe engine per bestand creëert onnodige overhead.  
- **Kwaliteitscontrole** – Na het rechtzetten kun je de gecorrigeerde bitmap exporteren via `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` om visueel de rotatiecorrectie te verifiëren.

## Volledig werkend voorbeeld (alles samen)

Hieronder staat het volledige, zelfstandige programma dat je kunt kopiëren en plakken in `Program.cs`. Het bevat commentaar, foutafhandeling en een optionele stap om de rechtgezette afbeelding op te slaan.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Het uitvoeren van het programma zal **tekst jpg** bestanden herkennen, automatisch elke scheefstand corrigeren, en schone, doorzoekbare tekst naar de console afdrukken.

## Afronding

Je hebt nu een solide, productie‑klaar fragment dat laat zien **hoe je een afbeelding kunt rechtzetten** en de inhoud ervan kunt extraheren met Aspose OCR. De aanpak werkt voor bonnetjes, facturen, gescande contracten, of elke JPEG waarbij de tekst niet perfect horizontaal staat.

Volgende stappen die je kunt verkennen:

- **Batchverwerking** van een map met JPEG’s en het schrijven van elk resultaat naar een `.txt`‑bestand (verwijst terug naar *jpeg naar tekst converteren*).  
- De OCR‑stap integreren in een ASP.NET Core API zodat clients afbeeldingen kunnen uploaden en JSON‑geformatteerde tekst ontvangen.  
- Experimenteren met verschillende OCR‑instellingen zoals `ocrEngine.Settings.Language` of `ocrEngine.Settings.RecognitionMode` om de nauwkeurigheid voor niet‑Engelse documenten te verbeteren.

Probeer het, pas de instellingen aan, en laat de engine het zware werk doen. Zoals altijd, als je tegen een probleem aanloopt of een slimme optimalisatie wilt delen, laat dan een reactie achter. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}