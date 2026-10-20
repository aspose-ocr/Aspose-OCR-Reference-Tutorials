---
category: general
date: 2026-02-11
description: Lär dig hur du kör OCR på en flersidig TIFF i C# med Aspose OCR. Konvertera
  TIFF till text, extrahera text från TIFF och känna igen text från bild snabbt.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: sv
og_description: Hur man kör OCR på en flersidig TIFF med Aspose OCR i C#. Steg‑för‑steg‑guide
  för att konvertera TIFF till text, extrahera text från TIFF och känna igen text
  från bild.
og_title: Hur man kör OCR på flersidiga TIFF‑bilder – Komplett C#‑handledning
tags:
- OCR
- C#
- Aspose
- TIFF
title: Hur man kör OCR på flersidiga TIFF‑bilder med Aspose OCR – C#‑guide
url: /sv/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR på flersidiga TIFF‑bilder med Aspose OCR

Har du någonsin undrat **how to run OCR** på en skannad TIFF som innehåller flera sidor? Du är inte ensam—många utvecklare stöter på detta problem när de behöver extrahera sökbar text från gamla dokument. Den goda nyheten? Med Aspose OCR kan du känna igen text från bildfiler med bara några rader C#‑kod, och du får en enkel sammansatt text klar för indexering eller vidare bearbetning.

I den här handledningen går vi igenom hela arbetsflödet: från installation av Aspose OCR‑paketet, laddning av en flersidig TIFF, till konvertering av TIFF till text och slutligen visning av det extraherade innehållet. När du är klar kommer du att kunna **extract text from TIFF**‑filer, **recognize text from image**‑källor, och till och med automatisera processen för dussintals filer i ett batchjobb. Ingen magi, bara tydliga, praktiska steg.

## Vad du kommer att lära dig

- Hur du konfigurerar Aspose OCR‑motorn för igenkänning av engelska.  
- Den exakta koden som behövs för att **convert TIFF to text** med `OcrEngine`‑klassen.  
- Tips för att hantera flersidiga bilder och säkerställa att varje sida separeras korrekt.  
- Vanliga fallgropar (som saknade inhemska beroenden) och hur du undviker dem.  

