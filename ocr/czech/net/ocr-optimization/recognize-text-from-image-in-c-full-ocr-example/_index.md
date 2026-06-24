---
category: general
date: 2026-06-22
description: Rozpoznávejte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak automaticky
  vyrovnat obrázek, předzpracovat jej pro OCR a povolit automatické vyrovnání v stručném
  příkladu OCR v C#.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: cs
og_description: Rozpoznávejte text z obrázku pomocí Aspose OCR v C#. Tento průvodce
  ukazuje, jak automaticky vyrovnat obrázek, předzpracovat jej pro OCR a povolit automatické
  vyrovnání v praktickém příkladu OCR v C#.
og_title: Rozpoznat text z obrázku v C# – kompletní příklad OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Rozpoznání textu z obrázku v C# – kompletní příklad OCR
url: /cs/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku v C# – Kompletní příklad OCR

Už jste se někdy zamýšleli, jak **rozpoznat text z obrázku** v C# aplikaci, aniž byste si trhali vlasy nad rozmazanými skeny? Nejste v tom sami. Ať už digitalizujete účtenky, extrahujete data z formulářů, nebo si jen hrajete s AI‑poháněnými triky na obrázky, získání čistých OCR výsledků závisí na správném předzpracování – například automatickém narovnání obrazu a redukci šumu.  

V tomto tutoriálu projdeme **c# ocr example**, který používá knihovnu Aspose.OCR k **povolení automatického narovnání**, automatickému vyrovnání šikmých fotografií a **předzpracování obrazu pro OCR** během několika řádků kódu. Na konci budete mít spustitelný program, který vytiskne rozpoznaný text přímo do konzole.

## What You’ll Learn

- Jak nainstalovat a odkazovat na NuGet balíček Aspose.OCR.  
- Nastavení `OcrEngine` s podporou anglického jazyka.  
- Povolení **auto deskew image** a dalších možností předzpracování v jednom kroku.  
- Spuštění enginu na reálné fotografii a zpracování výstupu.  
- Tipy pro řešení okrajových případů, jako jsou silně natočené obrázky nebo snímky s nízkým kontrastem.

> **Prerequisites** – Potřebujete .NET 6 (nebo novější) a základní znalosti C#. Předchozí zkušenosti s OCR nejsou vyžadovány.

---

## ## Recognize Text from Image – Install the Aspose.OCR Package

Než napíšeme jakýkoli kód, je třeba knihovnu přidat do projektu. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package Aspose.OCR
```

Tento příkaz stáhne nejnovější stabilní verzi Aspose.OCR, která obsahuje OCR engine, jazykové balíčky a utilitu pro předzpracování, kterou budeme potřebovat.  

*Pro tip:* Pokud cílíte na .NET Framework místo .NET Core, použijte UI správce NuGet balíčků ve Visual Studiu – stačí vyhledat “Aspose.OCR” a kliknout **Install**.

---

## ## Recognize Text from Image – Initialize the OCR Engine

Nyní, když je balíček připraven, můžeme vytvořit engine. Prvním krokem je říct enginu, jaký jazyk očekává. Ve většině případů stačí angličtina, ale knihovna podporuje desítky jazyků přímo z krabice.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Proč je to důležité:**  
- `Language = OcrLanguage.English` říká enginu, jakou znakovou sadu použít, což dramaticky zvyšuje přesnost.  
- Vlastnost `Preprocessing` kombinuje dva příznaky – `AutoDeskew` a `Denoise`. Tento **auto deskew image** krok otočí obrázek zpět na horizontální základnu, zatímco `Denoise` odstraňuje zrnitý šum, který by jinak engine zmátl.  

Pokud předzpracování přeskočíte, často uvidíte zkomolený výstup na naskenovaných účtenkách nebo fotografiích pořízených pod úhlem.

---

## ## Recognize Text from Image – Feed the Image to the Engine

S připraveným enginem je dalším krokem předat mu soubor s obrázkem. Aspose.OCR přijímá cestu nebo `Stream`, takže můžete pracovat s lokálními soubory, vloženými zdroji nebo dokonce obrázky staženými z webu.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Poznámka k okrajovým případům:**  
- Pokud je obrázek **silně natočen** (> 45°), `AutoDeskew` se stále pokusí, ale možná budete chtít předem otočit obrázek ručně pomocí `System.Drawing` nebo `ImageSharp`, než jej předáte enginu.  
- Pro **vícestránkové PDF** zavolejte `engine.RecognizePdf`; stejné příznaky předzpracování se použijí.

---

## ## Recognize Text from Image – Output the Result

Nakonec zobrazíme extrahovaný text. Objekt `result` obsahuje nejen prostý text – nabízí také skóre důvěry, ohraničující rámečky a původní obrázek se zvýrazněnými oblastmi. Pro rychlou ukázku stačí vytisknout `result.Text`.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

Po spuštění programu byste měli vidět něco podobného:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Pokud výstup vypadá rozbitě, zkontrolujte, že zdrojový obrázek je čistý, dobře osvětlený a že **preprocess image for OCR** je skutečně povoleno (příznaky `Preprocessing` výše).

---

## ## Recognize Text from Image – Handling Common Pitfalls

### 1. Low Contrast or Dark Backgrounds
Aspose.OCR nabízí další příznak `PreprocessingOptions.ContrastEnhancement`. Přidejte jej do řádku `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Non‑English Documents
Vyměňte `OcrLanguage.English` za `OcrLanguage.Spanish`, `OcrLanguage.French` atd. Engine automaticky načte odpovídající jazykový model.

