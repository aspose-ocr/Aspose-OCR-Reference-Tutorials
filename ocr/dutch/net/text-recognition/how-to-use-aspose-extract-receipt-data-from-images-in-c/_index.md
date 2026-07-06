---
category: general
date: 2026-04-04
description: Leer hoe u Aspose kunt gebruiken om bongegevens te extraheren, bonafbeelding
  te laden en bonafbeelding te OCR’en met een compleet C#‑voorbeeld. Stapsgewijze
  gids voor ontwikkelaars.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: nl
og_description: Hoe je Aspose gebruikt om bongegevens uit een gescande bonafbeelding
  te extraheren. Volledige C#-code, uitleg en tips voor OCR-bonafbeeldingsverwerking.
og_title: Hoe Aspose te gebruiken – Ontvangstgegevens uit afbeeldingen extraheren
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Hoe Aspose te gebruiken – Bongegevens uit afbeeldingen extraheren in C#
url: /nl/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe gebruik je Aspose – Ontvang bongegevens uit afbeeldingen in C#

Heb je je ooit afgevraagd **hoe je Aspose** kunt gebruiken om gestructureerde informatie uit een foto van een bon te halen? Je bent niet de enige. Of je nu een uitgaven‑tracking app bouwt of factuurinvoer automatiseert, het probleem is hetzelfde: je hebt een PNG of JPEG, en je hebt de naam van de winkel, datum en totaalbedrag nodig zonder handmatig te typen.

Hier is het punt—Aspose.OCR maakt die hele pijplijn een eitje. In deze tutorial lopen we door het laden van een bonafbeelding, het uitvoeren van OCR, en uiteindelijk het extraheren van bongegevens met een paar regels C#. Aan het einde heb je een uitvoerbaar console‑programma dat de winkel, datum en totaalbedrag direct naar de console print.

> **Quick win:** Als je alleen de code nodig hebt, ga dan naar de sectie “Complete Working Example” onderaan en kopieer‑plak.

## Wat je nodig hebt

- **.NET 6.0 of later** (de API werkt met .NET Core en .NET Framework)
- **Aspose.OCR for .NET** NuGet‑pakket (`Install-Package Aspose.OCR`)
- Een voorbeeld bonafbeelding (PNG, JPG of BMP) opgeslagen op je lokale schijf
- Visual Studio 2022 of een andere editor die C#‑projecten ondersteunt

Er zijn geen andere externe bibliotheken vereist. Het enige vereiste is een basisbegrip van C# console‑applicaties—als je “Hello World” hebt geschreven, ben je klaar om te gaan.

## Stap 1 – Installeer en verwijs naar Aspose.OCR

Om **hoe je Aspose gebruikt**, moet je eerst de bibliotheek in je project hebben. Open de Package Manager Console en voer uit:

```powershell
Install-Package Aspose.OCR
```

Of gebruik de NuGet‑UI en zoek naar “Aspose.OCR”. Zodra het geïnstalleerd is, voeg je de benodigde namespaces toe aan de bovenkant van je bestand:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** Houd je NuGet‑pakketten up‑to‑date. Vanaf vandaag (april 2026) is de nieuwste stabiele versie 23.11.0, die prestatieverbeteringen bevat voor OCR op hoge‑resolutie bonnen.

## Stap 2 – Laad de bonafbeelding

Wanneer je **bonafbeeldingen laadt**, heb je twee veelvoorkomende bronnen: een lokaal pad of een stream van een web‑request. Voor deze tutorial houden we het simpel en lezen we van de schijf:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Vervang `YOUR_DIRECTORY/receipt.png` door het daadwerkelijke pad naar je bonbestand. Als je met gebruikers‑uploads werkt, kun je een `MemoryStream` aan `ImageStream.FromStream` doorgeven.

> **Waarom dit belangrijk is:** Het specificeren van de taal (English) vertelt de OCR‑engine welke tekenset verwacht wordt, waardoor foutieve herkenningen afnemen—vooral belangrijk wanneer je **ocr receipt image** verwerkt die cijfers en symbolen bevat.

## Stap 3 – Voer OCR uit en capture lay‑outinformatie

De OCR‑stap doet meer dan alleen ruwe tekst produceren; hij legt ook de lay‑out vast, wat cruciaal is voor gestructureerde extractie later.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Na `Recognize()` voltooid is, bevat `ocrEngine` zowel de platte tekst als de positionele data van elk woord. Dit vormt de basis voor de volgende stap waarin we Aspose vragen om automatisch “**how to extract receipt**” velden te identificeren.

## Stap 4 – Initialise­er de Layout Recognizer

Aspose biedt een `LayoutRecognizer`‑klasse die weet hoe bonnen doorgaans zijn georganiseerd (winkelnaam bovenaan, datumregel, totaal onderaan). Je geeft simpelweg de geconfigureerde OCR‑engine door:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Onder de motorkap past de recognizer een reeks heuristieken toe—zoals zoeken naar valutatekens of datumpatronen—to map raw text to semantic fields.

