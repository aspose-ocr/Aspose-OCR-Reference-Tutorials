---
category: general
date: 2026-03-15
description: Hur du använder Aspose OCR för att extrahera text från bilder och konvertera
  en bild till JSON i C#. Lär dig att känna igen text från PNG och snabbt få strukturerad
  output.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: sv
og_description: Hur du använder Aspose OCR för att extrahera text från bilder och
  konvertera bild till JSON i C#. Denna guide går dig igenom att känna igen text från
  PNG och få strukturerad utdata.
og_title: Hur man använder Aspose OCR för att konvertera bild till JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Hur du använder Aspose OCR för att konvertera bild till JSON
url: /sv/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

code block unchanged.

Then closing shortcodes.

Now produce final output.

Be careful with markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här använder du Aspose OCR för att konvertera bild till JSON

Att använda Aspose OCR är en vanlig fråga när utvecklare behöver extrahera text från bilder. Om du vill **konvertera bild till JSON** eller **känna igen text från PNG**, så täcker den här guiden allt—utan onödig text, bara en praktisk, helhetslösning.

På några minuter går vi igenom allt du behöver: installera biblioteket, konfigurera motorn för JSON‑utmatning, läsa in en kvitto‑PNG, köra OCR och slutligen skriva resultatet till en `.json`‑fil. När du är klar kan du **extrahera text från bild**‑filer med ett enda metodanrop, och du förstår varför varje steg är viktigt.

> **Pro tip:** Aspose OCR fungerar med ett brett spektrum av bildformat (PNG, JPEG, BMP, TIFF). Samma kod nedan hanterar dem alla, så du slipper skriva format‑specifik logik.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+)  
- Ett giltigt Aspose.OCR‑NuGet‑paket (gratis provversion eller licens)  
- En bildfil du vill bearbeta (t.ex. `receipt.png`)  
- Visual Studio, VS Code eller någon annan C#‑redigerare du föredrar  

Det är allt—inga extra beroenden, inga externa tjänster. Är du redo? Låt oss dyka in.

![hur man använder aspose OCR‑motor](image-placeholder.png "hur man använder aspose OCR‑motor")

## Så här använder du Aspose OCR – Konfigurera JSON‑utmatning

Det första du måste göra när du **hur man använder aspose** för OCR är att skapa en `OcrEngine`‑instans och tala om för den att leverera JSON. Denna lilla konfigurationsväxel sparar dig från att manuellt serialisera resultatet senare.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Varför detta är viktigt:** Att sätta `OutputFormat` till `Json` betyder att OCR‑motorn redan strukturerar texten i en hierarki av sidor, rader och ord. Du behöver inte parsra råa strängar senare, vilket gör efterföljande bearbetning—t.ex. att mata in data i en databas—mycket renare.

## Konvertera bild till JSON med Aspose OCR

Nu när motorn är konfigurerad, låt oss gå närmare in på **konvertera bild till JSON**‑delen.

1. **Läs in bilden** – `Image.FromFile` fungerar för alla stödjade format. Om du arbetar med en ström (t.ex. en uppladdad fil) kan du använda `Image.FromStream` istället.  
2. **Kör `Recognize`** – den här metoden returnerar ett `OcrResult`‑objekt. Eftersom vi har satt utmatningen till JSON, innehåller `ocrResult.Text` redan en JSON‑sträng.  
3. **Skriv filen** – `File.WriteAllText` är det enklaste sättet att spara JSON‑en. Om du behöver lagra den i en molnbucket, byt bara ut den här raden mot rätt SDK‑anrop.

### Förväntad JSON‑utmatning

Ett typiskt JSON‑payload ser ut så här (trimmat för korthet):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Du kan nu föra in den här strukturen i vilket efterföljande system som helst—oavsett om det är ett rapportverktyg, en maskininlärningsmodell eller en enkel loggfil.

## Extrahera text från bild med Aspose OCR

Om du bara behöver den råa strängen (dvs. du bryr dig inte om JSON), byt helt enkelt ut utmatningsformatet till vanlig text:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**När du ska välja vanlig text?**  
- Snabb felsökning eller konsolutmatning.  
- Scenarier där du ska tillämpa egen efterbehandling (t.ex. regex‑extraktion).  

Men kom ihåg, **extrahera text från bild** med JSON ger dig positionsdata—användbart för att markera text i ett UI eller anpassa med formulärfält.

## Känna igen text från PNG‑filer

PNG är ett förlustfritt format, vilket ofta ger bättre OCR‑noggrannhet jämfört med kraftigt komprimerade JPEG‑filer. Här är en snabb checklista för att säkerställa bästa resultat när du **känner igen text från PNG**:

| Checklista | Varför det hjälper |
|------------|---------------------|
| Använd DPI 300+ | Högre upplösning ger motorn fler pixlar att arbeta med. |
| Håll bilden i gråskala | Minskar brus; Aspose OCR konverterar automatiskt, men förbehandling kan snabba upp processen. |
| Ta bort bakgrundsstörningar | Rena bakgrunder förbättrar förtroendesiffror. |

Om du får låga förtroendesiffror, prova att öka DPI eller applicera ett enkelt tröskelfilter innan du skickar bilden till Aspose.

## Så här extraherar du OCR‑resultat programatiskt

Förutom att bara spara JSON, kanske du vill läsa specifika fält programatiskt—t.ex. totalbeloppet på ett kvitto. Eftersom JSON‑en innehåller en hierarki kan du deserialisera den till ett C#‑objekt:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Nu kan du fråga `ocrData` med LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Varför detta fungerar:** JSON‑en berättar redan var varje ord finns på sidan, så du kan på ett pålitligt sätt lokalisera fält även om layouten förändras något.

## Edge Cases & Common Pitfalls

- **Null‑resultat:** Om `ocrEngine.Recognize` returnerar `null` kan bilden vara ett format som inte stöds eller vara korrupt. Säkerställ alltid att hantera detta:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Stora filer:** För bilder på flera megabyte, överväg att streama bilden eller minska storleken innan OCR för att undvika onödig minnesanvändning.

- **Licensproblem:** Provversionen lägger till ett vattenmärke i utmatningen. Se till att ladda din licens tidigt i programmet:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Icke‑latinska skript:** Aspose OCR stödjer många språk, men du måste sätta `Language`‑egenskapen korrekt (t.ex. `ocrEngine.Configuration.Language = Language.English;`).

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}