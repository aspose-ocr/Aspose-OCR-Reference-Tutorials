---
category: general
date: 2026-06-03
description: Voer OCR uit op een afbeelding en extraheer tekst uit de afbeelding met
  Aspose.OCR. Leer hoe je spelfouten kunt detecteren en spellingsuggesties kunt krijgen
  in één C#‑demo.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: nl
og_description: Voer OCR uit op een afbeelding om tekst uit de afbeelding te extraheren,
  detecteer vervolgens verkeerd gespelde woorden en krijg spellingsuggesties met Aspose.OCR
  in C#.
og_title: Voer OCR uit op afbeelding en detecteer verkeerd gespelde woorden in C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Voer OCR uit op afbeelding en detecteer verkeerd gespelde woorden in C#
url: /nl/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding en spelfouten detecteren in C#

Heb je je ooit afgevraagd hoe je **OCR op afbeelding** kunt uitvoeren zonder je haar uit te trekken? Je bent niet de enige. Of je nu oude brieven digitaliseert, bonnetjes scant of een slimme documentworkflow bouwt, ruwe tekst uit afbeeldingen halen is de eerste horde. Het goede nieuws? Met Aspose.OCR kun je in enkele minuten een oplossing opzetten, en het extra voordeel is dat je ook **spelfouten kunt detecteren** en **spellingsuggesties kunt krijgen** in dezelfde run.

In deze tutorial lopen we stap voor stap door een complete, kant‑klaar C# console‑applicatie die **tekst uit afbeelding** extraheert, een Engelse spellingscontrole uitvoert en elke fout met handige correctie‑ideeën afdrukt. Aan het einde weet je precies **hoe je tekst extraheert**, hoe je de spell‑check‑API aanroept en hoe de verwachte console‑output eruitziet.

## Wat je gaat bouwen

- Een bitmap (of PNG) laden die typografische fouten bevat.  
- Aspose.OCR gebruiken om **OCR op afbeelding** uit te voeren en ruwe string‑data te verkrijgen.  
- De ingebouwde Engelse spell‑checker initialiseren.  
- **Spelfouten detecteren** en **spellingsuggesties krijgen** voor elk woord.  
- Een nette rapportage naar de console afdrukken.

Geen externe services, geen ingewikkelde HTTP‑calls—slechts één NuGet‑pakket en een handvol regels code.

## Vereisten

- .NET 6.0 SDK of later (de code werkt ook op .NET Framework 4.7+).  
- Visual Studio 2022 (of een andere editor naar keuze).  
- Aspose.OCR for .NET NuGet‑pakket (`Aspose.OCR`).  
- Een afbeeldingsbestand (`letter_with_typos.png`) ergens geplaatst zodat je er vanuit het project naar kunt verwijzen.

Als je Aspose nog nooit hebt gebruikt, geen zorgen—het installeren van het pakket is net zo simpel als het uitvoeren van:

```bash
dotnet add package Aspose.OCR
```

Laten we nu de implementatie induiken.

## Stap 1: Het project opzetten en Aspose.OCR installeren

Maak een nieuw console‑project aan en haal de OCR‑bibliotheek binnen:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Nadat het restore‑proces is voltooid, open je `Program.cs`. We zullen later de standaardinhoud vervangen door de volledige demo‑code, maar eerst bespreken we waarom elke namespace belangrijk is.

- `Aspose.OCR` – Kern‑OCR‑engine en afbeeldingsverwerking.  
- `Aspose.OCR.SpellCheck` – Spell‑checking‑hulpmiddelen die bij de bibliotheek worden geleverd.  
- `System` – Standaard .NET‑basisklassen (bijv. `Console`).

## Stap 2: De afbeelding laden en OCR op afbeelding uitvoeren

Het eerste echte werk is de afbeelding aan de OCR‑engine voeren. Aspose.OCR leest vele formaten (PNG, JPEG, TIFF). Hieronder staat het fragment dat het zware werk doet:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Waarom dit belangrijk is:** `OcrImage.FromFile` abstraheert de pixel‑niveau details, terwijl `OcrEngine.Recognize` het getrainde neurale model draait dat visuele glyphs omzet in Unicode‑tekens. De eigenschap `ocrResult.Text` bevat nu de ruwe string—precies wat je nodig hebt om **tekst uit afbeelding** te **extraheren**.
> 
> **Pro tip:** Als je afbeelding meerdere talen bevat, kun je `ocrEngine.Language = OcrLanguage.Multilingual;` instellen vóór het aanroepen van `Recognize`.

