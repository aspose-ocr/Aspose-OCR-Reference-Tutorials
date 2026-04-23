---
category: general
date: 2026-02-13
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du läser text
  från jpg och kör OCR på bilden med ett komplett, körbart exempel.
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: sv
og_description: Extrahera text från bild med Aspose OCR i C#. Den här guiden visar
  hur du läser text från jpg och kör OCR på bilden med ett komplett kodexempel.
og_title: Extrahera text från bild med Aspose OCR – C# Snabbstart
tags:
- C#
- OCR
- Aspose
title: Extrahera text från bild med Aspose OCR – C# snabbstart
url: /sv/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med Aspose OCR – C# Quickstart

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket bibliotek du ska välja? Du är inte ensam—utvecklare kämpar ständigt med att läsa text från jpg‑filer, särskilt när innehållet är i ett icke‑latinskt skriftsystem. De goda nyheterna? Med Aspose OCR kan du köra OCR på bildfiler med bara några rader C#‑kod, och biblioteket tar hand om att ladda ner språkpaket vid behov.

I den här handledningen går vi igenom ett komplett, end‑to‑end‑exempel som visar hur du **extraherar text från bild** med Aspose OCR, begränsar igenkänningen till ryska och skriver ut resultatet till konsolen. När du är klar kommer du kunna läsa text från jpg‑filer, köra OCR på bildresurser av vilken storlek som helst och anpassa koden för andra språk med minimala förändringar.

> **Vad du kommer att lära dig**
> * Hur du installerar och refererar Aspose OCR i ett .NET‑projekt.  
> * De exakta stegen för att **extrahera text från bild**—initiera motorn, välja språk och anropa `RecognizeImage`.  
> * Varför du kanske vill låsa motorn till ett enda språkpaket (prestanda, noggrannhet).  
> * Vanliga fallgropar som saknade filer eller ej stödda format, och hur du hanterar dem på ett smidigt sätt.  

## Förutsättningar

| Krav | Orsak |
|-------------|--------|
| .NET 6.0 SDK or later | Aspose OCR riktar sig mot .NET Standard 2.0+, så .NET 6 ger dig de senaste runtime‑funktionerna. |
| Visual Studio 2022 (or any IDE you like) | Användbart för felsökning, men inte strikt nödvändigt. |
| An image file (`cyrillic_sample.jpg`) that contains Cyrillic text | Vi kommer att använda den här filen för att demonstrera **läsa text från jpg**. |
| Internet connection (first run only) | Aspose OCR laddar ner språkpaket vid behov. |

Om du saknar någon av dessa, hämta dem nu—det behövs ingen omstart efter att SDK:n installerats.

## Steg 1: Installera Aspose OCR NuGet‑paket

Det första du behöver är Aspose OCR‑biblioteket. Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Detta kommando hämtar den senaste stabila versionen (från och med februari 2026 är den 23.12) och lägger till den i din `.csproj`. Paketet innehåller den centrala OCR‑motorn och en lättviktsnedladdare för språkpaket, så du behöver inte paketera stora filer med din app.

**Proffstips:** Om du arbetar bakom en företagsproxy, sätt miljövariabeln `http_proxy` innan du kör kommandot för att undvika nedladdningsfel.

## Steg 2: Skapa ett konsolapplikations‑skelett

Låt oss sätta upp en minimal konsolapp som kommer att hysa vår OCR‑logik. Öppna `Program.cs` (eller skapa en ny fil) och klistra in skelettet nedan. Lägg märke till `using`‑direktiven högst upp—de importerar Aspose OCR‑namnrymderna.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

Vid detta tillfälle kompilerar projektet, men det gör ännu inget. De kommande avsnitten kommer att fylla i **run OCR on image**‑arbetsflödet.

## Steg 3: Initiera OCR‑motorn (Extrahera text från bild)

För att **extrahera text från bild** behöver du först en `OcrEngine`‑instans. Aspose OCR laddar ner språkresurser på begäran första gången de behövs, vilket håller den initiala binären liten.

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

Varför initiera här istället för ett statiskt fält? Att göra det inuti `Main` garanterar att eventuella undantag (som saknade inhemska beroenden) visas tidigt, vilket underlättar felsökning.

## Steg 4: Begränsa igenkänning till önskat språk (Läsa text från JPG)

