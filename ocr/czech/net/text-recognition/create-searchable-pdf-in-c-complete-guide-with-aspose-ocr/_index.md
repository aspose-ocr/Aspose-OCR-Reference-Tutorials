---
category: general
date: 2026-06-28
description: Vytvořte prohledávatelný PDF z obrázků pomocí C#. Naučte se, jak převést
  obrázek na PDF, extrahovat text z obrázku a rozpoznávat více jazyků v jednom procesu.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- how to recognize multiple languages
- how to generate searchable pdf
language: cs
og_description: Vytvořte prohledávatelný PDF pomocí C#. Tento průvodce ukazuje, jak
  převést obrázek na PDF, extrahovat text z obrázku a programově rozpoznávat více
  jazyků.
og_title: Vytvořte prohledávatelný PDF v C# – krok za krokem tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  headline: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  type: TechArticle
- description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  name: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code compiles with .NET Core as well). - An
      Aspose.OCR license (you can start with a free trial; the API works without a
      license but adds a watermark). - A sample image that contains English, Arabic,
      and Korean text (or any languages you need). - Visual Studio 2022 or yo'
  - name: What If a Language Isn't Recognized?
    text: If you add a language that the engine doesn’t have a model for, it will
      simply ignore it and fall back to the others. To avoid surprises, double‑check
      the supported language list in the Aspose documentation.
  - name: Expected Output
    text: '``` Plain text: Hello World! مرحبا بالعالم! 안녕하세요 세계! Searchable PDF saved.
      ```'
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Vytvořte prohledávatelný PDF v C# – Kompletní průvodce s Aspose OCR
url: /cs/net/text-recognition/create-searchable-pdf-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF v C# – Kompletní průvodce s Aspose OCR

Už jste se někdy zamýšleli, jak **vytvořit prohledávatelné PDF** přímo z obrázku, aniž byste opustili svůj C# projekt? Nejste v tom sami. Ať už digitalizujete vícejazyčné dokumenty nebo budujete aplikaci pro skenování účtenek, převod obrázku na PDF, který lze prohledávat, je revoluční schopnost.

V tomto tutoriálu projdeme přesně kroky, jak **vytvořit prohledávatelné PDF** pomocí Aspose.OCR, od načtení obrázku až po export plně prohledávatelného dokumentu. Navíc vám ukážeme, jak **převést obrázek na PDF**, **extrahovat text z obrázku** a **rozpoznat více jazyků** – vše v jedné asynchronní metodě.

## Co se naučíte

- Spustitelnou C# konzolovou aplikaci, která načte obrázek, provede OCR v režimu akcelerovaném GPU a zapíše prohledávatelné PDF.
- Proč má povolení GPU vliv na výkon.
- Techniky pro **extrahování textu z obrázku** pro další zpracování.
- Jasný vzor, **jak rozpoznat více jazyků** v jednom průchodu.
- Tipy, jak rozšířit kód pro podporu dalších formátů nebo vlastních nastavení OCR.

### Požadavky

- .NET 6.0 SDK nebo novější (kód se také kompiluje s .NET Core).
- Licence Aspose.OCR (můžete začít s bezplatnou zkušební verzí; API funguje i bez licence, ale přidá vodoznak).
- Ukázkový obrázek obsahující anglický, arabský a korejský text (nebo jakékoli jazyky, které potřebujete).
- Visual Studio 2022 nebo vaše oblíbené IDE.

Máte vše? Skvěle – pojďme na to.

---

## Krok 1: Nastavení projektu a instalace Aspose.OCR

Nejprve vytvořte nový konzolový projekt:

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
```

Poté přidejte NuGet balíček Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud plánujete spouštět OCR na stroji s GPU, nainstalujte také balíček `Aspose.OCR.Gpu`. Ten automaticky stáhne nativní CUDA knihovny.

## Krok 2: Vytvoření OCR enginu a povolení akcelerace GPU

Srdcem operace je `OcrEngine`. Povolení GPU může ušetřit sekundy při zpracování vysoce rozlišených obrázků.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// ...

// Step 2: Create an OCR engine and turn on GPU support
var ocrEngine = new OcrEngine();
ocrEngine.Settings.EnableGpu = true;   // ← speeds up large images dramatically
```

Proč povolit GPU? OCR je v podstatě masivní problém násobení matic; GPU zvládá tyto paralelní úlohy mnohem efektivněji než CPU. Pokud běžíte na serveru bez GPU, nechte `EnableGpu` nastaveno na `false` – engine se automaticky přepne na CPU.

## Krok 3: Asynchronní načtení obrázku

Asynchronní I/O udržuje UI responzivní a zabraňuje vyčerpání vláken v serverových scénářích. Pomocník `OcrImage.FromFileAsync` abstrahuje práci se streamy.

```csharp
using Aspose.OCR;

// ...

// Step 3: Load the image to be processed (async)
var imagePath = @"C:\Docs\multilingual_sample.jpg";
var image = await OcrImage.FromFileAsync(imagePath);
```

Pokud později potřebujete **převést obrázek na PDF**, mějte tuto instanci `OcrImage` po ruce; předáte ji přímo exportéru PDF.

## Krok 4: Rozpoznání textu ve více jazycích

Aspose.OCR umožňuje zadat čárkou oddělený seznam kódů jazyků. To je odpověď na **jak rozpoznat více jazyků** v jednom průchodu.

```csharp
using Aspose.OCR;

