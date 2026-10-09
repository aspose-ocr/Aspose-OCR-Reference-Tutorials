---
category: general
date: 2026-03-07
description: Extrahera text från PNG-filer med C#. Lär dig hur du konverterar bild
  till text i C# och läser text från skannade bilder snabbt.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: sv
og_description: Extrahera text från PNG-filer med C#. Den här guiden visar hur du
  konverterar bild till text i C# och läser text från skannade bilder med Aspose OCR.
og_title: Extrahera text från PNG i C# – Fullständig OCR‑guide
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahera text från PNG i C# – Fullständig OCR-guide
url: /sv/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PNG i C# – Fullständig OCR‑guide

Har du någonsin behövt **extrahera text från PNG**‑filer men inte vetat var du ska börja? Du är inte ensam – de flesta utvecklare stöter på detta när de först möter skannade grafikfiler eller skärmdumpar som måste bli sökbar text. Den goda nyheten? Med några rader C# och Aspose OCR kan du förvandla vilken PNG som helst till redigerbara strängar på ett ögonblick.

I den här handledningen går vi igenom hela processen: från att hitta PNG‑filer på disken, starta OCR‑uppgifter parallellt, till att visa en snygg förhandsgranskning av varje resultat. När du är klar vet du hur du **konverterar bild till text C#**‑stil, du kan **läsa text från skannade bilder** effektivt, och du ser det bästa sättet att **köra OCR på bilder** utan att blockera UI‑tråden.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även på .NET Core och .NET Framework)  
- Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)  
- En mapp fylld med *.png*-filer du vill bearbeta  
- Valfri IDE (Visual Studio, VS Code, Rider…)

Ingen extra konfiguration krävs; biblioteket levereras med allt som behövs för att avkoda PNG, JPEG, TIFF, du namnger det.

## Steg 1: Hitta alla PNG‑filer – “Extrahera text från PNG” börjar

Först måste vi hitta varje PNG vi tänker köra OCR på. Att använda `Directory.GetFiles` är snabbt och pålitligt.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Varför detta är viktigt:* Att skanna katalogen en gång håller resten av pipeline‑flödet enkelt, och den tidiga kontrollen förhindrar en tyst “ingen‑output”-situation som kan vara svår att felsöka senare.

## Steg 2: Starta parallella OCR‑uppgifter – Effektivt **köra OCR på bilder**

Att köra OCR sekventiellt är okej för ett fåtal filer, men verkliga projekt hanterar ofta dussintals eller hundratals. Genom att starta en `Task` per bild håller vi CPU:n upptagen medan biblioteket gör det tunga arbetet.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Proffstips:* `Task.Run` avlastar arbetet till trådpoolen, vilket betyder att ditt UI (om du har ett) förblir responsivt. Om du kör på en server skalar samma mönster fint över kärnor.

## Steg 3: Vänta på alla uppgifter – Samla resultaten

Nu väntar vi på att varje OCR‑operation ska bli klar. `Task.WhenAll` returnerar en array som matchar den ursprungliga filordningen, vilket gör det enkelt att para ihop resultat med filnamn.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Obs om kantfall:* Om någon enskild bild kastar ett undantag (korrupt fil, format som inte stöds) kommer hela `WhenAll` bubbla upp undantaget. Du kan omsluta den inre `Task.Run` med try/catch och returnera en tom sträng eller ett diagnostiskt meddelande om du behöver feltolerans.

## Steg 4: Visa en förhandsgranskning – Verifiera **konvertera bild till text C#**‑output

En snabb förhandsgranskning hjälper dig bekräfta att OCR fungerade innan du börjar lagra data någon annanstans.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Typisk konsolutskrift ser ut så här:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Om förhandsgranskningen visar meningslöst skräp, dubbelkolla bildkvaliteten eller överväg förbehandling (t.ex. binarisering) – men för de flesta rena PNG‑filer får Aspose OCR rätt på första försöket.

## Valfritt: Spara resultat till CSV – Ett verkligt användningsfall

De flesta projekt behöver den extraherade texten i ett strukturerat format. Nedan är en liten hjälpfunktion som skriver filnamnet och hela OCR‑texten till en CSV‑fil.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Nu kan du importera CSV‑filen till Excel, Power BI eller något annat system som förväntar sig **läsa text från skannade bilder**.

## Vanliga frågor

**Vad händer om mina PNG‑filer är stora (över 5 MB)?**  
Aspose OCR minskar automatiskt stora bilder för att hålla minnesanvändningen rimlig, men du kan manuellt ändra storlek med `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` för att begränsa bredden till 2000 px samtidigt som bildförhållandet bevaras.

**Kan jag köra detta på Linux?**  
Ja. Aspose OCR är plattformsoberoende; se bara till att de inhemska beroendena (`libgdiplus` på vissa distributioner) är installerade.

**Är OCR‑språket inställt på engelska som standard?**  
Korrekt. Om du behöver ett annat språk, sätt `engine.Language = OcrLanguage.French;` (eller någon annan stödjande enum) innan du anropar `Recognize()`.

**Hur hanterar jag lösenordsskyddade PDF‑filer som innehåller PNG‑bilder?**  
Konvertera PDF‑sidorna till bilder först (med Aspose PDF eller ett annat bibliotek), och mata sedan in dessa PNG‑filer i samma pipeline. Principen för **hur man kör OCR på bilder** förblir densamma.

## Fullt fungerande exempel (Async Main)

Nedan är ett självständigt program du kan kopiera och klistra in i ett konsolprojekt. Det innehåller alla delar ovan, plus en liten hjälpfunktion för att validera inmatningsmappen.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Förväntad utskrift** (exempel för två PNG‑filer):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Sammanfattning

Vi har precis gått igenom allt du behöver för att **extrahera text från PNG**‑filer med C#. Från att hitta filerna, starta parallella OCR‑jobb, förhandsgranska strängarna, till att spara dem i en CSV – den här guiden ger dig ett produktionsklart mönster för **konvertera bild till text C#**‑scenarier.  

Om du är redo för nästa steg, prova att köra samma pipeline på JPEG‑ eller TIFF‑filer, experimentera med olika OCR‑språk, eller koppla resultaten till ett sökindex så att du kan **läsa text från skannade bilder** direkt.  

Har du frågor om kantfall, prestandaoptimering eller licensiering? Lämna en kommentar eller kontakta Aspose‑communityn – lycka till med kodningen!  

![Extrahera text från PNG-exempel](extract-text-png.png "Extrahera text från PNG med Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}