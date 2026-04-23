---
category: general
date: 2026-03-17
description: Extrahera text från PNG med Aspose OCR i C#. Lär dig att läsa text från
  bild, bearbeta kvitto‑OCR och skapa en OCR‑motor med GPU‑acceleration.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: sv
og_description: Extrahera text från PNG med Aspose OCR. Den här guiden visar hur du
  läser text från en bild, bearbetar kvitto‑OCR och skapar en OCR‑motor effektivt.
og_title: Extrahera text från PNG – Läs text från bild med OCR
tags:
- OCR
- CSharp
- Aspose
title: Extrahera text från PNG – Läs text från bild med OCR
url: /sv/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

Will produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PNG – Läs text från bild med OCR

Har du någonsin behövt **extrahera text från PNG** men varit osäker på vilket bibliotek som ger pålitliga resultat? Du är inte ensam—utvecklare frågar ständigt: “Hur läser jag text från bildfiler som kvitton utan att skriva ett eget neuralt nätverk?” Den goda nyheten är att Aspose OCR sköter det tunga arbetet åt dig, och du kan till och med aktivera GPU för en hastighetsökning.

I den här handledningen går vi igenom allt du behöver för att **processa kvitto‑OCR**, från att installera NuGet‑paketet till att skapa en OCR‑motor som förstår din PNG‑fil. I slutet har du en fristående konsolapp som läser ett kvittobild, skriver ut den igenkända texten och visar hur du finjusterar motorn för olika scenarier. Inga externa dokument, bara ren kod och tydliga förklaringar.

## Förutsättningar

- .NET 6.0 SDK (eller någon nyare .NET‑version)  
- Visual Studio 2022 eller VS Code med C#‑tillägg  
- Ett stödjande NVIDIA‑GPU med den senaste drivrutinen (valfritt, men rekommenderas för GPU‑läge)  
- **Aspose.OCR**‑NuGet‑paketet (`dotnet add package Aspose.OCR`)  

Om du inte har ett GPU kan du fortfarande köra exemplet i CPU‑läge—hoppa bara över raderna för GPU‑konfiguration.

## Steg 1: Installera Aspose.OCR och skapa projektet

Skapa först ett nytt konsolprojekt och lägg till Aspose OCR‑biblioteket.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Varför detta är viktigt: `Aspose.OCR`‑paketet innehåller OCR‑motorn, bildläsare och valfritt GPU‑stöd. Att lägga till det via NuGet säkerställer att du får den senaste stabila versionen (från och med mars 2026 är det 23.10).

## Steg 2: Importera namnrymder och skapa OCR‑motorn

Öppna nu **Program.cs** och lägg till de nödvändiga `using`‑direktiven. Instansiera sedan motorn.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Proffstips:** Om du får `System.DllNotFoundException` på maskiner utan GPU, kommentera bara bort de två raderna som sätter `EngineMode` och `GpuDeviceId`. Motorn återgår automatiskt till CPU.

## Steg 3: Ladda PNG‑bilden du vill extrahera text från

Aspose OCR kan läsa bilder direkt från en filsökväg, en ström eller till och med en byte‑array. I detta demo‑exempel laddar vi en lokal kvittobild.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Observera hur vi skyddar mot en saknad fil. I verkliga appar skulle du troligen visa ett vänligt UI‑meddelande istället för att bara avsluta.

## Steg 4: Utför OCR‑igenkänning

Den faktiska textutvinningen sker med ett enda metodanrop. Motorn returnerar ett `OcrResult`‑objekt som innehåller den råa strängen, förtroendescore och layoutinformation.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Varför vi kontrollerar `ocrResult.Text`: ibland ger en lågkvalitativ PNG en tom sträng, och det är bättre att informera användaren än att tyst skriva ut ingenting.

## Steg 5: Skriv ut den igenkända texten

Till sist, skriv den extraherade strängen till konsolen. Du kan också skriva den till en fil, en databas eller skicka den till en annan tjänst.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

När du kör programmet (`dotnet run`) bör du se något liknande:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Detta är den **kompletta lösningen för att extrahera text från PNG**‑filer med Aspose OCR, och du har just lärt dig hur du **läser text från bild**‑filer som ser ut som kvitton.

## Valfritt: Fin‑justera OCR‑motorn (Avancerat)

Om du behöver högre precision för specifika typsnitt eller brusiga bakgrunder, överväg att justera dessa inställningar:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Dessa justeringar är särskilt användbara när du **processar kvitto‑OCR** i batchjobb där vissa skanningar är mindre än perfekta.

## Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| **GPU‑drivrutin saknas** | Motorn försöker ladda CUDA men hittar inte DLL‑filen. | Installera den senaste NVIDIA‑drivrutinen eller byt till CPU‑läge genom att ta bort raden `EngineMode.Gpu`. |
| **Felaktig bildsökväg** | `ImageStream.FromFile` kastar ett undantag om filen inte finns. | Validera alltid sökvägen (se Steg 3) eller använd `Path.Combine` för plattformsoberoende säkerhet. |
| **Låg förtroende på suddiga kvitton** | OCR‑motorn kan inte särskilja tecken. | Aktivera `EnableImagePreprocessing` och öka eventuellt bildens DPI innan du matar in den i motorn. |
| **Minnesläckage i långvariga tjänster** | Varje `OcrEngine` håller på ohanterade resurser. | Disposa motorn efter användning: `using var ocrEngine = new OcrEngine();` |

## Fullt fungerande exempel (Kopiera‑klistra)

Nedan är **hela programmet** som du kan klistra in i `Program.cs`. Det innehåller alla valfria justeringar kommenterade för enkel aktivering.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Spara, kör `dotnet run`, och du kommer att se kvittots innehåll skrivet i konsolen.

![extrahera text från png‑exempel](receipt.png "extrahera text från png‑exempel")

*Bilden ovan visar ett exempel‑kvitto i PNG‑format som koden kan bearbeta.*

## Sammanfattning

Vi har gått igenom hur du **extraherar text från PNG**‑filer med Aspose OCR, demonstrerat hur du **läser text från bild**‑filer, och gått igenom en komplett **processa kvitto‑OCR**‑pipeline som inkluderar valfri GPU‑acceleration. Genom att **skapa en OCR‑motor** själv får du full kontroll över konfiguration, prestanda och felhantering.

## Vad kan du utforska härnäst?

- **Batch‑behandling**: Loopa igenom en katalog med PNG‑kvitton och skriv varje resultat till en CSV‑fil.  
- **Integration med Azure Functions**: Gör om denna konsolapp till en serverlös endpoint som tar emot bilduppladdningar.  
- **Flerspråkigt stöd**: Byt `Language.English` mot `Language.Spanish` eller lägg till egna ordböcker.  
- **Efterbehandling**: Använd reguljära uttryck för att extrahera fält som totalbelopp, datum eller organisationsnummer från den råa OCR‑strängen.

Känn dig fri att experimentera—OCR är ett förvånansvärt flexibelt verktyg när du vet vilka reglage du ska vrida. Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose OCR API‑referensen för djupare insikter.

Lycka till med kodandet, och njut av att förvandla envisa PNG‑kvitton till sökbar text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}