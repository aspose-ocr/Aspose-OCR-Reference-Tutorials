---
category: general
date: 2026-01-13
description: Naučte se, jak rychle rozpoznávat text z obrázku a extrahovat text z
  účtenky pomocí Aspose OCR. Zahrnuje kroky načtení obrázku pro OCR a nastavení ID
  GPU zařízení.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: cs
og_description: Rozpoznávejte text z obrázku okamžitě pomocí Aspose OCR. Postupujte
  podle tohoto krok‑za‑krokem průvodce, načtěte obrázek pro OCR, nastavte ID GPU zařízení
  a extrahujte text z účtenky.
og_title: Rozpoznat text z obrázku – kompletní průvodce C# s GPU akcelerací
tags:
- Aspose OCR
- C#
- GPU computing
title: Rozpoznat text z obrázku pomocí Aspose OCR – GPU‑akcelerovaný C# tutoriál
url: /cs/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznat text z obrázku – Kompletní průvodce s GPU‑akcelerovaným C# Guide

Už jste někdy potřebovali **recognize text from image**, ale CPU verze byla bolestivě pomalá? Možná se snažíte **extract text from receipt** soubory a latence zabíjí uživatelský zážitek. Dobrou zprávou je, že se nemusíte spokojit s pomalým výkonem — GPU balíček Aspose OCR může proces zrychlit a kód má jen několik řádků.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje, jak **load image for OCR**, nakonfigurovat GPU pomocí **set GPU device ID**, a nakonec získat výsledek v prostém textu. Na konci budete mít připravený úryvek, který funguje na jakémkoli moderním Windows nebo Linux stroji s podporovanou NVIDIA kartou.

---

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.7.2+) – API funguje s oběma.
- **Aspose.OCR** NuGet balíček **plus** **Aspose.OCR.Gpu** add‑on.
- NVIDIA GPU s alespoň 2 GB VRAM (demo omezuje využití na 1 GB).
- Ukázkový obrázek, např. naskenovaný doklad (`receipt.jpg`).

Pokud již máte projekt, stačí spustit `dotnet add package Aspose.OCR` a `dotnet add package Aspose.OCR.Gpu`. Žádné další nativní knihovny nejsou potřeba; SDK obsahuje potřebné CUDA binární soubory.

---

## Krok‑za‑krokem implementace

### ## Jak rozpoznat text z obrázku pomocí Aspose OCR a GPU

Níže je **complete, self‑contained program**. Zkopírujte a vložte jej do nového konzolového projektu a stiskněte `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** Pokud má váš počítač více GPU, změňte `DeviceId` na `1`, `2` atd., abyste vybrali méně vytíženou kartu. SDK vyhodí jasnou `GpuDeviceNotFoundException`, pokud je ID mimo rozsah.

### ### Krok 1: Načíst obrázek pro OCR

`OcrImage.FromFile` dělá více než jen načíst bitmapu — předzpracovává obrázek (odklonění, binarizaci) na základě interních heuristik. Proto je **load image for OCR** samostatným krokem: můžete použít `MemoryStream`, pokud je váš obrázek uložen v databázi.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Pokud potřebujete **recognize text from image**, který je již v paměti:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Krok 2: Nastavit GPU device ID a limity paměti

GPU zdroje jsou omezené. Exponováním `DeviceId` a `MaxMemoryMb` umožňuje Aspose bezpečně **set GPU device ID**, čímž zabraňuje jednomu procesu přetížit celou kartu.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Pokud překročíte limit paměti, engine automaticky přenese data do systémové RAM, což je pomalejší, ale zabraňuje pádům.

### ### Krok 3: Extrahovat text z dokladu (recognize text from image)

Metoda `Recognize` vykonává těžkou práci. Můžete předat jakýkoli jazyk podporovaný Aspose OCR; pro doklady angličtina funguje většinou, ale můžete také přidat `OcrLanguage.Spanish` nebo vlastní jazykový balíček.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Očekávaný výstup** (ukázka):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Běžné varianty a okrajové případy

| Situace | Co změnit | Proč |
|-----------|----------------|-----|
| **Více dokladů na jednom obrázku** | Zavolejte `ocrEngine.Recognize` na každém oříznutém regionu (použijte `OcrImage.Crop`) | Zvyšuje přesnost, protože engine vidí menší, čistší oblast. |
| **Nízké rozlišení skenů (<150 dpi)** | Předzvětšete pomocí `receiptImage.Resize(2.0)` před rozpoznáním | Vyšší hustota pixelů poskytuje GPU více dat ke zpracování. |
| **Neanglické doklady** | Předávejte `OcrLanguage.French` (nebo vlastní `.traineddata`) | Jazykově specifické modely snižují falešně pozitivní výsledky. |
| **GPU není k dispozici** | Přepněte na `OcrEngine` (CPU) uvnitř try‑catch bloku | Zaručuje, že aplikace stále funguje na serverech bez grafického rozhraní. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Tipy pro produkční OCR

- **Batch processing:** Zabalte smyčku rozpoznávání do `Parallel.ForEach`, ale omezte stupeň paralelismu na počet GPU streamů, které můžete alokovat (obvykle 1‑2 na kartu).
- **Memory hygiene:** Okamžitě uvolňujte objekty `OcrImage` (`receiptImage.Dispose()`), zejména při zpracování tisíců dokladů.
- **Logging:** Zachyťte `ocrResult.Confidence` pro každý řádek; nízká důvěra může spustit manuální revizní workflow.
- **Security:** Při práci s citlivými doklady zajistěte, aby soubory obrázků byly uloženy v šifrovaných dočasných složkách a po zpracování vymazány.

---

## Závěr

Nyní máte **complete, runnable example**, který ukazuje, jak **recognize text from image** s GPU akcelerací Aspose OCR, **load image for OCR**, **set GPU device ID**, a nakonec **extract text from receipt** v několika stručných krocích. Kód je připravený ke zkopírování a vysvětlení vám poskytují dostatek kontextu pro přizpůsobení více jazykům, více GPU nebo scénářům s vysokou propustností.

Jste připraveni na další výzvu? Zkuste posílat živý video stream do `GpuOcrEngine` pro real‑time skenování dokladů, nebo integrujte výsledek do účetního API. Možnosti jsou neomezené, když spojíte rychlé GPU OCR s čistým C# designem.

*Šťastné programování a ať je vaše OCR vždy rychlé!*

![ukázkový screenshot rozpoznání textu z obrázku](placeholder-image.png "příklad rozpoznání textu z obrázku")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}