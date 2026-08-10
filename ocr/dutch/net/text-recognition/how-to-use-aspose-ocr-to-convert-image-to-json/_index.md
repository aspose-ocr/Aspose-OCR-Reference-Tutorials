---
category: general
date: 2026-03-15
description: Hoe je Aspose OCR gebruikt om tekst uit afbeeldingen te extraheren en
  een afbeelding naar JSON te converteren in C#. Leer tekst uit PNG te herkennen en
  krijg snel gestructureerde output.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: nl
og_description: Hoe je Aspose OCR gebruikt om tekst uit afbeeldingen te extraheren
  en een afbeelding naar JSON te converteren in C#. Deze gids leidt je stap voor stap
  door het herkennen van tekst uit PNG en het verkrijgen van gestructureerde output.
og_title: Hoe Aspose OCR te gebruiken om een afbeelding naar JSON te converteren
tags:
- Aspose
- OCR
- C#
- JSON
title: Hoe Aspose OCR te gebruiken om een afbeelding naar JSON te converteren
url: /nl/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

talen, maar je moet de `Language`‑eigenschap dienovereenkomstig instellen (bijv. `ocrEngine.Configuration.Language = Language.English;`)."

Next heading:

## Full Working Example (Copy‑Paste Ready)

Translate: "## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)"

Code block: keep as is.

But there is a truncated line at end: "throw new InvalidOperationException("OCR". The original truncated. We'll keep as is.

After code block, we have closing shortcodes.

We need to ensure we keep the shortcodes exactly.

Now produce final content with translations.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Aspose OCR te gebruiken om afbeelding naar JSON te converteren

Hoe Aspose OCR te gebruiken is een veelgestelde vraag wanneer ontwikkelaars tekst uit afbeeldingen moeten halen. Als je **afbeelding naar JSON converteren** of **tekst herkennen uit PNG** wilt, biedt deze gids alles wat je nodig hebt—geen poespas, alleen een praktische, end‑to‑end oplossing.

In de komende paar minuten lopen we alles door wat je nodig hebt: de bibliotheek installeren, de engine configureren voor JSON‑uitvoer, een bon‑PNG laden, OCR uitvoeren en uiteindelijk het resultaat naar een `.json`‑bestand schrijven. Aan het einde kun je **tekst uit afbeelding** bestanden extraheren met één methode‑aanroep, en begrijp je waarom elke stap belangrijk is.

> **Pro tip:** Aspose OCR werkt met een breed scala aan afbeeldingsformaten (PNG, JPEG, BMP, TIFF). De onderstaande code werkt met al deze formaten, zodat je geen formaat‑specifieke logica hoeft te schrijven.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)
- Een geldig Aspose.OCR NuGet‑pakket (gratis proefversie of gelicentieerd)
- Een afbeeldingsbestand dat je wilt verwerken (bijv. `receipt.png`)
- Visual Studio, VS Code, of elke C#‑editor die je verkiest  

Dat is alles—geen extra afhankelijkheden, geen externe services. Klaar? Laten we beginnen.

![hoe aspose OCR engine te gebruiken](image-placeholder.png "hoe aspose OCR engine te gebruiken")

## Hoe Aspose OCR te gebruiken – JSON‑uitvoer configureren

Het eerste wat je moet doen wanneer je **hoe aspose** voor OCR gebruikt, is een `OcrEngine`‑instantie maken en aangeven dat deze JSON moet genereren. Deze kleine configuratie‑schakelaar bespaart je het handmatig serialiseren van het resultaat later.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Waarom dit belangrijk is:** Door `OutputFormat` op `Json` in te stellen, structureert de OCR‑engine de tekst al in een hiërarchie van pagina’s, regels en woorden. Je hoeft later geen ruwe strings meer te parseren, wat downstream‑verwerking—zoals het invoeren van gegevens in een database—veel schoner maakt.

## Afbeelding naar JSON converteren met Aspose OCR

