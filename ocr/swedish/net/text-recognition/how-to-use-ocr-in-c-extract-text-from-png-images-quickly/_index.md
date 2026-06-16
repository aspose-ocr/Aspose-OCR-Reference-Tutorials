---
category: general
date: 2026-03-29
description: Hur man använder OCR med Aspose för att extrahera text från PNG‑filer
  och konvertera bilder till text. Lär dig steg‑för‑steg asynkron OCR i C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: sv
og_description: Hur man använder OCR med Aspose i C# för att extrahera text från PNG-filer.
  Denna guide går igenom asynkron OCR, kod och tips.
og_title: Hur man använder OCR i C# – Extrahera text från PNG‑bilder
tags:
- OCR
- C#
- Aspose
title: Hur man använder OCR i C# – Extrahera text från PNG‑bilder snabbt
url: /sv/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder OCR i C# – Extrahera text från PNG‑bilder snabbt

Har du någonsin undrat **hur man använder OCR** för att dra ut text från ett fåtal PNG‑skärmdumpar? Kanske har du skannade kvitton, fakturor eller UI‑mock‑ups och du behöver den texten i ett sökbart format. Den goda nyheten? Med Aspose.OCR kan du konvertera bilder till text med bara några rader asynkron C#‑kod.  

I den här handledningen visar vi exakt hur du extraherar text från PNG‑filer, förklarar varför varje steg är viktigt och ger dig ett färdigt program som skriver ut den igenkända texten för varje sida. I slutet kommer du att kunna **extrahera text från bilder** utan att gräva i dokumentationen.

## Vad du kommer att lära dig

- Installera och referera Aspose.OCR NuGet‑paketet.  
- Initiera OCR‑motorn och ange språket (engelska i detta exempel).  
- Mata in en array av PNG‑filer till `RecognizeImagesAsync` för snabb, icke‑blockerande bearbetning.  
- Loopa igenom `OcrResult`‑objekten och skriv ut de extraherade strängarna.  

Ingen extern tjänst, inga komplicerade callbacks—bara ren, async C# som fungerar på .NET 6+.

---

## Förutsättningar

| Requirement | Reason |
|-------------|--------|
| .NET 6 SDK (or later) | Moderna språkfunktioner som `async Main`. |
| Visual Studio 2022 or VS Code | IDE för att kompilera och köra koden. |
| Aspose.OCR NuGet‑paket (`Aspose.OCR`) | Tillhandahåller `OcrEngine`‑klassen som används i exemplet. |
| A few PNG images (`page1.png`, `page2.png`, …) | Inmatningsfiler för OCR‑processen. |

Om du redan har ett .NET‑projekt kör bara `dotnet add package Aspose.OCR`. Annars skapa en ny konsolapp med `dotnet new console -n OcrDemo`.

---

## Steg 1: Installera Aspose.OCR och konfigurera projektet

Först, lägg till OCR‑biblioteket i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

Varför detta är viktigt: Aspose.OCR paketet innehåller den inhemska OCR‑motorn, språkpaket och ett enkelt API. Genom att hämta det via NuGet säkerställer du versionskompatibilitet och automatiska uppdateringar.

---

## Steg 2: Initiera OCR‑motorn och välj ett språk

Motorn måste veta vilket språk den ska leta efter. Engelska är det vanligaste, men du kan byta till `Language.Spanish`, `Language.French`, osv.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Proffstips:** Ange alltid språket explicit; att låta det vara på standard kan försämra noggrannheten och öka bearbetningstiden.

---

## Steg 3: Förbered listan med PNG‑filer

Du kan mata in en enskild fil eller en array. Att leverera en array låter motorn batch‑processa dem asynkront, vilket är idealiskt för ett fåtal sidor.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Om dina bilder ligger i en undermapp, lägg bara till den relativa sökvägen (`"images/page1.png"`). Motorn kommer att kasta ett tydligt `FileNotFoundException` om en sökväg är fel—så dubbelkolla filnamnen.

---

