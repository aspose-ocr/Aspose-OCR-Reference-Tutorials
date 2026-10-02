---
category: general
date: 2026-01-10
description: Lär dig hur du känner igen text från en bild, extraherar textkoordinater
  och konverterar kvitto till JSON med Aspose OCR i C#. Steg‑för‑steg‑handledning.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: sv
og_description: Känn igen text från bild i C# med Aspose OCR. Den här guiden visar
  hur du extraherar text, får koordinater och konverterar kvitto till JSON.
og_title: igenkänna text från bild – Fullständig C# OCR-handledning
tags:
- OCR
- C#
- Aspose
title: igenkänna text från bild i C# – Komplett guide till OCR och JSON
url: /sv/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# känna igen text från bild – Fullständig C# OCR‑handledning

Har du någonsin behövt känna igen text från en bild men varit osäker på vilket bibliotek du ska välja? Du är inte ensam. I många verkliga appar – utgiftsspårare, kvittoskannrar eller dokumentarkiv – är pålitlig textutvinning det första hindret.  

I den här handledningen går vi igenom **hur man extraherar text**, hämtar dess avgränsningsrutor och slutligen **konverterar kvitto till JSON** med Aspose.OCR för .NET. När du är klar har du ett självständigt C#‑projekt som tar ett foto av ett kvitto och levererar en prydlig JSON‑fil med förtroendescore och koordinater.

## Vad du behöver

Innan vi sätter igång, se till att du har följande på din maskin:

- **.NET 6.0 SDK** (eller någon senare version). Äldre ramverk fungerar också, men .NET 6 är den optimala versionen för moderna bibliotek.
- **Visual Studio 2022** eller VS Code med C#‑tillägget.
- **Aspose.OCR for .NET** NuGet‑paket (`Aspose.OCR` och `Aspose.OCR.Output`). Du kan installera det via Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- En exempel‑kvittobild (t.ex. `receipt.jpg`) placerad i en mapp som du senare refererar till.

Det är allt – inga extra SDK:er, inga inhemska binärer, bara ren hanterad kod.

## Steg 1: Skapa ett nytt konsolprojekt

Först och främst, skapa en konsolapp. Det är det snabbaste sättet att testa OCR utan UI‑överbyggnad.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Proffstips:** Håll projektmappen prydlig; skapa en undermapp som heter `Resources` och lägg `receipt.jpg` där. Det gör sökvägshanteringen enkel.

## Steg 2: Ladda kvittobilden

Nu **känner vi igen text från bild**. Det första steget är att peka OCR‑motorn på filen.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Varför omsluter vi laddningen med en enkel existenskontroll? För i produktion hanterar du ofta användaruppladdningar som kan saknas eller vara korrupta. Att fånga problemet tidigt sparar dig från kryptiska undantag senare.

## Steg 3: Utför OCR – **recognize text from image**

Med bilden i minnet ber vi Aspose **recognize text from image**. Denna operation är synkron och returnerar ett rikt resultatset.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Bakom kulisserna kör Aspose ett neuralt nätverk tränat på miljontals tecken. Motorn fyller `ocrEngine.Text`, `ocrEngine.RecognitionResult` och en samling `OcrRegion`‑objekt som innehåller koordinater. Det är exakt vad vi behöver för nästa steg.

## Steg 4: **How to extract text** – Hämta den råa strängen

Om du bara är intresserad av ren text (kanske för en snabb sökning) kan du hämta den direkt från motorn:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Du kommer att märka radbrytningar där OCR identifierade styckegränser. I många kvittoskannings‑scenarier räcker den råa strängen för att plocka ut totalbelopp, datum eller leverantörsnamn med enkla regex‑uttryck.

## Steg 5: **extract text coordinates** – Avgränsningsrutor för varje ord

Ofta behöver du veta *var* på bilden en viss text finns – till exempel för att markera totalbeloppet i ett UI. Aspose ger oss detta via `OcrRegion`‑objekt.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Observera att vi loopar över **extract text coordinates** för varje igenkänd segment. Koordinaterna är relativa till originalbilden, så du kan överlagra dem i en grafik‑canvas eller ett HTML‑`<canvas>`‑element.

## Steg 6: **convert receipt to JSON** – Spara detaljerade resultat

Nu kommer delen som binder ihop allt: vi vill ha en maskinläsbar struktur som inkluderar text, förtroendescore och avgränsningsrutor. Aspose levereras med `JsonSaveOptions` som gör detta enkelt.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Den resulterande filen ser ungefär ut så här (trimmad för korthet):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Du har nu ett **convert receipt to JSON**‑artefakt som kan matas in i downstream‑tjänster – tänk utgift‑rapport‑API:er, analys‑pipelines eller till och med ett enkelt UI som ritar rektanglar runt varje ord.

## Fullt fungerande exempel

När alla bitar sätts ihop, här är hela `Program.cs` som du kan kopiera och klistra in i ditt projekt:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Kör programmet (`dotnet run`) och observera konsolutdata. Öppna `Resources/receipt.json` för att verifiera strukturen.

## Vanliga frågor & kantfall

- **Vad händer om bilden är suddig?**  
  Aspose OCR fungerar bäst med 300 dpi eller högre. Om du får låga förtroendescore, överväg att applicera ett skärpande filter innan du skickar bilden till motorn.

- **Kan jag känna igen flera språk?**  
  Ja. Sätt `ocrEngine.Language = Language.English | Language.Spanish;` innan du anropar `Recognize()`.

- **Hur begränsar jag utdata till endast siffror (t.ex. totalbelopp)?**  
  När du har den rena texten, kör en regex som `\d+\.\d{2}` på `ocrEngine.Text`. Eftersom vi redan har koordinater kan du mappa den matchade strängen tillbaka till dess region för visuell markering.

- **Är JSON‑formatet anpassningsbart?**  
  Klassen `JsonSaveOptions` exponerar ett antal flaggor. Om du behöver ett helt eget schema kan du iterera över `ocrEngine.RecognitionResult.Regions` och själv serialisera objekten med `System.Text.Json`.

## Slutsats

Vi har just demonstrerat hur man **recognize text from image** i C# med Aspose.OCR, **how to extract text**, hämtar **extract text coordinates**, och slutligen **convert receipt to JSON**. Hela flödet levereras i en enda, lättkörbar konsolapp, vilket gör den perfekt för prototyper eller som byggsten i större system.

Nästa steg? Prova att mata in JSON‑filen i ett front‑end som ritar avgränsningsrutorna, eller koppla utdata till en utgift‑rapport‑tjänst. Du kan också experimentera med olika bildformat (PNG, TIFF) eller batch‑processa en mapp med kvitton.

Har du fler frågor om OCR, Aspose eller JSON‑hantering? Lämna en kommentar nedan, och lycka till med kodandet! 

![Receipt image example for recognize text from image](receipt.jpg "Receipt image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}