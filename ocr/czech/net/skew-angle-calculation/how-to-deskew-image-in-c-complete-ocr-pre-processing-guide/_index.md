---
category: general
date: 2026-01-10
description: Jak vyrovnat obrázek a zlepšit výsledky OCR pomocí Aspose.OCR. Naučte
  se předzpracovat obrázek pro OCR, odstranit šum ze skenu a rozpoznat text ze skenu.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: cs
og_description: Jak vyrovnat sklon obrazu a zvýšit přesnost OCR. Tento průvodce ukazuje,
  jak předzpracovat obrázek pro OCR, odstranit šum ze skenu a rozpoznat text ze skenu
  pomocí Aspose.OCR.
og_title: Jak narovnat obrázek v C# – Kompletní průvodce předzpracováním OCR
tags:
- OCR
- C#
- Image Processing
title: Jak vyrovnat sklon obrázku v C# – Kompletní průvodce předzpracováním OCR
url: /cs/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vyrovnat obrázek v C# – Kompletní průvodce předzpracováním OCR

Už jste se někdy zamýšleli **jak vyrovnat obrázek** před tím, než jej předáte OCR enginu? Nejste v tom jediní. Naskenované dokumenty jsou často nakřivo, šumivé nebo s nízkým kontrastem, což ztěžuje jakýkoli pokus o rozpoznání textu.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **předzpracovává obrázek pro OCR**, odstraňuje šum ze skenu a nakonec **rozpozná text ze skenu** pomocí knihovny Aspose.OCR. Na konci budete mít jasnou představu o **tom, jak používat OCR** v C#, a to s krátkým a přehledným kódem.

> **Tip:** I když je rotace malá (5‑10°), může snížit přesnost OCR o 30 % nebo více. Vyrovnání (deskew) je první krok, který byste nikdy neměli přeskočit.

---

## Co budete potřebovat

- **.NET 6+** (kód funguje i na .NET Framework, ale .NET 6 je aktuální LTS)
- **Aspose.OCR for .NET** – můžete jej získat z NuGet (`Install-Package Aspose.OCR`)
- Vzorek souboru TIFF/PNG/JPEG, který je natočený nebo šumivý (v příkladu použijeme `noisy_rotated.tif`)
- Jakékoliv IDE, které máte rádi – Visual Studio, Rider nebo VS Code bude stačit

To je vše. Žádné další knihovny, žádné externí služby.

---

## Krok 1 – Načtení zdrojového obrázku (Proč je to důležité)

Než budeme moci **vyrovnat obrázek**, musíme jej načíst do Aspose `ImageStream`. Tento objekt abstrahuje souborové I/O a poskytuje OCR enginu jednotné rozhraní.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Proč načíst nejprve?* Protože všechny následující filtry pracují s obrázkem v paměti. Pokud soubor nelze načíst, celý pipeline selže.

---

## Krok 2 – Vytvoření pipeline předzpracování (Deskew + Denoise + Contrast)

Robustní OCR workflow obvykle řetězí několik filtrů. Zde **předzpracováváme obrázek pro OCR** a, co je důležitější, **automaticky vyrovnáváme obrázek**.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Proč právě tyto tři?**  
- **DeskewFilter** automaticky řeší problém „jak vyrovnat obrázek“; nemusíte hádat úhel.  
- **DenoiseFilter** řeší požadavek „odstranit šum ze skenu“, který jinak vytváří fantomové znaky.  
- **ContrastBoostFilter** pomáhá OCR enginu rozlišovat tmavý text od světlého pozadí, což je klasický problém při *předzpracování obrázku pro OCR*.

---

## Krok 3 – Aplikace pipeline (Vidět transformaci)

Nyní skutečně spustíme filtry. Vrácený `processedImage` je to, co předáme OCR enginu.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Pokud otevřete `cleaned_output.tif`, měli byste si všimnout, že text je rovný, méně zrnitý a s vyšším kontrastem. Tato vizuální kontrola je užitečná, když *odstraňujete šum ze skenu* a chcete potvrdit, že vyrovnání (deskew) fungovalo.

