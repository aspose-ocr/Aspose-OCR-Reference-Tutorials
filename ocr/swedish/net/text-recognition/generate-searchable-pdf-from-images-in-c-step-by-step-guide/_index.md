---
category: general
date: 2026-02-22
description: Skapa en sökbar PDF och extrahera text från en bild med Aspose OCR. Lär
  dig hur du konverterar en bild till PDF och får ut ren text i en enda handledning.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: sv
og_description: Skapa sökbar PDF från skannade bilder med Aspose OCR. Denna guide
  visar hur du extraherar text från en bild, får ren text och konverterar bilden till
  PDF.
og_title: Skapa sökbar PDF från bilder – Komplett C#‑handledning
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Skapa sökbar PDF från bilder i C# – Steg‑för‑steg‑guide
url: /sv/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generera sökbar PDF från bilder i C# – Komplett handledning

Har du någonsin behövt **generera sökbar PDF** från en skannad bild men varit osäker på var du ska börja? Du är inte ensam—de flesta utvecklare stöter på den muren när de först möter OCR. Den goda nyheten? Med Aspose OCR kan du **extrahera text från bild**, **generera ren text** och **konvertera bild till PDF** på bara några rader C#.

I den här guiden går vi igenom hela processen, från att läsa in en PNG‑fil till att spara en sökbar PDF och en ren‑text‑fil. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket .NET‑projekt som helst. Inga onödiga detaljer, bara det som får jobbet gjort.

## Vad du kommer att lära dig

- Hur du installerar **Aspose.OCR** i en .NET‑konsolapp.  
- Skillnaden mellan **output plain text** och **searchable PDF**‑lägen.  
- Hur du **extract text from image** och skriver den till en `.txt`‑fil.  
- Hur du **convert image to PDF** som behåller den ursprungliga bitmapen samtidigt som ett dolt textlager läggs till.  
- Tips för att hantera stora batcher, vanliga fallgropar och var du kan justera inställningarna för bättre noggrannhet.

> **Förutsättningar** – Du behöver .NET 6+ (eller .NET Framework 4.7+), Visual Studio 2022 (eller någon editor), och en Aspose OCR‑licens (eller en gratis provversion). Inga andra tredjepartsbibliotek krävs.

![exempel på genererad sökbar PDF](image-placeholder.png "Exempel på en genererad sökbar PDF")

## Steg 1: Installera Aspose OCR och skapa motorn

Först och främst—lägg till NuGet‑paketet i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

Nu kan vi starta OCR‑motorn och ange vilket språk vi arbetar med. Engelska är standard, men du kan byta till franska, spanska osv. genom att ändra `Language`‑enumet.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Varför detta är viktigt:** Motorn innehåller all konfiguration—språk, utdataformat och valfria förbehandlingsflaggor. Att ställa in den en gång och återanvända den undviker overheaden av att skapa en ny instans för varje fil.

## Steg 2: Extrahera text och spara som ren text

Om du bara behöver de råa tecknen, byt motorn till `OutputFormat.Text`. Detta instruerar Aspose OCR att hoppa över PDF‑generering helt och ge dig en sträng.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Proffstips:** `plainTextResult.Text` tar redan bort radbrytningar som hör till OCR‑layouten. Om du behöver det ursprungliga avståndet, inspektera `plainTextResult.TextBlocks` istället.

### Förväntat resultat

Öppna `output.txt` och du bör se något liknande:

```
Hello, world!
This is a sample scanned document.
```

Det är delen **output plain text** i handledningen—snabb, lättviktig och perfekt för efterföljande bearbetning (t.ex. indexering).

## Steg 3: Byt till sökbar PDF‑läge

Låt oss nu skapa en **sökbar PDF**. Motorn kommer att bädda in den ursprungliga bitmapen och lägga OCR‑genererad text under den, vilket gör dokumentet sökbart i vilken PDF‑visare som helst.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Varför vi åter‑igenkänner:** OCR‑motorn cachar den senaste bilden, men utdataformatet bestämmer vilken data den returnerar. Att byta format tvingar ett nytt pass som inkluderar det dolda textlagret.

### Så ser PDF‑filen ut

Öppna `output.pdf` i Adobe Reader eller någon annan visare och försök markera text. Du kommer att se att du kan kopiera, söka och markera innehållet—trots att den visuella framställningen fortfarande är den ursprungliga bitmapen. Det är kännetecknet för en **convert scanned image pdf**.

