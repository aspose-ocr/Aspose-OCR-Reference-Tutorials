---
category: general
date: 2026-05-28
description: Vytvořte prohledávatelný PDF pomocí Aspose OCR v C#. Naučte se, jak spustit
  OCR na PDF, rozpoznat text v PDF a převést OCR naskenovaný PDF do prohledávatelného
  PDF.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: cs
og_description: Vytvořte prohledávatelný PDF pomocí Aspose OCR v C#. Postupujte podle
  tohoto krok‑za‑krokem průvodce, abyste spustili OCR na PDF, rozpoznali text v PDF
  a zpracovali OCR naskenované PDF soubory.
og_title: Vytvořte prohledávatelný PDF s Aspose OCR – Spusťte OCR na PDF
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
title: Vytvořte prohledávatelný PDF pomocí Aspose OCR – Proveďte OCR na PDF
url: /cs/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF pomocí Aspose OCR – Spuštění OCR na PDF

Už jste někdy potřebovali **create searchable PDF** soubory ze zásobníku naskenovaných dokumentů? Nejste v tom sami. V mnoha kancelářských pracovních postupech je jedinou překážkou mezi vámi a plně prohledávatelným archivem několik řádků kódu, které spustí OCR na PDF stránkách.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který vám ukáže přesně, jak **create searchable PDF** soubory pomocí knihovny Aspose OCR pro .NET. Na konci budete vědět, jak *run OCR on PDF*, *recognize text PDF* soubory a jak převést *OCR scanned PDF* na prohledávatelnou verzi bez jakýchkoli služeb třetích stran.

> **Prerequisites** – Aktuální .NET SDK (doporučeno 6.0+), platná licence Aspose.OCR pro .NET (nebo dočasný evaluační klíč) a PDF, které chcete zpracovat.

![Create searchable PDF diagram](alt="Diagram znázorňující workflow vytvoření prohledávatelného PDF pomocí Aspose OCR")  

---

## Co tento průvodce pokrývá

- Nastavení knihovny Aspose OCR v C# projektu.  
- Načtení zdrojového PDF (libovolný počet stránek).  
- Konfigurace enginu pro výstup **searchable PDF**.  
- Spuštění OCR procesu a uložení výsledku.  
- Tipy pro práci s vícestránkovými dokumenty, výběr jazyka a běžné úskalí.  

Pokud budete postupovat podle každého kroku, získáte soubor, který můžete otevřít v Adobe Reader, stisknout **Ctrl + F** a okamžitě vyhledat jakékoli slovo, které se objevilo v původním skenu.

---

## Krok 1: Instalace Aspose OCR pro .NET

Než napíšete jakýkoli kód, přidejte NuGet balíček do svého projektu:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Použijte příznak `--version` pro uzamčení na nejnovější stabilní verzi (např. `Aspose.OCR 23.10`). Tím zajistíte kompatibilitu s .NET 6 a novějšími.

---

## Krok 2: Vytvoření instance OCR Engine

Srdcem procesu je `OcrEngine`. Představte si ho jako mozek, který čte obrázky a vydává text. Inicializace je jednoduchá:

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

Objekt `OcrEngine` bude obsahovat jak vstupní stream obrázku, tak konfiguraci, která říká Aspose, jaký výstup chcete.

---

## Krok 3: Načtení zdrojového PDF (Run OCR on PDF)

Aspose OCR může přímo načíst PDF; interně extrahuje každou stránku jako obrázek. Nahraďte zástupnou cestu umístěním vašeho naskenovaného dokumentu:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Proč to funguje:** Metoda `ImageStream.FromFile` automaticky detekuje formát PDF a připraví rastrovou reprezentaci pro OCR. Žádný další konverzní krok není potřeba.

---

## Krok 4: Konfigurace výstupního formátu a jazyka

Zde říkáme Aspose, co chceme zpět. Nastavením `OutputFormat` na `SearchablePdf` instruujeme engine, aby vložil rozpoznaný text za původní obrázky stránek, čímž vznikne **searchable PDF**. Můžete také vybrat jazyk pro zlepšení přesnosti – výchozí je angličtina, ale můžete přepnout na francouzštinu, němčinu atd.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Pokud potřebujete zpracovat bilingvní dokument, můžete kombinovat jazyky pomocí příznaků enumu `Language`.

---

## Krok 5: Spuštění OCR procesu – Recognize Text PDF

