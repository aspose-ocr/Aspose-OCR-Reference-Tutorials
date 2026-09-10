---
category: general
date: 2026-09-10
description: Jak použít OCR v C# k extrahování cyrilického textu, předzpracování obrázků
  a převodu do PDF nebo HTML souborů v jednom spustitelném příkladu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: cs
lastmod: 2026-09-10
og_description: Jak použít OCR v C# k extrakci cyrilického textu, předzpracování obrázků
  a exportu výsledků jako PDF nebo HTML. Postupujte podle tohoto krok‑za‑krokem průvodce.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Jak používat OCR v C# – extrahovat cyrilický text a převádět obrázky
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Jak použít OCR v C# k extrakci cyrilického textu
url: /cs/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít OCR v C# k extrahování cyrilického textu

Pokud potřebujete **how to use OCR** v C# pro extrahování cyrilického textu ze skenovaných dokumentů, tento průvodce vám ukáže kompletní, připravené řešení. Také se naučíte, jak **preprocess image for OCR**, a jak **convert image to PDF** nebo **convert image to HTML**, jakmile je text rozpoznán.

Projekty digitalizace dokumentů často narazí na dva problémy: skeny nízké kvality a potřebu ukládat výsledky v několika formátech. Tento tutoriál řeší oba problémy pomocí knihovny Aspose.OCR, která automaticky stahuje chybějící jazykové balíčky, nabízí vestavěné pomocníky pro zpracování obrazu a může exportovat výsledek OCR do PDF nebo HTML jedním voláním.

## Požadavky

* .NET 6.0 SDK nebo novější (kód také funguje s .NET Framework 4.7+).
* Visual Studio 2022 nebo jakýkoli editor, který podporuje C# projekty.
* Balíček **Aspose.OCR** NuGet. Nainstalujte jej pomocí:

```bash
dotnet add package Aspose.OCR
```

* Soubor obrázku, který obsahuje cyrilické znaky (např. `sample_cyrillic.jpg`).  
  Umístěte soubor do složky, na kterou můžete odkazovat jako `YOUR_DIRECTORY`.

Knihovna stáhne cyrilický jazykový balíček při prvním nastavení `ocrEngine.Language = Language.Cyrillic;`, takže není potřeba žádné ruční stahování.

## Krok 1 – Inicializace OCR enginu (how to use OCR)

Vytvoření instance `OcrEngine` připraví engine pro všechny následující operace.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Proč je to důležité:** Engine obsahuje konfiguraci jako jazyk, nastavení zpracování obrazu a výstupní možnosti. Jednorázová inicializace udržuje zbytek kódu čistý a thread‑safe.

## Krok 2 – Výběr cyrilického jazyka (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Proč je to důležité:** Přesnost OCR silně závisí na správném jazykovém modelu. Výběrem `Language.Cyrillic` engine použije tabulky četnosti znaků vhodné pro ruštinu, ukrajinštinu, bulharštinu atd.

## Krok 3 – Předzpracování obrazu pro OCR

Skeny nízké kvality obsahují zkosení, šmouhy nebo nerovnoměrné osvětlení. Vestavěný `ImageProcessor` může zlepšit míru rozpoznání pouhými dvěma voláními.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Proč je to důležité:** Předzpracování snižuje počet chybně rozpoznaných znaků a zvyšuje skóre důvěry. Zkosený text často vede k nesrozumitelnému výstupu; deskewing jej narovná. Despeckling odstraňuje drobné artefakty, které by OCR engine mohl mylně interpretovat jako písmena.

> **Tip:** Pokud jsou vaše zdrojové obrázky již čisté, můžete tato volání přeskočit. Pro silně poškozené skeny zvažte další kroky jako `Binarize()` nebo `ContrastStretch()`.

## Krok 4 – Provedení OCR na vstupním obrázku

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Proč je to důležité:** `Process` spustí rozpoznávací pipeline na dodaném bitmapu. Vrací `void`; rozpoznaný text je dostupný přes vlastnost `Text`.

## Krok 5 – Získání rozpoznaného textu a uložení do souboru

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Proč je to důležité:** Uložení surového textu umožňuje následné zpracování, jako je vyhledávání, indexování nebo předání do překladových služeb.

## Krok 6 – Export výsledku OCR do dalších formátů (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Proč je to důležité:** Konverze výsledku OCR do PDF nebo HTML vám umožní zachovat vizuální kontext původního obrázku a zároveň poskytnout prohledávatelný text. To je zvláště cenné pro právní nebo archivní workflow.

### Očekávaný výstup

Spuštěním programu s čistým cyrilickým skenem vzniknou tři soubory:

* `result.txt` – prostý Unicode text, např. `Пример текста на кириллице`.
* `result.pdf` – PDF obsahující obrázek s neviditelnou textovou vrstvou pro vyhledávání.
* `result.html` – HTML stránka zobrazující obrázek a vybratelný text.

Otevřete kterýkoli ze souborů a ověřte, že cyrilické znaky byly správně extrahovány.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Co když selže stažení jazykového balíčku?** | Ujistěte se, že má počítač přístup k internetu. Můžete také předem stáhnout balíček z webu Aspose a umístit jej do složky `bin`. |
| **Mohu rozpoznat jiné abecedy ve stejném běhu?** | Ano. Před voláním `Process` zavolejte `ocrEngine.Language = Language.English;` (nebo jakýkoli podporovaný enum). Možná budete muset spustit `Process` samostatně pro každý jazyk, pokud obrázek kombinuje různé skripty. |
| **Můj obrázek je multi‑page TIFF – funguje to?** | `OcrEngine` zpracovává jeden bitmap najednou. Načtěte každou stránku do `Bitmap` a volajte `Process` v cyklu, přičemž výsledky spojíte. |
| **Jak zvýšit výkon při velkých dávkách?** | Znovu použijte jedinou instanci `OcrEngine` a nastavte `ocrEngine.OptimizeMemory = true;`. Také zvažte paralelní zpracování s oddělenými instancemi enginu pro každý vlákno. |

## Závěr

Nyní víte **how to use OCR** v C# k **extract Cyrillic text**, **preprocess image for OCR** a **convert image to PDF** nebo **convert image to HTML** v několika stručných krocích. Kompletní příklad demonstruje produkční‑

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak použít AspOCR: Filtry pro předzpracování obrázku OCR pro .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Jak extrahovat OCR text v C# – Kompletní krok‑za‑krokem průvodce](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Jak použít Aspose OCR pro JSON výsledek v rozpoznávání obrazu](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}