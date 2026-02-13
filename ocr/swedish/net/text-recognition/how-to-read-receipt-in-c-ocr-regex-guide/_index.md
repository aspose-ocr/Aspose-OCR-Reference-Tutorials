---
category: general
date: 2026-02-13
description: Hur man läser kvitto snabbt med Aspose OCR och extraherar beloppet med
  regex. Lär dig steg‑för‑steg att bearbeta kvitto med OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: sv
og_description: Hur man läser kvitto i C# med Aspose OCR och regex. Den här guiden
  visar hur du bearbetar kvitto med OCR och extraherar det totala beloppet.
og_title: Hur man läser kvitto i C# – Komplett OCR- och Regex-handledning
tags:
- OCR
- C#
- Regex
- Aspose
title: Hur man läser kvitto i C# – OCR + Regex‑guide
url: /sv/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

" Not needed.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man läser kvitto i C# – OCR + Regex‑guide

Har du någonsin undrat **hur man läser kvitto** bilder utan att manuellt skriva in varje rad? I många småföretagsappar behöver du hämta totalsumman från ett foto av ett kvitto, och att göra det för hand undergräver automatiseringens syfte. De goda nyheterna? Med Aspose OCR kan du låta motorn göra det tunga arbetet, och sedan hittar ett enkelt reguljärt uttryck totalen. I den här handledningen går vi igenom **process receipt with OCR**, extraherar beloppet med regex och får ett färdigt totalvärde att använda.

Du kommer att se ett komplett, körbart exempel, upptäcka varför kvittospråkmodellen är viktig, och få tips för att hantera kantfall som olika valutasymboler eller saknade “Total”-etiketter. Inga externa dokument behövs—allt du behöver finns här.

## Vad du kommer att lära dig

- Hur man konfigurerar Aspose OCR för kvitto‑specifik igenkänning (språkmodellen `Receipt` räta automatiskt upp och tar bort brus från bilden).  
- Hur man tillämpar ett reguljärt uttryck som **extract amount using regex** mönster som fungerar för de flesta kvitton i US‑stil.  
- Hur man hanterar vanliga variationer såsom “TOTAL”, “Total:”, eller “Grand Total – $12.34”.  
- Hur man skriver ut resultatet på ett säkert sätt och vad man gör när mönstret inte hittas.  

**Förutsättningar**: .NET 6+ (eller .NET Framework 4.7+), en giltig Aspose OCR‑licens eller provversion, och en bild av ett kvitto sparad lokalt. Det är allt—inga extra NuGet‑paket utöver Aspose.OCR.

---

## Steg 1 – Installera Aspose OCR och förbered projektet

### Varför detta är viktigt

Aspose OCR tillhandahåller en specialbyggd **process receipt with OCR**‑modell som vet hur man räta upp ett skrynkligt papper och ignorera bakgrundsbrus. Att använda den generiska textmodellen skulle ge fler fel, särskilt på lågupplösta skanningar.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Proffstips:** Håll licensfilen utanför din källkontrollsmapp för att undvika oavsiktliga incheckningar.

---

## Steg 2 – Konfigurera OCR‑motorn för kvittoigenkänning

### Varför detta är viktigt

Språkmodellen `Receipt` innehåller inbyggd räta‑upp‑funktion och brusreducering, vilket dramatiskt förbättrar noggrannheten på verkliga kvitton som ofta är vikta eller skrynkliga.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Steg 3 – Läs av text från kvittobilden

### Varför detta är viktigt

Du behöver den råa texten innan du kan tillämpa något regex. Metoden `RecognizeImage` returnerar ett `OcrResult` som innehåller hela strängen, förtroendescore och mer om du behöver det senare.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Förväntad OCR‑utdata (exempel)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Steg 4 – Bygg ett regex för att **Extract Amount Using Regex**

### Varför detta är viktigt

Kvitton finns i många format, men ordet “Total” (eller en nära variant) följt av ett dollarbelopp är ett pålitligt ankare. Mönstret nedan tolererar valfria mellanslag, kolon, bindestreck och ett valfritt `$`‑tecken.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Förklaring av mönstret**