## Stap 5 – Extraheer gestructureerde bongegevens

Nu komt het leuke deel: **extract receipt data**. Eén methode‑aanroep doet het zware werk:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` is een object van het type `ReceiptData` (gedefinieerd in `Aspose.OCR.Structured`). Het bevat drie hoofd‑eigenschappen:

- `Merchant` – de naam van de winkel
- `Date` – de aankoopdatum als een `DateTime` (indien gedetecteerd)
- `TotalAmount` – het totaalbedrag als een `decimal`

Als de engine een bepaald veld niet kan vinden, zal de eigenschap `null` of `0` zijn. Je kunt indien nodig fallback‑logica toevoegen (bijv. de gebruiker om bevestiging vragen).

## Stap 6 – Toon de geëxtraheerde informatie

Tot slot, geef de resultaten weer in de console. Hier zie je de vruchten van je arbeid:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

De opmaak‑strings (`:d` en `:C`) produceren respectievelijk een korte datum en een valutatekenreeks, waardoor de output mens‑leesbaar wordt.

### Verwachte output

Stel dat de bon behoort tot “Coffee Corner”, gedateerd 2025‑12‑01, met een totaal van $4.75, dan toont de console:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Als een veld ontbreekt, zie je een lege regel of een standaardwaarde—perfect voor debuggen.

## Edge Cases & Common Pitfalls

### 1. Low‑Resolution Images
Als de bonafbeelding wazig is of minder dan 150 dpi heeft, daalt de OCR‑nauwkeurigheid drastisch. Het opschalen van de afbeelding met een eenvoudige bilineaire filter vóór je deze aan Aspose doorgeeft, kan de resultaten verbeteren.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Non‑English Receipts
Het primaire voorbeeld gebruikt `Language.English`. Voor meertalige bonnen stel je `Language` in op de juiste enum (bijv. `Language.French`) of gebruik `Language.AutoDetect` als je het niet zeker weet.

### 3. Multiple Receipts in One Image
Aspose’s layout recognizer verwacht één bon per afbeelding. Als je een foto hebt met meerdere bonnen naast elkaar, moet je de afbeelding eerst voorbewerken—crop elke bon naar een eigen bestand voordat je OCR uitvoert.

### 4. Missing Currency Symbol
Soms verschijnt het totaalbedrag zonder een `$`‑teken. De recognizer pikt nog steeds cijfers op, maar je moet mogelijk de string naverwerken om de juiste decimale plaatsing te garanderen.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro Tips voor productie

- **Cache de OCR‑engine** als je veel bonnen in één batch verwerkt; het hergebruiken van dezelfde instantie vermindert toewijzings‑overhead.
- **Log de ruwe OCR‑tekst** (`ocrEngine.Text`) voor audit‑trails. Handig wanneer een veld niet wordt geëxtraheerd.
- **Wrap de volledige flow in een try/catch** en geef een vriendelijke foutmelding weer (bijv. “Unable to read receipt, please upload a clearer image”).

## Complete Working Example

Hieronder vind je een zelfstandige console‑applicatie die je kunt compileren en direct kunt uitvoeren. Vervang alleen het afbeeldingspad en je bent klaar om te gaan.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Running the code**

1. Maak een nieuw .NET console‑project (`dotnet new console -n ReceiptExtractor`).
2. Voeg het Aspose.OCR‑pakket toe (`dotnet add package Aspose.OCR`).
3. Vervang de gegenereerde `Program.cs` door de bovenstaande snippet.
4. Plaats een bonafbeelding op het pad dat je hebt opgegeven.
5. Build en run (`dotnet run`).

Je zou de winkel, datum en totaal exact moeten zien zoals eerder getoond.

## Wrapping Up

In deze gids hebben we behandeld **how to use Aspose** om **load receipt image**, **ocr receipt image** uit te voeren, en uiteindelijk **extract receipt data** met slechts een handvol regels. De belangrijkste conclusie is dat Aspose.OCR het zware werk doet—zodra de OCR‑engine geconfigureerd is, zet de `LayoutRecognizer` ruwe tekst om in een gestructureerd object waarop je kunt vertrouwen.

Wat nu? Probeer de geëxtraheerde waarden in een database te plaatsen, een PDF‑bonsamenvatting te genereren, of ze zelfs te voeden aan een machine‑learning model voor uitgavenclassificatie. Je kunt ook experimenteren met andere gestructureerde documenttypen zoals facturen of verzendetiketten—Aspose’s `ExtractInvoiceData` werkt op zeer vergelijkbare wijze.

Heb je vragen over edge cases of wil je zien hoe je multi‑page PDF’s kunt verwerken? Laat een reactie achter of bekijk de officiële Aspose.OCR‑documentatie voor geavanceerde scenario’s. Happy coding, en geniet van de eenvoud van **how to use Aspose** voor bonautomatisering!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}