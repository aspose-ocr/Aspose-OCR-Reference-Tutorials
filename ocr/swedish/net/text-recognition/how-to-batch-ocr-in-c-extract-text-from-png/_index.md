---
category: general
date: 2026-03-26
description: Hur man batch‑OCR:ar i C# gör det enkelt att extrahera text från PNG‑filer.
  Följ den här steg‑för‑steg C# OCR‑handledningen för batchtextutvinning med Aspose
  OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: sv
og_description: Hur du batch‑OCR:ar i C# låter dig snabbt extrahera text från PNG‑filer.
  Denna guide går dig igenom en komplett C# OCR‑handledning med batchtextutdragning.
og_title: Hur man batchar OCR i C# – Extrahera text från PNG
tags:
- OCR
- C#
- Aspose
title: Hur man batch‑OCR i C# – Extrahera text från PNG
url: /sv/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch‑OCR:ar i C# – Extrahera text från PNG

Har du någonsin funderat **hur man batch‑OCR:ar** en hög med skärmdumpar utan att skriva ett separat program för varje fil? Du är inte ensam. I många projekt hamnar vi med dussintals PNG‑filer som behöver deras text extraheras, och att göra det en‑och‑en är jobbigt.  

Den goda nyheten? Med Aspose OCR kan du skapa ett litet C#‑konsolprogram som bearbetar alla dessa bilder parallellt, vilket ger dig snabb **batch‑textextraktion** och ett rent resultatset. I den här guiden går vi igenom ett komplett **c# ocr tutorial**, förklarar varför varje del är viktig och visar exakt hur utdata ser ut.

När du är klar med den här artikeln kommer du att kunna:

* Ladda en lista med PNG‑filer (eller någon annan stödd bild) på en gång.  
* Konfigurera en delad `OcrEngine` så att inställningarna förblir konsekventa genom hela batchen.  
* Köra igenkänningskön med upp till fyra parallella arbetare.  
* Hämta den igenkända texten för varje sida och skriva ut den i konsolen.

Ingen magi, bara solid kod som du kan släppa in i din lösning idag.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* .NET 6 SDK (eller någon nyare .NET‑version).  
* En giltig Aspose OCR‑licens eller en tillfällig evalueringsnyckel.  
* En mapp som innehåller de PNG‑filer du vill bearbeta.  
* Visual Studio 2022 eller din favoritredigerare.

Det är allt—inga extra NuGet‑paket utöver `Aspose.OCR` och standard‑`System.Collections.Generic`.

## Så här batch‑OCR:ar du – Ställ in projektet

Först och främst, skapa ett nytt konsolprojekt och hämta Aspose OCR‑biblioteket.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

När återställningen är klar, öppna **Program.cs** (eller skapa en ny fil) och lägg till de vanliga `using`‑direktiven:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Den enkla strukturen ger oss åtkomst till `OcrEngine`, `RecognitionQueue` och hjälparklasserna vi kommer att behöva senare.

## Extrahera text från PNG – Förbered bildlistan

Nu måste vi berätta för programmet **vilka PNG‑filer** som ska köras genom OCR. Det enklaste sättet är att bygga en `List<string>` som innehåller absoluta eller relativa sökvägar.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Byt ut `YOUR_DIRECTORY` mot den faktiska mappens sökväg. Om du har en dynamisk uppsättning kan du också använda `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` och mata in resultatet i listan. Huvudpoängen är att **extrahera text från PNG** bara handlar om att leverera rätt filnamn till kön.

