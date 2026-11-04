---
category: general
date: 2026-02-28
description: Vytvořte prohledávatelný PDF v C# kombinací obrázků vertikálně. Naučte
  se, jak vertikálně skládat obrázky a převést naskenované stránky PDF pomocí Aspose
  OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: cs
og_description: Vytvořte prohledávatelný PDF v C# sloučením obrázků vertikálně. Tento
  průvodce ukazuje, jak vertikálně uspořádat obrázky a převést naskenované stránky
  do PDF pomocí Aspose OCR.
og_title: Vytvořte prohledávatelný PDF v C# – Spojte obrázky vertikálně
tags:
- Aspose OCR
- C#
- PDF generation
title: Vytvořit prohledávatelný PDF v C# – Vertikálně spojit obrázky
url: /cs/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF v C# – Vertikální spojení obrázků

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** z několika naskenovaných PNG souborů, ale nevedeli jste, kde začít? Nejste v tom sami. V mnoha projektech automatizace dokumentů je největší problém převést hromadu souborů s obrázky na jeden úhledný, prohledávatelný PDF, který můžete indexovat a sdílet.

V tomto tutoriálu vás provedeme kompletním, připraveným příkladem, který ukazuje **jak vrstvit obrázky vertikálně**, **jak spojit obrázky vertikálně** a nakonec **převést naskenované stránky do PDF** do jediného prohledávatelného dokumentu pomocí GPU‑akcelerovaného enginu Aspose.OCR. Na konci budete mít samostatný program, který můžete vložit do libovolného .NET řešení.

> **Co se naučíte**
> - Inicializovat OCR engine s podporou GPU.
> - Zpracovat dávku obrázků paralelně.
> - **Spojit obrázky vertikálně** tak, aby napodobily vícestránkový sken.
> - Exportovat prohledávatelné PDF a podrobnou JSON zprávu pro následnou analýzu.

## Požadavky

- .NET 6+ (kód se kompiluje s .NET 6, .NET 7 nebo .NET 8)
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)
- Počítač s GPU, pokud chcete zachovat nastavení `ProcessingMode.Gpu` (CPU fallback také funguje)
- Složka s několika naskenovanými PNG/JPEG soubory (demo používá `page1.png`, `page2.png`, `page3.png`)

Žádné externí služby, žádné skryté konfigurační soubory – jen čistý C#.

## Krok 1 – Nastavení OCR enginu pro **vytvoření prohledávatelného PDF**