### 3. Large Images
Zpracování 5 MP fotografie může být náročné na paměť. Nejprve ji zmenšete:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Getting Bounding Boxes
Pokud potřebujete přesnou polohu každého slova (např. pro UI overlay), projděte `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## Recognize Text from Image – Full Working Example

Níže je **kompletní, připravený ke zkopírování** program, který zahrnuje všechny výše uvedené tipy. Uložte jej jako `Program.cs`, nahraďte `YOUR_DIRECTORY` složkou, kde máte testovací obrázek, a spusťte `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Očekávaný výstup v konzoli** (při předpokladu, že obrázek obsahuje jednoduchou účtenku):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Pokud se text vytiskne čistě, gratulujeme – úspěšně jste **rozpoznali text z obrázku** s automatickým narovnáním a předzpracováním!

---

## ## Recognize Text from Image – Next Steps & Related Topics

- **Dávkové zpracování:** Zabalte volání enginu do `foreach` smyčky, abyste zvládli desítky fotografií najednou.  
- **Konverze PDF:** Použijte `engine.RecognizePdf` pro vícestránkové dokumenty a poté sloučte výsledky.  
- **Vlastní slovníky:** Předejte seznam slov do `engine.CustomWords` pro zvýšení přesnosti u specifické terminologie (např. lékařské kódy).  
- **Ladění výkonu:** Cacheujte instanci `OcrEngine`, pokud zpracováváte mnoho obrázků; vytvoření enginu je nejdražší operace.  

Tyto rozšíření přirozeně využívají stejné koncepty – **preprocess image for OCR**, **enable auto deskew**, a **recognize text from image** – takže můžete znovu použít vzory kódu, které jste se právě naučili.

---

## Conclusion

Právě jsme prošli **c# ocr example**, který ukazuje, jak **rozpoznat text z obrázku** pomocí Aspose.OCR, přičemž automaticky narovná a odfiltruje šum. Povolením `AutoDeskew` (funkce **auto deskew image**) a přidáním několika příznaků předzpracování dramaticky zvýšíte spolehlivost OCR, aniž byste museli psát jediný řádek kódu pro manipulaci s obrázkem.

Nyní můžete tento kostra použít, vložit své vlastní obrázky a začít extrahovat data z faktur, ID nebo jakýchkoli jiných dokumentů, které jsou na papíře. Máte obtížný sken? Vyzkoušejte další předzpracovací možnosti, které jsme zmínili, nebo experimentujte s vlastními jazykovými balíčky. Možnosti jsou neomezené.

Pokud vám tento průvodce pomohl, zanechte komentář, podělte se o své výsledky nebo mě kontaktujte na GitHubu – šťastné kódování!

## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}