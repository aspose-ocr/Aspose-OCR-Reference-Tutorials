---
category: general
date: 2026-10-11
description: Leer hoe je OCR op een afbeelding uitvoert in C# met Aspose.OCR, inclusief
  het installeren van System.Drawing.Common en het extraheren van tekst uit JPG‑bestanden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: nl
lastmod: 2026-10-11
og_description: Voer OCR uit op een afbeelding in C# met Aspose.OCR. Deze gids laat
  zien hoe je System.Drawing.Common installeert, een afbeelding laadt voor OCR en
  tekst uit een JPG extraheert.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Voer OCR uit op een afbeelding in C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Hoe OCR op een afbeelding uit te voeren in C# met Aspose.OCR
url: /nl/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR op een afbeelding uit te voeren in C# met Aspose.OCR

Als je **OCR op afbeelding** bestanden in een .NET‑toepassing moet uitvoeren, laat deze gids je een volledige oplossing zien. Met Aspose.OCR kun je snel **tekst uit afbeelding** bestanden zoals JPG’s herkennen en het resultaat weergeven in een consolevenster.

Je leert hoe je:

* **System.Drawing.Common‑pakket installeren** – de bibliotheek die de `Image`‑klasse levert,
* **afbeelding laden voor OCR** – een JPEG of PNG in het geheugen lezen,
* het taalmodel configureren,
* **OCR op afbeelding uitvoeren** en uiteindelijk,
* **tekst uit JPG extraheren** en weergeven.

De stappen zijn geschreven voor .NET 6+, maar werken ook met .NET Framework 4.6.1 of hoger.

---

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6 SDK (of .NET Framework 4.6.1+) | Biedt de runtime voor de C#‑console‑applicatie. |
| Visual Studio 2022 (of een andere IDE) | Maakt het eenvoudig om NuGet‑pakketten toe te voegen en het programma uit te voeren. |
| Internetverbinding (alleen bij eerste uitvoering) | Aspose.OCR downloadt de taalmodule automatisch. |
| Een voorbeeldafbeelding met Cyrillische of Latijnse tekst (bijv. `sample_cyrillic.jpg`) | Wordt gebruikt om **tekst uit JPG** te demonstreren. |

---

## Stap 1: System.Drawing.Common‑pakket installeren

Het `System.Drawing.Common`‑NuGet‑pakket levert de `Image`‑klasse die je **afbeelding laadt voor OCR**. Open de Package Manager Console en voer uit:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Target `net6.0-windows` of voeg `<UseWindowsForms>true</UseWindowsForms>` toe aan het project‑bestand als je platform‑specifieke waarschuwingen tegenkomt op Linux/macOS.

---

## Stap 2: Het Aspose.OCR‑NuGet‑pakket toevoegen

Aspose.OCR bevat de OCR‑engine en taalmodellen. Installeer het met:

```powershell
Install-Package Aspose.OCR
```

Het pakket is lichtgewicht; de benodigde taaldataset (bijv. Cyrillisch) wordt gedownload bij de eerste keer dat je `OcrEngine.Language` instelt.

---

## Stap 3: Hoe afbeelding laden voor OCR

Het laden van de afbeelding is de eerste concrete stap voordat je **OCR op afbeelding kunt uitvoeren**. De methode `Image.FromFile` leest elk formaat dat door GDI+ wordt ondersteund, inclusief JPG, PNG, BMP en TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Als het bestand niet bestaat, wordt een `FileNotFoundException` gegooid – omring de aanroep met een try/catch‑blok voor productiecodelogica.*

---

## Stap 4: De engine configureren en **OCR op afbeelding uitvoeren**

Maak een `OcrEngine`‑instantie, selecteer het taalmodel, wijs de geladen afbeelding toe en roep `Recognize()` aan.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

De methode `Recognize()` retourneert een `OcrResult`‑object dat de geëxtraheerde tekst, vertrouwensscores en begrenzingsvakken bevat. De taalmodule wordt automatisch gedownload bij eerste gebruik, dus er zijn geen extra bestanden nodig.

---

## Stap 5: **Tekst uit JPG** extraheren en weergeven

Nu kun je **tekst uit afbeelding** herkennen en het resultaat weergeven. De eigenschap `Text` van `OcrResult` bevat de platte tekenreeks.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Verwachte console‑output

```
Recognized text:
Пример текста на кириллице
```

Als de bronafbeelding Engelse tekst bevat, zal de output de Engelse zin zijn die je in de afbeelding hebt geplaatst.

---

## Randgevallen en best‑practice‑tips

| Situatie | Aanbeveling |
|----------|-------------|
| **Grote afbeeldingen ( > 5 MB )** | Verklein de afbeelding tot ≤ 2000 px aan de langste zijde vóór OCR om geheugenverbruik te verminderen en de snelheid te verbeteren. |
| **Meerdere talen in één afbeelding** | Roep `ocrEngine.AddLanguage(OcrLanguage.English)` aan naast Cyrillisch, en stel vervolgens `ocrEngine.Language = OcrLanguage.Multilingual` in. |
| **Scans met weinig contrast** | Verhoog het contrast met `System.Drawing.Graphics` voordat je de bitmap aan de engine doorgeeft. |
| **Uitvoeren op Linux/macOS** | Zorg ervoor dat de native afhankelijkheid `libgdiplus` is geïnstalleerd (`sudo apt-get install -y libgdiplus`). |
| **Herhaalde OCR‑aanroepen** | Hergebruik dezelfde `OcrEngine`‑instantie en vervang alleen `ocrEngine.Image` om herhaald laden van de module te vermijden. |

---

## Volledig, uitvoerbaar programma

Hieronder vind je de complete console‑applicatie die alle voorgaande stappen combineert. Kopieer de code naar een nieuw C#‑console‑project, vervang het afbeeldingspad en voer het uit.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Het uitvoeren van het programma** print de herkende tekenreeks naar de console, waarmee je bevestigt dat je succesvol **OCR op afbeelding** hebt uitgevoerd en **tekst uit JPG** hebt geëxtraheerd.

---

## Conclusie

Je weet nu hoe je **OCR op afbeelding** bestanden in C# kunt uitvoeren met Aspose.OCR, van het installeren van het benodigde **System.Drawing.Common‑pakket** tot **afbeelding laden voor OCR**, het selecteren van de juiste taal en uiteindelijk **tekst uit JPG** extraheren. Dit end‑to‑end‑voorbeeld biedt een solide basis voor het bouwen van meer geavanceerde document‑verwerkings‑pijplijnen, zoals batch‑verwerking van mappen met afbeeldingen of het integreren van OCR in een web‑API.

### Wat nu?

* Verken **tekst uit afbeelding** herkennen in PDF‑bestanden door elke pagina eerst naar een afbeelding te converteren.
* Experimenteer met de `OcrEngine`‑eigenschappen `Resolution`, `Threshold` en `MaxProcessingTime` om de nauwkeurigheid bij ruisvolle scans af te stemmen.
* Combineer de OCR‑output met een natural‑language‑processing‑bibliotheek om automatisch geëxtraheerde inhoud te categoriseren.

Voel je vrij om de code aan te passen voor andere afbeeldingsformaten, foutafhandeling toe te voegen, of deze in grotere toepassingen te integreren. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}