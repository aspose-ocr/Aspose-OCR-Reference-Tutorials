---
category: general
date: 2026-03-21
description: 'c# ocr-handledning: Lär dig hur du extraherar urdustext från en PNG-bild
  med OCR i C#. Steg‑för‑steg‑kod, språkinställning och praktiska tips ingår.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: sv
og_description: 'c# OCR-handledning: Lär dig hur du extraherar urdustext från en PNG-bild
  med OCR i C#. Komplett guide med kod och tips.'
og_title: c# OCR-handledning – Extrahera urdetext från PNG-bilder
tags:
- OCR
- C#
- Urdu
- Image Processing
title: c# OCR-handledning – Extrahera urdutext från PNG-bilder
url: /sv/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extrahera urdutext från PNG‑bilder

Har du någonsin behövt ett **c# ocr tutorial** som faktiskt drar ut urdutext från en PNG‑fil? Du är inte ensam. I många projekt—fakturahantering, dokumentarkivering eller till och med ett snabbt översättningsverktyg—kommer du att stöta på punkten där du måste känna igen text i bilddata, och språket spelar roll.  

I den här guiden går vi igenom en komplett, färdig‑att‑köra‑lösning som extraherar urdutext från en PNG med en OCR‑motor. Du får se varför varje rad finns, hur du hanterar saknade språkpaket och vad du ska göra om bilden inte är perfekt. I slutet kommer du att vara säker nog att anpassa koden för andra språk eller filtyper.

## Vad du kommer att lära dig

- Hur du installerar ett C# OCR‑bibliotek (ingen dold magi)  
- De exakta stegen för att **extrahera urdutext** från en PNG‑fil  
- Varför det är viktigt att konfigurera språket till Urdu och hur motorn automatiskt laddar ner saknade data  
- Sätt att verifiera resultatet och felsöka vanliga fallgropar  

Inga externa dokumentationslänkar behövs—allt du behöver finns här.

## Förutsättningar (Vad du behöver innan du börjar)

| Krav | Varför det är viktigt |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | Moderna API:er och async‑stöd |
| Visual Studio 2022 (or VS Code with C# extension) | IDE med IntelliSense gör koden tydligare |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Tillhandahåller `Language.Urdu` och `Recognize`‑metoder |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | Källan för **recognize text image**‑operationen |

Om du ännu inte har ett OCR‑paket, kör den här enradaren i Package Manager Console:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

Det kommer att hämta `OcrEngine`‑klassen som vi kommer att använda senare.

> **Pro tip:** SDK:n hämtar automatiskt språkdata vid första användning, så du behöver inte manuellt ladda ner Urdu‑språkpaket.

## Steg 1: Installera och referera OCR‑biblioteket

Innan vi kan skapa en motor måste projektet referera OCR‑paketet. Lägg till följande `using`‑direktiv högst upp i din fil:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

Dessa namnrymder ger oss åtkomst till `OcrEngine`, `Language` och verktyg för bildladdning. Om du använder ett annat bibliotek, leta efter motsvarande namnrymder.

## Steg 2: Skapa en OCR‑motorinstans  

Nu startar vi faktiskt motorn. Tänk på motorn som hjärnan som tolkar pixelmönster som tecken.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Varför detta är viktigt:** `TryCreateFromLanguage` returnerar `null` om språkdata saknas, vilket ger oss möjlighet att misslyckas tidigt istället för att krascha senare.

## Steg 3: Ladda PNG‑bilden  

OCR‑motorn arbetar med `SoftwareBitmap`‑objekt, inte med råa filsökvägar. Följande hjälpfunktion laddar en PNG från disk och konverterar den till det format som krävs.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Edge case:** Om PNG‑filen är färgad kan konvertering till gråskala (`Gray8`) ofta förbättra igenkänning, särskilt för skript som Urdu som har känsliga diakritiska tecken.

## Steg 4: Känn igen text från bilden  

Här är kärnan i **c# ocr tutorial**—att be motorn läsa bilden.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

`OcrResult.Text`‑egenskapen innehåller den råa Unicode‑strängen. Eftersom vi tidigare satte språket till Urdu tillämpar motorn de korrekta skriptreglerna.

## Steg 5: Skriv ut och verifiera den extraherade texten  

Till sist skriver vi ut resultatet till konsolen. I en riktig app kan du lagra det i en databas eller skicka det till en översättningstjänst.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Vad du kan förvänta dig:** Om bilden är tydlig kommer du att se något liknande:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Om utskriften ser förvrängd ut, kontrollera bildkvaliteten (kontrast, brus) och överväg att förbehandla den (t.ex. binarisering).

## Så extraherar du urdutext från en PNG‑fil – Vanliga fallgropar  

1. **Låg kontrast** – OCR har svårt när förgrunds- och bakgrundsfärgerna är lika. Använd bildredigeringsverktyg för att öka kontrasten innan du kör koden.  
2. **Fel DPI** – Att skanna med 300 dpi eller högre ger motorn mer detaljer att arbeta med.  
3. **Saknat språkpaket** – Det första anropet till `TryCreateFromLanguage` kan utlösa en nedladdning; se till att din maskin har internetåtkomst.  

Att åtgärda dessa problem förbättrar **recognize text image**‑framgångsfrekvensen avsevärt.

## Recognize Text Image: Utöka till andra format  

Även om denna tutorial fokuserar på PNG fungerar samma arbetsflöde för JPEG, BMP eller TIFF—byt bara filändelsen och se till att avkodaren stöder den. Nyckelraden förblir `await ocrEngine.RecognizeAsync(bitmap);`.

## Tips för OCR från PNG‑fil – Prestanda och skalning  

- **Batch‑bearbetning:** Ladda flera bilder i en lista och kör `Task.WhenAll` för att parallellisera igenkänning.  
- **Cacha motorn:** Skapa en enda `OcrEngine`‑instans och återanvänd den över flera anrop; att konstruera den upprepade gånger ger extra overhead.  
- **Minneshantering:** Disposera `SoftwareBitmap`‑objekt efter användning (`bitmap.Dispose()`) för att hålla processen slank.

## Fullt fungerande exempel (Klar‑för‑kopiering)

Nedan är hela programmet som du kan kompilera och köra. Det inkluderar alla using‑satser, async‑hantering och felkontroller.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Förväntat resultat:** Konsolen skriver ut de exakta Urdu‑tecknen som finns i bilden, med bevarad höger‑till‑vänster‑ordning.

## Slutsats  

Du har just slutfört ett **c# ocr tutorial** som visar hur man **extraherar urdutext** från en PNG, konfigurerar språket och hanterar resultatet på ett säkert sätt. Stegen—installera biblioteket, skapa motorn, ladda bilden, känna igen text och skriva ut den—utgör ett återanvändbart mönster som du kan tillämpa på vilket skript eller filtyp som helst.  

Nästa steg kan vara att experimentera med **recognize text image** på flersidiga PDF‑filer (konvertera varje sida till PNG först) eller integrera ett översättnings‑API för att automatiskt översätta den extraherade Urdu‑texten till engelska. Himlen är gränsen när du har bemästrat detta grundläggande arbetsflöde.

Lycka till med kodandet, och må dina OCR‑resultat vara kristallklara!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}