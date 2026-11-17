---
category: general
date: 2026-03-13
description: Hur man batch‑OCR:ar snabbt och pålitligt samtidigt som man lär sig att
  extrahera text från tiff‑filer med Aspose.OCR. Följ den här steg‑för‑steg‑handledningen.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: sv
og_description: Lär dig hur du batchar OCR i C# och extraherar text från tiff‑filer
  med Aspose.OCR. Denna guide täcker installation, kod och bästa‑praxis‑tips.
og_title: Hur man batchar OCR i C# – Komplett programmeringsguide
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Hur man batchar OCR i C# – Komplett programmeringsguide
url: /sv/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch‑OCR:ar i C# – Komplett programmeringsguide

Har du någonsin undrat **hur man batch‑OCR:ar** en hög av skannade fakturor utan att skriva ett separat skript för varje fil? Du är inte ensam. I många verkliga projekt är smärtpunkten inte OCR‑noggrannheten i sig utan den enorma mängden bilder—ofta TIFF‑filer—som måste omvandlas till sökbar text.  

Denna handledning visar dig **hur man batch‑OCR:ar** med Aspose.OCR:s `BatchProcessor` samtidigt som du lär dig **extrahera text från tiff**‑filer i ett enda, rent körning. I slutet har du en färdig konsolapp som bearbetar en hel mapp, utnyttjar valfri GPU‑acceleration och sparar ren‑text‑resultat där du behöver dem.

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.7.2 om du föredrar den klassiska runtime‑miljön)  
- **Aspose.OCR for .NET** – du kan hämta NuGet‑paketet med `dotnet add package Aspose.OCR`.  
- En mapp med **TIFF**‑bilder du vill läsa (handledningen använder `Invoices` som exempel).  
- Valfritt: ett GPU som stödjer DirectX 11 eller CUDA om du vill snabba upp processen.  

Inga extra tjänster, inga moln‑nycklar—bara ett lokalt C#‑projekt och Aspose‑biblioteket.

## Steg 1: Skapa projektet och installera Aspose.OCR

Först, skapa en konsolapp.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Proffstips:** Om du kör på Windows och planerar att använda GPU‑acceleration, se till att den senaste grafikdrivrutinen är installerad. Annars faller flaggan `UseGpu = true` tillbaka till CPU automatiskt.

## Steg 2: Skapa BatchProcessor‑konfigurationen

Nu konfigurerar vi `BatchProcessor`. Detta är hjärtat i **hur man batch‑OCR:ar**—du talar om för Aspose vilket språk som förväntas, vilka förbehandlingsfilter som ska tillämpas och om du vill utnyttja GPU:n.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Varför dessa inställningar?**  
- `Language = Language.English` talar om för motorn att använda den engelska språkmodellen, som är mycket mer exakt än den generiska modellen.  
- `UseGpu` kan halvera behandlingstiden på ett bra GPU, men det är säkert att låta den `false` om du kör på en laptop utan sådan.  
- Filter‑pipeline:n speglar vad en människa skulle göra: räta upp sidan och rensa bort fläckar innan den skickas till OCR‑motorn.

## Steg 3: Peka processorn på din TIFF‑mapp

Nästa del av **hur man batch‑OCR:ar** är att berätta för biblioteket var källfilerna finns. Jokertecken stöds, så du kan plocka upp varje `.tif`‑fil i ett svep.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Särskilt fall:** Om dina bilder har blandade filändelser (`.tiff`, `.tif`, `.png`), anropa `AddFolder` flera gånger eller använd `*.*` och filtrera senare i koden.

## Steg 4: Välj var OCR‑resultaten ska hamna

Du kanske undrar, “Var hamnar den extraherade texten?” Det är den tredje pelaren i **hur man batch‑OCR:ar**—att definiera output‑plats och format. Vi sparar ren‑text‑filer sida‑vid‑sida med originalen.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Om du behöver JSON eller XML istället för ren text, byt bara `OutputFormat.PlainText` mot `OutputFormat.Json` eller `OutputFormat.Xml`. Biblioteket sköter konverteringen åt dig.

## Steg 5: Kör batch‑jobbet och rapportera resultat

Till sist, starta jobbet. Metoden `Execute` blockerar tills varje fil är bearbetad, sedan kan du inspektera `ProcessedCount` för att bekräfta att allt gick bra.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Förväntad utdata

När du kör programmet skriver konsolen ut något liknande:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

I mappen `Output` hittar du en `.txt`‑fil per käll‑TIFF, var och en namngiven efter den ursprungliga bilden (t.ex. `Invoice_001.txt`). Öppna någon fil så ser du den råa OCR‑texten—perfekt för att mata in i ett sökindex eller en efterföljande data‑extraktions‑pipeline.

## Hantera vanliga fallgropar

### 1. GPU ej tillgänglig

Om `UseGpu = true` men ingen kompatibel enhet hittas, faller Aspose tillbaka till CPU tyst. För att vara explicit kan du fånga `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Icke‑TIFF‑filer i samma mapp

När du har en blandad mapp, filtrera programatiskt:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Stora filer som överskrider minnet

För gigantiska flersidiga TIFF‑filer, aktivera streaming:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Proffstips för bättre noggrannhet när du **extraherar text från tiff**

- **Upplösning är viktig** – Sikta på 300 dpi eller högre. Under det kan OCR‑motorn missa tecken.  
- **Färg vs. Gråskala** – Konvertera färgskanningar till gråskala innan OCR; `DeskewFilter` gör redan detta under huven, men du kan lägga till `ColorDepthReductionFilter` för extra hastighet.  
- **Efterbehandling** – När du har ren‑text, kör en stavningskontroll eller regex‑rengöring för att fixa vanliga OCR‑missar (t.ex. “0” vs “O”).

## Fullt fungerande exempel (klart att kopiera och klistra in)

Nedan är hela programmet du kan kompilera och köra. Byt bara ut platshållar‑sökvägarna mot dina egna kataloger.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Kompilera och kör:

```bash
dotnet run
```

Du bör nu ha en prydlig samling av `.txt`‑filer—varje fil är resultatet av **extrahera text från tiff** via en fullt automatiserad batch‑process.

## Slutsats

Vi har gått igenom **hur man batch‑OCR:ar** i C# från start till mål, och täckt allt du behöver för att **extrahera text från tiff**‑filer effektivt. De viktigaste slutsatserna är:

1. Använd Aspose.OCR:s `BatchProcessor` för att undvika att skriva repetitiva loopar.  
2. Utnyttja förbehandlingsfilter (deskew, despeckle) för högre noggrannhet.  
3. Aktivera GPU‑acceleration när det är möjligt, men ha alltid ett CPU‑fallback.  
4. Spara resultat i en förutsägbar mappstruktur så efterföljande jobb kan plocka upp dem automatiskt.

Härifrån kan du utforska:

- Att mata in ren‑text i ett **sökindex** (t.ex. Elasticsearch) för att göra fakturor sökbara.  
- Att konvertera output till **JSON** och föra den till en maskininlärningsmodell som extraherar radposter.  
- Att lägga till **felhantering** för korrupta TIFF‑filer eller behörighetsproblem.

Ge det ett försök,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}