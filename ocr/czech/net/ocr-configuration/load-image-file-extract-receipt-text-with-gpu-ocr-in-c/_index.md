---
category: general
date: 2026-02-14
description: Načtěte soubor s obrázkem a extrahujte text z účtenky pomocí Aspose OCR
  GPU enginu. Naučte se nastavit maximální paměť GPU, konfigurovat paměť GPU a efektivně
  spustit OCR na obrázku.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: cs
og_description: Načtěte soubor s obrázkem a extrahujte text z účtenky pomocí Aspose
  OCR GPU engine. Tento návod ukazuje, jak nastavit maximální paměť GPU a spustit
  OCR na obrázku v C#.
og_title: Načíst soubor obrázku a extrahovat text účtenky pomocí GPU OCR v C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Načíst soubor obrázku a extrahovat text z účtenky pomocí GPU OCR v C#
url: /cs/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení souboru obrázku a extrakce textu z účtenky pomocí GPU OCR v C#

Už jste někdy potřebovali **load image file** a získat přesný text z účtenky, ale uvízli jste v kroku OCR? Nejste jediní. V mnoha reálných aplikacích—sledovačích výdajů, inventárních systémech nebo dokonce jednoduchých botách pro skenování účtenek—může schopnost rychle přečíst obrázek účtenky změnit hru.  

Dobrá zpráva? S GPU‑akcelerovaným enginem Aspose.OCR můžete **load image file**, **set max GPU memory** a **run OCR on image** vše v několika úhledných řádcích C#. Níže projdeme celý proces, od konfigurace GPU až po výpis extrahovaného prostého textu.

## Co se naučíte

V tomto tutoriálu se dozvíte, jak:

* **Load image file** z disku pomocí `ImageStream` od Aspose.
* **Configure GPU memory**, aby engine nikdy nevyčerpával více RAM, než povolíte.
* **Run OCR on image** a získat každý znak na účtence.
* Řešit běžné úskalí—např. chyby out‑of‑memory nebo rozmazané skeny.
* Ověřit výstup a doladit nastavení pro lepší přesnost.

Žádné externí služby, žádné nejasné triky—pouze čistý C# kód, který můžete vložit do libovolného projektu .NET 6+.

---

## Požadavky

Než se ponoříme, ujistěte se, že máte:

* .NET 6 SDK nebo novější nainstalovaný.
* Platnou licenci Aspose.OCR (nebo můžete použít režim bezplatného hodnocení).
* NuGet balíčky `Aspose.OCR` a `Aspose.OCR.Gpu` přidané do vašeho projektu.
* Vzorek obrázku účtenky (`receipt.png`) připravený na disku.

Pokud vám některý z nich není znám, zastavte se na chvíli a nainstalujte balíčky:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

A to je vše—žádné další nativní knihovny nejsou potřeba, protože podpora GPU je zabudována přímo v NuGet balíčku.

---

## Načtení souboru obrázku a příprava GPU enginu

První věc, kterou musíte udělat, je **load image file** do `ImageStream`. Tento objekt abstrahuje detaily souborového systému a poskytuje OCR engine čistou, paměťovou reprezentaci.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Proč je to důležité:**  
*Loading the image file* pomocí `ImageStream.FromFile` zaručuje, že engine vidí přesná pixelová data, zachovává DPI a barevnou hloubku. Přeskočení tohoto kroku nebo předání poškozeného streamu způsobí, že OCR vynechá znaky nebo vyhodí výjimky.

> **Pro tip:** Pokud pracujete s uživatelsky nahrávanými soubory, zabalte volání `FromFile` do try‑catch bloku a nejprve ověřte velikost souboru. Velké obrázky mohou zaplnit GPU paměť, pokud jste **configured GPU memory** správně.

---

## Nastavení maximální GPU paměti pro optimální výkon

GPU zdroje jsou cenné, zejména na sdílených serverech nebo laptopech s omezenou VRAM. Vlastnost `MaxDeviceMemory` říká Aspose, kolik paměti GPU může bezpečně alokovat.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Když **set max GPU memory**, engine se automaticky vrátí k CPU zpracování, pokud nemůže požadavek splnit—zabrání to pádům. Toto je nejbezpečnější způsob, jak **configure GPU memory** bez pevného kódování zařízení‑specifických limitů.

**Kdy upravit:**  
* Pokud během těžkého dávkového zpracování zaznamenáte `OutOfMemoryException`, snižte limit.  
* Pokud jsou vaše účtenky vysokého rozlišení (300 DPI+), zvyšte ho na 2 GB pro udržení vysoké rychlosti.

---

## Spuštění OCR na obrázku pro extrakci textu z účtenky

Nyní zábavná část—skutečně **run OCR on image** a získat text z účtenky. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje vlastnost `Text` s výstupem prostého textu.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

The console will display something like:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Proč to funguje:**  
GPU engine spouští model deep‑learning, který byl trénován na různých rozvrženích dokumentů. Poskytnutím čistého, správně načteného obrázku dáváte modelu nejlepší šanci **extract text from receipt** přesně.

---

## Ověření výstupu a běžné úskalí

I přes výkonný engine není OCR kouzlo. Zde je několik věcí, na které si dát pozor:

| Issue | Cause | Fix |
|-------|-------|-----|
| Zkreslené znaky | Nízký kontrast nebo rozmazaný obrázek | Předzpracujte pomocí `ImageProcessor` od Aspose pro zvýšení kontrastu |
| Chybějící řádky | Obrázek oříznutý příliš těsně | Zajistěte, aby účtenka plně zapadala do hran obrázku |
| Chyby out‑of‑memory | `MaxDeviceMemory` příliš nízká pro velikost obrázku | Zvyšte `MaxDeviceMemory` nebo nejprve zmenšete obrázek |
| Špatný jazyk | Účtenka obsahuje text v jiném jazyce než angličtině | Nastavte `gpuEngine.Language = OcrLanguage.Spanish;` (nebo vhodný) |

Pokud narazíte na některý z nich, rychlým řešením je změnit velikost obrázku na méně než 2000 px na nejdelší straně—tím výrazně snížíte zatížení GPU, aniž byste obětovali čitelnost většiny účtenek.

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, připravený ke kompilaci. Nahraďte cestu k souboru vlastní umístěním účtenky.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Očekávaný výstup v konzoli** (vaše účtenka se samozřejmě liší):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Spusťte program pomocí `dotnet run`. Pokud se text vytiskne, gratulujeme—úspěšně jste **load image file**, **set max GPU memory** a **run OCR on image** k **extract text from receipt**.

---

## Často kladené otázky

**Q: Funguje to na strojích bez dedikovaného GPU?**  
A: Ano. Aspose.OCR se elegantně vrátí do CPU režimu, pokud není detekováno kompatibilní GPU. Stále budete moci **load image file** a **run OCR on image**, jen o něco pomaleji.

**Q: Můžu zpracovávat více účtenek najednou?**  
A: Rozhodně. Zabalte kód rozpoznávání do `foreach` smyčky, ale pamatujte na opětovné použití stejné instance `GpuEngine`—tím se vyhnete opětovné inicializaci GPU zdrojů pro každý soubor.

**Q: Co když je moje účtenka v jiném jazyce než angličtina?**  
A: Nastavte jazyk před voláním `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

Engine pak použije odpovídající znakovou sadu.

---

## Další kroky a související témata

Nyní, když ovládáte základy, zvažte prozkoumání:

* **Fine‑tuning OCR accuracy** – experimentujte s `gpuEngine.RecognitionOptions` jako `EnableDeskew` nebo `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}