---
category: general
date: 2026-03-13
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je een
  afbeelding laadt voor OCR, OCR uitvoert op de afbeelding en Cyrillische tekst extraheert
  met duidelijke stapsgewijze code.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: nl
og_description: Tekst extraheren uit een afbeelding in C# met Aspose OCR. Deze tutorial
  laat zien hoe je een afbeelding laadt voor OCR, OCR op de afbeelding uitvoert en
  efficiënt Cyrillische tekst extraheert.
og_title: Tekst uit afbeelding extraheren met Aspose OCR – C#‑gids
tags:
- Aspose OCR
- C#
- Image Processing
title: Tekst uit afbeelding extraheren met Aspose OCR – C# programmeergids
url: /nl/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding met Aspose OCR – C# programmeergids

Heb je ooit **tekst uit afbeelding** moeten extraheren maar wist je niet welke bibliotheek Cyrillische tekens zonder problemen aankan? Je bent niet de enige. In veel projecten—factuurscanning, paspoortverificatie of snelle notities—het betrouwbaar verkrijgen van tekst uit een foto is essentieel.  

In deze gids lopen we stap voor stap door hoe je **afbeelding laadt voor OCR**, Aspose OCR configureert, **OCR uitvoert op afbeelding**, en uiteindelijk **Cyrillische tekst** extrahert met slechts een paar regels C#. Aan het einde heb je een kant-en-klare snippet die de herkende tekst naar de console print.

## Wat je zult leren

- Hoe je het Aspose OCR NuGet‑pakket installeert en referentieert.  
- De juiste manier om de engine naar de taal‑pakketbronnen te wijzen.  
- Waarom het selecteren van `Language.Cyrillic` belangrijk is voor niet‑Latijnse scripts.  
- Veelvoorkomende valkuilen (ontbrekende bronnen, niet‑ondersteunde afbeeldingsformaten) en hoe je ze kunt vermijden.  
- Een compleet, uitvoerbaar voorbeeld dat je in elk .NET‑project kunt plaatsen.

Geen ervaring met OCR is vereist, maar een basiskennis van C# en Visual Studio maakt de reis soepeler.

## Vereisten

