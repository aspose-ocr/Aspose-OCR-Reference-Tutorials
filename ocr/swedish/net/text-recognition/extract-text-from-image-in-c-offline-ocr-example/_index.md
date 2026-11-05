---
category: general
date: 2026-02-09
description: Extrahera text från bild med C# offline OCR. Ett komplett C# OCR‑exempel
  visar hur man laddar bild för OCR, känner igen kyrillisk text och extraherar text
  från pass.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: sv
og_description: Extrahera text från bild med C# offline OCR. Lär dig ett steg‑för‑steg
  C# OCR‑exempel som laddar en bild för OCR, känner igen kyrillisk text och extraherar
  text från ett pass.
og_title: Extrahera text från bild i C# – Offline OCR‑guide
tags:
- OCR
- C#
- Aspose
title: Extrahera text från bild i C# – Offline OCR‑exempel
url: /sv/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---






{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i C# – Offline OCR‑exempel

Har du någonsin behövt **extrahera text från bild** men fastnat på nätverksberoende API:er? Du är inte ensam. Många utvecklare stöter på problem när OCR‑tjänsten försöker ladda ner språkpaket vid körning, särskilt i begränsade miljöer.

I den här guiden går vi igenom ett **c# ocr example** som körs helt offline, laddar en bild för OCR och känner igen kyrillisk text från ett pass. När du är klar har du ett färdigt program som skriver ut ren‑textinnehållet från vilken stödjande bild som helst direkt till konsolen.

## Vad du kommer att lära dig

- Hur du konfigurerar Aspose.OCR för offline‑bearbetning.  
- Den exakta koden för att **load image for OCR** från disk.  
- Hur du ställer in motorn för att **recognize cyrillic text**.  
- Ett komplett, copy‑paste‑klart **c# ocr example** som extraherar text från ett pass‑liknande foto.  

Ingen förkunskap om Aspose krävs; bara ett .NET 6 (eller senare) SDK och Visual Studio 2022 (eller VS Code) räcker.

---

![Extrahera text från bild med Aspose OCR på ett passfoto](/images/ocr-passport.jpg "extrahera text från bild")

## Steg 1: Ställ in projektet för att extrahera text från bild

Innan du skriver någon kod, se till att Aspose.OCR‑NuGet‑paketet är tillagt i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

> **Proffstips:** Använd flaggan `--version` för att låsa till den senaste stabila versionen (t.ex. `13.9.0`). Detta garanterar kompatibilitet med .NET 6.

Att skapa en ny konsolapp är lika enkelt som:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Nu har du en ren startpunkt där vi kommer att **extract text from image** utan att någonsin röra internet.

## Steg 2: Ladda bild för OCR – Läs passfotot

Det första OCR‑motorn behöver är en bitmap eller stream som representerar bilden. I vårt scenario **load image for OCR** från en lokal fil som heter `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Varför detta är viktigt:** Att leverera en stream istället för en rå `Bitmap` låter Aspose hantera formatdetektering internt, vilket minskar boilerplate‑kod och potentiella buggar.

## Steg 3: Konfigurera offline‑läge och välj kyrilliskt språk

Aspose.OCR kan ladda ner språkmodeller i farten, men det går emot syftet med en offline‑lösning. Stäng av nätverksanrop och tala explicit om för motorn vilket språk som ska användas.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Edge case:** Om du senare behöver känna igen latinska tecken i samma dokument, lägg bara till `OcrLanguage.English` i arrayen. Motorn hanterar flerspråkig detektion automatiskt.

## Steg 4: Kör OCR‑motorn och känna igen kyrillisk text

Nu **recognize text from passport**‑liknande bilder. Metoden `Recognize` returnerar ett rikt resultatobjekt som innehåller ren text, förtroendescore och avgränsningsrutor.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Förväntad konsolutskrift

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Om resultatet ser förvrängt ut, dubbelkolla att källbilden är tydlig och att språkpaketet för `OfflineMode` för kyrilliska finns i Aspose‑installationsmappen (vanligtvis `\Aspose.OCR\resources\languages`).

## Komplett C# OCR‑exempel – Fullständig källkod

Nedan är **c# ocr example** i sin helhet. Kopiera och klistra in i `Program.cs` och kör `dotnet run`. Allt du behöver för att **extract text from image** finns här.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Köra exemplet

```bash
dotnet run
```

Du bör se att konsolen skriver ut passuppgifterna på kyrilliska. Det är ögonblicket då du vet att din **extract text from image**‑pipeline fungerar.

## Vanliga fallgropar & hur du åtgärdar dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|--------|
| Tom `PlainText` | Fel språkmodell eller bilden för mörk | Säkerställ att `OfflineMode`‑språket inkluderar `Cyrillic` och öka bildkontrasten |
| `System.DllNotFoundException` | Saknade inhemska Aspose OCR‑binärer | Återinstallera NuGet‑paketet eller kopiera `Aspose.OCR.Native.dll` till utmatningsmappen |
| Långsam prestanda på stora bilder | Motorn bearbetar full upplösning | Skala ner bilden till ≤ 1500 px i bredd innan du skickar den till `ImageStream` |
| Förvrängda tecken | Bilden roterad felaktigt | Använd `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` innan du skapar streamen |

## Nästa steg – Utöka offline OCR‑arbetsflödet

- **Load image for OCR** från en `MemoryStream` när du hanterar uppladdade filer i ASP.NET Core.  
- Byt till **recognize text from passport** i batch‑läge genom att loopa över en mapp med pass‑skanningar.  
- Kombinera resultatet med **regular expressions** för att extrahera fält som passnummer eller födelsedatum.  
- Experimentera med `ocrEngine.Configuration.UseParallelProcessing = true` för fler‑kärnors hastighetsökning.

---

### Slutsats

Vi har just visat hur du **extract text from image** med en helt offline C# OCR‑pipeline. Det korta, självständiga **c# ocr example** laddar en bild, konfigurerar motorn för att **recognize cyrillic text**, och skriver ut den extraherade passinformationen – utan någon nätverksförfrågan.

Känn dig fri att justera koden, lägga till fler språk eller koppla utdata till en databas. Himlen är gränsen när du har bemästrat grunderna för att **load image for OCR** och känna igen text från en pass‑liknande foto.

Har du frågor eller vill dela dina egna justeringar? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}