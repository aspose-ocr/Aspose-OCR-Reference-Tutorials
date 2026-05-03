---
category: general
date: 2026-05-02
description: Begränsa GPU‑minnesanvändning när du kör OCR på en bild i C#. Lär dig
  hur du aktiverar GPU‑acceleration, extraherar text från ett kvitto och behärskar
  en C#‑OCR‑handledning.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: sv
og_description: Begränsa GPU‑minnesanvändning när du kör OCR på en bild i C#. Denna
  guide visar hur du aktiverar GPU‑acceleration, extraherar text från ett kvitto och
  behärskar en C# OCR‑handledning.
og_title: Begränsa GPU‑minnesanvändning i C# OCR – Komplett guide
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Begränsa GPU‑minnesanvändning i C# OCR – Komplett guide
url: /sv/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# begränsa gpu-minnesanvändning i C# OCR – komplett guide

Har du någonsin behövt **begränsa GPU‑minnesanvändning** när du bearbetar en batch med kvitton? Du är inte ensam – utvecklare får ofta minnes‑out‑of‑error när GPU:n får jonglera för många bilder samtidigt. Den goda nyheten är att Aspose.OCR låter dig sätta en gräns för minnesavtrycket **och** starta GPU‑acceleration med en enda kodrad.  

I den här handledningen går vi igenom en praktisk, steg‑för‑steg‑lösning som visar **hur man aktiverar GPU‑acceleration**, hämtar text från ett exempel‑kvittobild och håller GPU‑RAM‑användningen under en prydlig 1 GB. I slutet har du en färdig‑att‑köra C#‑konsolapp samt ett antal tips du kan återanvända i alla **kör OCR på bild**‑scenarier.

## Vad du behöver

- .NET 6.0 SDK eller senare (koden kompilerar även med .NET 5+)  
- Aspose.OCR för .NET NuGet‑paket (`Aspose.OCR`) – installera med `dotnet add package Aspose.OCR`  
- Ett CUDA‑kompatibelt GPU eller en DirectML‑kompatibel Windows‑enhet  
- En exempel‑kvittobild (`receipt.jpg`) placerad i en mapp du kan referera till  

Det är allt – inga extra native‑bibliotek, inga krångliga DLL‑kopior. Aspose abstraherar GPU‑backend, så du kan fokusera på din affärslogik.

## Steg 1: Installera Aspose.OCR NuGet‑paketet

Först och främst. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Det hämtar den senaste stabila versionen (från och med maj 2026 är det 23.11). Paketet innehåller både CPU‑ och GPU‑binärer, så du behöver inte manuellt ladda ner CUDA‑ eller DirectML‑runtime – Aspose upptäcker vad som finns tillgängligt vid körning.

> **Pro tip:** Om du riktar in dig på en CI/CD‑pipeline, lås versionen i din `.csproj` för att undvika oväntade uppgraderingar.

## Steg 2: Skapa OCR‑motorn och **begränsa GPU‑minnesanvändning**

Nu ska vi instansiera `OcrEngine` och explicit säga åt den att inte överskrida 1 GB GPU‑minne. Detta är kärnan i kravet **begränsa GPU‑minnesanvändning**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

Lägg märke till kommentaren `// 👉 Limit GPU memory usage…` – den raden är svaret på huvudnyckelordet. Genom att sätta `GpuMemoryLimitMb` talar du om för den underliggande inferensmotorn att allokera högst den angivna mängden, vilket möjliggör flera samtidiga jobb utan att överbelasta GPU:n.

## Steg 3: **Hur man aktiverar GPU‑acceleration** (och varför det är viktigt)

Du kanske undrar: “Varför inte bara hålla fast vid CPU:n?” Svaret är hastighet. På ett modernt RTX 3080 bearbetas samma kvitto på under 200 ms jämfört med 1,2 sekunder på en 4‑kärnig CPU.  

