---
category: general
date: 2026-02-13
description: Hur man använder OCR i C# för att extrahera text från en bild, känna
  igen text från ett foto eller JPG, och köra OCR på en bild utan internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: sv
og_description: Hur man använder OCR i C# för att extrahera text från bild, känna
  igen text från foto och köra OCR på en bild med ett komplett, körbart exempel.
og_title: Hur man använder OCR i C# – Extrahera text från bild
tags:
- OCR
- C#
- Image Processing
title: Hur man använder OCR i C# – Extrahera text från bild och känna igen text från
  foto
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

" incomplete; we can translate as is? The original ends with "You might". Probably incomplete but keep as is? Should translate "Du kanske". Keep as is.

Then closing shortcodes.

Now produce final content with all translations.

Be careful to keep markdown formatting exactly.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från bild och känna igen text från foto

Har du någonsin undrat **hur man använder OCR** för att dra ut ord från en skärmdump, ett skannat kvitto eller ett slumpmässigt foto du tog med din telefon? Du är inte ensam. I många verkliga appar måste vi omvandla bilder till sökbar text, och att göra det lokalt—utan en opålitlig internetanslutning—kan kännas som ett pussel.

Det är därför den här guiden visar dig ett steg‑för‑steg‑sätt att **extrahera text från bild**‑filer med en C# OCR‑motor, och den täcker också hur man **känner igen text från foto**, **känner igen text från JPG**, och **kör OCR på bild**‑filer som ligger direkt på din disk. I slutet har du ett komplett, kopiera‑och‑klistra‑klart program som fungerar direkt ur lådan.

## Vad du kommer att lära dig

- Hur man konfigurerar en OCR‑motor för förenklad kinesiska (eller vilket språk du än ansluter).  
- Den exakta koden som behövs för att **ladda resurser** från en lokal mapp—inga nätverksanrop krävs.  
- Hur man **känner igen text från foto**‑filer såsom JPEG, PNG eller BMP.  
- Tips för att hantera vanliga kantfall som saknade modellfiler eller ej stödda bildformat.  
- Ett komplett, körbart exempel som du kan klistra in i Visual Studio och se resultat omedelbart.

### Förutsättningar

- .NET 6.0 eller senare (API:et som används här riktar sig mot .NET Standard 2.0, så äldre versioner fungerar också).  
- Grundläggande kunskap om C# och Visual Studio (eller någon IDE du föredrar).  
- OCR‑biblioteket du använder (kodsnutten förutsätter en fiktiv `OcrEngine`‑klass som levereras med språkmodeller).  
- En mapp som innehåller de nödvändiga språkmodellfilerna—tänk på den som “hjärnan” som motorn använder för att läsa kinesiska tecken.

> **Proffstips:** Om du ännu inte har de kinesiska modellfilerna, ladda ner dem en gång från leverantörens webbplats och placera dem i en mapp som `C:\OcrResources`. Motorn kommer aldrig behöva gå online igen.

---

![Diagram som visar OCR-processen på ett foto](path/to/ocr-diagram.png "Diagram som visar OCR-processen på ett foto")

## Så använder du OCR: Ställ in motorn

Det första du behöver är en instans av OCR‑motorn, konfigurerad för det språk du är intresserad av. I den här tutorialen riktar vi oss mot **Förenklad kinesiska**, men att byta `OcrLanguage.ChineseSimplified` mot `OcrLanguage.English` (eller något annat enum‑värde) är bara en radändring.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Varför detta är viktigt:**  
Att sätta `Language`‑egenskapen talar om för motorn vilken teckenuppsättning den ska förvänta sig. `ResourceFolder` är där motorn letar efter neurala nätverksvikter och språkordböcker—tänk på den som hjärnans minnesbank. Om du pekar på fel mapp kommer motorn att kasta ett `FileNotFoundException` och du fastnar.

## Extrahera text från bild – Ladda resurser

