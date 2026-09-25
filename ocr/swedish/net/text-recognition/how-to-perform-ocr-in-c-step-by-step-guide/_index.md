---
category: general
date: 2026-02-14
description: Hur man utför OCR i C# med Aspose.OCR – lär dig att extrahera text från
  en bild, ladda bild från fil och köra OCR på bilden snabbt.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: sv
og_description: Hur man utför OCR i C# med Aspose.OCR. Denna guide visar hur du extraherar
  text från en bild, laddar bild från fil och kör OCR på bilden effektivt.
og_title: Hur man utför OCR i C# – Komplett programmeringshandledning
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hur man utför OCR i C# – Steg‑för‑steg‑guide
url: /sv/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR i C# – Komplett programmeringshandledning

Har du någonsin undrat **hur man utför OCR** på en bild du just tagit med din telefon? Kanske behöver du hämta texten från ett gatunskylt i en JPEG för en navigationsapp, eller så har du en mängd skannade kontrakt och vill göra dem sökbara. Kort sagt vill du *extrahera text från bild* utan att skicka något till molnet.

Den goda nyheten är att du kan göra allt detta lokalt med Aspose.OCR för .NET. I den här handledningen går vi igenom hur man laddar en bild från fil, känner igen text från en JPG och slutligen **kör OCR på bild**-filer helt offline. I slutet har du ett färdigt kodexempel som skriver ut den igenkända arabiska texten till konsolen.

> **Vad du får:** ett självständigt, körbart C#‑program, förklaringar till varför varje rad är viktig, samt tips för att hantera vanliga kantfall som saknade resurser eller språk som inte stöds.

## Förutsättningar

