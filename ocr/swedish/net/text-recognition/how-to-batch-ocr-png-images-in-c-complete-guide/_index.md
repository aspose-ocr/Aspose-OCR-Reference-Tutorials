---
category: general
date: 2026-03-17
description: Hur man batch‑OCR:ar PNG‑bilder i C# snabbt. Lär dig att extrahera text
  från PNG‑filer, konvertera PNG till text och läsa bilder från en katalog med ett
  enkelt skript.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: sv
og_description: Hur du batch‑OCR‑ar PNG‑bilder i C# med steg‑för‑steg‑kod. Extrahera
  text från PNG‑filer, konvertera PNG till text och läs bilder från en katalog utan
  ansträngning.
og_title: Hur man batchar OCR på PNG‑bilder i C# – Komplett guide
tags:
- OCR
- C#
- Image Processing
title: Hur man batch-OCR:ar PNG‑bilder i C# – Komplett guide
url: /sv/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

Edge case", "Common pitfall". Should we translate those? Probably keep them as English? The rule says keep technical terms in English, but these are not technical terms. We can translate them: "Proffstips", "Tips", "Kantfall", "Vanligt fallgropp". Already translated.

Make sure we keep markdown formatting: headings, blockquote >, tables, code block placeholders unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch-OCR:ar PNG-bilder i C# – Komplett guide

Har du någonsin undrat **hur man batch-OCR:ar** en mapp full av skärmdumpar utan att öppna varje fil manuellt? Du är inte ensam—utvecklare frågar ständigt hur man batch-OCR:ar stora samlingar av PNG-filer, särskilt när målet är att extrahera text‑PNG‑filer för vidare analys.  

I den här handledningen går vi igenom ett färdigt C#‑exempel som **extraherar text‑PNG**‑filer, **konverterar PNG till text**, och visar dig det bästa sättet att **läsa bilder från katalog**. I slutet har du ett enda skript som skapar en `.txt`‑fil bredvid varje bild, vilket sparar dig timmar av manuellt kopierande.

## Vad du kommer att uppnå

- Initiera en OCR‑motor en gång och återanvänd den för hela batchen.  
- Skanna varje `*.png` i en given mapp utan att skriva en loop själv.  
- Skriv varje OCR‑resultat till en egen textfil, bevara det ursprungliga filnamnet.  
- Hantera vanliga kantfall som tomma mappar eller icke‑bildfiler på ett smidigt sätt.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Core och .NET Framework).  
- Ett OCR‑bibliotek som exponerar typerna `OcrEngine`, `ImageStream` och `OcrResult` (t.ex. det fiktiva **FastOCR**‑SDK:t som används i kodsnuttarna).  
- Grundläggande kunskaper i C#—inga avancerade mönster krävs.

---

## Så batch-OCR:ar du PNG‑bilder – Översikt

Nedan är det **kompletta, körbara programmet**. Kopiera och klistra in det i ett nytt konsolprojekt, ersätt platshållar‑sökvägarna och tryck på **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Förväntat resultat:** För varje `image01.png` hittar du en `image01.txt` som innehåller de igenkända tecknen. Konsolen listar varje fil när den skrivs.

![Diagram för batch OCR](how-to-batch-ocr-diagram.png "Diagram som illustrerar hur man batch-OCR:ar PNG‑bilder med C#")

---

## Steg‑för‑steg‑förklaring

### 1. Initiera OCR‑motorn – processens hjärta  

Raden `var ocrEngine = new OcrEngine();` skapar en enda motorinstans som återanvänds för hela batchen. Att återanvända motorn är **avgörande** eftersom de flesta OCR‑bibliotek allokerar tunga resurser (som språkmodeller) vid konstruktion. Att initiera en gång förbättrar prestandan dramatiskt—särskilt när du har dussintals eller hundratals PNG‑filer.  

> **Proffstips:** Om du behöver ett annat språk än engelska, sätt `ocrEngine.Config.Language = Language.Spanish;` (eller någon annan stödjande enum).  

### 2. Läs bilder från katalog – hitta varje PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` gör exakt vad det sekundära nyckelordet *read images from directory* lovar. Det returnerar en array av absoluta sökvägar, som vi senare matar in i OCR‑motorn.  

