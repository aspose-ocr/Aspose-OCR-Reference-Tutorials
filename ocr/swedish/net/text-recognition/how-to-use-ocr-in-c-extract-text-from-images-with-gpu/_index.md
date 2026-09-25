---
category: general
date: 2026-02-13
description: Lär dig hur du använder OCR i C# för att extrahera text från bildfiler,
  aktivera GPU‑bearbetning och konvertera skanningar till text snabbt.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: sv
og_description: Hur använder man OCR i C#? Den här guiden visar hur du extraherar
  text från bildfiler, aktiverar GPU-bearbetning och konverterar skanningar till text.
og_title: Hur man använder OCR i C# – Extrahera text från bilder med GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Hur man använder OCR i C# – Extrahera text från bilder med GPU
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från bilder med GPU

Har du någonsin undrat **how to use OCR** för att hämta text från ett skannat dokument utan ansträngning? Du är inte ensam—utvecklare frågar ständigt, “Hur kan jag extrahera text från bildfiler på ett effektivt sätt?” Den goda nyheten är att med Aspose.OCR kan du göra exakt det, och du kan till och med **enable GPU processing** för en märkbar hastighetsökning på stödjande hårdvara.

I den här handledningen går vi igenom ett komplett, end‑to‑end‑exempel som visar dig **how to use OCR**, hur man **extract text from image**, hur man **convert scan to text**, och vad man ska göra om GPU:n inte är tillgänglig. I slutet har du en färdig‑att‑köra C#‑konsolapp som skriver ut den igenkända texten och berättar om GPU:n faktiskt användes.

## Vad du behöver

- .NET 6 SDK eller senare (koden fungerar även med .NET Core)  
- Visual Studio 2022 eller någon editor du föredrar  
- Aspose.OCR för .NET‑paket (tillgängligt via NuGet)  
- En hög‑upplöst bildfil (t.ex. `highres_scan.tif`) för testning  

Ingen avancerad konfiguration krävs—bara några NuGet‑kommandon så är du redo att köra.

## Steg 1: Installera Aspose.OCR och förbered projektet

Först och främst. Du måste lägga till OCR‑biblioteket i ditt projekt. Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Det skapar ett nytt konsolprojekt med namnet **OcrDemo** och lägger till `Aspose.OCR`‑NuGet‑paketet. Biblioteket innehåller klassen `OcrEngine` som vi kommer att använda.

> **Pro tip:** Om du använder en maskin med ett dedikerat GPU, se till att den senaste grafikdrivrutinen är installerad; annars kommer biblioteket automatiskt att falla tillbaka till CPU‑läge.

## Steg 2: Skriv den kompletta OCR‑koden

Öppna nu `Program.cs` och ersätt dess innehåll med följande. Varje rad är kommenterad så att du kan se *varför* vi gör som vi gör.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Varför detta fungerar

- **ProcessingMode = Gpu** talar om för motorn att först försöka med GPU. Biblioteket abstraherar bort de lågnivå CUDA/OpenCL‑anropen, så du behöver inte hantera enhetskontexter själv.  
- **IsGpuEnabled** är en boolean som bekräftar om GPU‑vägen lyckades. Om du ser `false` har motorn automatiskt fallit tillbaka till CPU—ingen anledning att oroa sig.  
- **RecognizeImage** gör allt tungt arbete: den laddar bilden, kör OCR‑modellen och returnerar resultatet som ren text. Ingen behov av att manuellt förbehandla bitmapen om du inte har speciella krav (t.ex. deskewing).

## Steg 3: Kör applikationen och verifiera outputen

Kompilera och kör:

```bash
dotnet run
```

Om allt är korrekt konfigurerat kommer du att se något liknande:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Om GPU:n inte är tillgänglig kommer den första raden att visa `GPU used: False`, men den extraherade texten kommer fortfarande att visas—tack vare den eleganta fallback‑mekanismen.

> **Common question:** *What if my image is a JPEG instead of a TIFF?*  
> Metoden `RecognizeImage` accepterar alla format som stöds av .NET:s `System.Drawing` (JPEG, PNG, BMP, etc.). Byt bara filändelsen i `imagePath`.

## Steg 4: Valfritt – Justera inställningar för bättre noggrannhet

Aspose.OCR erbjuder några reglage du kan justera:

| Setting | Vad den gör | När den ska användas |
|---------|--------------|----------------------|
| `ocrEngine.Language` | Tvingar ett specifikt språk (t.ex. `OcrLanguage.English`) | Om du känner till dokumentets språk |
| `ocrEngine.PageSegMode` | Styr hur motorn delar upp sidor i block | För flerkolumnslayouter |
| `ocrEngine.DetectOrientation` | Auto‑roterar text som inte är upprätt | Skanningar som kan vara upp och ner |

Du kan sätta dessa egenskaper innan du anropar `RecognizeImage`. Till exempel:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Steg 5: Visualisera flödet (Bild med alt‑text)

Nedan är ett enkelt diagram som illustrerar **how to use OCR** med valfri GPU‑acceleration. Det är inte ett krav för att koden ska köras, men det hjälper dig att se helheten.

![Diagram som visar hur man använder OCR med GPU‑behandling](/images/ocr-gpu-flow.png)

*Alt text:* *Diagram som visar hur man använder OCR med GPU‑behandling, med markering av fallback till CPU när det behövs.*

## Edge Cases & Felsökning

1. **Out‑of‑Memory on GPU** – Mycket stora bilder kan överskrida GPU‑minnet. I så fall återgår biblioteket automatiskt till CPU. Du kan för‑skala bilden för att hålla minnesanvändningen låg.  
2. **Unsupported Image Format** – Om `RecognizeImage` kastar *NotSupportedException*, verifiera filändelsen och säkerställ att bilden inte är korrupt. Att konvertera till PNG löser ofta problemet.  
3. **Low Confidence Scores** – När OCR‑resultatet innehåller många oläsliga tecken, överväg förbehandling (binarisering, brusreducering) eller byt till en högre upplösning på skanningen.  

## Sammanfattning: Vad vi uppnådde

Vi har precis gått igenom **how to use OCR** i en C#‑konsolapp, demonstrerat hur man **extract text from image**‑filer, och visat hur man **enable GPU processing** för snabbare resultat. Du vet nu hur man **convert scan to text**, verifierar om GPU:n faktiskt användes, och justerar några inställningar för edge‑case‑scenarier.

### Nästa steg

- Försök att mata utdata till ett **search index** (t.ex. Elasticsearch) så att dina skannade PDF‑filer blir sökbara.  
- Experimentera med **batch processing**—loopa över en mapp med bilder och skriv varje resultat till en `.txt`‑fil.  
- Kombinera OCR med **translation APIs** för att automatiskt översätta skannade dokument på främmande språk.  

Har du fler frågor? lämna en kommentar, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}