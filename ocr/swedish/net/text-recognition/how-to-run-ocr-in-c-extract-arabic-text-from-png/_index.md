---
category: general
date: 2026-01-10
description: Hur man kör OCR snabbt och extraherar arabisk text från en bild. Lär
  dig att konvertera bild till text, läsa text från PNG och se hur man extraherar
  text med Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: sv
og_description: Hur man kör OCR i C# och extraherar arabisk text från en PNG-bild.
  Denna guide visar dig hur du konverterar bild till text och läser text från PNG
  steg för steg.
og_title: Hur man kör OCR i C# – Extrahera arabisk text från PNG
tags:
- OCR
- C#
- Aspose
title: Hur man kör OCR i C# – Extrahera arabisk text från PNG
url: /sv/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR i C# – Extrahera arabisk text från PNG

Har du någonsin undrat **hur man kör OCR** på en bild som innehåller arabiska tecken? Du är inte ensam. Många utvecklare fastnar när de måste **extrahera arabisk text** från en PNG men inte vet vilket bibliotek som hanterar höger‑till‑vänster‑skript utan huvudvärk.  

I den här handledningen går vi igenom allt du behöver veta för att **konvertera bild till text**, **läsa text från PNG**, och slutligen **hur man extraherar text** med Aspose.OCR i en ren C#‑konsolapp. När du är klar har du ett färdigt program som skriver ut den arabiska strängen direkt i din terminal.

## Vad du kommer att lära dig

- Installera och referera Aspose.OCR‑paketet från NuGet.  
- Konfigurera OCR‑motorn för stöd av arabiska.  
- Ladda en PNG‑bild och köra igenkänningsprocessen.  
- Hämta och visa den extraherade texten.  
- Justera inställningar för bättre noggrannhet och hantera vanliga fallgropar.

Ingen tidigare erfarenhet av OCR krävs, bara en grundläggande förståelse för C# och en .NET‑utvecklingsmiljö (Visual Studio, Rider eller `dotnet`‑CLI räcker).

---

## Hur man kör OCR – Installera Aspose OCR

### Steg 1: Lägg till Aspose.OCR‑paketet från NuGet

Det första vi behöver är själva OCR‑biblioteket. Aspose.OCR är en kommersiell produkt, men den erbjuder en gratis provperiod som fungerar utmärkt för lärande.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternativt kan du öppna **NuGet Package Manager** i Visual Studio, söka efter **Aspose.OCR** och klicka på **Install**.

> **Pro tip:** Om du planerar att använda biblioteket i en CI‑pipeline, lägg till flaggan `-v` för att låsa versionen, t.ex. `dotnet add package Aspose.OCR -v 23.10`.

### Steg 2: Skapa ett nytt konsolprojekt (om du inte redan har ett)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Nu har du en ny `Program.cs`‑fil klar för vår kod.

---

## Extrahera arabisk text – Skriva OCR‑koden

Nedan är det kompletta, färdiga programmet. Spara det som `Program.cs` (eller ersätt den automatiskt genererade filen).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Varför varje rad är viktig

- **`OcrEngine`**: Den centrala klassen som koordinerar bildladdning, språkval och igenkänning.  
- **`Language = OcrLanguage.Arabic`**: Arabiska använder ett höger‑till‑vänster‑skript och unika tecken; genom att sätta språket talar du om för motorn att använda rätt teckensnittsmodeller.  
- **`ImageStream.FromFile`**: Hanterar PNG, JPEG, BMP och många andra format. Om du någonsin behöver läsa från en `MemoryStream` (t.ex. en uppladdad fil), ersätt detta anrop därefter.  
- **`Recognize()`**: Utför det tunga arbetet – pixelanalys, segmentering och teckenklassificering.  
- **`ocrEngine.Text`**: Den slutgiltiga Unicode‑strängen, klar för vidare bearbetning, lagring eller visning.

### Förväntad utskrift

Om `arabic_sample.png` innehåller frasen “مرحبا بالعالم” (Hello World) kommer konsolen att skriva ut:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Om utskriften ser förvrängd ut, dubbelkolla att bilden är tydlig, att språket är satt till Arabiska och att OCR‑motorns version matchar dokumentationen.

---

## Konvertera bild till text – Finjustera noggrannheten

Standardinställningarna fungerar för de flesta rena skanningar, men verkliga bilder kräver ofta lite extra omsorg.

| Inställning | Vad den gör | När du ska använda den |
|------------|-------------|------------------------|
| `ocrEngine.Config.Preprocess = true` | Aktiverar automatisk binarisering och brusreducering. | Skannade dokument med **skuggor**. |
| `ocrEngine.Config.Deskew = true` | Rotera bilden för att korrigera lätt lutning. | Fotografi tagna i vinkeln. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Behandlar hela bilden som ett **block** med text. | Enkla bildtexter **eller** enradiga etiketter. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Begränsar igenkänning till enbart arabiska tecken. | Minskar falska positiva på blandade språk‑sidor. |

Du kan lägga till dessa rader precis efter att du skapat motorn:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Läs text från PNG – Hantera olika bildkällor

Ibland finns PNG‑filen i en databas eller kommer från en webbförfrågan. Här är en snabb variant som läser från en `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Resten av flödet är identiskt, vilket betyder att **hur man extraherar text** förblir konsekvent oavsett källa.

---

## Hur man extraherar text – Avancerade alternativ & kantfall

### 1. Fler‑sidiga PDF‑ eller TIFF‑filer

Om du behöver OCR:a ett dokument med flera sidor, loopa över varje sida:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Note:** Du behöver `Aspose.PDF`‑paketet för detta kodexempel.

### 2. Automatisk språkdetection

Aspose.OCR erbjuder också auto‑detect, men det är långsammare. Om du är osäker på om bilden innehåller arabiska eller ett annat skript, aktivera detta:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Motorn provar varje språkmodell och väljer den bästa matchen.

### 3. Prestandatips

- **Återanvänd `OcrEngine`**‑objektet för flera bilder; att skapa en ny instans varje gång ger extra overhead.  
- **Kör parallellt** endast om du har separata motorinstanser per **tråd** – att dela en instans orsakar race‑conditions.

---

## Slutsats

Vi har gått igenom **hur man kör OCR** i C# från början till slut, visat hur man **extraherar arabisk text**, **konverterar bild till text**, **läser text från PNG**, och svarat på **hur man extraherar text** i en rad olika **scenarier**. Exempelkoden är komplett, självständig och klar att klistra in i vilket .NET‑konsolprojekt som helst.

Nästa steg? Prova att **byta** `OcrLanguage.Arabic` mot **Koreanska** eller **Serbiska kyrilliska** för att se bibliotekets flerspråkiga kraft. Experimentera med förbehandlingsflaggorna **för att öka noggrannheten** på brusiga skanningar, eller **integrera** OCR‑rutinen i ett **web‑API** så att **användare** kan **ladda upp** bilder och få **omedelbara** textresultat.

Lycka till med kodandet, och må dina OCR‑resultat alltid vara **kristallklara**!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}