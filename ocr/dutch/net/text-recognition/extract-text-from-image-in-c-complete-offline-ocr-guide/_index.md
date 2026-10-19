---
category: general
date: 2026-03-18
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je tekst
  kunt extraheren, OCR-herkenning kunt uitvoeren en Cyrillische tekst kunt herkennen
  zonder internet.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: nl
og_description: Haal tekst uit een afbeelding met Aspose OCR. Stapsgewijze handleiding
  om OCR-herkenning uit te voeren, hoe je tekst kunt extraheren en Cyrillische tekst
  offline kunt herkennen.
og_title: Tekst uit afbeelding extraheren in C# – Offline OCR‑tutorial
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Tekst extraheren uit afbeelding in C# – Complete offline OCR-gids
url: /nl/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding – Complete Offline OCR-gids

Heb je ooit **tekst uit een afbeelding moeten extraheren** en was je bang voor netwerk‑latentie of licentiebeperkingen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur wanneer hun app in een sandbox‑omgeving moet werken, maar toch betrouwbare OCR nodig heeft. Het goede nieuws? Met Aspose OCR kun je de volledige pipeline lokaal uitvoeren, **tekst uit een afbeelding extraheren** zonder ooit het internet aan te raken.

In deze tutorial lopen we een praktisch voorbeeld door dat laat zien **hoe je tekst kunt extraheren**, een offline engine opzet, **OCR‑herkenning uitvoert**, en zelfs **Cyrillische tekst herkent**. Aan het einde heb je een kant‑klaar C# console‑applicatie die de gedetecteerde string rechtstreeks naar de console print.

## Wat je nodig hebt

- .NET 6.0 SDK (of een recente .NET‑versie)  
- Visual Studio 2022 of VS Code – wat je maar prefereert  
- Aspose.OCR for .NET NuGet‑pakket  
- Een map met de Aspose OCR‑modelbestanden (eenmalig downloaden van het Aspose‑portaal)  
- Een afbeeldingsbestand dat zowel Engelse als Cyrillische tekens bevat (bijv. `cyrillic_doc.jpg`)

Geen externe services, geen verborgen downloads tijdens runtime – alles staat op je schijf.

## Stap 1: Installeer Aspose.OCR en bereid bronnen voor

Voeg eerst het Aspose.OCR NuGet‑pakket toe aan je project:

```bash
dotnet add package Aspose.OCR
```

Maak vervolgens een map genaamd `AsposeOCRResources` ergens op je machine en kopieer de modelbestanden die je van Aspose hebt gedownload naar die map. De OCR‑engine zoekt naar taalpakketten in deze directory, dus zorg dat het pad klopt.

> **Pro tip:** Houd de resources‑map naast je `.csproj`‑bestand; dit vereenvoudigt pad‑beheer tijdens de ontwikkeling.

## Stap 2: Bouw de offline OCR‑engine

Nu gaan we de engine instantieren en wijzen we hem naar de resources‑map. Dit is de cruciale stap die ons in staat stelt **OCR‑herkenning volledig offline** uit te voeren.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

Waarom talen expliciet laden? Omdat we de engine hebben verteld offline te blijven; hij zal geen verbinding maken met Aspose‑servers om ontbrekende pakketten op te halen. Als je een taal vergeet te laden, worden alle tekens uit dat script genegeerd.

## Stap 3: Geef de afbeelding aan de engine

Met de engine klaar, leveren we nu de afbeelding die we willen verwerken. De helper `ImageStream.FromFile` leest het bestand in een formaat dat de OCR‑engine begrijpt.

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

Als je afbeelding groot is, overweeg dan om deze van tevoren te verkleinen om snelheid en nauwkeurigheid te verbeteren. De OCR‑engine werkt het beste met een DPI van ongeveer 300.

## Stap 4: Voer het herkenningsproces uit

