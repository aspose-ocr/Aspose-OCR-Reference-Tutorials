---
category: general
date: 2026-01-01
description: Herken Russische tekst direct met Aspose OCR C#. Leer hoe je Chinese
  tekst herkent, het aantal PDF‑pagina’s leest en PDF‑paginatekst converteert in één
  tutorial.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: nl
og_description: herken Russische tekst snel met Aspose OCR C#. Deze tutorial behandelt
  ook hoe je Chinese tekst herkent, het aantal PDF-pagina's leest en PDF-pagina-tekst
  converteert.
og_title: Herken Russische tekst met Aspose OCR C# – Volledige gids
tags:
- Aspose OCR
- C#
- PDF processing
title: herken Russische tekst met Aspose OCR C# – Volledige meerpagina‑PDF‑gids
url: /nl/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# herken Russische tekst met Aspose OCR C# – Volledige Multi‑Page PDF Tutorial

Heb je ooit **Russische tekst moeten herkennen** in een PDF die meerdere talen bevat, en je afgevraagd hoe je dat kunt doen zonder voor elke pagina een apart hulpmiddel te gebruiken? Je bent niet de enige. In veel real‑world projecten krijg je één PDF die Engels, Russisch en zelfs Chinees op verschillende pagina's bevat, en wil je toch één enkele, schone tekstoutput.

In deze gids laten we je precies zien hoe je **Russische tekst kunt herkennen** (en andere talen) met behulp van **Aspose OCR C#**, terwijl we ook laten zien hoe je **pdf-pagina‑aantal kunt lezen**, **Chinese tekst kunt herkennen**, en **pdf-pagina‑tekst kunt converteren** naar een handige console‑dump. Geen externe services, geen verborgen stappen—alleen pure C#‑code die je kunt kopiëren‑plakken en uitvoeren.

> **Wat je zult meenemen**  
> * Een uitvoerbare C# console‑applicatie die een multi‑page PDF verwerkt.  
> * Per‑pagina taalselectie (Russisch, Chinees, Engels).  
> * Technieken om het paginacount van de PDF op te vragen en de tekst van elke pagina te extraheren.  
> * Tips, valkuilen en uitbreidingen die je op je eigen projecten kunt toepassen.  

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
- **Aspose.OCR for .NET** NuGet‑pakket geïnstalleerd (`dotnet add package Aspose.OCR`).  
- Een PDF‑bestand dat gemengde talen bevat; voor de demo verwijzen we naar `mixed_lang.pdf`.  
- Basiskennis van C# console‑applicaties.

Als je een van deze mist, haal dan de nieuwste Aspose OCR van NuGet en plaats je PDF ergens bereikbaar vanuit de projectmap.

## Stap 1 – Initialiseer de Aspose OCR Engine

Het allereerste wat je nodig hebt is een instantie van `OcrEngine`. Dit object bevat alle instellingen (zoals taal) en voert het zware werk uit.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Waarom dit belangrijk is:**  
> De engine is herbruikbaar, zodat we geen geheugen verspillen door voor elke pagina een nieuwe instantie te maken. Het hergebruiken stelt ons ook in staat de taal dynamisch te wijzigen, wat essentieel is voor **Russische tekst herkennen** op één pagina en **Chinese tekst herkennen** op een andere.

## Stap 2 – Laad de PDF en ontdek hoeveel pagina's het heeft

