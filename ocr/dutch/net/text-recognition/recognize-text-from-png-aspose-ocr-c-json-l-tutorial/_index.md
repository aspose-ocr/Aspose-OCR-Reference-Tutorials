---
category: general
date: 2026-03-26
description: herken tekst uit png en extraheer bongegevens met Aspose OCR in C#. converteer
  afbeelding naar JSON‑L en verwerk de bon met OCR in een volledig voorbeeld.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: nl
og_description: herken tekst van png en zet bonnen om in JSON‑L met Aspose OCR in
  C#. volledige stap‑voor‑stap code en tips.
og_title: Tekst herkennen van PNG – Aspose OCR C# gids
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: herken tekst van png – Aspose OCR C# JSON‑L handleiding
url: /nl/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit png – Volledige Aspose OCR C# Gids

Heb je ooit **tekst herkennen uit png** bestanden nodig gehad, maar wist je niet welke bibliotheek je schone, regel‑voor‑regel resultaten geeft? Je bent niet de enige. In veel kleine‑ondernemingsapps staat het bonnetje als een PNG‑afbeelding, en het extraheren van het bedrag, de datum of de verkopernaam is een dagelijks pijnpunt.  

Het goede nieuws? Met een paar regels C# en de **Aspose OCR**‑bibliotheek kun je **tekst uit bonnetje extraheren**, vervolgens **afbeelding naar jsonl converteren** voor downstream‑analyse. In deze tutorial lopen we de volledige pipeline door – een PNG laden, OCR uitvoeren en elke regel naar een JSON‑L‑bestand schrijven – zodat je **bonnetje met OCR verwerken** direct kunt doen.

We behandelen alles wat je nodig hebt: vereiste NuGet‑pakketten, een compleet uitvoerbaar programma, uitleg waarom elke stap belangrijk is, en een reeks praktische tips die je zult waarderen wanneer de bonnetjes rommelig worden. Geen externe documentatie nodig; gewoon kopiëren‑plakken, uitvoeren en aanpassen.

---

## Wat je zult leren

- Hoe je **tekst herkennen uit png** kunt doen met `Aspose.OCR`.
- Hoe je **tekst uit bonnetje extraheren** uit regelobjecten en vertrouwensscores vastlegt.
- Hoe je **afbeelding naar jsonl converteert** zodat elke OCR‑regel een afzonderlijk JSON‑object wordt.
- Hoe je **bonnetje met OCR verwerken** end‑to‑end, met aandacht voor randgevallen zoals lege afbeeldingen of regels met lage vertrouwensscore.
- Tips voor het oplossen van veelvoorkomende OCR‑problemen en het verbeteren van de nauwkeurigheid.

### Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework).
- Visual Studio 2022 of een IDE naar keuze.
- Een geldige Aspose OCR‑licentie (je kunt starten met een gratis tijdelijke licentie van Aspose.com).
- Een voorbeeldbonnetje opgeslagen als `receipt.png` in een map die je beheert.

---

## Stap 1: Tekst herkennen uit png met Aspose OCR

Het eerste wat we nodig hebben is een geïnitialiseerde `OcrEngine`. Dit object bevat de OCR‑engine‑instellingen (taal, detectiemodus, enz.). Standaard gebruikt het Engels en detecteert het automatisch de paginalay‑out, wat voor de meeste bonnetjes prima werkt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Waarom dit belangrijk is:**  
`OcrEngine` is het zware werkende component; het één keer aanmaken en hergebruiken voor veel afbeeldingen vermindert geheugen‑churn. Als je een andere taal nodig hebt (bijv. Spaanse bonnetjes), kun je `ocrEngine.Language = OcrLanguage.Spanish;` instellen vóór het aanroepen van `Recognize`.

---

## Stap 2: Tekst uit bonnetje‑regels extraheren

