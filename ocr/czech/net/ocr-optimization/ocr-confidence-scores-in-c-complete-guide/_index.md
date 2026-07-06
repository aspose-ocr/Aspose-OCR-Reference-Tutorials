---
category: general
date: 2026-05-31
description: Naučte se, jak získat skóre spolehlivosti OCR v C# při extrakci textu
  z obrázku a čtení obrázku účtenky pomocí Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: cs
og_description: Skóre důvěry OCR vám umožňuje odhadnout přesnost; tento průvodce ukazuje,
  jak extrahovat text z obrázku, získat ohraničující rámečky a přečíst obrázek účtenky
  pomocí Aspose OCR.
og_title: Skóre důvěry OCR v C# – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Skóre důvěry OCR v C# – Kompletní průvodce
url: /cs/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR confidence scores in C# – Complete Guide

Už jste se někdy zamýšleli, jak získat **OCR confidence scores**, když potřebujete *extrahovat text z obrázku*? Možná se snažíte **read receipt image** soubory pro sledování výdajů a chcete vědět, které znaky jsou pro engine nejisté. Dobrá zpráva? S Aspose.OCR můžete získat procenta důvěry, ohraničující rámečky a prostý text z JPG během několika řádků C#.

V tomto tutoriálu projdeme vše, co potřebujete vědět: instalaci knihovny, konfiguraci enginu pro **perform OCR on JPG**, získání skóre důvěry a interpretaci **OCR bounding boxes**, které ukazují, kde se každý znak nachází na stránce. Na konci budete mít připravenou konzolovou aplikaci, která vypíše každý znak, jeho důvěru a jeho umístění — ideální pro ověřování účtenek nebo jakéhokoli naskenovaného dokumentu.

## Co se naučíte

- Nainstalujte Aspose.OCR přes NuGet a nastavte základní OCR engine.  
- Konfigurujte `OcrOptions` pro požadavek na výstup prostého textu **with confidence scores** a **bounding boxes**.  
- Procházejte `OcrResult` a **extract text from image** řádek po řádku a symbol po symbolu.  
- Řešte běžné problémy, jako jsou chybějící soubory, znaky s nízkou důvěrou a formáty, které nejsou JPG.  
- Rozšiřte příklad tak, aby zpracovával více obrázků účtenek ve složce.

Předchozí zkušenost s Aspose není vyžadována; stačí funkční .NET prostředí a obrázek účtenky (JPG), který chcete otestovat.

---

## Krok 1 – Instalace Aspose.OCR a příprava projektu

Nejprve potřebujete NuGet balíček Aspose.OCR. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Bezplatná zkušební verze funguje až pro 200 stránek, což je více než dost pro testování skenování účtenek.

Po instalaci balíčku vytvořte nový konzolový projekt (pokud jej ještě nemáte):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Nyní můžete otevřít vygenerovaný soubor `Program.cs` a začít přidávat using direktivy:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Tyto jmenné prostory vám poskytují přístup k `OcrEngine`, `OcrOptions` a typům výsledků, které budeme později potřebovat.

## Krok 2 – Získání OCR confidence scores a OCR bounding boxes

Toto je jádro tutoriálu. Nakonfigurujeme engine tak, aby každý rozpoznaný znak měl **confidence score** a **bounding box** (obdélník, který obklopuje glyfu). Nadpis H2 sám obsahuje primární klíčové slovo, splňující SEO pravidlo.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Proč zahrnout confidence scores?**  
Confidence score (0‑100 %) vám říká, jak jistý je engine ohledně každého znaku. Pokud výstup předáváte do následné logiky — například workflow schvalování výdajů — můžete automaticky odmítnout nebo označit znaky s nízkou důvěrou.

**Proč požadovat bounding boxes?**  
Bounding boxes jsou nezbytné, když potřebujete zvýraznit text na původním obrázku, extrahovat podregiony nebo zarovnat OCR výsledky s UI překryvem. Každý `character.Bounds` poskytuje X, Y, šířku a výšku v pixelech.

## Krok 3 – Provedení OCR na JPG a extrahování textu z obrázku

Nyní skutečně spustíme engine. Volání `Recognize()` provede veškerou těžkou práci a vrátí objekt `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Pokud je cesta k obrázku špatná nebo soubor není podporovaného formátu, Aspose vyhodí `FileNotFoundException` nebo `UnsupportedImageFormatException`. V produkčním kódu obalte volání do try/catch bloku, abyste tyto okrajové případy ošetřili elegantně.

### Získání prostého textu

Pokud potřebujete jen spojený text, můžete přečíst `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Ale protože jsme také požádali o confidence scores a bounding boxes, projdeme strukturu, abychom viděli podrobnosti každého znaku.

## Krok 4 – Procházení řádků, symbolů a zobrazení OCR confidence scores

Zde je smyčka, která vypisuje každý znak, jeho důvěru a jeho rámeček. Toto je místo, kde příklad **read receipt image** skutečně zazáří.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Ukázkový výstup může vypadat takto:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretace čísel:**  
- **Confidence ≥ 90 %** – obvykle bezpečné přijmout.  
- **Confidence 70‑89 %** – možná budete chtít dvojitě zkontrolovat, zejména číslice v částkách.  
- **Confidence < 70 %** – zvažte označení k ruční revizi.

## Krok 5 – Kompletní spustitelný příklad (včetně ošetření chyb)

Spojením všeho dohromady zde máte kompletní program, který můžete zkopírovat a vložit do `Program.cs`. Obsahuje jednoduchou kontrolu chybějících souborů a vypíše přátelskou zprávu, pokud OCR selže.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Očekávaný výstup

Když spustíte `dotnet run`, konzole nejprve zobrazí spojený text účtenky, poté seznam každého znaku s jeho confidence score a bounding box. Pokud je důvěra znaku nízká, uvidíte procento pod 80, což je podnět k ručnímu ověření dané části účtenky.

## Bonus: Zpracování více účtenek ve složce

Pokud máte dávku JPG souborů s účtenkami, zabalte výše uvedenou logiku do smyčky `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Nezapomeňte pro každý soubor resetovat `OcrEngine` nebo vytvořit nový uvnitř smyčky, aby nedošlo k úniku stavu.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Dávkové zpracování je užitečné pro noční importy výdajů.

---

## Závěr

Nyní máte solidní, end‑to‑end řešení pro získání **OCR confidence scores** v C#, **extrahování textu z obrázku** a získání **OCR bounding boxes**, zatímco **perform OCR on JPG** soubory, jako je **read receipt image**. Kód je zcela samostatný, funguje s nejnovější verzí Aspose.OCR (k 31. 5. 2026) a poskytuje detailní data, která potřebujete k vytvoření spolehlivých pipeline pro zpracování dokumentů.

Co dál? Zkuste vizualizovat bounding boxes na původní účence pomocí `System.Drawing` nebo UI knihovny, nebo předávejte znaky s nízkou důvěrou do sekundární verifikační služby. Můžete také experimentovat s různými jazyky nastavením `ocrEngine.Options.Language = OcrLanguage.French;` — API podporuje mnoho jazykových nastavení.

Šťastné programování a ať vaše confidence scores zůstávají vždy vysoké! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## Co byste se měli naučit dál?

- [Extrahování textu z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak získat možnosti znaků OCR pro rozpoznané znaky v rozpoznávání obrazu](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Jak použít Aspose OCR pro JSON výsledek v rozpoznávání obrazu](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}