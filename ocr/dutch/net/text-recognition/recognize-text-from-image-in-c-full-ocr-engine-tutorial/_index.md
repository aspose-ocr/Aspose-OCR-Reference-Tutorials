---
category: general
date: 2026-06-06
description: Herken tekst van een afbeelding met de C# OCR-engine. Leer hoe je een
  afbeelding naar JSON converteert, een afbeelding naar XML converteert en een afbeelding
  laadt voor OCR in enkele minuten.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: nl
og_description: Herken tekst van afbeelding met C# OCR‑engine. Exporteer resultaten
  naar JSON en XML, en beheer het laden van afbeeldingen voor OCR.
og_title: Tekst herkennen uit afbeelding in C# – Volledige OCR‑engine tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: Tekst herkennen uit afbeelding in C# – Volledige OCR‑engine tutorial
url: /nl/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst herkennen van afbeelding in C# – Volledige OCR Engine Tutorial

Heb je ooit **tekst van afbeelding moeten herkennen** maar wist je niet welke C#-bibliotheek je moest kiezen? Je bent niet de enige—ontwikkelaars worstelen voortdurend met het omzetten van gescande bonnen, screenshots of handgeschreven notities naar doorzoekbare tekst. Het goede nieuws? Met een moderne **OCR engine C#** kun je het in slechts een paar regels doen, en dan **afbeelding naar JSON converteren** of **afbeelding naar XML converteren** voor downstream verwerking.

In deze gids lopen we elke stap door: het installeren van het OCR‑pakket, het laden van een afbeelding voor OCR, het extraheren van de tekst, en uiteindelijk het exporteren van de resultaten naar zowel JSON als XML. Aan het einde heb je een zelfstandige console‑app die je in elk .NET‑project kunt gebruiken. Geen vage verwijzingen, alleen een complete, uitvoerbare oplossing.

## Wat je zult meenemen

- Een duidelijk beeld van hoe je **load image for OCR** gebruikt met een populaire C# OCR‑engine.  
- Werkende code die **recognize text from image** en een rijk resultaatobject retourneert.  
- Eenvoudige snippets die **convert image to JSON** en **convert image to XML** uitvoeren zonder extra bibliotheken.  
- Tips voor het verwerken van multi‑page PDF’s, verschillende afbeeldingsformaten, en veelvoorkomende valkuilen zoals scans met weinig contrast.  

### Vereisten

- .NET 6 SDK of later (je kunt ook .NET Framework 4.8 targeten als je dat liever hebt).  
- Basis C#‑kennis—niets geavanceerds, alleen een begrip van klassen en `async`/`await`.  
- Een afbeeldingsbestand (`structured.png` in de voorbeelden) dat je wilt OCR’en.  

Als je dat hebt, laten we beginnen.

---

## Tekst herkennen van afbeelding – OCR‑engine instellen

Allereerst. We hebben een betrouwbare OCR‑bibliotheek nodig. Voor deze tutorial gebruiken we **IronOcr**, een commerciële engine die wordt geleverd met een gratis community‑editie op NuGet. Het ondersteunt Engels direct en levert ons de `OcrEngine`‑klasse die in het oorspronkelijke fragment wordt getoond.

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **Pro tip:** Als je een strakker budget hebt, vervang `IronOcr` door `Tesseract`—de API is iets anders maar de concepten blijven identiek.

Nu een nieuw console‑project maken en de benodigde `using`‑statements toevoegen:

```csharp
using IronOcr;
using System.IO;
```

### Stap‑voor‑stap engineconfiguratie

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*Waarom dit belangrijk is:* Het initialiseren van de engine één keer en hergebruiken voor veel afbeeldingen vermindert overhead. Bovendien voorkomt het expliciet instellen van de taal de auto‑detect‑routine van de engine, die trager en minder nauwkeurig kan zijn.

---

## Afbeelding laden voor OCR – De engine de juiste data geven

De engine verwacht een `OcrInput`‑object. Je kunt het wijzen naar een bestandspad, een stream, of zelfs een `Bitmap`. Hier is de eenvoudigste aanpak:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **Randgeval:** Als je bron een multi‑page PDF is, roep dan `input.AddPdf("file.pdf")` aan in plaats van een PNG. De OCR‑engine behandelt elke pagina automatisch als een aparte afbeelding.

---

## Tekst herkennen van afbeelding – OCR‑proces uitvoeren

