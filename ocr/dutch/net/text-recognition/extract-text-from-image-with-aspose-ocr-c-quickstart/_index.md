---
category: general
date: 2026-02-13
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je tekst
  uit een jpg kunt lezen en OCR op een afbeelding kunt uitvoeren met een compleet,
  uitvoerbaar voorbeeld.
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: nl
og_description: Tekst extraheren uit een afbeelding met Aspose OCR in C#. Deze gids
  laat zien hoe je tekst uit een jpg leest en OCR op een afbeelding uitvoert met een
  volledig codevoorbeeld.
og_title: Tekst extraheren uit afbeelding met Aspose OCR – C# Quickstart
tags:
- C#
- OCR
- Aspose
title: Tekst uit afbeelding extraheren met Aspose OCR – C# Quickstart
url: /nl/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding met Aspose OCR – C# Quickstart

Heb je ooit **tekst uit afbeelding moeten extraheren** maar wist je niet welke bibliotheek je moet kiezen? Je bent niet de enige—ontwikkelaars worstelen constant met het lezen van tekst uit jpg‑bestanden, vooral wanneer de inhoud in een niet‑Latijns schrift staat. Het goede nieuws? Met Aspose OCR kun je OCR uitvoeren op afbeeldingsbestanden in slechts een paar regels C#‑code, en de bibliotheek regelt het downloaden van taalpakketten on demand.

In deze tutorial lopen we een compleet, end‑to‑end voorbeeld door dat laat zien hoe je **tekst uit afbeelding kunt extraheren** met Aspose OCR, de herkenning beperkt tot Russisch, en het resultaat naar de console print. Aan het einde kun je tekst uit jpg‑bestanden lezen, OCR uitvoeren op afbeeldings‑assets van elke grootte, en de code aanpassen voor andere talen met minimale wijzigingen.

> **Wat je zult leren**
> * Hoe je Aspose OCR installeert en referentieert in een .NET‑project.  
> * De exacte stappen om **tekst uit afbeelding te extraheren**—het initialiseren van de engine, het selecteren van een taal, en het aanroepen van `RecognizeImage`.  
> * Waarom je de engine mogelijk wilt vergrendelen op één taalpakket (snelheid, nauwkeurigheid).  
> * Veelvoorkomende valkuilen zoals ontbrekende bestanden of niet‑ondersteunde formaten, en hoe je deze elegant afhandelt.  

## Vereisten

Voordat we beginnen, zorg ervoor dat je het volgende op je machine hebt:

| Vereiste | Reden |
|----------|-------|
| .NET 6.0 SDK or later | Aspose OCR richt zich op .NET Standard 2.0+, dus .NET 6 geeft je de nieuwste runtime‑functies. |
| Visual Studio 2022 (or any IDE you like) | Handig voor debugging, maar niet strikt vereist. |
| An image file (`cyrillic_sample.jpg`) that contains Cyrillic text | Een afbeeldingsbestand (`cyrillic_sample.jpg`) dat Cyrillische tekst bevat. We gebruiken dit bestand om **tekst uit jpg te lezen** te demonstreren. |
| Internet connection (first run only) | Aspose OCR downloadt taalpakketten on demand. |

Als je een van deze mist, haal ze dan nu—herstarten is niet nodig na het installeren van de SDK.

## Stap 1: Installeer Aspose OCR NuGet‑pakket

Het eerste wat je nodig hebt is de Aspose OCR‑bibliotheek. Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Dit commando haalt de nieuwste stabiele versie op (vanaf februari 2026 is dat 23.12) en voegt deze toe aan je `.csproj`. Het pakket bevat de core OCR‑engine en een lichtgewicht downloader voor taalpakketten, zodat je geen enorme bestanden met je app hoeft te bundelen.

> **Pro tip:** Als je achter een bedrijfsproxy werkt, stel dan de `http_proxy`‑omgevingsvariabele in voordat je het commando uitvoert om download‑fouten te voorkomen.

## Stap 2: Maak een console‑applicatie‑skelet

Laten we een minimale console‑app opzetten die onze OCR‑logica host. Open `Program.cs` (of maak een nieuw bestand) en plak het onderstaande skelet. Let op de `using`‑directieven bovenaan—deze brengen de Aspose OCR‑namespaces in scope.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

Op dit moment compileert het project, maar doet nog niets. De volgende secties zullen de **OCR uitvoeren op afbeelding**‑workflow uitwerken.

## Stap 3: Initialiseer de OCR‑engine (tekst uit afbeelding extraheren)

Om **tekst uit afbeelding te extraheren**, heb je eerst een `OcrEngine`‑instantie nodig. Aspose OCR downloadt taalbronnen lui de eerste keer dat ze nodig zijn, waardoor de initiële binary klein blijft.

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

Waarom hier initialiseren in plaats van in een static field? Door het binnen `Main` te doen, wordt gegarandeerd dat eventuele uitzonderingen (zoals ontbrekende native dependencies) vroeg verschijnen, waardoor debuggen makkelijker wordt.

## Stap 4: Beperk herkenning tot de gewenste taal (tekst uit JPG lezen)