---

## Krok 4 – Vytvoření a konfigurace OCR enginu (Jak používat OCR)

S čistým obrázkem v ruce vytvoříme instanci `OcrEngine`. To je jádro **jak používat OCR** s Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Proč nastavit `AutoPageSegmentation`?* Protože mnoho skenů obsahuje tabulky nebo více sloupců. Zapnutím umožníte enginu inteligentně rozdělit stránku, což zlepšuje konečný výsledek **rozpoznání textu ze skenu**.

---

## Krok 5 – Spuštění procesu rozpoznávání (Konečně rozpoznat text)

Nyní nastává okamžik pravdy: požádáme engine, aby přečetl text.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Pokud vše proběhne hladce, uvidíte čistý blok textu, který odpovídá původnímu dokumentu. To je odměna za správné **vyrovnání obrázku**, **odstranění šumu** a **předzpracování obrázku pro OCR**.

---

## Krok 6 – Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní program, připravený ke kompilaci. Stačí nahradit cestu k souboru a můžete spustit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Pokud výstup vypadá poškozeně, dvakrát zkontrolujte, že zdrojový obrázek není natočený více než 30°, nebo zvyšte `DeskewFilter.MaxAngle`.

---

## Často kladené otázky (okrajové případy a varianty)

| Question | Answer |
|----------|--------|
| **Co když je můj sken natočený o 45°?** | `DeskewFilter` omezuje na `MaxAngle`. Zvyšte ho (např. `MaxAngle = 60`) nebo předem otočte obrázek pomocí grafické knihovny, než jej předáte pipeline. |
| **Mohu zpracovávat PDF stránku po stránce?** | Ano. Převěďte každou stránku PDF na obrázek (např. pomocí `Aspose.Pdf`) a spusťte stejnou pipeline na každém bitmapu. |
| **Můj dokument je ve francouzštině – musím něco změnit?** | Nastavte `ocrEngine.Language = Language.French;` nebo načtěte vlastní jazykový balíček. Zbytek pipeline zůstává stejný. |
| **Je možné zachovat původní rozlišení?** | `PreprocessPipeline` pracuje s originálním bitmapem, zachovává DPI. Jen se vyhněte volání `ImageStream.Resize`, pokud nepotřebujete snížit rozlišení pro výkon. |
| **Jak ovlivňuje zesílení kontrastu barevné skeny?** | `ContrastBoostFilter` pracuje na každém kanálu; je bezpečný pro odstíny šedi i barevné obrázky, ale můžete také nejprve převést na odstíny šedi pomocí `new GrayscaleFilter()`. |

---

## Příklad obrázku (vizuální pomůcka)

![příklad, jak vyrovnat obrázek](/images/deskew-example.png)

*Obrázek ukazuje před/po 12° natočeném, šumivém skenu, který byl vyrovnán a vyčištěn.*

---

## Závěr

Probrali jsme **jak vyrovnat obrázek** pomocí Aspose.OCR, předvedli kompletní pipeline **předzpracování obrázku pro OCR**, ukázali **odstranění šumu ze skenu** a nakonec **rozpoznání textu ze skenu** pomocí několika řádků C#. Řetězením `DeskewFilter`, `DenoiseFilter` a `ContrastBoostFilter` získáte čistý bitmap, který umožní OCR enginu vykonat svou práci bez zakopnutí o artefakty.

Další kroky? Vyzkoušejte experimentovat s různými silami filtrů, přidejte `BinarizationFilter` pro čistý černobílý výstup, nebo předávejte vyčištěný obrázek do následného NLP pipeline. Stejný vzor funguje stejně pro účtenky, pasy i historické dokumenty.

Máte další otázky ohledně **jak používat OCR** v jiných jazycích nebo frameworkech? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}