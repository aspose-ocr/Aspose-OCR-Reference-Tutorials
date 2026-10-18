---
category: general
date: 2026-03-21
description: Lär dig hur du räta upp bildfiler och känner igen textbilder med Aspose
  OCR. Konvertera jpg till text och korrigera bildrotation med några rader C#‑kod.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: sv
og_description: Hur man räta upp en bild och extraherar text från JPEG-filer med Aspose
  OCR. Följ den här steg‑för‑steg‑guiden för att konvertera jpg till text och korrigera
  bildrotation.
og_title: Hur man räta upp en bild i C# – Snabb Aspose OCR-handledning
tags:
- OCR
- C#
- Aspose
title: Hur man räta upp en bild i C# – Komplett guide med Aspose OCR
url: /sv/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man räta upp bild i C# – Komplett guide med Aspose OCR

Har du någonsin undrat **hur man räta upp bild** filer som kom ut från en scanner snett? Du är inte ensam—många utvecklare stöter på detta problem när de försöker extrahera text från kvitton, fakturor eller handskrivna anteckningar. Den goda nyheten är att med Aspose OCR kan du korrigera bildrotation och hämta ren, sökbar text på bara några rader.

I den här handledningen går vi igenom hela processen: från att installera biblioteket, aktivera automatisk räta upp, till att känna igen text i bild och slutligen konvertera en JPG till text. I slutet har du en färdig‑att‑köra konsolapp som **recognize text jpg** filer utan att manuellt rotera dem först.

## Vad du behöver

- **.NET 6.0** eller senare (koden fungerar på .NET Core och .NET Framework lika)  
- **Aspose.OCR for .NET** NuGet‑paket – version 23.12 eller nyare rekommenderas  
- Ett exempel på **skewed JPEG** (t.ex. `skewed_receipt.jpg`) placerad någonstans där din app kan läsa den  
- Visual Studio, VS Code eller någon annan C#‑redigerare du föredrar  

Inga andra tredjepartsverktyg krävs. Biblioteket hanterar räta upp, OCR och till och med språkdetection internt.

![exempel på hur man räta upp bild](/images/deskew-example.png "hur man räta upp bild med Aspose OCR")

## Steg 1: Ställ in projektet och installera Aspose.OCR

För att hålla det organiserat, starta ett nytt konsolprojekt:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package`‑raden hämtar **Aspose.OCR**‑binärerna plus alla inhemska beroenden. Om du är på Windows får du de inhemska DLL‑filerna automatiskt; på Linux/macOS kan du behöva paketet `libgdiplus`, men det är en engångsinstallation.

## Steg 2: Aktivera automatisk räta upp (korrigera bildrotation)

Öppna nu `Program.cs` och ersätt dess innehåll med koden nedan. Den viktiga raden här är `ocrEngine.Settings.Deskew = true;` – det är flaggan som talar om för motorn **hur man räta upp bild** automatiskt.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Varför aktivera räta upp?

När en scanner matar in en sida i en vinkel är textbaslinjen sned. Traditionella OCR‑motorer skulle läsa varje tecken som en sned version, vilket kraftigt minskar noggrannheten. Genom att sätta `Deskew = true` kör Aspose OCR en snabb Hough‑transform under huven, roterar bitmapen tillbaka till horisontell och utför sedan igenkänning. Resultatet är detsamma som om du manuellt roterade bilden i Photoshop—men snabbare och helt automatiserat.

## Steg 3: Känn igen text i bild och konvertera JPG till text

`Recognize`‑anropet gör två saker samtidigt:

1. **Räta upp** bilden (eftersom vi satte flaggan).  
2. **Extraherar** den textuella innehållet, vilket returneras i ett `OcrResult`‑objekt.

Du kan behandla `ocrResult.Text` som en vanlig sträng, skriva den till en fil eller skicka den vidare i bearbetningspipelines. Om du behöver de råa förtroendesiffrorna per ord, ger `ocrResult.Words` dig en samling med `Confidence`‑värden.

### Exempel på utdata

Om vi antar att `skewed_receipt.jpg` innehåller ett enkelt kvitto, kan du se något liknande:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Lägg märke till hur siffrorna ligger snyggt i linje trots att originalbilden var roterad med cirka 7°. Det är magin med **korrigera bildrotation** som är inbyggd i biblioteket.

## Steg 4: Köra exemplet och verifiera resultat

Kompilera och kör:

```bash
dotnet run
```

Om allt är korrekt konfigurerat kommer du att se den extraherade texten skriven till konsolen. Om du får ett undantag som `FileNotFoundException`, dubbelkolla sökvägen till din JPEG och säkerställ att filen är läsbar.

### Vanliga fallgropar & pro‑tips

- **Stora bilder** – OCR‑minnesanvändning växer med bildens dimensioner. Ändra storlek på alltför stora filer (t.ex. > 3000 px bredd) innan du matar dem till motorn.  
- **Icke‑latinska skript** – Som standard antar motorn engelska. Sätt `ocrEngine.Settings.Language = OcrLanguage.French;` (eller något annat stödd språk) om du behöver **recognize text image** i andra alfabet.  
- **Batch‑behandling** – För många filer, återanvänd samma `OcrEngine`‑instans; att skapa en ny motor per fil ger onödig overhead.  
- **Kvalitetskontroll** – Efter räta upp kan du exportera den korrigerade bitmapen via `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` för att visuellt verifiera rotationsfixen.

## Fullt fungerande exempel (allt tillsammans)

Nedan är det kompletta, självständiga programmet som du kan kopiera‑klistra in i `Program.cs`. Det inkluderar kommentarer, felhantering och ett valfritt steg för att spara den räta upp bilden.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Att köra programmet kommer att **recognize text jpg** filer, automatiskt korrigera eventuell snedvridning och skriva ut ren, sökbar text till konsolen.

## Avslutning

Du har nu ett robust, produktionsklart kodexempel som visar **hur man räta upp bild** filer och extrahera deras innehåll med Aspose OCR. Metoden fungerar för kvitton, fakturor, skannade kontrakt eller vilken JPEG som helst där texten inte är helt horisontell. 

Nästa steg du kan utforska:

- **Batch‑behandling** av en mapp med JPEG‑filer och skriva varje resultat till en `.txt`‑fil (kopplar tillbaka till *convert jpg to text*).  
- Integrera OCR‑steget i ett ASP.NET Core‑API så att klienter kan ladda upp bilder och få JSON‑formaterad text.  
- Experimentera med olika OCR‑inställningar som `ocrEngine.Settings.Language` eller `ocrEngine.Settings.RecognitionMode` för att förbättra noggrannheten för icke‑engelska dokument.  

Prova det, justera inställningarna och låt motorn göra det tunga arbetet. Som alltid, om du stöter på ett problem eller har en smart optimering att dela, lämna en kommentar nedan. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}