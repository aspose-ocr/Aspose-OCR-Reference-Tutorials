---
category: general
date: 2026-08-22
description: Leer tekst uit een afbeelding te herkennen met Aspose.OCR. Deze gids
  behandelt ook OCR van afbeelding naar tekst en het extraheren van tekst uit jpg
  in een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: nl
lastmod: 2026-08-22
og_description: Herken tekst in een afbeelding met Aspose.OCR in C#. Volg deze tutorial
  om een afbeelding naar tekst te OCR’en, tekst uit een jpg te extraheren en Cyrillische
  tekstafbeeldingen te lezen.
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: Tekst herkennen uit afbeelding met Aspose.OCR – stapsgewijze C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Hoe tekst uit een afbeelding te herkennen met Aspose.OCR in C#
url: /nl/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Herken tekst van afbeelding met Aspose.OCR – volledige C# tutorial

Als je tekst van een afbeelding moet herkennen in een .NET‑project, laat deze tutorial je een kant‑en‑klaar werkende oplossing zien. Je ziet hoe je de OCR‑engine instelt, de juiste taalmodule kiest en de geëxtraheerde tekens uitvoert. Het voorbeeld toont ook hoe je een afbeelding naar tekst OCR‑t voor een Cyrillisch plaatje, wat het veelvoorkomende geval van het lezen van Cyrillische tekst‑afbeeldingsbestanden dekt.

Naast de kernstappen leer je hoe je tekst uit jpg‑bestanden kunt extraheren, afbeelding naar tekst kunt converteren voor andere formaten, en situaties kunt afhandelen waarbij de taalmodule automatisch moet worden gedownload. Er zijn geen externe services vereist, behalve het Aspose.OCR NuGet‑pakket.

## Vereisten

