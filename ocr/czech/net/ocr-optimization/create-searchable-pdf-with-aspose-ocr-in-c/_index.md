---
category: general
date: 2026-04-01
description: Vytvořte prohledávatelný PDF v C# pomocí Aspose OCR – naučte se převádět
  naskenované PDF, přidávat OCR do PDF a povolit akceleraci GPU pro rychlé výsledky.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: cs
og_description: Rychle vytvořte prohledávatelný PDF v C# – převod naskenovaného PDF,
  přidání OCR do PDF a povolení GPU akcelerace pro vysoký výkon.
og_title: Vytvořte prohledávatelný PDF pomocí Aspose OCR v C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Vytvořte prohledávatelný PDF s Aspose OCR v C#
url: /cs/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF pomocí Aspose OCR v C#

Už jste někdy potřebovali **create searchable PDF** soubory z hromady naskenovaných dokumentů? Nejste jediní — mnoho týmů bojuje s převodem PDF obsahujících jen obrázky na textově prohledávatelné soubory. Dobrá zpráva? S Aspose OCR můžete **convert scanned PDF** na plně prohledávatelnou verzi během několika řádků C# kódu. V tomto průvodci projdeme celý proces, od přidání OCR do PDF až po volitelné **enable GPU acceleration** pro zvýšení rychlosti.

Ukážeme vám také, jak **convert pdf to searchable** formát, probereme, proč byste mohli chtít **add OCR to PDF**, a poskytneme praktické tipy pro zpracování velkých dávek. Na konci budete mít připravenou konzolovou aplikaci, která vytvoří prohledávatelné PDF, jež můžete vložit do libovolného systému správy dokumentů.

---

## Co budete potřebovat

Než se pustíme do práce, ujistěte se, že máte následující:

- **.NET 6.0** nebo novější (API funguje i s .NET Framework, ale .NET 6+ je ideální).
- **Aspose.OCR for .NET** NuGet balíček (`Install-Package Aspose.OCR`).
- Naskenovaný PDF soubor (pouze obrázek), který použijete jako vstup.
- Volitelně: stroj kompatibilní s GPU a nainstalovaným CUDA®, pokud chcete **enable GPU acceleration**.

A to je vše — žádné těžké OCR enginy, žádné externí služby. Vše běží lokálně.

---

## Vytvoření prohledávatelného PDF – Přehled krok za krokem

Níže je vysoká úroveň postupu, který budeme následovat:

1. **Initialize the OCR engine** — řekněte Aspose, jaký jazyk má hledat a zda má použít GPU.
2. **Point the engine at your scanned PDF** — definujte vstupní a výstupní cesty.
3. **Run the conversion** — Aspose provede těžkou práci a zapíše prohledávatelné PDF.
4. **Verify the result** — otevřete výstup a zkuste vyhledat text.

Každý krok je rozdělen do vlastní sekce, takže si můžete vybrat jen to, co potřebujete.

---

## Převod naskenovaného PDF na prohledávatelné PDF

Prvním krokem je vytvořit instanci `OcrEngine`. Tento objekt je „pracovní kůň“, který čte rastrové obrázky uvnitř vašeho PDF a extrahuje text.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Proč to funguje:** `ConvertToSearchablePdf` načte každou stránku, provede OCR na rastrovém obsahu a poté vloží neviditelnou textovou vrstvu za původní obrázek. Výsledek vypadá přesně jako původní naskenovaný dokument, ale nyní můžete text kopírovat, vybírat a vyhledávat.

---

## Přidání OCR do PDF pomocí Aspose

Pokud již máte PDF a jen chcete **add OCR to PDF** bez převodu celého souboru, můžete zavolat stejnou metodu — Aspose operaci interpretuje jako „přidání OCR“. Výše uvedený kód to už dělá, ale zde je rychlá varianta, která ukazuje, jak můžete zpracovávat více souborů ve smyčce:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Tip:** Používejte stejnou instanci `OcrEngine` pro celou dávku. Vytváření nové instance pokaždé přidává zbytečnou režii, zejména když **enable GPU acceleration**.

