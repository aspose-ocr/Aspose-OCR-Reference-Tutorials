---
category: general
date: 2026-01-02
description: Spusťte OCR na PNG rychle pomocí Aspose OCR a podpory GPU. Naučte se,
  jak rozpoznat text z obrázku, extrahovat text z obrázku a nastavit limit paměti
  GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: cs
og_description: Spusťte OCR na PNG efektivně pomocí Aspose OCR a akcelerace GPU. Tento
  tutoriál vám ukáže, jak rozpoznat text z obrázku, extrahovat text z obrázku a řídit
  využití paměti GPU.
og_title: Spusťte OCR na PNG s GPU – Kompletní průvodce C#
tags:
- OCR
- C#
- GPU
title: Spusťte OCR na PNG s GPU – kompletní průvodce C#
url: /cs/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# spuštění OCR na PNG s GPU – Kompletní průvodce v C#

Už jste někdy potřebovali **spustit OCR na PNG** souborech, ale uvízli jste na výkonnostní hranici? Nejste v tom sami. V mnoha reálných pipelinech může jediný vysoce rozlišený PNG zpomalit OCR engine běžící jen na CPU, což z rychlé kontroly udělá minutové čekání.  

Dobrou zprávou je, že Aspose OCR přichází s GPU rozšířeními, která vám umožní **rozpoznat text z obrázku** během zlomku času. V tomto tutoriálu si projdeme praktický příklad, který vám ukáže, jak **spustit OCR na PNG** pomocí C#, jak **extrahovat text z obrázku** a dokonce jak **nastavit limit paměti GPU**, abyste zůstali v rozpočtu svého hardwaru.

Probereme také „jak“ i „proč“ každého kroku, takže si odnesete solidní mentální model – ne jen hotový útržek kódu.

## Co se naučíte

- Předpoklady pro použití GPU podpory v Aspose OCR.  
- Jak načíst PNG do `Bitmap` a předat jej OCR engine.  
- Jak nakonfigurovat `GpuDevice` a `GpuMemoryLimitMb` pro optimální výkon.  
- Jak **rozpoznat text z obrázku** a získat výsledek v prostém textu.  
- Tipy pro řešení běžných okrajových případů, jako jsou GPU s nízkou pamětí nebo více‑stránkové PNG.  

Na konci tohoto průvodce budete schopni **spustit OCR na PNG** souborech na GPU rychlostí a sebejistě řídit paměťovou stopu svých OCR úloh.

![Diagram ukazující spuštění OCR na PNG s akcelerací GPU](run-ocr-on-png-diagram.png "příklad spuštění OCR na PNG")

## Předpoklady

Než se pustíme dál, ujistěte se, že máte:

1. .NET 6.0 nebo novější (kód funguje i s .NET Core a .NET Framework).  
2. NVIDIA GPU s podporou CUDA (příklad používá zařízení s indexem 0).  
3. NuGet balíček Aspose.OCR a jeho GPU rozšíření (`Aspose.OCR.Extensions`).  
4. Ukázkový PNG (`input.png`) umístěný ve složce, na kterou můžete odkazovat z projektu.  

Pokud vám některý z těchto bodů není známý, nebojte se – uvedeme alternativy tam, kde je to relevantní.

---

## Krok 1 – Instalace Aspose OCR a GPU rozšíření

Nejprve je potřeba mít správné knihovny, jinak se kód nebude kompilovat.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Balíček `Aspose.OCR.Extensions` přináší nativní CUDA binárky potřebné pro akceleraci na GPU.  
*Tip:* Pokud nemáte GPU, můžete projekt stále kompilovat; jen později nastavíte `PreferGpu = false`.

---

## Krok 2 – Načtení PNG, který chcete zpracovat

Nyní skutečně **spustíme OCR na PNG** načtením do `Bitmap`. Tento krok je jednoduchý, ale stojí za krátkou poznámku: `Bitmap` očekává cestu k souboru, takže se ujistěte, že cesta je správná vzhledem k vašemu spustitelnému souboru.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Pokud je PNG neobvykle velký (např. > 5000 px na jedné straně), můžete jej nejprve zmenšit, aby nedošlo k vyčerpání paměti GPU. Právě zde se později hodí volba **nastavit limit paměti GPU**.

