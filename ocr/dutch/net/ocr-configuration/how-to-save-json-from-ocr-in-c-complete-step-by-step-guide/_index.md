---
category: general
date: 2026-03-02
description: Leer hoe je JSON kunt opslaan terwijl je tekst uit een afbeelding haalt
  met Aspose OCR. Inclusief code om een JSON‑bestand te schrijven, tips voor het laden
  van bitmap‑afbeeldingen en een volledig C#‑voorbeeld.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: nl
og_description: Ontdek hoe je JSON kunt opslaan terwijl je tekst uit een afbeelding
  haalt met Aspose OCR. Complete C#‑code, stappen om een JSON‑bestand te schrijven
  en praktische tips.
og_title: Hoe JSON van OCR in C# op te slaan – Volledige programmeertutorial
tags:
- C#
- OCR
- Aspose
- JSON
title: Hoe JSON van OCR in C# op te slaan – Complete stapsgewijze handleiding
url: /nl/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe JSON van OCR in C# op te slaan – Complete stapsgewijze gids

Heb je je ooit afgevraagd **hoe je JSON** kunt opslaan die de tekst bevat die je net uit een afbeelding hebt gehaald? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze *tekst uit afbeelding* moeten extraheren en die informatie vervolgens moeten opslaan als een netjes geformatteerd JSON‑bestand. Het goede nieuws? De oplossing is vrij eenvoudig zodra je de juiste onderdelen hebt.

In deze tutorial lopen we een real‑world scenario door: met Aspose.OCR **tekst uit een afbeelding** extraheren, vervolgens **JSON‑bestand** wegschrijven, en uiteindelijk **hoe JSON op te slaan** op schijf. Onderweg laten we ook zien hoe je **bitmap‑afbeeldingen** correct laadt, en behandelen we een paar randgevallen die je kunt tegenkomen. Aan het einde heb je een zelfstandige C# console‑app die alles doet, van het laden van de afbeelding tot het produceren van een kant‑klaar JSON‑document.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)  
- Aspose.OCR voor .NET (je kunt een gratis proef‑NuGet‑pakket pakken)  
- Een voorbeeld‑PNG‑ of JPG‑afbeelding met Engelse tekst  
- Visual Studio, VS Code, of een andere C#‑compatibele IDE  

Er zijn geen extra bibliotheken nodig — alleen de standaard `System.Drawing` namespace voor bitmap‑verwerking en `System.Text.Json` voor serialisatie.

---

## Stap 1 – Laad de bitmap‑afbeelding (het “load bitmap image” gedeelte)

Voordat er OCR kan plaatsvinden, moet je de afbeelding in het geheugen krijgen als een `Bitmap`. Beschouw dit als het openen van een boek voordat je de pagina’s gaat lezen.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Pro tip:** Als de afbeelding groot is, overweeg dan eerst te schalen om de prestaties te verbeteren. De OCR‑engine werkt sneller op afbeeldingen onder de 2 MB.

---

## Stap 2 – Configureer de Aspose OCR Engine

Nu de bitmap klaar is, hebben we een `OcrEngine` nodig. Dit object weet hoe **tekst uit afbeelding** te **extraheren** en kan ons optioneel geometrische gegevens zoals begrenzings‑boxen geven.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Waarom `ExportBoundingBoxes` inschakelen? Als je ooit woorden in een UI wilt markeren, zijn die coördinaten goud waard. Als je ze niet nodig hebt, kun je de vlag op `false` zetten en wordt het JSON‑bestand iets slanker.

---

## Stap 3 – Voer OCR uit en krijg een gestructureerd resultaat

Met de engine geconfigureerd, is de volgende stap de daadwerkelijke **hoe je tekst extrahert** operatie. De `RecognizeToOcrResult`‑methode retourneert een rijk object dat de herkende tekst, vertrouwensscores en optionele lay‑out‑data bevat.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

