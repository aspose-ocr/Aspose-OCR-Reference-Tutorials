---
category: general
date: 2026-06-03
description: Aspose OCR C#-exempel som visar hur man ställer in GPU‑minnesgräns, laddar
  bild för OCR och känner igen text från TIF‑filer med fullständig kod och tips.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: sv
og_description: 'Lär dig ett komplett Aspose OCR C#-exempel: aktivera GPU, ange GPU‑minnesgräns,
  ladda en bild för OCR och känna igen text från TIF‑filer. Fullständig kod inkluderad.'
og_title: Aspose OCR C#-exempel – GPU-acceleration, minnesgräns och TIF-bearbetning
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Aspose OCR C#-exempel – Aktivera GPU, ange minnesgräns och bearbeta TIF‑bilder
url: /sv/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# Example – Aktivera GPU, Sätt Minnesgräns & Bearbeta TIF‑bilder

Har du någonsin funderat på hur du får ut maximal prestanda ur **Aspose OCR C# example**‑koden när du hanterar massiva TIFF‑skanningar? Du är inte ensam. I många verkliga projekt—tänk dig att digitalisera arkiv eller extrahera data från högupplösta kvitton—är flaskhalsen inte OCR‑algoritmen i sig, utan hårdvaruanvändningen.

Här är grejen: Aspose OCR stödjer GPU‑acceleration, men du måste berätta exakt hur mycket minne den får använda, ladda rätt bildtyp och slutligen hämta den igenkända texten från en .tif‑fil. Den här handledningen guidar dig genom varje steg, från installation av SDK till justering av GPU‑inställningarna, så att du kan köra OCR i blixtsnabb hastighet utan att tömma ditt GPU‑RAM.

Vi kommer också att ströa in några “vad händer om”‑scenarier—som att hantera flersidiga TIFF‑filer eller falla tillbaka till CPU när ingen GPU finns—så att du får en robust lösning, inte bara ett engångssnutt.

## Vad du behöver

Innan vi dyker ner, se till att du har följande på din maskin:

| Förutsättning | Varför det är viktigt |
|---------------|-----------------------|
| **.NET 6 SDK** (eller senare) | Aspose OCR riktar sig mot .NET Standard 2.0+, så vilken modern .NET‑version som helst fungerar. |
| **Aspose.OCR NuGet‑paket** (`Install-Package Aspose.OCR`) | Huvudbiblioteket som tillhandahåller `OcrEngine`, `GpuSettings` osv. |
| **CUDA 11+** (NVIDIA) **eller ROCm 5+** (AMD) | Krävs för GPU‑acceleration; SDK:n kontrollerar kompatibel drivrutin vid körning. |
| En **GPU med minst 2 GB VRAM** (vi sätter gränsen till 2048 MB) | Utan tillräckligt minne kan motorn tyst falla tillbaka till CPU. |
| En **högupplöst TIFF‑bild** du vill bearbeta | Aspose OCR kan läsa i princip alla rasterformat, men TIF är vanligt för skanningar. |
| Visual Studio 2022 (eller någon annan editor du föredrar) | För att bygga och debugga C#‑projektet. |

Om någon av dessa saknas kommer koden fortfarande att kompilera, men du får inte de prestandafördelar vi siktar på.

## Steg 1: Skapa Aspose OCR C# Example‑motorn

Det första i varje **Aspose OCR C# example** är att instansiera OCR‑motorn. Tänk på `OcrEngine` som filmregissören—den koordinerar allt från bildladdning till textutdragning.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Proffstips:** Om du planerar att bearbeta många bilder i rad, håll en enda `OcrEngine` levande. Att återskapa den per bild ger overhead som kan överskugga OCR‑tiden.

## Steg 2: Sätt GPU‑minnesgräns (och aktivera acceleration)

Nu kommer delen som ofta får folk att snubbla: **sätt GPU‑minnesgräns**. Som standard försöker Aspose OCR använda så mycket VRAM som möjligt, vilket på en delad arbetsstation kan svälta andra program. Objektet `GpuSettings` låter dig begränsa allokeringen.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Varför sätta en minnesgräns?

- **Stabilitet:** Förhindrar krascher på grund av minnesbrist när enorma bilder bearbetas.  
- **Samspelet:** Gör att andra GPU‑tunga appar (t.ex. TensorFlow‑modeller) kan köras samtidigt.  
- **Förutsägbarhet:** Gör prestandatester reproducerbara eftersom GPU:n inte börjar byta ut minne.

Om du utelämnar `MemoryLimitMb` allokerar Aspose vad den anser nödvändigt, vilket kan vara okej på en dedikerad inferensserver men riskabelt på en utvecklar‑laptop.