Nejprve vytvoříme `OcrEngine`, zapneme GPU akceleraci, vybereme angličtinu jako jazyk a přidáme několik předzpracovatelských filtrů. Tyto filtry zvyšují přesnost narovnáním nakloněných stránek (`DeskewFilter`) a odstraněním šumu (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Proč je to důležité:** OCR engine provádí těžkou práci rozpoznávání textu. Povolení `ProcessingMode.Gpu` může na moderní grafické kartě zkrátit čas rozpoznávání na polovinu, zatímco filtry snižují běžné artefakty skenování, které by jinak vedly k nečitelné výstupní podobě.

## Krok 2 – Konfigurace dávkového procesoru pro **efektivní převod naskenovaných stránek do PDF**

Zpracování každé stránky po jedné je v pořádku pro pár obrázků, ale v reálných projektech často jde o desítky nebo stovky stránek. `OcrBatchProcessor` od Aspose.OCR nám umožňuje spouštět rozpoznávání paralelně, což dramaticky zrychluje krok **převodu naskenovaných stránek do PDF**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Tip:** Pokud používáte jen CPU, nastavte `ProcessingMode = ProcessingMode.Cpu`. Dávkový procesor i tak bude respektovat `MaxDegreeOfParallelism`, takže jej můžete nastavit tak, aby nepřetěžoval stroj.

## Krok 3 – Spuštění OCR na dávce a shromáždění výsledků

Nyní skutečně rozpoznáváme text. Metoda `Recognize` vrací seznam objektů `OcrResult`, z nichž každý obsahuje původní obrázek i extrahovaný text.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

V tomto okamžiku máte vše, co potřebujete k **vytvoření prohledávatelného PDF**: obrázky (stále v paměti) a související textové vrstvy.

## Krok 4 – **Spojit obrázky vertikálně** a vygenerovat prohledávatelné PDF

Většina naskenovaných dokumentů jsou vícestránkové PDF, takže musíme spojit jednotlivé obrázky stránek do jednoho vysokého obrázku, který odráží fyzický stack. Aspose.OCR poskytuje `Image.CombineVertical` právě pro tento účel.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Výsledný soubor (`combined_searchable.pdf`) obsahuje vybratelný, prohledávatelný text pod každým obrázkem stránky – přesně to, co potřebujete k **vytvoření prohledávatelného PDF** ze skenovaných zdrojů.

![Příklad vytvoření prohledávatelného PDF](/images/create-searchable-pdf.png "příklad vytvoření prohledávatelného PDF")

*Alt text obrázku: příklad vytvoření prohledávatelného PDF ukazující kombinované PDF s prohledávatelným textem.*

**Proč vertikální spojení?** Mnoho OCR knihoven zachází s každým obrázkem jako s oddělenou stránkou. Spojením je zachováme pořadí stránek v PDF a zároveň využijeme jeden OCR průchod pro celý dokument.

## Krok 5 – Export podrobného JSON pro první stránku (užitečné pro následné workflowy)

Někdy potřebujete více než PDF; možná chcete předat OCR data do databáze nebo do pipeline strojového učení. Aspose.OCR vám umožní serializovat každý `OcrResult` do JSON, zachovávající ohraničovací rámečky, skóre důvěry a další informace.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Očekávaný úryvek JSON (zkrácený):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Nyní můžete tento JSON předat libovolnému následnému systému – ať už indexujete text v Elasticsearch nebo jej posíláte do vlastního analytického dashboardu.

---

## Jak **vrstvit obrázky vertikálně** – Rychlé shrnutí

Pokud se ptáte **jak vrstvit obrázky vertikálně** bez Aspose, můžete použít `System.Drawing` k vytvoření nového bitmapu a vykreslit každou stránku po sobě. Nicméně vestavěná metoda Aspose `Image.CombineVertical` se postará o DPI, formát pixelů a správu paměti, což z ní dělá nejspolehlivější volbu pro produkční kód.

### Alternativa: Použití `System.Drawing` (jen ze zvědavosti)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Manuální přístup funguje, ale ztrácíte pohodlí automatické správy DPI a možnost přímo předat výsledek zpět do `RecognizeToPdf`. Držte se `CombineVertical`, pokud nemáte velmi specifický požadavek.

## Časté úskalí a jak se jim vyhnout

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Chyby nedostatku paměti** při zpracování desítek vysoce rozlišených skenů | Každý obrázek zůstává v paměti, dokud není PDF zapsáno | Uvolněte objekty `Image` hned po použití (`using` bloky) nebo před spojením zmenšete rozlišení obrázků |
| **Nečistý text** po OCR | Nakloněné skeny nebo nízký kontrast | Zachovejte `DeskewFilter` a `DenoiseFilter`; v případě potřeby zvažte přidání `ContrastFilter` |
| **Chybějící prohledávatelná vrstva** | Použili jste `Recognize` místo `RecognizeToPdf` | Ujistěte se, že na spojeném obrázku voláte `ocrEngine.RecognizeToPdf` |
| **Selhání GPU fallbacku** na strojích bez správných ovladačů | `ProcessingMode.Gpu` vyvolá výjimku | Zabalte vytvoření enginu do try/catch a přepněte na `ProcessingMode.Cpu` |

## Další kroky – Rozšíření workflowu

Nyní, když víte, jak **vytvořit prohledávatelné PDF**, můžete chtít:

- **Dávkově zpracovat celé složky** pomocí `Directory.GetFiles` a `foreach` smyčky.
- **Přidat vodoznaky** na každou stránku před spojením (použijte `ImageProcessor` z Aspose.Imaging).
- **Rozdělit prohledávatelné PDF zpět na jednotlivé stránky** pokud později potřebujete PDF po stránkách (`PdfDocument.Split` z Aspose.PDF).
- **Integrovat s Azure Blob Storage** pro načtení obrázků z cloudu a nahrání finálního PDF zpět.

Všechny tyto rozšíření přirozeně zahrnují stejné základní koncepty: nastavení OCR, manipulaci s obrázky a export PDF.

---

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření prohledávatelného PDF** ze sady naskenovaných obrázků v C#. Inicializací GPU‑povoleného `OcrEngine`, spuštěním paralelní dávky pomocí `OcrBatchProcessor`, **spojením obrázků vertikálně** a nakonec voláním `RecognizeToPdf` získáte úhledný, prohledávatelný dokument připravený k archivaci nebo indexaci. Extra export do JSON vám poskytuje úplný přehled o výsledcích OCR, což otevírá možnosti pro analytiku nebo vlastní workflowy.

Vyzkoušejte to, experimentujte s různými filtry a sledujte, jak se vaše pipeline pro automatizaci dokumentů stane mnohem plynulejší. Pokud narazíte na nějaké potíže, zanechte komentář – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}