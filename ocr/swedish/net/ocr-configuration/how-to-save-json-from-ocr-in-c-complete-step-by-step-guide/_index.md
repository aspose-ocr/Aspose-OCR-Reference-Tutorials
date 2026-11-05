---
category: general
date: 2026-03-02
description: Lär dig hur du sparar JSON när du extraherar text från en bild med Aspose
  OCR. Inkluderar kod för att skriva JSON‑fil, tips för att ladda bitmap‑bild och
  ett komplett C#‑exempel.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: sv
og_description: Upptäck hur du sparar JSON när du extraherar text från en bild med
  Aspose OCR. Komplett C#‑kod, steg för att skriva JSON‑fil och praktiska tips.
og_title: Hur man sparar JSON från OCR i C# – Fullständig programmeringshandledning
tags:
- C#
- OCR
- Aspose
- JSON
title: Hur man sparar JSON från OCR i C# – Komplett steg‑för‑steg‑guide
url: /sv/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar JSON från OCR i C# – Komplett steg‑för‑steg‑guide

Har du någonsin funderat **hur man sparar JSON** som innehåller texten du just extraherade från en bild? Du är inte ensam. Många utvecklare stöter på problem när de behöver *extrahera text från bild*-data och sedan lagra den informationen som en snyggt formaterad JSON‑fil. Den goda nyheten? Lösningen är ganska enkel när du har rätt komponenter på plats.

I den här handledningen går vi igenom ett verkligt scenario: att använda Aspose.OCR för att **extrahera text från en bild**, sedan **skriva JSON‑fil** och slutligen **hur man sparar JSON** på disk. På vägen visar vi också hur du **laddar bitmap‑bild**‑objekt korrekt, och täcker några kantfall du kan stöta på. I slutet har du en självständig C#‑konsolapp som gör allt från att ladda bilden till att producera ett färdigt JSON‑dokument.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework)
- Aspose.OCR för .NET (du kan hämta ett gratis prov‑NuGet‑paket)
- Ett exempel‑PNG‑ eller JPG‑foto som innehåller engelsk text
- Visual Studio, VS Code eller någon C#‑kompatibel IDE

Inga ytterligare bibliotek krävs—endast standard‑namnrymden `System.Drawing` för bitmap‑hantering och `System.Text.Json` för serialisering.

---

## Steg 1 – Ladda bitmap‑bilden (delen “load bitmap image”)

Innan någon OCR kan ske måste du få bilden i minnet som en `Bitmap`. Tänk på det som att öppna en bok innan du börjar läsa dess sidor.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Pro tip:** Om bilden är stor, överväg att ändra storlek först för att förbättra prestandan. OCR‑motorn arbetar snabbare på bilder under 2 MB.

---

## Steg 2 – Konfigurera Aspose OCR‑motorn

Nu när bitmap‑en är klar behöver vi en `OcrEngine`. Detta objekt vet hur man **extraherar text från bild** och kan även ge oss geometridata som avgränsningsrutor.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Varför aktivera `ExportBoundingBoxes`? Om du någonsin behöver markera ord i ett UI är de koordinaterna guld värda. Om du inte behöver dem kan du sätta flaggan till `false` och JSON‑en blir lite smalare.

---

## Steg 3 – Utför OCR och få ett strukturerat resultat

Med motorn konfigurerad är nästa steg själva **hur man extraherar text**‑operationen. Metoden `RecognizeToOcrResult` returnerar ett rikt objekt som innehåller den igenkända texten, förtroendesiffror och valfri layout‑data.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Variabeln `ocrResult` innehåller nu allt du behöver. Om du inspekterar den i debuggern ser du en hierarki av `Page`, `Paragraph`, `Line` och `Word`‑objekt, var och en med sin egen `Text`‑egenskap.

---

## Steg 4 – Serialisera resultatet till en formaterad JSON‑sträng

Här börjar den riktiga **hur man sparar json**‑magin. Vi använder `System.Text.Json` eftersom den är inbyggd, snabb och stödjer snygg utskrift direkt ur lådan.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Om du behöver ett annat namngivningskonvention (t.ex. camelCase) lägger du bara till `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` i alternativen.

---

## Steg 5 – Skriv JSON‑filen till disk (steg “write json file”)

Till sist **skriver vi JSON‑fil** till filsystemet. Detta är det konkreta svaret på **hur man sparar json** i en C#‑miljö.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

När den här raden har körts hittar du en snyggt indenterad `sample-page.json` bredvid din ursprungliga bild. Öppna den med vilken textredigerare som helst eller skicka den till en annan tjänst—dina OCR‑data är nu portabla.

---

## Steg 6 – Verifiera utdata (Vad bör du se?)

Att köra programmet bör skriva en kort bekräftelse till konsolen:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Öppna den genererade JSON‑filen så ser du något i stil med:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Om flaggan `ExportBoundingBoxes` var sann kommer varje ord också innehålla `Rectangle`‑koordinater. Detta är praktiskt för efterföljande UI‑arbete.

---

## Vanliga frågor & kantfall

### Vad händer om bildsökvägen är ogiltig?

Omge bitmap‑laddningen med ett `try/catch`‑block och visa ett tydligt felmeddelande:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Hur hanterar jag icke‑engelska språk?

Byt bara `Language`‑egenskapen:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose stödjer över 50 språk, så välj det som matchar ditt källmaterial.

### Måste jag disponera `Bitmap`‑objekt?

Ja. `Bitmap` implementerar `IDisposable`, så omge det med ett `using`‑statement för att snabbt frigöra inhemska resurser.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Vad om jag vill ha en kompakt JSON utan indentering?

Byt ut `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Det minskar filstorleken—användbart i bandbreddsbegränsade scenarier.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra)

Nedan är det kompletta programmet som inkluderar alla stegen, felhantering och bästa praxis‑tips som diskuterats ovan. Spara det som `Program.cs` och kör det från kommandoraden eller din IDE.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Vad detta gör:**  
1. Kontrollerar att bilden finns.  
2. Laddar den säkert med ett `using`‑block.  
3. Kör OCR för att **extrahera text från bild**.  
4. Serialiserar resultatet till en snyggt indenterad JSON‑sträng.  
5. Sparar den strängen till disk, vilket svarar på kärnfrågan **hur man sparar json**.

Kör `dotnet run` (eller tryck F5 i Visual Studio) så ser du bekräftelsemeddelandet när filen har skrivits.

---

## Slutsats

Du har nu ett komplett, produktionsklart recept för **hur man sparar JSON** som härrör från OCR‑baserad textutvinning. Från att ladda en bitmap‑bild till att skriva en ren JSON‑fil förklaras varje steg med “varför” bakom koden, så att du kan anpassa lösningen till dina egna projekt.

Om du är nyfiken på nästa steg, överväg:

- **Hur man extraherar text** från PDF‑filer genom att först konvertera varje sida till en bild.  
- Att använda avgränsningsrutor för att markera ord i ett WPF‑ eller WinForms‑UI.  
- Att streama JSON‑en direkt till ett webb‑API istället för att skriva en fil (använd `HttpClient`).

Ge det ett försök, justera alternativen, och låt OCR‑data driva den applikation du bygger. Har du frågor? Lämna en kommentar, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}