Het aanroepen van `Recognize` doet het zware werk. De methode retourneert een `OcrResult`‑object dat de geëxtraheerde string, confidence‑scores en meer bevat.

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Achter de schermen parseert Aspose de bitmap, draait taal‑specifieke neurale netwerken en zet de tekens aan elkaar. Omdat we zowel Engels als Cyrillisch hebben geladen, worden documenten met gemengde scripts naadloos afgehandeld.

## Stap 5: Toon de geëxtraheerde tekst

Tot slot geven we het resultaat weer. In een echte app sla je het misschien op in een database of geef je het door aan een andere service, maar voor deze demo printen we het gewoon.

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Het uitvoeren van het programma zou iets moeten opleveren als:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

Zie je onleesbare tekens, controleer dan of het Cyrillische taalpakket correct in de resources‑map staat en of de afbeelding niet te onscherp is.

![voorbeeld van tekst extraheren uit afbeelding](extract_text_image.png "tekst extraheren uit afbeelding")

*Afbeeldings‑alt‑tekst: tekst extraheren uit afbeelding – OCR‑resultaat met Engelse en Cyrillische regels.*

## Veelvoorkomende valkuilen behandelen

### Ontbrekende taalpakketten

Als je een uitzondering krijgt met de melding “Language data not found”, kon de engine de modelbestanden niet vinden. Controleer `ResourcesPath` en zorg dat de map `english.dat` en `cyrillic.dat` (of gelijknamige bestanden) bevat.

### Lage confidence‑scores

Soms geeft de OCR‑engine een lage confidence voor bepaalde tekens, vooral als de afbeelding ruis bevat. Je kunt de nauwkeurigheid verbeteren door:

- De afbeelding naar grijstinten om te zetten voordat je deze aan de engine geeft  
- Een mediane filter toe te passen om vlekjes te verminderen  
- Zeker te stellen dat de tekst horizontaal uitgelijnd is (indien nodig roteren)

### Grote afbeeldingen

Het verwerken van een foto van 10 MP kan traag zijn. Schaal af tot een maximale breedte van 2000 px terwijl je de beeldverhouding behoudt; de engine zal nog steeds de meeste tekens nauwkeurig vastleggen.

## Het voorbeeld uitbreiden

- **Batchverwerking:** Plaats de herkenningslogica in een lus die over alle bestanden in een map iterereert.  
- **Uitvoerformaten:** `OcrResult` biedt ook een `TextLines`‑collectie met begrenzings‑boxen – handig voor het markeren van tekst in UI‑applicaties.  
- **Extra talen:** Roep simpelweg `LoadLanguage` aan met een andere ondersteunde enum‑waarde (bijv. `Language.French`).  

Al deze uitbreidingen volgen nog steeds het **hoe tekst te extraheren**‑principe — laad gewoon de juiste taalpakketten en laat de engine de rest doen.

## Volledige broncode‑overzicht

Hieronder staat het complete, kant‑klaar programma. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op jouw machine.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Sla dit op als `Program.cs`, voer `dotnet run` uit, en zie hoe de console de tekst print die de engine uit je afbeelding heeft gehaald. Dat is alles — je hebt **tekst uit een afbeelding geëxtraheerd** in een offline scenario.

## Conclusie

We hebben alles behandeld wat je nodig hebt om **tekst uit een afbeelding te extraheren** met Aspose OCR in een volledig offline omgeving. De gids toonde **hoe je tekst kunt extraheren**, demonstreerde **OCR‑herkenning uitvoeren**, en bewees dat je **Cyrillische tekst** naast Engels kunt herkennen zonder netwerk‑calls.  

Van het installeren van het NuGet‑pakket tot het afhandelen van randgevallen zoals ontbrekende taalpakketten, je hebt nu een solide basis om OCR‑gedreven functionaliteit in elke .NET‑applicatie te bouwen.  

Wat nu? Probeer PDF’s te verwerken, meerdere pagina’s te scannen, of de output te integreren met een zoekindex. De mogelijkheden zijn eindeloos zodra je offline OCR onder de knie hebt.

Happy coding, en moge je afbeeldingen altijd kristalhelder zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}