## Steg 4: Kör asynkron OCR på alla bilder

`RecognizeImagesAsync`‑metoden returnerar en array av `OcrResult`. Eftersom den är async förblir ditt UI (eller konsol) responsivt medan OCR körs i bakgrunden.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Varför async?**  
Om du integrerar OCR i ett webb‑API eller en skrivbordsapp vill du inte att tråden ska blockeras medan motorn skannar varje pixel. `await` släpper tillbaka tråden till trådpoolen, vilket förbättrar skalbarheten.

---

## Steg 5: Visa den extraherade texten för varje sida

Nu när vi har resultaten, iterera igenom dem och skriv ut den igenkända texten. `Text`‑egenskapen innehåller ren‑text‑utdata, klar för vidare bearbetning (t.ex. sparande till en databas).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Förväntad utdata

Om vi antar att `page1.png` innehåller “Invoice #12345” och `page2.png` innehåller “Total: $89.99”, kommer du att se något liknande:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Om OCR misslyckas med att hitta någon text kommer `Text`‑egenskapen att vara en tom sträng—hantera detta i produktionskod genom att kontrollera `string.IsNullOrWhiteSpace`.

---

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i `Program.cs`. Det inkluderar alla using‑direktiv, async `Main`, och kommentarer som förklarar varje steg.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Spara filen, placera dina PNG‑filer bredvid den körbara filen (eller justera sökvägarna), och kör:

```bash
dotnet run
```

Du bör se den extraherade texten skriven till konsolen, vilket bekräftar att du framgångsrikt har **konverterat bilder till text**.

---

## Hantera vanliga edge‑cases

| Situation | What to Do |
|-----------|------------|
| **Low‑resolution PNG** | Öka `ocrEngine.ImageProcessingOptions.Dpi` före igenkänning. |
| **Multiple languages** | Sätt `ocrEngine.Language = Language.English | Language.Spanish;` (bitvis OR). |
| **Large batch (hundreds of files)** | Processa i omgångar (t.ex. 20 filer per `RecognizeImagesAsync`‑anrop) för att undvika minnesspikar. |
| **Need the confidence score** | Använd `ocrResults[i].Confidence` (en float mellan 0 och 1) för att filtrera lågkvalitetsresultat. |

Dessa justeringar håller din OCR‑pipeline robust, särskilt när du går från en demo till produktion.

---

## Bonus: Spara resultaten till en textfil

Om du föredrar en beständig kopia istället för konsolutdata, lägg till en liten hjälpfunktion:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Nu har du en enda fil som **extraherar text från bilder** för efterföljande bearbetning—perfekt för indexering, sökning eller att mata in i en språkmodell.

---

## Slutsats

Vi har gått igenom **hur man använder OCR** i C# med Aspose för att **extrahera text från PNG**‑filer och **konvertera bilder till text** på ett effektivt sätt. Den asynkrona metoden säkerställer att din applikation förblir responsiv, medan det enkla API‑et håller koden läsbar och underhållbar.  

Prova det med dina egna dokument, experimentera med olika språk, och kanske till och med kedja utdata till ett sökindex eller en sammanfattningstjänst. Himlen är gränsen när du på ett pålitligt sätt kan omvandla bilder till sökbara strängar.

---

### Nästa steg & relaterade ämnen

- **Extrahera text från bilder** i andra format (JPEG, TIFF) – byt bara filändelserna.  
- **Batch‑bearbetning med Parallel.ForEach** för massiva arbetsbelastningar.  
- **Post‑OCR‑rengöring** med reguljära uttryck för att normalisera datum, belopp eller ID:n.  
- **Integrera med Azure Cognitive Services** om du behöver molnbaserad OCR med ytterligare funktioner.  

Känn dig fri att lämna en kommentar om du stöter på problem, eller dela hur du har utökat detta grundflöde. Lycka till med kodandet!   (Image: ![OCR‑resultatskärmdump som visar extraherad text](/images/ocr-result.png){.align-center alt="exempel på OCR‑utdata"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}