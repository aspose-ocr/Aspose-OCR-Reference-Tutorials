---
category: general
date: 2026-04-04
description: Lär dig hur du använder Aspose för att extrahera kvittodata, ladda kvittabilden
  och OCR:a kvittabilden med ett komplett C#‑exempel. Steg‑för‑steg‑guide för utvecklare.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: sv
og_description: Hur man använder Aspose för att extrahera kvittoinformation från en
  skannad kvittobild. Fullständig C#‑kod, förklaringar och tips för OCR‑bearbetning
  av kvittobilder.
og_title: Så här använder du Aspose – Extrahera kvittodata från bilder
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Så använder du Aspose – Extrahera kvittodata från bilder i C#
url: /sv/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du Aspose – Extrahera kvittodata från bilder i C#

Har du någonsin undrat **how to use Aspose** för att hämta strukturerad information från ett foto av ett kvitto? Du är inte ensam. Oavsett om du bygger en utgiftsspårningsapp eller automatiserar fakturainmatning, är smärtan densamma: du har en PNG eller JPEG, och du behöver butiksnamnet, datumet och totalbeloppet utan manuell inmatning.

Här är grejen—Aspose.OCR gör hela pipelineprocessen till en barnlek. I den här handledningen går vi igenom hur man laddar en kvittobild, kör OCR och slutligen extraherar kvittodata med några få rader C#. I slutet har du ett körbart konsolprogram som skriver ut butiksnamn, datum och totalbelopp direkt i konsolen.

> **Quick win:** Om du bara behöver koden, hoppa till avsnittet “Complete Working Example” längst ner och kopiera‑klistra.

## Vad du behöver

- **.NET 6.0 eller senare** (API:et fungerar med .NET Core och .NET Framework)
- **Aspose.OCR for .NET** NuGet‑paket (`Install-Package Aspose.OCR`)
- En exempelkvittobild (PNG, JPG eller BMP) sparad lokalt
- Visual Studio 2022 eller någon editor som stödjer C#‑projekt

Inga andra tredjepartsbibliotek krävs. Det enda förutsättningen är en grundläggande förståelse för C#‑konsolapplikationer—om du har skrivit “Hello World”, är du redo att köra.

## Steg 1 – Installera och referera Aspose.OCR

För att **how to use Aspose**, behöver du först biblioteket i ditt projekt. Öppna Package Manager Console och kör:

```powershell
Install-Package Aspose.OCR
```

Alternativt, använd NuGet‑gränssnittet och sök efter “Aspose.OCR”. När det är installerat, lägg till de nödvändiga namnrymderna högst upp i din fil:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** Håll dina NuGet‑paket uppdaterade. Från och med idag (april 2026) är den senaste stabila versionen 23.11.0, som inkluderar prestandaförbättringar för OCR på högupplösta kvitton.

## Steg 2 – Ladda kvittobilden

När du **load receipt image**‑filer har du två vanliga källor: en lokal sökväg eller en ström från en webbförfrågan. För den här handledningen håller vi det enkelt och läser från disk:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Byt ut `YOUR_DIRECTORY/receipt.png` mot den faktiska sökvägen till din kvittofil. Om du hanterar användaruppladdningar kan du mata in en `MemoryStream` till `ImageStream.FromStream`.

> **Why this matters:** Att specificera språket (English) talar om för OCR‑motorn vilken teckenuppsättning som förväntas, vilket minskar falska igenkänningar—särskilt viktigt när du **ocr receipt image** som innehåller siffror och symboler.

## Steg 3 – Kör OCR och fånga layoutinformation

OCR‑steget gör mer än att bara sputta ut råtext; det fångar också layouten, vilket är avgörande för strukturerad extraktion senare.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

När `Recognize()` är klar innehåller `ocrEngine` både vanlig text och positionsdata för varje ord. Detta är grunden för nästa steg där vi ber Aspose att automatiskt “**how to extract receipt**” fält.

## Steg 4 – Initiera LayoutRecognizer

Aspose tillhandahåller en `LayoutRecognizer`‑klass som vet hur kvitton vanligtvis är organiserade (butik högst upp, datumrad, total längst ner). Du skickar helt enkelt den konfigurerade OCR‑motorn:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Bakom kulisserna tillämpar recognizern en uppsättning heuristiker—som att leta efter valutasymboler eller datummönster—för att mappa råtext till semantiska fält.

## Steg 5 – Extrahera strukturerade kvittodata

