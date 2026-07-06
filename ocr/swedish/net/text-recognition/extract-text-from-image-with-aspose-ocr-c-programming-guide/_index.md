---
category: general
date: 2026-03-13
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du laddar en
  bild för OCR, kör OCR på bilden och extraherar kyrillisk text med tydlig steg‑för‑steg‑kod.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: sv
og_description: Extrahera text från bild i C# med Aspose OCR. Den här handledningen
  visar hur du laddar en bild för OCR, kör OCR på bilden och extraherar kyrillisk
  text effektivt.
og_title: Extrahera text från bild med Aspose OCR – C#‑guide
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrahera text från bild med Aspose OCR – C#‑programmeringsguide
url: /sv/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild med Aspose OCR – C# programmeringsguide

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket bibliotek som klarar kyrilliska tecken utan problem? Du är inte ensam. I många projekt—fakturaskanning, passverifiering eller snabb anteckningstagning—är det avgörande att få pålitlig text ur en bild.  

I den här guiden går vi igenom de exakta stegen för att **ladda bild för OCR**, konfigurera Aspose OCR, **kör OCR på bild**, och slutligen **extrahera kyrillisk text** med bara några rader C#. I slutet har du ett färdigt kodexempel som skriver ut den igenkända texten till konsolen.

## Vad du kommer att lära dig

- Hur du installerar och refererar Aspose OCR NuGet-paketet.  
- Det korrekta sättet att peka mot språkpaketresurserna.  
- Varför valet av `Language.Cyrillic` är viktigt för icke‑latinska skript.  
- Vanliga fallgropar (saknade resurser, bildformat som inte stöds) och hur du undviker dem.  
- Ett komplett, körbart exempel som du kan lägga in i vilket .NET‑projekt som helst.

Ingen tidigare OCR‑erfarenhet krävs, men en grundläggande förtrogenhet med C# och Visual Studio gör resan smidigare.

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **.NET 6.0** eller senare installerat (koden fungerar på .NET Core och .NET Framework).  
2. **Visual Studio 2022** (eller någon editor som stödjer C#).  
3. Aspose.OCR NuGet‑paketet. Installera det via Package Manager Console:  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. En mapp som innehåller OCR‑språkpaketen (nedladdningsbara från Asposes webbplats).  
5. En bildfil (`cyrillic.png` i exemplet) som innehåller kyrillisk text du vill läsa.

> **Proffstips:** Håll språkpaketsmappen bredvid ditt projekts `bin`‑katalog; det förenklar hanteringen av sökvägen.

## Steg 1 – Ladda bild för OCR

Det första du måste göra är att ge motorn en bitmap att arbeta med. Aspose OCR accepterar ett `ImageStream`, som kan skapas direkt från en filsökväg.

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*Varför detta är viktigt:* Att ladda bilden tidigt låter dig verifiera att filen finns och är i ett stödformat (PNG, JPEG, BMP, osv.). Om filen saknas kommer `FromFile`‑anropet att kasta ett tydligt undantag, vilket sparar dig från oklara OCR‑fel senare.

## Steg 2 – Ställ in OCR‑motor och resurser

Nästa steg är att skapa en instans av OCR‑motorn och peka den mot mappen som innehåller språkpaketen. Utan rätt resurser kommer motorn inte att kunna tolka kyrilliska tecken.

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*Varför detta är viktigt:* Metoden `SetResourcesPath` är bron mellan din kod och datafilerna som innehåller teckengestalt för varje stödjande språk. Att glömma detta steg resulterar vanligtvis i förvrängd output eller ett `ResourceNotFoundException`.

## Steg 3 – Välj språk och **kör OCR på bild**

Nu väljer vi det språk vi förväntar oss. Eftersom exemplet handlar om kyrilliska, sätter vi `Language.Cyrillic`. Om du behöver hantera flera skript kan du kombinera dem med en bitvis OR (`|`)‑operator.

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*Varför detta är viktigt:* Att specificera språket begränsar sökområdet för OCR‑algoritmen, vilket dramatiskt förbättrar både hastighet och noggrannhet. När du **kör OCR på bild** med rätt språkflagga får du betydligt färre felaktiga igenkänningar.

## Steg 4 – Hämta och använd den extraherade kyrilliska texten

När igenkänningen är klar lagrar motorn resultatet i egenskapen `Text`. Du kan nu visa det, skriva det till en fil eller skicka det till ett annat system.

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

Typisk konsolutskrift ser ut så här:

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

Om utskriften innehåller oväntade symboler, dubbelkolla att språkpaketen matchar versionen av Aspose OCR du har installerat.

## Fullt fungerande exempel – Alla steg kombinerade

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt. Ersätt `YOUR_DIRECTORY` med de faktiska sökvägarna på din maskin.

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### Förväntat resultat

När programmet körs bör det skriva ut exakt den text som visas i `cyrillic.png`. Om bilden innehåller frasen “Привет, мир!” kommer du att se den raden i konsolen utan extra symboler.

## Särskilda fall & felsökning

| Situation | Vad att kontrollera | Föreslagen åtgärd |
|-----------|---------------------|-------------------|
| **Saknade språkpaket** | Pekar `resourcesPath` på en mapp som innehåller `.dat`‑filer? | Ladda ner paketen igen från Aspose och placera dem i den angivna mappen. |
| **Ej stödformat för bild** | Är filen en PNG, JPEG, BMP eller TIFF? | Konvertera bilden till ett av de stödformat som finns innan du anropar `FromFile`. |
| **Skräptecken i output** | Har du ställt in `ocrEngine.Language` korrekt? | Använd `Language.Cyrillic` (eller kombinera flaggor för flera språk). |
| **Prestandafördröjning på stora bilder** | Bildens upplösning > 3000 px? | Skala ner bilden till en rimlig storlek (t.ex. 1024 px bredd) innan OCR. |

## Relaterade ämnen du kanske vill utforska härnäst

- **Extrahera text från bild** i PDF:er med Aspose PDF + OCR.  
- **Ladda bild för OCR** från en `Stream` (användbart när bilder kommer från ett web‑API).  
- Använda **kör OCR på bild** parallellt för att snabba upp batch‑behandling.  
- **Extrahera kyrillisk text** från handskrivna anteckningar med Aspose OCR:s handskriftsläge.  
- Integrera resultatet med **igenkänna kyrillisk text** i en databas för sökindexering.

## Slutsats

Vi har precis visat hur man **extraherar text från bild** med Aspose OCR, och täckt allt från att ladda bilden till att skriva ut de igenkända kyrilliska tecknen. Det korta, fristående programmet demonstrerar den minsta kod du behöver, medan felsökningstabellen sparar dig från de vanligaste problemen.  

Prova det på dina egna skärmbilder, byt ut språkpaketet mot arabiska eller kinesiska, och se hur samma mönster fungerar över hela världen. Lycka till med kodandet, och må dina OCR‑resultat alltid vara kristallklara! 

![Exempel på extrahering av text från bild](extract-text-from-image.png "Exempel på extrahering av text från bild")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}