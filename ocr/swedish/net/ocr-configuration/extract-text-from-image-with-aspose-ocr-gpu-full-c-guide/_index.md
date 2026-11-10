---
category: general
date: 2026-04-06
description: Extrahera text från bild med Aspose OCR GPU i C#. Lär dig att läsa in
  en bild från fil och ställa in GPU‑minnesgränsen i den här steg‑för‑steg‑guiden.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: sv
og_description: Extrahera text från bild med Aspose OCR GPU i C#. Lär dig att läsa
  in en bild från fil och ställa in GPU‑minnesgränsen i den här steg‑för‑steg‑guiden.
og_title: Extrahera text från bild med Aspose OCR GPU – Fullständig C#‑guide
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Extrahera text från bild med Aspose OCR GPU – Fullständig C#‑guide
url: /sv/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med Aspose OCR GPU – Fullständig C#‑guide

Har du någonsin behövt **extrahera text från bild** men känt dig fast när prestanda blev avgörande? Du är inte ensam—många utvecklare stöter på samma hinder när OCR blir en flaskhals. I den här handledningen visar vi exakt hur du extraherar text från bild med Aspose OCR:s GPU‑runtime, laddar bild från fil och till och med sätter en GPU‑minnesgräns för striktare resurskontroll.

Vi går igenom ett komplett, färdigt‑att‑köra C#‑exempel, förklarar varför varje rad är viktig och pekar på vanliga fallgropar du kan stöta på. När du är klar har du en solid grund för att bygga snabba, skalbara OCR‑pipelines som körs på GPU:n.

## Vad den här guiden täcker

- **Förutsättningar**: .NET 6+ (eller .NET Framework 4.6+), Aspose.OCR NuGet‑paket, en kompatibel GPU‑drivrutin.
- **Steg‑för‑steg‑kod** som laddar en bild från fil, konfigurerar Aspose OCR GPU‑motor och extraherar text.
- **Varför** du kanske vill sätta en GPU‑minnesgräns och hur du gör det på ett säkert sätt.
- **Hantering av kantfall**: lågupplösta bilder, saknad GPU och felsökning av förtroendescore.
- **Nästa steg**: batch‑bearbetning, integration med ASP.NET Core och återgång till CPU om det behövs.

> **Proffstips:** Om du är osäker på om din GPU används, kontrollera GPU‑aktivitetsmonitoren (t.ex. NVIDIA‑SMI) medan OCR körs. Du kommer att se en topp i minnesanvändning som matchar den gräns du satt.

---

![Diagram som visar flödet för att extrahera text från bild med Aspose OCR GPU-motorn](extract-text-from-image-aspose-ocr-gpu.png "extrahera text från bild med Aspose OCR GPU")

## Steg 1: Initiera Aspose OCR‑motorn för GPU‑bearbetning

Det första du behöver är en `OcrEngine`‑instans som vet att den ska köras på GPU:n. Aspose tillhandahåller ett rent `OcrEngineSettings`‑objekt där du kan specificera runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Varför detta är viktigt:** Som standard faller Aspose OCR tillbaka till CPU, vilket är okej för små bilder men kan vara fruktansvärt långsamt för högupplösta foton. Genom att explicit sätta `Runtime = OcrRuntime.Gpu` flyttas det tunga arbetet till grafikkortet, vilket ger en märkbar hastighetsökning.

## Steg 2: (Valfritt) Sätt en GPU‑minnesgräns

Om du kör på en delad arbetsstation eller i en container med begränsade GPU‑resurser kan du begränsa hur mycket minne OCR‑motorn får använda. Detta förhindrar minnesutmatningskrascher och håller andra processer nöjda.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**När du bör använda det:**  
- **Multi‑tenant‑miljöer** där flera tjänster delar samma GPU.  
- **CI/CD‑pipelines** som allokerar en fast mängd GPU‑minne per jobb.  

Om du utelämnar den här raden kommer Aspose att använda så mycket minne som behövs, vilket är okej på en dedikerad arbetsstation.

## Steg 3: Ladda bild från fil

Nu måste vi föra in bilden i minnet. Aspose OCR arbetar med `System.Drawing.Image`, så vi använder `Image.FromFile`. Se till att sökvägen pekar på en riktig fil; annars kastas ett undantag.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Varför laddning från fil är viktigt:** Många utvecklare försöker mata in en byte‑array direkt, vilket fungerar men lägger till ett onödigt konverteringssteg. Att använda `Image.FromFile` är enkelt, och `using`‑satsen garanterar att filhandtaget frigörs omedelbart.

## Steg 4: Kör OCR och hämta resultatet

Med motorn konfigurerad och bilden laddad kan vi äntligen extrahera texten. Metoden `Recognize` returnerar ett `OcrResult` som innehåller både råtexten och ett förtroendepoäng.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Förståelse av output:**  
- `Confidence` är ett värde mellan 0 och 1. Ett förtroende på 0,95 (eller 95 %) betyder vanligtvis att OCR‑resultatet är prickfritt.  
- `Text` innehåller radbrytningar exakt som de visas i bilden, vilket är praktiskt för vidare bearbetning.

## Steg 5: Verifiera output och hantera kantfall

### Kontroll av förtroendenivåer

Om förtroendet sjunker under, säg, 80 % kan du vilja falla tillbaka till CPU‑bearbetning eller tillämpa bildförbehandling (t.ex. binarisering).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Hantera saknad GPU

Inte alla maskiner har en kompatibel GPU. Aspose kastar ett `OcrException` om den inte kan initiera GPU‑runtime.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Högupplösta bilder

Mycket stora bilder (t.ex. > 4000 px i bredd) kan förbruka mycket GPU‑minne. Om du når den gräns du satte tidigare kommer Aspose att avbryta bearbetningen. I sådana fall bör du först skala ner bilden:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt. Det innehåller alla stegen, felhantering och valfri fallback‑logik.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Förväntad output

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Om förtroendet faller under tröskeln kommer du att se de extra CPU‑fallback‑meddelandena.

---

## Slutsats

Du vet nu **hur du extraherar text från bild** med Aspose OCR:s GPU‑motor, **hur du laddar bild från fil**, och varför du kan vilja **sätta GPU‑minnesgräns** för produktionsarbetsbelastningar. Exemplet ovan är en fullt funktionell, citeringsvärd lösning som du kan släppa in i vilket .NET‑projekt som helst.

Vad blir nästa steg? Överväg:

- **Batch‑bearbetning**: loopa igenom en mapp med bilder och skriv resultat till en CSV.  
- **ASP.NET Core‑integration**: exponera en API‑endpoint som tar emot en uppladdad bild och returnerar OCR‑texten.  
- **Prestandatuning**: experimentera med olika `GpuMemoryLimit`‑värden och övervaka GPU‑användning för att hitta den optimala balansen.

Känn dig fri att anpassa koden till ditt eget scenario—oavsett om du bygger en dokument‑digitaliseringspipeline, en real‑time‑översättningsapp eller en kvittoskanningsservice. Grundprinciperna är desamma: initiera GPU‑motorn, hantera minnet klokt och verifiera alltid förtroendet.

Har du frågor eller stöter på ett problem? lämna en kommentar nedan så felsöker vi tillsammans. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}