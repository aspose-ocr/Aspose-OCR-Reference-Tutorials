---
category: general
date: 2026-03-05
description: hur man använder OCR i C# för att extrahera text från kvittobilder. Lär
  dig hur du laddar bild för OCR och känner igen kvittobilden på några minuter.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: sv
og_description: hur man använder OCR i C# för att extrahera text från kvitton. Följ
  den här steg‑för‑steg‑guiden för att ladda en bild för OCR och känna igen kvittobilden
  effektivt.
og_title: hur man använder OCR i C# – Snabb extrahering av kvittotext
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: hur man använder OCR i C# – Extrahera text från kvitton snabbt
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# så här använder du OCR i C# – Extrahera text från kvitton snabbt

Har du någonsin undrat **how to use OCR** för att hämta data direkt från ett foto av ett matvarukvitto? Du är inte ensam. I många småföretagsappar är flaskhalsen att omvandla en suddig PNG till strukturerad text som du faktiskt kan arbeta med.  

Den goda nyheten? Med några rader C# och Aspose.OCR kan du **load image for OCR**, köra motorn och **recognize receipt image** på under en minut. Nedan ser du ett komplett, färdigt‑att‑köra exempel, plus tips för de knepiga delarna som de flesta handledningar hoppar över.

## Vad den här guiden täcker

Vi går igenom allt du behöver veta:

* Installera Aspose.OCR NuGet‑paketet.  
* Ställ in OCR‑motorn – kärnan i **how to use OCR** korrekt.  
* Ladda en kvittofil (det är **load image for OCR**‑steget).  
* Kör igenkänningsprocessen och hämta både JSON‑ och XML‑layoutdata.  
* Hantera vanliga fallgropar som saknade licenser eller ej stödda bildformat.  

När du är klar har du ett självständigt program som extraherar texten från vilket kvitto du än lägger i en mapp. Inga externa tjänster, ingen dold magi.

## Förutsättningar

* .NET 6 SDK eller senare (koden kompileras även med .NET Core).  
* En giltig Aspose.OCR‑licensfil (`Aspose.OCR.lic`). Du kan få en gratis provversion från Aspose om du ännu inte har en.  
* En exempelkvittobild – `receipt.png` fungerar bra, men vilket vanligt rasterformat som helst går.  

Om du redan har dem, toppen – låt oss dyka ner.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Steg 1: Installera Aspose.OCR och skapa ett nytt projekt

Först och främst: du behöver biblioteket som faktiskt gör det tunga arbetet. Öppna en terminal i din projektmapp och kör:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Det kommandot skapar en konsolapp och hämtar det senaste Aspose.OCR‑paketet. Enligt min erfarenhet gör ett kort projektnamn de genererade sökvägarna lättare att läsa, särskilt när du börjar jonglera flera demo‑appar.

## Steg 2: Initiera OCR‑motorn – hjärtat i **how to use OCR**

Nu ska vi skriva koden som svarar på frågan “**how to use OCR** i C#”. Öppna `Program.cs` och ersätt innehållet med kodsnutten nedan. Lägg märke till kommentarerna – de förklarar *varför* bakom varje rad, inte bara *vad*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Varför detta fungerar

* **`OcrEngine`** är ingångspunkten; den innehåller all konfiguration du eventuellt kan justera senare (språk, DPI osv.).
* **`SetLicense`** tar bort utvärderingsvattenstämpeln – ett avgörande steg när du planerar att distribuera koden.
* **`ImageStream.FromFile`** utför **load image for OCR**‑arbetet och hanterar PNG, JPEG, BMP, TIFF och mer.
* **`Recognize()`** är metoden som faktiskt **recognize receipt image**. Under huven utför den binarisering, segmentering och teckenklassificering.
* Export till JSON och XML ger dig både en mänskligt läsbar dump och en maskinvänlig struktur som du kan mata in i efterföljande parsers.

## Steg 3: Kör demon och verifiera resultatet

Kompilera och kör:

```bash
dotnet run
```

Om allt är korrekt konfigurerat kommer du att se något liknande:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Konsolen skriver ut ren text, medan `receipt.json` och `receipt.xml` innehåller detaljerad layoutinformation (koordinater, förtroendescore osv.). Dessa filer är praktiska om du senare behöver mappa varje rad till ett databasfält.

## Edge Cases & Pro‑tips

### 1️⃣ Saknad eller ogiltig licens
Om `SetLicense` misslyckas faller motorn tillbaka till provläge och du får en vattenstämpel i resultatet. Omge anropet med en try/catch och logga ett vänligt meddelande:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Ej stödda bildformat
Aspose.OCR stöder de flesta rasterformat, men om du matar in en PDF eller en fler‑sidig TIFF måste du först konvertera den sida du är intresserad av till en bild. Biblioteket `Aspose.PDF` kan hantera den konverteringen.

### 3️⃣ Stora kvitton & prestanda
Att bearbeta en 10 MB bild kan vara långsamt. Minska upplösningen innan du skickar den till motorn:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

`Resize`‑metoden behåller bildförhållandet (`0` för höjd) och minskar filstorleken dramatiskt utan att offra OCR‑noggrannheten för vanliga kvitton.

### 4️⃣ Språk‑ och teckensnittsproblem
Kvitton kan innehålla specialtecken (€, ¥ osv.). Ställ in språket explicit om du känner till lokalen:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

För kvitton med blandade språk kan du aktivera flerspråkigt läge:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Extrahera strukturerad data
Råtexten är användbar, men de flesta appar behöver strukturerade fält (datum, total, artiklar). JSON‑layouten innehåller `BoundingBox`‑koordinater för varje ord. Du kan efterbehandla den så här:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Den kodsnutten visar idén; i produktion skulle du sannolikt använda ett reguljärt uttryck eller en liten regelmotor.

## Vanliga frågor

**Q: Kan jag köra detta på Linux?**  
A: Absolut. Aspose.OCR är plattformsoberoende; installera bara .NET‑runtime på din Linux‑maskin så fungerar samma kod.

**Q: Vad händer om jag måste bearbeta dussintals kvitton per minut?**  
A: Skapa en `Parallel.ForEach`‑loop och återanvänd en enda `OcrEngine`‑instans – den är trådsäker för skriv‑fria operationer. Kom ihåg att hantera licensens samtidighetsgränser.

**Q: Fungerar detta med mobilfoton tagna i vinkeln?**  
A: Motorn innehåller grundläggande deskewing, men för kraftigt snedvridna bilder kan du förbehandla med ett bildbehandlingsbibliotek (t.ex. OpenCV) för att räta upp kvittot först.

## Fullt fungerande exempel (kopiera‑klistra in)

Nedan är det *hela* programmet som du kan klistra in i `Program.cs`. Inga andra filer krävs förutom licensen och en kvittobild.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}