---
category: general
date: 2026-02-20
description: Lär dig hur du läser ett kvitto i C# genom att extrahera text från en
  bild och konvertera den till JSON. Steg‑för‑steg‑kod med Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: sv
og_description: Upptäck hur du läser kvitto i C# genom att ladda en bildfil, extrahera
  text med Aspose OCR och konvertera resultatet till JSON. Fullständigt kodexempel.
og_title: Hur man läser kvitto i C# – Extrahera text, konvertera till JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Hur man läser kvitto i C# – Komplett guide för att extrahera text från bild
url: /sv/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man läser kvitto i C# – Komplett guide

Har du någonsin undrat **how to read receipt** bilder programatiskt? Kanske bygger du en utgiftsspårningsapp och behöver hämta radposter från ett foto av ett matvarukvitto. Enligt min erfarenhet är den största smärtan att omvandla den suddiga JPEG‑filen till strukturerad data som du faktiskt kan använda. De goda nyheterna? Med några rader C# och Aspose OCR kan du **extract text from image**, sedan **convert image to JSON** på ett sätt som känns nästan magiskt.

I den här handledningen får du en färdig‑att‑köra lösning som **loads an image file C#**, kör OCR och spottar ut en detaljerad JSON‑payload. Inga externa tjänster, inga krångliga REST‑anrop—bara ren .NET‑kod som du kan slänga in i vilket konsol‑ eller ASP.NET‑projekt som helst. I slutet kommer du att förstå varför varje steg är viktigt, hur du hanterar vanliga edge cases (som icke‑standardiserade kvittostorlekar), och hur JSON‑utdata faktiskt ser ut.

## Vad du behöver

- **.NET 6.0 eller senare** – koden använder `System.Drawing.Common` som stöds på Windows, Linux och macOS.
- **Aspose.OCR för .NET** – du kan hämta ett gratis prov‑NuGet‑paket (`Aspose.OCR`) eller använda en licensierad kopia om du har en.
- En **sample receipt image** (`receipt.jpg`) placerad någonstans där din app kan läsa den.
- Valfri IDE du föredrar (Visual Studio, Rider, VS Code).  

Det är allt. Ingen extra konfiguration, inga API‑nycklar.

---

## Steg 1 – Load the Image File C# (Primary Keyword in Action)

Innan OCR‑motorn kan göra sin magi måste du få bilden in i minnet. Detta är det klassiska “load image file C#”‑steget som många utvecklare förbiser.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Varför detta är viktigt:**  
`Image.FromFile` läser filen *en gång* och behåller ett öppet handtag, vilket är perfekt för ett snabbt OCR‑pass. Om du bearbetar många kvitton i en loop, överväg att använda `Image.FromStream` för att undvika att låsa filen.

> **Proffstips:** Om du får en *FileNotFoundException*, dubbelkolla sökvägen och se till att bilden faktiskt finns där. Relativa sökvägar fungerar också (`"./receipt.jpg"`), men absoluta sökvägar är säkrare för produktionsjobb.

---

## Steg 2 – Create and Configure the OCR Engine

Aspose OCR levereras med en färdig `OcrEngine`. Du behöver inte träna en modell; biblioteket vet redan hur man läser tryckt text, vilket är exakt vad de flesta kvitton använder.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Varför vi sätter dessa alternativ:**  
`DetectOrientation` instruerar motorn att automatiskt rotera bilden om kvittot skannades upp och ner. Att ange språk begränsar teckenuppsättningen, vilket kan förbättra noggrannheten—särskilt när du bara behöver engelska alfanumeriska data.

---

## Steg 3 – Recognize the Image and Convert to JSON

Nu kommer den roliga delen: **extract text from image** och **convert image to JSON** i ett enda anrop.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

`RecognizeToJson`‑metoden returnerar en rik JSON‑struktur som innehåller:

- `Text`: den enkla sammanslagna texten.
- `Lines`: en array av rad‑objekt med koordinater.
- `Words`: varje ord med förtroendescore.
- `Regions`: avgränsningsrutor för upptäckta textblock.

Du kan deserialisera denna JSON till ett C#‑objekt om du behöver typad åtkomst, men för många scenarier räcker det att skriva ut den råa JSON‑en.

---

## Steg 4 – Output the JSON (or Store It)

Låt oss titta på utskriften och diskutera vad man ska göra med den.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Exempel på utskrift

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Vad gör man härnäst?**  
Parsa `Lines`‑arrayen för att hämta `Total`‑beloppet, eller skicka JSON‑en till en downstream‑tjänst som lagrar utgiftsposter. Eftersom resultatet redan är JSON kan du ansluta det direkt till vilken NoSQL‑databas, Azure Function eller Power Automate‑flöde som helst.

---

## Steg 5 – Handling Common Edge Cases

Även de bästa OCR‑motorerna snubblar på några saker. Nedan är scenarier du kan stöta på när du lär dig **how to read receipt** bilder.

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **Lågupplöst kvitto (≤ 150 dpi)** | Upscale the image first using `Bitmap` and `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Roterat eller skevt kvitto** | Keep `DetectOrientation = true`. For severe skew, pre‑process with `Image.RotateFlip` or a third‑party library like OpenCV. |
| **Färgad bakgrund (t.ex. kvitto på ett bord)** | Convert to grayscale and increase contrast before OCR (`ImageAttributes`). |
| **Flera kvitton i ett foto** | Crop each receipt region manually or use `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Stora filer som orsakar OutOfMemory** | Use `using` statements to dispose `Image` objects promptly, or process in chunks. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Steg 6 – Full Working Example (Copy‑Paste Ready)

Nedan är det *kompletta* programmet som du kan kompilera direkt nu. Det inkluderar alla stegen, korrekta `using`‑direktiv och elegant felhantering.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Kör det:**  
`dotnet run` från projektmappen. Om allt är korrekt konfigurerat kommer du att se JSON‑en skriven i konsolen och sparad bredvid din kvittobild.

---

## Slutsats

Vi har precis gått igenom **how to read receipt** bilder i C# från början till slut. Genom att ladda bilden, konfigurera Aspose OCR och anropa `RecognizeToJson` kan du **extract text from image** och **convert image to JSON** med praktiskt taget ingen boilerplate. Metoden skalar—från en enkeldemonstration till en batch‑processor som hanterar hundratals kvitton varje natt.

Nästa steg du kan utforska:

- **Parse the JSON** för att hämta datum, totalbelopp och radposter (använd `System.Text.Json` eller `Newtonsoft.Json`).
- **Integrate with a database** (SQL, Cosmos DB) för att automatiskt lagra utgiftsposter.
- **Add a UI** (WinForms, WPF eller Blazor) så att användare kan dra‑och‑släppa kvitton.
- **Swap Aspose OCR** mot en annan motor (Tesseract, Microsoft Azure OCR) om licensiering är ett problem—behåll bara samma “load image file C#”‑mönster.

Känn dig fri att experimentera, bryta saker, och sedan komma tillbaka hit för en uppfriskning. Om du stöter på problem är communityn (och Aspose‑forumet) bra ställen att fråga på. Lycka till med kodandet, och njut av att förvandla papperkvitton till ren, sökbar data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}