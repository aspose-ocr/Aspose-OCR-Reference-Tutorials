---
category: general
date: 2026-03-29
description: Hoe OCR uit te voeren in C# en tekst uit PNG‑bestanden te lezen. Leer
  hoe je Russische tekst kunt extraheren, tekst uit PNG kunt lezen en hoe je tekst
  kunt extraheren met Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: nl
og_description: Hoe OCR uit te voeren in C# met Aspose OCR. Deze gids laat zien hoe
  je tekst uit een PNG leest, Russische tekst extraheert en een volledige C# OCR‑oplossing
  implementeert.
og_title: Hoe OCR in C# uit te voeren – Volledige PNG-tekstextractie
tags:
- OCR
- C#
- Aspose
title: Hoe OCR uit te voeren op PNG-afbeeldingen in C# – Stapsgewijze handleiding
url: /nl/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op PNG-afbeeldingen in C# – Complete Tutorial

Heb je ooit **OCR moeten uitvoeren** op een screenshot of gescand document, maar wist je niet waar je in C# moest beginnen? Je bent niet de enige. Ontwikkelaars vragen constant: “Hoe lees ik tekst uit PNG‑bestanden zonder ze naar een externe service te sturen?” Het goede nieuws is dat je met Aspose.OCR **Russische tekst kunt extraheren**, **tekst uit png kunt lezen**, en een schone string terugkrijgt in slechts een paar regels code.

In deze tutorial lopen we alles door wat je nodig hebt: de bibliotheek instellen, het juiste taalmodel kiezen, de herkenning uitvoeren en veelvoorkomende valkuilen afhandelen. Aan het einde kun je **tekst extraheren** uit elke PNG‑afbeelding, of het nu Engels, Russisch of een van de 70+ talen is die Aspose ondersteunt. Geen poespas, alleen een praktisch, uitvoerbaar voorbeeld dat je direct in een console‑app kunt plaatsen.

---

## Wat je zult leren

- Installeer en verwijs naar het Aspose.OCR NuGet‑pakket.
- Initialiseer de OCR‑engine in de standaard auto‑downloadmodus.
- Configureer de engine om **Russische tekst te extraheren** met behulp van het Cyrillisch taalmodel.
- Voer OCR uit op een lokaal PNG‑bestand en toon het resultaat.
- Tips voor het oplossen van ontbrekende taalbestanden en het verbeteren van de nauwkeurigheid.

**Voorwaarden**: .NET 6+ (of .NET Framework 4.7.2+), Visual Studio 2022 of VS Code, en een internetverbinding voor de eerste uitvoering (het taalmodel wordt automatisch gedownload).

---

## Stap 1 – Installeer Aspose.OCR‑pakket

Om te beginnen, voeg je de Aspose.OCR‑bibliotheek toe aan je project. Open een terminal in de projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Of, als je de Visual Studio‑UI verkiest, klik met de rechtermuisknop op **Dependencies → Manage NuGet Packages**, zoek naar **Aspose.OCR**, en klik op **Install**.

> **Pro tip**: Het pakket is slechts een paar megabytes, en de taalmodellen worden op aanvraag opgehaald, zodat je je app niet opzadelt met onnodige bestanden.

---

## Stap 2 – Initialiseer de OCR‑engine (Primaire trefwoord in actie)

Het aanmaken van de engine is eenvoudig. De constructor schakelt automatisch *auto‑downloadmodus* in, wat betekent dat de eerste keer dat je een taal vraagt die niet lokaal aanwezig is, Aspose deze voor je downloadt.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Waarom dit belangrijk is**: Door de standaard auto‑downloadmodus te gebruiken, vermijd je handmatige bestandsafhandeling. Als je later **tekst uit png moet lezen** in een andere taal, wijzig je gewoon `Language.RussianCyrillic` naar de juiste enum‑waarde.

---

## Stap 3 – Bereid je PNG‑afbeelding voor

Zorg ervoor dat de afbeelding die je wilt verwerken toegankelijk is tijdens runtime. Plaats `sample_russian.png` in dezelfde map als de gecompileerde `.exe`, of gebruik een absoluut pad als je dat liever hebt. De afbeelding moet een duidelijke scan of screenshot zijn; de OCR‑nauwkeurigheid daalt sterk bij onscherpe of sterk gecomprimeerde PNG‑bestanden.

