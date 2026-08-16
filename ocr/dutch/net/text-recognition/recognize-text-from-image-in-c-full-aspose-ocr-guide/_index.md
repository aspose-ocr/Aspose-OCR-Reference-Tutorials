---
category: general
date: 2026-04-03
description: herken tekst uit een afbeelding met Aspose OCR in C#. Leer hoe je een
  afbeelding laadt voor OCR, tekst uit een afbeelding extraheert, een JSON‑bestand
  schrijft in C# en OCR uitvoert op PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: nl
og_description: herken tekst van afbeelding met Aspose OCR in C#. Stapsgewijze handleiding
  om afbeelding te laden voor OCR, tekst uit afbeelding te extraheren, JSON‑bestand
  te schrijven in C# en OCR uit te voeren op PNG.
og_title: herken tekst uit afbeelding in C# – Complete Aspose OCR Tutorial
tags:
- OCR
- C#
- Aspose
title: tekst herkennen uit afbeelding in C# – Volledige Aspose OCR-gids
url: /nl/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit afbeelding herkennen in C# – Complete Aspose OCR Tutorial

Heb je ooit **tekst uit een afbeelding moeten herkennen** maar wist je niet welke bibliotheek je moest kiezen? Misschien heb je een stapel gescande bonnetjes, een PNG‑screenshot, of een handgeschreven notitie die je wilt omzetten naar doorzoekbare data. Het goede nieuws: met Aspose.OCR kun je dit in een paar regels C#‑code doen, en je krijgt zelfs een net JSON‑bestand dat je in andere systemen kunt gebruiken.

In deze tutorial lopen we stap voor stap door het laden van een afbeelding voor OCR, het extraheren van tekst uit de afbeelding, het serialiseren van het resultaat naar een JSON‑bestand, en tenslotte het verwerken van PNG‑bestanden zonder moeite. Aan het einde heb je een kant‑klaar console‑applicatie die **tekst uit afbeelding herkent** en de uitvoer schrijft naar *output.json*.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Framework)
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`)
- Een PNG (of een ander ondersteund formaat) die je wilt verwerken
- Visual Studio, VS Code, of een andere C#‑editor naar keuze

Er zijn geen extra third‑party libraries nodig—alleen de Aspose OCR‑engine en de ingebouwde `System.Text.Json`‑serializer.

## Stap 1: Tekst uit afbeelding herkennen met Aspose OCR

Het eerste wat je moet doen is een `OcrEngine`‑instantie maken. Dit object doet het zware werk achter de schermen.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Waarom dit belangrijk is:** Het één keer instantieren van `OcrEngine` en hergebruiken is efficiënter dan voor elk bestand een nieuwe engine te maken. De aanroep `RecognizeToResult` retourneert een `OcrResult`‑object dat al de geëxtraheerde tekst, vertrouwensscores en begrenzingsvakken bevat—perfect voor verdere verwerking.

## Stap 2: Afbeelding laden voor OCR – verschillende formaten afhandelen

Aspose OCR kan PNG, JPEG, BMP en vele andere formaten lezen. Als je een PNG met transparantie verwerkt, wil je die eerst flattenen om onverwachte lege plekken te voorkomen.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Pro tip:** Controleer altijd of de afmetingen van de afbeelding redelijk zijn (bijv. breedte > 50 px). Zeer kleine afbeeldingen kunnen ervoor zorgen dat de OCR‑engine tekens mist, wat leidt tot lage vertrouwensscores.

## Stap 3: JSON‑bestand schrijven in C# – de output bruikbaar maken

De `System.Text.Json`‑serializer is snel en ingebouwd, maar je kunt hem vervangen door `Newtonsoft.Json` als je aangepaste converters nodig hebt. Het voorbeeld hierboven gebruikt al `WriteIndented = true`, zodat het resulterende bestand mens‑leesbaar is.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Het hebben van OCR‑data in JSON maakt het eenvoudig om deze te importeren in databases, over HTTP te versturen, of te voeden aan machine‑learning‑pijplijnen.

## Stap 4: Resultaat verifiëren – snelle sanity‑check

Na het uitvoeren van het programma, open `output.json` en zoek naar het veld `"Text"`. Als dit de verwachte string bevat, heb je met succes **tekst uit afbeelding geëxtraheerd**. Als de vertrouwensscore laag is, overweeg dan om de afbeelding voor te bewerken (bijv. contrast verhogen of een binaire drempel toepassen).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

Het uitvoeren van de console geeft iets als volgt weer:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Dat is een duidelijk teken dat de OCR heeft gewerkt zoals bedoeld.

## Veelvoorkomende valkuilen & randgevallen

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Lege output** | Afbeelding is te donker of heeft een niet‑ondersteunde kleurenruimte | Converteer naar grijstinten, verhoog de helderheid, of flatten de PNG (zie Stap 2) |
| **Onzinnige tekens** | Lage DPI (< 72) of veel ruis | Schaal de afbeelding op of pas een denoise‑filter toe vóór `RecognizeToResult` |
| **Grote bestanden veroorzaken geheugenstress** | Een multi‑megapixel PNG in een `Bitmap` laden verbruikt veel RAM | Verwerk afbeeldingen in delen of schaal ze omlaag terwijl leesbaarheid behouden blijft |
| **JSON‑serialisatie‑fout** | `OcrResult` bevat circulaire referenties (onwaarschijnlijk) | Gebruik `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus: OCR uitvoeren op PNG in een batch‑lus

Als je een map vol PNG‑bestanden hebt, kun je de demo uitbreiden om ze één voor één te verwerken:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Nu **voert het programma OCR uit op PNG**‑bestanden in bulk, en schrijft het voor elke afbeelding een bijbehorend JSON‑bestand.

## Conclusie

Je hebt zojuist geleerd hoe je **tekst uit afbeelding herkent** in C# met Aspose OCR, **afbeelding laadt voor OCR**, **tekst uit afbeelding extraheert**, en **JSON‑bestand schrijft in C#** om de resultaten op te slaan. Het volledige, uitvoerbare voorbeeld behandelt de essentiële stappen, legt uit waarom elk onderdeel belangrijk is, en laat zelfs zien hoe je PNG‑specifieke eigenaardigheden kunt afhandelen.

Volgende stappen? Probeer de JSON te voeden aan een zoekindex, combineer het met taalherkenning, of integreer het in een web‑API die uploads on‑the‑fly verwerkt. Je kunt ook Aspose’s ondersteuning voor handschriftherkenning verkennen als jouw use‑case dat vereist.

Vragen over randgevallen of prestatie‑optimalisatie? Laat een reactie achter—happy coding! 

![demo tekstherkenning van afbeelding](/images/ocr-demo.png "Diagram dat laat zien hoe Aspose OCR tekst uit een afbeelding herkent")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}