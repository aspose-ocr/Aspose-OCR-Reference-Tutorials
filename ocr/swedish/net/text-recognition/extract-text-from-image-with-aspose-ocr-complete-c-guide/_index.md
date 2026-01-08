---
category: general
date: 2026-01-07
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du känner igen
  text från foto, förbättrar OCR‑noggrannheten, laddar bild för OCR och ställer in
  OCR‑språk.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: sv
og_description: Extrahera text från bild med Aspose OCR. Denna guide visar hur du
  känner igen text från foto, förbättrar OCR‑noggrannheten, laddar bild för OCR och
  ställer in OCR‑språk.
og_title: Extrahera text från bild med Aspose OCR – C#‑handledning
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahera text från bild med Aspose OCR – Komplett C#‑guide
url: /sv/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild – Fullständig C#-implementation med Aspose OCR

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket bibliotek som ger pålitliga resultat? Du är inte ensam. I många verkliga applikationer—kvittoskannrar, ID‑verifierare eller bara ett snabbt verktyg för att ta anteckningar—är det en nödvändig funktion att kunna **igenkänna text från foto**.

I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra exempel som visar hur du **laddar bild för OCR**, konfigurerar motorn för att **ange OCR‑språk**, och tillämpar några förbehandlingsknep för att **förbättra OCR‑noggrannheten**. I slutet har du en enda C#‑fil som skriver ut den extraherade texten till konsolen, och du förstår varför varje inställning är viktig.

> **Tips:** Koden fungerar med Aspose.OCR ≥ 23.5, .NET 6+ och alla Windows-, Linux- eller macOS-miljöer som kan köra .NET Core.

## Förutsättningar

- .NET 6 SDK (eller nyare) installerat  
- Visual Studio 2022, VS Code, eller någon annan editor du föredrar  
- NuGet‑paketet `Aspose.OCR` (installera via `dotnet add package Aspose.OCR`)  
- En bildfil (JPEG/PNG) som innehåller tydlig tryckt eller skriven text  

Om du har detta, låt oss dyka ner.

![exempel på extrahering av text från bild](/images/ocr-example.png "extrahera text från bild – Aspose OCR‑utdata")

## Steg 1: Skapa och avyttra OCR‑motorn – “Extrahera text från bild” kärnan

Det första du behöver är en instans av `OcrEngine`. Att omsluta den i ett `using`‑block garanterar korrekt avyttring av inhemska resurser.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Varför detta är viktigt:** `OcrEngine` håller ohanterat minne för de inhemska OCR‑DLL‑erna. Att avyttra den omedelbart förhindrar minnesläckor, särskilt när du bearbetar många bilder i en batch.

## Steg 2: Definiera igenkänningsinställningar – Förbättra OCR‑noggrannheten

Därefter skapar vi ett `RecognitionSettings`‑objekt. Här **anger vi OCR‑språk** och lägger till förbehandlingsfilter som ofta gör skillnaden mellan en förvrängd sträng och ett rent resultat.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Varför dessa filter?**  
- **Deskew** åtgärdar det vanliga problemet med att ett foto taget med telefonen är några grader snett.  
- **Denoise** tar bort fläckar som kan tolkas som tecken.  
- **ContrastEnhance** får svagt bläck att sticka ut, vilket är avgörande för att **förbättra OCR‑noggrannheten**.

## Steg 3: Ladda bilden – Ladda bild för OCR effektivt

Aspose tillhandahåller `ImageStream.FromFile` för snabb laddning. Du kan också mata in en `MemoryStream` om bilden kommer från en webbförfrågan eller en databas.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Vanligt fallgropp:** Att ange en sökväg med snedstreck på Windows fungerar, men att använda `Path.Combine` är säkrare för plattformsoberoende projekt.

## Steg 4: Utför igenkänning – Känn igen text från foto

Nu anropar vi `Recognize`, och skickar både bildströmmen och våra inställningar. Metoden returnerar en enkel sträng med den extraherade texten.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Om bilden innehåller flera textblock, sammanfogar Aspose dem med radbrytningar och bevarar den ursprungliga layouten så gott det går.

## Steg 5: Skriv ut resultatet – Verifiera extraheringen

Till sist skriver du resultatet till konsolen. I en riktig applikation kan du lagra det i en databas, skicka det till en annan tjänst eller visa det i ett UI.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Förväntad konsolutmatning

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Om du ser förvrängda tecken, dubbelkolla att bilden är tydlig, att språket matchar texten och att förbehandlingsfiltren är lämpliga.

## Steg 6: Valfria justeringar – Finjustera för specialfall

### a. Byta språk

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Lägga till anpassade filter

Aspose erbjuder också `PreprocessFilter.Sharpen` eller `PreprocessFilter.Binarize`. Experimentera med dem när standardtrion inte räcker till.

### c. Hantera stora bilder

För mycket högupplösta foton, skala ner först för att hålla minnesanvändningen låg:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Vanliga frågor

**Q: Fungerar detta med handskrivna anteckningar?**  
A: Aspose OCR är optimerat för tryckt text. Handstift igenkänning kräver en annan motor (t.ex. Aspose.OCR for Handwriting eller en maskininlärningsmodell).

**Q: Kan jag bearbeta flera bilder i en loop?**  
A: Absolut. Flytta bara `using (var ocrEngine = new OcrEngine())`‑blocket utanför loopen och återanvänd motorn för bättre prestanda.

**Q: Vad händer om bilden är en PDF‑sida?**  
A: Konvertera PDF‑sidan till en bild först (Aspose.PDF kan rendera sidor som PNG/JPEG), och mata sedan in den till OCR‑motorn.

## Sammanfattning – Vad vi uppnådde

- **Extraherade text från bild** med ett enda, självständigt C#‑program.  
- Demonstrerade hur man **känner igen text från foto** med förbehandling som **förbättrar OCR‑noggrannheten**.  
- Visade det korrekta sättet att **ladda bild för OCR** och **ange OCR‑språk** för flerspråkiga scenarier.  

## Nästa steg & relaterade ämnen

- **Batch‑bearbetning:** Kombinera detta kodsnutt med `Directory.GetFiles` för att OCR:a en hel mapp.  
- **Efterbehandling:** Använd reguljära uttryck för att rensa upp datum, belopp eller ID:n efter extrahering.  
- **Integrationer:** Mata den extraherade texten till Azure Cognitive Search eller Elastic för sökbara dokument.  

Känn dig fri att experimentera med olika filterkombinationer, språk och bildkällor. Kärnmönstret förblir detsamma: skapa motorn, konfigurera inställningarna, ladda bilden, känna igen och skriva ut. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}