**Veelvoorkomende randgeval**: Als de PNG meerdere talen bevat, kun je `ocrEngine.Language = Language.Multilingual;` instellen zodat de engine elk blok automatisch detecteert.

---

## Stap 4 – Voer de applicatie uit en controleer de output

Compileer en voer het programma uit:

```bash
dotnet run
```

Je zou de geëxtraheerde Russische tekst in de console moeten zien verschijnen, bijvoorbeeld:

```
Привет, мир! Это пример текста на русском языке.
```

Als je een lege string krijgt, controleer dan het volgende:

1. Het bestandspad is correct.
2. De afbeelding is niet volledig wit of volledig zwart.
3. Het taalmodel is succesvol gedownload (zoek naar een `Aspose.OCR`‑map onder je gebruikersprofiel).

---

## Stap 5 – Geavanceerde aanpassingen voor betere nauwkeurigheid

Hoewel de standaardinstellingen voor de meeste gevallen werken, wil je de engine misschien fijn afstemmen:

| Instelling | Wat het doet | Wanneer te gebruiken |
|------------|--------------|----------------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | Corrigeert lichte rotatie | Gescande documenten die niet perfect uitgelijnd zijn |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | Verwijdert achtergrondruis | Lage‑kwaliteit PNG's van mobiele camera's |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | Beperkt tekens tot cijfers | Cijfers extraheren uit facturen |

Voeg een van deze toe vóór het aanroepen van `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## Stap 6 – Resultaten exporteren naar een bestand (optioneel)

Als je **tekst wilt extraheren** naar een bestand voor latere verwerking, schrijf dan simpelweg het resultaat naar schijf:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

Nu heb je een permanente kopie die kan worden ingevoerd in een database, zoekindex of vertaalengine.

---

## Veelgestelde vragen

**Q: Werkt dit met andere afbeeldingsformaten zoals JPEG of BMP?**  
A: Absoluut. `RecognizeImage` accepteert elk formaat dat wordt ondersteund door de `System.Drawing`‑bibliotheek van .NET, inclusief JPEG, BMP en TIFF.

**Q: Wat als ik in dezelfde run Engelse tekst moet extraheren?**  
A: Maak een tweede `OcrEngine`‑instantie met `Language.English` of wissel de taal‑eigenschap tussen oproepen.

**Q: Kan ik OCR uitvoeren in een web‑API zonder de hoofdthread te blokkeren?**  
A: Ja. Omhul de herkenningsaanroep met `Task.Run` of gebruik de async‑overload `RecognizeImageAsync` (beschikbaar in nieuwere Aspose‑versies).

**Q: Is er een limiet aan de grootte van de PNG?**  
A: De bibliotheek kan grote afbeeldingen aan, maar het geheugenverbruik groeit met de resolutie. Als je een `OutOfMemoryException` krijgt, overweeg dan de afbeelding eerst te verkleinen.

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma dat je kunt plakken in een nieuw console‑project (`dotnet new console`) en direct kunt uitvoeren na het installeren van het NuGet‑pakket.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**Verwachte console‑output** (ervan uitgaande dat het voorbeeld de zin “Привет, мир!” bevat):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## Conclusie

We hebben **hoe OCR uit te voeren** op PNG‑afbeeldingen met C# behandeld, van het installeren van Aspose.OCR tot het aanpassen van preprocess‑opties en het exporteren van de resultaten. Je weet nu hoe je **tekst uit png kunt lezen**, **tekst kunt extraheren** in verschillende talen, en specifiek **Russische tekst kunt extraheren** met minimale code.

Klaar voor de volgende uitdaging? Probeer de OCR‑output te voeden aan een taal‑detectiebibliotheek, of combineer het met Azure Cognitive Services voor vertaling. De mogelijkheden zijn eindeloos wanneer je een betrouwbare OCR‑engine combineert met het krachtige C#‑ecosysteem.

Als je deze **c# ocr tutorial** nuttig vond, geef hem een ster, deel hem met teamgenoten, of laat een reactie achter met je eigen tips. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}