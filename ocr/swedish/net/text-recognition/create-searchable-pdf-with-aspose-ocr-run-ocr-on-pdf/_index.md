---
category: general
date: 2026-05-28
description: Skapa sökbar PDF med Aspose OCR i C#. Lär dig hur du kör OCR på PDF,
  känner igen text i PDF och omvandlar en OCR‑skannad PDF till en sökbar PDF.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: sv
og_description: Skapa sökbar PDF med Aspose OCR i C#. Följ den här steg‑för‑steg‑guiden
  för att köra OCR på PDF, känna igen text i PDF och hantera OCR‑skannade PDF‑filer.
og_title: Skapa sökbar PDF med Aspose OCR – Kör OCR på PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Skapa sökbar PDF med Aspose OCR – Kör OCR på PDF
url: /sv/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF med Aspose OCR – Kör OCR på PDF

Har du någonsin behövt **skapa sökbara PDF**‑filer från en hög med skannade dokument? Du är inte ensam. I många kontorsarbetsflöden är det enda som står mellan dig och ett fullt sökbart arkiv några rader kod som kör OCR på PDF‑sidor.  

I den här handledningen går vi igenom ett komplett, färdigt exempel som visar exakt hur du **skapar sökbara PDF**‑filer med Aspose OCR för .NET‑biblioteket. När du är klar vet du hur du *kör OCR på PDF*, *känner igen text‑PDF*‑filer och omvandlar en *OCR‑skannad PDF* till en sökbar version utan några tredjepartstjänster.

> **Förutsättningar** – Ett aktuellt .NET‑SDK (6.0+ rekommenderas), en giltig Aspose.OCR för .NET‑licens (eller en tillfällig utvärderingsnyckel) samt en PDF‑fil du vill bearbeta.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## Vad den här guiden täcker

- Installera Aspose OCR‑biblioteket i ett C#‑projekt.  
- Ladda en käll‑PDF (valfritt antal sidor).  
- Konfigurera motorn för att producera en **sökbar PDF**.  
- Köra OCR‑processen och spara resultatet.  
- Tips för att hantera flersidiga dokument, språkval och vanliga fallgropar.  

Om du följer varje steg får du en fil som du kan öppna i Adobe Reader, trycka **Ctrl + F**, och omedelbart söka efter vilket ord som helst som fanns i den ursprungliga skanningen.

---

## Steg 1: Installera Aspose OCR för .NET

Innan du skriver någon kod, lägg till NuGet‑paketet i ditt projekt:

```bash
dotnet add package Aspose.OCR
```

> **Pro‑tips:** Använd flaggan `--version` för att låsa till den senaste stabila versionen (t.ex. `Aspose.OCR 23.10`). Detta säkerställer kompatibilitet med .NET 6 och nyare.

---

## Steg 2: Skapa en OCR‑motorinstans

Kärnan i processen är `OcrEngine`. Tänk på den som hjärnan som läser bilder och ger tillbaka text. Att initiera den är enkelt:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

`OcrEngine`‑objektet kommer att hålla både inmatnings‑imagestreamen och konfigurationen som talar om för Aspose hur du vill ha utdata.

---

## Steg 3: Ladda käll‑PDF‑filen (Kör OCR på PDF)

Aspose OCR kan läsa in en PDF direkt; den extraherar varje sida som en bild internt. Ersätt platshållar‑sökvägen med platsen för ditt skannade dokument:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Varför detta fungerar:** Metoden `ImageStream.FromFile` upptäcker automatiskt PDF‑formatet och förbereder en rasterrepresentation för OCR. Inget extra konverteringssteg behövs.

---

## Steg 4: Konfigurera utdataformat och språk

Här talar vi om för Aspose vad vi vill ha tillbaka. Genom att sätta `OutputFormat` till `SearchablePdf` instrueras motorn att bädda in den igenkända texten bakom de ursprungliga sidbilderna, vilket skapar en **sökbar PDF**. Du kan också välja språk för att förbättra noggrannheten – engelska är standard, men du kan byta till franska, tyska osv.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Om du behöver bearbeta ett tvåspråkigt dokument kan du kombinera språk med `Language`‑enum‑flaggorna.

---

## Steg 5: Kör OCR‑processen – Känn igen text‑PDF

