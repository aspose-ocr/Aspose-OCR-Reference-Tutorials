---
category: general
date: 2026-05-21
description: Utför OCR på en bild med C#. Lär dig hur du laddar en bild för OCR, extraherar
  text från PNG och känner igen text från en bild med ett litet kodexempel.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: sv
og_description: Utför OCR på bild i C# snabbt. Denna guide visar hur du laddar en
  bild för OCR, extraherar text från PNG och känner igen text från bilden med layout‑medveten
  HTML‑utdata.
og_title: Utför OCR på bild med C# – Fullständig programmeringshandledning
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Utför OCR på bild med C# – Komplett steg‑för‑steg‑guide
url: /sv/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild med C# – Komplett steg‑för‑steg guide

Har du någonsin undrat hur man **perform OCR on image** filer utan att trassla med tunga GUI‑program? Du är inte ensam. Oavsett om du digitaliserar kvitton, hämtar data från skannade formulär, eller bara behöver omvandla en PNG till sökbar text, så kan några rader C# göra jobbet.

I den här handledningen går vi igenom hur man laddar en bild för OCR, känner igen text från bild, och slutligen extraherar text från PNG som ren HTML. I slutet har du en färdig‑att‑köra konsolapp som **performs OCR on image** filer och bevarar den ursprungliga layouten.

## Vad du kommer att bygga

- Ett minimalt konsolprogram som läser en PNG (eller någon annan stödd bild)  
- Använder en OCR‑motor för att **recognize text from image**  
- Sparar resultatet som layout‑medveten HTML, med den ursprungliga bilden inbäddad  
- Visar hur man **load image for OCR**, **extract text from PNG**, och hanterar vanliga edge cases  

> **Förutsättningar**  
> - .NET 6.0 SDK eller senare (du kan också rikta mot .NET Framework 4.7+)  
> - Ett NuGet‑kompatibelt OCR‑bibliotek – exemplet använder *Aspose.OCR* men vilket bibliotek som helst med liknande API fungerar  
> - Grundläggande C#‑kunskaper (inget avancerat)  

Har du det? Bra—låt oss dyka in.

## Utför OCR på bild – Fullständig kodgenomgång

Nedan är det **complete, runnable** programmet. Kopiera‑klistra in det i ett nytt konsolprojekt (`dotnet new console`) och tryck **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Förväntad output**  
> ```
> HTML with layout saved.
> ```  
> Efter körningen hittar du `form.html` bredvid din PNG. Öppna den i en webbläsare så ser du exakt samma layout, men nu är texten markerbar och sökbar.

### Ladda bild för OCR

Raden `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` är där vi **load image for OCR**. `ImageStream`‑hjälpen abstraherar bort filformatdetaljer, så du kan mata in JPEG, BMP eller TIFF utan att ändra kod.  

**Varför inte bara skicka en `Bitmap`?**  
Eftersom många OCR‑SDK:er förväntar sig en ström som också innehåller DPI‑metadata. Genom att använda bibliotekets inbyggda laddare försäkrar du att motorn ser bilden exakt som den visas på skärmen, vilket förbättrar noggrannheten.

#### Pro tip
Om du bearbetar en batch av filer, omslut laddningssteget i en `try/catch` och logga eventuella `FileNotFoundException`. Det förhindrar att hela batchen kraschar för att en ensam fil saknas.

### Extrahera text från PNG

När `engine.Recognize()` är klar, håller OCR‑motorn den igenkända texten internt. Du kan hämta den som en sträng om du bara behöver råtext:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Detta är det snabbaste sättet att **extract text from PNG** när du inte bryr dig om layout. För de flesta datainmatningsuppgifter räcker ren text—kom bara ihåg att trimma radbrytningar om du planerar att importera till en CSV.

### Känn igen text från bild

`Recognize()`‑anropet gör det tunga arbetet. Under huven:

1. Normaliserar bilden (rättar snedvridning, tar bort brus)  
2. Segmenterar den i rader och ord  
3. Kör en neuronnäts‑klassificerare tränad på miljontals glyfer  

Eftersom vi satte `Language = OcrLanguage.English`, använder motorn engelskspecifika ordböcker, vilket kraftigt minskar falska positiva. Om du behöver flerspråkigt stöd, skicka helt enkelt en array av språk:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Hantera layout‑medveten HTML‑output

De flesta utvecklare stannar vid ren text, men `HtmlSaveOptions` vi använde låter dig **perform OCR on image** och behålla den visuella strukturen intakt. Två flaggor är viktiga:

- `PreserveLayout = true` – behåller kolumner, tabeller och avstånd.  
- `EmbedImages = true` – infogar den ursprungliga PNG:n som ett Base64‑kodat `<img>`‑element, så HTML‑filen är självständig.

Om du föredrar en lättare fil, sätt `EmbedImages = false` så kommer HTML‑filen att referera till den ursprungliga PNG:n på disk istället.

#### Edge case: Stora filer

För bilder större än 5 MB kan inbäddning blåsa upp HTML‑storleken. I sådana fall, byt till externa bildreferenser och överväg att komprimera PNG:n i förväg med `ImageProcessor.Compress`.

## Vanliga fallgropar och pro‑tips

| Symptom | Trolig orsak | Lösning |
|--------|--------------|-----|
| Felaktiga tecken | Fel språk inställt eller saknar språkpaket | Installera lämpliga språkdatafiler och sätt `engine.Language` korrekt |
| Ingen text i output | Bilden är för mörk eller låg upplösning | Pre‑process med `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Layout trasig i HTML | `PreserveLayout` left at default `false` | Set `PreserveLayout = true` in `HtmlSaveOptions` |
| Långsam bearbetning på många sidor | Engine re‑initializes per file | Reuse the same `OcrEngine` instance and only change `engine.Image` each loop |

### Skala till flera filer

Om du behöver **perform OCR on image** filer i en mapp, omslut kärnlogiken i en enkel loop:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Observera att vi **load image for OCR** inom loopen, men behåller samma `engine` och `htmlOptions`‑objekt. Detta minskar minnesanvändning och snabbar upp batchjobb.

## Gå längre: Exportera till PDF eller DOCX

Samma `engine` kan spara till andra format:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Om ditt downstream‑system förväntar sig sökbara PDF‑filer, är detta en endradsändring—ingen anledning att skriva en separat konverteringspipeline.

## Slutsats

Vi har just visat dig hur du **perform OCR on image** filer med C#, från att ladda bilden till **extract text from PNG** och slutligen **recognize text from image** till en layout‑medveten HTML‑fil. Det fullständiga exemplet är redo att köras, och du förstår nu varför varje steg är viktigt, hur du justerar det för olika språk, och vilka fallgropar du bör se upp för.

Nästa steg, prova att byta ut engelska mot ett annat språk, experimentera med `PreserveLayout = false` för att få en smalare HTML, eller skicka ren‑text‑outputen till en databas för sökbara arkiv. Himlen är gränsen när du kombinerar en robust OCR‑motor med några rader C#.

Har du frågor om hantering av fler‑sidiga TIFF‑filer, eller vill veta hur du integrerar detta i ett ASP.NET Core‑API? Lämna en kommentar nedan, och lycka till med kodandet!

## Relaterade handledningar

- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahera text från bild – känna igen rad med Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}