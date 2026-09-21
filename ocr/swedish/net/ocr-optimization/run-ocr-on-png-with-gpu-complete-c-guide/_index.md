---
category: general
date: 2026-01-02
description: Kör OCR på PNG snabbt med Aspose OCR och GPU‑stöd. Lär dig hur du känner
  igen text från en bild, extraherar text från en bild och ställer in GPU‑minnesgränsen.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: sv
og_description: Kör OCR på PNG effektivt genom att utnyttja Aspose OCR och GPU-acceleration.
  Denna handledning visar hur du känner igen text från en bild, extraherar text från
  en bild och styr GPU-minnesanvändning.
og_title: Kör OCR på PNG med GPU – Komplett C#-guide
tags:
- OCR
- C#
- GPU
title: Kör OCR på PNG med GPU – Komplett C#‑guide
url: /sv/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på PNG med GPU – Komplett C#‑guide

Har du någonsin behövt **köra OCR på PNG**‑filer men känt dig fast vid prestandagränsen? Du är inte ensam. I många verkliga pipelines kan en enda högupplöst PNG begränsa en enbart CPU‑baserad OCR‑motor, vilket förvandlar vad som borde vara en snabb sökning till ett minutlångt väntande.

Den goda nyheten är att Aspose OCR levereras med GPU‑tillägg som låter dig **igenkänna text från bild**‑filer på en bråkdel av tiden. I den här handledningen går vi igenom ett praktiskt exempel som visar exakt hur du **kör OCR på PNG** med C#, hur du **extraherar text från bild**, och till och med hur du **sätter GPU‑minnesgräns** så att du håller dig inom din hårdvarubudget.

Vi kommer också att gå igenom “hur” och “varför” bakom varje steg, så att du får en solid mental modell – inte bara ett kopiera‑och‑klistra‑kodsnutt.

## Vad du kommer att lära dig

- Förutsättningarna för att använda Aspose OCR:s GPU‑stöd.  
- Hur du laddar en PNG i en `Bitmap` och matar den till OCR‑motorn.  
- Hur du konfigurerar `GpuDevice` och `GpuMemoryLimitMb` för optimal prestanda.  
- Hur du **igenkänner text från bild** och hämtar resultatet som ren text.  
- Tips för att hantera vanliga kantfall såsom GPU:er med lite minne eller flersidiga PNG‑filer.  

I slutet av den här guiden kommer du att kunna **köra OCR på PNG**‑filer med GPU‑hastighet och tryggt kontrollera minnesavtrycket för dina OCR‑jobb.

![Diagram som visar kör OCR på PNG med GPU‑acceleration](run-ocr-on-png-diagram.png "exempel på kör OCR på PNG")

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework).  
2. Ett NVIDIA‑GPU med CUDA‑stöd (exemplet väljer enhetsindex 0).  
3. Aspose.OCR NuGet‑paketet och dess GPU‑tillägg (`Aspose.OCR.Extensions`).  
4. En exempel‑PNG (`input.png`) placerad i en mapp som du kan referera till från ditt projekt.  

Om någon av dessa känns obekanta, oroa dig inte – vi kommer att notera alternativ där det är relevant.

---

## Steg 1 – Installera Aspose OCR och GPU‑tillägg

