---
category: general
date: 2026-04-04
description: Vytvořte prohledávatelný PDF ze souboru TIF v C# – naučte se, jak převést
  obrázek na PDF, přidat metadata PDF a vygenerovat prohledávatelný dokument pomocí
  Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: cs
og_description: Vytvořte prohledávatelný PDF ze souboru TIF pomocí C#. Převést obrázek
  na PDF, přidat metadata PDF a vytvořit prohledávatelný dokument pomocí Aspose.OCR.
og_title: Vytvořte prohledávatelný PDF z TIF – krok za krokem
tags:
- Aspose.OCR
- C#
- PDF generation
title: Vytvořte prohledávatelný PDF z TIF – Převod obrázku na PDF, přidání PDF metadat
url: /cs/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z TIF – Kompletní průvodce v C#

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenované faktury, ale nebyli jste si jisti, jak zachovat text prohledávatelný a metadata souboru úhledná? Nejste v tom sami. V mnoha automatizačních projektech musí být PDF jak strojově čitelné, tak správně označené informacemi jako název, autor a prahové hodnoty důvěry.

V tomto průvodci projdeme kompletní řešení, které **převádí obrázek na PDF**, vkládá **metadata PDF** a filtruje výsledky OCR s nízkou důvěrou — vše pomocí knihovny Aspose.OCR. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu, a také několik tipů pro řešení okrajových případů.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)  
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)  
- Obrázek TIF, který chcete převést na prohledávatelné PDF (např. `input.tif`)  
- Základní znalost C# a Visual Studio (nebo vašeho oblíbeného IDE)

Nejsou potřeba žádné externí služby — celý proces běží lokálně.

## Krok 1 – Nastavení OCR enginu (Vytvoření jádra prohledávatelného PDF)

První, co potřebujeme, je instance `OcrEngine`, která ví, jaký jazyk má rozpoznávat. Ve většině obchodních scénářů stačí angličtina, ale můžete nahradit `Language.English` libovolným podporovaným jazykem.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Proč je to důležité:** OCR engine provádí těžkou práci převodu rastrových pixelů na Unicode text. Správné nastavení jazyka zvyšuje přesnost a snižuje počet slov s nízkou důvěrou, která jsou později odfiltrována.

> **Pro tip:** Pokud zpracováváte vícejazykové dokumenty, vytvořte více engineů nebo použijte `Language.Multilingual`, aby Aspose automaticky detekoval jazyk.

## Krok 2 – Načtení TIF obrázku (Vytvoření PDF z TIF)

Nyní nasměrujeme engine na zdrojový soubor. Pomocná třída `ImageStream.FromFile` načte obrázek do proudu, který OCR engine může zpracovat.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Možná se ptáte, *„Mohu místo toho použít JPEG nebo PNG?“* Rozhodně — Aspose.OCR podporuje většinu rastrových formátů. Stačí změnit příponu souboru a můžete pokračovat.

## Krok 3 – Konfigurace PDF možností (Přidání metadat do PDF)

Před konverzí definujeme objekt `PdfOptions`. Zde **přidáváme metadata PDF**, jako je název a autor, a také říkáme enginu, aby zahodil slova, jejichž důvěra je pod nastaveným prahem.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Co se zde děje?**  
- `Title` a `Author` se stanou součástí slovníku informací o dokumentu PDF, což usnadní indexaci v systémech správy dokumentů.  
- `MinConfidence` funguje jako ochranná zábrana: OCR často špatně rozpozná slabé znaky; jejich filtrování udržuje prohledávatelnou vrstvu čistou a zlepšuje následné získávání textu.

Pokud potřebujete vlastní metadata (např. `Subject`, `Keywords`), můžete je nastavit pomocí `PdfOptions.CustomProperties`.

## Krok 4 – Převod obrázku na prohledávatelné PDF (Převod obrázku na PDF)