Als je de taal van de te scannen tekst kent—bijvoorbeeld Russisch—kun je zowel snelheid als nauwkeurigheid verbeteren door de `Language`‑property in te stellen. Dit is vooral nuttig wanneer je **tekst uit jpg**‑bestanden leest die Cyrillische tekens bevatten.

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

Achter de schermen zal Aspose OCR het Russische taalpakket downloaden de eerste keer dat je deze regel bereikt. Volgende runs hergebruiken het gecachte pakket, dus er is geen netwerk‑penalty na de eerste download.

> **Waarom de taal vergrendelen?**  
> * **Performance:** De engine slaat het scannen over voor tekens buiten het geselecteerde alfabet.  
> * **Accuracy:** Taal‑specifieke heuristieken (zoals veelvoorkomende woordfrequenties) worden toegepast, waardoor mis‑herkenningen verminderen.  

Als je meerdere talen moet ondersteunen, kun je een door komma’s gescheiden lijst doorgeven, bijv. `OcrLanguage.English | OcrLanguage.Russian`.

## Stap 5: Voer OCR uit op de doel‑JPG (OCR uitvoeren op afbeelding)

Nu voeren we daadwerkelijk **OCR uitvoeren op afbeelding** uit. Geef het volledige pad naar je JPG‑bestand op—Aspose OCR accepteert veel formaten (`.png`, `.bmp`, `.tif`, enz.), maar we blijven voor deze demo bij `.jpg`.

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

Als het bestand niet wordt gevonden, gooit `RecognizeImage` een `FileNotFoundException`. Om de tutorial robuust te maken, wikkel je de aanroep in een try‑catch‑blok:

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

De `RecognizeImage`‑methode retourneert een `OcrResult`‑object waarvan de `Text`‑property de platte‑tekst‑extractie bevat. Je kunt ook `Boxes` benaderen voor bounding‑box‑gegevens als je later layout‑informatie nodig hebt.

## Stap 6: Verifieer de output

Wanneer je het programma uitvoert (`dotnet run`), zou je iets moeten zien als:

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

Als de output er rommelig uitziet, controleer dan of de afbeelding duidelijk is en of je de juiste taal hebt geselecteerd. Vage of laag‑contrast afbeeldingen zijn de meest voorkomende oorzaak van slechte OCR‑resultaten.

### Randgevallen & Veelgestelde vragen

| Situatie | Wat te doen |
|----------|-------------|
| **Afbeelding bevat meerdere talen** | Stel `ocrEngine.Language` in op een combinatie, bijv. `OcrLanguage.English | OcrLanguage.Russian`. |
| **Grote batch afbeeldingen** | Herbruik dezelfde `OcrEngine`‑instantie voor meerdere bestanden; deze cachet taalgegevens. |
| **Uitvoeren op een headless server** | Geen UI vereist—Aspose OCR werkt prima in Docker of Azure Functions. |
| **Hogere nauwkeurigheid nodig** | Pas `ocrEngine.Options` aan (bijv. `ocrEngine.Options.Denoise = true`). |
| **Niet‑ondersteund bestandsformaat** | Converteer de afbeelding naar een ondersteund formaat (PNG of JPG) voordat je `RecognizeImage` aanroept. |

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑en‑klaar te kopiëren programma dat alle bovenstaande stappen bevat. Sla het op als `Program.cs` en voer het uit vanaf de commandoregel.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**Verwachte console‑output** (ervan uitgaande dat de voorbeeldafbeelding de zin “Пример текста на кириллице” bevat):

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

Als je de afbeelding vervangt door een Engelse foto en `ocrEngine.Language = OcrLanguage.English;` wijzigt, zal dezelfde code **tekst uit jpg** in het Engels lezen zonder verdere aanpassingen.

## Bonus: OCR uitvoeren op meerdere bestanden

Vaak moet je **OCR uitvoeren op afbeelding**‑collecties. Hier is een snel fragment dat door een map loopt:

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

De engine hergebruikt het eerder gedownloade taalpakket, zodat de batch efficiënt draait.

## Conclusie

Je hebt nu een solide, productie‑klaar patroon voor **tekst uit afbeelding extraheren** met Aspose OCR in C#. De tutorial behandelde alles van het installeren van het NuGet‑pakket tot het afhandelen van fouten en opschalen naar meerdere bestanden. Of je nu **tekst uit jpg**‑assets leest, PDF’s scant, of een document‑automatiserings‑pipeline bouwt, dezelfde aanpak geldt—vervang gewoon het taalpakket of pas de OCR‑opties aan.

Klaar voor de volgende stap? Probeer:

* Experimenteren met andere talen (bijv. `OcrLanguage.ChineseSimplified`).  
* Lay‑out‑informatie extraheren via `recognizedResult.Boxes`.  
* De OCR‑flow integreren in een ASP.NET Core API zodat andere services on‑demand tekst‑extractie kunnen aanvragen.

Veel plezier met coderen, en moge je afbeeldingen altijd scherp genoeg zijn voor perfecte OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}