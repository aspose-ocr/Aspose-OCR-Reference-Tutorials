---
category: general
date: 2026-01-09
description: c# OCR-handledning som visar hur man extraherar text från bildfiler och
  konverterar DJVU till text med Aspose.OCR. Lär dig steg‑för‑steg‑extraktion på några
  minuter.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: sv
og_description: c# OCR-handledning som snabbt visar hur man extraherar text från bildfiler
  och konverterar DJVU till text med Aspose.OCR. Följ guiden för en fungerande lösning.
og_title: c# OCR-handledning – Extrahera text från bild & DJVU
tags:
- OCR
- C#
- Aspose
title: 'c# OCR-handledning: Extrahera text från bild och DJVU-filer'
url: /sv/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR‑handledning – Extrahera text från bild och DJVU‑filer

Har du någonsin undrat hur man extraherar text från bildfiler utan att rycka ur håret? I den här **c# OCR‑handledningen** går vi igenom ett komplett, färdigt‑att‑köra‑exempel som drar ut text från en vanlig bild *och* ett DJVU‑dokument.

Om du också letar efter ett snabbt sätt att **konvertera DJVU till text**, är du på rätt plats—inga extra konverterare, bara ren C#‑kod.

## Vad du kommer att lära dig

- Hur du installerar Aspose.OCR‑biblioteket i ett .NET‑projekt.  
- Den exakta koden du behöver för att **extrahera text från bild**‑filer.  
- En kort metod för **extrahering av text från DJVU**‑filer (ja, samma motor gör det).  
- Vanliga fallgropar (stora filer, saknade typsnitt, licensiering) och hur du undviker dem.  

Allt du behöver är ett aktuellt .NET‑SDK och en internetanslutning för att hämta NuGet‑paketet. Ingen tidigare OCR‑erfarenhet krävs.

## Förutsättningar

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.OCR riktar sig mot .NET Standard 2.0, så .NET 6+ ger dig bästa prestanda. |
| Visual Studio 2022 (or VS Code) | IDE:er gör paketshantering smärtfri, men vilken editor som helst fungerar. |
| NuGet package **Aspose.OCR** | Detta är motorn som faktiskt gör det tunga lyftet. |
| A sample image (`sample.png`) and a DJVU file (`sample.djvu`) | Vi kommer att använda dessa för att demonstrera båda extraktionsscenarierna. |

Du kan installera paketet med följande kommando:

```bash
dotnet add package Aspose.OCR
```

> **Proffstips:** Om du kör på en CI‑server, lägg till `--no-restore` i byggsteget och återställ en gång i början för att snabba upp processen.

## Steg 1: Initiera OCR‑motorn – hjärtat i c# OCR‑handledningen

Det första vi gör är att skapa en instans av `OcrEngine`. Tänk på det som att slå på skannern i din programvara.

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

Varför skapa en ny motor varje gång? Eftersom motorn innehåller konfiguration (språk, detekteringsläge osv.). Genom att börja på nytt undviker du att gamla inställningar läcker mellan körningar.

## Steg 2: Ladda och känna igen en bild – hur man extraherar text från bild

Nu matar vi in en vanlig bitmap (PNG, JPEG, BMP…) i motorn. Metoden `RecognizeImage` returnerar den detekterade strängen.

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

A few things to note:

* **Filens existens** – Om sökvägen är fel kastar metoden `FileNotFoundException`. Omge den med ett `try/catch` om du förväntar dig användar‑angivna sökvägar.
* **Bildkvalitet** – OCR fungerar bäst på 300 dpi eller högre. Lågreolerade skanningar kan ge förvrängd output.
* **Språkstöd** – Som standard antar Aspose.OCR engelska. För att ändra det, sätt `ocrEngine.Language = Language.Spanish;` innan `RecognizeImage`.

## Steg 3: Känna igen text från ett DJVU‑dokument – konvertera DJVU till text

DJVU är ett containerformat som kan innehålla flera sidor. Aspose.OCR kan hantera det direkt; du pekar bara på filen.

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

Bakom kulisserna extraherar motorn varje sida som en bild och kör samma igenkänningspipeline. Därför behöver du inget separat steg för “konvertera DJVU till text”—OCR‑motorn gör det åt dig.

### Hantera flersidiga DJVU‑filer

Om ditt DJVU innehåller flera sidor, concatenar `RecognizeImage` dem i ordning. Om du behöver varje sida separat, kan du använda överlagringen som returnerar en `List<string>`:

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## Steg 4: Finjustera motorn för bättre noggrannhet – varför detta är viktigt

Resultaten direkt ur lådan är hyfsade, men du kan förbättra dem genom att justera ett par inställningar:

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

Dessa flaggor är särskilt användbara när du **extraherar text** från skannade PDF‑filer som först sparats som DJVU. Att slå på orienteringsdetektering sparar dig från att manuellt rotera bilder.

## Steg 5: Hantera licensiering och körningsfel

Aspose.OCR levereras med en gratis provversion som stämplar “Demo” på output efter några sidor. För att ta bort vattenstämpeln, lägg till din licensfil:

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

Om du glömmer detta steg fungerar motorn fortfarande, men resultatet kommer att innehålla ordet “Demo”. Var också uppmärksam på `OutOfMemoryException` när du bearbetar enorma DJVU‑filer—överväg att bearbeta sida‑för‑sida som visat tidigare.

## Komplett, körbart exempel

Nedan är ett självständigt konsolprogram som sätter ihop allt. Kopiera‑klistra, justera filsökvägarna och tryck på **Run**.

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Förväntad output** (förutsatt att filerna innehåller frasen “Hello World”):

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

Om källan innehåller flera rader kommer de att visas exakt som i originaldokumentet.

## Vanliga frågor & hantering av kantfall

* **Vad händer om bilden är svart‑vit?**  
  OCR fungerar bra, men du kan förbättra kontrasten med `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;`.

* **Kan jag extrahera bara siffror?**  
  Ja—sätt `ocrEngine.CharWhitelist = "0123456789";` innan du anropar `RecognizeImage`.

* **Finns det någon gräns för filstorlek?**  
  Motorn läser in hela filen i minnet. För filer större än ~100 MB, bearbeta sida‑för‑sida (se steg 3:s list‑överlagring).

* **Hur skiljer sig detta från Tesseract?**  
  Aspose.OCR är ett kommersiellt bibliotek med inbyggt DJVU‑stöd och utan inhemska beroenden, medan Tesseract kräver native‑binärer och separata verktyg för DJVU‑konvertering.

## Slutsats

Du har just slutfört en **c# OCR‑handledning** som visar hur man **extraherar text från bild**‑filer och sömlöst **konverterar DJVU till text** med Aspose.OCR. Exemplet täcker allt från paketinstallation till licensiering, från enkelsidig bildextraktion till hantering av flersidiga DJVU‑filer, och även tips för att öka noggrannheten.

Nästa steg kan du utforska **hur man extraherar text** från PDF‑filer, integrera OCR‑steget i ett webb‑API, eller experimentera med språkpaket för flerspråkiga dokument. Himlen är gränsen—kom bara ihåg huvudpoängerna: ställ in motorn, mata den med en fil, och läs tillbaka strängen.

Har du fler frågor? Lämna en kommentar, prova koden på dina egna dokument, och lycka till med kodandet! 

![c# OCR‑handledning skärmbild som visar konsoloutput](/images/csharp-ocr-tutorial.png "c# OCR‑handledning – exempel på konsoloutput")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}