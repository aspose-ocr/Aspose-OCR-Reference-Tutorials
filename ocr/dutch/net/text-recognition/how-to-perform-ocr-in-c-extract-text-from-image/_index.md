---
category: general
date: 2026-04-03
description: Leer hoe je OCR in C# uitvoert en tekst uit een afbeelding haalt met
  Aspose OCR, met spellingscontrole voor de Russische taal.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: nl
og_description: Leer hoe je OCR in C# uitvoert en tekst uit een afbeelding haalt met
  Aspose OCR, met spellingscontrole voor de Russische taal.
og_title: Hoe OCR uit te voeren in C# – Tekst uit afbeelding extraheren
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Hoe OCR in C# uit te voeren – Tekst uit afbeelding extraheren
url: /nl/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in C# – Tekst extraheren uit een afbeelding

Heb je je ooit afgevraagd **hoe OCR uit te voeren** op een foto van een handgeschreven notitie? Misschien heb je een gescande bon, een bord in een vreemde taal, of een PDF‑pagina die niet wil kopiëren‑plakken. Het goede nieuws? Met een paar regels C# en de Aspose OCR‑bibliotheek kun je die foto in een handomdraai omzetten naar bewerkbare tekst.  

In deze gids laten we niet alleen zien **hoe OCR uit te voeren**, we lopen ook door **tekst extraheren uit afbeelding**, **afbeelding omzetten naar tekst**, en zelfs **hoe spelling te controleren** wanneer je met documenten in het Russisch werkt. Klinkt als veel? Blijf hangen – we splitsen alles stap voor stap op.

## Wat je zult leren

Aan het einde van deze tutorial kun je:

* Aspose OCR configureren voor ondersteuning van de Russische taal.  
* Een afbeeldingsbestand laden en optische tekenherkenning uitvoeren om **tekst uit afbeelding te extraheren**.  
* De ingebouwde spellingscontrole gebruiken om automatisch verkeerd gespelde woorden te corrigeren – het perfecte antwoord op “**hoe spelling te controleren**” van OCR‑output.  
* De opgeschoonde string naar de console printen, klaar voor verdere verwerking of opslag.

**Prerequisites** – je hebt nodig:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.8).  
* Een geldige Aspose OCR‑licentie of een tijdelijke evaluatiesleutel.  
* Een afbeeldingsbestand dat Russische tekst bevat (voor de demo noemen we het `russian_note.jpg`).  

Als een van deze onbekend klinkt, geen zorgen. De stappen hieronder bevatten het exacte NuGet‑commando om Aspose OCR binnen te halen, en de code is volledig zelfstandig.

![voorbeeld van OCR uitvoeren](/images/ocr-demo.png "voorbeeld van OCR uitvoeren in C# voorbeeld")

## Stap 1 – Installeer Aspose OCR en voeg namespaces toe

Allereerst heb je de bibliotheek nodig. Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Dat commando haalt de nieuwste stabiele versie op (vanaf april 2026 is dat 22.9). Nadat het pakket is hersteld, voeg je de benodigde `using`‑directieven toe aan de bovenkant van je C#‑bestand:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Pro tip:* Als je Visual Studio gebruikt, zal de IDE deze automatisch voorstellen zodra je de eerste klassenaam intypt.

## Stap 2 – Initialiseert de OCR‑engine voor de Russische taal

Het **hoe OCR uit te voeren**‑deel begint met het aanmaken van een `OcrEngine`‑instantie. Door `OcrLanguage.Russian` op te geven, vertellen we de engine het Cyrillische teken­set en taalspecifieke heuristieken te laden.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Waarom is dit belangrijk? Zonder de taal in te stellen, valt de engine terug op Engels en zal veel Cyrillische tekens verkeerd interpreteren, wat leidt tot onleesbare output. Het expliciet configureren van de taal verbetert de nauwkeurigheid drastisch.

## Stap 3 – Laad de afbeelding en **afbeelding omzetten naar tekst**

Nu brengen we de foto in het geheugen. De methode `Image.FromFile` werkt met de meeste gangbare formaten (JPG, PNG, BMP). Na het laden roepen we `Recognize` aan om **afbeelding omzetten naar tekst**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