Om du vet språket på den text du skannar—t.ex. ryska—kan du förbättra både hastighet och noggrannhet genom att sätta `Language`‑egenskapen. Detta är särskilt användbart när du **läser text från jpg**‑filer som innehåller kyrilliska tecken.

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

Bakom kulisserna kommer Aspose OCR att ladda ner det ryska språkpaketet första gången du kör den här raden. Efterföljande körningar återanvänder det cachade paketet, så det finns ingen nätverkspåverkan efter den första nedladdningen.

> **Varför låsa språket?**  
> * **Prestanda:** Motorn hoppar över skanning av tecken utanför det valda alfabetet.  
> * **Noggrannhet:** Språkspecifika heuristiker (som vanliga ords frekvens) tillämpas, vilket minskar felaktiga igenkänningar.  

Om du behöver stödja flera språk kan du skicka en kommaseparerad lista, t.ex. `OcrLanguage.English | OcrLanguage.Russian`.

## Steg 5: Utför OCR på mål‑JPG (Kör OCR på bild)

Nu kör vi faktiskt **OCR på bild**. Ange den fullständiga sökvägen till din JPG‑fil—Aspose OCR accepterar många format (`.png`, `.bmp`, `.tif`, etc.), men vi håller oss till `.jpg` för den här demonstrationen.

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

Om filen inte hittas kastar `RecognizeImage` ett `FileNotFoundException`. För att göra handledningen robust, omslut anropet i ett try‑catch‑block:

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

`RecognizeImage`‑metoden returnerar ett `OcrResult`‑objekt vars `Text`‑egenskap innehåller den rena textutdragningen. Du kan också komma åt `Boxes` för avgränsningsruta‑data om du senare behöver layoutinformation.

## Steg 6: Verifiera utskriften

När du kör programmet (`dotnet run`) bör du se något liknande:

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

Om utskriften ser förvrängd ut, dubbelkolla att bilden är tydlig och att du har valt rätt språk. Suddiga eller lågkontrastbilder är den vanligaste orsaken till dåliga OCR‑resultat.

### Edge Cases & Vanliga frågor

| Situation | Vad att göra |
|-----------|--------------|
| **Bilden innehåller flera språk** | Sätt `ocrEngine.Language` till en kombination, t.ex. `OcrLanguage.English | OcrLanguage.Russian`. |
| **Stort antal bilder** | Återanvänd samma `OcrEngine`‑instans för flera filer; den cachar språkdata. |
| **Kör på en huvudlös server** | Ingen UI krävs—Aspose OCR fungerar bra i Docker eller Azure Functions. |
| **Behöver högre noggrannhet** | Justera `ocrEngine.Options` (t.ex. `ocrEngine.Options.Denoise = true`). |
| **Ej stödd filformat** | Konvertera bilden till ett stödd format (PNG eller JPG) innan du anropar `RecognizeImage`. |

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som innehåller alla stegen ovan. Spara det som `Program.cs` och kör det från kommandoraden.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**Förväntad konsolutskrift** (förutsatt att exempelbilden innehåller frasen “Пример текста на кириллице”):

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

Om du ersätter bilden med ett engelskt foto och ändrar `ocrEngine.Language = OcrLanguage.English;`, kommer samma kod att **läsa text från jpg** på engelska utan ytterligare ändringar.

## Bonus: Köra OCR på flera filer

Ofta behöver du **köra OCR på bild**‑samlingar. Här är ett snabbt kodexempel som loopar igenom en mapp:

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

Motorn återanvänder det tidigare nedladdade språkpaketet, så batch‑körningen blir effektiv.

## Slutsats

Du har nu ett robust, produktionsklart mönster för att **extrahera text från bild** med Aspose OCR i C#. Handledningen täckte allt från att installera NuGet‑paketet till att hantera fel och skala till flera filer. Oavsett om du **läser text från jpg**‑resurser, skannar PDF‑filer eller bygger en dokument‑automatiseringspipeline, gäller samma tillvägagångssätt—byt bara språkpaketet eller justera OCR‑alternativen.

Redo för nästa steg? Prova:

* Experimentera med andra språk (t.ex. `OcrLanguage.ChineseSimplified`).  
* Extrahera layoutinformation via `recognizedResult.Boxes`.  
* Integrera OCR‑flödet i ett ASP.NET Core‑API så att andra tjänster kan begära textutdragning på begäran.

Lycklig kodning, och må dina bilder alltid vara tillräckligt skarpa för perfekt OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}