Met de engine en input klaar, is de daadwerkelijke herkenning een één‑regelige code:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` is een `OcrResult`‑object dat bevat:

- `Text` – ruwe geëxtraheerde string.  
- `Lines` – collectie van `OcrLine`‑objecten met vertrouwensscores.  
- `Words` – collectie van individuele woorden, ook met vertrouwensscore.  

Je kunt het direct in de debugger inspecteren, maar meestal wil je de data serialiseren.

---

## Afbeelding naar JSON converteren – OCR‑resultaten exporteren

IronOcr wordt geleverd met ingebouwde JSON‑serialisatie via `System.Text.Json`. Het volgende fragment schrijft een net JSON‑bestand naast je bronafbeelding:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**Wat je zult zien:** een mooi geformatteerd JSON‑document dat de ruwe tekst, vertrouwensscores en begrenzingskaders voor elke regel en elk woord bevat. Deze structuur is perfect om te voeden aan downstream‑services zoals ElasticSearch of Azure Cognitive Search.

---

## Afbeelding naar XML converteren – Gestructureerde data‑output

Sommige legacy‑systemen verwachten nog steeds XML. De `ToXml()`‑methode van IronOcr biedt een snelle conversie:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

De XML spiegelt de JSON‑hiërarchie, met `<Line>`‑ en `<Word>`‑elementen die `Confidence`‑attributen bevatten. Als je een aangepast schema nodig hebt, kun je `result` handmatig projecteren naar een `XDocument`—de API is volledig LINQ‑compatibel.

---

## Volledige end‑to‑end voorbeeldcode

Alles samenvoegend, hier is een kant‑en‑klaar `Program.cs`:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**Verwachte output** (ingekort voor de beknoptheid):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

Voer het programma uit met `dotnet run`. Als alles correct is aangesloten, zie je de console‑dump en verschijnen er twee bestanden in `YOUR_DIRECTORY`.

---

## Veelgestelde vragen & valkuilen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de afbeelding een JPEG is met EXIF-rotatie?* | Gebruik `input.AutoRotate()` vóór `Deskew()`. IronOcr leest de EXIF‑tag en corrigeert de oriëntatie. |
| *Kan ik een map met afbeeldingen in één keer OCR’en?* | Absoluut. Plaats de bovenstaande logica in een `foreach (var file in Directory.GetFiles(folder, "*.png"))`‑lus. |
| *Hoe verbeter ik de nauwkeurigheid bij ruisende scans?* | Verhoog `input.Denoise()` en overweeg `input.BlackWhiteThreshold(120)`. Geef ook een taalpakket op dat overeenkomt met de taal van het document. |
| *Is het JSON‑formaat compatibel met andere OCR‑bibliotheken?* | Het schema is algemeen genoeg—`Text`, `Lines`, `Words`—zodat je het kunt mappen naar de output van Tesseract met minimale transformatie. |

---

## Prestatietips (Pro‑niveau)

- **Herbruik de engine**: Het instantieren van `IronTesseract` binnen een strakke lus kan de doorvoer met tot 30 % verminderen. Houd een singleton per applicatiedomein.  
- **Paralleliseer I/O**: Als je tientallen afbeeldingen verwerkt, lees ze dan gelijktijdig in het geheugen (`Task.WhenAll`) en geef elke `OcrInput` aan dezelfde engine—IronOcr is thread‑safe.  
- **Batch‑export**: In plaats van elk JSON/XML‑bestand afzonderlijk te schrijven, verzamel resultaten in één collectie en serialiseer één keer. Dit vermindert schijfactiviteit.

---

## Volgende stappen & gerelateerde onderwerpen

Nu je **tekst van afbeelding kunt herkennen**, overweeg de pipeline uit te breiden:

- **Zoekintegratie** – stuur de JSON naar Elasticsearch voor full‑text zoeken.  
- **Documentclassificatie** – voer de OCR‑output in een lichtgewicht ML‑model om facturen, contracten of bonnen automatisch te labelen.  
- **Handgeschreven tekst** – schakel het taalpakket naar `OcrLanguage.EnglishHandwritten` (beschikbaar in de premium‑tier van IronOcr).  

Elk van deze bouwt voort op de basis die je net hebt gelegd, en ze houden je weken bezig.

## Conclusie

We hebben zojuist behandeld hoe je **tekst van afbeelding kunt herkennen** met een moderne **OCR engine C#**, vervolgens **afbeelding naar JSON** en **afbeelding naar XML** kunt converteren, en tenslotte hoe je **afbeelding voor OCR kunt laden** op een robuuste manier. Het volledige voorbeeld draait in minder dan een minuut, en de geëxporteerde bestanden zijn klaar voor elk downstream‑systeem.

Probeer de code uit, pas de

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}