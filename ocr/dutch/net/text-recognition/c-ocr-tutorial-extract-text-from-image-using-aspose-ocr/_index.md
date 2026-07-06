---
category: general
date: 2026-03-26
description: c# ocr‑tutorial die laat zien hoe je tekst uit een afbeelding haalt,
  tekst herkent uit een jpeg en een afbeelding laadt voor ocr – bevat Cyrillische
  ondersteuning.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpeg
- load image for ocr
- recognize cyrillic text
language: nl
og_description: c# OCR-tutorial die je stap voor stap begeleidt bij het laden van
  een afbeelding voor OCR, het herkennen van tekst uit een JPEG en het extraheren
  van Cyrillische tekst in een paar eenvoudige stappen.
og_title: c# OCR‑tutorial – Tekst extraheren uit afbeelding met Aspose OCR
tags:
- OCR
- C#
- Aspose
- ImageProcessing
title: c# OCR-tutorial – Tekst extraheren uit afbeelding met Aspose OCR
url: /nl/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Tekst extraheren uit afbeelding met Aspose OCR

Heb je ooit een **c# ocr tutorial** nodig gehad die je echt van een lege JPEG naar leesbare Unicode‑tekst brengt? Misschien bouw je een document‑archiverings‑tool, een kassabon‑scanner, of ben je gewoon nieuwsgierig naar het halen van tekst uit afbeeldingen. Hoe dan ook, je bent op de juiste plek. In deze gids laten we je zien hoe je **extract text from image** bestanden, **recognize text from jpeg** assets, en zelfs het lastige **recognize cyrillic text** scenario kunt behandelen—zonder cloud‑aanroepen.

We zullen Aspose.OCR gebruiken, een volledig offline bibliotheek die taalmodules levert die je op schijf kunt aanwijzen. Aan het einde van deze tutorial heb je een zelfstandige console‑app die een afbeelding laadt voor OCR, de engine uitvoert en het resultaat naar de console print. Geen externe services, geen API‑sleutels—gewoon pure C#.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)
- Visual Studio 2022 of een IDE naar keuze
- Aspose.OCR NuGet‑pakket (`Aspose.OCR`) en de bijbehorende `Aspose.OCR.Resources`‑map
- Een JPEG‑afbeelding die Cyrillische tekens bevat (of een andere taal die je wilt testen)

Als je een van deze mist, haal dan het NuGet‑pakket via de Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

en download de taalresources van de Aspose‑website, pak ze uit in een map zoals `C:\OCR\Aspose.OCR.Resources`.

Laten we beginnen.

## Stap 1: Laad de OCR‑resources – load image for ocr