- .NET 6.0 SDK of later geïnstalleerd  
- Visual Studio 2022 (of een andere editor die C# ondersteunt)  
- Internettoegang voor de eerste uitvoering (de Cyrillische taalmodule wordt op aanvraag opgehaald)  
- Het Aspose.OCR NuGet‑pakket (`dotnet add package Aspose.OCR`)  

Deze items stellen je in staat de code te compileren en uit te voeren zonder extra configuratie.

## Stap 1: Maak een nieuw console‑project

Open een terminal en voer de volgende commando's uit om een minimale console‑applicatie te genereren:

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

Het commando `dotnet new console` maakt een `Program.cs`‑bestand en een projectbestand dat verwijst naar de Aspose.OCR‑bibliotheek. Het toevoegen van het pakket lost alle benodigde assemblies op.

## Stap 2: Importeer de Aspose.OCR‑namespace

Bewerk **Program.cs** en voeg de `using Aspose.OCR;`‑directive toe aan de bovenkant van het bestand. Hierdoor zijn de OCR‑klassen beschikbaar zonder volledig gekwalificeerde namen.

```csharp
using System;
using Aspose.OCR;
```

De `using`‑statement verbetert de leesbaarheid en houdt de code gericht op de OCR‑workflow.

## Stap 3: Initialise de OCR‑engine

Instantieer `OcrEngine`. De engine bevat configuratie zoals de taalmodule en herkenningsinstellingen.

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

Het één keer aanmaken van de engine per applicatie is efficiënt omdat de onderliggende native bibliotheken slechts één keer worden geladen.

## Stap 4: Selecteer de taalmodule

Voor Cyrillische tekst stel je de `Language`‑eigenschap in op `Language.Cyrillic`. Aspose.OCR downloadt de module automatisch als deze ontbreekt, dus de eerste uitvoering kan enkele seconden duren.

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

Als je later een afbeelding naar tekst wilt OCR‑en in een andere taal (bijv. Engels of Arabisch), vervang je `Language.Cyrillic` door de juiste enum‑waarde. Deze flexibiliteit stelt je in staat afbeelding naar tekst te converteren voor elk ondersteund script.

## Stap 5: Herken tekst van een JPG‑bestand

Roep `RecognizeImage` aan met het volledige pad naar de afbeelding. De methode retourneert een `OcrResult` die de geëxtraheerde tekenreeks bevat.

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

De aanroep werkt met elk raster‑afbeeldingsformaat dat door Aspose.OCR wordt ondersteund (JPG, PNG, BMP, TIFF). Het gebruik van een JPG zorgt ervoor dat je tekst uit jpg‑bestanden kunt extraheren zonder extra conversiestappen.

## Stap 6: Output de herkende tekst

Schrijf tenslotte de herkende tekst naar de console. Dit toont een eenvoudige manier om een Cyrillisch tekst‑afbeelding te lezen en weer te geven.

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

Wanneer je het programma uitvoert, zou je de Cyrillische tekens exact moeten zien zoals ze in de bronafbeelding staan.

## Volledig werkend voorbeeld

Hieronder staat het volledige **Program.cs**‑bestand dat je direct kunt kopiëren, plakken en uitvoeren.

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### Verwachte output

```
Recognised text:
Пример текста на кириллице
```

De exacte output hangt af van de inhoud van `sample_image.jpg`. Als de afbeelding Engelse tekst bevat, zal dezelfde code de Engelse tekenreeks retourneren zolang je `ocrEngine.Language = Language.English;` instelt.

## Veelvoorkomende valkuilen behandelen

| Probleem | Waarom het gebeurt | Hoe op te lossen |
|----------|--------------------|------------------|
| Taalmodule niet gevonden | De eerste uitvoering probeert de module te downloaden, maar het proces mislukt door firewall‑beperkingen. | Zorg ervoor dat de machine `https://downloads.aspose.com/ocr` kan bereiken of download de module handmatig van het Aspose‑portaal en plaats deze in de standaardmap (`%APPDATA%\Aspose\OCR\`). |
| Lage nauwkeurigheid bij ruisende afbeeldingen | OCR‑engines vertrouwen op duidelijk contrast tussen tekst en achtergrond. | Pre‑process de afbeelding (bijv. contrast verhogen, converteren naar grijstinten) voordat je `RecognizeImage` aanroept. Aspose.OCR biedt `ImagePreprocessing`‑opties die je kunt verkennen. |
| Niet‑JPG‑formaten | Sommige ontwikkelaars gaan ervan uit dat de code alleen met JPG‑bestanden werkt. | De API accepteert ook PNG, BMP en TIFF. Pas de bestandsextensie in `imagePath` hierop aan. |
| Grote bestanden veroorzaken lange verwerkingstijd | Grotere afbeeldingen vereisen meer geheugen en CPU‑cycli. | Verklein de afbeelding tot een redelijke resolutie (bijv. 1500 × 1500) vóór herkenning. |

Deze tips helpen je om afbeelding naar tekst betrouwbaar te converteren in verschillende scenario's.

## De oplossing uitbreiden

Zodra je tekst van een afbeelding kunt herkennen, wil je misschien:

- **Resultaat opslaan naar een bestand** – schrijf `result.Text` naar een `.txt`‑ of `.docx`‑document.  
- **Batchverwerking van een map** – loop door alle bestanden in een map en pas dezelfde OCR‑logica toe.  
- **Combineren met reguliere expressies** – extraheer telefoonnummers, datums of andere patronen uit de herkende tekenreeks.  

Al deze uitbreidingen hergebruiken dezelfde kerncode, waardoor de implementatie beknopt blijft.

## Conclusie

Je hebt nu een volledige gids om tekst van een afbeelding te herkennen met Aspose.OCR in C#. De tutorial besprak hoe je het project opzet, de OCR‑engine initialiseert, de Cyrillische taalmodule selecteert en tekst uit een JPG‑bestand extraheert. Door deze stappen te volgen kun je ook afbeelding naar tekst OCR‑en voor andere talen, tekst uit jpg‑bestanden extraheren en afbeelding naar tekst converteren in elke .NET‑applicatie.

Voel je vrij om te experimenteren met extra talen, grotere batches of post‑processinglogica. Als je een Cyrillische tekst‑afbeelding moet lezen in een andere context — bijvoorbeeld een web‑API of een Windows‑service — geldt hetzelfde patroon. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Afbeeldingstekst extraheren C# met taalkeuze via Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [tekst van afbeelding herkennen met Aspose OCR voor meerdere talen](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [ocr-preprocessing-pijplijn – Hoe tekst van afbeelding te herkennen in C#](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}