| Part | Meaning |
|------|---------|
| `Total` | Söker efter ordet “Total” (skiftlägesokänsligt). |
| `\s*[:\-]?` | Tillåter valfritt whitespace, sedan ett valfritt kolon eller bindestreck. |
| `\s*\$?` | Valfritt whitespace och valfritt dollartecken. |
| `(\d+(\.\d{2})?)` | Fångar en eller flera siffror, eventuellt följt av en decimal och två cent. |

---

## Steg 5 – Skriv ut den extraherade totalen eller hantera saknad data

### Varför detta är viktigt

Även den bästa OCR:n kan missa ett ord, särskilt på suddiga kvitton. Att erbjuda en elegant återgång förhindrar krascher och ger dig en möjlighet för anpassad logik (t.ex. be användaren bekräfta).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Exempel på konsolutdata**

```
Total: $12.25
```

---

## Fullt fungerande exempel – Alla steg i en fil

Nedan är ett enda, självständigt program som du kan kopiera‑klistra in i ett konsolprojekt. Det innehåller kommentarer, felhantering och den valfria licensladdningen.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Köra programmet**

1. Skapa ett nytt konsolprojekt (`dotnet new console -n ReceiptReader`).  
2. Lägg till Aspose.OCR NuGet‑paketet (`dotnet add package Aspose.OCR`).  
3. Byt ut `YOUR_DIRECTORY/receipt.jpg` mot den faktiska sökvägen till en kvittobild.  
4. Bygg och kör (`dotnet run`).  

Du bör se OCR‑utskriften följt av `Total: $xx.xx` om allt stämmer.

---

## Hantera kantfall & vanliga variationer

### 1. Olika valutasymboler

If you deal with euros (€) or pounds (£), extend the pattern:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Saknad “Total”-etikett

Some receipts only show “Grand Total”. Add an alternation:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Flera totaler (t.ex. “Subtotal” och “Total”)

If the regex matches the first occurrence, you may want the **last** match:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Lågre­sultatbilder

- Öka DPI när du skannar (`300 DPI` är en bra nivå).  
- Förprocessa bilden med ett enkelt sudd‑reduceringsfilter innan du skickar den till Aspose (utanför denna guides omfattning, men värt att utforska).

---

## Proffstips för verkliga projekt

- **Cachea OCR‑resultatet** om du behöver extrahera flera fält (skatt, artiklar osv.) – du betalar OCR‑kostnaden bara en gång.  
- **Logga den råa OCR‑texten** till en databas; den blir ett värdefullt revisionsspår för tvistade utgifter.  
- När du bygger ett webb‑API, **kör OCR i en bakgrundsarbetsprocess**; det kan ta några hundra millisekunder, vilket är okej asynkront men inte idealiskt för en synkron begäran.  
- **Validera det extraherade beloppet** mot affärsregler (t.ex. beloppet måste vara > 0) innan du sparar.

---

## Slutsats

Vi har gått igenom **how to read receipt**‑bilder i C# med Aspose OCR, och sedan **extract amount using regex** för att på ett pålitligt sätt hitta totalraden. Genom att utnyttja språkmodellen `Receipt` får du räta‑upp‑ och brusreducerad text, och ett koncist reguljärt uttryck hanterar de flesta formateringsavvikelser. Kodsnutten ovan är klar att klistra in i vilket .NET‑konsol‑ eller tjänsteprojekt som helst, och de extra kantfallsförslagen ger dig en solid grund för produktionsanvändning.

Redo för nästa steg? Försök att utöka lösningen för att hämta enskilda radposter, beräkna skatt automatiskt, eller integrera med ett utgiftsspårnings‑API. Och om du stöter på ett kvitto som bryter mönstret, kom ihåg att **regex find total**‑metoden bara är en startpunkt—du kan alltid justera mönstret för att passa din specifika region.

Lycka till med kodningen, och må din kvittobearbetning vara snabb, exakt och helt automatiserad!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}