---

## Krok 3 – Vytvoření a konfigurace OCR engine pro použití GPU

Tady je jádro tutoriálu: nastavení OCR engine tak, aby **rozpoznal text z obrázku** pomocí GPU. Dvě vlastnosti jsou klíčové:

- `GpuDevice` – vybírá, které CUDA zařízení použít.  
- `GpuMemoryLimitMb` – omezuje množství paměti GPU, kterou engine může alokovat.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Proč nastavit limit paměti?** Některé GPU sdílejí paměť s displejem nebo běží více úloh současně. Omezováním alokace zabráníte pádům kvůli nedostatku paměti, zejména při paralelním zpracování mnoha PNG.

---

## Krok 4 – Definování možností rozpoznání (jazyk a preference GPU)

Objekt `RecognitionOptions` říká engine, jaký jazyk má hledat a zda **preferovat GPU** i pro malé obrázky. Pro většinu anglických dokumentů to stačí, ale můžete nahradit `Language.English` jiným podporovaným jazykem.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Pokud budete potřebovat **extrahovat text z obrázku** v jiném jazyce než angličtině, stačí změnit výčtový typ `Language`. Knihovna podporuje desítky jazyků přímo z krabice.

---

## Krok 5 – Spuštění OCR a získání výsledku

Po nastavení všeho je poslední volání jednou řádkou, která skutečně **spustí OCR na PNG** a vrátí bohatý výsledek.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` obsahuje nejen prostý text (`ocrResult.Text`), ale i skóre důvěry, ohraničující rámečky a dokonce i původní obrázek se zvýrazněnými slovy – užitečné při ladění nebo vizualizaci extrakce.

**Očekávaný výstup** (pro ukázkový PNG, který říká „Hello World”):

```
=== OCR Output ===
Hello World
```

Pokud se text zobrazí poškozený, zkontrolujte, že PNG není poškozený a že limit paměti GPU není nastaven příliš nízko pro velikost obrázku.

---

## Krok 6 – Řešení okrajových případů a tipy pro nejlepší praxi

### GPU s nízkou pamětí

Pokud se objeví výjimka typu `CudaException: out of memory`, snižte `GpuMemoryLimitMb` nebo rozdělte PNG na dlaždice před zpracováním. Dlaždicování lze provést pomocí `Graphics.DrawImage` na klonu `Bitmap`.

### Více PNG v dávce

Při zpracování složky s PNG opakovaně používejte stejnou instanci `OcrEngine` – inicializace jednou šetří přepínání kontextu GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Přepnutí na CPU

Pokud GPU není k dispozici, jednoduše nastavte `PreferGpu = false`. Engine automaticky přejde na CPU bez jakýchkoli změn kódu.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat do nového konzolového projektu. Obsahuje všechny výše uvedené kroky a několik bezpečnostních kontrol.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Uložte soubor jako `Program.cs`, spusťte `dotnet run` a měly by se vám v konzoli vypsat extrahované texty.

---

## Závěr

Ukázali jsme, jak **spustit OCR na PNG** souborech pomocí GPU rozšíření Aspose OCR, jak **rozpoznat text z obrázku** a jak **extrahovat text z obrázku** při řízení **nastavení limitu paměti GPU**. Konfigurací `GpuDevice` a `GpuMemoryLimitMb` udržíte aplikaci rychlou a stabilní, i na skromných GPU.

Od sem můžete:

- Experimentovat s dalšími jazyky (`Language.French`, `Language.Spanish`).  
- Integrovat OCR krok do většího pipeline pro zpracování dokumentů.  
- Přidat post‑processing jako kontrolu pravopisu nebo extrakci entit pro vylepšení surového textu.  

Pamatujte, že klíč není jen kód, ale pochopení, proč každé nastavení má smysl. Když víte, jak **nastavit limit paměti GPU** a kdy přejít na CPU, vytvoříte OCR řešení, která škálují elegantně.

Máte otázky ohledně konkrétní velikosti PNG, více‑stránkových TIFF nebo ladění GPU chyb? Zanechte komentář níže a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}