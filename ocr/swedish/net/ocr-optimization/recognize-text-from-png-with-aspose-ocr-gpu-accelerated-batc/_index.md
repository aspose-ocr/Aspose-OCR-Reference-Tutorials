---
category: general
date: 2026-04-01
description: Lär dig att snabbt känna igen text från png‑filer genom att ange GPU‑enhets‑ID
  och aktivera GPU‑acceleration i Aspose OCR. Steg‑för‑steg C#‑guide.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: sv
og_description: Igenkänn text från PNG-filer snabbt genom att ange GPU-enhetens ID.
  Följ den här kompletta C#‑guiden för att aktivera GPU‑acceleration med Aspose OCR.
og_title: igenkänn text från png – GPU‑accelererad Aspose OCR‑handledning
tags:
- C#
- OCR
- GPU
- Aspose
title: igenkänn text från png med Aspose OCR – GPU‑accelererad batchdemo
url: /sv/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# känna igen text från png – Full C# GPU‑Accelererad Batch‑handledning

Har du någonsin behövt **känna igen text från png**‑bilder men upptäckt att processen är fruktansvärt långsam? Du är inte ensam. De flesta utvecklare börjar med ett enkelt OCR‑anrop, för att sedan stirra på en konsol som kryper som en snigel när en mapp innehåller dussintals skärmdumpar.  

Den goda nyheten? Aspose OCR kan avlasta det tunga arbetet till ditt grafikkort, och med bara ett par rader kan du **set gpu device id** för att välja exakt det GPU du vill använda. I den här guiden går vi igenom ett komplett, körbart exempel som hämtar alla PNG‑filer från en mapp, slår på GPU‑acceleration, väljer det första GPU‑tillståndet och skriver ut teckenantalet för varje fil.

När du är klar har du ett självständigt program som du kan slänga in i vilket .NET‑projekt som helst, och du förstår varför GPU‑aktivering är viktig, hur du hanterar kantfall och vad du kan justera för ännu bättre prestanda.

## Vad du behöver

- **.NET 6.0** eller senare (koden kompileras även med .NET Core).  
- **Aspose.OCR**‑NuGet‑paketet – installera det med `dotnet add package Aspose.OCR`.  
- En maskin med ett CUDA‑kompatibelt GPU (NVIDIA är vanligast) och rätt drivrutin.  
- En mapp full av **PNG**‑bilder som du vill bearbeta.  

Om någon av dessa punkter låter obekant, panikera inte. Stegen nedan innehåller exakt de kommandon du behöver, och vi diskuterar också vad du ska göra när ett GPU‑kort saknas.

## Steg 1: Initiera OCR‑motorn och aktivera GPU‑acceleration  

Det första du måste göra är att skapa en `OcrEngine`‑instans och slå på GPU‑stöd. Denna flagga talar om för Aspose att använda de inbyggda CUDA‑biblioteken under huven.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Varför detta är viktigt:** Utan `UseGpuAcceleration` bearbetas varje bild på CPU:n, vilket kan vara flera storleksordningar långsammare, särskilt för högupplösta PNG‑filer. Att slå på flaggan förbereder också motorn för att senare acceptera en specifik GPU‑enhet.

## Steg 2: Ange GPU‑enhets‑ID (valfritt men rekommenderat)  

Om din arbetsstation har mer än ett GPU kan du bestämma vilket du vill använda. Enhets‑ID:n börjar på **0**, så `0` väljer det första GPU‑tillståndet, `1` det andra och så vidare.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Proffstips:** När du kör på en delad server kan ett explicit angivet GPU‑enhets‑ID förhindra att ditt jobb tar resurser från andra processer. Om du utelämnar den här raden väljer Aspose standard‑enheten, vilket vanligtvis är okej för en enkel‑GPU‑konfiguration.

## Steg 3: Samla alla PNG‑filer från din batch‑mapp  

Nästa steg är att lokalisera varje PNG du vill köra OCR på. Metoden `Directory.GetFiles` gör det tunga arbetet.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Kantfall:** Om mappen är tom blir `imageFiles` en tom array. Det hanterar vi senare med ett vänligt meddelande.

