---
category: general
date: 2026-01-10
description: Hoe OCR snel uit te voeren en Arabische tekst uit een afbeelding te extraheren.
  Leer hoe je een afbeelding naar tekst converteert, tekst uit een PNG leest, en zie
  hoe je tekst kunt extraheren met Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: nl
og_description: Hoe OCR uit te voeren in C# en Arabische tekst uit een PNG‑afbeelding
  te extraheren. Deze gids laat je stap voor stap zien hoe je een afbeelding naar
  tekst converteert en tekst uit een PNG leest.
og_title: Hoe OCR in C# uit te voeren – Arabische tekst uit PNG extraheren
tags:
- OCR
- C#
- Aspose
title: Hoe OCR in C# uit te voeren – Arabische tekst uit PNG extraheren
url: /nl/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in C# – Arabische tekst uit PNG halen

Heb je je ooit afgevraagd **hoe je OCR** kunt uitvoeren op een afbeelding met Arabische tekens? Je bent niet de enige. Veel ontwikkelaars komen vast te zitten wanneer ze **Arabische tekst** uit een PNG moeten **extraheren**, maar niet weten welke bibliotheek rechts‑naar‑links scripts zonder gedoe ondersteunt.  

In deze tutorial lopen we stap voor stap door alles wat je moet weten om **afbeelding naar tekst** te **converteren**, **tekst uit PNG** te **lezen**, en uiteindelijk **tekst te extraheren** met Aspose.OCR in een nette C# console‑applicatie. Aan het einde heb je een kant‑klaar programma dat de Arabische string direct naar je terminal print.

## Wat je zult leren

- Het Aspose.OCR NuGet‑pakket installeren en refereren.  
- De OCR‑engine configureren voor Arabische taalondersteuning.  
- Een PNG‑afbeelding laden en het herkenningsproces uitvoeren.  
- De geëxtraheerde tekst ophalen en weergeven.  
- Instellingen afstemmen voor betere nauwkeurigheid en veelvoorkomende valkuilen aanpakken.

Ervaring met OCR is niet vereist, alleen een basisbegrip van C# en een .NET‑ontwikkelomgeving (Visual Studio, Rider of de `dotnet` CLI volstaat).

---

## Hoe OCR uit te voeren – Aspose OCR instellen

### Stap 1: Voeg het Aspose.OCR NuGet‑pakket toe

Het eerste wat we nodig hebben is de OCR‑bibliotheek zelf. Aspose.OCR is een commercieel product, maar biedt een gratis proefversie die perfect werkt voor leerdoeleinden.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Of open de **NuGet Package Manager** in Visual Studio, zoek naar **Aspose.OCR**, en klik op **Install**.

> **Pro tip:** Als je de bibliotheek in een CI‑pipeline wilt gebruiken, voeg dan de `-v`‑vlag toe om de versie vast te zetten, bv. `dotnet add package Aspose.OCR -v 23.10`.

### Stap 2: Maak een nieuw console‑project (als je er nog geen hebt)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Nu heb je een frisse `Program.cs`‑file klaar voor onze code.

---

## Arabische tekst extraheren – De OCR‑code schrijven

Hieronder staat het volledige, kant‑klaar programma. Sla het op als `Program.cs` (of vervang het automatisch gegenereerde bestand).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Waarom elke regel belangrijk is

- **`OcrEngine`**: De centrale klasse die het laden van afbeeldingen, de taalkeuze en de herkenning coördineert.  
- **`Language = OcrLanguage.Arabic`**: Arabisch gebruikt een rechts‑naar‑links script en unieke glyphs; door de taal in te stellen, vertelt je de engine om de juiste tekenmodellen te gebruiken.  
- **`ImageStream.FromFile`**: Ondersteunt PNG, JPEG, BMP en vele andere formaten. Als je ooit moet lezen vanuit een `MemoryStream` (bijv. een geüpload bestand), vervang dan deze aanroep overeenkomstig.  
- **`Recognize()`**: Voert het zware werk uit – pixelanalyse, segmentatie en karakterclassificatie.  
- **`ocrEngine.Text`**: De uiteindelijke Unicode‑string, klaar voor verdere verwerking, opslag of weergave.

### Verwachte output

Als `arabic_sample.png` de zin “مرحبا بالعالم” (Hello World) bevat, zal de console het volgende printen:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Als de output er onduidelijk uitziet, controleer dan of de afbeelding scherp is, de taal op Arabisch staat ingesteld, en de OCR‑engine‑versie overeenkomt met de documentatie.

---

## Afbeelding naar tekst – Nauwkeurigheid verbeteren

Hoewel de standaardinstellingen voor de meeste schone scans volstaan, hebben real‑world afbeeldingen vaak extra aandacht nodig.

| Instelling | Wat het doet | Wanneer te gebruiken |
|------------|--------------|----------------------|
| `ocrEngine.Config.Preprocess = true` | Schakelt automatische binarisatie en ruisverwijdering in. | Gescande documenten met schaduwen. |
| `ocrEngine.Config.Deskew = true` | Roteert de afbeelding om een lichte kanteling te corrigeren. | Foto’s genomen onder een hoek. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Behandelt de hele afbeelding als één tekstblok. | Eenvoudige bijschriften of één‑regelige labels. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Beperkt herkenning tot alleen Arabische tekens. | Vermindert valse positieven op pagina’s met gemengde talen. |

Je kunt deze regels direct na het aanmaken van de engine toevoegen:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Tekst uit PNG lezen – Verschillende afbeeldingsbronnen afhandelen

Soms bevindt de PNG zich in een database of komt hij van een web‑request. Hier is een snelle variant die leest vanuit een `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

De rest van de workflow blijft identiek, wat betekent dat **hoe je tekst extrahert** consistent blijft, ongeacht de bron.

---

## Hoe tekst extraheren – Geavanceerde opties & randgevallen

### 1. Multi‑page PDF’s of TIFF’s

Als je een meer‑pagina document moet OCR‑en, loop dan over elke pagina:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Opmerking:** Voor dit fragment heb je het `Aspose.PDF`‑pakket nodig.

### 2. Taal automatisch detecteren

Aspose.OCR biedt ook auto‑detectie, maar dat is trager. Als je niet zeker weet of de afbeelding Arabisch of een ander script bevat, schakel het in:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

De engine probeert elk taalmodel en kiest de beste overeenkomst.

### 3. Prestatietips

- **Hergebruik het `OcrEngine`‑object** voor meerdere afbeeldingen; elke keer een nieuwe instantie maken voegt overhead toe.  
- **Voer parallel uit** alleen als je aparte engine‑instanties per thread hebt – het delen van één instantie veroorzaakt race‑conditions.

---

## Conclusie

We hebben **hoe je OCR** in C# van begin tot eind uitvoert behandeld, je laten zien hoe je **Arabische tekst** kunt **extraheren**, **afbeelding naar tekst** kunt **converteren**, **tekst uit PNG** kunt **lezen**, en antwoord gegeven op **hoe je tekst extrahert** in diverse scenario’s. De voorbeeldcode is volledig, zelfstandig en klaar om in elk .NET console‑project geplakt te worden.

Volgende stappen? Vervang `OcrLanguage.Arabic` door Korean of Serbian Cyrillic om de meertalige kracht van de bibliotheek te ervaren. Experimenteer met de preprocessing‑vlaggen om de nauwkeurigheid op ruisende scans te verhogen, of integreer de OCR‑routine in een web‑API zodat gebruikers afbeeldingen kunnen uploaden en direct tekstresultaten krijgen.

Veel programmeerplezier, en moge je OCR‑resultaten altijd kristalhelder zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}