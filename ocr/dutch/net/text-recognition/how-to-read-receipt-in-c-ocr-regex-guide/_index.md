---
category: general
date: 2026-02-13
description: Hoe een bon snel te lezen met Aspose OCR en het bedrag te extraheren
  met regex. Leer stap‑voor‑stap het verwerken van een bon met OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: nl
og_description: Hoe een bon te lezen in C# met Aspose OCR en regex. Deze gids laat
  zien hoe je een bon verwerkt met OCR en het totaalbedrag extraheert.
og_title: Hoe een bon te lezen in C# – Complete OCR- en regex-tutorial
tags:
- OCR
- C#
- Regex
- Aspose
title: Hoe een ontvangstbewijs te lezen in C# – OCR + Regex-gids
url: /nl/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een bon te lezen in C# – OCR + Regex gids

Heb je je ooit afgevraagd **hoe je bon kunt lezen** afbeeldingen zonder elke regel handmatig te typen? In veel kleine‑ondernemingsapps moet je het totaalbedrag uit een foto van een bon halen, en dit handmatig doen ondermijnt het doel van automatisering. Het goede nieuws? Met Aspose OCR kun je de engine het zware werk laten doen, waarna een eenvoudige reguliere expressie het totaal vindt. In deze tutorial lopen we door **bon verwerken met OCR**, halen we het bedrag op met regex, en eindigen we met een kant‑klaar totaalbedrag.

Je ziet een volledig, uitvoerbaar voorbeeld, ontdekt waarom het bon‑taalmodel belangrijk is, en krijgt tips voor het omgaan met randgevallen zoals verschillende valutasymbolen of ontbrekende “Total”‑labels. Er zijn geen externe documenten nodig—alles wat je nodig hebt staat hier.

## Wat je zult leren

- Hoe Aspose OCR in te stellen voor bon‑specifieke herkenning (het `Receipt` taalmodel corrigeert automatisch scheefstand en ruis in de afbeelding).  
- Hoe een reguliere expressie toe te passen die **bedrag extraheren met regex** patronen gebruikt die werken voor de meeste Amerikaanse bonnen.  
- Hoe om te gaan met veelvoorkomende variaties zoals “TOTAL”, “Total:”, of “Grand Total – $12.34”.  
- Hoe het resultaat veilig uit te voeren en wat te doen wanneer het patroon niet wordt gevonden.  

**Prerequisites**: .NET 6+ (of .NET Framework 4.7+), een geldige Aspose OCR‑licentie of proefversie, en een afbeelding van een bon die lokaal is opgeslagen. Dat is alles—geen extra NuGet‑pakketten naast Aspose.OCR.

---

## Stap 1 – Installeer Aspose OCR en bereid het project voor

### Waarom dit belangrijk is

Aspose OCR biedt een speciaal **bon verwerken met OCR** model dat weet hoe een gekreukeld papier recht te maken en achtergrondruis te negeren. Het gebruik van het generieke tekstmodel zou meer fouten opleveren, vooral bij scans met lage resolutie.

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

> **Pro tip:** Houd het licentiebestand buiten je source‑control map om per ongeluk committen te voorkomen.

---

## Stap 2 – Configureer de OCR‑engine voor bonherkenning

### Waarom dit belangrijk is

Het `Receipt` taalmodel bevat ingebouwde scheefstand‑ en ruiscorrectie, wat de nauwkeurigheid drastisch verbetert bij echte bonnen die vaak gevouwen of gekreukt zijn.

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

## Stap 3 – Herken tekst uit de bonafbeelding

### Waarom dit belangrijk is

Je hebt de ruwe tekst nodig voordat je een regex kunt toepassen. De `RecognizeImage`‑methode retourneert een `OcrResult` met de volledige string, vertrouwensscores en meer als je die later nodig hebt.

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

**Verwachte OCR‑output (voorbeeld)**  
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

## Stap 4 – Bouw een regex om **Bedrag extraheren met regex**

### Waarom dit belangrijk is

Bonnen komen in veel formaten, maar het woord “Total” (of een nabije variant) gevolgd door een bedrag in dollars is een betrouwbare anker. Het patroon hieronder staat optionele spaties, dubbele punten, koppeltekens en een optioneel `$`‑teken toe.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Uitleg van het patroon**

