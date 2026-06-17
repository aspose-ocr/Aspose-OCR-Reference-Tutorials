---
category: general
date: 2026-03-17
description: Rychle vytvořte prohledávatelný PDF převodem naskenovaného PDF pomocí
  OCR. Naučte se, jak spustit OCR, extrahovat text z PDF a další.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: cs
og_description: Vytvořte prohledávatelný PDF ze skenovaných dokumentů. Tento průvodce
  ukazuje, jak převést skenovaný PDF, spustit OCR a extrahovat text pomocí C#.
og_title: Vytvořte prohledávatelný PDF – kompletní C# OCR tutoriál
tags:
- OCR
- PDF
- C#
- .NET
title: Vytvořte prohledávatelný PDF ze skenovaných souborů – krok za krokem C# průvodce
url: /cs/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF – Kompletní C# tutoriál

Už jste někdy potřebovali **vytvořit prohledávatelný PDF** z hromady naskenovaných stránek? Možná digitalizujete staré smlouvy, nebo jen chcete, aby vaše PDF byla prohledávatelná ve Windows Průzkumníku. Každopádně se pravděpodobně ptáte, jak **převést naskenovaný PDF** na něco, co můžete skutečně prohledávat.  

Dobrá zpráva? S několika řádky C# a OCR enginem můžete proměnit libovolný PDF založený na obrázcích na plně prohledávatelný PDF – bez externích služeb. V tomto tutoriálu projdeme celý proces, od instalace knihovny po extrakci textu, a vysvětlíme „proč“ za každým krokem, abyste opravdu pochopili, co se děje pod kapotou.

> **Rychlá odpověď:** jen nastavte `PdfConversionMode = PdfConversionMode.SearchablePdf`, načtěte naskenovaný soubor, zavolejte `Recognize()` a výsledek uložte.  

Níže najdete vše, co potřebujete k tomu, aby to fungovalo ještě dnes.

---

## Co budete potřebovat

