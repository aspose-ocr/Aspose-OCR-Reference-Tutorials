---
category: general
date: 2026-04-01
description: Naučte se rychle rozpoznávat text z PNG souborů nastavením ID GPU zařízení
  a povolením GPU akcelerace v Aspose OCR. Krok za krokem průvodce v C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: cs
og_description: Rozpoznávejte text z PNG souborů rychle nastavením ID GPU zařízení.
  Postupujte podle tohoto kompletního průvodce v C#, který umožňuje akceleraci GPU
  pomocí Aspose OCR.
og_title: Rozpoznat text z PNG – GPU‑akcelerovaný tutoriál Aspose OCR
tags:
- C#
- OCR
- GPU
- Aspose
title: Rozpoznat text z PNG pomocí Aspose OCR – GPU‑akcelerovaná dávková ukázka
url: /cs/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznat text z png – Kompletní C# GPU‑akcelerovaný dávkový tutoriál

Už jste někdy potřebovali **rozpoznat text z png** obrázků, ale proces byl bolestivě pomalý? Nejste v tom sami. Většina vývojářů začíná jednoduchým voláním OCR a pak zírá na konzoli, která se táhne jako šnek, když složka obsahuje desítky snímků obrazovky.  

Dobrá zpráva? Aspose OCR může přenést těžkou práci na vaši grafickou kartu a pomocí několika řádků můžete **nastavit id GPU zařízení** a vybrat přesně tu GPU, kterou chcete. V tomto průvodci projdeme kompletním, spustitelným příkladem, který načte všechny PNG ze složky, zapne GPU akceleraci, vybere první GPU a vypíše počet znaků pro každý soubor.

Na konci budete mít samostatný program, který můžete vložit do libovolného .NET projektu, a pochopíte, proč je zapnutí GPU důležité, jak zacházet s okrajovými případy a co vyladit pro ještě lepší výkon.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód se také kompiluje s .NET Core).  
- Balíček **Aspose.OCR** NuGet – nainstalujte jej pomocí `dotnet add package Aspose.OCR`.  
- Počítač s CUDA‑kompatibilní GPU (typicky NVIDIA) a odpovídajícím ovladačem.  
- Složka plná **PNG** obrázků, které chcete zpracovat.  

Pokud vám některá z těchto věcí není známá, nepanikařte. Níže uvedené kroky obsahují přesné příkazy, které potřebujete, a také se podíváme na to, co dělat, když GPU není k dispozici.

## Krok 1: Inicializace OCR enginu a zapnutí GPU akcelerace  

První věc, kterou musíte udělat, je vytvořit instanci `OcrEngine` a zapnout podporu GPU. Toto nastavení říká Aspose, aby pod kapotou používal nativní knihovny CUDA.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Proč je to důležité:** Bez `UseGpuAcceleration` je každý obrázek zpracováván na CPU, což může být řádově pomalejší, zejména u vysokého rozlišení PNG. Zapnutí tohoto nastavení také připraví engine na přijetí konkrétního GPU zařízení později.

## Krok 2: Nastavení ID GPU zařízení (volitelné, ale doporučené)  

Pokud má vaše pracovní stanice více než jedno GPU, můžete si vybrat, které použijete. ID zařízení začínají na **0**, takže `0` vybere první GPU, `1` druhou a tak dále.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Tip:** Při běhu na sdíleném serveru může explicitní nastavení ID GPU zařízení zabránit vašemu úkolu v kradení prostředků od jiných procesů. Pokud tento řádek vynecháte, Aspose vybere výchozí zařízení, což je obvykle v pořádku pro jednosložkové GPU nastavení.

## Krok 3: Shromáždění všech PNG souborů z vaší dávkové složky  

Dále potřebujeme najít každé PNG, na kterém chcete spustit OCR. Metoda `Directory.GetFiles` vykoná těžkou práci.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Okrajový případ:** Pokud je složka prázdná, `imageFiles` bude prázdné pole. Později to ošetříme přátelskou zprávou.

## Krok 4: Zpracování každého obrázku a výpis rozpoznaného počtu znaků  