`OcrResult` bevat een collectie genaamd `Lines`. Elke regel bevat de ruwe tekst en een vertrouwensscore (0‑100). Deze eruit halen geeft je granulaire controle – je kunt regels met lage vertrouwensscore negeren of markeren voor handmatige controle.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Waarom we JSON escapen:**  
Bonnetjestekst kan aanhalingstekens (`"`) of backslashes (`\`) bevatten die een naïeve JSON‑string zouden breken. De `EscapeJson`‑methode garandeert een geldige JSON‑regel.

**Hoe de output eruitziet:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Elke regel is een afzonderlijk record, perfect voor streaming naar een data‑lake of het voeden van een machine‑learning‑model.

---

## Stap 3: Afbeelding naar JSONL converteren – randgevallen afhandelen

Wanneer je een batch bonnetjes verwerkt, kunnen enkele afbeeldingen leeg, corrupt of met extreem lage vertrouwensscores zijn. Laten we de pipeline wat robuuster maken.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Waarom filteren:**  
Bonnetjes gedrukt op vervaagd papier kunnen vreemde tekens met lage vertrouwensscore opleveren. Alles onder 80 % verwijderen verwijdert meestal ruis terwijl de bruikbare data behouden blijft.

---

## Stap 4: Bonnetje met OCR verwerken – end‑to‑end voorbeeld

Alles samenvoegend, hier is het **complete, kant‑klaar** programma. Vervang `YOUR_DIRECTORY` door de map die je PNG‑bestand bevat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**De code uitvoeren:**  
1. Open een terminal in de projectmap.  
2. `dotnet add package Aspose.OCR` – installeert de bibliotheek.  
3. `dotnet run` – je zou een succesbericht moeten zien en een `receipt.jsonl`‑bestand verschijnen.

**Verwacht resultaat:** Een regel‑gescheiden JSON‑bestand waarbij elke regel een bonnetje‑regel weerspiegelt, compleet met vertrouwensscores. Je kunt dit bestand nu doorsturen naar Power BI, Elastic, of elk analytics‑tool dat JSON‑L begrijpt.

---

## Veelvoorkomende valkuilen & Pro‑tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Lege output** | Pad naar afbeelding onjuist of bestand is geen PNG. | Controleer het pad, gebruik `File.Exists(imagePath)`. |
| **Vreemde tekens** | Lage DPI of sterk gecomprimeerde PNG. | Gebruik scans van minimaal 300 dpi; vermijd agressieve JPEG‑compressie. |
| **Te veel regels met lage vertrouwensscore** | Bonnetje gedrukt op thermisch papier met vervaging. | Verhoog de `minConfidence`‑drempel of pre‑process de afbeelding (contrast/drempel). |
| **JSON‑parsing fouten** | Niet‑geëscapeerde aanhalingstekens in de bontekst. | Houd de `EscapeJson`‑helper of schakel over naar `System.Text.Json` voor robuuste serialisatie. |

**Pro tip:** Als je specifieke velden moet extraheren (bijv. totaalbedrag), voer dan een eenvoudige regex uit op elke `line.Text` nadat je het JSON‑L‑bestand hebt. Dit houdt OCR gescheiden van de bedrijfslogica en maakt debugging makkelijker.

---

## De oplossing uitbreiden

- **Batchverwerking:** Plaats de `Main`‑logica in een `foreach` over alle PNG‑bestanden in een map.
- **Meertalige ondersteuning:** Stel `ocrEngine.Language = OcrLanguage.Spanish;` (of een andere ondersteunde taal) in vóór `Recognize`.
- **Gestructureerde output:** In plaats van regel‑voor‑regel JSON, bouw een `Receipt`‑object met `Date`, `Merchant`, `Total`‑eigenschappen en serialiseer één keer.

Al deze variaties **converteren nog steeds afbeelding naar jsonl** in de kern, zodat je de downstream‑consumer kunt wisselen zonder de OCR‑kant aan te raken.

---

## Conclusie

We hebben zojuist laten zien hoe je **tekst herkennen uit png** bestanden kunt doen met Aspose OCR, **tekst uit bonnetje extraheren**, en **afbeelding naar jsonl converteren** voor eenvoudige downstream‑verwerking. Het volledige, zelfstandige C#‑programma demonstreert de volledige workflow – van het laden van een PNG, het afhandelen van randgevallen, tot het schrijven van een schoon JSON‑L‑bestand – zodat je direct **bonnetje met OCR verwerken** in je eigen projecten kunt.

Probeer het met een paar voorbeeldbonnetjes, pas de vertrouwensdrempel aan, en je zult zien hoe snel een rommelige stapel afbeeldingen verandert in gestructureerde data klaar voor analyse. Zodra je er vertrouwd mee bent, kun je batchverwerking verkennen of een klein ML‑model toevoegen om uitgaven‑categorieën automatisch te classificeren.

Heb je vragen, of heb je een slimme aanpassing ontdekt? Laat een reactie achter – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}