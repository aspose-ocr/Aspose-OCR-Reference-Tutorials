---
category: general
date: 2026-02-17
description: Hur man batch‑OCR:ar flera PDF‑filer och bilder i C# med Aspose OCR.
  Lär dig att extrahera text från PDF, konvertera PDF till text och känna igen text
  i bilder.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: sv
og_description: Hur man batch‑OCR:ar flera dokument i C# med Aspose OCR. Få steg‑för‑steg‑kod
  för att extrahera text från PDF, konvertera PDF till text och känna igen text från
  bilder.
og_title: Hur man batchar OCR-filer i C# – Komplett guide
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Hur man batchar OCR-filer i C# – Fullständigt kodexempel
url: /sv/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så batchar du OCR-filer i C# – Komplett guide

Har du någonsin funderat **how to batch OCR** en hög med PDF‑ och bildskanningar utan att skriva en separat loop för varje fil? Du är inte ensam. De flesta utvecklare stöter på detta hinder när de behöver hämta text från dussintals sidor på en gång. Den goda nyheten? Med Aspose OCR kan du mata in en samling filer till en enda motor och låta den sköta det tunga arbetet.  

I den här handledningen går vi igenom en praktisk lösning som låter dig **extract text from pdf**, **convert pdf to text** och **recognize text from images** i ett enda batch‑körning. När du är klar har du en färdig konsolapp som skriver ut OCR‑resultatet för varje sida, och du förstår varför varje steg behövs så att du kan anpassa det till dina egna projekt.

## Förutsättningar – Vad du behöver innan vi börjar

- **.NET 6.0 eller senare** (koden fungerar även på .NET Framework, men .NET 6+ rekommenderas)
- **Aspose.OCR NuGet‑paket** – installera med `dotnet add package Aspose.OCR`
- Ett par exempel‑filer: en fler‑sidig PDF (`doc1.pdf`) och en skannad TIFF (`doc2.tif`). Placera dem i en mapp du kan referera till, t.ex. `C:\OCRSamples`.
- Grundläggande kunskaper i C# – du bör vara bekväm med `using`‑satser och samlingar.

> Pro‑tips: Om du saknar licens erbjuder Aspose en gratis temporär nyckel som tar bort 100‑sidorsgränsen under utveckling.

## Steg 1: Skapa projektet och importera namnrymder

Skapa först ett nytt konsolprojekt (eller lägg till i ett befintligt) och importera de nödvändiga namnrymderna.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Varför detta är viktigt:** Att importera `Aspose.OCR.Image` ger dig den smidiga metoden `ImageStream.FromFile`, som automatiskt delar upp PDF‑sidor i separata bild‑strömmar. Det är den hemliga ingrediensen som gör batch‑bearbetning smärtfri.

## Steg 2: Initiera OCR‑motorn

Motorn är arbetshästen som kommunicerar med det underliggande OCR‑systemet. Du behöver bara en instans för hela batchen.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Förklaring:** Att återanvända samma `OcrEngine` minskar minnes‑churn och snabbar upp bearbetningen eftersom de inhemska biblioteken förblir laddade mellan sidor.

## Steg 3: Bygg en lista med bild‑strömmar

Här samlar vi alla dokument vi vill bearbeta. `ImageStream.FromFile` är smart nog att dela upp en PDF i enskilda sidor, så en tre‑sidig PDF blir tre separata strömmar bakom kulisserna.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Edge case:** Om du har en blandning av PDF‑, TIFF‑, JPEG‑ eller PNG‑filer, lägg bara till dem i samma lista – Aspose hanterar formatdetektionen automatiskt.

## Steg 4: Kör batch‑OCR‑operationen

Nu överlämnar vi listan till motorn. `RecognizeBatch` returnerar en samling `OcrResult`‑objekt, ett per sida.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Varför batch?** Att köra OCR sida‑för‑sida i en manuell loop tvingar motorn att initieras om varje gång, vilket kan dubbla bearbetningstiden. `RecognizeBatch` håller motorn varm och strömmar tillbaka resultat så snart de är tillgängliga.

## Steg 5: Skriv ut den igenkända texten

Till sist loopar vi igenom resultaten och skriver varje sidas text till konsolen. Här kan du ersätta `Console.WriteLine` med fil‑skrivningar, databas‑insättningar eller någon annan efterföljande åtgärd.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Förväntad konsolutdata

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Om du kör programmet med exempel‑filerna bör du se ett textblock för varje sida, vilket bevisar att du framgångsrikt **extract text scanned pdf** innehåll i ett enda pass.

## Hantera vanliga fallgropar

| Problem | Varför det händer | Snabb lösning |
|---------|-------------------|---------------|
| **Out‑of‑memory‑fel** | Stora PDF‑filer genererar många högupplösta bilder. | Begränsa DPI när du laddar PDF‑er: `ocrEngine.Settings.ImageDpi = 200;` |
| **Garbage‑tecken** | Källskanningen är låg kvalitet eller använder ett språk som inte stöds. | Ange språket explicit: `ocrEngine.Language = Language.English;` |
| **Partiella resultat** | Batch‑listan innehåller en korrupt fil. | Omge `RecognizeBatch` med try/catch och logga `e.Message` för den felande filen. |
| **Prestandaflaskhals** | Kör på en enda tråd på en maskin med flera kärnor. | Använd `Parallel.ForEach` med separata `OcrEngine`‑instanser per tråd (avancerat). |

## Bonus: Spara OCR‑resultat till textfiler

Om du föredrar att ha en separat `.txt`‑fil per sida, lägg bara till ett litet skrivblock i loopen:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Nu har du förvandlat **convert pdf to text** till en prydlig mapp med ren‑text‑filer – perfekt för efterföljande indexering eller sökning.

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Inga dolda beroenden, inga externa skript.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Kör `dotnet run` från projektmappen och se hur konsolen fylls med den extraherade texten. Det är **how to batch OCR** en samling dokument i bara några rader C#.

## Vad vi gick igenom – Snabb sammanfattning

- Skapade en .NET‑konsolapp och installerade Aspose.OCR.  
- Skapade en enda `OcrEngine`‑instans för att hålla processen effektiv.  
- Byggde en lista med `ImageStream`‑objekt som automatiskt delade upp PDF‑er i sidor.  
- Exekverade `RecognizeBatch` för att **extract text from pdf** och andra bildformat i ett svep.  
- Skröt ut resultaten och sparade dem eventuellt som individuella `.txt`‑filer, vilket fullbordade **convert pdf to text**‑arbetsflödet.  

## Nästa steg och relaterade ämnen

- **Skala upp**: Använd `Parallel.ForEach` med en pool av `OcrEngine`‑objekt för att bearbeta hundratals filer parallellt.  
- **Språkpaket**: Byt `Language.English` mot `Language.French` eller ladda ett eget lexikon när du behöver **recognize text from images** på andra språk.  
- **Efterbehandling**: Skicka OCR‑utdata genom en stavningskontroll eller en naturlig språk‑parser för att förbättra noggrannheten i skannade kontrakt.  
- **Alternativa bibliotek**: Jämför Aspose OCR med Tesseract.NET om du letar efter ett open‑source‑alternativ – båda kan **extract text scanned pdf**, men skiljer sig åt i licensiering och färdig noggrannhet.

---

![how to batch OCR example](alt="exempel på batch OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}