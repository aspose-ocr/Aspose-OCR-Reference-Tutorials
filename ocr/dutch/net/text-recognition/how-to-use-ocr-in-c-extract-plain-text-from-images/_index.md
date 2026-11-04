---
category: general
date: 2026-04-06
description: Hoe OCR in C# te gebruiken om platte tekst uit JPG‑afbeeldingen te extraheren,
  inclusief Cyrillische tekens. Leer hoe je een afbeelding laadt voor OCR, tekst in
  JPG herkent en betrouwbare resultaten krijgt.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: nl
og_description: Hoe OCR in C# te gebruiken om platte tekst uit JPG‑bestanden te extraheren.
  Deze gids laat zien hoe je een afbeelding voor OCR laadt, tekst in JPG herkent en
  Cyrillische tekst verwerkt.
og_title: Hoe OCR in C# te gebruiken – Haal platte tekst uit afbeeldingen
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Hoe OCR in C# te gebruiken – Platte tekst uit afbeeldingen extraheren
url: /nl/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Platte tekst uit afbeeldingen extraheren

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** in een .NET‑project zonder te worstelen met native bibliotheken? Misschien heb je een map met gescande bonnetjes, een handvol screenshots met Cyrillische bijschriften, of moet je gewoon de tekst uit een JPEG halen voor snelle analyse. Het goede nieuws is dat Aspose OCR dat hele proces een eitje maakt.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien **hoe je OCR kunt gebruiken** om **platte tekst** uit een JPEG‑afbeelding te **extraheren**, hoe je **een afbeelding laadt voor OCR**, en zelfs hoe je **Cyrillische tekst** kunt **extraheren** wanneer de brontaal niet Latijn is. Aan het einde heb je een kleine console‑app die de herkende tekst rechtstreeks naar de console print—geen extra bestanden, geen mysterieuze bijwerkingen.

> **Wat je krijgt**  
> * Een stap‑voor‑stap gids die je kunt copy‑pasten in Visual Studio.  
> * Uitleg over *waarom* elke regel belangrijk is, niet alleen *wat* hij doet.  
> * Tips voor het omgaan met grote afbeeldingen, meerdere talen, en veelvoorkomende valkuilen.

## Vereisten

* .NET 6 SDK of later (de code werkt ook met .NET Core en .NET Framework).  
* Visual Studio 2022 (of elke editor die je verkiest).  
* Internettoegang de eerste keer dat je het voorbeeld uitvoert—Aspose OCR downloadt taalpakketten on‑demand.

Als je het Aspose OCR NuGet‑pakket mist, behandelen we dat in de eerste stap.

## Stap 1 – Installeer Aspose OCR via NuGet (en waarom het belangrijk is)

De **load image for OCR** stap kan niet plaatsvinden totdat de bibliotheek aanwezig is. Het gebruik van NuGet garandeert dat je de nieuwste, beveiligings‑gepatchte binaries krijgt en automatisch alle vereiste afhankelijkheden binnenhaalt.

```bash
dotnet add package Aspose.OCR
```

*Waarom dit belangrijk is*: Aspose OCR wordt geleverd met een kleine core‑DLL en haalt taaldatasets alleen op wanneer je erom vraagt. Dat houdt je app lichtgewicht en voorkomt dat je megabytes aan ongebruikte taalbestaanden bundelt.

## Stap 2 – Initialiseer de OCR‑engine (het hart van **hoe je OCR kunt gebruiken**)

Het aanmaken van een `OcrEngine`‑instantie is de eerste echte code‑regel die van belang is voor **hoe je OCR kunt gebruiken**. De engine staat standaard in de “on‑demand” modus, wat betekent dat hij het taalpakket downloadt de eerste keer dat je een specifieke taal aanvraagt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Pro tip**: Als je achter een bedrijfsproxy werkt, stel `OcrEngine.Proxy` in vóór de eerste herkenningsaanroep zodat de download slaagt.

## Stap 3 – Kies de taal – **Cyrillische tekst extraheren** wanneer nodig

Aspose OCR ondersteunt tientallen scripts. Om **Cyrillische tekst te extraheren**, stel je simpelweg de `Language`‑eigenschap in op `OcrLanguage.Cyrillic`. De eerste keer dat deze regel wordt uitgevoerd, wordt de Cyrillische module (≈ 5 MB) opgehaald van Aspose’s CDN.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Als je afbeelding alleen Latijnse tekens bevat, kun je `Cyrillic` vervangen door `English`. Hetzelfde patroon werkt voor elke ondersteunde taal.

## Stap 4 – **Load Image for OCR** – Van schijf of stream

