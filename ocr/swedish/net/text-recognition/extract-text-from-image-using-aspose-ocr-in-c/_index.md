---
category: general
date: 2026-08-09
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du laddar en
  bild för OCR, ställer in OCR-språk, bearbetar bildens OCR och konverterar bilden
  till text på ett effektivt sätt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: sv
lastmod: 2026-08-09
og_description: Extrahera text från bild med Aspose OCR i C#. Denna handledning visar
  hur du laddar en bild för OCR, ställer in OCR-språk, bearbetar bildens OCR och konverterar
  bilden till text med några få kodrader.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Extrahera text från bild med Aspose OCR – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahera text från bild med Aspose OCR i C#
url: /sv/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med Aspose OCR i C#

Om du behöver **extrahera text från bild** i en .NET‑applikation, guidar den här handledningen dig genom en komplett, färdig‑att‑köra‑lösning. Du kommer att se hur du **laddar bild för OCR**, väljer rätt språkmodul, kör OCR‑motorn och slutligen **konverterar bild till text** med bara några rader C#.

Handledningen täcker allt som krävs för att få pålitliga resultat med Aspose.OCR, inklusive vanliga fallgropar som ej stödda bildformat och språk‑specifika nyanser. I slutet har du ett självständigt program som skriver ut den igenkända texten till konsolen.

## Vad du kommer att uppnå

* Ladda en bildfil i Aspose OCR‑motorn.  
* **Ställ in OCR‑språk** (Kyrilliska i exemplet, men vilket stödjande språk som helst fungerar).  
* **Processa bild‑OCR** och erhåll den textuella representationen.  
* **Konvertera bild till text** och visa den, redo för vidare bearbetning eller lagring.  

**Förutsättningar**

* .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+).  
* Visual Studio 2022 (eller någon IDE som stödjer C#).  
* Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`).  

---

## Extrahera text från bild – fullständig kodgenomgång

Nedan är det kompletta, körbara programmet. Kopiera det till ett nytt konsolprojekt och ersätt `YOUR_DIRECTORY/sample_cyrillic.jpg` med sökvägen till din egen bild.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Varför varje steg är viktigt

1. **Skapa en OCR‑motorsinstans** – `OcrEngine` kapslar in all OCR‑funktionalitet. Att avyttra den omedelbart frigör inhemska resurser, vilket är kritiskt för lång‑körande tjänster.  
2. **Ställ in OCR‑språk** – Att välja rätt språkmodul förbättrar noggrannheten avsevärt. Aspose erbjuder över 30 språkpaket; standard är engelska. Exemplet använder kyrilliska för att demonstrera ett icke‑latinskt skriftsystem.  
3. **Ladda bild för OCR** – Motorn arbetar med ett `ImageStream`. Att tillhandahålla en högupplöst bild (≥300 dpi) minskar feligenkänning, särskilt för komplexa skript.  
4. **Processa bild‑OCR** – Här sker den tunga bearbetningen. Metoden returnerar ett `OcrResult` som innehåller den extraherade texten, förtroendesiffror och valfri layoutdata.  
5. **Konvertera bild till text** – `result.Text` är en vanlig `string`. Du kan skriva den till en fil, mata in den i ett sökindex eller skicka den till nedströms NLP‑pipeline.  

---

## Ladda bild för OCR

`ImageStream.FromFile`‑metoden stödjer vanliga rasterformat. Om du får bilder som byte‑arrayer (t.ex. från ett web‑API), använd `ImageStream.FromBytes(byte[])` istället:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Proffstips:** Verifiera alltid att bilden inte är korrupt innan du skickar den till motorn. Ett snabbt `try { Image.FromFile(...); } catch { ... }`‑skydd förhindrar körningsfel.

---

## Ställ in OCR‑språk

Aspose.OCR levereras med språkpaket som du kan aktivera vid körning. För att lista alla tillgängliga språk:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Om du behöver känna igen flera språk i samma dokument, kombinera dem med bitvis OR‑operatorn:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Edge case:** Att blanda höger‑till‑vänster (RTL) språk (t.ex. arabiska) med vänster‑till‑höger‑skript kan kräva extra layout‑hantering. Aspose upptäcker automatiskt riktning, men du kan finjustera det via `engine.PageSegmentationMode`.

---

## Processa bild‑OCR

`Process`‑anropet är synkront och blockerar tills motorn är klar. För stora batcher eller UI‑applikationer, överväg den asynkrona överlagringen:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Vanlig fallgrop:** Att glömma att sätta `engine.Image` innan du anropar `Process` kastar ett `InvalidOperationException`. Tilldela alltid bilden först.

---

## Konvertera bild till text

Den extraherade strängen kan manipuleras som vilken annan .NET `string` som helst. Till exempel, för att skriva utdata till en fil:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Om du behöver behålla **radbrytningar** exakt som de visas i bilden, använd `result.Text` direkt. För efterbearbetning (t.ex. ta bort extra blanksteg), använd standardsträngmetoder:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Sammanfattning av komplett exempel

När allt sätts ihop, gör programmet:

1. Instansierar `OcrEngine`.  
2. **Ställer in OCR‑språk** till kyrilliska (eller vilket språk du väljer).  
3. **Laddar bild för OCR** från disk.  
4. **Processar bild‑OCR** för att få det textuella resultatet.  
5. **Konverterar bild till text** och skriver ut den.  

Att köra exemplet med en tydlig kyrillisk bild ger en utskrift liknande:

```
=== Recognized Text ===
Пример текста на кириллице
```

Om bilden innehåller engelsk text, ändra helt enkelt `engine.Language = OcrLanguage.English;` så kommer samma kod att **extrahera text från bild** korrekt.

---

## Slutsats

Du vet nu hur du **extraherar text från bild** med Aspose OCR i C#. Handledningen täckte inläsning av bilden, val av lämpligt språk, körning av OCR‑processen och **konvertering av bild till text** för vidare användning.  

Härifrån kan du:

* Experimentera med andra språk (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Integrera OCR‑steget i en större pipeline (t.ex. dokumentintag, sökbara PDF‑filer).  
* Optimera prestanda genom att batcha bilder eller använda den asynkrona API:n.  

Känn dig fri att utforska Aspose.OCR‑dokumentationen för avancerade funktioner som anpassade ordböcker, sidsegmenteringslägen och finjustering av OCR‑noggrannhet. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Hur man utför bildtextutdragning från ström med Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}