## Steg 4: Hantera flera filer (valfritt)

Verkliga projekt hanterar sällan bara en bild. Nedan är en snabb loop som bearbetar varje PNG i en mapp och skapar motsvarande `.txt`‑ och `.pdf`‑filer.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Obs om kantfall:** Stora bilder kan tömma minnet. Om du får `OutOfMemoryException`, överväg att skala ner med `Image.Resize` innan igenkänning, eller bearbeta filer i mindre batcher.

## Steg 5: Finjustera OCR‑noggrannhet

Aspose OCR erbjuder några reglage du kan justera:

| Inställning | Vad den gör | När den används |
|------------|-------------|-----------------|
| `ocrEngine.PageSegmentationMode` | Styr hur motorn delar upp bilden i textblock. | Användbart för flerkolumnslayouter. |
| `ocrEngine.Deskew` | Auto‑roterar lätt lutade sidor. | Skannade dokument som inte är perfekt justerade. |
| `ocrEngine.RemoveNoise` | Försöker rensa fläckar och bakgrundsartefakter. | Lågt kvalitativa skanningar eller faxade sidor. |

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Att aktivera dessa alternativ kan öka behandlingstiden, men vinsten i **extract text from image**‑kvalitet är ofta värd det.

## Steg 6: Verifiera utdata programatiskt

Ibland behöver du bekräfta att PDF‑filen faktiskt innehåller sökbar text (t.ex. i automatiserade tester). Det enklaste testet är att verifiera att PDF‑byte‑arrayen inte är tom och att `RawData`‑längden överstiger bildens storlek.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

För djupare validering kan du använda ett PDF‑bibliotek (som iTextSharp) för att extrahera textströmmen och jämföra den med `plainTextResult.Text`.

## Vanliga fallgropar & hur du undviker dem

- **Missing License** – Utan en giltig Aspose‑licens körs biblioteket i evalueringsläge, vilket lägger till ett vattenmärke i PDF‑filer. Registrera din licens tidigt (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Incorrect Path** – Att hårdkoda absoluta sökvägar fungerar på din maskin men går sönder någon annanstans. Använd `Path.Combine` med `AppDomain.CurrentDomain.BaseDirectory` för portabilitet.  
- **Unsupported Image Formats** – GIF‑ och TIFF‑filer med flera ramar kräver särskild hantering (`Image.LoadMultiPage`). Konvertera dem till PNG/JPEG först om du bara behöver den första sidan.  
- **Performance Bottlenecks** – Att återskapa `OcrEngine` i en loop är kostsamt. Behåll en enda instans och ändra bara `OutputFormat` som visas.

## Sammanfattning

Vi har gått igenom hela arbetsflödet för att **generate searchable PDF** från en skannad bild med Aspose OCR:

1. Installera NuGet‑paketet och skapa en `OcrEngine`.  
2. Ställ in `OutputFormat.Text` till **output plain text** och skriv den till en `.txt`‑fil.  
3. Byt till `OutputFormat.SearchablePdf` för att **convert image to PDF** med ett osynligt textlager.  
4. Spara PDF‑bytena och loopa eventuellt över en katalog för batch‑bearbetning.  
5. Finjustera noggrannheten med deskew, noise removal och page segmentation‑alternativ.  

Allt detta får plats i ett kompakt, självständigt program som du kan kopiera‑klistra in i Visual Studio.

## Vad du kan prova härnäst?

- **Batch processing** med ett UI‑gränssnitt (WinForms eller WPF) så att användare kan dra‑och‑släppa filer.  
- **Language detection** – Aspose OCR kan automatiskt upptäcka språk; prova `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑processing** – Skicka den extraherade texten till ett sökindex (ElasticSearch, Azure Cognitive Search) för omedelbar dokumenthämtning.  
- **Alternative outputs** – Använd `OutputFormat.Hocr` för HTML‑baserade OCR‑resultat, användbart för webbförhandsvisningar.

Känn dig fri att experimentera med olika bildupplösningar, färglägen och OCR‑inställningar. Ju mer du leker, desto bättre förstår du avvägningarna mellan hastighet och noggrannhet.

---

**Lycka till med kodningen!** Om du stöter på några problem, lämna en kommentar nedan eller kolla Aspose OCR‑dokumentationen för djupare insikter. Ditt nästa projekt—oavsett om det handlar om fakturering, arkivering eller att bygga en sökbar kunskapsbas—har precis blivit mycket enklare.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}