> **Varför inte använda `SearchOption.AllDirectories`?** Om dina bilder är nästlade kan du byta till `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Kom bara ihåg att djupare sökningar kan medföra oönskade filer, så filtrera därefter.  

### 3. Konvertera filsökvägar till ImageStream‑objekt  

De flesta OCR‑SDK:n förväntar sig en ström snarare än en rå sökväg. LINQ‑uttrycket `Select(path => ImageStream.FromFile(path)).ToList()` bygger en **lista av strömmar** som batch‑igenkännaren kan konsumera i ett anrop. Detta steg säkerställer också att filhandtag öppnas endast en gång, vilket minskar I/O‑överhead.  

> **Kantfall:** Om en fil är korrupt kan `ImageStream.FromFile` kasta ett undantag. Omge konverteringen med en `try/catch` om du behöver motståndskraft.  

### 4. Känn igen text i hela batchen  

`ocrEngine.RecognizeBatch(imageStreams)` är den perfekta lösningen för *how to batch OCR*. Istället för att loopa över varje bild och anropa en enskild‑bild‑metod, överlämnar vi hela samlingen till motorn. Internt kan biblioteket parallellisera arbetet, vilket ger dig en hastighetsökning på fler‑kärniga maskiner.  

> **Tips:** Om ditt OCR‑bibliotek inte exponerar en batch‑metod kan du ändå uppnå liknande prestanda genom att använda `Parallel.ForEach` runt den enskilda bild‑`Recognize`‑anropet.  

### 5. Skriv varje OCR‑resultat – konvertera PNG till text  

Den sista `for`‑loopen skriver `ocrResults[i].Text` till en `.txt`‑fil vars namn speglar den ursprungliga PNG‑filen. Detta är exakt vad det sekundära nyckelordet *convert PNG to text* beskriver. Anropet `Path.Combine` garanterar att utmatningsmappen finns och förhindrar path‑traversal‑buggar.  

> **Vanligt fallgropp:** Att glömma att skapa utmatningsmappen först kommer att orsaka ett `DirectoryNotFoundException`. Raden `Directory.CreateDirectory(outputFolder);` löser det i förväg.  

---

## Hantera variationer i verkligheten

| Situation | Vad som ska ändras | Varför |
|-----------|--------------------|--------|
| **Tom inmatningsmapp** | Behåll det tidiga `if (imagePaths.Length == 0)`‑skyddet | Förhindrar ett onödigt OCR‑anrop och ger ett vänligt meddelande |
| **Blandade filtyper** | Använd `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Säkerställer att du endast bearbetar PNG‑filer, vilket uppfyller *extract text png* utan fel |
| **Stora bilder ( > 5 MB )** | Nedskala innan du matar in i OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (om API stödjer) | Minskar minnesbelastning och förbättrar ofta igenkänningsnoggrannheten |
| **Annat OCR‑språk** | Sätt `ocrEngine.Config.Language = Language.French;` | Anpassar motorn till språket i källbilderna |

---

## Vanliga frågor (FAQ)

**Q: Fungerar detta med JPEG‑ eller TIFF‑filer?**  
A: Kärnlogiken förblir densamma; byt bara sökmönstret till `"*.jpg"` eller `"*.tif"` och säkerställ att OCR‑biblioteket kan avkoda dessa format.

**Q: Hur kan jag bearbeta tusentals bilder utan att få slut på minne?**  
A: Ersätt batch‑anropet med ett strömnings‑tillvägagångssätt—processa en delmängd på t.ex. 50 bilder åt gången, och släpp sedan strömmarna innan nästa del laddas.

**Q: Jag behöver OCR‑konfidenspoängen. Var hittar jag den?**  
A: De flesta `OcrResult`‑objekt exponerar en `Confidence`‑egenskap. Du kan utöka skriv‑steget:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Sammanfattning

Vi har precis gått igenom **hur man batch-OCR:ar** PNG‑bilder i C# från början till slut. Genom att initiera en enda motor, läsa bilder från katalog, konvertera dem till strömmar, känna igen hela batchen och slutligen skriva varje resultat till en textfil, har du nu ett robust, produktionsklart mönster för uppgifterna **extract text PNG**, **convert PNG to text** och **read images from directory**.  

Vad blir nästa steg? Prova att byta OCR‑leverantör, lägg till flertrådad efterbehandling (t.ex. stavningskontroll), eller mata `.txt`‑filerna i ett sökindex. Himlen är gränsen när du har bemästrat batch‑arbetsflödet.  

Har du ett eget knep du vill dela? Lämna en kommentar, och lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}