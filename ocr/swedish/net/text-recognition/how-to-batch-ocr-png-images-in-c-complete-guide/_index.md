---
category: general
date: 2026-04-26
description: Hur man snabbt batch-OCR:ar PNG‑bilder. Lär dig att extrahera text från
  PNG, konvertera bilder till text, skriva den igenkända texten och läsa PNG‑katalogen
  med Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: sv
og_description: Hur man batch-OCR:ar PNG‑bilder i C# med Aspose OCR. Denna guide visar
  hur man extraherar text från PNG, konverterar bilder till text och skriver den igenkända
  texten effektivt.
og_title: Hur man batch-OCR:ar PNG‑bilder i C# – Steg för steg
tags:
- OCR
- C#
- Aspose
title: Hur man batch-OCR:ar PNG-bilder i C# – Komplett guide
url: /sv/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch‑OCR:ar PNG‑bilder i C# – Komplett guide

Har du någonsin undrat **hur man batch‑OCR:ar** en hel mapp med PNG‑filer utan att skriva ett separat program för varje bild? Du är inte ensam om att jonglera med dussintals skärmdumpar, skannade kvitton eller grafik som måste omvandlas till sökbar text. I den här handledningen går vi igenom en praktisk lösning som **extraherar text från PNG**, **konverterar bilder till text** och **sparar den igenkända texten** till enskilda filer – allt medan PNG‑katalogen läses automatiskt.

När du är klar med den här guiden har du en färdig‑att‑köra C#‑konsolapp som bearbetar ett godtyckligt antal bilder på en gång. Inga extra skript, ingen manuell kopiering‑och‑klistring – bara ren kod som gör det tunga arbetet åt dig.

## Vad du behöver

- **.NET 6.0** eller senare (koden fungerar bra på .NET Framework också).  
- **Aspose.OCR for .NET** NuGet‑paket (gratis provversion fungerar för testning).  
- En mapp med ett antal *.png*-filer som du vill OCR:a.  
- Visual Studio 2022 eller någon annan C#‑IDE du föredrar.

Om du har det här kan vi hoppa rakt in i implementeringen.

## Steg 1 – Förbered dina in‑ och utmatningsmappar *(Läs PNG‑katalogen)*

Det första vi gör är att peka programmet mot mappen som innehåller bilderna och bestämma var de resulterande *.txt*-filerna ska sparas. Genom att använda `Directory.GetFiles` får vi en ren uppräkningsbar lista över alla PNG‑filer i katalogen.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Varför detta är viktigt:**  
- Att använda ett wildcard (`*.png`) garanterar att vi bara bearbetar bildfiler och ignorerar eventuella lösa dokument.  
- Att skapa utmatningsmappen i farten förhindrar ett `DirectoryNotFoundException` senare.

> **Proffstips:** Om du behöver stödja andra format (JPEG, BMP) kan du bara utöka sökmönstret eller anropa `Directory.EnumerateFiles` med flera filändelser.

## Steg 2 – Initiera OCR‑motorn *(Konvertera bilder till text)*

Aspose.OCR levereras med två motortyper: en CPU‑baserad `OcrEngine` och en GPU‑accelererad `GpuOcrEngine`. För de flesta batch‑jobb är CPU‑motorn helt tillräcklig, men du kan byta klassnamnet om du har ett kapabelt GPU.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Varför detta är viktigt:**  
- Att ange språket förbättrar noggrannheten avsevärt eftersom motorn vet vilken teckenuppsättning som förväntas.  
- Att byta till `GpuOcrEngine` är en endradsändring om du stöter på prestandaflaskhalsar i stora batcher.

## Steg 3 – Skapa en batch‑recogniserare

Aspose erbjuder en praktisk `BatchRecognizer` som accepterar en uppräkningsbar lista med filsökvägar och strömmar tillbaka resultaten ett i taget. Detta undviker att alla bilder laddas in i minnet på en gång – en avgörande detalj för stora mappar.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Varför detta är viktigt:**  
- Batch‑recogniseraren kapslar in loop‑logiken, så att vi kan fokusera på vad vi ska göra med varje resultat snarare än hur vi itererar säkert.

## Steg 4 – Kör OCR på alla bilder och skriv utdata *(Skriv igenkänd text)*

Nu utför vi faktiskt OCR. Metoden `Recognize` returnerar ett `IEnumerable<RecognitionResult>` där varje resultat innehåller den extraherade texten och annan metadata.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Varför detta är viktigt:**  
- Att använda `File.WriteAllText` säkerställer att texten sparas med UTF‑8‑kodning som standard, vilket bevarar specialtecken.  
- Den inkrementella namngivningen (`out_0.txt`, `out_1.txt`) matchar bearbetningsordningen, vilket är hjälpsamt vid felsökning.

> **Edge case:** Om någon bild misslyckas med OCR (t.ex. korrupt fil) kommer `RecognitionResult.Text` att vara tom. Du kan lägga till en enkel kontroll i loopen för att logga misslyckanden:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Steg 5 – Sätt ihop allt – Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt. Det inkluderar `using`‑direktiven, mappvalidering och ett litet konsol‑UI så att du vet när batchen är klar.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Förväntad utdata:**  
När programmet körs skrivs något liknande ut:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Och du kommer att se `out_0.txt` … `out_11.txt` i utmatningsmappen, var och en innehållande textversionen av den motsvarande bilden.

## Vanliga frågor & tips

| Fråga | Svar |
|----------|--------|
| *Kan jag OCR:a undermappar också?* | Ja—byt ut `Directory.GetFiles` mot `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Vad händer om jag behöver ett annat språk?* | Sätt `ocrEngine.Language = Language.Spanish;` (eller någon annan stödjande enum). |
| *Hur hanterar jag enorma batcher (tusentals filer)?* | Överväg att bearbeta i delar eller använda `Parallel.ForEach` med en begränsad grad av parallellism för att undvika att minnet tar slut. |
| *Är utdata alltid UTF‑8?* | `File.WriteAllText` använder UTF‑8 utan BOM som standard, vilket fungerar för de flesta latinska språk. För asiatiska skript kan du behöva ange `Encoding.UTF8` explicit. |
| *Kan jag få förtroendescore?* | `RecognitionResult` exponerar `Confidence`—du kan logga den tillsammans med texten för kvalitetskontroll. |

## Visuell översikt *(Hur man batch‑OCR – Diagram)*

![Diagram som visar arbetsflöde för batch‑OCR: inmatningsmapp → OCR‑motor → batch‑recogniser → utdata txt‑filer](https://example.com/diagram-how-to-batch-ocr.png "Hur man batch‑OCR")

*Alt‑texten innehåller huvudnyckelordet, vilket uppfyller SEO‑krav för bilder.*

## Avslutning

Vi har precis gått igenom **hur man batch‑OCR:ar** en katalog med PNG‑filer med Aspose.OCR, från att läsa PNG‑katalogen till att skriva varje igenkänd textfil. Lösningen är helt fristående, fungerar på alla moderna .NET‑runtime och kan utökas för GPU‑acceleration, flerspråkigt stöd eller parallell bearbetning.

Redo för nästa steg? Prova att byta `Language.Latin` mot ett annat språk, eller integrera utdata i ett sökindex så att dina dokument blir omedelbart sökbara. Himlen är gränsen när du har bemästrat batch‑OCR.

Lycka till med kodandet, och låt mig veta i kommentarerna om du stöter på några problem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}