S připraveným enginem a nastavenými možnostmi provede poslední volání samotnou konverzi. Zapíše prohledávatelné PDF na disk a vloží OCR textovou vrstvu pod původní obrázek.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Po spuštění tohoto řádku `output.pdf` obsahuje:
- Původní TIF obrázek jako vizuální pozadí  
- Neviditelnou textovou vrstvu, kterou mohou číst vyhledávače i operace kopírování‑vkládání  
- Metadata, která jsme definovali dříve (název, autor atd.)

### Očekávaný výsledek

Otevřete vygenerované PDF v Adobe Readeru nebo libovolném PDF prohlížeči a zkuste vybrat text. Měli byste být schopni kopírovat věty odpovídající původnímu skenu. Dialog **Properties** dokumentu zobrazí název „Invoice #12345“ a autora „MyCompany“.

## Krok 5 – Ověření filtrování důvěry (Proč MinConfidence pomáhá)

Je užitečné potvrdit, že slova s nízkou důvěrou byla skutečně odstraněna. Skrytý text v PDF můžete zkontrolovat pomocí nástroje jako `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Pokud se slovo vůbec neobjeví, filtr `MinConfidence` fungoval podle očekávání. Upravit práh (např. `0.7f`) můžete, pokud potřebujete agresivnější nebo mírnější filtr.

## Krok 6 – Zpracování více stránek (Vytvoření prohledávatelného PDF z více‑stránkového TIF)

Mnoho faktur přichází jako více‑stránkové TIFFy. Aspose.OCR automaticky zachází s každým snímkem jako samostatnou stránkou. Stačí nasměrovat engine na více‑stránkový soubor; stejná metoda `ConvertToSearchablePdf` vygeneruje více‑stránkové prohledávatelné PDF.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Okrajový případ:** Pokud je stránka prázdná, OCR může stále vytvořit prázdnou textovou vrstvu, což není problém. Prázdné stránky můžete přeskočit kontrolou `ocrEngine.HasText` před konverzí.

## Krok 7 – Balíčkování kompletního příkladu (Všechny kroky dohromady)

Níže je jeden kompletní program připravený ke spuštění, který spojuje všechny kroky. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Spusťte program (`dotnet run` nebo stiskněte **F5** ve Visual Studiu) a uvidíte potvrzovací zprávu. Vygenerované PDF bude ležet vedle vašeho zdrojového obrázku, připravené k indexaci nebo archivaci.

## Často kladené otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Mohu přidat vlastní font do prohledávané vrstvy?** | OCR vrstva používá Unicode; vizuální vzhled je řízen původním obrázkem, takže není nutné vkládat další fonty. |
| **Co když je můj TIF barevný?** | Aspose.OCR automaticky převádí barevné obrázky na odstíny šedi pro OCR, ale můžete zachovat původní barvy v PDF nastavením `PdfOptions.PreserveColor = true`. |
| **Je knihovna thread‑safe?** | Každá instance `OcrEngine` by měla být používána pouze jedním vláknem. Pro paralelní zpracování vytvořte samostatný engine pro každé vlákno. |
| **Jak mohu PDF zašifrovat?** | Použijte `PdfOptions.Security` k nastavení hesla a oprávnění po konverzi OCR. |

## Další kroky (Rozšiřte svůj PDF nástroj)

- **Dávkové zpracování:** Procházet složku s TIFF soubory a pro každý vygenerovat prohledávatelné PDF.  
- **Post‑zpracování:** Použít Aspose.PDF ke sloučení vygenerovaných PDF do jednoho hlavního dokumentu.  
- **Pokročilá metadata:** Vyplnit vlastní XMP pole pro lepší integraci se SharePoint nebo ECM systémy.  

Všechny tyto rozšíření staví na základním vzoru, který jsme právě probrali: **vytvořit prohledávatelné PDF**, **převést obrázek na PDF** a **přidat metadata PDF**.

*Šťastné programování! Pokud narazíte na potíže, zanechte komentář níže nebo se podívejte do dokumentace Aspose.OCR pro nejnovější aktualizace API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}