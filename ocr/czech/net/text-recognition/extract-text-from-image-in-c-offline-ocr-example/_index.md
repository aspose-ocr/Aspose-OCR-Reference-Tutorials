---
category: general
date: 2026-02-09
description: Extrahujte text z obrázku pomocí offline OCR v C#. Kompletní příklad
  OCR v C# ukazuje, jak načíst obrázek pro OCR, rozpoznat cyrilský text a extrahovat
  text z pasu.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: cs
og_description: Extrahujte text z obrázku pomocí offline OCR v C#. Naučte se krok
  za krokem příklad OCR v C#, který načte obrázek pro OCR, rozpozná cyrilický text
  a extrahuje text z pasu.
og_title: Extrahování textu z obrázku v C# – Offline OCR průvodce
tags:
- OCR
- C#
- Aspose
title: Extrahování textu z obrázku v C# – Příklad offline OCR
url: /cs/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

preserve pipes.

Now produce final content with translated text.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v C# – Příklad offline OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale uvízli jste na API závislých na síti? Nejste v tom sami. Mnoho vývojářů narazí na problém, když OCR služba během běhu zkouší stáhnout jazykové balíčky, zejména v omezených prostředích.

V tomto průvodci si projdeme **c# ocr example**, který běží zcela offline, načte obrázek pro OCR a rozpozná cyrilické texty z pasu. Na konci budete mít připravený program, který vytiskne prostý text obsahu libovolného podporovaného obrázku přímo do konzole.

## Co se naučíte

- Jak nastavit Aspose.OCR pro offline zpracování.  
- Přesný kód pro **load image for OCR** z disku.  
- Jak nakonfigurovat engine k **recognize cyrillic text**.  
- Kompletní, připravený k zkopírování **c# ocr example**, který extrahuje text z fotografie ve stylu pasu.  

Předchozí zkušenost s Aspose není vyžadována; stačí .NET 6 (nebo novější) SDK a Visual Studio 2022 (nebo VS Code).

---

![Extrahovat text z obrázku pomocí Aspose OCR na fotografii pasu](/images/ocr-passport.jpg "extrahovat text z obrázku")

## Krok 1: Nastavení projektu pro extrahování textu z obrázku

Než napíšete jakýkoli kód, ujistěte se, že do projektu byl přidán balíček Aspose.OCR NuGet:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Použijte příznak `--version` pro uzamčení na nejnovější stabilní verzi (např. `13.9.0`). To zaručuje kompatibilitu s .NET 6.

Vytvoření nové konzolové aplikace je tak jednoduché:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Nyní máte čistý start, kde budeme **extract text from image** aniž bychom se kdykoli dotkli internetu.

## Krok 2: Načtení obrázku pro OCR – Čtení fotografie pasu

První věc, kterou OCR engine potřebuje, je bitmapa nebo stream představující obrázek. V našem scénáři **load image for OCR** z lokálního souboru nazvaného `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Proč je to důležité:** Poskytnutí streamu místo surové `Bitmap` umožňuje Aspose interně detekovat formát, což snižuje boilerplate a potenciální chyby.

## Krok 3: Konfigurace offline režimu a výběr cyrilického jazyka

Aspose.OCR může stahovat jazykové modely za běhu, ale to jde proti smyslu offline řešení. Vypněte síťová volání a explicitně řekněte engine, který jazyk má použít.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Okrajový případ:** Pokud později potřebujete rozpoznat latinské znaky ve stejném dokumentu, stačí přidat `OcrLanguage.English` do pole. Engine automaticky zvládne detekci více jazyků.

## Krok 4: Spuštění OCR engine a rozpoznání cyrilického textu

Nyní skutečně **recognize text from passport**‑stylové obrázky. Metoda `Recognize` vrací bohatý objekt výsledku obsahující prostý text, skóre důvěry a ohraničující rámečky.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Očekávaný výstup v konzoli

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Pokud výsledek vypadá poškozeně, zkontrolujte, že zdrojový obrázek je čistý a že jazykový balíček `OfflineMode` pro cyriliku je přítomen ve složce instalace Aspose (obvykle `\Aspose.OCR\resources\languages`).

## Kompletní C# OCR příklad – celý zdrojový kód

Níže je **c# ocr example** v plné šíři. Zkopírujte jej do `Program.cs` a spusťte `dotnet run`. Vše, co potřebujete k **extract text from image**, je zde.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Spuštění příkladu

```bash
dotnet run
```

Měli byste vidět, že konzole vytiskne údaje pasu v cyrilice. To je okamžik, kdy víte, že vaše pipeline **extract text from image** funguje.

## Časté problémy a jak je opravit

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Empty `PlainText` | Špatný jazykový model nebo obrázek je příliš tmavý | Ensure `OfflineMode` language includes `Cyrillic` and increase image contrast |
| `System.DllNotFoundException` | Chybějící nativní binární soubory Aspose OCR | Re‑install the NuGet package or copy the `Aspose.OCR.Native.dll` to the output folder |
| Pomalý výkon u velkých obrázků | Engine zpracovává plné rozlišení | Downscale the image to ≤ 1500 px width before feeding it to `ImageStream` |
| Poškozené znaky | Obrázek byl nesprávně otočen | Use `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` before creating the stream |

## Další kroky – Rozšíření offline OCR workflow

- **Load image for OCR** z `MemoryStream` při práci s nahranými soubory v ASP.NET Core.  
- Přepněte na **recognize text from passport** v dávkovém režimu iterací přes složku skenů pasů.  
- Spojte výsledek s **regular expressions** pro získání polí jako číslo pasu nebo datum narození.  
- Experimentujte s `ocrEngine.Configuration.UseParallelProcessing = true` pro vícejádrové zrychlení.

---

### Závěr

Právě jsme vám ukázali, jak **extract text from image** pomocí zcela offline C# OCR pipeline. Krátký, samostatný **c# ocr example** načte obrázek, nakonfiguruje engine k **recognize cyrillic text** a vytiskne extrahovaná data pasu – vše bez jediného síťového požadavku.

Neváhejte kód upravit, přidat další jazyky nebo výstup připojit k databázi. Možnosti jsou neomezené, jakmile zvládnete základy načítání obrázku pro OCR a rozpoznávání textu z fotografie ve stylu pasu.

Máte otázky nebo chcete sdílet své úpravy? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}