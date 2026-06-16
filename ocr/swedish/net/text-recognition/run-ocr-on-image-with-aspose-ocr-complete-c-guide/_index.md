---
category: general
date: 2026-02-17
description: Kör OCR på en bild med Aspose OCR i C#. Lär dig hur du extraherar text
  från jpg, förbehandlar bilden för OCR och laddar bilden för OCR med steg‑för‑steg‑kod.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: sv
og_description: Kör OCR på bild med Aspose OCR i C#. Den här guiden visar hur du extraherar
  text från jpg, förbehandlar bilden och laddar bilden för OCR.
og_title: Kör OCR på bild med Aspose OCR – Komplett C#‑guide
tags:
- Aspose OCR
- C#
- Image Processing
title: Kör OCR på bild med Aspose OCR – Komplett C#‑guide
url: /sv/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på bild med Aspose OCR – Komplett C#-guide

Har du någonsin behövt **run OCR on image** filer men varit osäker på var du ska börja? I många verkliga applikationer – tänk fakturaskannrar eller kvittospårning – är det första hindret att få pålitlig text ur en JPEG. Den goda nyheten? Med Aspose OCR kan du **run OCR on image** filer med bara några rader C#‑kod, och du kommer också att lära dig hur du **extract text from jpg**, **preprocess image for OCR**, och **load image for OCR** utan att leta igenom spridda dokument.

I den här handledningen går vi igenom ett komplett, kopiera‑och‑klistra‑klart exempel som visar exakt hur du ställer in motorn, lägger till användbara förbehandlingsfilter, matar in en bild i igenkännaren och skriver ut resultatet till konsolen. När du är klar har du ett självständigt program som du kan släppa in i vilket .NET‑projekt som helst och omedelbart börja hämta text från bilder.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även på .NET Core)  
- Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)  
- En exempel‑JPEG (`input.jpg`) placerad i en mapp du kan referera till  
- Grundläggande förståelse för C#‑syntax (inget exotiskt)

Om du redan har dessa delar på plats, toppen – låt oss dyka in. Om inte, hämta NuGet‑paketet och en testbild; resten av guiden förutsätter att du har gjort det.

## Steg 1: Skapa OCR‑motorn – Kärnan i att köra OCR på bild

Det första du måste göra för att **run OCR on image** data är att instansiera `OcrEngine`. Detta objekt innehåller all konfiguration och status som behövs för igenkänning.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Varför detta är viktigt:** `OcrEngine` är porten till Asposes igenkänningspipeline. Utan den kan du inte komma åt filter, språkpaket eller `Recognize`‑metoden.

## Steg 2: Lägg till förbehandlingsfilter – Öka noggrannheten när du **extract text from jpg**

Bilder direkt från en kamera är sällan perfekta. Snedvridna vinklar eller slumpmässigt brus kan få även de bästa OCR‑algoritmerna att misslyckas. Att lägga till ett par filter innan du **extract text from jpg** kan dramatiskt förbättra resultaten.

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

**Proffstips:** Om dina källbilder redan är rena kan du hoppa över `DenoiseGaussianFilter`. För mycket utjämning kan radera svaga tecken.

## Steg 3: Ladda bild för OCR – Mata in JPEG‑en i motorn

Nu kommer delen där du **load image for OCR**. Aspose tillhandahåller en bekväm `ImageStream.FromFile`‑hjälpare som omsluter en filsökväg till en ström som motorn förstår.

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

**Edge case:** Om filen inte finns, kastar `FromFile` ett `FileNotFoundException`. Omge anropet med try/catch om du förväntar dig saknade filer vid körning.

## Steg 4: Hämta och visa den igenkända texten

Till sist, när motorn är klar, kan du komma åt resultatet som ren text via `Text`‑egenskapen. Att skriva ut det till konsolen räcker för en snabb demo, men du kan också skriva det till en databas eller en textfil.

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Förväntad output**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

Det exakta innehållet beror på bilden du matar in, men du bör se ett snyggt formaterat textblock istället för nonsens.

![Diagram som visar OCR‑pipeline – run OCR on image, preprocess, load, recognize](/images/ocr-pipeline.png "run OCR on image pipeline diagram")

### Varför varje steg är viktigt

| Steg | Syfte | Vad händer om du hoppar över |
|------|-------|------------------------------|
| **Skapa motor** | Initierar interna strukturer | Ingen igenkännare tillgänglig – du får ett `NullReferenceException`. |
| **Lägg till filter** | Förbättrar noggrannheten genom att korrigera rotation och brus | Snedvridna eller brusiga bilder ger förvrängd output. |
| **Ladda bild** | Förser motorn med den råa bitmapen | Motorn har inget att bearbeta, vilket resulterar i ett tomt `Text`‑fält. |
| **Läs resultat** | Extraherar ren‑textsträngen för vidare användning | Du har kört OCR men ser aldrig resultatet – inte särskilt användbart! |

## Vanliga variationer & hur du finjusterar processen

### Ändra språkpaketet

Aspose OCR stödjer flera språk direkt ur lådan. Om du behöver **run OCR on image** filer som innehåller, till exempel, fransk eller tysk text, sätt `Language`‑egenskapen innan du anropar `Recognize`.

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### Hantera flersidiga PDF‑filer

Om din källa är en flersidig PDF snarare än en enskild JPEG, kan du först konvertera varje sida till en bild (med Aspose.PDF) och sedan mata in varje bild i samma pipeline. Att loopa över sidor är enkelt:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### Hantera stora filer

När du bearbetar högupplösta bilder kan minnesförbrukningen skjuta i höjden. Överväg att nerprova bilden innan du **load image for OCR**:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## Fullt, färdigt‑att‑köra‑exempel

Nedan är det kompletta programmet som inkluderar allt vi har diskuterat. Kopiera‑klistra in det i ett nytt konsolprojekt, ersätt `YOUR_DIRECTORY` med mappen som innehåller `input.jpg`, och tryck **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### Verifiera resultatet

1. Kör programmet.  
2. Kontrollera konsolen – du bör se texten som fanns på `input.jpg`.  
3. Om output ser förvrängd ut, försök justera `Sigma`‑värdet på `DenoiseGaussianFilter` eller lägg till ytterligare filter som `ContrastEnhancementFilter`.

## Sammanfattning & nästa steg

Vi har precis gått igenom hur man **run OCR on image** filer med Aspose OCR, från att sätta upp motorn till att leverera ren, läsbar text. De viktigaste slutsatserna:

- Skapa en `OcrEngine`‑instans.  
- **Preprocess image for OCR** med filter som `DeskewFilter` och `DenoiseGaussianFilter`.  
- **Load image for OCR** med `ImageStream.FromFile`.  
- Anropa `Recognize` och läs `ocrResult.Text` för att **extract text from jpg**.

Vill du gå längre? Prova dessa idéer:

- **Batch processing** – läs en mapp med JPEG‑filer och skriv ut varje resultat till en separat `.txt`‑fil.  
- **Integrate with Azure Blob Storage** – hämta bilder från molnet, kör OCR, och lagra sedan tillbaka texten.  
- **Combine with NLP** – mata den extraherade texten i en språkförståelse‑modell för att automatiskt kategorisera fakturor.  

Känn dig fri att experimentera med olika filterkombinationer, språkpaket, eller till och med byta till PNG‑ och TIFF‑filer – samma pipeline fungerar så länge du **load image for OCR** korrekt.

---

Om du stöter på några problem, lämna en kommentar nedan eller kolla Aspose OCR‑dokumentationen för avancerade inställningar. Lycka till med kodandet, och njut av att förvandla bilder till sökbar text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}