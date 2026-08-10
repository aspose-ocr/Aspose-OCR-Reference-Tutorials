---
category: general
date: 2026-04-08
description: Lär dig hur du utför OCR på en bild och skriver en JSON‑fil i C# med
  Aspose OCR. Denna Aspose OCR C#‑handledning visar OCR‑bild‑till‑JSON‑konvertering
  med konfidensvärden.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: sv
og_description: Utför OCR på en bild och exportera resultaten till en JSON-fil i C#.
  Denna handledning täcker hela Aspose OCR C#‑arbetsflödet, inklusive konfidenspoäng.
og_title: Utför OCR på bild till JSON i C# – Aspose OCR‑guide
tags:
- Aspose
- OCR
- C#
- JSON
title: Utför OCR på bild till JSON i C# med Aspose
url: /sv/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild till JSON i C# med Aspose

Har du någonsin behövt **perform OCR on image** filer men var osäker på hur du får resultaten i ett strukturerat format? Du är inte ensam—utvecklare frågar ständigt, “Hur omvandlar jag en skannad bild till användbara data?” Den goda nyheten är att Aspose.OCR gör detta till en barnlek, och du kan till och med **write JSON file C#**‑stil med medföljande förtroendesiffror.

I den här guiden går vi igenom en komplett **aspose OCR C# tutorial** som täcker allt från att ladda en bild till att exportera den igenkända texten som JSON. När du är klar har du en körbar konsolapp som **perform OCR on image**, konverterar resultatet till JSON (inklusive förtroendevärden) och sparar det med en enda kodrad. Inga dolda steg, inga externa skript—bara ren C#.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar även med .NET Core och .NET Framework)
- Visual Studio 2022 (eller någon annan editor du föredrar)
- En giltig **Aspose.OCR for .NET**-licens eller en gratis tillfällig licens (gratisprovversionen fungerar för testning)
- En bildfil (`input.png`) som du vill bearbeta (valfritt vanligt format—PNG, JPG, BMP—fungerar)

Det är allt. Om du saknar någon av dessa, skaffa dem nu; resten av guiden förutsätter att de redan är på plats.

## Steg 1: Installera Aspose.OCR NuGet-paketet

Först och främst—lägg till biblioteket i ditt projekt. Öppna en terminal i projektmappen och kör:

```bash
dotnet add package Aspose.OCR
```

Detta hämtar den senaste versionen (från och med april 2026 är det 23.12) och lägger till de nödvändiga DLL-filerna i `bin`-mappen. Ingen extra konfiguration krävs.

## Steg 2: Initiera OCR-motorn (Perform OCR on Image)

Nu skapar vi en `OcrEngine`-instans och talar om vilken språk som ska användas. Engelska (`"en"`) är den vanligaste, men du kan byta till `"fr"`, `"de"` eller något annat stödjert språk.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Varför vi initierar här:** `OcrEngine` innehåller all konfiguration som behövs för igenkänningsprocessen. Att ställa in språket i förväg säkerställer att motorn använder rätt teckenuppsättning, vilket dramatiskt förbättrar noggrannheten.

## Steg 3: Känn igen bilden och fånga förtroende

När motorn är klar matar vi den med bildfilen. Metoden `RecognizeImage` returnerar ett `OcrResult`-objekt som innehåller både den extraherade texten och ett förtroendevärde för varje ord.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Vad händer under huven?** Aspose kör en neuronnätsbaserad igenkännare som analyserar varje pixelblock, matchar det mot sin språkmodell och bifogar ett förtroendevärde (0‑100) som visar hur säker den är på varje ord.

## Steg 4: Konvertera resultatet till JSON (OCR Image to JSON)

Aspose gör konverteringen enkel. Genom att skicka `includeConfidence: true` får vi en JSON-payload som ser ut så här:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Här är koden som producerar JSON-strängen:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Varför inkludera förtroende?** Om du planerar att mata data till efterföljande processer (t.ex. validering, UI-markering), så låter kunskapen om vilka ord som är osäkra dig avgöra om du ska be användaren om bekräftelse.

## Steg 5: Skriv JSON-filen i C#‑stil

Nu skriver vi faktiskt **write JSON file C#**. Metoden `File.WriteAllText` är atomisk och fungerar över plattformar, vilket gör den perfekt för konsolappar.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Det är hela arbetsflödet—fem koncisa steg som **perform OCR on image**, omvandlar resultatet till JSON och sparar det.

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i `Program.cs`. Se till att `input.png` finns i samma mapp som den kompilerade binären eller justera sökvägarna därefter.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Förväntad output

När du kör programmet (`dotnet run`) kommer du att se något liknande:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Och `output.json` kommer att innehålla den strukturerade JSON som visades tidigare, komplett med förtroendeprocent för varje ord.

## Proffstips & kantfall

- **Missing file handling:** Omslut anropet till `RecognizeImage` med en `try/catch` för `FileNotFoundException` om du förväntar dig dynamiska sökvägar.
- **Different languages:** Sätt `ocrEngine.Language = "fr"` för franska, eller ladda ett anpassat språkpaket via `ocrEngine.LoadLanguage("custom.lang")`.
- **Large documents:** För fler‑sidiga PDF‑filer, konvertera varje sida till en bild först (t.ex. med `Aspose.PDF`) och loopa igenom OCR‑stegen.
- **Performance tuning:** Om du bara behöver snabba resultat, byt till `RecognitionMode.Fast`—du förlorar lite noggrannhet men får hastighet.
- **JSON formatting:** Vill du ha vackert formaterad JSON? Använd `JsonConvert.SerializeObject` från Newtonsoft med `Formatting.Indented` efter att ha deserialiserat Aspose JSON‑strängen.

## Vanliga frågor

**Q: Fungerar detta med .NET Framework?**  
A: Absolut. Samma NuGet‑paket riktar sig mot .NET Standard 2.0, så du kan referera det från .NET Framework 4.6.1 och nyare.

**Q: Vad händer om jag behöver förtroendet för hela dokumentet, inte per ord?**  
A: `OcrResult` exponerar också `OverallConfidence`. Du kan lägga till det manuellt i JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Kan jag streama JSON direkt till ett web‑API?**  
A: Ja. Byt ut `File.WriteAllText` mot en `HttpClient` POST som skickar `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}