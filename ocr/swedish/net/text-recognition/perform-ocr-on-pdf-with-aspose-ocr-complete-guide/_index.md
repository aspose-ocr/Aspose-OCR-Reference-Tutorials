---
category: general
date: 2026-05-06
description: Lär dig hur du utför OCR på PDF-filer med Aspose OCR i C#. Denna handledning
  visar också hur du extraherar text från PDF och laddar PDF för OCR.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: sv
og_description: Upptäck hur du utför OCR på PDF med Aspose OCR i C#. Steg‑för‑steg‑kod,
  förklaringar och tips för att effektivt extrahera text från PDF.
og_title: Utför OCR på PDF med Aspose OCR – Komplett guide
tags:
- Aspose OCR
- C#
- PDF processing
title: Utför OCR på PDF med Aspose OCR – Komplett guide
url: /sv/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på PDF med Aspose OCR – Komplett guide

Har du någonsin behövt **perform OCR on PDF** filer men varit osäker på var du ska börja? Du är inte ensam. I många verkliga projekt—tänk automatiserad fakturabehandling eller digitalisering av arkiverade rapporter—är det ett måste att kunna extrahera text från en skannad PDF.  

I den här handledningen går vi igenom en praktisk lösning som inte bara **performs OCR on PDF** med Aspose OCR‑biblioteket, utan också visar hur du **extract text from PDF**, **load PDF for OCR**, och även hanterar flerspråkiga dokument. I slutet har du ett färdigt C#‑program som omvandlar vilken skannad PDF som helst till sökbar, redigerbar text.

## Vad du kommer att lära dig

- Hur du installerar Aspose OCR i ett .NET‑projekt.  
- De exakta stegen för att **load PDF for OCR** och mata in den i motorn.  
- Hur du mappar olika språk till enskilda sidor—användbart när en PDF blandar engelska, franska och tyska.  
- Sätt att verifiera resultatet och felsöka vanliga fallgropar.  

> **Pro tip:** Om du arbetar med stora PDF‑filer, överväg att bearbeta sidor parallellt för att spara minuter av körtid. Vi kommer att beröra det senare.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework).  
- En giltig Aspose OCR‑licens eller en temporär utvärderingsnyckel.  
- En skannad PDF med namnet `multilang.pdf` placerad i en mapp som du kan referera till från din kod.  

Inga andra tredjepartspaket krävs.

---

## Steg 1 – Installera Aspose OCR och skapa motorn

Först, lägg till NuGet‑paketet Aspose.OCR i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

När paketet är installerat kan du instansiera OCR‑motorn. Detta objekt är hjärtat i operationen; det vet hur man läser bilder, PDF‑filer och konverterar dem till text.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Varför detta är viktigt:** Att initiera motorn en gång och återanvända den över sidor minskar minnesbelastningen och snabbar upp bearbetningen.

---

## Steg 2 – Ladda PDF‑dokumentet för OCR

Motorn kan öppna PDF‑filer direkt, men du måste ange vilken fil den ska arbeta med. Detta är steget **load PDF for OCR** som många utvecklare förbiser.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

Byt ut `YOUR_DIRECTORY` mot den faktiska sökvägen på din maskin. Om filen är inbäddad som en resurs kan du också ladda den från en ström.

> **Edge case:** Om PDF‑filen är lösenordsskyddad, anropa `ocrEngine.LoadPdf(path, password)` för att ange dekrypteringslösenordet.

---

## Steg 3 – Mappa språk till sidor (valfritt men kraftfullt)

Ofta innehåller en skannad PDF sidor på olika språk. Som standard antar Aspose OCR engelska, vilket ger dåliga resultat på franska eller tyska sidor. Vi kommer att bygga en enkel ordbok som talar om för motorn vilket språk som ska användas per sida.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Varför du gör detta:** Att ange rätt språk förbättrar noggrannheten avsevärt, särskilt för accentuerade tecken och språk‑specifik interpunktion.

---

## Steg 4 – Kör OCR och fånga resultatet

Nu sker det tunga arbetet. Att anropa `Recognize()` bearbetar *alla* sidor enligt språk‑mappen vi just satte.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

`recognitionResult`‑objektet innehåller en `Text`‑egenskap som samlar den igenkända texten från varje sida.

---

## Steg 5 – Skriv ut den extraherade texten

Till sist skriver vi helt enkelt den kombinerade texten till konsolen—eller så kan du skriva den till en fil, en databas eller något annat system.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

Om du föredrar en fil:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Verifieringstips:** Öppna den resulterande `extracted_text.txt` och sök efter kända ord från varje språk. Om franska accenter visas felaktigt, dubbelkolla din språk‑karta.

---

## Fullt fungerande exempel

När alla bitar satts ihop, här är ett komplett, färdigt program. Kopiera och klistra in det i ett nytt konsolprojekt och tryck **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**Förväntad output** (avkortad för korthet):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## Hantera stora PDF‑filer och prestandajusteringar

Om din PDF innehåller hundratals sidor, överväg dessa justeringar:

1. **Chunked processing** – Processa 50 sidor åt gången, skriv sedan mellanstegresultat till disk.  
2. **Parallelism** – Använd `Parallel.ForEach` med separata `OcrEngine`‑instanser (varje motor är trådsäker efter initiering).  
3. **Memory management** – Anropa `ocrEngine.Dispose()` efter varje del för att frigöra inhemska resurser.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## Vanliga fallgropar & hur du åtgärdar dem

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Felaktiga tecken på franska sidor | Fel språk angivet | Se till att `PageLanguageProvider` returnerar `OcrLanguage.French` för dessa sidor. |
| Tom utdatafil | PDF inte laddad (fel sökväg) | Verifiera sökvägen och att filen inte är låst av en annan process. |
| Out‑of‑memory‑undantag på stora PDF‑filer | Motorn laddar hela PDF‑filen på en gång | Använd enkelsidiga överlagringen av `LoadPdf` eller bearbeta i delar. |
| Långsam bearbetning (> 5 min för 100 sidor) | Enkeltrådad körning | Aktivera parallell bearbetning som visat ovan. |

---

## Nästa steg – Gå bortom grundläggande OCR

Nu när du kan **perform OCR on PDF** och **extract text from PDF**, kanske du vill:

- **Searchable PDF creation** – Använd Aspose.PDF för att bädda in OCR‑texten tillbaka i den ursprungliga PDF‑filen, så den blir sökbar.  
- **Data extraction** – Använd reguljära uttryck för att extrahera fakturanummer, datum eller totalsummor från den extraherade texten.  
- **Integration with AI** – Skicka OCR‑resultatet till en språkmodell (t.ex. Azure OpenAI) för sammanfattning eller klassificering.  

Alla dessa tillägg bygger fortfarande på kärnfunktionen **load PDF for OCR**, så du har redan grunden.

---

## Slutsats

Vi har gått igenom allt du behöver för att **perform OCR on PDF**‑filer med Aspose OCR i C#. Från att installera biblioteket, ladda PDF‑filen, tilldela språk per sida, köra igenkänningsmotorn, och slutligen **extract text from PDF** och spara den, ger handledningen dig en självständig, produktionsklar lösning.  

Känn dig fri att experimentera med parallell bearbetning, olika språk‑kombinationer, eller till och med kombinera OCR‑texten med andra dokument‑bearbetningsbibliotek. Om du stöter på problem, kolla felsökningstabellen ovan eller lämna en kommentar—lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}