Först och främst. Utan rätt bibliotek kommer resten av koden inte att kompilera.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions`‑paketet hämtar de inhemska CUDA‑binärerna som krävs för GPU‑acceleration.  
*Proffstips:* Om du är på en maskin utan GPU kan du fortfarande kompilera projektet; bara sätt `PreferGpu = false` senare.

---

## Steg 2 – Ladda PNG‑filen du vill bearbeta

Nu **kör vi OCR på PNG** genom att ladda den i en `Bitmap`. Detta steg är enkelt men förtjänar en snabb notering: `Bitmap` förväntar sig en filsökväg, så se till att sökvägen är korrekt i förhållande till din körbara fil.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Om PNG‑filen är ovanligt stor (t.ex. > 5000 px på en sida) kan du vilja skala ner den först för att undvika att tömma GPU‑minnet. Det är där alternativet **sätt GPU‑minnesgräns** blir praktiskt senare.

---

## Steg 3 – Skapa och konfigurera OCR‑motorn för GPU‑användning

Här är kärnan i handledningen: att konfigurera OCR‑motorn för att **igenkänna text från bild** med GPU. Två egenskaper är nyckeln:

- `GpuDevice` – väljer vilken CUDA‑enhet som ska användas.  
- `GpuMemoryLimitMb` – begränsar mängden GPU‑minne som motorn kan allokera.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Varför sätta en minnesgräns?** Vissa GPU:er delar minne med skärmen eller kör flera arbetsbelastningar samtidigt. Genom att begränsa allokeringen förhindrar du minnesbrist‑krascher, särskilt när du bearbetar många PNG‑filer parallellt.

---

## Steg 4 – Definiera igenkänningsalternativ (språk & GPU‑preferens)

`RecognitionOptions`‑objektet talar om för motorn vilket språk den ska leta efter och om den ska **föredra GPU** även för små bilder. För de flesta engelska dokument är detta tillräckligt, men du kan byta `Language.English` mot andra stödjade språk.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Om du någonsin behöver **extrahera text från bild** på ett annat språk än engelska, byt bara `Language`‑enum. Biblioteket stödjer dussintals språk direkt.

---

## Steg 5 – Kör OCR och hämta resultatet

När allt är kopplat ihop är det sista anropet en enda rad som faktiskt **kör OCR på PNG** och returnerar ett rikt resultatobjekt.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` innehåller inte bara ren text (`ocrResult.Text`) utan även förtroendescore, avgränsningsrutor och till och med originalbilden med markerade ord – användbart om du behöver felsöka eller visualisera extraktionen.

**Förväntad output** (för en exempel‑PNG som säger “Hello World”):

```
=== OCR Output ===
Hello World
```

Om texten ser förvrängd ut, dubbelkolla att PNG‑filen inte är skadad och att GPU‑minnesgränsen inte är för låg för bildens storlek.

---

## Steg 6 – Hantera kantfall och bästa praxis‑tips

### GPU:er med lite minne

Om du får ett undantag som `CudaException: out of memory`, sänk `GpuMemoryLimitMb` eller dela upp PNG‑filen i rutor innan bearbetning. Tiling kan göras med `Graphics.DrawImage` på en `Bitmap`‑klon.

### Flera PNG‑filer i en batch

När du bearbetar en mapp med PNG‑filer, återanvänd samma `OcrEngine`‑instans – att initiera den en gång sparar GPU‑kontextbyten.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Fallback till CPU

Om en GPU inte är tillgänglig, sätt helt enkelt `PreferGpu = false`. Motorn kommer automatiskt att falla tillbaka till CPU utan några kodändringar.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt. Det inkluderar alla stegen ovan, samt några säkerhetskontroller.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spara filen som `Program.cs`, kör `dotnet run`, och du bör se den extraherade texten skrivas ut i konsolen.

---

## Slutsats

Vi har just demonstrerat hur man **kör OCR på PNG**‑filer med Aspose OCR:s GPU‑tillägg, hur man **igenkänner text från bild**, och hur man **extraherar text från bild** samtidigt som man styr **GPU‑minnesgränsen**. Genom att konfigurera `GpuDevice` och `GpuMemoryLimitMb` håller du din applikation snabb och stabil, även på modest GPU.

Från här kan du:

- Experimentera med andra språk (`Language.French`, `Language.Spanish`).  
- Integrera OCR‑steget i en större dokument‑bearbetningspipeline.  
- Lägg till efterbearbetning såsom stavningskontroll eller entitetsutvinning för att förfina den råa texten.  

Kom ihåg, nyckeln är inte bara koden utan att förstå varför varje inställning är viktig. När du vet hur du **sätter GPU‑minnesgräns** och när du ska falla tillbaka till CPU, kommer du att bygga OCR‑lösningar som skalar smidigt.

Har du frågor om en specifik PNG‑storlek, flersidiga TIFF‑filer eller felsökning av GPU‑fel? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}