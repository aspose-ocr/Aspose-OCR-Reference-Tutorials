---
category: general
date: 2026-03-28
description: Lär dig hur du batchar OCR i C# och enkelt konverterar TIFF till text.
  Denna steg‑för‑steg‑guide visar hur du extraherar text från TIFF‑filer med Aspose
  OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: sv
og_description: Hur batchar man OCR i C#? Följ den här kompletta handledningen för
  att konvertera flersidiga TIFF-filer till sökbar text med Aspose OCR.
og_title: Hur man batchar OCR i C# – Konvertera flersidig TIFF till text
tags:
- OCR
- C#
- Aspose
title: Hur man batch‑OCR:ar i C# – Konvertera flersidig TIFF till text
url: /sv/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch-OCR:ar i C# – Konvertera flersidig TIFF till text

Har du någonsin funderat på **hur man batch-OCR:ar** en hög med skannade sidor utan att skriva en loop för varje bild? Du är inte ensam. I många projekt—tänk fakturabehandling eller arkivdigitalisering—dyker behovet av att **konvertera TIFF till text** upp dagligen, och att göra det en sida i taget blir snabbt en mardröm.

The good news? Med några rader C# och Aspose OCR kan du mata in en hel flersidig TIFF i motorn och få en dictionary med sidnummer kopplade till deras extraherade strängar. I den här handledningen går vi igenom ett komplett, körbart exempel som visar exakt **hur man batch-OCR:ar**, hur man **extraherar text från TIFF**, och varför detta tillvägagångssätt slår det manuella alternativet.

## Vad du kommer att lära dig

- Installera Aspose OCR‑biblioteket i ett .NET‑projekt.  
- Ladda en flersidig TIFF‑fil med `Image.FromMultiPageFile`.  
- Kör `RecognizeBatch` för att få en `Dictionary<int,string>` med resultat per sida.  
- Skriv ut resultatet i ett rent, läsbart format.  

Vid slutet har du en färdigkörbar konsolapp som omvandlar vilken flersidig TIFF som helst till vanlig text—utan extra verktyg.  

### Förutsättningar

- .NET 6.0 SDK (eller någon nyare .NET‑version).  
- Visual Studio 2022 eller VS Code—din favorit‑IDE räcker.  
- En giltig Aspose OCR‑licens eller en gratis utvärderingsnyckel (API:et fungerar utan licens men lägger till ett vattenmärke).  
- Ett exempel på en flersidig TIFF med namnet `multipage.tif` placerad i en mapp du kan referera till.

> **Proffstips:** Om du är på Windows är standardprojektmappen ett praktiskt ställe att lägga TIFF‑filen; på Linux/macOS justerar du bara sökvägen därefter.

## Steg 1: Installera Aspose OCR NuGet‑paket

Innan vi skriver någon kod behöver vi OCR‑biblioteket. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Detta hämtar den senaste stabila versionen (från mars 2026 v23.9) och lägger till de nödvändiga DLL‑filerna i ditt projekt. Ingen extra konfiguration behövs för en enkel konsolapp.

## Steg 2: Skapa konsolapplikationens skelett

Låt oss skapa ett minimalt program som refererar OCR‑motorn. `using`‑direktiven är avgörande—utan dem kommer kompilatorn klaga på saknade typer.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Varför detta är viktigt:** `Image`‑klassen finns i ett under‑namnrymd, och om du glömmer `ImageProcessing`‑importen får du ett felmeddelande “type or namespace not found” som kan slösa bort en timme på felsökning.

Nu lägger vi till `Main`‑metoden och en kort kommentar som beskriver syftet:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Steg 3: Initiera OCR‑motorn

`OcrEngine` är arbetshästen. Att instansiera den en gång och återanvända den för alla sidor är både minnes‑effektivt och snabbt.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Vad händer under huven?** Motorn laddar språkmodeller och förkonfigurerar standardinställningar (t.ex. engelska, auto‑rotate). Du kan justera dessa senare, men standardinställningarna fungerar bra för de flesta dokument.

## Steg 4: Ladda den flersidiga TIFF‑filen

Aspose gör det enkelt att ladda flermotorsbilder. Ange den fullständiga sökvägen eller en relativ sökväg från exekverbara filens arbetskatalog.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Om filen inte hittas kastar `FromMultiPageFile` ett `FileNotFoundException`. Omge den med en `try/catch` om du vill ha elegant felhantering—något vi visar i nästa steg.

## Steg 5: Utför batch‑OCR

Nu kommer stjärnan i showen: `RecognizeBatch`. Den returnerar en `Dictionary<int,string>` där nyckeln är sidindex (börjar på 0) och värdet är den igenkända texten.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Kantfall:** Vissa TIFF‑filer innehåller tomma sidor. Aspose returnerar en tom sträng för dessa sidor, vilket du kan filtrera bort senare om du inte vill ha skräp i ditt resultat.

## Steg 6: Visa resultaten

Till sist itererar du över dictionaryn och skriver ut varje sidas text. Interpolerade strängar håller koden snygg.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Kör programmet bör ge något liknande:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Om du ser förvrängd output, dubbelkolla att käll‑TIFF‑filen inte är korrupt och att språkets text matchar motorns standard (engelska). Du kan också sätta `ocrEngine.Language = OcrLanguage.Spanish;` för icke‑engelska dokument.

## Fullt fungerande exempel

Sätter vi ihop alla bitar får du hela programmet som du kan kopiera‑klistra in i `Program.cs` och köra:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Spara, bygg och kör:

```bash
dotnet run
```

Du bör se varje sidas extraherade innehåll skrivet till konsolen. Det är hela **c# ocr tutorial** du bad om.

## Vanliga frågor & kantfall

### Vad händer om min TIFF innehåller dussintals sidor?

`RecognizeBatch` bearbetar alla ramar i ett enda anrop, men minnesanvändningen växer linjärt med antalet sidor. För mycket stora dokument (hundratals sidor) överväg att bearbeta i delar:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Kan jag spara den extraherade texten till filer istället för att skriva ut?

Absolut. Ersätt `Console.WriteLine`‑blocket med fil‑I/O:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Nu får varje sida sin egen `.txt`‑fil—perfekt för efterföljande indexering.

### Hur ändrar jag utspråket eller aktiverar auto‑rotation?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Dessa inställningar måste appliceras **innan** du anropar `RecognizeBatch`.

## Slutsats

Vi har gått igenom **hur man batch-OCR:ar** en flersidig TIFF med Aspose OCR i C#. Genom att ladda bilden en gång, anropa `RecognizeBatch` och iterera över den resulterande dictionaryn kan du **konvertera TIFF till text** på några sekunder. Exemplet visar också hur du **extraherar text från TIFF**, hanterar fel och eventuellt skriver resultat till filer—allt i en ren, självständig konsolapp.

Klar för nästa steg? Prova att kombinera detta tillvägagångssätt med ett PDF‑genereringsbibliotek för att skapa sökbara PDF‑filer, eller koppla outputen till en databas för sökbara arkiv. Du kan också experimentera med andra bildformat (PNG, JPEG) genom att byta `Image.FromMultiPageFile` mot `Image.FromFile`.

Har du fler frågor om OCR, licensiering eller prestandaoptimering? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}