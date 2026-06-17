---
category: general
date: 2026-03-18
description: Vytvořte prohledávatelný PDF pomocí Aspose OCR v C#. Převod obrázku na
  PDF, přidání OCR textové vrstvy a zápis PDF bajtů do souboru během několika jednoduchých
  kroků.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: cs
og_description: Rychle vytvořte prohledávatelný PDF pomocí Aspose OCR v C#. Naučte
  se, jak převést obrázek na PDF, přidat OCR textovou vrstvu a zapsat PDF data do
  souboru.
og_title: Vytvořte prohledávatelný PDF z obrázku – Rychlý průvodce OCR v C#
tags:
- OCR
- PDF
- C#
- Aspose
title: Vytvořte prohledávatelný PDF z obrázku s OCR – průvodce C#
url: /cs/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku s OCR – C# průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného obrázku? S Aspose OCR to můžete udělat během několika řádků, bez nutnosti těžkých knihoven. V tomto tutoriálu **převedeme obrázek na PDF**, přidáme **vrstvu OCR textu** a nakonec **zapíšeme PDF bajty do souboru**, takže získáte standardem vyhovující dokument PDF/A‑2b, který uživatelé skutečně mohou prohledávat.

Pokud se ptáte, proč byste se měli obtěžovat s prohledávatelným PDF místo čistého souboru jen s obrázkem, zamyslete se nad uživatelským zážitkem: prohledávatelné PDF umožňuje lidem kopírovat, vybírat a indexovat text – skvělé pro archivy, právní dokumenty nebo jakýkoli pracovní postup, který později potřebuje extrahovat text. Pojďme na to.

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje také na .NET Framework 4.7+)
- NuGet balíček Aspose.OCR (`Aspose.OCR` verze 23.10 nebo novější)
- Rasterový obrázek (`.png`, `.jpg`, atd.), který chcete převést na prohledávatelné PDF
- Základní znalost C# – nic složitého, jen základy

To je vše. Žádné externí nástroje, žádné další konvertory. Veškeré těžké zpracování provádí engine Aspose OCR.

## Vytvoření prohledávatelného PDF – přehled

Než se ponoříme do kódu, shrňme proces:

1. **Instantiate** OCR engine – tento objekt umí číst text z obrázků.  
2. **Load** zdrojový obrázek – předáme engine `ImageStream`.  
3. **Configure** možnosti uložení PDF/A‑2b – řekne Aspose, aby vložil rozpoznaný text jako skrytou vrstvu.  
4. **Run** OCR a **capture** výsledné PDF bajty.  
5. **Write** tyto bajty na disk, čímž vznikne finální prohledávatelné PDF.

Každý z těchto kroků odpovídá přímo jedné nebo dvěma řádkům C#, takže celý pracovní postup působí jako malý skript, nikoli jako rozsáhlý projekt.

## Krok 1: Převod obrázku na PDF – načtení obrázku

Nejprve musíme OCR engine poskytnout něco, co může číst. Pomocník `ImageStream.FromFile` načte soubor do proudu, který Aspose může zpracovat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Tip:** Udržujte rozlišení obrázku na 300 dpi nebo vyšší; přesnost OCR dramaticky klesá u nízkého rozlišení.

## Krok 2: Rozpoznání textu z obrázku a přidání OCR textové vrstvy

Nyní vytvoříme OCR engine a řekneme mu, aby rozpoznal text. Magie nastane, když spojíme výsledek rozpoznání s `PdfSaveOptions`, kde je `IncludeTextLayer = true`. Toto nastavení nutí Aspose vložit extrahované znaky jako neviditelnou textovou vrstvu, což dělá PDF prohledávatelným.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Proč PDF/A‑2b? Jedná se o archivní formát podle ISO, který zaručuje dlouhodobou archivaci a, co je pro nás důležité, nutí PDF obsahovat prohledávatelnou textovou vrstvu. Pokud archivní shoda není potřeba, můžete `PdfCompliance` úplně vynechat, ale jeho zachování vás nic nestojí.

## Krok 3: Zapsání PDF bajtů do souboru – uložení výsledku

S připraveným engine a nastavenými možnostmi spustíme rozpoznání a okamžitě požádáme Aspose, aby nám poskytl PDF jako `byte[]`. Pak tyto bajty zapíšeme na disk pomocí `File.WriteAllBytes`. Jednoduché, ale výkonné.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Řádek `Console.WriteLine` je volitelný, ale poskytuje okamžitou zpětnou vazbu při spuštění programu z terminálu.

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní, připravený program. Zkopírujte jej do nového konzolového projektu, nahraďte `YOUR_DIRECTORY` skutečnou cestou a stiskněte **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Očekávaný výstup

- Soubor s názvem `output.pdf` se objeví ve složce, kterou jste zadali.  
- Otevřete jej v Adobe Acrobat Reader nebo jakémkoli PDF prohlížeči a zkuste vybrat text – pokud můžete kopírovat slova, úspěšně jste **vytvořili prohledávatelné PDF**.  
- Dokument také projde nástroji pro validaci PDF/A‑2b, protože jsme použili správný příznak shody.

## Časté otázky a okrajové případy

**Co když můj obrázek obsahuje více stránek?**  
Zabalte každou stránku do vlastního `ImageStream` a předávejte je postupně `OcrEngine`. Aspose automaticky spojí stránky do jednoho PDF.

**Mohu změnit jazyk OCR?**  
Určitě. Před voláním `Recognize` nastavte `ocrEngine.Language = Language.English;` (nebo jakýkoli podporovaný jazyk).

**Jak to vypadá s využitím paměti u obrovských souborů?**  
Pokud zpracováváte skeny v gigabajtech, zvažte streamování výsledku přímo do `FileStream` místo držení celého `byte[]` v paměti:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Potřebuji licenci?**  
Aspose nabízí bezplatnou zkušební verzi bez vodoznaku. Pro produkční použití zakupte licenci, která odstraní evaluační banner a odemkne všechny funkce.

## Tipy pro lepší přesnost OCR

- **Předzpracujte** obrázek: odstraňte sklon, šum a zvýšte kontrast.  
- **Používejte bezztrátové formáty** jako PNG; artefakty komprese JPEG mohou engine zmást.  
- **Vyhněte se barevným pozadím**; čisté bílé pozadí poskytuje nejlepší výsledky.

## Další kroky

Teď, když můžete **vytvořit prohledávatelné PDF**, můžete chtít:

- **Dávkové zpracování** složky obrázků pomocí `Directory.GetFiles`.  
- **Extrahovat skrytý text** později pomocí API `PdfDocument` pro indexaci.  
- **Kombinovat OCR s digitálními podpisy** pro vytvoření archivů odolných proti manipulaci.

Všechny tyto možnosti staví na stejném základním vzoru, který jsme probírali: načíst, rozpoznat, nakonfigurovat, uložit.

---

*Připraveni převést své naskenované archivy na prohledávatelná PDF? Vezměte kód, nasměrujte jej na své obrázky a nechte Aspose udělat těžkou práci. Šťastné programování!*

![Příklad vytvoření prohledávatelného PDF](/images/create-searchable-pdf.png "Ilustrace prohledávatelného PDF vygenerovaného z obrázku")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}