De variabele `rawText` bevat nu de ruwe OCR‑output, die nog typfouten of verkeerd herkende tekens kan bevatten. Je kunt deze afdrukken om te zien wat de engine heeft vastgelegd:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Stap 4 – **Hoe spelling te controleren** van het OCR‑resultaat

Russische OCR kan rommelig zijn, vooral bij scans met lage resolutie. Aspose biedt een `SpellChecker`‑klasse die Russische woordenboeken direct ondersteunt. Zo roep je het aan:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

De methode `CheckAndCorrect` retourneert een nieuwe string waarin verkeerd gespelde woorden zijn vervangen door de meest waarschijnlijke correcte alternatieven. Hij houdt ook rekening met interpunctie, zodat je niet eindigt met een muur van tekst.

*Edge case:* Als de OCR‑output leeg is (bijvoorbeeld wanneer de afbeelding volledig wit is), zal `CheckAndCorrect` simpelweg een lege string teruggeven. Het is verstandig hierop te controleren als je van plan bent het resultaat naar een bestand te schrijven.

## Stap 5 – Toon het opgeschoonde resultaat

Tot slot geven we de gecorrigeerde string weer. In een echte applicatie schrijf je deze misschien naar een database, een JSON‑API, of een Word‑document. Voor deze demo volstaat een console‑dump:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Wanneer je het programma uitvoert, zou je iets moeten zien als:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Let op hoe de spellingscontrole “Привeт” (gemengde Latijnse ‘e’) omzet naar het juiste Cyrillische “Привет”. Dat is de magie van **hoe spelling te controleren** van OCR‑output.

## Volledig werkend voorbeeld

Hieronder staat het complete, uitvoerbare programma dat alle stappen samenbrengt. Kopieer‑plak het in een nieuw console‑project en druk op **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Verwachte output

Het uitvoeren van het programma met een duidelijke, hoge‑resolutie foto van Russisch handschrift levert doorgaans een schone, menselijk leesbare zin op. Als de afbeelding onscherp is, kun je nog steeds gedeeltelijk correcte woorden krijgen, maar de spellingscontrole zal de meeste duidelijke fouten gladstrijken.

## Veelvoorkomende valkuilen & tips

| Issue | Why it Happens | How to Fix / Avoid |
|-------|----------------|--------------------|
| **Garbage characters** | Low DPI or noisy background | Pre‑process the image (increase contrast, resize to ≥300 dpi) before feeding it to `Recognize`. |
| **Empty output** | Wrong file path or unsupported format | Verify the path, and use `Image.FromFile` inside a `try/catch` block to surface errors. |
| **Spell checker misses errors** | Rare words not in dictionary | Extend the dictionary by loading a custom word list via `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Performance lag on large batches** | OCR is CPU‑intensive | Run OCR on a background thread or use `Parallel.ForEach` for multiple images. |
| **License exception** | Using evaluation version beyond trial period | Purchase a license and call `License license = new License(); license.SetLicense("Aspose.Total.lic");` before creating `OcrEngine`. |

## Volgende stappen – Verder gaan dan eenvoudige OCR

Nu je **hoe OCR uit te voeren** onder de knie hebt, overweeg je de volgende uitbreidingen:

* **Batchverwerking** – Loop door een map met afbeeldingen en schrijf elke gecorrigeerde tekst naar een `.txt`‑bestand.  
* **PDF‑conversie** – Gebruik Aspose PDF om de geëxtraheerde tekst terug te embedden in een doorzoekbare PDF.  
* **Taaldetectie** – Als je meerdere talen moet verwerken, inspecteer dan eerst de OCR‑resultaten en schakel `OcrLanguage` dienovereenkomstig.  
* **Integratie met Azure Cognitive Services** – Vergelijk de resultaten van Aspose met de OCR‑API van Microsoft voor een hybride aanpak.

Al deze onderwerpen bevatten natuurlijk de secundaire zoekwoorden **extract text from image**, **convert image to text**, en **how to spell check**, dus

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}