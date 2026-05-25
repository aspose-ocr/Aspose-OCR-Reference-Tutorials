---
category: general
date: 2026-05-25
description: rozpoznat text z obrázku pomocí Aspose OCR v C#. Naučte se, jak načíst
  obrázek pro OCR, nastavit jazyk OCR, vytvořit OCR engine a extrahovat text z TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: cs
og_description: Rozpoznávat text z obrázku pomocí Aspose OCR v C#. Tento tutoriál
  ukazuje, jak vytvořit OCR engine, načíst obrázek pro OCR, nastavit jazyk OCR a extrahovat
  text z TIFFu.
og_title: rozpoznat text z obrázku pomocí Aspose OCR – kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Rozpoznat text z obrázku pomocí Aspose OCR – kompletní průvodce C#
url: /cs/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku pomocí Aspose OCR – Kompletní průvodce v C#

Už jste někdy potřebovali **rozpoznat text z obrázku**, ale nebyli jste si jisti, která knihovna vám poskytne jak rychlost, tak přesnost? Nejste v tom sami. V mnoha projektech zpracování faktur nebo archivace je největším problémem získat čistý, prohledávatelný text z TIFF souborů bez psaní vlastního parseru.

Takže: Aspose OCR pro .NET udělá celý tento proces hračkou. V tomto průvodci projdeme vše, co potřebujete – instalaci balíčku, **vytvoření OCR engine**, načtení TIFF, nastavení jazyka OCR a nakonec **extrahování textu z TIFF**. Na konci budete mít připravenou konzolovou aplikaci, která dokáže **rozpoznat text z obrázku** během okamžiku.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework)
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete)
- Aspose.OCR NuGet package (GPU podpora vyžaduje doplněk `Aspose.OCR.Gpu`)
- GPU s podporou CUDA, pokud chcete extra rychlost (volitelné, ale doporučené)

> **Pro tip:** Pokud nemáte GPU, stačí vynechat řádek `GpuDevice` a engine se automaticky přepne na CPU.

## Krok 1: Instalace Aspose OCR a vytvoření OCR engine

Nejprve přidejte potřebné balíčky přes NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Nyní můžeme **vytvořit OCR engine**. Tento objekt je srdcem procesu; obsahuje konfiguraci, jako je zařízení, na kterém běží, a limity paměti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Proč je to důležité:** Připojením engine k GPU dramaticky zkrátíte dobu potřebnou k **rozpoznání textu z obrázku**, zejména u velkých dávkách vysoce rozlišených TIFF souborů.

## Krok 2: Načtení obrázku pro OCR

Dále potřebujeme **načíst obrázek pro OCR**. Aspose.OCR pracuje s `System.Drawing.Image`, takže jakýkoli formát podporovaný GDI+ (včetně multi‑page TIFF) je v pořádku.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Pokud pracujete s multi‑page TIFF, můžete procházet stránky pomocí `image.SelectActiveFrame`, ale ve většině scénářů stačí jedno volání.

## Krok 3: Nastavení jazyka OCR

Engine si sám neví, v jakém jazyce skenujete. **Nastavte jazyk OCR** před spuštěním rozpoznávače; jinak získáte spoustu nesmyslného výstupu.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Věděli jste?** Přepínání jazyků za běhu je levné – můžete dokonce zpracovat dokument s více jazyky změnou této vlastnosti mezi stránkami.

## Krok 4: Provedení rozpoznání – Rozpoznání textu z obrázku

Teď ta zábavná část: skutečně **rozpoznat text z obrázku**. Metoda `Recognize` vrací prostý řetězec se všemi detekovanými znaky.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Pokud potřebujete skóre důvěry nebo ohraničující rámečky, můžete použít přetíženou verzi, která vrací objekt `OcrResult`, ale pro většinu úloh extrakce stačí prostý řetězec.

## Krok 5: Extrahování textu z TIFF (a zpracování souborů s více stránkami)

Když je zdroj TIFF obsahující několik stránek, budete chtít opakovat kroky 2‑4 pro každý rámec. Zde je rychlá smyčka, která **extrahuje text z TIFF** stránku po stránce:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

Výše uvedený kód vypisuje extrahovaný text pro každou stránku, což usnadňuje přesměrování výsledků do databáze nebo vyhledávacího indexu.

## Krok 6: Zobrazení nebo uložení extrahovaného textu

Nakonec **zobrazíme extrahovaný text** a případně jej zapíšeme do souboru pro pozdější zpracování.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Spuštění programu by mělo vypsat rozpoznané znaky a vytvořit `extracted_text.txt` vedle vašeho zdrojového TIFF.

---

## Časté otázky a okrajové případy

- **Co když není moje GPU detekováno?**  
  Odstraňte řádek `GpuDevice`; engine se automaticky přepne do režimu CPU. Výkon bude pomalejší, ale výsledky zůstanou přesné.

- **Mohu zpracovávat soubory PNG nebo JPEG?**  
  Rozhodně – `Image.FromFile` funguje s jakýmkoli formátem podporovaným System.Drawing, takže můžete **načíst obrázek pro OCR** bez ohledu na příponu.

- **Jak zacházet s nízkým rozlišením skenů?**  
  Zvyšte `ocrEngine.PreprocessOptions.Dpi` před voláním `Recognize`. Vyšší DPI poskytne engine více pixelů k práci, což zlepšuje přesnost.

- **Existuje limit velikosti TIFF?**  
  Vlastnost `GpuMemoryLimit` omezuje využití GPU. Pokud limit překročíte, engine přejde na CPU pro zbývající stránky.

## Závěr

Nyní máte kompletní, připravený k nasazení úryvek kódu, který **rozpozná text z obrázku** pomocí Aspose OCR v C#. Tutoriál pokryl, jak **vytvořit OCR engine**, **načíst obrázek pro OCR**, **nastavit jazyk OCR** a **extrahovat text z TIFF** – vše s využitím akcelerace GPU pro rychlost.

Od sem můžete:

- Experimentovat s různými jazyky (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified` atd.).
- Integrovat výstup do prohledávatelného indexu ElasticSearch.
- Přidat post‑processing (kontrola pravopisu, čištění regulárními výrazy) pro zlepšení kvality dat.

Vyzkoušejte to na vlastní dávce faktur, upravte limity paměti a sledujte, jak OCR výkon stoupá. Šťastné programování!

## Související tutoriály

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}