1. **.NET 6.0** of later geïnstalleerd (de code werkt op .NET Core en .NET Framework).  
2. **Visual Studio 2022** (of elke editor die C# ondersteunt).  
3. Het **Aspose.OCR** NuGet‑pakket. Installeer het via de Package Manager Console:  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. Een map die de OCR‑taalpakketten bevat (downloadbaar vanaf de site van Aspose).  
5. Een afbeeldingsbestand (`cyrillic.png` in het voorbeeld) dat Cyrillische tekst bevat die je wilt lezen.

> **Pro tip:** Houd de map met taal‑pakketten naast de `bin`‑directory van je project; dit vereenvoudigt het padbeheer.

## Stap 1 – Afbeelding laden voor OCR

Het eerste wat je moet doen is de engine een bitmap geven om mee te werken. Aspose OCR accepteert een `ImageStream`, die direct van een bestandspad kan worden aangemaakt.

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*Waarom dit belangrijk is:* Het vroegtijdig laden van de afbeelding laat je controleren of het bestand bestaat en in een ondersteund formaat (PNG, JPEG, BMP, enz.) is. Als het bestand ontbreekt, zal de `FromFile`‑aanroep een duidelijke uitzondering werpen, waardoor je later obscure OCR‑fouten vermijdt.

## Stap 2 – OCR‑engine en bronnen instellen

Vervolgens maak je een instantie van de OCR‑engine en wijs je deze naar de map die de taal‑pakketten bevat. Zonder de juiste bronnen weet de engine niet hoe hij Cyrillische glyphs moet interpreteren.

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*Waarom dit belangrijk is:* De `SetResourcesPath`‑methode vormt de brug tussen jouw code en de data‑bestanden die de tekenvormen voor elke ondersteunde taal bevatten. Het vergeten van deze stap leidt meestal tot onsamenhangende uitvoer of een `ResourceNotFoundException`.

## Stap 3 – Taal kiezen en **OCR uitvoeren op afbeelding**

Nu kiezen we de taal die we verwachten. Omdat het voorbeeld Cyrillisch betreft, stellen we `Language.Cyrillic` in. Als je meerdere scripts moet verwerken, kun je ze combineren met een bitwise OR (`|`) operator.

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*Waarom dit belangrijk is:* Het specificeren van de taal verkleint de zoekruimte voor het OCR‑algoritme, wat zowel de snelheid als de nauwkeurigheid aanzienlijk verbetert. Wanneer je **OCR uitvoert op afbeelding** met de juiste taal‑vlag, zie je veel minder verkeerde herkenningen.

## Stap 4 – Het geëxtraheerde Cyrillische tekst ophalen en gebruiken

Na voltooiing van de herkenning slaat de engine het resultaat op in de `Text`‑eigenschap. Je kunt het nu weergeven, naar een bestand schrijven of doorgeven aan een ander systeem.

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

Typische console‑output ziet er als volgt uit:

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

Als de output onverwachte symbolen bevat, controleer dan of de taal‑pakketten overeenkomen met de versie van Aspose OCR die je hebt geïnstalleerd.

## Volledig werkend voorbeeld – Alle stappen gecombineerd

Hieronder staat het volledige programma dat je kunt kopiëren en plakken in een nieuw console‑project. Vervang `YOUR_DIRECTORY` door de daadwerkelijke paden op jouw machine.

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### Verwacht resultaat

Het uitvoeren van het programma moet exact de tekst afdrukken die in `cyrillic.png` staat. Als de afbeelding de zin “Привет, мир!” bevat, zie je die regel in de console zonder extra symbolen.

## Randgevallen & probleemoplossing

| Situatie | Wat te controleren | Aanbevolen oplossing |
|-----------|--------------------|----------------------|
| **Ontbrekende taal‑pakketten** | Wijst `resourcesPath` naar een map met `.dat`‑bestanden? | Download de pakketten opnieuw van Aspose en plaats ze in de opgegeven map. |
| **Niet‑ondersteund afbeeldingsformaat** | Is het bestand een PNG, JPEG, BMP of TIFF? | Converteer de afbeelding naar een van de ondersteunde formaten voordat je `FromFile` aanroept. |
| **Onzinnige tekens in output** | Heb je `ocrEngine.Language` correct ingesteld? | Gebruik `Language.Cyrillic` (of combineer vlaggen voor meerdere talen). |
| **Prestatie‑vertraging bij grote afbeeldingen** | Beeldresolutie > 3000 px? | Schaal de afbeelding naar een redelijke grootte (bijv. 1024 px breed) vóór OCR. |

## Gerelateerde onderwerpen die je later kunt verkennen

- **Tekst extraheren uit afbeelding** in PDF's met Aspose PDF + OCR.  
- **Afbeelding laden voor OCR** vanuit een `Stream` (handig wanneer afbeeldingen van een web‑API komen).  
- **OCR uitvoeren op afbeelding** parallel om batch‑verwerking te versnellen.  
- **Cyrillische tekst extraheren** uit handgeschreven notities met de handschriftherkenningsmodus van Aspose OCR.  
- Het resultaat integreren met **cyrillische tekst herkennen** in een database voor zoekindexering.

## Conclusie

We hebben zojuist laten zien hoe je **tekst uit afbeelding** kunt **extraheren** met Aspose OCR, van het laden van de afbeelding tot het afdrukken van de herkende Cyrillische tekens. Het korte, zelfstandige programma toont de minimale code die je nodig hebt, terwijl de tabel met probleemoplossingen je beschermt tegen de meest voorkomende obstakels.  

Probeer het op je eigen screenshots, verwissel het taal‑pakket voor Arabisch of Chinees, en zie hoe hetzelfde patroon wereldwijd werkt. Veel programmeerplezier, en moge je OCR‑resultaten altijd kristalhelder zijn! 

![Extract text from image example](extract-text-from-image.png "Extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}