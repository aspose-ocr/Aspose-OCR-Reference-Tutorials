---
category: general
date: 2026-10-11
description: Lär dig hur du utför OCR på en bild i C# med Aspose.OCR, inklusive installation
  av System.Drawing.Common och extrahering av text från JPG-filer.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: sv
lastmod: 2026-10-11
og_description: Utför OCR på bild i C# med Aspose.OCR. Denna guide visar hur du installerar
  System.Drawing.Common, laddar en bild för OCR och extraherar text från JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Utför OCR på en bild i C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Hur man utför OCR på en bild i C# med Aspose.OCR
url: /sv/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på bild i C# med Aspose.OCR

Om du behöver **utföra OCR på bild**-filer i en .NET-applikation visar den här guiden en komplett lösning. Med Aspose.OCR kan du snabbt **igenkänna text från bild**-filer såsom JPG och visa resultatet i ett konsolfönster.

Du kommer att lära dig hur du:

* **installerar System.Drawing.Common-paketet** – biblioteket som tillhandahåller `Image`-klassen,
* **laddar bild för OCR** – läs en JPEG eller PNG till minnet,
* konfigurerar språkmodellen,
* **utför OCR på bild** och slutligen,
* **extraherar text från JPG** och skriver ut den.

Stegen är skrivna för .NET 6+, men de fungerar också med .NET Framework 4.6.1 eller senare.

---

## Förutsättningar

| Krav | Varför det är viktigt |
|------|------------------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Tillhandahåller runtime för C#-konsolappen. |
| Visual Studio 2022 (or any IDE) | Gör det enkelt att lägga till NuGet-paket och köra programmet. |
| Internet connection (first run only) | Aspose.OCR laddar ner språkmodulen automatiskt. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Används för att demonstrera **extrahera text från JPG**. |

---

## Steg 1: Installera System.Drawing.Common-paketet

`System.Drawing.Common`-NuGet-paketet tillhandahåller `Image`-klassen som du kommer att **ladda bild för OCR**. Öppna Package Manager Console och kör:

```powershell
Install-Package System.Drawing.Common
```

> **Proffstips:** Rikta in på `net6.0-windows` eller lägg till `<UseWindowsForms>true</UseWindowsForms>` i projektfilen om du får plattforms‑specifika varningar på Linux/macOS.

---

## Steg 2: Lägg till Aspose.OCR NuGet-paketet

Aspose.OCR innehåller OCR-motorn och språkmodellerna. Installera det med:

```powershell
Install-Package Aspose.OCR
```

Paketet är lättviktigt; den nödvändiga språkdata (t.ex. Kyrilliska) laddas ner första gången du sätter `OcrEngine.Language`.

---

## Steg 3: Hur man laddar bild för OCR

Att ladda bilden är det första konkreta steget innan du kan **utföra OCR på bild**. Metoden `Image.FromFile` läser alla format som stöds av GDI+, inklusive JPG, PNG, BMP och TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Om filen inte finns kastas `FileNotFoundException` – omslut anropet med ett try/catch‑block i produktionskod.*

---

## Steg 4: Konfigurera motorn och **utföra OCR på bild**

Skapa en `OcrEngine`-instans, välj språkmodellen, tilldela den laddade bilden och anropa `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()`‑metoden returnerar ett `OcrResult`‑objekt som innehåller den extraherade texten, förtroendesiffror och avgränsningsrutor. Språkmodulen laddas ner automatiskt vid första användning, så inga extra filer behövs.

---

## Steg 5: **Extrahera text från JPG** och visa den

Nu kan du **igenkänna text från bild** och skriva ut resultatet. `Text`‑egenskapen i `OcrResult` innehåller den rena strängen.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Förväntad konsolutmatning

```
Recognized text:
Пример текста на кириллице
```

Om källbilden innehåller engelsk text blir utdata den engelska meningen du placerade i bilden.

---

## Kantfall och bästa‑praxis‑tips

| Situation | Rekommendation |
|-----------|----------------|
| **Stora bilder ( > 5 MB )** | Ändra storlek på bilden till ≤ 2000 px på den längsta sidan innan OCR för att minska minnesanvändning och förbättra hastigheten. |
| **Flera språk i en bild** | Anropa `ocrEngine.AddLanguage(OcrLanguage.English)` utöver Kyrilliska, och sätt sedan `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Låga kontrastskanningar** | Öka kontrasten med `System.Drawing.Graphics` innan du skickar bitmapen till motorn. |
| **Kör på Linux/macOS** | Säkerställ att den inhemska beroendet `libgdiplus` är installerat (`sudo apt-get install -y libgdiplus`). |
| **Upprepade OCR-anrop** | Återanvänd samma `OcrEngine`‑instans och byt bara `ocrEngine.Image` för att undvika upprepad modul‑laddning. |

---

## Fullständigt, körbart program

Nedan är den kompletta konsolapplikationen som innehåller alla tidigare steg. Kopiera koden till ett nytt C#‑konsolprojekt, ersätt bildsökvägen och kör den.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Körning av programmet** skriver ut den igenkända strängen till konsolen, vilket bekräftar att du framgångsrikt **utfört OCR på bild** och **extraherat text från JPG**.

---

## Slutsats

Du vet nu hur du **utför OCR på bild**‑filer i C# med Aspose.OCR, från att installera det nödvändiga **System.Drawing.Common‑paketet** till **ladda bild för OCR**, välja rätt språk och slutligen **extrahera text från JPG**. Detta end‑to‑end‑exempel ger dig en solid grund för att bygga mer avancerade dokument‑bearbetnings‑pipelines, såsom batch‑bearbetning av mappar med bilder eller integrering av OCR i ett webb‑API.

### Vad blir nästa?

* Utforska **igenkänna text från bild** i PDF‑filer genom att först konvertera varje sida till en bild.
* Experimentera med `OcrEngine`‑egenskaperna `Resolution`, `Threshold` och `MaxProcessingTime` för att finjustera noggrannheten på brusiga skanningar.
* Kombinera OCR‑utdata med ett naturlig‑språk‑bearbetningsbibliotek för att automatiskt kategorisera extraherat innehåll.

Känn dig fri att anpassa koden för andra bildformat, lägga till felhantering eller integrera den i större applikationer. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild i C# – Komplett Aspose OCR‑guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extrahera bildtext i C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hur man utför bildtextextraktion från ström med Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}