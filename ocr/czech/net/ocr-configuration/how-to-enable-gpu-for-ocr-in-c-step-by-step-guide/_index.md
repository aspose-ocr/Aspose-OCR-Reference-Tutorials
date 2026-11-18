---
category: general
date: 2026-04-04
description: Jak rychle povolit GPU v Aspose OCR. Naučte se extrahovat text z obrázku,
  načíst obrázek pro OCR a rozpoznat text pomocí C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: cs
og_description: Jak rychle povolit GPU v Aspose OCR. Postupujte podle tohoto tutoriálu
  pro extrakci textu z obrázku, načtení obrázku pro OCR a rozpoznání textu pomocí
  C#.
og_title: Jak povolit GPU pro OCR v C# – Kompletní průvodce
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Jak povolit GPU pro OCR v C# – krok za krokem průvodce
url: /cs/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit GPU pro OCR v C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak povolit GPU** při používání Aspose OCR? Možná jste narazili na výkonnostní limit při zpracování stovek účtenek a CPU už nestačí. Dobrou zprávou je, že zapnutí akcelerace GPU je hračka a jakmile je zapnutá, uvidíte, jak OCR engine projíždí obrázky jako drak.

V tomto tutoriálu nejen přepneme přepínač GPU, ale také vám ukážeme, jak **načíst obrázek pro OCR**, **rozpoznat text** a nakonec **extrahovat text z obrázku** pomocí čistého C# příkladu. Na konci budete mít připravený program, který vytáhne prostý text z libovolného podporovaného obrázku – bez potřeby externích služeb.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.7.2 a novější).  
- Aspose.OCR pro .NET, verze 24.2.0 nebo novější (vlajka GPU byla přidána v tomto vydání).  
- Počítač s podporou GPU a odpovídajícími ovladači (NVIDIA CUDA 11+ funguje skvěle).  
- Soubor s obrázkem, který chcete zpracovat – například naskenovaná účtenka, vyfocená faktura nebo ručně psaná poznámka.

Pokud je už máte, skvělé — pojďme na to.

## Krok 1: Jak povolit GPU – Konfigurace OCR enginu

První věc, kterou musíte udělat, je říct Aspose OCR, aby používalo GPU. To se provede nastavením vlastnosti `UseGpu` na instanci `OcrEngine`. Výchozí hodnota je `false`, takže ji explicitně zapneme.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Proč je to důležité:** Když je `UseGpu` nastaveno na `true`, knihovna přesune těžké maticové výpočty na grafický procesor. Na skromné RTX 3060 si všimnete poklesu latence z několika sekund na obrázek na zlomek sekundy.

> **Pro tip:** Pokud běžíte v headless CI prostředí, ujistěte se, že je nainstalován GPU driver a že má servisní účet oprávnění přistupovat k zařízení. Jinak engine tiše přejde do režimu CPU.

## Krok 2: Načíst obrázek pro OCR – Nasměrujte engine na váš soubor

Dále potřebujeme **načíst obrázek pro OCR**. Aspose OCR přijímá jakýkoli formát obrázku podporovaný System.Drawing (PNG, JPEG, BMP, TIFF, atd.). Pomocná metoda `ImageStream.FromFile` zabalí soubor do požadovaného stream objektu.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Pokud raději načítáte z `byte[]` (například když obrázek pochází z databáze), můžete místo toho použít `ImageStream.FromBytes(byteArray)` — stejný výsledek, jen jiný zdroj.

## Krok 3: Jak rozpoznat text – Spusťte OCR proces

Nyní, když je engine nakonfigurován a obrázek načten, je čas **rozpoznat text**. Metoda `Recognize` udělá veškerou těžkou práci a vrátí objekt `OcrResult`, který obsahuje prostý text, skóre spolehlivosti a dokonce i ohraničující rámečky, pokud je budete potřebovat později.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Můžete také změnit jazyk nastavením `ocrEngine.Language = OcrLanguage.French;` před voláním `Recognize()`. GPU akcelerace funguje bez ohledu na jazykový balíček, který načtete.

## Krok 4: Jak extrahovat text z obrázku – Výstup výsledku

Nakonec **extrahujeme text z obrázku** čtením vlastnosti `Text` objektu výsledku. Pro demonstrační účely jej jen vypíšeme do konzole, ale můžete jej zapsat do souboru, databáze nebo předat dalšímu servisu.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Očekávaný výstup** (váš skutečný text se bude lišit podle obrázku):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Pokud potřebujete surové hodnoty spolehlivosti, můžete iterovat `ocrResult.Regions` a zkontrolovat každou `Region.Confidence`.

## Kompletní funkční příklad – Jeden soubor, připravený ke spuštění

Níže je kompletní program. Zkopírujte jej do nového konzolového projektu, obnovte NuGet balíček Aspose.OCR a stiskněte **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Poznámka:** Nahraďte `YOUR_DIRECTORY/receipt.jpg` skutečnou cestou k vašemu obrázku. Pokud program vyhodí `FileNotFoundException`, zkontrolujte cestu a oprávnění k souboru.

## Časté otázky a okrajové případy

### Co když GPU není detekováno?

Aspose OCR se automaticky vrátí do režimu CPU a zapíše varování. Pro ověření, který režim je aktivní, zkontrolujte `ocrEngine.IsGpuEnabled` po vytvoření — vrací `true` pouze když je GPU driver úspěšně načten.

### Můžu zpracovávat více obrázků v cyklu?

Určitě. Stačí přesunout řádek `ocrEngine.Image = …` dovnitř smyčky `foreach (var file in files)`. Používejte stejnou instanci `OcrEngine`; opětovné použití eliminuje režii spojenou s opakovaným alokováním GPU zdrojů.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Jak zacházet s neanglickými jazyky?

Nastavte jazyk před voláním `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

GPU akcelerace funguje stejně; mění se jen jazykový model.

### Co s velkými, vysokorozlišovacími fotografiemi?

Pokud narazíte na chyby nedostatku paměti, nejprve zmenšete rozlišení obrázku. Aspose OCR poskytuje `ImageHelper.Resize` — rychlý způsob, jak zmenšit obrázek bez výrazné ztráty detailů.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Závěr

Probrali jsme **jak povolit GPU** pro Aspose OCR, ukázali vám, jak **načíst obrázek pro OCR**, prošli **jak rozpoznat text** a demonstrovali **jak extrahovat text z obrázku** pomocí stručného, připraveného C# programu pro produkci. Přepnutím příznaku `UseGpu` získáte znatelný nárůst rychlosti, zejména při zpracování dávky účtenek, faktur nebo jakéhokoli vysokokapacitního dokumentového proudu.

Jste připraveni na další krok? Zkuste propojit tento OCR pipeline s databází pro ukládání extrahovaných účtenek, nebo předat prostý text do modelu zpracování přirozeného jazyka pro kategorizaci výdajů. Můžete také prozkoumat kolekci `OcrResult.Regions` a získat souřadnice ohraničujících rámečků a vytvořit UI, které zvýrazní každé slovo na původním obrázku.

Šťastné programování a užijte si extra výkon, který GPU akcelerace přináší vašim OCR úlohám! 

---

![ilustrace jak povolit GPU](gpu-ocr-diagram.png "ilustrace jak povolit GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}