Nu **laden we de afbeelding voor OCR**. De `System.Drawing.Image`‑klasse ondersteunt de meeste gangbare formaten (JPG, PNG, BMP). Als je op een niet‑Windows platform werkt, overweeg dan `ImageSharp`, maar voor deze tutorial is het ingebouwde type voldoende.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Waarom dit belangrijk is**: Het laden van de afbeelding binnen een `using`‑blok garandeert dat de unmanaged GDI+‑resources snel worden vrijgegeven, waardoor geheugenlekken in langdurige services worden voorkomen.

## Stap 5 – **Recognize Text JPG** – Voer het OCR‑proces uit

Met de engine geconfigureerd en de afbeelding geladen, **herkennen we tekst jpg** eindelijk. De `Recognize`‑methode retourneert een `OcrResult` die de platte string, vertrouwensscores, en zelfs begrenzingskaders bevat als je die later nodig hebt.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Als je de nauwkeurigheid wilt bijstellen, kun je `ocrEngine.Config` aanpassen (bijv. `AutoRotate` inschakelen of `TextOrientation` instellen). Voor de meeste eenvoudige scenario's werken de standaardinstellingen verrassend goed.

## Stap 6 – **Extract Plain Text** – Toon het resultaat

Het laatste onderdeel van **hoe je OCR kunt gebruiken** is het halen van de herkende string uit `ocrResult` en er iets mee doen. Hier schrijven we het simpelweg naar de console, wat ook laat zien hoe je **platte tekst kunt extraheren** uit het result‑object.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Verwachte uitvoer

Als `cyrillic_sample.jpg` de zin “Привет мир” (Hello world) bevat, zou je moeten zien:

```
=== Recognized Text ===
Привет мир
```

Als de afbeelding onscherp is of de tekst te klein, kan de uitvoer fouten bevatten; je kunt `ocrResult.Confidence` inspecteren om te bepalen of je moet herproberen met een bron van hogere resolutie.

## Volledig, kant‑klaar voorbeeld

Hieronder staat het volledige programma. Kopieer het in een nieuw Console‑App‑project (`dotnet new console`) en voer het uit. Er zijn geen extra bestanden nodig, behalve de afbeelding waarnaar je verwijst.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Opmerking**: Vervang `YOUR_DIRECTORY\cyrillic_sample.jpg` door het daadwerkelijke pad naar je JPEG‑bestand.

## Veelgestelde vragen & randgevallen

### Wat als ik **recognize text jpg** nodig heb vanuit een stream in plaats van een bestand?

Je kunt direct een `MemoryStream` voeden:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Hoe ga ik om met meerdere talen in dezelfde afbeelding?

Stel `ocrEngine.Language` in op `OcrLanguage.Multilingual`. De engine zal automatisch elke script detecteren, wat handig is wanneer een bon Engels en Cyrillisch mengt.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Mijn afbeelding is enorm (meer dan 5 MP). Zult de engine vastlopen?

Grote afbeeldingen verhogen het geheugenverbruik en kunnen de herkenning vertragen. Een snelle voor‑resize helpt:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Kan ik de vertrouwensscore per regel krijgen?

Ja—`ocrResult.Lines` bevat `Confidence` per regel. Door er doorheen te itereren kun je resultaten met lage vertrouwensscore filteren.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Pro‑tips voor productie‑klare OCR

* **Cache language packs** – de eerste download kan enkele seconden duren; sla de bestanden op in een bekende map en stel `ocrEngine.LanguageDataPath` in om ze opnieuw te gebruiken.  
* **Batch processing** – hergebruik één `OcrEngine`‑instantie voor veel afbeeldingen; een nieuwe engine per bestand creëert onnodige overhead.  
* **Error handling** – wikkel de `Recognize`‑aanroep in een try/catch‑blok. Aspose gooit `OcrException` voor corrupte afbeeldingen of niet‑ondersteunde formaten.  
* **Logging** – registreer `ocrResult.Confidence` zodat je later kunt auditen welke pagina's handmatige controle nodig hadden.

## Conclusie

We hebben zojuist **hoe je OCR kunt gebruiken** in C# om **platte tekst** uit een JPEG te **extraheren**, de stappen getoond om **een afbeelding te laden voor OCR**, laten zien hoe je **recognize text jpg** uitvoert, en zelfs **Cyrillische tekst** uit de afbeelding gehaald. Het voorbeeld is volledig functioneel, vereist slechts één NuGet‑pakket, en kan worden uitgebreid om documenten met meerdere talen, batch‑taken, of realtime‑scan‑scenario's te verwerken.

Klaar voor de volgende uitdaging? Probeer de Cyrillische taal te vervangen door Arabisch, experimenteer met de `AutoRotate`‑vlag, of integreer de output in een zoekindex. De mogelijkheden zijn eindeloos

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}