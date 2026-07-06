---
category: general
date: 2026-04-03
description: igenkänna text från en bild med Aspose OCR i C#. Lär dig att ladda bild
  för OCR, extrahera text från bilden, skriva JSON‑fil i C# och utföra OCR på PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: sv
og_description: Känn igen text från bild med Aspose OCR i C#. Steg‑för‑steg‑guide
  för att ladda bild för OCR, extrahera text från bilden, skriva JSON‑fil i C# och
  utföra OCR på PNG.
og_title: Känn igen text från bild i C# – Komplett Aspose OCR-handledning
tags:
- OCR
- C#
- Aspose
title: Igenkänna text från bild i C# – Fullständig Aspose OCR‑guide
url: /sv/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna text från bild i C# – Komplett Aspose OCR-handledning

Har du någonsin behövt **igenkänna text från bild** men varit osäker på vilket bibliotek du ska välja? Kanske har du en bunt skannade kvitton, en PNG‑skärmdump eller en handskriven lapp som du vill omvandla till sökbar data. Den goda nyheten: med Aspose.OCR kan du göra det på några få rader C#‑kod, och du får dessutom en prydlig JSON‑fil som du kan mata in i andra system.

I den här handledningen går vi igenom hur du laddar en bild för OCR, extraherar text från bilden, serialiserar resultatet till en JSON‑fil och slutligen hanterar PNG‑filer utan att svettas. När du är klar har du en färdig konsolapp som **igenkänner text från bild** och skriver utdata till *output.json*.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även med .NET Framework)
- Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)
- En PNG (eller något annat stödformat) som du vill bearbeta
- Visual Studio, VS Code eller någon annan C#‑redigerare du föredrar

Inga ytterligare tredjepartsbibliotek krävs – bara Aspose OCR‑motorn och den inbyggda `System.Text.Json`‑serialisatorn.

## Steg 1: Igenkänna text från bild med Aspose OCR

Det första du måste göra är att skapa en `OcrEngine`‑instans. Detta objekt sköter det tunga arbetet bakom kulisserna.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Varför det är viktigt:** Att instansiera `OcrEngine` en gång och återanvända den är mer effektivt än att skapa en ny motor för varje fil. Anropet `RecognizeToResult` returnerar ett `OcrResult`‑objekt som redan innehåller den extraherade texten, förtroendesiffror och avgränsningsrutor – perfekt för vidare bearbetning.

## Steg 2: Ladda bild för OCR – hantera olika format

Aspose OCR kan läsa PNG, JPEG, BMP och många andra format. Om du arbetar med en PNG som innehåller transparens kan det vara bra att platta till den först för att undvika oväntade tomrum.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Proffstips:** Kontrollera alltid att bildens dimensioner är rimliga (t.ex. bredd > 50 px). Mycket små bilder kan få OCR‑motorn att missa tecken, vilket ger låga förtroendesiffror.

## Steg 3: Skriva JSON‑fil i C# – göra utdata konsumabel

`System.Text.Json`‑serialisatorn är snabb och inbyggd, men du kan byta ut den mot `Newtonsoft.Json` om du behöver anpassade konverterare. Exemplet ovan använder redan `WriteIndented = true` så den resulterande filen blir lättläst för människor.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Att ha OCR‑data i JSON gör det enkelt att importera till databaser, skicka över HTTP eller mata in i maskininlärnings‑pipelines.

## Steg 4: Verifiera resultatet – snabb kontroll

När programmet har körts, öppna `output.json` och leta efter fältet `"Text"`. Om det innehåller den förväntade strängen har du lyckats **extrahera text från bild**. Om förtroendet är lågt, överväg att förbehandla bilden (t.ex. öka kontrasten eller applicera ett binärt tröskelvärde).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

Körning av konsolen skriver ut något i stil med:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Det är ett tydligt tecken på att OCR‑processen fungerade som avsett.

## Vanliga fallgropar & kantfall

| Problem | Varför det händer | Så löser du det |
|---------|-------------------|-----------------|
| **Tomt resultat** | Bilden är för mörk eller har ett färgrymd som inte stöds | Konvertera till gråskala, öka ljusstyrkan eller platta till PNG (se Steg 2) |
| **Skräptecken** | Låg DPI (< 72) eller mycket brus | Skala upp bilden eller applicera ett brusreduceringsfilter innan du anropar `RecognizeToResult` |
| **Stora filer ger minnespress** | Att ladda en multi‑megapixel PNG i en `Bitmap` förbrukar RAM | Bearbeta bilder i delar eller skala ner dem samtidigt som läsbarheten bevaras |
| **JSON‑serialiseringsfel** | `OcrResult` innehåller cirkulära referenser (osannolikt) | Använd `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus: Utföra OCR på PNG i en batch‑loop

Om du har en mapp full av PNG‑filer kan du utöka demon för att iterera över dem:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Nu **utför programmet OCR på PNG**‑filer i mängd och skriver en motsvarande JSON‑fil för varje bild.

## Slutsats

Du har precis lärt dig hur du **igenkänner text från bild** i C# med Aspose OCR, **laddar bild för OCR**, **extraherar text från bild** och **skriver JSON‑fil i C#** för att lagra resultaten. Det kompletta, körbara exemplet täcker de viktigaste stegen, förklarar varför varje del är viktig och visar även hur du hanterar PNG‑specifika nycker.

Nästa steg? Prova att mata in JSON‑filen i ett sökindex, kombinera den med språkdetection eller integrera den i ett webb‑API som bearbetar uppladdningar i realtid. Du kan också utforska Asposes stöd för handskriftigenkänning om ditt användningsfall kräver det.

Har du frågor om kantfall eller prestandaoptimering? Lämna en kommentar nedan – lycka till med kodandet! 

![igenkänna text från bild demo](/images/ocr-demo.png "Diagram som visar hur Aspose OCR igenkänner text från bild")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}