Innan motorn faktiskt kan läsa något måste du ladda de modellfilerna i minnet. Detta steg är **avgörande** eftersom det undviker ett nätverksanrop varje gång du bearbetar en bild.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Vad kan gå fel?**  
Om sökvägen till mappen är fel eller filerna är korrupta, kommer `LoadResources()` att kasta ett undantag. `try/catch`‑blocket ovan visar hur du hanterar fel på ett graciöst sätt—något du ofta behöver i produktion.

## Känn igen text från foto – Köra OCR

Nu blir det roligt: mata in en bildfil till motorn och få tillbaka den igenkända texten. Detta är kärnan i **kör OCR på bild**‑scenarier, oavsett om bilden är en JPEG, PNG eller till och med en BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage`‑metoden returnerar ett `RecognitionResult` (eller vad ditt SDK kallar det) som vanligtvis innehåller:

- `Text` – den rena texttranskriptionen.  
- `Confidence` – ett numeriskt värde som visar hur säker motorn är på varje rad.  
- `BoundingBoxes` – valfria koordinater för var varje ord finns i bilden.

**Varför du kan bry dig om förtroendet:**  
Om du bygger ett verktyg för data‑inmatningsautomatisering kan du sätta ett tröskelvärde (t.ex. 0.85) och be användaren bekräfta rader med låg förtroendegrad. Det förbättrar den totala noggrannheten dramatiskt.

## Känn igen text från JPG – Hantera olika format

Många utvecklare antar att OCR bara fungerar med PNG, men moderna motorer hanterar **JPG**‑filer utan problem. Det enda haken är att JPEG‑komprimering kan introducera artefakter som förvirrar modellen.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Om du inte har en `DenoiseAndDeskew`‑hjälpfunktion, erbjuder många bibliotek (t.ex. OpenCvSharp) dessa funktioner. Huvudpoängen är: **kör OCR på bild**‑filer efter en liten rengöring om de kommer från en skanner eller en telefonkamera.

## Kör OCR på bild – Tips, kantfall och bästa praxis

### 1. Minneshantering
Att ladda stora språkmodeller kan ta hundratals megabyte. Disposera motorn när du är klar:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Batch‑behandling
Om du behöver bearbeta dussintals foton, ladda resurser en gång och loopa sedan:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Fler‑språksscenarier
Du kan byta språk i farten genom att återtilldela `ocrEngine.Language` och anropa `LoadResources()` igen. Var bara medveten om den extra laddningstiden.

### 4. Hantera tomma resultat
Ibland returnerar motorn en tom sträng. Det betyder oftast att bilden är för suddig eller att textfärgen smälter in i bakgrunden. En snabb kontroll:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Säkerhetsaspekter
Mata aldrig in användaruppladdade filer direkt i OCR‑motorn utan validering. Minst bör du verifiera filändelse och storlek, och överväga att skanna efter skadlig kod.

## Komplett fungerande exempel

Nedan är ett enda, självständigt program som du kan kopiera in i ett nytt Console App‑projekt. Det demonstrerar **hur man använder OCR**, **extrahera text från bild**, **känna igen text från foto**, **känna igen text från JPG**, och **kör OCR på bild**—allt i ett.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Förväntad utskrift (exempel):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Din faktiska text kommer att skilja sig beroende på bildens innehåll, men du bör se ett block med Unicode‑tecken skrivet till konsolen tillsammans med en förtroendeprocent.

## Slutsats

Vi har gått igenom **hur man använder OCR** i C# från början till slut—konfigurera motorn, ladda språkresurser och slutligen **känna igen text från foto** eller **JPG**‑filer utan att någonsin röra internet. Genom att följa stegen ovan kan du **extrahera text från bild**‑filer, **kör OCR på bild**‑tillgångar, och hantera de vanligaste fallgroparna som får nybörjare att snubbla.

Redo för nästa utmaning? Prova att mata in en PDF‑sida konverterad till en bild, eller experimentera med ett annat språkpaket för att se hur förtroendesiffrorna förändras. Du kanske

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}