---
category: general
date: 2026-03-17
description: Extrahujte text z PNG pomocí Aspose OCR v C#. Naučte se číst text z obrázku,
  zpracovávat OCR účtenek a vytvořit OCR engine s akcelerací GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: cs
og_description: Extrahujte text z PNG pomocí Aspose OCR. Tento průvodce ukazuje, jak
  číst text z obrázku, zpracovat OCR účtenek a efektivně vytvořit OCR engine.
og_title: Extrahovat text z PNG – Číst text z obrázku pomocí OCR
tags:
- OCR
- CSharp
- Aspose
title: Extrahovat text z PNG – Číst text z obrázku pomocí OCR
url: /cs/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z PNG – Číst text z obrázku pomocí OCR

Už jste někdy potřebovali **extrahovat text z PNG**, ale nebyli jste si jisti, která knihovna vám poskytne spolehlivé výsledky? Nejste v tom jediní — vývojáři se stále ptají: „Jak přečíst text ze souborů obrázků, jako jsou účtenky, aniž bychom psali vlastní neuronovou síť?“ Dobrou zprávou je, že Aspose OCR za vás udělá těžkou práci a můžete dokonce zapnout GPU pro zvýšení rychlosti.

V tomto tutoriálu projdeme vše, co potřebujete k **zpracování OCR účtenek**, od instalace balíčku NuGet až po vytvoření OCR enginu, který rozumí vašemu PNG souboru. Na konci budete mít samostatnou konzolovou aplikaci, která načte obrázek účtenky, vypíše rozpoznaný text a ukáže vám, jak upravit engine pro různé scénáře. Žádná externí dokumentace, jen čistý kód a jasná vysvětlení.

## Požadavky

- .NET 6.0 SDK (nebo jakákoli novější verze .NET)  
- Visual Studio 2022 nebo VS Code s rozšířeními C#  
- Podporovaná NVIDIA GPU s nejnovějším ovladačem (volitelné, ale doporučené pro režim GPU)  
- Balíček **Aspose.OCR** NuGet (`dotnet add package Aspose.OCR`)  

Pokud nemáte GPU, můžete příklad stále spustit v režimu CPU — stačí přeskočit řádky s konfigurací GPU.

## Krok 1: Nainstalujte Aspose.OCR a nastavte projekt

Nejprve vytvořte nový konzolový projekt a přidejte knihovnu Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Proč je to důležité: balíček `Aspose.OCR` obsahuje OCR engine, načítače obrázků a volitelnou podporu GPU. Přidání přes NuGet vám zajistí nejnovější stabilní verzi (k březnu 2026 je to 23.10).

## Krok 2: Importujte jmenné prostory a vytvořte OCR engine

Nyní otevřete **Program.cs** a přidejte požadované `using` direktivy. Poté vytvořte instanci engine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Tip:** Pokud narazíte na `System.DllNotFoundException` na počítačích bez GPU, jednoduše zakomentujte dva řádky, které nastavují `EngineMode` a `GpuDeviceId`. Engine se automaticky přepne na CPU.

## Krok 3: Načtěte PNG obrázek, ze kterého chcete extrahovat text

Aspose OCR může číst obrázky přímo ze souborové cesty, proudu nebo dokonce z pole bajtů. Pro tuto ukázku načteme lokální obrázek účtenky.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Všimněte si, jak chráníme před chybějícím souborem. Ve skutečných aplikacích byste pravděpodobně zobrazili uživatelsky přívětivou zprávu místo pouhého ukončení.

## Krok 4: Proveďte OCR rozpoznání

Skutečná extrakce textu proběhne jedním voláním metody. Engine vrátí objekt `OcrResult`, který obsahuje surový řetězec, skóre důvěry a informace o rozložení.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Proč kontrolujeme `ocrResult.Text`: někdy nízkokvalitní PNG vrátí prázdný řetězec a je lepší uživatele o tom informovat, než tiše nic nevypsat.

## Krok 5: Výstup rozpoznaného textu

Nakonec vytiskněte extrahovaný řetězec do konzole. Můžete jej také zapsat do souboru, databáze nebo předat jinému servisu.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Když spustíte program (`dotnet run`), měli byste vidět něco jako:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

To je **kompletní řešení pro extrakci textu z PNG** souborů pomocí Aspose OCR a právě jste se naučili, jak **číst text z obrázku** souborů, které vypadají jako účtenky.

## Volitelné: Doladění OCR engine (pokročilé)

Pokud potřebujete vyšší přesnost pro specifické fonty nebo šumivé pozadí, zvažte úpravu těchto nastavení:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Tyto úpravy jsou zvláště užitečné, když **zpracováváte OCR účtenek** ve dávkových úlohách, kde některé skeny nejsou dokonalé.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se stane | Oprava |
|-------|----------------|-----|
| **Chybějící GPU driver** | Engine se snaží načíst CUDA, ale DLL nenajde. | Nainstalujte nejnovější NVIDIA driver nebo přepněte do CPU režimu odstraněním řádku `EngineMode.Gpu`. |
| **Nesprávná cesta k obrázku** | `ImageStream.FromFile` vyhodí výjimku, pokud soubor není nalezen. | Vždy validujte cestu (viz Krok 3) nebo použijte `Path.Combine` pro multiplatformní bezpečnost. |
| **Nízká důvěra u rozmazaných účtenek** | OCR engine nedokáže rozlišit znaky. | Povolit `EnableImagePreprocessing` a případně zvýšit DPI obrázku před předáním engine. |
| **Únik paměti v dlouho běžících službách** | Každý `OcrEngine` drží neřízené zdroje. | Uvolněte engine po použití: `using var ocrEngine = new OcrEngine();` |

## Kompletní funkční příklad (kopírujte‑vložit)

Níže je **celý program**, který můžete vložit do `Program.cs`. Obsahuje všechny volitelné úpravy zakomentované pro snadnou aktivaci.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Uložte, spusťte `dotnet run` a uvidíte obsah účtenky vytištěný v konzoli.

![příklad extrakce textu z png](receipt.png "příklad extrakce textu z png")

*Obrázek výše ukazuje ukázkový PNG soubor účtenky, který kód dokáže zpracovat.*

## Shrnutí

Probrali jsme, jak **extrahovat text z PNG** souborů pomocí Aspose OCR, ukázali, jak **číst text z obrázku**, a prošli kompletním **pipeline pro zpracování OCR účtenek**, který zahrnuje volitelné GPU zrychlení. **Vytvořením OCR engine** sami získáte plnou kontrolu nad konfigurací, výkonem a ošetřením chyb.

## Co zkusit dál?

- **Dávkové zpracování**: Procházet adresář s PNG účtenkami a zapsat každý výsledek do CSV souboru.  
- **Integrace s Azure Functions**: Přeměnit tuto konzolovou aplikaci na serverless endpoint, který přijímá nahrávání obrázků.  
- **Podpora více jazyků**: Vyměnit `Language.English` za `Language.Spanish` nebo přidat vlastní slovníky.  
- **Post‑zpracování**: Použít regulární výrazy k extrakci polí jako celková částka, datum nebo DIČ z čistého OCR řetězce.

Neváhejte experimentovat — OCR je překvapivě flexibilní nástroj, jakmile znáte správné nastavení. Pokud narazíte na problémy, zanechte komentář níže nebo si prohlédněte referenci Aspose OCR API pro podrobnější informace.

Šťastné kódování a užijte si převod těch neústupných PNG účtenek na prohledávatelný text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}