---

## Povolení GPU akcelerace pro rychlejší OCR

GPU akcelerace může u velkých dávek ušetřit minuty. Aspose OCR využívá pod kapotou NVIDIA CUDA, takže stačí přepnout boolean flag:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Kdy použít:** Pokud zpracováváte PDF větší než 10 MB nebo více než několik desítek souborů, GPU vám typicky přinese 2‑3× rychlejší zpracování. Na skromném notebooku bez CUDA‑kompatibilního GPU nechte `false` — knihovna automaticky přejde na CPU.

**Častý úskalí:** Zapomenutí nainstalovat správnou verzi CUDA driveru může způsobit výjimku za běhu (`CudaException`). Ujistěte se, že váš driver odpovídá verzi, kterou Aspose očekává (zkontrolujte poznámky k vydání na stránce NuGet).

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je samostatná konzolová aplikace, kterou můžete zkopírovat do nového .NET projektu. Obsahuje užitečné komentáře, ošetření chyb a závěrečný ověřovací krok, který vypíše počet zpracovaných stránek.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Otevřete `output.pdf` v libovolném prohlížeči PDF a zkuste napsat slovo, které se vyskytuje na naskenovaných obrázcích. Pokud je text zvýrazněn, úspěšně jste **create searchable pdf**.

---

## Časté problémy a profesionální tipy

| Problém | Proč se vyskytuje | Jak opravit / vyhnout se |
|---------|-------------------|--------------------------|
| **GPU není detekováno** | Chybějící nebo nesprávná verze CUDA driveru. | Nainstalujte verzi driveru uvedenou v poznámkách k vydání Aspose; jako záložní možnost nastavte `UseGpuAcceleration = false`. |
| **Špatný jazyk** | OCR výchozí na angličtinu; jiné jazyky vyžadují explicitní nastavení. | Před konverzí nastavte `Language = Language.Spanish` (nebo jakýkoli podporovaný enum). |
| **Velké PDF způsobují OutOfMemory** | Engine načítá celé stránky do paměti. | Zpracovávejte PDF po částech pomocí `ocrEngine.PageRange = new PageRange(1, 5)` pro každou dávku. |
| **Výstupní soubor je poškozený** | Cílová složka nemá práva zápisu. | Spusťte aplikaci s vyššími právy nebo zvolte zapisovatelnou cestu. |
| **Textová vrstva není prohledávatelná** | Prohlížeč kešuje starou verzi. | Obnovte (refresh) prohlížeč PDF nebo soubor znovu otevřete. |

**Profesionální tip:** Když pracujete s mixem naskenovaných a nativních PDF, zkontrolujte pro každou stránku flag `HasText` (`PdfPageInfo.HasText`) před spuštěním OCR. Ušetříte tak CPU cykly a vyhnete se dvojitému OCR na stránkách, které jsou již prohledávatelné.

---

## Programatické ověření výsledku (volitelné)

Pokud chcete automatizovat ověření, Aspose.PDF může extrahovat skrytý text:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Tento úryvek dokazuje, že skutečně **convert pdf to searchable** formát, ne jen překryjete obrázek.

---

## Příklad obrázku

![Create searchable PDF output example](https://example.com/images/searchable-pdf.png "Create searchable PDF using Aspose OCR")

*Alternativní text:* **create searchable pdf** příklad ukazující před (naskenovaný) a po (prohledávatelný) zobrazení.

---

## Další kroky a související témata

- **Batch processing:** Zabalte smyčku z části „Add OCR to PDF“ do Windows Service nebo Azure Function pro noční úlohy.
- **Pokročilá podpora jazyků:** Prozkoumejte `ocrEngine.Language = Language.Multilingual` pro dokumenty obsahující smíšené skripty.
- **Čištění po OCR:** Použijte `TextFragmentAbsorber` z Aspose.PDF k opravě častých OCR chyb (např. „0“ vs „O“).
- **Security

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}