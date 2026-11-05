---
category: general
date: 2026-03-13
description: Hur man använder OCR i C# för att extrahera text från skanningar. Lär
  dig konvertera TIFF till text med Aspose OCR, GPU‑acceleration och steg‑för‑steg‑kod.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: sv
og_description: Hur du använder OCR i C# för att extrahera text från skanningar. Denna
  guide visar hur du konverterar TIFF till text med Aspose OCR och GPU-acceleration.
og_title: Hur man använder OCR i C# – Extrahera text från skanningar snabbt
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hur du använder OCR i C# – Extrahera text från skanningar snabbt
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från skanningar snabbt

Har du någonsin undrat **hur man använder OCR** för att hämta läsbar text från en hög med skannade TIFF‑filer? Du är inte ensam. I många verkliga projekt—tänk fakturadigitalisering, arkivering av historiska dokument, eller helt enkelt att göra PDF‑filer sökbara—behöver utvecklare ett pålitligt sätt att **extrahera text från skanningar** utan att anstränga sig.

Den goda nyheten? Med Aspose OCR och några rader C# kan du konvertera TIFF till text på några sekunder, även på en modest arbetsstation. Nedan får du ett komplett, färdigt‑att‑köra exempel, plus resonemanget bakom varje val så att du kan anpassa det till ditt eget arbetsflöde.

## Vad du behöver

Innan vi dyker ner, se till att du har följande tillgängligt:

| Förutsättning | Varför det är viktigt |
|--------------|-----------------------|
| .NET 6+ (or .NET Framework 4.7+) | Aspose OCR NuGet‑paketet riktar sig mot moderna .NET‑runtime. |
| Visual Studio 2022 (or any IDE you like) | Ger dig IntelliSense och enkel felsökning. |
| A CUDA‑compatible GPU & driver (optional) | Aktiverar `ocrEngine.UseGpu = true` för en märkbar hastighetsökning på stora batcher. |
| A folder of TIFF images you want to process | Denna handledning använder `*.tif`‑filer, men du kan anpassa mönstret. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Det kärnbibliotek som gör det tunga lyftet. |

Om du saknar någon av dessa, skaffa dem nu—det är ingen idé att läsa vidare bara för att stöta på en saknad beroende senare.

## Översikt av lösningen

På en hög nivå gör programmet tre saker:

1. **Skapa en OCR‑motor** och eventuellt aktivera GPU‑acceleration.  
2. **Iterera över varje TIFF‑fil** i en katalog, kör igenkänning och fånga den resulterande rentexten.  
3. **Skriv texten** till en `.txt`‑fil som ligger bredvid originalbilden.

Det är allt. Koden är avsiktligt liten, men den visar bästa praxis som explicit språkval, korrekt resursrensning och felhantering för de vanligaste kantfallen.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## Steg 1: Initiera OCR‑motorn (Hur man använder OCR)

Det första du behöver är en instans av `OcrEngine`. Detta objekt är porten till all Aspose OCR‑funktionalitet. Som standard kör den på CPU, men genom att sätta `UseGpu = true` instrueras biblioteket att avlasta de tunga matrisberäkningarna till ditt grafikkort—förutsatt att du har en CUDA‑kompatibel drivrutin installerad.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Varför detta är viktigt:**  
- **GPU‑acceleration** kan minska behandlingstiden med upp till 70 % för högupplösta skanningar.  
- **Explicit språkval** undviker att motorn gissar och förbättrar noggrannheten, särskilt för icke‑latinska skript.

## Steg 2: Peka motorn mot dina skanningar (Konvertera TIFF till text)

Nästa steg är att tala om för programmet var det ska leta efter bilderna. Att använda `Directory.GetFiles` med ett `*.tif`‑filter håller logiken enkel och undviker att hämta orelaterade filer som `.jpg` eller `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Kantfallsanteckning:** Om katalogen är tom körs loopen nedan helt enkelt aldrig, vilket är helt okej. Du kommer senare att se ett vänligt meddelande “No files found”.

## Steg 3: Bearbeta varje TIFF‑fil (Extrahera text från skanningar)

Nu hjärtat i programmet: ladda varje bild, köra OCR och spara resultatet. Hjälpmetoden `ImageStream.FromFile` strömmar filen direkt till minnet, vilket är mer effektivt än att först ladda en `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Varför vi omsluter varje iteration i ett `try/catch`:**  
Att skanna en batch med dokument är rörigt; en korrupt TIFF eller ett minnesbrist‑ögonblick bör inte avbryta hela körningen. `catch`‑blocket loggar problemet och fortsätter, vilket håller pipeline robust.

### Förväntad utdata

För varje `example.tif` hittar du en syskonfil `example.txt` som innehåller något liknande:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Om OCR‑motorn inte kan läsa en rad, lämnar den helt enkelt en tom rad eller ett förvrängt tecken—inget kraschar.

## Steg 4: Rensa upp och disponera (Bästa praxis)

`OcrEngine` implementerar `IDisposable`, så det är artigt att frigöra inhemska resurser när du är klar. I en kort konsolapp kan du förlita dig på GC, men explicit disponering är en vana som är värd att utveckla.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet som du kan klistra in i ett nytt Console App‑projekt. Det kompilerar som det är, förutsatt att du har lagt till Aspose.OCR NuGet‑paketet.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Snabb checklista

- **GPU‑flagga** – ta bort eller sätt till `false` om du inte har en CUDA‑drivrutin.  
- **Språk** – byt `Language.English` mot något annat stödjande språk.  
- **Fil‑mönster** – ändra `"*.tif"` till `"*.png"` eller `"*.*"` om dina skanningar är i ett annat format.

## Vanliga fallgropar & pro‑tips (c# OCR‑handledning)

| Fallgropar | Hur man undviker det |
|------------|----------------------|
| **Out‑of‑memory‑fel** på stora batcher | Bearbeta filer i mindre delar eller anropa `GC.Collect()` efter var 50:e fil (sällan behövs). |
| **GPU upptäcks inte** men `UseGpu = true` | Motorn faller tyst tillbaka till CPU, men du kan kontrollera `ocrEngine.IsGpuAvailable` efter konstruktion. |
| **Fel språkpaket** leder till förvrängd output | Sätt alltid `ocrEngine.Language` explicit; standard kan vara `Language.Unknown`. |
| **Filsökväg innehåller Unicode‑tecken** | Använd `Path.GetFullPath` för att normalisera, eller prefixa med `@"\\?\"` på Windows om sökvägarna överskrider |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}