| Deel | Betekenis |
|------|-----------|
| `Total` | Zoekt naar het woord “Total” (hoofdletter‑ongevoelig). |
| `\s*[:\-]?` | Staat elke witruimte toe, gevolgd door een optioneel dubbele punt of koppelteken. |
| `\s*\$?` | Optionele witruimte en optioneel dollarteken. |
| `(\d+(\.\d{2})?)` | Vangt één of meer cijfers, eventueel gevolgd door een decimaal en twee centen. |

---

## Stap 5 – Geef het geëxtraheerde totaal weer of verwerk ontbrekende gegevens

### Waarom dit belangrijk is

Zelfs de beste OCR kan een woord missen, vooral op vage bonnen. Een elegante fallback voorkomt crashes en geeft je een houvast voor aangepaste logica (bijv. de gebruiker laten bevestigen).

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

**Voorbeeld console‑output**

```
Total: $12.25
```

---

## Volledig werkend voorbeeld – Alle stappen in één bestand

Hieronder vind je een enkel, zelf‑voorzienend programma dat je kunt copy‑pasten in een console‑project. Het bevat commentaar, foutafhandeling en het optionele laden van de licentie.

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

**Het programma uitvoeren**

1. Maak een nieuw console‑project (`dotnet new console -n ReceiptReader`).  
2. Voeg het Aspose.OCR NuGet‑pakket toe (`dotnet add package Aspose.OCR`).  
3. Vervang `YOUR_DIRECTORY/receipt.jpg` door het daadwerkelijke pad naar een bonafbeelding.  
4. Build en voer uit (`dotnet run`).  

Je zou de OCR‑dump moeten zien, gevolgd door `Total: $xx.xx` als alles klopt.

---

## Randgevallen behandelen & Veelvoorkomende variaties

### 1. Verschillende valutasymbolen

Als je met euro’s (€) of ponden (£) werkt, breid je het patroon uit:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Ontbrekend “Total”‑label

Sommige bonnen tonen alleen “Grand Total”. Voeg een alternatie toe:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Meerdere totalen (bijv. “Subtotal” en “Total”)

Als de regex de eerste vondst retourneert, wil je misschien de **laatste** match gebruiken:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Low‑Resolution afbeeldingen

- Verhoog de DPI bij het scannen (`300 DPI` is een goed uitgangspunt).  
- Pre‑process de afbeelding met een eenvoudige blur‑reduce filter voordat je deze naar Aspose stuurt (buiten de scope van deze gids, maar zeker het overwegen waard).

---

## Pro‑tips voor real‑world projecten

- **Cache het OCR‑resultaat** als je meerdere velden moet extraheren (belasting, items, enz.) – je betaalt de OCR‑kost dan maar één keer.  
- **Log de ruwe OCR‑tekst** naar een database; dit wordt een waardevol audit‑spoor voor betwiste uitgaven.  
- Bij het bouwen van een web‑API, **voer OCR uit in een achtergrond‑worker**; het kan enkele honderden milliseconden duren, wat asynchroon prima is maar niet ideaal voor een synchrone request.  
- **Valideer het geëxtraheerde bedrag** tegen bedrijfsregels (bijv. bedrag moet > 0 zijn) voordat je het opslaat.

---

## Conclusie

We hebben behandeld **hoe je bonnen kunt lezen** in C# met Aspose OCR, en vervolgens **bedrag extraheren met regex** om betrouwbaar de totalelijn te vinden. Door gebruik te maken van het `Receipt` taalmodel krijg je scheefstand‑ en ruis‑gecorrigeerde tekst, en een beknopte reguliere expressie behandelt de meeste opmaak‑eigenaardigheden. Het volledige code‑fragment hierboven kan direct in elk .NET console‑ of service‑project worden geplaatst, en de extra randgevallen‑suggesties geven je een solide basis voor productiegebruik.

Klaar voor de volgende stap? Probeer de oplossing uit te breiden om individuele regelitems te halen, belasting automatisch te berekenen, of te integreren met een onkosten‑tracking API. En als je een bon tegenkomt die het patroon breekt, onthoud dan dat de **regex find total**‑aanpak slechts een startpunt is—je kunt het patroon altijd aanpassen aan jouw specifieke locale.

Happy coding, en moge je bonverwerking snel, nauwkeurig en volledig geautomatiseerd zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}