De variabele `ocrResult` bevat nu alles wat je nodig hebt. Als je deze in de debugger inspecteert, zie je een hiërarchie van `Page`, `Paragraph`, `Line` en `Word` objecten, elk met hun eigen `Text`‑eigenschap.

---

## Stap 4 – Serialiseer het resultaat naar een geformatteerde JSON‑string

Hier begint de **hoe je JSON opslaat**‑magie echt. We gebruiken `System.Text.Json` omdat het ingebouwd, snel en out‑of‑the‑box pretty‑printing ondersteunt.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Als je een andere naamgevingsconventie nodig hebt (bijv. camelCase), voeg dan `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` toe aan de opties.

---

## Stap 5 – Schrijf de JSON naar schijf (de “write json file” stap)

Tot slot **schrijven we het JSON‑bestand** naar het bestandssysteem. Dit is het concrete antwoord op **hoe je JSON opslaat** in een C#‑omgeving.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Nadat deze regel is uitgevoerd, vind je een mooi ingesprongen `sample-page.json` naast je originele afbeelding. Open het met elke teksteditor of voer het in een andere service in — je OCR‑data is nu draagbaar.

---

## Stap 6 – Verifieer de output (Wat zou je moeten zien?)

Het uitvoeren van het programma moet een korte bevestiging naar de console printen:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Open het gegenereerde JSON‑bestand en je ziet iets als:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Als de `ExportBoundingBoxes`‑vlag `true` was, bevat elk woord ook `Rectangle`‑coördinaten. Handig voor downstream UI‑werk.

---

## Veelgestelde vragen & randgevallen

### Wat als het afbeeldingspad ongeldig is?

Wrap het laden van de bitmap in een `try/catch`‑blok en geef een duidelijke foutmelding:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Hoe ga ik om met niet‑Engelse talen?

Verander simpelweg de `Language`‑eigenschap:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose ondersteunt meer dan 50 talen, dus kies de taal die bij je bronmateriaal past.

### Moet ik `Bitmap`‑objecten disposen?

Ja. `Bitmap` implementeert `IDisposable`, dus plaats het in een `using`‑statement om native resources direct vrij te geven.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Wat als ik een compact JSON zonder inspringing wil?

Vervang de `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Dat verkleint de bestandsgrootte — handig voor scenario’s met beperkte bandbreedte.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

Hieronder staat het volledige programma dat alle stappen, foutafhandeling en best‑practice‑tips combineert. Sla het op als `Program.cs` en voer het uit vanaf de commandoregel of in je IDE.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Wat dit doet:**  
1. Controleert of de afbeelding bestaat.  
2. Laadt deze veilig met een `using`‑block.  
3. Voert OCR uit om **tekst uit afbeelding** te **extraheren**.  
4. Serialiseert het resultaat naar een mooi ingesprongen JSON‑string.  
5. Slaat die string op schijf op, waarmee de kernvraag **hoe je JSON opslaat** beantwoord wordt.

Voer `dotnet run` uit (of druk op F5 in Visual Studio) en je ziet het bevestigingsbericht zodra het bestand is geschreven.

---

## Conclusie

Je hebt nu een volledige, productieklare handleiding voor **hoe je JSON opslaat** die voortkomt uit OCR‑gebaseerde tekste­xtractie. Van het laden van een bitmap‑afbeelding tot het wegschrijven van een schoon JSON‑bestand, elke stap wordt uitgelegd met het “waarom” achter de code, zodat je de oplossing kunt aanpassen aan je eigen projecten.

Als je nieuwsgierig bent naar de volgende stap, overweeg dan:

- **Hoe je tekst** uit PDF’s kunt extraheren door elke pagina eerst naar een afbeelding te converteren.  
- Het gebruiken van de begrenzings‑box‑data om woorden te markeren in een WPF‑ of WinForms‑UI.  
- Het direct streamen van de JSON naar een web‑API in plaats van een bestand te schrijven (gebruik `HttpClient`).

Probeer het, pas de opties aan, en laat de OCR‑data de motor zijn van elke applicatie die je bouwt. Vragen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}