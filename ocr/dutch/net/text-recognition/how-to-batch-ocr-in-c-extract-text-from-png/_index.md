---
category: general
date: 2026-03-26
description: Hoe batch‑OCR in C# het extraheren van tekst uit PNG‑bestanden eenvoudig
  maakt. Volg deze stap‑voor‑stap C# OCR‑tutorial voor batch‑tekstekstractie met Aspose
  OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: nl
og_description: Hoe batch-OCR in C# je in staat stelt snel tekst uit PNG‑bestanden
  te extraheren. Deze gids leidt je door een volledige C# OCR‑tutorial met batch‑tekstextractie.
og_title: Hoe batch-OCR in C# uit te voeren – Tekst uit PNG extraheren
tags:
- OCR
- C#
- Aspose
title: Hoe batch-OCR in C# uitvoeren – Tekst uit PNG extraheren
url: /nl/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch-OCR uit te voeren in C# – Tekst extraheren uit PNG

Heb je je ooit afgevraagd **hoe je batch-OCR** kunt uitvoeren op een stapel screenshots zonder voor elk bestand een apart programma te schrijven? Je bent niet de enige. In veel projecten eindigen we met tientallen PNG's waarvan de tekst moet worden gehaald, en het één‑voor‑één doen is een gedoe.  

Het goede nieuws? Met Aspose OCR kun je een klein C# console‑appje opzetten dat al die afbeeldingen parallel verwerkt, waardoor je snelle **batch‑tekstextractie** krijgt en een nette resultaatsset. In deze gids lopen we een volledige **c# ocr tutorial** door, leggen we uit waarom elk onderdeel belangrijk is, en laten we je precies zien hoe de output eruitziet.

Aan het einde van dit artikel kun je:

* Een lijst met PNG‑bestanden (of elke ondersteunde afbeelding) in één keer laden.  
* Een gedeelde `OcrEngine` configureren zodat de instellingen consistent blijven gedurende de batch.  
* De herkenningswachtrij uitvoeren met maximaal vier parallelle workers.  
* De herkende tekst voor elke pagina ophalen en naar de console afdrukken.

Geen magie, gewoon degelijke code die je vandaag nog in je oplossing kunt opnemen.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

* .NET 6 SDK (of een recente .NET‑versie).  
* Een geldige Aspose OCR‑licentie of een tijdelijke evaluatiesleutel.  
* Een map die de PNG‑bestanden bevat die je wilt verwerken.  
* Visual Studio 2022 of je favoriete editor.

Dat is alles—geen extra NuGet‑pakketten behalve `Aspose.OCR` en de standaard `System.Collections.Generic`.

## Hoe batch-OCR uit te voeren – Het project opzetten

Allereerst, maak een nieuw console‑project aan en haal de Aspose OCR‑bibliotheek binnen.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Nadat het herstel is voltooid, open **Program.cs** (of maak een nieuw bestand) en voeg de gebruikelijke `using`‑directieven toe:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Die eenvoudige scaffolding geeft ons toegang tot de `OcrEngine`, `RecognitionQueue` en hulpprogrammaklassen die we later nodig hebben.

## Tekst extraheren uit PNG – Lijst met afbeeldingen voorbereiden

Nu moeten we het programma vertellen **welke PNG's** door OCR te laten gaan. De meest eenvoudige manier is een `List<string>` te bouwen die absolute of relatieve paden bevat.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Vervang `YOUR_DIRECTORY` door het daadwerkelijke mappad. Als je een dynamische set hebt, kun je ook `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` gebruiken en het resultaat in de lijst stoppen. Het belangrijkste is dat **tekst extraheren uit PNG** gewoon neerkomt op het aanleveren van de juiste bestandsnamen aan de wachtrij.

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")

*Afbeeldingsalt‑tekst: diagram van batch‑OCR‑workflow*

## C# OCR tutorial – De herkenningswachtrij configureren

Het hart van de batch‑operatie is de `RecognitionQueue`. Zie het als een lopende band die elke afbeelding aan een gedeelde `OcrEngine` doorgeeft. Door de engine te delen houden we het geheugenverbruik laag en garanderen we identieke instellingen voor elke pagina.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Waarom `MaxDegreeOfParallelism` op 4 zetten? Op een typische quad‑core laptop levert dat de beste doorvoer zonder het besturingssysteem te benadelen. Als je op een server met meer cores draait, verhoog dan het aantal dienovereenkomstig.

