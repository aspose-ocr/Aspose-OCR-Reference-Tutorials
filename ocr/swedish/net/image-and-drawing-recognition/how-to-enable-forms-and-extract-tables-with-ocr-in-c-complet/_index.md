---
category: general
date: 2026-01-04
description: Lär dig hur du aktiverar formulär och extraherar tabeller från bilder
  med OCR i C#. Denna steg‑för‑steg‑handledning visar också hur du kör OCR på en bild
  och upptäcker tabeller med OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: sv
og_description: Steg‑för‑steg‑guide om hur du aktiverar formulär, extraherar tabeller,
  kör OCR på bild och upptäcker tabeller med OCR i C#.
og_title: Hur man aktiverar formulär och extraherar tabeller med OCR i C#
tags:
- OCR
- C#
- Computer Vision
title: Hur man aktiverar formulär och extraherar tabeller med OCR i C# – Komplett
  guide
url: /sv/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man aktiverar formulär och extraherar tabeller med OCR i C# – Komplett guide

Har du någonsin undrat **hur man aktiverar formulär** när du skannar fakturor, kvitton eller något strukturerat dokument? Du är inte ensam. I många verkliga projekt är den största friktionen att få OCR att förstå både formulärfält **och** tabeller utan en miljon rader av anpassad parsning.  

I den här handledningen går vi igenom en praktisk, end‑to‑end‑lösning som visar **hur man aktiverar formulär**, **hur man extraherar tabeller**, och till och med **hur man kör OCR‑bild**‑behandling i ett enda C#‑program. I slutet har du ett färdigt kodexempel som upptäcker tabeller i OCR‑stil, hämtar nyckel‑värde‑par och skriver ut dem i konsolen.

> **Förutsättningar** – .NET 6+ (eller .NET Framework 4.7+), en referens till det OCR‑SDK du använder (exemplet förutsätter en generisk `OcrEngine`‑klass), och en bildfil (`invoice_table.png`) som innehåller en tabell eller ett formulär. Inga andra externa bibliotek krävs.

![hur man aktiverar formulär med OCR C#](image.png)

## Vad den här handledningen täcker

- **Enable form recognition** så att fält som “Invoice Number” eller “Date” identifieras automatiskt.  
- **Extract tables** från skannade dokument, vilket ger dig rad-/kolumnantal och cellinnehåll.  
- **Run OCR image**‑behandling i ett enda anrop och hantera resultatet programatiskt.  
- Tips för **detect tables OCR**‑kantfall, såsom sammanslagna celler eller saknade kanter.  

Låt oss dyka ner.

## Steg 1: Ställ in OCR‑motorn – how to enable forms

Innan någon igenkänning kan ske behöver du en OCR‑motorns instans. De flesta SDK:er exponerar en enkel konstruktor; vi kommer också att påpeka var du kan justera konfigurationsalternativ senare.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Varför detta är viktigt:** Att instansiera motorn allokerar interna resurser (som språkmodeller). Om du hoppar över detta steg kommer det efterföljande `Recognize`‑anropet att kasta ett `NullReferenceException`.

## Steg 2: Aktivera strukturerad extraktion – how to extract tables & detect tables OCR

Nu aktiverar vi de två kärnfunktionerna: tabelligenkänning och formulärfältsextraktion. De flesta moderna OCR‑motorer exponerar booleska flaggor eller ett mer detaljerat `Config`‑objekt.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Proffstips:** Om du bara behöver en av funktionerna kan du inaktivera den andra för att förbättra prestandan med upp till 20 %.

## Steg 3: Kör OCR‑bild och hämta resultatet – run OCR image

Med motorn konfigurerad gör ett enda metodanrop det tunga arbetet. Det returnerade `OcrResult` innehåller samlingar för tabeller och formulärfält.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Förväntad konsolutmatning

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

De exakta siffrorna kommer att skilja sig beroende på din källbild, men du bör se en sammanfattningsrad för varje tabell följt av den första radens cellvärden, och sedan en lista med nyckel‑värde‑par för formulärfälten.

## Steg 4: Hantera kantfall vid detektering av tabeller OCR

Även med `EnableTableRecognition = true` kan OCR snubbla på:

| Problem | Varför det händer | Snabb lösning |
|---------|-------------------|---------------|
| **Merged cells** | Motorn behandlar det sammanslagna området som en enda cell. | Efterbearbeta rader: leta efter ovanligt breda celler och dela dem baserat på blanksteg. |
| **Missing borders** | Tabelllinjer är svaga eller brutna. | Öka bildkontrasten innan du skickar den till motorn (`ocrEngine.PreprocessImage`). |
| **Rotated tables** | Dokumentet skannades i en vinkel. | Använd `ocrEngine.Config.AutoRotate = true` (om tillgängligt). |

**Tips:** Validera alltid `table.Rows.Count` och `table.Columns.Count` innan du åtkommer index för att undvika `IndexOutOfRangeException`.

## Steg 5: Sätt ihop allt – ett komplett, körbart exempel

Nedan är hela programmet som du kan kopiera‑klistra in i ett nytt konsolprojekt. Det inkluderar `using`‑direktiven, motorinställningarna och den bearbetningslogik som visades tidigare.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Kör programmet (`dotnet run` eller `Ctrl+F5` i Visual Studio) så ser du konsolutmatningen som beskrivits tidigare.

## Vanliga frågor (FAQ)

**Q: Fungerar detta med PDF‑inmatning?**  
A: De flesta OCR‑SDK:er accepterar PDF‑filer genom att intern rasterisera varje sida. Anropa bara `ocrEngine.LoadPdf("file.pdf")` istället för `LoadImage`.

**Q: Vad händer om min bild innehåller både en tabell *och* en signatur?**  
A: Signaturen kommer att visas som ett separat bildområde. Du kan ignorera den genom att kontrollera `ocrResult.Images` för text med låg förtroendegrad.

**Q: Kan jag exportera tabellerna till CSV?**  
A: Absolut. Efter att ha itererat över `table.Rows`, skriv varje `cell.Text` till en `StringBuilder` separerad med kommatecken, och spara sedan strängen till en `.csv`‑fil.

## Slutsats

Du vet nu **how to enable forms**, **how to extract tables**, och de exakta stegen för att **run OCR image**‑behandling med C#. Exemplet demonstrerar hela arbetsflödet – från motor‑skapande, genom konfiguration, till resultat‑hantering – så att du kan kopiera det direkt in i dina egna projekt.  

Nästa steg, prova att byta ut exempelbilden mot en flersidig faktura‑PDF, experimentera med `ocrEngine.Config.AutoRotate`, eller skicka de extraherade data till en databas. Dessa tillägg kommer att fördjupa din behärskning av **detect tables OCR** och **use OCR C#** i produktionsscenarier.

Om du stöter på problem, lämna gärna en kommentar nedan. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}