Nyní se děje těžká práce. Metoda `Recognize` prohledá každou stránku, extrahuje glyfy a vytvoří interní PDF stream, který obsahuje jak původní obrázek, tak neviditelnou textovou vrstvu. Toto je krok, kde *recognize text PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Často kladená otázka:** *Co když PDF má 200 stránek?*  
> Engine zpracovává stránky sekvenčně a streamuje výsledky, takže spotřeba paměti zůstává skromná. Pro extrémně velké soubory však můžete zvýšit nastavení `MemoryLimit` v `ocrEngine.Configuration`.

---

## Krok 6: Uložení prohledávatelného PDF

Nakonec zapíšeme výstup na disk. Metoda `Save` uloží interní stream do nového souboru, který můžete otevřít libovolným PDF prohlížečem.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Spusťte program (`dotnet run`) a sledujte, jak konzole potvrdí vytvoření souboru. Otevřete `handbook_searchable.pdf` a zkuste vyhledat slovo, o kterém víte, že se v původním skenu vyskytuje – měly by se okamžitě zobrazit shody.

---

## Řešení okrajových případů a pokročilých scénářů

### Více jazyků (OCR Scanned PDF)

Pokud váš zdrojový PDF obsahuje jak anglický, tak španělský text, kombinujte jazyky:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR přepíná slovníky za běhu, což zvyšuje přesnost u dokumentů s mixovanými jazyky.

### PDF chráněná heslem

Při práci se zabezpečenými PDF před zavoláním `Recognize` poskytněte heslo:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Pokud je heslo špatné, `Recognize` vyhodí `InvalidPasswordException`; zachycením výjimky můžete uživatele požádat o správné heslo.

### Řízení kvality obrázku

Vyšší DPI přináší lepší OCR výsledky, ale spotřebovává více paměti. Upravte DPI, pokud zaznamenáte zkreslené znaky:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Licence vs. evaluační režim

V evaluačním režimu se na každou stránku přidá vodoznak. Pro jeho odstranění aplikujte licenci před jakýmkoli voláním OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Pro tipy pro produkční použití

- **Dávkové zpracování:** Zabalte hlavní logiku do `foreach` smyčky, která iteruje přes seznam PDF souborů. Po každém souboru uvolněte `OcrEngine`, aby se uvolnily nativní zdroje.
- **Logování:** Použijte `ocrEngine.Configuration.Logger` k zachycení podrobných OCR statistik (např. rozpoznané znaky za sekundu). To je neocenitelné při řešení nízké přesnosti.
- **Ladění výkonu:** Pro multi‑core servery vytvořte samostatné instance `OcrEngine` pro každý vláken; knihovna je thread‑safe, pokud je každá instance izolovaná.
- **Zpracování chyb:** Vždy obalte `Recognize` a `Save` bloky `try/catch`. Typické výjimky zahrnují `FileNotFoundException`, `OutOfMemoryException` a `UnsupportedFormatException`.

---

## Kompletní funkční příklad (připravený ke kopírování)

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

**Očekávaný výstup** (konzole):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Otevřete výsledný soubor, stiskněte **Ctrl + F** a budete moci najít jakékoli slovo, které se objevilo v původních naskenovaných stránkách. To je kouzlo převodu *OCR scanned PDF* na **searchable PDF**.

---

## Závěr

Právě jsme ukázali, jak **create searchable PDF** soubory s Aspose OCR pro .NET, pokrývající vše od instalace balíčku po práci s vícejazyčnými a heslem chráněnými PDF. Dodržením těchto kroků můžete spolehlivě *run OCR on PDF* dokumenty, *recognize text PDF* obsah a převést jakýkoli *OCR scanned PDF* na plně prohledávatelný zdroj.

### Co dál?

- Prozkoumejte dále **aspose ocr pdf** API: extrahujte čistý text, exportujte do DOCX nebo generujte prohledávatelné PDF ve velkém množství.  
- Kombinujte výstup prohledávatelného PDF s Aspose.PDF pro přidání záložek nebo vodoznaků.  
- Experimentujte s různými nastaveními DPI nebo vlastními OCR slovníky pro specifické fonty.

Neváhejte upravit ukázku, integrovat ji do vašeho pipeline pro správu dokumentů nebo klást otázky v komentářích. Šťastné kódování a užívejte si přeměnu nečitelné skeny na prohledávatelný poklad!

## Související tutoriály

- [Jak provést OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}