Nyní hlavní smyčka. Pro každé PNG zavoláme `Recognize` a poté vypíšeme název souboru a délku extrahovaného textu.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Co uvidíte:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Pokud obrázek neobsahuje žádný text, počet bude `0`. To je naprosto normální pro snímky obrazovky, které jsou čistě grafické.

## Krok 5: Spuštění programu a ověření využití GPU  

Zkompilujte soubor (`dotnet build`) a spusťte jej (`dotnet run`). Během posouvání konzole můžete otevřít nástroj pro sledování GPU (např. NVIDIA Smi), abyste viděli krátký nárůst využití GPU pro každý obrázek. Pokud žádnou aktivitu nevidíte, zkontrolujte:

1. Ovladač CUDA je nainstalován.  
2. `UseGpuAcceleration` je nastaven na `true`.  
3. Správné `GpuDeviceId` odpovídá fyzickému GPU.

Pokud GPU není k dispozici, Aspose automaticky přejde na CPU, ale ztratíte tak výhodu rychlosti.

## Běžné varianty a tipy  

| Situace | Co změnit |
|-----------|----------------|
| **Jiný formát obrázku** (např. JPEG) | Změňte vzor hledání na `*.jpg` nebo `*.*` a Aspose stále rozpozná text. |
| **Velikost dávky je obrovská** (tisíce souborů) | Zpracovávejte po částech, abyste se vyhnuli tlaku na paměť: rozdělte `imageFiles` na menší pole. |
| **Potřebujete skutečný text, ne jen délku** | Nahraďte `ocrResult.Text.Length` v `WriteLine` za `ocrResult.Text`. |
| **Běh na serveru bez grafického rozhraní** | Ujistěte se, že server má GPU ovladač; jinak nastavte `UseGpuAcceleration = false`, aby se předešlo zbytečným chybám. |
| **Více GPU, chcete vyvážit zátěž** | V cyklu `foreach` nastavujte `ocrEngine.GpuDeviceId = i % gpuCount`, aby se zařízení otáčela. |

## Očekávaný výstup a ověření  

Když vše funguje, konzole vypíše název každého souboru následovaný počtem znaků, jak bylo ukázáno dříve. Pro dvojitou kontrolu skutečného OCR výstupu můžete dočasně vypsat text:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Jen si pamatujte, že pro velké dávky je třeba tento řádek odstranit nebo zakomentovat; tisk tisíců řádků může zaplavit váš terminál.

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Uložte tento soubor jako `GpuBatchDemo.cs`, spusťte `dotnet add package Aspose.OCR` a poté `dotnet run`. Měli byste vidět, že počty znaků se objeví téměř okamžitě pro každé PNG, díky GPU akceleraci.

## Závěr  

Nyní víte, jak **rozpoznat text z png** souborů efektivně tím, že zapnete GPU akceleraci a explicitně **nastavíte id GPU zařízení** v Aspose OCR. Kompletní program připravený ke kopírování zvládá vyhledávání složek, kontrolu okrajových případů a poskytuje okamžitou zpětnou vazbu o výkonu OCR.

Další kroky? Zkuste nahradit volání `Recognize` za `ocrEngine.RecognizeAsync`, pokud potřebujete neblokující zpracování, nebo experimentujte s různými možnostmi předzpracování obrázků (např. binarizace), které Aspose poskytuje. Můžete také přesměrovat výsledky OCR do databáze nebo vyhledávacího indexu pro řešení full‑textového vyhledávání.

Máte otázky ohledně zpracování více‑stránkových PDF, nebo chcete porovnat Aspose OCR s Tesseract? Zanechte komentář nebo prozkoumejte naše další tutoriály o **batch OCR C#**, **tipy na výkon OCR** a **GPU‑řízeném zpracování obrázků**. Šťastné kódování!  

![Výstup konzole zobrazující rozpoznané počty znaků pro PNG soubory – rozpoznat text z png pomocí GPU akcelerace](image-placeholder.png "příklad výstupu rozpoznání textu z png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}