Innan vi dyker ner, se till att du har:

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.OCR riktar sig mot .NET Standard 2.0, så alla moderna runtime‑miljöer fungerar. |
| Visual Studio 2022 (or VS Code with C# extension) | En IDE gör det enkelt att hantera NuGet‑paket och köra konsol‑appen. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Detta är biblioteket som faktiskt utför OCR‑arbetet. |
| A folder containing the offline OCR resources (download from Aspose) | Offline‑resurser undviker alla HTTP‑anrop under igenkänning. |
| An image file (e.g., `arabic_sign.jpg`) | Vi kommer att använda en JPEG som innehåller arabisk text, men alla språk fungerar. |

Om du saknar någon av dessa, skaffa dem nu—det är ingen idé att börja en handledning bara för att stöta på en saknad beroende halvvägs igen.

## Steg 1: Installera Aspose.OCR och förbered resurser

Först, lägg till Aspose.OCR‑paketet i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

När paketet är installerat, ladda ner **offline‑OCR‑resurspaketet** från Aspose‑webbplatsen. Extrahera det till en mapp på din dator, till exempel:

```
C:\OCRResources\
```

> **Varför detta är viktigt:** Att ladda resurserna en gång vid start eliminerar nätverkslatens och gör din lösning GDPR‑vänlig eftersom inget lämnar maskinen.

## Steg 2: Skapa OCR‑motorn och peka den på resursmappen

Nu kommer vi att instansiera klassen `Engine` och berätta var resurserna finns. Detta är kärnan i **hur man utför OCR** lokalt.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Proffstips:** Omge anropet `LoadResources` med ett try‑catch‑block om du förväntar dig att sökvägen kan vara fel. Undantaget kommer att berätta exakt vilken fil som saknas.

## Steg 3: Ladda bilden från fil

Nästa steg är att **ladda bild från fil** så att motorn kan analysera den. Aspose.OCR arbetar med sin egen `ImageStream`‑wrapper.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Om din bild finns någon annanstans, ändra bara sökvägen. Klassen `ImageStream` abstraherar bort den underliggande bitmap‑hanteringen, så du behöver inte oroa dig för GDI+‑kompatibilitet.

## Steg 4: Känn igen text från JPG med språkinställningar

Nu kommer kärnan i **hur man utför OCR**—att faktiskt känna igen tecknen. Vi kommer att begära arabisk igenkänning, men du kan byta `Language.Arabic` mot något annat stödjande språk.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Varför ange ett språk?** OCR‑motorn använder språk‑specifika ordböcker och teckenmodeller. Att ange rätt språk förbättrar noggrannheten avsevärt, särskilt för skript med komplexa former som arabiska.

## Steg 5: Visa den extraherade texten

Till sist, låt oss **extrahera text från bild** och skriva ut den. Detta är det enklaste sättet att verifiera att OCR lyckades.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

När du kör programmet bör du se den arabiska frasen som fanns på skylten skriven i konsolen. Om utskriften ser förvrängd ut, dubbelkolla att rätt språk valdes och att resursmappen innehåller de arabiska datafilerna.

## Fullt fungerande exempel

Nedan är det kompletta, färdiga att kompilera programmet som binder ihop alla steg. Kopiera‑klistra in det i ett nytt konsolprojekt (`dotnet new console`) och tryck **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Förväntad utskrift (exempel):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Om du ersätter bilden med ett engelskt skylt och sätter `Language.English`, kommer samma kod att skriva ut den engelska texten. Det visar hur flexibel **kör OCR på bild** kan vara.

## Extrahera text från bild – Hantera vanliga scenarier

### 1. Flera sidor eller flermålsbilder

Vissa bildformat (som TIFF) kan innehålla flera sidor. För att **extrahera text från bild** i sådana fall, loopa över varje ram:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. LågdPI‑bilder

OCR‑noggrannheten sjunker dramatiskt under 70 dpi. Om du får suddiga resultat, överväg att först skala upp bilden.

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Saknat språkpaket

Om du får ett undantag som *“Language data not found”*, dubbelkolla att motsvarande `.dat`‑filer finns i din `ResourceFolder`. Aspose levererar en separat zip för varje språk.

## Kör OCR på bild – Prestandatips

- **Cachea motorn:** Att skapa en ny `Engine` för varje bild ger extra overhead. Behåll en enda instans vid liv för batch‑bearbetning.
- **Parallellisera säkert:** `Engine` är trådsäker för skriv‑skyddade operationer efter `LoadResources`. Du kan starta flera uppgifter som var och en anropar `Recognize` på olika bilder.
- **Dispose när klar:** Även om `Engine` implementerar `IDisposable` kommer .NET GC att rensa upp så småningom. Att explicit anropa `ocrEngine.Dispose()` i ett `using`‑block är en bra vana.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Känn igen text från JPG – Edge‑cases att hålla utkik efter

| Situation | What to Check | Fix |
|-----------|---------------|-----|
| **Corrupted JPEG** | `ImageStream.FromFile` throws `FileNotFoundException` or `ArgumentException`. | Verify file integrity, maybe re‑save the image with a graphics editor. |
| **Unsupported language** | `Language` enum doesn’t contain your target language. | Update Aspose.OCR to the latest version; new languages are added regularly. |
| **Mixed‑script images** (e.g., English + Arabic) | Single language option may miss the secondary script. | Run OCR twice with different language options and concatenate results. |

## Sammanfattning – Du vet nu hur man utför OCR i C#

I den här guiden gick vi igenom **hur man utför OCR** med Aspose.OCR, från installation av NuGet‑paketet till att skriva ut den igenkända texten. Du lärde dig att **ladda bild från fil**, **extrahera text från bild**, **känna igen text från jpg**, och säkert **köra OCR på bild** på ett produktionsklart sätt.

### Vad blir nästa?

- **Experimentera med andra filformat** som PNG eller BMP—byt bara filändelsen.
- **Integrera med en databas** för att lagra OCR‑resultat för sökbara arkiv.
- **Kombinera med datorseende** (t.ex. upptäck textregioner innan OCR) för hastighetsvinster.

Känn dig fri att justera språkinställningarna, batch‑processa mappar eller koppla utskriften till ett web‑API. OCR är en byggsten; den verkliga kraften kommer när du väver in den i större arbetsflöden.

Lycka till med kodandet, och må dina bilder alltid vara kristallklara!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}