Nu sker det tunga arbetet. Metoden `Recognize` skannar varje sida, extraherar glyfer och bygger ett internt PDF‑flöde som innehåller både originalbilden och ett osynligt textlager. Detta är steget där vi *känner igen text‑PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Vanlig fråga:** *Vad händer om PDF‑filen har 200 sidor?*  
> Motorn bearbetar sidor sekventiellt och strömmar resultat, så minnesanvändningen förblir måttlig. För extremt stora filer kan du vilja öka inställningen `MemoryLimit` i `ocrEngine.Configuration`.

---

## Steg 6: Spara den sökbara PDF‑filen

Till sist skriver vi utdata till disk. Metoden `Save` skriver det interna flödet till en ny fil som du kan öppna med vilken PDF‑visare som helst.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Kör programmet (`dotnet run`) och se konsolen bekräfta att filen skapats. Öppna `handbook_searchable.pdf` och försök söka efter ett ord du vet finns i den ursprungliga skanningen – du bör se träffar omedelbart.

---

## Hantera kantfall och avancerade scenarier

### Flera språk (OCR‑skannad PDF)

Om din käll‑PDF innehåller både engelska och spanska texter, kombinera språk:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR byter automatiskt ordböcker, vilket ökar noggrannheten för dokument med blandade språk.

### Lösenordsskyddade PDF‑filer

När du arbetar med skyddade PDF‑filer, ange lösenordet innan du anropar `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Om lösenordet är fel kastar `Recognize` ett `InvalidPasswordException`; genom att fånga detta kan du be användaren om ett korrekt lösenord.

### Styr bildkvaliteten

Högre DPI ger bättre OCR‑resultat men kräver mer minne. Justera DPI‑värdet om du märker otydliga tecken:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Licens vs. utvärderingsläge

I utvärderingsläge visas ett vattenstämpel på varje sida. För att ta bort den, applicera din licens innan något OCR‑anrop:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Pro‑tips för produktionsanvändning

- **Batch‑behandling:** Packa in kärnlogiken i en `foreach`‑loop som itererar över en lista med PDF‑filer. Disposera `OcrEngine` efter varje fil för att frigöra inhemska resurser.  
- **Loggning:** Använd `ocrEngine.Configuration.Logger` för att samla detaljerad OCR‑statistik (t.ex. erkända tecken per sekund). Detta är ovärderligt när du felsöker låg noggrannhet.  
- **Prestanda‑optimering:** På fler‑kärniga servrar, skapa separata `OcrEngine`‑objekt per tråd; biblioteket är trådsäkert när varje instans är isolerad.  
- **Felhantering:** Omslut alltid `Recognize` och `Save` med `try/catch`‑block. Vanliga undantag inkluderar `FileNotFoundException`, `OutOfMemoryException` och `UnsupportedFormatException`.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Förväntad utskrift** (konsol):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Öppna den resulterande filen, tryck **Ctrl + F**, och du kan hitta vilket ord som helst som fanns i de ursprungliga skannade sidorna. Det är magin i att omvandla en *OCR‑skannad PDF* till en **sökbar PDF**.

---

## Slutsats

Vi har just demonstrerat hur man **skapar sökbara PDF**‑filer med Aspose OCR för .NET, och täckt allt från installation av paketet till hantering av flerspråkiga och lösenordsskyddade PDF‑filer. Genom att följa dessa steg kan du på ett pålitligt sätt *köra OCR på PDF*‑dokument, *känna igen text‑PDF*‑innehåll och konvertera vilken *OCR‑skannad PDF* som helst till en fullt sökbar resurs.

### Vad blir nästa steg?

- Utforska **aspose ocr pdf**‑API:n vidare: extrahera ren text, exportera till DOCX eller generera sökbara PDF‑filer i bulk.  
- Kombinera den sökbara PDF‑utdata med Aspose.PDF för att lägga till bokmärken eller vattenstämplar.  
- Experimentera med olika DPI‑inställningar eller anpassade OCR‑ordböcker för specialteckensnitt.

Känn dig fri att justera exemplet, integrera det i din dokumenthanterings‑pipeline eller ställa frågor i kommentarerna. Lycka till med kodandet, och njut av att förvandla de oläsliga skanningarna till sökbart guld!

## Relaterade handledningar

- [Hur man OCR‑ar PDF i .NET med Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Hur man gör OCR på PDF i .NET med Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [Hur man utför OCR på en PDF‑fil i .NET med Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}