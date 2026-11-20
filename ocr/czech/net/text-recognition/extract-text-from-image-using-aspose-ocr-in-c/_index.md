---
category: general
date: 2026-08-09
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak načíst
  obrázek pro OCR, nastavit jazyk OCR, zpracovat OCR obrázku a efektivně převést obrázek
  na text.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: cs
lastmod: 2026-08-09
og_description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Tento tutoriál ukazuje,
  jak načíst obrázek pro OCR, nastavit jazyk OCR, zpracovat OCR obrázku a převést
  obrázek na text pomocí několika řádků kódu.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Extrahujte text z obrázku pomocí Aspose OCR – průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahovat text z obrázku pomocí Aspose OCR v C#
url: /cs/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku pomocí Aspose OCR v C#

Pokud potřebujete **extrahovat text z obrázku** v .NET aplikaci, tento průvodce vás provede kompletním, připraveným řešením. Uvidíte, jak **načíst obrázek pro OCR**, vybrat správný jazykový modul, spustit OCR engine a nakonec **převést obrázek na text** pomocí několika řádků C#.

Tutoriál pokrývá vše potřebné k získání spolehlivých výsledků s Aspose.OCR, včetně běžných úskalí, jako jsou nepodporované formáty obrázků a jazykové specifické nuance. Na konci budete mít samostatný program, který vypíše rozpoznaný text do konzole.

## Co dosáhnete

* Načíst soubor obrázku do Aspose OCR engine.  
* **Nastavit jazyk OCR** (v příkladu Cyrillic, ale funguje jakýkoli podporovaný jazyk).  
* **Zpracovat OCR obrázku** a získat textovou reprezentaci.  
* **Převést obrázek na text** a zobrazit jej, připravený pro další zpracování nebo uložení.  

**Požadavky**

* .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.6+).  
* Visual Studio 2022 (nebo jakékoli IDE podporující C#).  
* NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Extrahovat text z obrázku – kompletní průchod kódem

Níže je kompletní, spustitelný program. Zkopírujte jej do nového konzolového projektu a nahraďte `YOUR_DIRECTORY/sample_cyrillic.jpg` cestou k vašemu vlastnímu obrázku.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Proč je každý krok důležitý

1. **Vytvořit instanci OCR engine** – `OcrEngine` zapouzdřuje veškerou funkčnost OCR. Okamžité uvolnění prostřednictvím `Dispose` uvolní nativní zdroje, což je kritické pro dlouhodobě běžící služby.  
2. **Nastavit jazyk OCR** – Výběr správného jazykového modulu výrazně zvyšuje přesnost. Aspose poskytuje více než 30 jazykových balíčků; výchozí je angličtina. Příklad používá Cyrillic pro demonstraci ne‑latinského skriptu.  
3. **Načíst obrázek pro OCR** – Engine pracuje s `ImageStream`. Poskytnutí obrázku ve vysokém rozlišení (≥300 dpi) snižuje chybovost, zejména u složitých skriptů.  
4. **Zpracovat OCR obrázku** – Zde probíhá těžká práce. Metoda vrací `OcrResult`, který obsahuje extrahovaný text, skóre důvěry a volitelná data o rozložení.  
5. **Převést obrázek na text** – `result.Text` je obyčejný `string`. Můžete jej zapsat do souboru, vložit do vyhledávacího indexu nebo předat do následných NLP pipeline.  

---

## Načíst obrázek pro OCR

`ImageStream.FromFile` metoda podporuje běžné rastrové formáty. Pokud získáváte obrázky jako pole bajtů (např. z webového API), použijte místo toho `ImageStream.FromBytes(byte[])`:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Tip:** Vždy ověřte, že obrázek není poškozený před předáním engine. Rychlá kontrola `try { Image.FromFile(...); } catch { ... }` zabrání výjimkám za běhu.

---

## Nastavit jazyk OCR

Aspose.OCR obsahuje jazykové balíčky, které můžete aktivovat za běhu. Pro vypsání všech dostupných jazyků:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Pokud potřebujete rozpoznat více jazyků ve stejném dokumentu, kombinujte je pomocí bitového OR operátoru:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Okrajový případ:** Míchání jazyků psaných zprava doleva (RTL) (např. arabština) s levostrannými skripty může vyžadovat další zpracování rozložení. Aspose automaticky detekuje směr, ale můžete jej doladit pomocí `engine.PageSegmentationMode`.

---

## Zpracovat OCR obrázku

Volání `Process` je synchronní a blokuje, dokud engine nedokončí. Pro velké dávky nebo UI aplikace zvažte asynchronní přetížení:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Častý úskalí:** Zapomenutí nastavit `engine.Image` před voláním `Process` vyvolá `InvalidOperationException`. Vždy nejprve přiřaďte obrázek.

---

## Převést obrázek na text

Extrahovaný řetězec lze manipulovat jako jakýkoli jiný .NET `string`. Například pro zápis výstupu do souboru:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Pokud potřebujete zachovat konce řádků přesně tak, jak jsou v obrázku, použijte přímo `result.Text`. Pro následné zpracování (např. odstranění nadbytečných mezer) použijte standardní metody řetězců:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Shrnutí kompletního příkladu

Spojením všech částí program:

1. Vytvoří instanci `OcrEngine`.  
2. **Nastaví jazyk OCR** na Cyrillic (nebo jakýkoli jazyk, který zvolíte).  
3. **Načte obrázek pro OCR** z disku.  
4. **Zpracuje OCR obrázku** pro získání textového výsledku.  
5. **Převádí obrázek na text** a vypíše jej.  

Spuštěním vzorku s čistým cyrilickým obrázkem získáte výstup podobný:

```
=== Recognized Text ===
Пример текста на кириллице
```

Pokud obrázek obsahuje anglický text, jednoduše změňte `engine.Language = OcrLanguage.English;` a stejný kód **extrahuje text z obrázku** správně.

---

## Závěr

Teď už víte, jak **extrahovat text z obrázku** pomocí Aspose OCR v C#. Tutoriál pokrýval načtení obrázku, výběr vhodného jazyka, spuštění OCR procesu a **převod obrázku na text** pro následné použití.  

Od tady můžete:

* Experimentovat s dalšími jazyky (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Integrovat krok OCR do většího pipeline (např. ingestování dokumentů, prohledávatelné PDF).  
* Optimalizovat výkon dávkováním obrázků nebo použitím asynchronního API.

Neváhejte prozkoumat dokumentaci Aspose.OCR pro pokročilé funkce, jako jsou vlastní slovníky, režimy segmentace stránek a ladění přesnosti OCR. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)
- [Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}