## Steg 4: Bearbeta varje bild och skriv ut det igenkända teckenantalet  

Nu kommer huvudloopen. För varje PNG anropar vi `Recognize` och skriver sedan ut filnamnet samt längden på den extraherade texten.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Vad du kommer att se:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Om en bild inte innehåller någon text blir räknaren `0`. Det är helt normalt för skärmdumpar som bara är grafiska.

## Steg 5: Kör programmet och verifiera GPU‑användning  

Kompilera filen (`dotnet build`) och kör den (`dotnet run`). Medan konsolen scrollar kan du öppna ditt GPU‑övervakningsverktyg (t.ex. NVIDIA Smi) för att se GPU‑utnyttjandet kortvarigt öka för varje bild. Om du inte ser någon aktivitet, dubbelkolla att:

1. CUDA‑drivrutinen är installerad.  
2. `UseGpuAcceleration` är satt till `true`.  
3. Det korrekta `GpuDeviceId` matchar ett fysiskt GPU.

Om GPU‑enheten inte är tillgänglig faller Aspose automatiskt tillbaka till CPU, men du förlorar hastighetsfördelen.

## Vanliga variationer & tips  

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Annat bildformat** (t.ex. JPEG) | Ändra sökmönstret till `*.jpg` eller `*.*` så kommer Aspose fortfarande att känna igen texten. |
| **Batch‑storleken är enorm** (tusentals filer) | Bearbeta i omgångar för att undvika minnespress: dela `imageFiles` i mindre arrayer. |
| **Behöver den faktiska texten, inte bara längden** | Byt ut `ocrResult.Text.Length` mot `ocrResult.Text` i `WriteLine`. |
| **Kör på en huvudlös server** | Säkerställ att servern har en GPU‑drivrutin; annars sätt `UseGpuAcceleration = false` för att undvika onödiga fel. |
| **Flera GPU‑enheter, vill balansera belastning** | Loopa över `ocrEngine.GpuDeviceId = i % gpuCount` inuti `foreach` för att rotera enheter. |

## Förväntad output & verifiering  

När allt fungerar skriver konsolen ut varje filnamn följt av teckenantalet, precis som visat tidigare. För att dubbelkolla själva OCR‑resultatet kan du tillfälligt dumpa texten:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Kom bara ihåg att ta bort eller kommentera den raden för stora batcher; att skriva ut tusentals rader kan översvämma din terminal.

## Fullt fungerande exempel (Kopiera‑klistra‑redo)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Spara detta som `GpuBatchDemo.cs`, kör `dotnet add package Aspose.OCR` och sedan `dotnet run`. Du bör se teckenantalet visas nästan omedelbart för varje PNG, tack vare GPU‑acceleration.

## Slutsats  

Du vet nu hur du **känner igen text från png**‑filer effektivt genom att aktivera GPU‑acceleration och explicit **set gpu device id** i Aspose OCR. Det kompletta, kopiera‑och‑klistra‑programmet hanterar mappupptäckt, kantfalls‑kontroller och ger dig omedelbar återkoppling på OCR‑prestanda.  

Nästa steg? Prova att byta ut `Recognize`‑anropet mot `ocrEngine.RecognizeAsync` om du behöver icke‑blockerande bearbetning, eller experimentera med olika bild‑förbehandlingsalternativ (t.ex. binarisering) som Aspose erbjuder. Du kan också skicka OCR‑resultaten till en databas eller ett sökindex för en fulltextsökning.

Har du frågor om hantering av flersidiga PDF‑filer, eller vill du jämföra Aspose OCR med Tesseract? Lämna en kommentar eller utforska våra andra handledningar om **batch OCR C#**, **OCR‑prestandatips** och **GPU‑driven bildbehandling**. Lycka till med kodningen!  

![Konsolutdata som visar igenkända teckenantal för PNG‑filer – känna igen text från png med GPU‑acceleration](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}