| Předpoklad | Proč je důležitý |
|------------|-------------------|
| .NET 6 nebo novější (nebo .NET Framework 4.7+) | OCR SDK, které použijeme, cílí na tyto runtimey. |
| Visual Studio 2022 (nebo jakékoli C# IDE) | Usnadňuje ladění a správu NuGet balíčků. |
| NuGet‑kompatibilní OCR knihovna (např. **Aspose.OCR** nebo **Tesseract.NET**) | Poskytuje třídu `OcrEngine` ukázanou v kódu. |
| Naskenovaný PDF soubor pro testování | Ten převedeme na prohledávatelný PDF. |

Pokud už máte projekt, stačí přidat OCR balíček přes Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

*(Nahraďte `Aspose.OCR` knihovnou dle vašeho výběru; API, které demonstrujeme, je poměrně obecné.)*

---

## Implementace krok za krokem

Níže u každého kroku najdete přesný C# kód, který můžete zkopírovat‑vložit, plus stručné vysvětlení **proč** daný řádek existuje.

### Krok 1: Inicializace OCR enginu  

Vytvoření enginu je první věc, kterou uděláte, protože drží veškerou konfiguraci a stav pro běh rozpoznávání.

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Pro tip:** Opakované používání jedné instance `OcrEngine` pro více souborů snižuje zatížení paměti, zejména při zpracování velkých dávek.

### Krok 2: Nastavení enginu pro prohledávatelný PDF  

Engine může výstupně generovat čistý text, obrázky nebo prohledávatelný PDF. Nastavení správného režimu říká knihovně, aby do původních obrázků stránek vložila neviditelnou textovou vrstvu.

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*Proč?* Bez tohoto příznaku by OCR běh vrátil jen `string` rozpoznaného textu, což není užitečné, pokud stále potřebujete původní rozložení stránky.

### Krok 3: Načtení naskenovaného dokumentu  

Většina OCR SDK přijímá `Image` nebo `ImageStream`. Zde používáme pomocnou funkci, která načte PDF soubor a každou stránku zachází jako obrázek.

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

> **Edge case:** Pokud vaše PDF obsahuje smíšené rastrové a vektorové stránky, některé enginy mohou vektorové stránky přeskočit. V takovém případě předem převěšte PDF na obrázky (např. pomocí Ghostscript) před předáním OCR enginu.

### Krok 4: Spuštění OCR rozpoznání  

Volání `Recognize()` provádí těžkou práci – detekci textu, jazykové modelování a generování PDF probíhá na pozadí.

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

Pokud potřebujete **extrahovat text z PDF** také, můžete jej získat z `ocrResult.Text`:

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### Krok 5: Uložení prohledávatelného PDF  

Nakonec zapíšete výstup na disk. Vlastnost `PdfDocument` obsahuje plně vytvořený PDF s neviditelným textovým překryvem.

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

Když otevřete `searchable.pdf` v Adobe Readeru nebo Edge, budete moci zadat slovo do vyhledávacího pole a okamžitě skočit na odpovídající místo – stejně jako u nativního PDF.

---

## Ověření výsledku

1. Otevřete vygenerovaný soubor v libovolném PDF prohlížeči.  
2. Stiskněte **Ctrl + F** a zadejte slovo, o kterém víte, že se v naskenovaných stránkách vyskytuje.  
3. Pokud prohlížeč zvýrazní termín, úspěšně jste **vytvořili prohledávatelný PDF**.

Pokud se nic nenajde, zkontrolujte, že zdrojové PDF skutečně obsahuje čitelný text (některé skeny jsou tak nízkého rozlišení, že OCR nic nepozná). Zvýšení DPI před OCR (např. `ocrEngine.Config.Dpi = 300`) často pomůže.

---

## Časté problémy a jak je opravit

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Prázdný prohledávatelný PDF | `PdfConversionMode` zůstalo v defaultu (pouze obrázek) | Nastavte `PdfConversionMode = PdfConversionMode.SearchablePdf`. |
| Zkreslené znaky | Špatný jazykový model | `ocrEngine.Config.Language = Language.English;` (nebo příslušný jazyk). |
| Pomalejší zpracování velkých souborů | Engine se inicializuje pro každou stránku | Znovu použijte stejnou instanci `OcrEngine`, nebo povolte vícevláknové zpracování, pokud knihovna podporuje. |
| Po konverzi není žádný text prohledávatelný | Vstupní PDF je pouze vektorové (žádné rastrové obrázky) | Nejprve renderujte stránky PDF na obrázky (např. `PdfRenderer` z Aspose.PDF). |

---

## Bonus: Přímá extrakce textu z prohledávatelného PDF  

Někdy potřebujete surový text pro indexaci nebo analytiku. Protože `ocrResult` už poskytuje `Text`, můžete přeskočit otevření PDF znovu. Pokud však později máte jen PDF soubor, použijte extraktor textu z PDF:

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

Nyní máte **extrahovat text z PDF** bez opětovného spouštění OCR – užitečná zkratka při zpracování mnoha souborů.

---

## Kompletní funkční příklad (všechny kroky v jednom souboru)

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Pokud uvidíte stejný úryvek dvakrát, OCR proběhlo úspěšně a PDF nyní obsahuje prohledávatelnou textovou vrstvu.

---

## Další kroky a související témata

- **Dávkové zpracování:** Procházejte složku se skenovanými PDF a opakovaně používejte stejnou instanci `OcrEngine` pro zvýšení propustnosti.  
- **Detekce jazyka:** Pro vícejazyčné archivy dynamicky přepínejte `ocrEngine.Config.Language` na základě metadat souboru.  
- **Soulad s PDF/A:** Některá odvětví vyžadují archivní PDF; nastavte `PdfConversionMode = PdfConversionMode.SearchablePdfA`, pokud to vaše SDK podporuje.  
- **Ladění výkonu:** Experimentujte s `ocrEngine.Config.UseParallelProcessing = true` (pokud je k dispozici) pro zrychlení velkých úloh.

Všechny tyto body staví na základním konceptu **jak spustit OCR** efektivně a **vytvořit prohledávatelný PDF** soubor, který je okamžitě indexovatelný.

---

## Závěr

Nyní máte kompletní, připravený recept na převod libovolného skenovaného dokumentu na **vytvoření prohledávatelného PDF** mistrovské dílo. Konfigurací OCR enginu, načtením zdroje, spuštěním rozpoznání a uložením výsledku jste pokryli celý pipeline – od surového obrázku po prohledávatelný, textově extrahovatelný PDF.  

Vyzkoušejte to na svých souborech, pohrávejte si s DPI nebo nastavením jazyka a uvidíte, jak se vám to podaří.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}