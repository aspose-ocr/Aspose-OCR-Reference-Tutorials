---
category: general
date: 2026-05-25
description: Konvertera TIFF till text med Aspose.OCR i C#. Lär dig batchkonvertering
  av bilder till text och extrahera text från TIFF‑filer effektivt.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: sv
og_description: Konvertera TIFF till text med Aspose.OCR. Denna guide visar batchkonvertering
  av bild till text och hur du extraherar text från TIFF-filer i några få rader C#.
og_title: Konvertera TIFF till text i C# – Komplett batch‑OCR‑guide
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Konvertera TIFF till text i C# – Komplett batch‑OCR‑guide
url: /sv/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera TIFF till text i C# – Komplett batch-OCR-guide

Har du någonsin behövt **konvertera TIFF till text** men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på problem med batch-OCR när de hanterar skannade dokument. I den här handledningen går vi igenom en praktisk lösning som **extraherar text från TIFF**‑filer med Aspose.OCR, och vi gör det parallellt så att stora mappar blir klara på sekunder.

Vi kommer också att beröra bästa praxis för **batch bild‑till‑text‑konvertering**, så att du i slutet har ett återanvändbart kodsnutt som omvandlar en hel katalog med skannade bilder till prydliga *.txt*-filer—perfekt för indexering, sökning eller för att mata in i efterföljande analyser.

## Vad du behöver

- **.NET 6.0** eller senare (koden kompileras även på .NET Framework)  
- **Aspose.OCR for .NET** NuGet‑paket (`Install-Package Aspose.OCR`)  
- En mapp som innehåller en eller flera *.tif*-filer (det klassiska TIFF‑skanningsformatet)  
- Din favorit‑IDE (Visual Studio, VS Code, Rider—vad du än föredrar)

Det är allt. Inga externa tjänster, inga API‑nycklar, bara ren C# och Aspose.

![Skärmbild av en TIFF‑fil som bearbetas och den resulterande textfilen](/images/ocr-result.png "OCR‑resultat som visar konverterad TIFF till text‑utdata")

*(Alt‑text: Skärmbild som visar konverterad TIFF till text‑utdata på skärmen)*

## Steg 1: Ställ in OCR‑motorn – Konvertera TIFF till text

Först och främst behöver vi en `OcrEngine`‑instans som vet att den ska läsa engelska tecken. Motorn är hjärtat i konverteringen; att konfigurera den korrekt säkerställer pålitliga resultat.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Varför detta är viktigt:*  
Aspose.OCR stöder dussintals språk. Om du hanterar flerspråkiga skanningar, ändra helt enkelt `OcrLanguage.English` till rätt enum‑värde. Att låta språket vara odefinierat tvingar motorn till auto‑detekteringsläge, vilket kan vara långsammare och mindre exakt.

## Steg 2: Samla alla TIFF‑filer – Extrahera text från TIFF effektivt

Nästa steg hämtar varje *.tif*-fil från en mapp du anger. Genom att använda `Directory.GetFiles` får vi en ren array som vi kan skicka till batch‑processorn.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Pro‑tips:* Flaggan `SearchOption.AllDirectories` kan användas om dina skanningar ligger i undermappar. Kom bara ihåg att djupare rekursion kan öka minnesanvändningen under batch‑steget.

## Steg 3: Utför parallell OCR – Batch bild‑till‑text‑konvertering

Nu kommer den roliga delen. Aspose.OCR levereras med en statisk hjälpfunktion `BatchOcr.RecognizeAll` som accepterar en array av filsökvägar, en motor och ett `parallelism`‑tips. Vi startar fyra trådar, vilket på en modern quad‑core‑laptop ger nästan linjär hastighetsökning.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Varför parallellism?*  
Att skanna en batch med högupplösta TIFF‑filer kan vara CPU‑intensivt. Genom att fördela arbetet över flera trådar håller vi alla kärnor upptagna, vilket kraftigt minskar total körtid. Om du kör detta på en server med fler kärnor, öka `parallelism`‑värdet därefter.

## Steg 4: Skriv utdata – Konvertera skannade bild‑TXT‑filer

Till sist loopar vi igenom ordboken och skriver varje textstycke till en *.txt*-fil som har samma grundnamn som originalet. Detta är ögonblicket då **convert scanned images txt** blir verklighet.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Vad koden gör, på enkel svenska

1. **Skapa** en OCR‑motor inställd på engelska.  
2. **Samla** varje TIFF‑fil från mål‑mappen.  
3. **Kör** `BatchOcr.RecognizeAll` med fyra trådar, vilket omvandlar varje bild till en sträng.  
4. **Loop** över resultaten, byter `.tif`‑ändelsen till `.txt` och skriver strängen till disk.

Det är hela **convert TIFF to text**‑arbetsflödet på under 50 kodrader.

## Hantera kantfall – När saker inte går smidigt

- **Saknade eller korrupta TIFF‑filer** – `BatchOcr` kastar ett `OcrException`. Omge anropet med ett `try / catch` om du behöver en mjuk nedtrappning.  
- **Icke‑engelska dokument** – ändra `OcrLanguage.English` till `OcrLanguage.Spanish`, `OcrLanguage.French` osv., eller använd `OcrLanguage.AutoDetect`.  
- **Mycket stora bilder** – överväg att sänka DPI innan OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) för att spara minne, även om du kan förlora lite noggrannhet.  
- **Utdata‑kodning** – om du behöver en specifik kodsida (t.ex. Windows‑1252), skicka den till `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Pro‑tips för robusta batch‑konverteringar

- **Logga fel**: skapa en `List<string> failedFiles` och lägg till varje fil som kastar ett undantag; skriv listan till en logg efter loopen.  
- **Återanvänd motorn**: samma `OcrEngine`‑instans kan återanvändas för många filer; skapa den inte i loopen.  
- **Validera resultatet**: en snabb `if (string.IsNullOrWhiteSpace(extractedText))` kan flagga skanningar som var tomma eller oläsliga.  
- **Kombinera med PDF**: om din källa är en flersidig PDF, konvertera varje sida till TIFF först (Aspose.PDF gör det) och kör sedan denna batch.

## Nästa steg – Gå bortom enkel konvertering

Nu när du kan **extrahera text från TIFF**‑filer i bulk, kanske du vill:

- Mata *.txt*-filerna i ett sökindex (Elasticsearch, Azure Cognitive Search).  
- Köra språkdetection på varje resultat för att dirigera dokument till lokalspecifika pipelines.  
- Generera sökbara PDF‑filer genom att lägga OCR‑texten över de ursprungliga bilderna (Aspose.PDF igen).

Alla dessa scenarier bygger på samma grundidé: **batch image to text conversion** är en byggsten för större dokument‑bearbetningssystem.

---

### Slutsats

Du har precis lärt dig hur du **konverterar TIFF till text** med Aspose.OCR, bearbetar en hel mapp parallellt och sparar varje resultat som en ren *.txt*-fil. Lösningen är lättviktig, fullt konfigurerbar och klar för produktion—oavsett om du digitaliserar äldre fakturor, arkiverar skannade kontrakt eller driver en textsökmotor.

Prova den, justera parallellismen, och börja mata in de nygenererade textfilerna i vilket arbetsflöde du än behöver. Lycka till med OCR!

---

## Relaterade handledningar

- [Extrahera text från bilder med OCR‑operation på mappar](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}