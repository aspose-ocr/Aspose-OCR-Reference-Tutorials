---
category: general
date: 2026-02-13
description: Vytvořte vyhledávatelný PDF z obrázku pomocí Aspose.OCR. Naučte se převést
  obrázek na PDF, extrahovat text z obrázku, vložit písma do PDF a rozpoznat text
  z PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose.OCR. Tento návod
  ukazuje, jak převést obrázek na PDF, vložit písma a snadno extrahovat text z PNG.
og_title: Vytvořte prohledávatelný PDF z obrázku – krok za krokem C# tutoriál
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Vytvořte prohledávatelný PDF z obrázku – kompletní C# průvodce
url: /cs/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku – Kompletní C# průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného PNG, ale nevedeli jste, kde začít? Nejste v tom sami. V mnoha projektech – například digitalizace faktur nebo archivace starých příruček – je schopnost převést obrázek na PDF, které lze skutečně prohledávat, skutečným průlomem.  

V tomto tutoriálu projdeme přesně kroky k **převodu obrázku na PDF**, **extrakci textu z obrázku**, vložení potřebných fontů a nakonec získáme plně prohledávatelný PDF soubor. Žádné vágní odkazy, jen kompletní, spustitelný příklad, který můžete dnes zkopírovat a vložit do Visual Studia.

> **Co získáte:** C# konzolovou aplikaci, která načte `input.png`, spustí OCR, vloží fonty, zachová původní rastrový obrázek jako pozadí a zapíše `output.pdf`. Na konci pochopíte *proč* je každý řádek důležitý a jak jej upravit pro své vlastní scénáře.

---

## Požadavky

- .NET 6.0 SDK nebo novější (kód funguje také s .NET Framework 4.7+).  
- Aspose.OCR pro .NET – můžete jej získat z NuGet (`Install-Package Aspose.OCR`).  
- Ukázkový PNG obrázek (`input.png`) umístěný ve složce, kterou ovládáte.  
- Základní znalost C# konzolových projektů (pokud jste takový ještě nevytvořili, otevřete Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Tip:** Aspose nabízí bezplatnou zkušební licenci; stačí umístit soubor `.lic` vedle spustitelného souboru a knihovna bude fungovat bez vodoznaků.

---

## Krok 1: Nastavení OCR enginu – Rozpoznání textu z PNG

Prvním, co potřebujeme, je OCR engine, který dokáže skutečně přečíst znaky v PNG souboru. Aspose.OCR to dělá velmi jednoduše.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Proč je to důležité:**  
Nastavení `Language` říká enginu, jakou znakovou sadu má očekávat. Pokud to přeskočíte, engine použije výchozí generický režim, který může špatně interpretovat diakritické znaky nebo čísla. Pro vícejazyčné dokumenty můžete předat čárkou oddělený seznam, např. `OcrLanguage.English | OcrLanguage.French`.

---

## Krok 2: Načtení a rozpoznání obrázku – Extrakce textu z obrázku

Nyní, když je engine připravený, předáme mu PNG, který chceme zpracovat.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Co se děje pod kapotou?**  
`RecognizeImage` prohledá bitmapu, identifikuje textové bloky a uloží výsledek do `ocrEngine`. Později můžete přistupovat k `ocrEngine.Text`, pokud potřebujete jen surový řetězec, ale pro prohledávatelný PDF necháme převod provést přímo Aspose.

> **Hraniční případ:** Pokud je váš PNG obrovský (více než 10 MB), můžete narazit na nedostatek paměti. V takovém případě zvažte nejprve změnu velikosti obrázku nebo použijte `OcrEngine.RecognizeImage(Stream)` pro streamování dat.

---

## Krok 3: Konfigurace možností exportu PDF – Vložení fontů do PDF

