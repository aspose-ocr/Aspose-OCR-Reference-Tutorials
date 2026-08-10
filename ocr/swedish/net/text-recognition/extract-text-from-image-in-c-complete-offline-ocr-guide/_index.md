---
category: general
date: 2026-03-18
description: Extrahera text från bild med Aspose OCR i C#. Lär dig hur du extraherar
  text, kör OCR-igenkänning och känner igen kyrillisk text utan internet.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: sv
og_description: Extrahera text från bild med Aspose OCR. Steg‑för‑steg‑guide för att
  köra OCR‑igenkänning, hur du extraherar text och känner igen kyrillisk text offline.
og_title: Extrahera text från en bild i C# – Offline OCR-handledning
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahera text från bild i C# – Komplett offline OCR-guide
url: /sv/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild – Komplett offline OCR‑guide

Har du någonsin behövt **extrahera text från bild** men oroat dig för nätverkslatens eller licensrestriktioner? Du är inte ensam. Många utvecklare stöter på problem när deras app måste fungera i en sandlådemiljö, men ändå kräver pålitlig OCR. De goda nyheterna? Med Aspose OCR kan du köra hela pipeline lokalt, **extrahera text från bild** utan att någonsin ansluta till internet.

I den här handledningen går vi igenom ett praktiskt exempel som visar **hur man extraherar text**, sätter upp en offline‑motor, **kör OCR‑igenkänning**, och till och med **igenkänner kyrillisk text**. I slutet har du en färdig‑att‑köra C#‑konsolapp som skriver ut den upptäckta strängen direkt till konsolen.

## Vad du behöver

- .NET 6.0 SDK (eller någon nyare .NET‑version)  
- Visual Studio 2022 eller VS Code – vad du föredrar  
- Aspose.OCR för .NET NuGet‑paket  
- En mapp som innehåller Aspose OCR‑modellfilerna (ladda ner en gång från Aspose‑portalen)  
- En bildfil som innehåller engelska och kyrilliska tecken (t.ex. `cyrillic_doc.jpg`)

Inga externa tjänster, inga dolda nedladdningar vid körning – allt finns på din disk.

## Steg 1: Installera Aspose.OCR och förbered resurser

Först, lägg till Aspose.OCR NuGet‑paketet i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

Skapa sedan en mapp med namnet `AsposeOCRResources` någonstans på din maskin och kopiera modellfilerna du laddade ner från Aspose till den. OCR‑motorn kommer att leta efter språkpaket i den här katalogen, så se till att sökvägen är korrekt.

> **Proffstips:** Håll resursmappen bredvid din `.csproj`‑fil; det förenklar hantering av sökvägar under utveckling.

## Steg 2: Bygg den offline OCR‑motorn

Nu kommer vi att instansiera motorn och peka den mot resursmappen. Detta är det avgörande steget som låter oss **köra OCR‑igenkänning** helt offline.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

Varför ladda språk explicit? Eftersom vi instruerade motorn att hålla sig offline; den kommer inte att kontakta Aspose‑servrar för att hämta saknade paket. Om du glömmer att ladda ett språk kommer alla tecken från det skriptet att ignoreras.

## Steg 3: Mata bilden till motorn

Med motorn klar, förser vi nu den med bilden vi vill bearbeta. Hjälpfunktionen `ImageStream.FromFile` läser filen till ett format som OCR‑motorn förstår.

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

Om din bild är stor, överväg att ändra storlek på den i förväg för att förbättra hastighet och noggrannhet. OCR‑motorn fungerar bäst med en DPI på omkring 300.

## Steg 4: Utför igenkänningsprocessen

Att anropa `Recognize` utför det tunga arbetet. Metoden returnerar ett `OcrResult`‑objekt som innehåller den extraherade strängen, förtroendescore och mer.

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Bakom kulisserna parsar Aspose bitmapen, kör språk‑specifika neurala nätverk och sätter ihop tecknen. Eftersom vi laddade både engelska och kyrilliska, hanteras blandade skript‑dokument sömlöst.

## Steg 5: Visa den extraherade texten

Till sist skriver vi ut resultatet. I en riktig app kan du lagra det i en databas eller skicka det till en annan tjänst, men för den här demonstrationen skriver vi bara ut det.

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Att köra programmet bör ge dig något i stil med:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

Om du ser förvrängda tecken, dubbelkolla att det kyrilliska språkpaketet är korrekt placerat i resursmappen och att bilden inte är för suddig.

![exempel på att extrahera text från bild](extract_text_image.png "extrahera text från bild")

*Bildtext: extrahera text från bild – OCR‑resultat som visar engelska och kyrilliska rader.*

## Hantera vanliga fallgropar

### Saknade språkpaket

Om du får ett undantag som säger “Language data not found,” kunde motorn inte hitta modellfilerna. Verifiera `ResourcesPath` och se till att mappen innehåller `english.dat` och `cyrillic.dat` (eller liknande namngivna filer).

### Låga förtroendescore

Ibland kommer OCR‑motorn att returnera låg förtroende för vissa tecken, särskilt om bilden har brus. Du kan förbättra noggrannheten genom att:

- Konvertera bilden till gråskala innan du matar den till motorn  
- Applicera ett medianfilter för att minska prickar  
- Säkerställa att texten är horisontellt inriktad (rotera om nödvändigt)

### Stora bilder

Att bearbeta ett 10 MP‑foto kan vara långsamt. Skala ner till en maximal bredd på 2000 px samtidigt som bildförhållandet bevaras; motorn kommer fortfarande att fånga de flesta tecken korrekt.

## Utöka exemplet

- **Batch‑behandling:** Packa in igenkänningslogiken i en loop som itererar över alla filer i en katalog.  
- **Utdataformat:** `OcrResult` erbjuder också en `TextLines`‑samling som innehåller avgränsningsrutor – användbart för att markera text i UI‑applikationer.  
- **Ytterligare språk:** Anropa helt enkelt `LoadLanguage` med något annat stödd enum‑värde (t.ex. `Language.French`).  

Alla dessa utökningar följer fortfarande principen **hur man extraherar text** – ladda bara de lämpliga språkpaketen och låt motorn göra resten.

## Fullständig källkodssammanfattning

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen på din maskin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spara detta som `Program.cs`, kör `dotnet run`, och se konsolen skriva ut texten som motorn hämtade från din bild. Så är det – du har framgångsrikt **extraherat text från bild** offline.

## Slutsats

Vi har gått igenom allt du behöver för att **extrahera text från bild** med Aspose OCR i ett helt offline‑scenario. Guiden visade **hur man extraherar text**, demonstrerade **kör OCR‑igenkänning**, och bevisade att du kan **igenkänna kyrillisk text** tillsammans med engelska utan några nätverksanrop.  

Från att sätta upp NuGet‑paketet till att hantera kantfall som saknade språkpaket, har du nu en solid grund för att bygga OCR‑drivna funktioner i vilken .NET‑applikation som helst.  

Vad blir nästa steg? Prova att mata in PDF‑filer, skanna flera sidor, eller integrera resultatet med ett sökindex. Himlen är gränsen när du behärskar offline OCR.

Lycka till med kodningen, och må dina bilder alltid vara kristallklara!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}