Het eerste wat de engine nodig heeft is een pad naar de taalmodules. Beschouw het als het vertellen aan de OCR waar zijn woordenboek zich bevindt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Point to the folder that contains the language modules
ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");
```

> **Pro tip:** Gebruik een absoluut pad tijdens ontwikkeling. Wanneer je de app distribueert, overweeg dan om de resources in te sluiten of ze naast het uitvoerbare bestand te kopiëren.

## Stap 2: Kies de taal – recognize cyrillic text

Aspose ondersteunt tientallen talen, maar je moet de gewenste taal kiezen. Voor Cyrillische tekst gebruiken we `OcrLanguage.CyrillicExtended`. Als je alleen Latijnse tekens nodig hebt, vervang je dit door `OcrLanguage.English`.

```csharp
// Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.CyrillicExtended   // This enables Cyrillic recognition
};
```

Waarom is dit belangrijk? De engine laadt taalspecifieke classifiers; het kiezen van de verkeerde kan de nauwkeurigheid drastisch verlagen.

## Stap 3: Laad de JPEG – recognize text from jpeg

Nu laden we daadwerkelijk de afbeelding die we willen scannen. Aspose kan gangbare formaten lezen zoals JPEG, PNG, BMP en TIFF.

```csharp
// Load the image file (replace with your own path)
var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");
```

Als de afbeelding groot is, wil je deze mogelijk verkleinen voordat je hem aan de engine geeft—dit versnelt de verwerking en vermindert het geheugenverbruik.

## Stap 4: Voer de herkenning uit – extract text from image

Met de engine geconfigureerd en de afbeelding in het geheugen, is de herkenningsstap één enkele regel.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Achter de schermen voert de engine een cascade van voorverwerking (ruisverwijdering, binarisatie) uit en vergelijkt vervolgens de visuele patronen met het geselecteerde taamodel.

## Stap 5: Toon het resultaat – extract text from image

Tot slot geven we de herkende tekenreeks weer. In een echte applicatie zou je dit naar een bestand, een database of een zoekindex kunnen schrijven.

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Verwacht resultaat** (ervan uitgaande dat de voorbeeldafbeelding “Привет мир!” bevat):

```
=== OCR Output ===
Привет мир!
```

Als je onleesbare tekens ziet, controleer dan of je de juiste taal hebt geselecteerd en of de afbeelding niet te veel ruis bevat.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar‑te‑kopiëren programma. Sla het op als `Program.cs` in een nieuw console‑project en voer het uit.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class OfflineOcrDemo
{
    static void Main()
    {
        // Step 1: Point the OCR engine to the folder that contains the language modules
        ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");

        // Step 2: Create the OCR engine and select the required language (Cyrillic Extended)
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.CyrillicExtended
        };

        // Step 3: Load the image that contains the text to be recognized
        var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");

        // Step 4: Perform the recognition operation
        OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 5: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Opmerking:** Vervang de paden door de daadwerkelijke locaties op jouw machine. Het programma werkt offline; er is geen internetverbinding nodig zodra de resources aanwezig zijn.

## Veelgestelde vragen & randgevallen

### Wat als mijn afbeelding een PNG is in plaats van een JPEG?

Aspose.OCR behandelt PNG op dezelfde manier als JPEG. Verander gewoon de bestandsextensie in `FromFile`. De **recognize text from jpeg** stap werkt voor elk ondersteund formaat.

### Hoe verbeter ik de nauwkeurigheid bij scans van lage kwaliteit?

- Pre‑process de afbeelding (verhoog contrast, corrigeer scheefstand) met `ocrImage.AdjustContrast(1.2)` of soortgelijke methoden.
- Gebruik `OcrEngine.PreprocessImage` vóór het aanroepen van `Recognize`.
- Kies een taal die bij het schrift past; voor gemengde Latijnse/Cyrillische tekst kun je `Language = OcrLanguage.Multilingual` instellen.

### Kan ik alleen nummers of datums extraheren?

Ja. Nadat je `ocrResult.Text` hebt, kun je reguliere expressies toepassen om de benodigde delen te filteren. De OCR zelf retourneert de ruwe tekenreeks; verdere parsing is aan jou.

### Is het mogelijk om dit op Linux uit te voeren?

Absoluut. Aspose.OCR is cross‑platform. Installeer gewoon de .NET‑runtime op je Linux‑machine en wijs `SetLocalResourcesPath` naar de juiste map.

## Pro‑tips voor productie

- **Cache de OcrEngine**: Een nieuwe engine voor elk verzoek maken voegt overhead toe. Houd een singleton aan als je veel afbeeldingen verwerkt.
- **Thread‑veiligheid**: De engine is standaard niet thread‑veilig. Vergrendel rond `Recognize` of instantieer aparte engines per thread.
- **Geheugenbeheer**: Maak `OcrImage`‑objecten na gebruik vrij (`ocrImage.Dispose()`) om native buffers vrij te geven.
- **Logging**: Leg `ocrResult.Confidence` vast (indien beschikbaar) om scans met lage zekerheid te detecteren en een fallback te activeren.

## Conclusie

Je hebt nu een **c# ocr tutorial** die je door elke stap leidt om **load image for ocr**, **recognize text from jpeg**, **extract text from image**, en **recognize cyrillic text** te gebruiken met Aspose.OCR. De voorbeeldcode is klaar om te draaien, en de uitleg laat zien waarom elke regel belangrijk is—niet alleen hoe.

Vanaf hier kun je experimenteren met andere talen, de OCR integreren in een web‑API, of de geëxtraheerde strings in een zoekmachine voeren. De mogelijkheden zijn net zo breed als de afbeeldingen die je erin stopt.

Als je tegen problemen aanloopt, laat dan een reactie achter of raadpleeg de Aspose‑documentatie voor diepere configuratie‑opties. Veel plezier met coderen, en moge je afbeeldingen altijd kristalhelder zijn!

![c# ocr tutorial screenshot showing console output of extracted text](/images/ocr-demo.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}