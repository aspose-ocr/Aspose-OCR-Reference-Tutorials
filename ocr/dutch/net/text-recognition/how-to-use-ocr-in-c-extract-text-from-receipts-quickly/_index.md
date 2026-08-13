---
category: general
date: 2026-03-05
description: Hoe OCR te gebruiken in C# om tekst uit bonafbeeldingen te extraheren.
  Leer hoe je een afbeelding laadt voor OCR en een bonafbeelding in enkele minuten
  herkent.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: nl
og_description: Hoe OCR in C# te gebruiken voor het extraheren van tekst uit bonnen.
  Volg deze stapsgewijze handleiding om een afbeelding te laden voor OCR en bonafbeeldingen
  efficiënt te herkennen.
og_title: hoe OCR te gebruiken in C# – Snelle bontekstextractie
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Hoe OCR in C# te gebruiken – Haal snel tekst uit bonnen
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe OCR te gebruiken in C# – Tekst snel extraheren uit kassabonnen

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** om gegevens rechtstreeks uit een foto van een kassabon te halen? Je bent niet de enige. In veel kleine‑ondernemingsapps is de bottleneck het omzetten van een wazige PNG naar gestructureerde tekst waarmee je echt kunt werken.  

Het goede nieuws? Met een paar regels C# en Aspose.OCR kun je **een afbeelding laden voor OCR**, de engine uitvoeren, en **een kassabonafbeelding herkennen** in minder dan een minuut. Hieronder zie je een volledig, kant‑klaar voorbeeld, plus tips voor de lastige details die de meeste tutorials overslaan.

## Wat deze gids behandelt

We lopen alles door wat je moet weten:

* Het installeren van het Aspose.OCR NuGet‑pakket.  
* Het opzetten van de OCR‑engine – de kern van **hoe OCR te gebruiken** op de juiste manier.  
* Het laden van een kassabonbestand (dat is de **load image for OCR** stap).  
* Het uitvoeren van het herkenningsproces en zowel JSON als XML lay‑outgegevens ophalen.  
* Het afhandelen van veelvoorkomende valkuilen zoals ontbrekende licenties of niet‑ondersteunde afbeeldingsformaten.  

Aan het einde heb je een zelfstandige applicatie die de tekst uit elke kassabon die je in een map plaatst, extraheert. Geen externe services, geen verborgen magie.

## Vereisten

* .NET 6 SDK of later (de code compileert ook met .NET Core).  
* Een geldig Aspose.OCR‑licentiebestand (`Aspose.OCR.lic`). Je kunt een gratis proefversie krijgen van Aspose als je er nog geen hebt.  
* Een voorbeeld‑kassabonafbeelding – `receipt.png` werkt prima, maar elk gangbaar rasterformaat is geschikt.  

Als je die al hebt, geweldig – laten we beginnen.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Stap 1: Installeer Aspose.OCR en maak een nieuw project

Allereerst: je hebt de bibliotheek nodig die het zware werk doet. Open een terminal in je projectmap en voer uit:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Dat commando maakt een console‑app en haalt het nieuwste Aspose.OCR‑pakket op. Naar mijn ervaring maakt een korte projectnaam de gegenereerde paden makkelijker leesbaar, vooral wanneer je meerdere demo‑apps gaat beheren.

## Stap 2: Initialiseert de OCR‑engine – het hart van **hoe OCR te gebruiken**

Nu schrijven we de code die de vraag beantwoordt “**hoe OCR te gebruiken** in C#”. Open `Program.cs` en vervang de inhoud door de onderstaande snippet. Let op de commentaren – ze leggen het *waarom* achter elke regel uit, niet alleen het *wat*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Waarom dit werkt

* **`OcrEngine`** is het toegangspunt; het bevat alle configuraties die je later kunt aanpassen (taal, DPI, enz.).  
* **`SetLicense`** verwijdert het evaluatiewatermerk – een cruciale stap wanneer je de code wilt distribueren.  
* **`ImageStream.FromFile`** doet het **load image for OCR** werk, en ondersteunt PNG, JPEG, BMP, TIFF en meer.  
* **`Recognize()`** is de methode die daadwerkelijk **recognize receipt image** uitvoert. Intern voert het binarisatie, segmentatie en tekenclassificatie uit.  
* Exporteren naar JSON en XML geeft je zowel een mens‑leesbare dump als een machine‑vriendelijke structuur die je kunt doorgeven aan downstream‑parsers.

## Stap 3: Voer de demo uit en controleer de output

Compileer en voer uit:

```bash
dotnet run
```

Als alles correct is ingesteld zie je iets als:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

De console print de platte tekst, terwijl `receipt.json` en `receipt.xml` gedetailleerde lay‑outinformatie bevatten (coördinaten, vertrouwensscores, enz.). Die bestanden zijn handig als je later elke regel aan een database‑veld wilt koppelen.

## Randgevallen & Pro‑tips

### 1️⃣ Ontbrekende of ongeldige licentie
Als `SetLicense` faalt, schakelt de engine over naar de proefmodus en krijg je een watermerk in de output. Plaats de aanroep in een try/catch en log een vriendelijke melding:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Niet‑ondersteunde afbeeldingsformaten
Aspose.OCR ondersteunt de meeste rasterformaten, maar als je een PDF of een multi‑page TIFF invoert, moet je de pagina die je nodig hebt eerst naar een afbeelding converteren. De `Aspose.PDF`‑bibliotheek kan die conversie uitvoeren.

### 3️⃣ Grote kassabonnen & prestaties
Het verwerken van een afbeelding van 10 MB kan traag zijn. Verlaag de resolutie voordat je deze aan de engine geeft:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

De `Resize`‑methode behoudt de beeldverhouding (`0` voor hoogte) en verkleint de bestandsgrootte drastisch zonder de OCR‑nauwkeurigheid voor typische kassabonnen te verliezen.

### 4️⃣ Taal‑ en lettertype‑problemen
Kassabonnen kunnen speciale tekens bevatten (€, ¥, enz.). Stel de taal expliciet in als je de locale kent:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Voor kassabonnen met meerdere talen kun je de meertalige modus inschakelen:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Gestructureerde gegevens extraheren
De ruwe tekst is nuttig, maar de meeste apps hebben gestructureerde velden nodig (datum, totaal, items). De JSON‑lay‑out bevat `BoundingBox`‑coördinaten voor elk woord. Je kunt het als volgt post‑processen:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Die snippet toont het idee; in productie zou je waarschijnlijk een reguliere expressie of een kleine regel‑engine gebruiken.

## Veelgestelde vragen

**Q: Werkt dit op Linux?**  
A: Absoluut. Aspose.OCR is cross‑platform; installeer simpelweg de .NET‑runtime op je Linux‑machine en dezelfde code werkt.

**Q: Wat als ik tientallen kassabonnen per minuut moet verwerken?**  
A: Gebruik een `Parallel.ForEach`‑lus en hergebruik één `OcrEngine`‑instantie – deze is thread‑safe voor alleen‑lezen operaties. Vergeet niet de licentie‑concurrentielimieten te respecteren.

**Q: Werkt dit met mobiele foto’s die onder een hoek zijn genomen?**  
A: De engine bevat basis‑deskewing, maar bij sterk scheve afbeeldingen kun je eerst een beeldverwerkingsbibliotheek (bijv. OpenCV) gebruiken om de kassabon recht te zetten.

## Volledig werkend voorbeeld (Kopie‑Plak)

Hieronder staat het *complete* programma dat je in `Program.cs` kunt plakken. Er zijn geen andere bestanden nodig, behalve de licentie en een kassabon‑afbeelding.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}