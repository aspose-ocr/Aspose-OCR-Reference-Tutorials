---
category: general
date: 2026-01-15
description: c# OCR tutoriál, který vám ukáže, jak rozpoznat text z obrázku, extrahovat
  text z faktury a převést obrázek na text pomocí Aspose OCR na GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: cs
og_description: c# OCR tutoriál, který vás naučí rozpoznávat text z obrázku, extrahovat
  text z faktury a převádět obrázek na text pomocí Aspose OCR na GPU.
og_title: c# OCR tutoriál – Rychlé rozpoznávání textu s GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: c# OCR tutoriál – Rozpoznání textu z obrázku s akcelerací GPU
url: /cs/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Rozpoznání textu z obrázku s akcelerací GPU

Už jste někdy potřebovali **c# ocr tutorial**, který skutečně splní úkol bez nekonečného pokusu‑a‑omylu? Možná se díváte na fakturu ve vysokém rozlišení a přemýšlíte, jak **extrahovat text z faktury** soubory během několika sekund. Dobrou zprávou je, že nemusíte znovu vymýšlet kolo — Aspose.OCR vám poskytuje čisté, GPU‑akcelerované API, které za vás udělá těžkou práci.

V tomto průvodci projdeme kompletním, spustitelným příkladem, který ukazuje, jak **rozpoznat text z obrázku** soubory, **převést obrázek na text**, a jak řešit nejčastější úskalí. Na konci budete mít samostatný program, který dokáže přečíst jakýkoli obrázek dokumentu, od účtenek po naskenované smlouvy, a výstupem bude čistý, prohledávatelný text.

## Co se naučíte

- Jak nainstalovat a odkazovat na NuGet balíček Aspose.OCR.
- Jak nakonfigurovat OCR engine tak, aby běžel na GPU pro bleskově rychlý výkon.
- Správný způsob, jak **načíst obrázek pro OCR** pomocí `OcrImage.FromFile`.
- Jak zavolat `Recognize` s požadovaným jazykem a získat výsledek.
- Tipy pro práci s více‑stránkovými PDF, snímky s nízkým kontrastem a zpracování chyb.

Předchozí zkušenost s Aspose není vyžadována; stačí funkční vývojové prostředí .NET (Visual Studio 2022 nebo VS Code) a slušná GPU (i integrovaná Intel GPU postačí).

## Krok 1 – Instalace Aspose.OCR a příprava projektu

Nejprve: potřebujete knihovnu Aspose.OCR. Nejjednodušší způsob je přes NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud cílíte na .NET 6 nebo novější, balíček automaticky stáhne nativní GPU binárky pro Windows, Linux a macOS. Žádné další DLL kópie nejsou potřeba.

Po přidání balíčku otevřete soubor projektu (`*.csproj`) a ověřte odkaz:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Nyní máte vše, co potřebujete k zahájení kódování.

## Krok 2 – Vytvoření OCR engine s podporou GPU (c# ocr tutorial)

Jádrem **c# ocr tutorial** je `OcrEngine`. Nastavením `Engine = Engine.Gpu` říkáme Aspose, aby použil grafickou kartu místo CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Proč GPU?** GPU může zpracovávat tisíce pixelů paralelně, čímž zkrátí dobu OCR z několika sekund na zlomky sekundy u velkých, vysokého DPI obrázků.

## Krok 3 – Načtení obrázku pro OCR (load image for ocr)

Správné načtení obrázku je důležitější, než si možná myslíte. `OcrImage.FromFile` podporuje PNG, JPEG, BMP, TIFF a dokonce i PDF stránky. Také načte DPI obrázku, což ovlivňuje přesnost.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Poznámka:** Pokud pracujete s PDF, můžete extrahovat každou stránku jako `OcrImage` a předávat je po jedné.

## Krok 4 – Rozpoznání textu z obrázku (recognize text from image)

Nyní se děje magie. Požádáme engine, aby rozpoznal anglický text, ale můžete zadat jakýkoli jazyk podporovaný Aspose (španělština, němčina, čínština atd.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

Vlastnost `result.Text` obsahuje prostý řetězec. Pokud potřebujete skóre důvěry pro každé slovo, můžete prozkoumat `result.Regions`.

### Očekávaný výstup

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Pokud je obrázek rozmazaný, můžete vidět poškozené znaky — zde pomáhá předzpracování ze Krok 3.

## Krok 5 – Extrahování textu z faktury – Reálný příklad

Řekněme, že máte složku plnou naskenovaných faktur a chcete získat celkovou částku. Níže je rychlé rozšíření předchozího kódu, které používá jednoduchý regulární výraz.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Po vytištění výsledku OCR byste zavolali `ExtractTotalAmount(result.Text);`. To ukazuje, jak snadné je **extrahovat text z faktury** souborů, jakmile máte surový řetězec.

## Krok 6 – Hromadné převádění obrázku na text (convert image to text)

Zpracování jedné souboru je v pořádku pro ukázku, ale produkční kód často potřebuje zvládnout desítky nebo stovky obrázků. Zde je stručná smyčka, která zpracuje celý adresář:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Spuštěním `ProcessFolder(ocrEngine, @"C:\Invoices")` **převodí obrázek na text** pro každý podporovaný soubor ve složce, využívajíc GPU pro rychlost.

## Okrajové případy a běžné úskalí

| Situace | Proč k tomu dochází | Rychlé řešení |
|-----------|----------------|-----------|
| **Snímek s nízkým kontrastem** | OCR má potíže rozlišit popředí od pozadí. | Zvyšte kontrast (`ImagePreprocessor.AdjustContrast`) nebo použijte adaptivní prahování. |
| **Více‑stránkový PDF** | `OcrImage.FromFile` načte pouze první stránku. | Použijte `PdfDocument` k extrakci každé stránky jako `OcrImage` a iterujte. |
| **Nepodporovaný jazyk** | Výchozí nastavený jazyk je angličtina. | Předávejte `Language.Spanish` nebo jakoukoli podporovanou hodnotu enumu. |
| **GPU nebyla detekována** | Chybějící nativní binárky nebo zastaralý ovladač. | Ověřte, že je ovladač GPU aktuální; přeinstalujte NuGet balíček s příznakem `-runtime`. |
| **Nedostatek paměti u obrovských obrázků** | Paměť GPU je omezená. | Zmenšete rozlišení obrázku (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do nové konzolové aplikace. Obsahuje všechny pomocné metody zmíněné výše.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}