Nu de engine is geconfigureerd, laten we het **afbeelding naar JSON converteren** gedeelte in meer detail bespreken.

1. **Laad de afbeelding** – `Image.FromFile` werkt voor elk ondersteund formaat. Als je met een stream werkt (bijv. een geüpload bestand), kun je in plaats daarvan `Image.FromStream` gebruiken.  
2. **Voer `Recognize` uit** – deze methode retourneert een `OcrResult`‑object. Omdat we de uitvoer op JSON hebben ingesteld, bevat `ocrResult.Text` al een JSON‑string.  
3. **Schrijf het bestand** – `File.WriteAllText` is de eenvoudigste manier om de JSON op te slaan. Als je het in een cloud‑bucket wilt opslaan, vervang dan deze regel door de juiste SDK‑aanroep.

### Verwachte JSON‑output

Een typisch JSON‑payload ziet er als volgt uit (ingekort voor de beknoptheid):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Je kunt deze structuur nu in elk downstream‑systeem gebruiken—of het nu een rapportagetool, een machine‑learning‑model of een eenvoudig logbestand is.

## Tekst uit afbeelding extraheren met Aspose OCR

Als je alleen de ruwe string nodig hebt (d.w.z. je geeft geen om JSON), schakel dan eenvoudig de uitvoerindeling terug naar platte tekst:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Wanneer kies je platte tekst?**  
- Snelle debugging of console‑output.  
- Scenario’s waarin je aangepaste post‑processing toepast (bijv. regex‑extractie).  

Maar onthoud, **tekst uit afbeelding extraheren** met JSON geeft je positionele data—handig voor het markeren van tekst in een UI of het uitlijnen met formuliervelden.

## Tekst herkennen uit PNG‑bestanden

PNG is een verliesvrij formaat, wat vaak leidt tot betere OCR‑nauwkeurigheid vergeleken met sterk gecomprimeerde JPEG’s. Hier is een snelle checklist om ervoor te zorgen dat je de beste resultaten krijgt wanneer je **tekst herkent uit PNG**:

| Checklist‑item | Waarom het helpt |
|----------------|-------------------|
| Gebruik een DPI van 300+ | Hogere resolutie geeft de engine meer pixels om mee te werken. |
| Houd de afbeelding grijswaarden | Vermindert ruis; Aspose OCR converteert automatisch, maar voorbewerking kan het versnellen. |
| Verwijder achtergrondrommel | Schone achtergronden verbeteren de vertrouwensscores. |

Als je lage vertrouwensscores tegenkomt, probeer dan de DPI te verhogen of een eenvoudige drempel‑filter toe te passen voordat je de afbeelding aan Aspose geeft.

## OCR‑resultaten programmatisch extraheren

Naast het opslaan van de JSON, wil je misschien programmatisch specifieke velden lezen—bijv. het totaalbedrag op een bon. Omdat de JSON een hiërarchie bevat, kun je deze deserialiseren naar een C#‑object:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Nu kun je `ocrData` bevragen met LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Waarom dit werkt:** De JSON vertelt al waar elk woord zich op de pagina bevindt, zodat je betrouwbaar velden kunt lokaliseren, zelfs als de lay-out enigszins verandert.

## Randgevallen & Veelvoorkomende valkuilen

- **Null‑resultaat:** Als `ocrEngine.Recognize` `null` retourneert, is de afbeelding mogelijk niet ondersteund of corrupt. Bescherm hier altijd tegen:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Grote bestanden:** Voor afbeeldingen van meerdere megabytes, overweeg de afbeelding te streamen of te verkleinen vóór OCR om overmatig geheugenverbruik te voorkomen.

- **Licentie‑problemen:** De proefversie voegt een watermerk toe aan de output. Zorg ervoor dat je je licentie vroeg in het programma laadt:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Niet‑Latijnse scripts:** Aspose OCR ondersteunt veel talen, maar je moet de `Language`‑eigenschap dienovereenkomstig instellen (bijv. `ocrEngine.Configuration.Language = Language.English;`).

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}