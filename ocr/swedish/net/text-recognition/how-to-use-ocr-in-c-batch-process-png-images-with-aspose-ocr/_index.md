---
category: general
date: 2026-02-14
description: Hur man använder OCR i C# för att snabbt extrahera text från PNG-filer.
  Lär dig batch‑OCR av bilder, bearbeta flera bilder och använda Aspose OCR C# i en
  enda guide.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: sv
og_description: Hur man använder OCR i C# med Aspose OCR C#. Denna handledning visar
  hur man extraherar text från PNG‑filer, batch‑OCR‑bilder och bearbetar flera bilder
  effektivt.
og_title: Hur du använder OCR i C# – Batchextrahering av text från PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hur man använder OCR i C# – Batchbearbeta PNG-bilder med Aspose OCR
url: /sv/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Batch‑processa PNG‑bilder med Aspose OCR

Har du någonsin undrat **how to use OCR** för att hämta text från en massa PNG‑filer utan att skriva en separat rutin för varje? Du är inte ensam. Många utvecklare stöter på problem när de måste **extract text PNG**‑tillgångar i stor skala, särskilt när bilderna ligger i en mapp och du måste starta OCR‑motorn för varje fil.  

I den här guiden går vi igenom en komplett, färdig‑att‑köra lösning som **batch OCR images**, **process multiple images** i parallell, och utnyttjar det kraftfulla **Aspose OCR C#**‑biblioteket. I slutet har du ett enda körbart program som läser ett godtyckligt antal PNG‑filer, extraherar deras text och skriver ut resultaten till konsolen – allt med bara några rader kod.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework)  
- En giltig Aspose.OCR för .NET‑licens (eller gratis provversion) – du kan hämta den från Aspose‑webbplatsen.  
- En mapp som innehåller PNG‑filerna du vill läsa.  
- Visual Studio 2022 (eller någon C#‑kompatibel IDE).  
- Inga ytterligare NuGet‑paket krävs förutom `Aspose.OCR`.

## Steg 1: How to Use OCR – Initiera Aspose OCR Engine

Det första du behöver är en instans av klassen `Engine`. Detta objekt abstraherar den underliggande OCR‑teknologin och kan köras på CPU eller GPU, beroende på din hårdvara och licens.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Varför detta är viktigt:* Att initiera motorn en gång och återanvända den över trådar sparar minne och undviker overheaden av att upprepade gånger ladda OCR‑modeller. Det garanterar också konsekventa inställningar för alla bilder.

## Steg 2: Extract Text PNG – Samla bildvägarna

Nästa steg är att samla en samling av filvägar. I ett riktigt projekt kan du läsa katalogen dynamiskt, men för tydlighetens skull listar vi några exempel‑filer.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tips:* Ersätt `YOUR_DIRECTORY` med den absoluta eller relativa sökvägen till dina bilder. Om du har dussintals filer kan du ersätta den manuella listan med `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Steg 3: Batch OCR Images – Kör igenkänning parallellt

Att bearbeta bilder en efter en är enkelt men långsamt. Genom att använda `Parallel.ForEach` kan vi **process multiple images** samtidigt och utnyttja fler‑kärniga CPU:er.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Varför parallellt?* Varje OCR‑anrop är CPU‑intensivt men oberoende, så att köra dem samtidigt kan kraftigt minska den totala körtiden, särskilt på en maskin med 4‑kärnor eller mer.

## Steg 4: Process Multiple Images – Visa den extraherade texten

Nu när vi har en samling av `OcrResult`‑objekt kan vi iterera över dem och skriva ut den igenkända texten. Detta är stället där du normalt skulle lagra resultatet i en databas eller skriva till filer, men konsolutskrift håller exemplet kortfattat.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Förväntad konsolutskrift (exempel):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Om någon bild misslyckas att läsas in kastar Aspose ett undantag; du kan omsluta anropet `engine.Recognize` i ett try/catch‑block för att logga fel utan att avbryta hela batchen.

## Steg 5: Full Working Example – Alla delar tillsammans

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt C#‑konsolprojekt. Det innehåller allt från `using`‑satserna till den sista utskriftsloopen.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Köra exemplet

1. Skapa ett nytt **Console App**‑projekt i Visual Studio.  
2. Lägg till **Aspose.OCR**‑NuGet‑paketet (`Install-Package Aspose.OCR`).  
3. Ersätt `YOUR_DIRECTORY` med sökvägen som innehåller dina PNG‑filer.  
4. Bygg och kör – du bör se den extraherade texten skriven till konsolen.

## Pro‑tips & specialfall

- **GPU acceleration:** Om du har ett kompatibelt GPU och en licensierad Aspose OCR, aktivera det via `EngineSettings` innan du skapar motorn. Detta kan spara sekunder per bild.  
- **Large files:** För bilder större än 10 MB, överväg att skala ner dem först för att minska minnesbelastningen.  
- **Language support:** Som standard antar motorn engelska. Sätt `engine.Language = Language.French;` (eller något annat stödjert språk) för att förbättra noggrannheten på icke‑engelsk text.  
- **Error handling:** `try/catch`‑blocket i den parallella loopen säkerställer att en korrupt fil inte avbryter hela batchen. Du kan också logga misslyckanden till en fil för senare granskning.  
- **Result storage:** Istället för att skriva ut kan du skriva `result.Text` till en `.txt`‑fil med `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Slutsats

Du vet nu **how to use OCR** i C# för att **extract text PNG**‑filer, **batch OCR images**, och **process multiple images** effektivt med Aspose OCR C#. Lösningen är helt självständig, körs parallellt och kan utökas för att hantera hundratals eller tusentals filer med minimala förändringar.

Redo för nästa steg? Prova att byta ut konsolutskriften mot en CSV‑rapport, experimentera med GPU‑acceleration, eller mata OCR‑texten till ett sökindex. Möjligheterna är oändliga, och huvudmönstret – initiera en gång, kör parallellt, hantera fel på ett smidigt sätt – kommer att tjäna dig väl i alla bild‑bearbetningspipelines.

Lycka till med kodandet, och må dina OCR‑jobb vara snabba och felfria!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}