// ...

// Step 4: Run OCR with English, Arabic, and Korean support
var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
{
    Language = "en,ar,ko"   // ← multiple languages, order doesn’t matter
});
```

Vlastnost `ocrResult.Text` nyní obsahuje prostý textový výstup všeho, co Aspose dokázal dešifrovat. To je jádro **extrahování textu z obrázku**.

```csharp
Console.WriteLine("Plain text extracted:");
Console.WriteLine(ocrResult.Text);
```

### Co když jazyk není rozpoznán?

Pokud přidáte jazyk, pro který engine nemá model, jednoduše jej ignoruje a přepne se na ostatní. Pro předejití překvapení si dvakrát ověřte seznam podporovaných jazyků v dokumentaci Aspose.

## Krok 5: Přímý export prohledávatelného PDF

Místo ručního vytváření PDF a překrytí textu poskytuje Aspose.OCR jednorázovou metodu **jak generovat prohledávatelné PDF**. Metoda vloží OCR text jako neviditelnou vrstvu, čímž je PDF prohledávatelné a zároveň zachová původní obrázek.

```csharp
using Aspose.OCR.Output;

// ...

// Step 5: Export the recognized content as a searchable PDF
await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
{
    Language = "en,ar,ko",               // keep language consistency
    OutputPath = @"C:\Docs\sample_searchable.pdf"
});

Console.WriteLine("Searchable PDF saved at C:\\Docs\\sample_searchable.pdf");
```

Za scénou Aspose vytvoří PDF stránku, kde je původní bitmapa viditelným pozadím a přidá skrytou textovou vrstvu, která odpovídá souřadnicím obrázku. Když soubor otevřete v Adobe Reader a stisknete **Ctrl + F**, budete moci najít slova ve všech třech jazycích.

## Krok 6: Spojení všeho – kompletní asynchronní `Main`

Níže je kompletní, připravený program. Vložte jej do `Program.cs`, upravte cesty k souborům a stiskněte **F5**.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Output;

class AllInOne
{
    static async Task Main()
    {
        // Step 2: Create an OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.EnableGpu = true;

        // Step 3: Load the image to be processed (async)
        var image = await OcrImage.FromFileAsync(@"C:\Docs\multilingual_sample.jpg");

        // Step 4: Recognize text in the image using multiple languages
        var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
        {
            Language = "en,ar,ko"
        });

        Console.WriteLine("Plain text:");
        Console.WriteLine(ocrResult.Text);

        // Step 5: Export the recognized content as a searchable PDF
        await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
        {
            Language = "en,ar,ko",
            OutputPath = @"C:\Docs\sample_searchable.pdf"
        });

        Console.WriteLine("Searchable PDF saved.");
    }
}
```

### Očekávaný výstup

```
Plain text:
Hello World!
مرحبا بالعالم!
안녕하세요 세계!
Searchable PDF saved.
```

Když otevřete `sample_searchable.pdf` a vyhledáte „Hello“, „العالم“ nebo „세계“, engine najde odpovídající slova, i když jsou vykreslená jako součást obrázku.

## Krok 7: Časté problémy a jejich řešení

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| **GPU není detekováno** | Na stroji chybí CUDA ovladače nebo není nainstalován balíček `Aspose.OCR.Gpu`. | Nainstalujte NVIDIA ovladače, ověřte verzi CUDA, nebo nastavte `EnableGpu = false`. |
| **Chybí podpora jazyka** | Kód jazyka není v zabudovaném modelovém setu. | Stáhněte si doplňkový jazykový balíček z Aspose nebo omezte se na podporované kódy. |
| **PDF je prázdné** | Výstupní cesta je neplatná nebo proces nemá oprávnění k zápisu. | Použijte absolutní cestu s odpovídajícími oprávněními, např. `C:\Temp\output.pdf`. |
| **Zpomalení výkonu** | Velké obrázky (>5 MP) zatěžují paměť. | Před OCR zmenšete rozlišení obrázku nebo zvýšte limit paměti procesu. |

## Rozšíření příkladu

- **Dávkové zpracování:** Zabalte hlavní logiku do `foreach` smyčky, která iteruje přes složku s obrázky.
- **Vlastní nastavení OCR:** Upravit `ocrEngine.Settings.PageSegMode` pro jednosloupcové nebo více sloupcové rozvržení.
- **Vkládání metadat:** Použijte `PdfExportOptions` k vložení autora, názvu nebo data vytvoření do prohledávatelného PDF.

---

## Závěr

Nyní máte solidní, end‑to‑end recept na **vytvoření prohledávatelného PDF** přímo z obrázků pomocí C#. Dodržením výše uvedených kroků jste se naučili, jak **převést obrázek na PDF**, **extrahovat text z obrázku** a **rozpoznat více jazyků** – vše při zachování čistého a asynchronního kódu.

Odtud můžete experimentovat s různými jazykovými balíčky, přidat post‑processing OCR (např. kontrolu pravopisu) nebo integrovat tok do webového API, které na požádání poskytuje prohledávatelná PDF. Možnosti jsou neomezené a kód, který jste právě napsali, je robustní základ pro jakýkoli projekt automatizace dokumentů.

Máte otázky ohledně optimalizace výkonu nebo licencování? Zanechte komentář a pojďme konverzaci posunout dál. Šťastné programování!

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}