Voordat we beginnen met herkennen, hebben we het PDF‑object en het paginacount nodig. Aspose OCR behandelt elke pagina als een `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Tip:** Als de PDF enorm is, wil je misschien eerst het aantal lezen en beslissen of je alle pagina's of slechts een deel wilt verwerken.

## Stap 3 – Koppel elke pagina aan de gewenste taal

Aspose OCR ondersteunt veel talen, maar je moet aangeven welke je voor elke pagina wilt gebruiken. Hieronder maken we een `Dictionary<int, OcrLanguage>` waarbij de sleutel de nul‑gebaseerde paginanaam is.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Waarom dit cruciaal is:**  
> Zonder deze map zou de OCR‑engine één standaardtaal voor elke pagina proberen, wat leidt tot onleesbare output voor Russische of Chinese tekst. Deze stap maakt **Russische tekst herkennen** en **Chinese tekst herkennen** correct mogelijk.

## Stap 4 – Loop door alle pagina's, stel de taal in en herken de tekst

Nu itereren we over elke pagina, wisselen we de taal op basis van onze map, en roepen we `Recognize` aan. Het resultaat wordt opgeslagen in `OcrResult`, waaruit we de platte tekst extraheren.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Verwachte console‑output

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **Uitleg van de flow:**  
> * De loop respecteert het **pdf-pagina‑aantal lezen** dat we eerder hebben afgedrukt.  
> * Door `ocrEngine.Settings.Language` elke iteratie te wisselen, garanderen we nauwkeurige **Russische tekst herkennen** op pagina 2 en **Chinese tekst herkennen** op pagina 3.  
> * De `Console.WriteLine`‑statements converteren effectief **pdf-pagina‑tekst** naar een mens‑leesbare string.

## Stap 5 – Uitvoeren, verifiëren en aanpassen

1. Bouw het project (`dotnet build`).  
2. Voer het uit (`dotnet run`).  
3. Vergelijk de console‑output met de originele PDF.

Als je ontbrekende tekens opmerkt, overweeg dan:

- **De OCR‑nauwkeurigheid verhogen** door `ocrEngine.Settings.DetectTextOrientation = true;` in te stellen.  
- **Een aangepast taalpakket leveren** als de ingebouwde Russische of Chinese woordenboeken verouderd zijn.  
- **DPI aanpassen** bij het laden van de PDF (`OcrImage.FromFile(path, 300)`), wat de herkenning bij scans met lage resolutie kan verbeteren.

## Bonus: Randgevallen afhandelen

### Wat als de taal van een pagina niet in de map staat?

De code valt al terug op Engels, maar je kunt ook een fallback toevoegen die een waarschuwing logt:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Kunnen we PDF's verwerken met meer dan drie talen?

Zeker. Breid `languageMap` uit met extra indexen en ondersteunde `OcrLanguage`‑waarden (bijv. `OcrLanguage.French`). De loop zal elk aantal pagina's aan kunnen.

### Hoe exporteer je de resultaten naar een bestand in plaats van de console?

Vervang de `Console.WriteLine`‑aanroepen door `File.AppendAllText("output.txt", …)` of gebruik een `StringBuilder` die je eenmaal na de loop wegschrijft.

## Afbeeldingsillustratie

![voorbeeld van Russische tekst herkennen](/images/recognize-russian-text.png "Screenshot die OCR-output voor Russische tekst toont")

*De bovenstaande afbeelding toont de console‑output wanneer **Russische tekst herkennen** wordt uitgevoerd op een PDF met gemengde talen.*

## Conclusie

We hebben een compleet, end‑to‑end voorbeeld doorlopen dat laat zien hoe je **Russische tekst kunt herkennen** (en ook **Chinese tekst kunt herkennen**) uit een multi‑page PDF met behulp van **Aspose OCR C#**. Door hetinacount van de PDF te lezen, elke pagina aan de juiste taal te koppelen en door het document te loopen, kun je **pdf-pagina‑tekst** omzetten naar platte strings die klaar zijn voor opslag, indexering of verdere analyse.

In het kort:

- **Initialiseer** een enkele `OcrEngine`.  
- **Laad** de PDF en **pdf-pagina‑aantal lezen**.  
- **Koppel** pagina's aan talen (Russisch, Chinees, enz.).  
- **Itereer**, stel `ocrEngine.Settings.Language` in, en **herken** elke pagina.  
- **Output** of sla de geëxtraheerde tekst op.

Voel je vrij dit patroon aan te passen voor grotere documenten, foutafhandeling toe te voegen, of de resultaten in een zoekindex te integreren. Het kernidee—per‑pagina taalselectie—blijft hetzelfde, en het is wat betrouwbare **Russische tekst herkennen** mogelijk maakt in PDF's met gemengde talen.

Heb je een ander scenario, zoals het scannen van afbeeldingen in plaats van PDF's? Dezelfde engine werkt; vervang gewoon `OcrImage.FromFile` door `OcrImage.FromStream` of `FromBitmap`. Veel plezier met coderen, en moge je OCR altijd nauwkeurig zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}