Prohledávatelný PDF není užitečný, pokud nejsou fonty vloženy; dokument by vypadal poškozeně na počítačích, které nemají požadované typy písma. Aspose nám umožňuje toto nastavit pomocí jednoduchého objektu možností.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Proč vkládat fonty?**  
Když je `EmbedFonts` nastaveno na `true`, PDF nese data fontu uvnitř souboru. To zajišťuje, že jakýkoli prohlížeč – Chrome, Adobe Reader nebo mobilní aplikace – zobrazí text přesně tak, jak má být, i když cílový systém font nemá.

**Kdy nastavit `KeepOriginalImage` na `false`?**  
Pokud potřebujete jen extrahovaný text a chcete menší soubor, vypnutí této volby odstraní pozadí obrázku a vytvoří „čistý“ PDF pouze s textem.

---

## Krok 4: Export do prohledávatelného PDF – Převod obrázku na PDF

S výsledky OCR a připravenými PDF možnostmi je posledním krokem jednorázový příkaz, který zapíše prohledávatelný PDF na disk.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Co uvidíte:**  
Po otevření `output.pdf` v libovolném prohlížeči můžete vybrat text, kopírovat jej a dokonce spustit hledání (`Ctrl + F`) pro nalezení slov, která původně existovala jen jako pixely v PNG.

---

## Kompletní funkční příklad

Níže je celý program, který můžete okamžitě zkompilovat a spustit. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Očekávaný výstup v konzoli:**

```
Searchable PDF created.
```

Otevřete `output.pdf` a zkuste vyhledat slovo, o kterém víte, že se v `input.png` nachází. Pokud se zvýrazní, úspěšně jste **vytvořili searchable PDF** z obrázku.

---

## Často kladené otázky a profesionální tipy

### „Mohu zpracovat více obrázků v jednom běhu?“

Určitě. Zabalte logiku rozpoznání a exportu do smyčky, například pomocí `Directory.GetFiles(..., "*.png")`. Jen nezapomeňte každému PDF přiřadit jedinečný název, např. `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### „Co když můj dokument obsahuje jak anglický, tak španělský text?“

Nastavte vlastnost jazyka na kombinovaný příznak:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose se pak pokusí detekovat znaky z obou abeced.

### „PDF soubor je obrovský – jak ho zmenšit?“

Dva rychlé triky:

1. Nastavte `pdfOptions.KeepOriginalImage = false`, čímž odstraníte rastrové pozadí.  
2. Použijte `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (budete muset přidat tuto vlastnost) pro kompresi vloženého obrázku.

### „Potřebuji licenci pro produkční použití?“

Zkušební verze funguje dobře pro testování, ale pro komerční nasazení musíte zakoupit licenci a zaregistrovat ji co nejdříve ve své aplikaci:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Rozšíření řešení

Nyní, když víte, jak **vytvořit searchable PDF**, můžete chtít:

- **Přidat vodoznak** – použijte `PdfDocument` z Aspose.PDF k překrytí textu po OCR.  
- **Dávkové zpracování PDF** – sloučte více searchable PDF do jednoho pomocí `PdfFileEditor`.  
- **Integrace s Azure Blob Storage** – čtěte/zapisujte obrázky a PDF streamy přímo z cloudu, čímž eliminujete lokální I/O.

Každé z těchto rozšíření následuje stejný vzor: získáte výsledek OCR, nakonfigurujete další knihovnu a spojíte operace do řetězce.

---

## Závěr

Právě jste se naučili, jak **vytvořit searchable PDF** z PNG obrázku pomocí Aspose.OCR v C#. Inicializací OCR enginu, rozpoznáním textu, konfigurací `SearchablePdfOptions` pro **vložení fontů do PDF** a exportem získáte soubor, který je vizuálně identický s originálem a zároveň plně prohledávatelný.  

Od zde můžete experimentovat s dávkovými konverzemi, různými jazyky nebo silnější kompresí – co nejlépe vyhovuje vašemu workflow. Pokud narazíte na problémy, fóra Aspose a API dokumentace jsou skvělé zdroje, ale výše uvedené kroky pokryjí 90 % typických případů použití.

Šťastné kódování a ať jsou vaše PDF vždy prohledávatelná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}