## Stap 3: De Engelse spell‑checker initialiseren

Aspose.OCR wordt geleverd met een ingebouwde spell‑checking engine die Engels direct ondersteunt. Initialiseren is één regel:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Waarom deze stap cruciaal is:** De OCR‑output kan verkeerd herkende tekens bevatten (bijv. “l” vs “1”) of echte typefouten uit het bron‑document. De spell‑checker scant de string, lokaliseert verdachte tokens en stelt alternatieven voor.

## Stap 4: Spelfouten detecteren en spellingsuggesties krijgen

Nu voeren we de OCR‑tekst in de checker:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` is een collectie waarbij elk item het foutieve woord en een array met mogelijke correcties bevat.

## Stap 5: De resultaten weergeven

Tot slot itereren we over de collectie en printen we een mens‑leesbaar rapport:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Verwachte console‑output

Stel dat `letter_with_typos.png` de zin bevat:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Het uitvoeren van de demo levert iets als het volgende op:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Merk op dat elke typefout wordt gekoppeld aan een handvol plausibele correcties—precies wat je nodig hebt bij het bouwen van een gebruiksvriendelijke correctie‑UI.

## Volledig werkend voorbeeld

Hieronder staat het **complete, copy‑paste‑klare** programma. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad naar je afbeeldingsbestand.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Randgevallen om in overweging te nemen**  
> - **Lege afbeelding:** Als de OCR‑engine een lege string retourneert, zal `spellChecker.Check` simpelweg een lege collectie teruggeven—geen crash.  
> - **Niet‑Engelse tekst:** Vervang `OcrLanguage.English` door `OcrLanguage.French` (of een andere ondersteunde taal) om **spelfouten te detecteren** in andere locale.  
> - **Grote documenten:** Voor multi‑page PDF’s zou je over elke pagina itereren, OCR uitvoeren en vervolgens de resultaten aggregeren vóór het spell‑checken.

## Visueel overzicht (Afbeeldings‑alt‑tekst)

![Diagram dat de stroom toont om OCR op afbeelding uit te voeren, tekst uit afbeelding te extraheren en vervolgens spelfouten met spellingsuggesties te detecteren](perform-ocr-on-image-flow.png)

*Het diagram hierboven illustreert de end‑to‑end‑pipeline: afbeelding → OCR‑engine → ruwe tekst → spell‑checker → suggesties.*

## Veelgestelde vragen & Pro‑tips

| Vraag | Antwoord |
|----------|--------|
| **Heb ik een internetverbinding nodig?** | Nee. Aspose.OCR draait volledig lokaal; perfect voor offline of beveiligde omgevingen. |
| **Hoe nauwkeurig is de spell‑checker?** | Hij gebruikt een woordenboek van ~150 k Engelse woorden en fuzzy matching, dus de meeste gangbare typefouten worden opgevangen. |
| **Kan ik het woordenboek aanpassen?** | Ja. `SpellChecker.AddUserDictionary("custom.txt")` laat je domeinspecifieke termen (bijv. productnamen) laden. |
| **Wat als de afbeelding scheef staat?** | De OCR‑engine detecteert automatisch de oriëntatie, maar je kunt handmatig `ocrEngine.ImagePreprocessing.Rotate(angle)` aanroepen voor hardnekkige gevallen. |
| **Is er een manier om suggesties te markeren in de UI?** | Nadat je de `misspellings`‑collectie hebt, kun je elk `entry.Word` terugkoppelen naar de positie in `ocrResult.Text` en onderstrepen in een RichTextBox of web‑view. |

## Conclusie

We hebben je laten zien **hoe je OCR op afbeelding uitvoert**, **tekst uit afbeelding extraheert**, en vervolgens **spelfouten detecteert** terwijl je **spellingsuggesties krijgt**—alles met een beknopte C# console‑app. Het kernidee is simpel: laat Aspose.OCR het zware werk van tekenherkenning doen, en laat de ingebouwde spell‑checker de output opschonen. Vanaf hier kun je de demo uitbreiden tot een volledige documentverwerkingsservice, integreren met een web‑API, of koppelen aan een desktop‑editor.

Klaar voor de volgende stap? Probeer de taal te wisselen naar Spaans, voer een multi‑page PDF in, of bouw een kleine WPF‑frontend waarmee gebruikers op een woord kunnen klikken om een suggestie te accepteren. De bouwblokken liggen al klaar—blijf experimenteren.

Als je tegen problemen aanloopt of ideeën hebt voor uitbreidingen, laat dan een reactie achter. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}