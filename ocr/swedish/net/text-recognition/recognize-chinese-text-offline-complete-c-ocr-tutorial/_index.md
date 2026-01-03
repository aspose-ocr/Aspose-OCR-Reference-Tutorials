---
category: general
date: 2026-01-02
description: Lär dig hur du känner igen kinesisk text och extraherar text från PNG-filer
  med offline‑textigenkänning med Aspose.OCR. Ingen internetuppkoppling behövs – utför
  OCR på bilden på bara några steg.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: sv
og_description: Känn igen kinesisk text utan internet. Den här handledningen visar
  hur man extraherar text från PNG med offline-textigenkänning och utför OCR på en
  bild i C#.
og_title: känn igen kinesisk text offline – steg‑för‑steg C#‑guide
tags:
- OCR
- C#
- Aspose
title: igenkänn kinesisk text offline – Komplett C# OCR-handledning
url: /sv/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Känn igen kinesisk text offline – Komplett C# OCR-handledning

Har du någonsin behövt **recognize chinese text** från en skannad PNG men din app körs på en maskin utan internet? Du är inte ensam. I många företags‑scenarier—tänk luft‑avskilda servrar eller fält‑enheter—är det helt enkelt inte ett alternativ att förlita sig på molntjänster.  

I den här guiden går vi igenom en själv‑innehållande lösning som låter dig **extract text from png**‑filer, köra **offline text recognition**, och **perform OCR on image**‑tillgångar med Aspose.OCR. I slutet har du ett färdigt C#‑konsolprogram som skriver ut de kinesiska tecknen direkt i konsolen.

## Förutsättningar

- .NET 6 SDK (eller någon nyare .NET‑version) installerad lokalt.  
- Visual Studio 2022 eller VS Code – vad du föredrar.  
- En kopia av Aspose.OCR för .NET NuGet‑paketet (`Aspose.OCR`).  
- Språkresursfilerna för English och Simplified Chinese (handledningen visar hur du laddar ner dem automatiskt).  
- En bild med namnet `chinese_doc.png` placerad i en mapp du kan referera till (`YOUR_DIRECTORY`‑platshållare).

Inga extra tjänster, inga API‑nycklar—bara en lokal DLL och ett par resursfiler.

---

## Steg 1 – Ladda ner de nödvändiga språkresurserna (en gång)

Aspose.OCR lagrar språkpaket på disk. Första gången du kör appen måste du hämta dem. Anropet `ResourceManager.DownloadResources` gör exakt det, och eftersom vi skickar både English och Simplified Chinese kan motorn senare växla mellan dem utan extra nätverkstrafik.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tip:** Behåll den nedladdade mappen (`Aspose.OCR.Resources`) under versionskontroll om du behöver reproducerbara byggen på flera maskiner.

## Steg 2 – Initiera OCR‑motorn i offline‑läge

Att sätta `OfflineMode = true` instruerar biblioteket att undvika alla HTTP‑anrop. Detta är nyckeln till sann **offline text recognition**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Why this matters:** Vissa OCR‑bibliotek faller tillbaka på molntjänster när ett språkpaket saknas. Genom att tvinga offline‑läge garanterar vi deterministisk prestanda och efterlevnad av dataskyddspolicys.

## Steg 3 – Läs in PNG‑filen du vill bearbeta

Vi kommer att använda `System.Drawing.Bitmap` för att läsa bilden. Om ditt projekt riktar sig mot .NET 6+ på icke‑Windows‑plattformar, överväg `SkiaSharp` som ett alternativ, men för de flesta Windows‑centrerade distributioner fungerar `Bitmap` bra.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Edge case:** Om PNG‑filen är mycket stor (över 5 MP) kan du vilja skala ner den först för att snabba upp igenkänning och minska minnesanvändning:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Steg 4 – Kör igenkänning med Simplified Chinese‑språk

Här talar vi om för motorn exakt vilket språk som ska användas. Objektet `RecognitionOptions` låter dig också justera saker som `DetectOrientation` eller `PreserveFormatting`, men standardinställningarna fungerar bra för de flesta tryckta dokument.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Steg 5 – Visa (eller vidarebearbeta) den extraherade texten

Egenskapen `OcrResult.Text` innehåller den rena textrepresentationen. Du kan skriva den till konsolen, en fil, eller föra in den i en efterföljande NLP‑pipeline.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Förväntad utdata

Om `chinese_doc.png` innehåller frasen “你好，世界！”, kommer konsolen att visa:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Note:** OCR‑noggrannhet beror på bildkvalitet, teckensnittsklarhet och kontrast. För bästa resultat, använd högupplösta skanningar (300 dpi eller högre) och se till att texten inte är snedvriden.

---

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Spara det som `Program.cs` i ett nytt konsolprojekt och kör `dotnet run`. Alla steg är samlade, så du kan se flödet från resursnedladdning till slutlig utdata.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tip:** Omge anropet `ResourceManager.DownloadResources` med ett `try/catch`‑block om du vill ha en smidig hantering när internet verkligen är otillgängligt. Metoden kommer annars att kasta ett `NetworkException`.

---

## Vanliga frågor (FAQ)

| Question | Answer |
|----------|--------|
| **Can I recognise Traditional Chinese?** | Ja—byt ut `Language.ChineseSimplified` mot `Language.ChineseTraditional` och ladda ner motsvarande paket. |
| **What if I need to extract text from a JPEG instead of PNG?** | Samma kod fungerar; byt bara filändelsen. `Bitmap` stödjer de flesta vanliga rasterformat. |
| **Is there a way to get bounding boxes for each character?** | Sätt `RecognitionOptions.DetectRegions = true`. `OcrResult` kommer då innehålla `Region`‑objekt med koordinater. |
| **How do I run this on Linux?** | Använd paketet `System.Drawing.Common` (1.0+). På huvudlös Linux kan du behöva den inhemska beroendet `libgdiplus`. |
| **Can I batch‑process a folder of images?** | Absolut—omge igenkänningslogiken i en `foreach (var file in Directory.GetFiles(folder, "*.png"))`‑loop. |

## Nästa steg & relaterade ämnen

- **Improve accuracy**: experimentera med `RecognitionOptions.PreprocessImage = true` för att låta motorn automatiskt förbättra kontrasten.  
- **Combine languages**: du kan skicka en array av språk till `ResourceManager.DownloadResources` och låta motorn auto‑detektera.  
- **Integrate with a UI**: flytta konsolkoden till en WinForms‑ eller WPF‑app och visa OCR‑resultatet i en textruta.  
- **Explore other Aspose libraries**: `Aspose.PDF` för PDF‑generering, `Aspose.Slides` för bildspels‑automatisering, etc.

Om du är intresserad av att extrahera text från andra bildformat gäller samma mönster—byt bara filvägen och justera eventuellt förbehandlingsalternativen. Lycka till med kodandet!

---

![exempel på att känna igen kinesisk text](/images/recognize-chinese-text.png "Skärmbild som visar utdata för recognize chinese text i konsolen")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}