---
category: general
date: 2026-03-13
description: Vytvořte prohledávatelný PDF z libovolného obrázku pomocí Aspose OCR.
  Naučte se, jak převést obrázek na EPUB, přidat prohledávatelný text a vygenerovat
  prohledávatelný PDF v C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: cs
og_description: Vytvořte prohledávatelný PDF z libovolného obrázku pomocí Aspose OCR.
  Tento průvodce ukazuje, jak převést obrázek na EPUB, přidat prohledávatelný text
  a vygenerovat prohledávatelný PDF v C#.
og_title: Vytvořte prohledávatelný PDF – Převod obrázku na EPUB a přidání textu
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Vytvořte prohledávatelný PDF – převod obrázku na EPUB a přidání textu
url: /cs/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte prohledávatelný PDF – Převod obrázku na EPUB a přidání textu

Chcete **vytvořit prohledávatelný PDF** ze skenované účtenky nebo jakéhokoli obrázku? V tomto tutoriálu vám ukážeme, jak vytvořit prohledávatelný PDF pomocí Aspose OCR a zároveň **převést obrázek na EPUB** a **přidat vrstvy prohledávatelného textu** – vše v jediném projektu C#.

Pokud jste někdy narazili na PDF, které vypadá dobře, ale nelze ho prohledávat, nejste sami. Dobrou zprávou je, že skrytá textová vrstva může proměnit plochý obrázek v plně prohledávatelný dokument a Aspose to dělá téměř bez námahy.

## Co se naučíte

* Jak inicializovat engine Aspose OCR a nastavit jazyk.  
* Přesné kroky k **převodu obrázku na EPUB** pro distribuci e‑knih.  
* Jak nakonfigurovat PDF writer tak, aby výstup obsahoval skrytou, prohledávatelnou textovou vrstvu.  
* Tipy pro řešení okrajových případů, jako jsou vícestránkové účtenky nebo neanglické jazyky.  

Vše, co potřebujete předem, je vývojové prostředí .NET (Visual Studio 2022 nebo novější) a NuGet balíček Aspose OCR. Žádné externí služby, žádné nejasné konfigurační soubory – jen čistý C#, který můžete zkopírovat, vložit a spustit.

## Předpoklady

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR cílí na .NET Standard 2.0+, takže .NET 6 vám poskytuje nejnovější vylepšení runtime. |
| Aspose.OCR NuGet package | Poskytuje třídy `OcrEngine`, `EpubWriter` a `PdfWriter`, které jsou v kódu použity. |
| An image file (e.g., `receipt.jpg`) | Zdroj, na který spustíte OCR. Jakýkoli rastrový obrázek (PNG, JPEG, BMP) funguje. |
| Basic C# knowledge | Budete číst a upravovat úryvky, ne učit se jazyk od nuly. |

Balíček můžete nainstalovat pomocí následujícího příkazu:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Pokud používáte Visual Studio, UI NuGet Package Manager dělá totéž – stačí vyhledat “Aspose.OCR”.

## Krok 1 – Vytvoření prohledávatelného PDF pomocí Aspose OCR

První, co potřebujeme, je instance `OcrEngine`, která ví, který jazyk rozpoznávat. Angličtina je výchozí, ale můžete ji vyměnit za francouzštinu, němčinu atd. nastavením `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Proč nejprve inicializovat engine? Engine drží model rozpoznávání v paměti, takže jeho jednorázové vytvoření a opakované používání napříč více obrázky šetří jak CPU, tak RAM. Ve větších dávkových úlohách byste udržovali stejnou instanci po celou dobu běhu.

## Krok 2 – Načtení obrázku a provedení OCR

Dále nasměrujeme engine na soubor, který chceme zpracovat. `ImageStream.FromFile` načte obrázek do formátu, který OCR engine rozumí.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Co když je obrázek vícestránkový?**  
> Aspose OCR dokáže zpracovat vícestránkové TIFF soubory přímo. Stačí předat cestu k TIFF souboru; engine automaticky projde každou stránku.

## Krok 3 – Převod obrázku na EPUB

Pokud potřebujete také e‑knihu ze skenovaného dokumentu, Aspose to zvládne jedním řádkem. `EpubWriter` používá stejnou instanci `OcrEngine`, což znamená, že výsledky OCR jsou znovu použity bez dalšího zpracování.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Proč exportovat do EPUB? EPUB je formát s plynulým rozložením – ideální pro mobilní čtečky. OCR text se stane výběrným a původní obrázek zůstane na pozadí, čímž zachová vzhled původního skenu.

## Krok 4 – Přidání vrstvy prohledávatelného textu do PDF

Nyní přichází část, která skutečně **vytváří prohledávatelný PDF**. Aktivací `AddSearchableTextLayer` PDF writer vloží neviditelnou textovou vrstvu, která odráží výstup OCR. Uživatelé mohou vyhledávat, kopírovat nebo zvýrazňovat text stejně jako v nativním PDF.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Častý úskalí:** Zapomenutí nastavit `AddSearchableTextLayer` vede k PDF, které vypadá stejně, ale neobsahuje žádný prohledávatelný text. Vždy tuto volbu zkontrolujte, když potřebujete prohledávatelný dokument.

## Krok 5 – Kompletní funkční příklad

Spojením všech částí získáte samostatnou konzolovou aplikaci, kterou můžete vložit do nového .NET projektu a okamžitě spustit.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Očekávaný výstup

* `receipt.epub` – soubor EPUB, který můžete otevřít v Calibre, Apple Books nebo jakémkoli e‑readeru.  
* `receipt_searchable.pdf` – PDF, kde můžete stisknout **Ctrl + F** a najít jakékoli slovo, které se objevilo v původním obrázku.

Pokud otevřete PDF v Adobe Acrobat a podíváte se na **File → Properties → Description**, uvidíte skrytý textový proud pod záložkou **Fonts**, což potvrzuje, že prohledávatelná vrstva je přítomna.

## Časté otázky a okrajové případy

**Q: Funguje to i s neanglickými jazyky?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}