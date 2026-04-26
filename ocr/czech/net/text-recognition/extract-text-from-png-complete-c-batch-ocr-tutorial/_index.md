---
category: general
date: 2026-04-26
description: Rychle extrahujte text z PNG souborů pomocí C#. Naučte se, jak převádět
  obrázky na text, číst PNG soubory, procházet obrázky a provádět hromadné OCR obrázků
  během několika minut.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: cs
og_description: Extrahujte text z PNG souborů rychle pomocí C#. Tento průvodce ukazuje,
  jak převést obrázky na text, číst PNG soubory, procházet obrázky a provádět hromadné
  OCR obrázků.
og_title: Extrahování textu z PNG – Kompletní C# dávkový OCR tutoriál
tags:
- C#
- OCR
- Aspose
title: Extrahování textu z PNG – Kompletní C# dávkový OCR tutoriál
url: /cs/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z PNG – Kompletní C# dávkový OCR tutoriál

Už jste někdy potřebovali **extrahovat text z PNG** souborů, ale nevedeli jste, kde začít? Nejste sami — mnoho vývojářů narazí na tento problém, když poprvé zkouší OCR na složce se screenshoty. Dobrou zprávou je, že s několika řádky C# a Aspose OCR můžete převést obrázky na text, číst PNG soubory, procházet obrázky a vše dávkově zpracovat najednou.  

V tomto tutoriálu projdeme připravenou konzolovou aplikaci, která přesně to dělá. Na konci budete mít samostatné řešení, které vytáhne text ze všech PNG v adresáři a vytvoří odpovídající soubor `.txt` vedle každého obrázku. Žádné extra skripty, žádné ruční kopírování — jen čistý kód.

## Co budete potřebovat

- **.NET 6 SDK** (nebo jakoukoli novější verzi .NET). Je zdarma, rychlý a funguje všude.
- **Aspose.OCR for .NET** (balíček NuGet). Knihovna obsahuje akceleraci GPU, pokud máte kompatibilní grafickou kartu, ale automaticky přejde na CPU, pokud není k dispozici.
- Složku s několika **PNG obrázky**, které chcete zpracovat.  
- Textový editor nebo IDE — Visual Studio, VS Code, Rider — cokoli preferujete.

To je vše. Pokud už máte výše uvedené, můžete začít.

![extract text from png example](image.png "extract text from png demo screenshot")

*Alt text obrázku: “extrahovat text z png pomocí C# dávkového OCR”*

## Krok 1 – Nastavení projektu a instalace Aspose.OCR

Nejprve vytvořte nový konzolový projekt a přidejte balíček Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Proč používáme konzolovou aplikaci? Je to nejjednodušší hostitel pro dávkové úlohy a můžete ji spustit z příkazové řádky nebo naplánovat pomocí plánovače úloh. Pokud později budete potřebovat UI, můžete jen přesunout jádro logiky do knihovny tříd.

## Krok 2 – Inicializace OCR enginu s akcelerací GPU (nebo fallback na CPU)

Aspose nabízí `GpuOcrEngine`, který automaticky detekuje podporovanou GPU. Pokud žádná není nalezena, přepne se na běžný CPU engine — žádný další kód není potřeba.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Tip:** Pokud běžíte na serveru bez GPU, můžete nahradit `GpuOcrEngine` za `OcrEngine` a kód se bude chovat naprosto stejně.

## Krok 3 – Procházení obrázků v cílovém adresáři

Musíme **procházet obrázky** a vybírat jen PNG soubory. Metoda `Directory.GetFiles` udělá těžkou práci a my se ochráníme před prázdnou složkou.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Všimněte si použití `SearchOption.TopDirectoryOnly`. Pokud později potřebujete rekurzivně procházet podadresáře, stačí přepnout na `AllDirectories`. Tato malá změna vám umožní **převést obrázky na text** v celém stromu jedním řádkem.

## Krok 4 – Provést OCR a uložit výsledek

Nyní přichází jádro workflow **dávkového OCR obrázků**. Načteme každý PNG, spustíme `Recognize()` a zapíšeme získaný řetězec do souboru `.txt`, který má stejný základní název.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Proč to obalit do try/catch?** V reálných dávkách obrázků se často objeví poškozený soubor nebo PNG s neobvyklým barevným profilem. Zachycení výjimky zabrání zhroucení celého běhu a umožní pokračovat ve zpracování zbývajících souborů.

## Krok 5 – Spusťte aplikaci a ověřte výstup

Sestavte a spusťte aplikaci:

```bash
dotnet run
```

Měli byste vidět výstup v konzoli podobný tomuto:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Otevřete kterýkoli z vygenerovaných souborů `.txt` — tam je váš extrahovaný text. Pokud je soubor prázdný, zkontrolujte kvalitu obrázku; OCR funguje nejlépe s čistým, vysokokontrastním textem.

### Rychlý ověřovací skript (volitelně)

Chcete-li se ujistit, že každý PNG má odpovídající textový soubor, spusťte tento malý PowerShell one‑liner:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Běžné varianty a okrajové případy

| Situace | Co změnit |
|-----------|----------------|
| **Jazyky mimo latinku** (např. cyrilice) | Nastavte `ocrEngine.Language = Language.Cyrillic;` |
| **Velký soubor obrázků (>10 000 souborů)** | Použijte `Parallel.ForEach` pro zrychlení, ale sledujte využití GPU paměti. |
| **Potřeba zachovat původní pořadí obrázků** | Seřaďte `pngFiles` před `foreach` (`Array.Sort(pngFiles);`). |
| **Běh na CI serveru bez GPU** | Nahraďte `GpuOcrEngine` za `OcrEngine`, aby nedošlo k chybám při inicializaci GPU. |
| **Chcete zpracovat jen soubory obsahující konkrétní klíčové slovo** | Po získání `result.Text` zkontrolujte `result.Text.Contains("Invoice")` před zápisem souboru. |

Tyto úpravy vám umožní přizpůsobit **pipeline převodu obrázků na text** téměř jakémukoli scénáři, na který narazíte.

## Kompletní zdrojový kód (připravený ke kopírování)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Uložte tento soubor jako `Program.cs`, spusťte `dotnet run` a sledujte, jak se děje magie.

## Závěr

Nyní máte **kompletní, produkčně připravený způsob, jak extrahovat text z PNG** souborů pomocí C#. Tutoriál pokryl vše — od nastavení projektu, přes inicializaci OCR enginu s akcelerací GPU, **procházení obrázků**, až po **dávkové OCR obrázky** a uložení výsledků jako prostý text.  

Pokud vás zajímají další kroky, zkuste:

- **Převést obrázky na text** pro jiné formáty (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}