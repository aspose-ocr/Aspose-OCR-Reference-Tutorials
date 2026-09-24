---
category: general
date: 2026-02-16
description: Naučte se provádět OCR v C# pomocí Aspose.OCR – rozpoznávejte text z
  fotografie, čtěte text ze skenu a extrahujte text z účtenky s vysokou přesností.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: cs
og_description: Naučte se provádět OCR v C# s Aspose.OCR. Tento průvodce vám ukáže,
  jak rozpoznat text z fotografie, přečíst text ze skenu a extrahovat text z účtenky.
og_title: Jak provést OCR v C# – Kompletní průvodce Aspose
tags:
- C#
- Aspose.OCR
- Image Processing
title: Jak provést OCR v C# – Kompletní průvodce Aspose
url: /cs/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR v C# – Kompletní průvodce Aspose

Už jste se někdy zamysleli nad tím, **jak provést OCR** na rozmazaném účtence nebo náhodné fotografii, kterou jste pořízili telefonem? Nejste v tom sami. V mnoha reálných aplikacích potřebujeme **rozpoznat text z fotografie** souborů, **číst text ze skenovaných** dokumentů nebo **extrahovat text z obrázků účtenek** bez odesílání dat do cloudové služby.  

V tomto tutoriálu projdeme samostatným příkladem, který vám ukáže **jak provést OCR** pomocí Aspose.OCR, a přidáme tipy, jak **zlepšit přesnost OCR** během cesty. Na konci budete mít připravený spustitelný C# konzolový program, který vytáhne prostý text z libovolného obrázku, na který ukážete.

> **Co budete potřebovat**  
> * .NET 6 SDK (nebo jakákoli recentní verze .NET)  
> * NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)  
> * Vzorek obrázku – například fotografie účtenky pojmenovaná `photo_receipt.jpg`  

![how to perform OCR example](image.png){alt="jak provést OCR"}

## Jak provést OCR pomocí Aspose.OCR v C#

Prvním krokem je nastavit OCR engine a načíst anglický jazykový model. To je jádro **jak provést OCR** s Aspose; bez jazykového modelu by engine nevěděl, které znaky hledat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Proč je to důležité*: Načtení správného jazykového modelu přímo ovlivňuje rychlost rozpoznávání a přesnost. Angličtina je nejčastější případ, ale Aspose poskytuje desítky dalších, pokud někdy potřebujete **číst text ze skenovaných** dokumentů ve francouzštině, němčině atd.

## Rozpoznat text z fotografie

Fotografie pořízené telefonem často trpí rotací, šumem nebo nízkým kontrastem. Než požádáme engine o **rozpoznání textu z fotografie**, nakonfigurujeme některé předzpracovací možnosti, které obrázek vyčistí.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Tip*: Pokud si všimnete chybějících znaků, zkuste změnit `DenoiseLevel` na `High` nebo použít `BinarizeMethod.Sauvola`. Tyto úpravy jsou součástí strategií **zlepšení přesnosti OCR**.

## Číst text ze skenu

Nyní, když je engine připraven, načteme obrázek. Ať už jde o naskenovanou stránku PDF uloženou jako JPEG nebo fotografii tištěného formuláře, kód zůstává stejný.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Pokud máte `Stream` místo cesty k souboru, stačí nahradit `FromFile` za `FromStream`. Tato flexibilita je užitečná, když **čtete text ze skenovaných** obrázků, které pocházejí z webového nahrání.

## Extrahovat text z účtenky

Po nastavení všeho je skutečné volání OCR jediný řádek. Metoda vrací extrahovaný řetězec prostého textu, který můžeme následně zobrazit, uložit nebo předat do jiného systému.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Očekávaný výstup** (příklad pro jednoduchou účtenku):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Pokud výstup vypadá poškozeně, vraťte se k sekci předzpracování – to je nejčastější místo, kde **zlepšit přesnost OCR**.

## Zlepšení přesnosti OCR – Pokročilé úpravy

Zatímco výchozí nastavení funguje pro mnoho případů, produkční pipeline často vyžadují další péči:

| Situace | Úprava | Důvod |
|-----------|------------|--------|
| Velmi tmavé pozadí | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Zvyšuje oddělení textu od pozadí |
| Ručně psané poznámky | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Specializovaný model pro kurzívní tahy |
| Vícestránkové skeny | Loop over each page image and call `Recognize()` per iteration | Udržuje nízkou paměťovou stopu |
| Velké obrázky (> 2000 px) | Resize before feeding to OCR (`Image.Resize(width, height)`) | Rychlejší zpracování, méně paměťových výpadků |

Pamatujte, **jak provést OCR** není univerzální recept – často budete experimentovat s těmito nastaveními, dokud výstup nesplní vaše požadavky na kvalitu.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Obsahuje všechny části, o kterých jsme mluvili, plus malý pomocník, který kontroluje, zda soubor existuje, než se ho pokusí načíst.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Spusťte program pomocí `dotnet run`. Pokud je vše nastaveno správně, uvidíte extrahovaný text vytištěný do konzole.

## Časté otázky a okrajové případy

**Q: Co když je obrázek PDF?**  
A: Převést každou stránku PDF nejprve na obrázek (např. pomocí `Aspose.Pdf` nebo `PdfSharp`) a poté předat vzniklý bitmap do `ocrEngine.Image`.

**Q: Mohu zpracovávat obrázky paralelně?**  
A: Ano, ale vytvořte samostatný `OcrEngine` pro každé vlákno. Engine není vláknově bezpečný, takže sdílení jedné instance může způsobit závodní podmínky.

**Q: Funguje to na Linuxu?**  
A: Rozhodně. Aspose.OCR je multiplatformní; stačí zajistit, že jsou nainstalovány nativní závislosti (`libgdiplus` pro .NET Core na Linuxu).

**Q: Jak zacházet s vícejazyčnými účtenkami?**  
A: Načtěte před rozpoznáním více jazykových modelů:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Engine bude zkoušet každý model v pořadí.

## Závěr

Nyní máte solidní, end‑to‑end odpověď na **jak provést OCR** v C# s Aspose.OCR. Tutoriál pokryl vše od inicializace engine, **rozpoznání textu z fotografie**, **čtení textu ze skenovaných** dokumentů až po **extrahování textu z účtenky**, a poskytl vám praktické způsoby, jak **zlepšit přesnost OCR**.  

Další kroky? Zkuste vyměnit anglický model za model pro ručně psané texty, experimentujte s různými hodnotami `BinarizeMethod` nebo integrujte volání OCR do ASP.NET API, které zpracovává nahrané soubory za běhu. Možnosti jsou tak široké, jako jsou obrázky, které mu předáte.

Máte další otázky ohledně OCR, předzpracování obrázků nebo knihoven Aspose? Zanechte komentář nebo prozkoumejte oficiální dokumentaci Aspose.OCR pro podrobnější informace. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}