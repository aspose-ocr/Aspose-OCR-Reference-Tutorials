---
category: general
date: 2026-03-21
description: 'c# OCR tutoriál: Naučte se, jak pomocí OCR v C# extrahovat urdský text
  z PNG obrázku. Krok za krokem kód, nastavení jazyka a praktické tipy jsou zahrnuty.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: cs
og_description: 'c# ocr tutoriál: Naučte se, jak pomocí OCR v C# extrahovat urdský
  text z PNG obrázku. Kompletní průvodce s kódem a tipy.'
og_title: c# OCR návod – Extrahujte urdský text z PNG obrázků
tags:
- OCR
- C#
- Urdu
- Image Processing
title: c# OCR tutoriál – Extrahovat urdský text z PNG obrázků
url: /cs/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutoriál – Extrahování urdského textu z PNG obrázků

Už jste někdy potřebovali **c# OCR tutoriál**, který skutečně vytáhne urdský text z PNG souboru? Nejste v tom sami. V mnoha projektech — zpracování faktur, archivace dokumentů nebo dokonce rychlý překladový nástroj — narazíte na situaci, kdy musíte rozpoznat text z obrázku a jazyk je důležitý.  

V tomto průvodci vás provedeme kompletním, připraveným řešením, které extrahuje urdský text z PNG pomocí OCR enginu. Uvidíte, proč každá řádka existuje, jak zacházet s chybějícími jazykovými balíčky a co dělat, pokud obrázek není dokonalý. Na konci budete dostatečně sebejistí, abyste mohli kód přizpůsobit pro jiné jazyky nebo typy souborů.

## Co se naučíte

- Jak nastavit C# OCR knihovnu (bez skrytých triků)  
- Přesné kroky k **extrahování urdského textu** z PNG souboru  
- Proč nastavení jazyka na Urdu má význam a jak engine automaticky stahuje chybějící data  
- Způsoby, jak ověřit výstup a řešit běžné problémy  

Nejsou potřeba žádné externí odkazy na dokumentaci – vše, co potřebujete, je zde.

## Předpoklady (Co potřebujete před zahájením)

| Požadavek | Proč je to důležité |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | Moderní API a podpora async |
| Visual Studio 2022 (or VS Code with C# extension) | IDE s IntelliSense usnadňuje čtení kódu |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Poskytuje `Language.Urdu` a metody `Recognize` |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | Zdroj pro operaci **recognize text image** |

Pokud ještě nemáte OCR balíček, spusťte tento jednorázový příkaz v Package Manager Console:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

> **Tip:** SDK automaticky stáhne jazyková data při prvním použití, takže není potřeba ručně stahovat Urdu jazykové balíčky.

## Krok 1: Instalace a reference OCR knihovny

Než vytvoříme engine, projekt musí odkazovat na OCR balíček. Přidejte následující `using` direktivy na začátek souboru:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

## Krok 2: Vytvoření instance OCR enginu  

Nyní skutečně spustíme engine. Představte si engine jako mozek, který bude interpretovat pixlové vzory jako znaky.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Proč je to důležité:** `TryCreateFromLanguage` vrací `null`, pokud nejsou k dispozici jazyková data, což nám dává možnost rychle selhat místo pozdějšího zhroucení.

## Krok 3: Načtení PNG obrázku  

OCR engine pracuje s objekty `SoftwareBitmap`, nikoli s čistými cestami k souborům. Následující pomocná funkce načte PNG z disku a převede jej do požadovaného formátu.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Hraniční případ:** Pokud je PNG barevný, převod na odstíny šedi (`Gray8`) často zlepšuje rozpoznání, zejména u skriptů jako Urdu, které mají jemné diakritické znaky.

## Krok 4: Rozpoznání textu z obrázku  

Zde je jádro **c# OCR tutoriálu** — požádání engine o přečtení obrázku.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

Vlastnost `OcrResult.Text` obsahuje surový Unicode řetězec. Protože jsme dříve nastavili jazyk na Urdu, engine použije správná pravidla skriptu.

## Krok 5: Výstup a ověření extrahovaného textu  

Nakonec výsledek vytiskneme do konzole. Ve skutečné aplikaci jej můžete uložit do databáze nebo předat překladové službě.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Co očekávat:** Pokud je obrázek jasný, uvidíte něco jako:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Pokud výstup vypadá poškozeně, zkontrolujte kvalitu obrázku (kontrast, šum) a zvažte předzpracování (např. binarizaci).

## Jak extrahovat urdský text z PNG souboru – Časté úskalí  

1. **Nízký kontrast** – OCR má potíže, když jsou barvy popředí a pozadí podobné. Použijte nástroje pro úpravu obrázků ke zvýšení kontrastu před spuštěním kódu.  
2. **Nesprávné DPI** – Skenování při 300 dpi nebo vyšším poskytuje engine více detailů.  
3. **Chybějící jazykový balíček** – První volání `TryCreateFromLanguage` může spustit stažení; ujistěte se, že váš počítač má přístup k internetu.  

Řešení těchto problémů výrazně zvyšuje úspěšnost **recognize text image**.

## Rozpoznání textu z obrázku: Rozšíření na jiné formáty  

I když se tento tutoriál zaměřuje na PNG, stejný postup funguje pro JPEG, BMP nebo TIFF — stačí změnit příponu souboru a zajistit, aby dekodér podporoval daný formát. Klíčová řádka zůstává `await ocrEngine.RecognizeAsync(bitmap);`.

## Tipy pro OCR z PNG souboru – Výkon a škálování  

- **Dávkové zpracování:** Načtěte více obrázků do seznamu a spusťte `Task.WhenAll` pro paralelní rozpoznávání.  
- **Cacheování engine:** Vytvořte jedinou instanci `OcrEngine` a znovu ji použijte v různých voláních; opakované vytváření přidává režii.  
- **Správa paměti:** Po použití uvolněte objekty `SoftwareBitmap` (`bitmap.Dispose()`), aby byl proces úsporný.

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, který můžete zkompilovat a spustit. Obsahuje všechny `using` příkazy, asynchronní zpracování a kontroly chyb.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Očekávaný výstup:** Konzole vytiskne přesné urdské znaky nalezené v obrázku, zachovávající pořadí zprava doleva.

## Závěr  

Právě jste dokončili **c# OCR tutoriál**, který ukazuje, jak **extrahovat urdský text** z PNG, nakonfigurovat jazyk a bezpečně zpracovat výsledek. Kroky — instalace knihovny, vytvoření engine, načtení obrázku, rozpoznání textu a jeho výstup — tvoří znovupoužitelný vzor, který můžete aplikovat na jakýkoli skript nebo typ souboru.  

Dále můžete experimentovat s **recognize text image** na vícestránkových PDF (nejprve převést každou stránku na PNG) nebo integrovat překladové API, které automaticky převede extrahovaný urdštinu do angličtiny. Možnosti jsou neomezené, jakmile zvládnete tento základní workflow.

Šťastné programování a ať jsou vaše OCR výsledky krystalicky čisté!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}