Nu kommer den bästa delen: **extract receipt data**. Ett metodanrop gör det tunga lyftet:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` är ett objekt av typen `ReceiptData` (definierad i `Aspose.OCR.Structured`). Det innehåller tre huvudegenskaper:

- `Merchant` – butikens namn
- `Date` – inköpsdatum som en `DateTime` (om det upptäcktes)
- `TotalAmount` – totalbeloppet som en `decimal`

Om motorn inte kan hitta ett specifikt fält kommer egenskapen att vara `null` eller `0`. Du kan lägga till reservlogik om det behövs (t.ex. be användaren bekräfta).

## Steg 6 – Visa den extraherade informationen

Till sist, skriv ut resultaten till konsolen. Här ser du frukterna av ditt arbete:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Formatsträngarna (`:d` och `:C`) producerar ett kort datum respektive en valutastring, vilket gör utskriften mänskligt läsbar.

### Förväntad utskrift

Om vi antar att kvittot tillhör “Coffee Corner”, daterat 2025‑12‑01, med en total på $4.75, kommer konsolen att visa:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Om något fält saknas kommer du att se en tom rad eller ett standardvärde—perfekt för felsökning.

## Edge Cases & Vanliga fallgropar

### 1. Lågre­s­lösningsbilder

Om kvittobilden är suddig eller under 150 dpi, sjunker OCR‑noggrannheten dramatiskt. Att skala upp bilden med ett enkelt bilinjärt filter innan du matar den till Aspose kan förbättra resultatet.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Icke‑engelska kvitton

Det primära exemplet använder `Language.English`. För flerspråkiga kvitton, sätt `Language` till rätt enum (t.ex. `Language.French`) eller använd `Language.AutoDetect` om du är osäker.

### 3. Flera kvitton i en bild

Asposes layoutrecognizer förväntar sig ett enda kvitto per bild. Om du har ett foto av flera kvitton sida‑vid‑sida, måste du förbehandla bilden—beskära varje kvitto till en egen fil innan du kör OCR.

### 4. Saknad valutasymbol

Ibland visas totalbeloppet utan ett `$`‑tecken. Recognizern plockar fortfarande upp siffrorna, men du kan behöva efterbehandla strängen för att säkerställa korrekt decimalplacering.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro Tips för produktion

- **Cache the OCR engine** om du bearbetar många kvitton i en batch; återanvändning av samma instans minskar allokeringskostnaden.
- **Log the raw OCR text** (`ocrEngine.Text`) för revisionsspår. Det är användbart när ett fält misslyckas med att extraheras.
- **Wrap the entire flow in a try/catch** och visa ett vänligt felmeddelande (t.ex. “Unable to read receipt, please upload a clearer image”).

## Komplett fungerande exempel

Nedan är en fristående konsolapplikation som du kan kompilera och köra som den är. Byt bara ut bildsökvägen så är du redo att köra.

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

**Köra koden**

1. Skapa ett nytt .NET‑konsolprojekt (`dotnet new console -n ReceiptExtractor`).
2. Lägg till Aspose.OCR‑paketet (`dotnet add package Aspose.OCR`).
3. Ersätt den genererade `Program.cs` med kodsnutten ovan.
4. Placera en kvittobild på den sökväg du angav.
5. Bygg och kör (`dotnet run`).

Du bör se butiksnamn, datum och total utskrivna exakt som visat tidigare.

## Avslutning

I den här guiden gick vi igenom **how to use Aspose** för att **load receipt image**, köra **ocr receipt image**, och slutligen **extract receipt data** med bara ett fåtal rader. Den viktigaste insikten är att Aspose.OCR gör det tunga lyftet—när OCR‑motorn är konfigurerad omvandlar `LayoutRecognizer` råtext till ett strukturerat objekt du kan lita på.

Nästa steg? Försök att mata in de extraherade värdena i en databas, generera en PDF‑sammanfattning av kvittot, eller till och med mata dem i en maskininlärningsmodell för kostnadsklassificering. Du kan också experimentera med andra strukturerade dokumenttyper som fakturor eller fraktetiketter—Asposes `ExtractInvoiceData` fungerar på ett mycket liknande sätt.

Har du frågor om specialfall eller vill se hur man hanterar flersidiga PDF‑filer? Lämna en kommentar eller kolla den officiella Aspose.OCR‑dokumentationen för avancerade scenarier. Lycka till med kodandet, och njut av enkelheten med **how to use Aspose** för kvittoautomatisering!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}