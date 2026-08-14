---
category: general
date: 2026-02-28
description: hur man kör OCR i C# med Aspose OCR – lär dig hur du extraherar text
  från en bild, konverterar bilden till JSON eller XML på bara några steg.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: sv
og_description: hur man kör OCR i C# med Aspose OCR – upptäck hur du extraherar text
  från en bild och konverterar bilden till JSON eller XML med ett färdigt exempel
  som är redo att köras.
og_title: hur man kör OCR med Aspose OCR i C# – Komplett guide
tags:
- OCR
- C#
- Aspose
- Image Processing
title: så här kör du OCR med Aspose OCR i C# – Komplett guide
url: /sv/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man kör OCR med Aspose OCR i C# – Komplett guide

Om du undrar **hur man kör OCR** på en kvittobild med C#, har du kommit till rätt ställe. I den här handledningen går vi igenom **extrahera text från bild** och sedan **konvertera bild till JSON** eller **konvertera bild till XML** med Aspose OCR—allt i ett enda, fristående program.

Föreställ dig att du bygger en app för utgiftsspårning och behöver hämta rader från fotograferade kvitton. Att skriva in varje post manuellt är jobbigt, eller hur? I slutet av den här guiden har du ett återanvändbart kodsnutt som läser vilken bild som helst, returnerar strukturerad text och ger dig både JSON- och XML-representationer redo för vidare bearbetning.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar också på .NET Framework 4.8)
- Visual Studio 2022 (eller någon annan editor du föredrar)
- Ett aktivt **Aspose.OCR** NuGet‑paket (`Install-Package Aspose.OCR`)
- En exempelbild (t.ex. `receipt.png`) placerad i en mapp du kan referera till

Ingen ytterligare konfiguration krävs; biblioteket levereras med alla nödvändiga OCR-modeller.

![Kvitto bild för OCR‑behandling – hur man kör OCR](receipt.png)

> *Alt text: Kvitto bild för OCR‑behandling – hur man kör OCR*

## Steg‑för‑steg‑implementering

Nedan delar vi upp lösningen i logiska delar. Varje steg förklarar **varför** vi gör det, inte bara **vad** koden ser ut.

### 1️⃣ Initiera OCR‑motorn – grunden för **hur man kör OCR**

`OcrEngine`‑klassen är ingångspunkten. Att instansiera den laddar de interna språkmodellerna och förbereder motorn för igenkänning.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Proffstips:** Att återanvända samma `OcrEngine` för flera bilder minskar minnesanvändning och snabbar upp batch‑bearbetning.

### 2️⃣ Ladda bilden – kärnan i **extrahera text från bild**

Aspose OCR arbetar med sin egen `Image`‑wrapper. Att använda ett `using`‑statement garanterar att filhandtaget släpps omedelbart.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Om bilden är i ett annat format (BMP, TIFF, PDF) hanterar samma `Load`‑metod den—ingen extra konvertering behövs.

### 3️⃣ Kör OCR‑igenkänning – hjärtat i **hur man kör OCR**

Att anropa `Recognize` utför det tunga arbetet: layoutanalys, teckensegmentering och språk‑specifik klassificering.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Det returnerade `OcrResult` innehåller råtext, förtroendescore och ett detaljerat layoutträd som kan serialiseras.

### 4️⃣ Konvertera bild till JSON – det enkla sättet att **konvertera bild till json**

JSON är perfekt för webb‑API:er eller NoSQL‑lagring. `ToJson`‑metoden ger dig en snyggt formaterad sträng, vilket gör felsökning enkelt.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Typisk JSON‑utdata ser ut så här (avkortad för korthet):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Du kan nu skicka denna JSON direkt till en REST‑endpoint eller lagra den i Azure Cosmos DB.

### 5️⃣ Konvertera bild till XML – när **konvertera bild till xml** krävs

Vissa äldre system använder fortfarande XML. Aspose tillhandahåller `ToXml` för en ren, schema‑kompatibel representation.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Exempel på XML‑snutt:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Båda formaten bevarar samma hierarkiska data, så du kan välja det som passar din efterföljande pipeline.

## Vanliga fallgropar & hur man extraherar text pålitligt

Även med ett robust bibliotek kan verkliga bilder ge oväntade problem. Här är tre problem du kan stöta på och motsvarande lösningar.

### 📏 Lågre­sultatbilder

**Varför det är viktigt:** Små teckensnitt smälter ihop, vilket minskar förtroendescore.  
**Lösning:** Förprocessa bilden—skala upp med `Image.Resize` eller applicera ett skärpande filter innan du skickar den till `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Dålig kontrast

**Varför det är viktigt:** Ljus text på mörk bakgrund förvirrar segmenteringsalgoritmen.  
**Lösning:** Invertera färger eller justera ljusstyrka/kontrast via `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Flerspråkiga dokument

**Varför det är viktigt:** Standard språkmodell är engelska; blandade språk ger förvrängd utdata.  
**Lösning:** Sätt `ocrEngine.Language = OcrLanguage.Multilingual;` innan igenkänning.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Att hantera dessa kantfall säkerställer att **extrahera text** från vilken bild som helst blir en pålitlig rutin snarare än ett spel.

## Fullt fungerande exempel (Kopiera‑klistra redo)

Nedan är det kompletta programmet, redo att kompileras och köras. Byt bara ut `YOUR_DIRECTORY` mot sökvägen till din bild och tryck F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Förväntad konsolutdata** (formaterad för läsbarhet) visar både JSON‑ och XML‑strukturer som innehåller den extraherade texten och avgränsningsrutorna.

## Sammanfattning – Vad vi gick igenom

- **hur man kör OCR** med Aspose OCR i C#
- Steg‑för‑steg‑processen för **extrahera text från bild**
- Två serialiseringsalternativ: **konvertera bild till json** och **konvertera bild till xml**
- Tips för att hantera lågre­sultat, låg‑kontrast och flerspråkiga scenarier
- Ett komplett, kopiera‑klistra‑redo kodexempel som du kan lägga in i vilket .NET‑projekt som helst

## Vad blir nästa?

Nu när du kan **extrahera text** och få strukturerad data, fundera på dessa uppföljningsidéer:

- Skicka JSON till en Azure Function som lagrar kvitton i Cosmos DB.
- Använd XML‑utdata för att fylla i ett befintligt SOAP‑baserat bokföringssystem.
- Kombinera Aspose OCR med en maskininlärningsmodell för att automatiskt kategorisera utgiftstyper.

Känn dig fri att experimentera—byt ut `receipt.png` mot fakturor, visitkort eller handskrivna anteckningar. Samma mönster fungerar över

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}