![Hur man batch‑OCR:ar arbetsflöde](https://example.com/placeholder.png "Diagram som illustrerar hur man batch‑OCR:ar en samling PNG‑filer")

*Bildtext: diagram som visar hur man batch‑OCR:ar en samling PNG‑filer*

## C# OCR‑tutorial – Konfigurera igenkänningskön

Kärnan i batch‑operationen är `RecognitionQueue`. Tänk på den som ett löpband som överlämnar varje bild till en delad `OcrEngine`. Genom att dela motorn håller vi minnesanvändningen låg och garanterar identiska inställningar för varje sida.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Varför sätta `MaxDegreeOfParallelism` till 4? På en vanlig quad‑core‑laptop ger det bästa genomflödet utan att svälta operativsystemet. Om du kör på en server med fler kärnor, öka siffran därefter.

### Pro‑tips

Om du behöver anpassade språkpaket, DPI‑inställningar eller beskärning av intresseområde, gör det **en gång** på den delade `Engine` innan du köar in några bilder. Till exempel:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Alla efterföljande igenkänningar ärver automatiskt dessa alternativ—detta är kärnan i **hur man skapar OCR**‑pipelines som förblir konsekventa.

## Batch‑textextraktion – Köa bilder och kör kön

När kön är klar är nästa steg att lägga varje bild i den. Metoden `Enqueue` accepterar en `OcrImage`‑instans, som vi skapar från en filsökväg.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

När alla filer är köade, startar vi bearbetningen:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blockerar tills varje bild är klar, och returnerar sedan en lista där varje element motsvarar indataordningen. Detta garanterar att sid 1:s resultat finns på index 0, sid 2 på index 1, osv.—praktiskt när du behöver mappa resultat tillbaka till källfilerna.

## Hur man skapar OCR – Visa resultaten

Till sist, låt oss skriva ut den igenkända texten i konsolen. Här ser du verkligen **batch‑textextraktion** i aktion.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

När du kör programmet (`dotnet run`) bör du se något i stil med:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Om någon bild misslyckas (t.ex. korrupt fil) får motsvarande `OcrResult` en tom `Text`‑egenskap och du kan inspektera `ocrResults[i].Exception` för diagnostik.

## Hur man skapar OCR – Tips, kantfall och bästa praxis

### Hantera stora batcher

Att bearbeta hundratals PNG‑filer kan fortfarande äta minne om du behåller alla `OcrResult`‑objekt levande. I sådana fall, strömma utdata till en fil eller databas så snart varje resultat anländer:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Hantera icke‑PNG‑format

Aspose OCR stödjer även JPEG, BMP och TIFF direkt ur lådan. Byt bara filändelsen i din lista eller använd en jokerteckensökning. Samma **c# ocr tutorial**‑steg gäller—ingen kodändring behövs.

### Hoppa över tomma sidor

Om du har skannade PDF‑filer som ibland innehåller tomma sidor kan du filtrera resultaten:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Licensöverväganden

Utvärderingsversionen märker varje sida med ett vattenstämpel. För produktionsbruk, se till att du bäddar in din licensfil i början av `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Justering av parallellism

`MaxDegreeOfParallelism` har standardvärdet `Environment.ProcessorCount`. Om du märker hög CPU‑användning eller minnespress, sänk värdet. Omvänt, på en moln‑VM med många kärnor, höj det för att utnyttja hårdvaran fullt ut.

## Sammanfattning

Du har nu en komplett **hur man batch‑OCR:ar**‑lösning i C# som kan **extrahera text från PNG**‑filer, köra dem parallellt och ge dig rena, ordnade resultat. Genom att dela en enda `OcrEngine` har du lärt dig **hur man skapar OCR**‑pipelines som både är minnes‑effektiva och enkla att underhålla. Detta **c# ocr tutorial** visar också hur du skalar upp till **batch‑textextraktion** för hundratals bilder med bara några extra rader kod.

---

### Vad blir nästa steg?

* Prova att lägga till språkdetection (`Engine.Language = Language.AutoDetect`).  
* Experimentera med utdataformat—skriv resultat till JSON eller CSV för vidare analys.  
* Kombinera detta batch‑OCR med ett PDF‑till‑bild‑konverteringssteg för att bearbeta hela skannade dokument.

Känn dig fri att justera parallellismen, byta ut dina egna bildkällor eller plugga in resultaten i ett sökindex. Himlen är gränsen när du behärskar **hur man batch‑OCR:ar** i C#.

Lycka till med kodandet, och må dina OCR‑körningar vara snabba och felfria!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}