## Steg 3: Ladda bild för OCR

Att ladda rätt filformat är nästa kritiska steg. Metoden `OcrImage.FromFile` upptäcker automatiskt bildtypen, men du bör ändå verifiera att filen finns och att den är en stödjande TIFF‑variant (t.ex. LZW‑komprimerad eller CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Hantera flersidiga TIFF‑filer

Om din TIFF innehåller flera sidor läser Aspose OCR bara den första som standard. För att bearbeta alla sidor kan du loopa över `image.Pages` (tillgängligt i nyare SDK‑versioner) och skicka varje sida till motorn separat.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

Snutten ovan demonstrerar ett **load image for OCR**‑mönster som fungerar för både enkel‑ och flersidiga filer.

## Steg 4: Känn igen text från TIF (eller någon raster)

Nu när bilden lever i minnet ber vi Aspose utföra sin magi. Metoden `Recognize` returnerar ett `OcrResult` som innehåller ren text, förtroendescore och till och med bound‑box‑information om du behöver den.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Varför detta fungerar bra med TIF

- **Förlustfri kompression:** TIFF lagrar ofta råa pixeldata, vilket ger OCR‑motorn högsta möjliga detaljrikedom.  
- **Flera färgrymder:** Aspose kan hantera gråskala, RGB eller till och med CMYK‑TIFF utan extra konverteringskod.

Om du behöver justera språkpaket (t.ex. franska eller japanska), sätt `ocrEngine.Settings.Language = "fr"` innan du anropar `Recognize`.

## Steg 5: Visa den igenkända texten

Till sist skriver vi ut texten till konsolen. I en riktig applikation kanske du skriver till en databas, en JSON‑fil eller matar strängen in i en efterföljande NLP‑pipeline.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Förväntad utskrift

Att köra programmet på en klar, 300 dpi‑skanning av en tryckt sida ger vanligtvis något i stil med:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Om bilden är suddig eller GPU‑minnesgränsen är för låg kan du se förvrängda tecken eller ett avklippt resultat. Att sänka `MemoryLimitMb` under bildens fotavtryck (ofta ~1 GB för en 6000×8000 pixel‑TIFF) kan få motorn att automatiskt falla tillbaka till CPU.

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet. Kopiera‑klistra in det i ett nytt Console‑App‑projekt, ersätt `YOUR_DIRECTORY/large_photo.tif` med sökvägen till din egen TIFF och tryck **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Snabb checklista

- ✅ **Aspose OCR C# example** kompilerad utan fel.  
- ✅ **GPU aktiverad** (`Enable = true`).  
- ✅ **GPU‑minnesgräns** satt till 2048 MB.  
- ✅ **Bild laddad** från en TIF‑fil.  
- ✅ **Text igenkänd** och skriven ut.

## Vanliga fallgropar & hur du undviker dem

| Symtom | Trolig orsak | Åtgärd |
|--------|--------------|--------|
| `System.DllNotFoundException: cudart64_110.dll` | CUDA‑runtime saknas eller fel version. | Installera CUDA 11.x (eller 12.x) som matchar din drivrutin. |
| OCR returnerar tom sträng | Bilden är för mörk eller DPI < 150. | Förbehandla med `image.AdjustContrast()` eller resampla till 300 dpi. |
| Minneskrasch på GPU | `MemoryLimitMb` för låg för bilden. | Höj gränsen eller dela upp bilden i kakel via `image.Crop`. |
| `Unsupported image format`‑fel | TIFF använder en exotisk kompression (t.ex. JPEG‑2000). | Konvertera TIFF till ett stödjande format med ImageMagick innan OCR. |

## Utöka demonstrationen

Nu när du har ett stabilt **aspose ocr c# example**, kan du utforska:

- **Batch‑bearbetning:** Loopa över en mapp med TIF‑filer, skriv varje resultat till en `.txt`‑fil.  
- **Språkpaket:** `ocrEngine.Settings.Language = "es"` för spanska, eller ladda egna ordböcker.  
- **Bound‑boxes:** Använd `ocrResult.Regions` för att få koordinater för varje ord—praktiskt för redigeringsverktyg.  
- **CPU‑fallback:** Omge GPU‑blocket med try‑catch; vid fel, sätt `ocrEngine.Settings.Gpu.Enable = false` och försök igen.

Dessa tillägg behåller kärnmönstret samtidigt som de ger extra värde för specifika användningsfall.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementeringssätt i egna projekt.

- [Extrahera text från bild med Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Extrahera bildtext i C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}