**Förutsättningar** – du behöver .NET 6 eller senare, Visual Studio (eller någon C#‑redigerare) och en internetanslutning för den automatiska resurshämtningsfunktionen. Det är allt; inga extra inhemska bibliotek att kämpa med.

## Steg 1 – Installera Aspose OCR NuGet‑paket

Innan du kan **perform OCR on image**‑filer måste du lägga till biblioteket i ditt projekt.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Om du arbetar i Visual Studio kan du också högerklicka på projektet → *Manage NuGet Packages* → söka efter “Aspose.OCR” och klicka *Install*.

Paketet innehåller allt du behöver, och med `AutomaticResourceDownload = true` hämtar motorn språkpaket automatiskt vid körning.

## Steg 2 – Initiera OCR‑motorn (How to Run OCR)

Nu när paketet är på plats skapar och konfigurerar vi en `OcrEngine`‑instans. Detta är kärnan i **how to run OCR** i vårt scenario.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Varför detta är viktigt:** Att sätta `Language` talar om för motorn vilken teckenuppsättning som förväntas, medan `AutomaticResourceDownload` sparar dig från att manuellt placera språkfiler på servern. `OutputFormat` som `Text` ger oss en enkel sträng—perfekt för **convert TIFF to text**‑pipelines.

## Steg 3 – Ladda den flersidiga TIFF‑filen (Recognize Text from Image)

En TIFF kan innehålla många ramar, där varje ram representerar en sida. `System.Drawing.Image`‑klassen abstraherar detta åt oss.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Vad händer om filen inte ligger i samma mapp?** Ange bara en fullständig absolut sökväg eller använd `Path.Combine` med `AppContext.BaseDirectory`.  
> **Vad gäller minnesanvändning?** `using`‑satsen frigör bilden efter bearbetning, vilket förhindrar läckor—avgörande när du batch‑processar dussintals stora TIFF‑filer.

`Recognize`‑anropet itererar automatiskt över varje sida i TIFF‑filen och sammanfogar resultaten med radbrytningar. Det är därför du ser varje sida separerad när du skriver ut `ocrResult.Text`.

## Steg 4 – Fullt fungerande exempel (Alla steg i en fil)

Nedan finns ett komplett, körklart konsolprogram. Kopiera och klistra in det i ett nytt .NET‑konsolprojekt och tryck **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Förväntad output** (avkortad för korthet):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Varje sida visas på en egen rad eftersom `OcrOutputFormat.Text` sätter in en radbrytning mellan ramarna. Om du behöver en annan avgränsare kan du efterbehandla `result.Text` med `String.Replace`.

## Steg 5 – Hantera vanliga edge‑cases

### 5.1 Stora TIFF‑filer  
När du arbetar med gigabyte‑stora TIFF‑filer kan det vara problematiskt att ladda hela filen i minnet. En lösning är att bearbeta varje ram individuellt:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Icke‑engelska dokument  
Om du behöver **recognize text from image** på spanska eller franska, ändra bara `Language`‑egenskapen:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose laddar automatiskt ner de lämpliga språkresurserna.

### 5. Spara resultatet  
Ofta vill du **convert TIFF to text** och lagra resultatet i en `.txt`‑fil:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Du kan också dela upp outputen per sida med `String.Split(Environment.NewLine)` och skriva varje del till en separat fil.

## Pro‑tips & fallgropar

- **AutomaticResourceDownload** fungerar första gången du kör appen; efterföljande körningar är offline.  
- Om du ser felaktiga tecken, dubbelkolla `Language`‑inställningen; felaktiga språkpaket orsakar felaktig igenkänning.  
- För PDF‑filer som har rasteriserats till TIFF‑filer kan du vilja öka `ocrEngine.Dpi` (standard är 300) för bättre noggrannhet.  
- Omslut alltid `Image.FromFile` i ett `using`‑block; annars låser du filen och kan inte radera eller flytta den senare.

## Vanliga frågor

**Q: Fungerar detta med enkelsidiga TIFF‑filer?**  
A: Absolut. Motorn behandlar en enkelframig TIFF på samma sätt; du får bara en rad text.

**Q: Kan jag bearbeta PNG‑ eller JPEG‑filer på samma sätt?**  
A: Ja—byt bara filändelsen. `Recognize`‑metoden accepterar alla `System.Drawing.Image`‑format.

**Q: Vad händer om jag behöver OCR‑resultatet som PDF istället för ren text?**  
A: Sätt `OutputFormat = OcrOutputFormat.Pdf` så innehåller `ocrResult` en PDF‑byte‑array som du kan skriva till disk.

## Slutsats

Du har nu en komplett, end‑to‑end‑lösning för **how to run OCR** på flersidiga TIFF‑filer med Aspose OCR i C#. Genom att konfigurera motorn, ladda bilden och anropa `Recognize` kan du **extract text from TIFF**, **convert TIFF to text** och **recognize text from image** med bara några rader kod. Känn dig fri att justera språk, outputformat eller ram‑för‑ram‑bearbetning för att passa dina egna batch‑behandlingsbehov.

Redo för nästa steg? Prova att kombinera detta tillvägagångssätt med en mapp‑övervakningstjänst för att automatiskt **perform OCR on image**‑filer när de landar i en drop‑mapp, eller integrera outputen i ett sökindex för omedelbar fulltextsökning. Möjligheterna är oändliga, och koden du just har sett är en solid grund.

Om du stöter på några problem, lämna en kommentar nedan eller skriv till mig på GitHub. Lycka till med kodandet, och njut av att förvandla envisa TIFF‑filer till sökbar text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}