Att aktivera GPU‑acceleration är så enkelt som att växla `EngineMode`‑enumen:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose väljer automatiskt den bästa backend‑lösningen:

| Upptäckt backend | Vad den gör |
|------------------|--------------|
| CUDA (NVIDIA)    | Använder cuDNN‑kärnor för OCR, bäst för Windows/Linux med NVIDIA‑kort |
| DirectML (Windows) | Utnyttjar DirectX 12, fungerar på AMD/Intel‑GPU:er utan extra drivrutiner |
| None (fallback)  | Faller tillbaka till en optimerad CPU‑väg |

Om varken CUDA eller DirectML finns, återgår motorn tyst till CPU – ingen krasch, bara långsammare prestanda.

## Steg 4: **Kör OCR på bild** och **extrahera text från kvitto**

Med motorn konfigurerad är det enkelt att mata in en bild. Metoden `RecognizeImage` accepterar en filsökväg, en `Stream` eller till och med en `Bitmap`. Här är det minsta anropet:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

Förutsatt att kvittot innehåller:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Bör du se en utskrift liknande:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Om texten ser förvrängd ut, kontrollera att bilden har hög kontrast och är korrekt orienterad – OCR älskar rena skanningar.

## Steg 5: Verifiera minnesgränser och hantera kantfall

Efter första körningen kan du fråga hur mycket GPU‑minne motorn faktiskt använde:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

Planerar du att bearbeta dussintals kvitton parallellt kan du vilja sänka gränsen till 512 MB och köra flera motorinstanser. Kom bara ihåg att varje instans respekterar samma globala tak; biblioteket kommer automatiskt att strypa allokeringar.

> **Vanligt fallgropp:** Att sätta gränsen för lågt (t.ex. 100 MB) kan få motorn att byta till CPU mitt i körningen, vilket leder till inkonsekvent prestanda. Testa med en realistisk arbetsbelastning innan du låser värdet.

## Fullt fungerande exempel

Nedan finns ett komplett, copy‑paste‑klart konsolprogram. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen till din kvittobild.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

Spara filen, kör `dotnet run`, och du bör se den extraherade kvittotexten skriven till konsolen, tillsammans med en liten rapport om GPU‑minnesförbrukning.

## Felsökning & FAQ

**Q: Mitt GPU upptäcks inte – varför?**  
A: Säkerställ att den senaste NVIDIA‑drivrutinen (för CUDA) eller Windows 10 1809+ (för DirectML) är installerad. Verifiera också att `Aspose.OCR`‑DLL:arna matchar din processarkitektur (x64 rekommenderas).

**Q: Utdata är tom.**  
A: Kontrollera bildkvaliteten – suddiga eller roterade kvitton kräver ofta förbehandling (deskew, binarisering). Aspose erbjuder `ImagePreprocessor` som du kan koppla in före `RecognizeImage`.

**Q: Kan jag köra detta på Linux?**  
A: Ja, så länge du har ett NVIDIA‑GPU med CUDA 11+ installerat. Samma kod fungerar oförändrad.

## Slutsats

Vi har gått igenom allt du behöver för att **begränsa GPU‑minnesanvändning** medan du **kör OCR på bild** med Aspose.OCR i C#. Från installation av NuGet‑paketet till konfiguration av motorn, aktivering av GPU‑acceleration och slutligen **extrahera text från kvitto**, ger guiden dig en färdig lösning som är både minnesvänlig och blixtsnabb.

Nästa steg kan vara att utforska mer avancerade **c# OCR tutorial**‑ämnen – som batch‑bearbetning, egna språkpaket eller att integrera resultaten i en databas. Experimentera med olika `GpuMemoryLimitMb`‑värden för att hitta den optimala balansen för din arbetsbelastning, och håll ett öga på diagnostiken för minnesanvändning för att undvika överraskningar.

Lycka till med kodningen, och må ditt GPU hålla sig svalt medan ditt OCR förblir skarpt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}