### Pro‑tip

Als je aangepaste taalpakketten, DPI‑instellingen of bijsnijden van een regio‑van‑interesse nodig hebt, doe dat **eenmalig** op de gedeelde `Engine` voordat je afbeeldingen in de wachtrij plaatst. Bijvoorbeeld:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Alle daaropvolgende herkenningen erven deze opties automatisch—dit is de essentie van **hoe je OCR**‑pijplijnen maakt die consistent blijven.

## Batch‑tekstextractie – Afbeeldingen in de wachtrij plaatsen en de wachtrij uitvoeren

Met de wachtrij klaar, is de volgende stap elke afbeelding erop te plaatsen. De `Enqueue`‑methode accepteert een `OcrImage`‑instantie, die we van een bestandspad maken.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Zodra elk bestand in de wachtrij staat, starten we de verwerking:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blokkeert tot elke afbeelding is voltooid, en retourneert vervolgens een lijst waarbij elk element overeenkomt met de invoervolgorde. Dit garandeert dat het resultaat van pagina 1 op index 0 staat, pagina 2 op index 1, enzovoort—handig wanneer je resultaten terug moet koppelen aan de bronbestanden.

## Hoe OCR te maken – Resultaten weergeven

Ten slotte, laten we de herkende tekst naar de console afdrukken. Hier zie je echt de **batch‑tekstextractie** in actie.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Wanneer je het programma uitvoert (`dotnet run`), zie je iets als:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Als een afbeelding faalt (bijv. beschadigd bestand), zal het bijbehorende `OcrResult` een lege `Text`‑eigenschap hebben en kun je `ocrResults[i].Exception` inspecteren voor diagnostiek.

## Hoe OCR te maken – Tips, randgevallen en best practices

### Grote batches verwerken

Het verwerken van honderden PNG's kan nog steeds veel geheugen verbruiken als je alle `OcrResult`‑objecten in leven houdt. In dat geval kun je de output naar een bestand of database streamen zodra elk resultaat binnenkomt:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Omgaan met niet‑PNG‑formaten

Aspose OCR ondersteunt ook JPEG, BMP en TIFF direct. Verander gewoon de bestandsextensie in je lijst of gebruik een wildcard‑zoekopdracht. Dezelfde **c# ocr tutorial**‑stappen gelden—geen code‑wijzigingen nodig.

### Lege pagina's overslaan

Als je gescande PDF's hebt die soms lege pagina's bevatten, kun je resultaten filteren:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Licentie‑overwegingen

De evaluatieversie plaatst op elke pagina een watermerk. Voor productie, zorg ervoor dat je je licentiebestand embedt aan het begin van `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Parallelisme afstemmen

`MaxDegreeOfParallelism` heeft standaard `Environment.ProcessorCount`. Als je hoge CPU‑belasting of geheugen‑druk merkt, verlaag dan de waarde. Omgekeerd, op een cloud‑VM met veel cores, verhoog het om de hardware volledig te benutten.

## Samenvatting

Je hebt nu een volledige **hoe batch-OCR**‑oplossing in C# die **tekst uit PNG**‑bestanden kan **extraheren**, ze parallel kan uitvoeren en je schone, geordende resultaten geeft. Door één enkele `OcrEngine` te delen, heb je geleerd **hoe je OCR**‑pijplijnen maakt die zowel geheugen‑efficiënt als gemakkelijk te onderhouden zijn. Deze **c# ocr tutorial** laat ook zien hoe je kunt opschalen naar **batch‑tekstextractie** voor honderden afbeeldingen met slechts een paar extra regels.

---

### Wat is het vervolg?

* Probeer taaldetectie toe te voegen (`Engine.Language = Language.AutoDetect`).  
* Experimenteer met uitvoerformaten—schrijf resultaten naar JSON of CSV voor downstream‑analyse.  
* Combineer deze batch‑OCR met een PDF‑naar‑afbeelding conversiestap om volledige gescande documenten te verwerken.

Voel je vrij om het parallelisme aan te passen, je eigen afbeeldingsbronnen te gebruiken, of de resultaten in een zoekindex te pluggen. De mogelijkheden zijn eindeloos als je **hoe batch-OCR** in C# onder de knie hebt.

Veel programmeerplezier, en moge je OCR‑runs snel en foutloos zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}