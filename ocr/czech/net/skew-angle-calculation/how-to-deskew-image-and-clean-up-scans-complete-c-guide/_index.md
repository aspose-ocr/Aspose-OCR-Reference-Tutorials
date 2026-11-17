---
category: general
date: 2026-03-18
description: Jak vyrovnat sklon obrazu a snížit šum ve skenovaných souborech. Naučte
  se načíst obrázek ze souboru, extrahovat text z TIFF a rozpoznat text z obrázku
  pomocí Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: cs
og_description: Jak rychle vyrovnat zkosení obrázku pomocí Aspose OCR. Tento průvodce
  ukazuje, jak snížit šum, načíst obrázek ze souboru a extrahovat text z TIFF v C#.
og_title: Jak narovnat obrázek – kompletní C# OCR tutoriál
tags:
- OCR
- C#
- Image Processing
title: Jak narovnat obrázek a vyčistit skeny – Kompletní průvodce C#
url: /cs/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opravit zkosení obrázku – Kompletní C# OCR tutoriál

Už jste se někdy zamýšleli **jak opravit zkosení obrázku** souborů, které vypadají, jako by byly pořízeny z roztřeseného skeneru? Nejste v tom sami. Většina vývojářů narazí na tento problém, když je zdrojový TIFF trochu šikmý, a výsledky OCR jsou nepořádek. Dobrá zpráva? Pár řádků C# vám umožní narovnat obrázek, potlačit zrnitý podklad a získat čistý, prohledávatelný text přímo ze souboru.

V tomto průvodci projdeme **jak snížit šum**, **načíst obrázek ze souboru** a nakonec **rozpoznat text z obrázku** pomocí Aspose OCR. Na konci budete schopni **extrahovat text z tiff** dokumentů bez potíží.

> **Tip:** Pokud už používáte Aspose OCR v jiných projektech, můžete tyto filtry přidat bez dalších licenčních komplikací.

---

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje i na .NET Core)  
- NuGet balíček Aspose.OCR (`Install-Package Aspose.OCR`)  
- Naskenovaný TIFF, který je mírně natočený nebo šumivý (použijeme `skewed_scanned_doc.tif` jako příklad)  
- Textový editor nebo IDE (Visual Studio, VS Code, Rider – vyberte si)

Žádné další knihovny nejsou potřeba; filtry, které použijeme, jsou součástí Aspose OCR.

---

## Krok 1 – Vytvořte OCR Engine (Jak opravit zkosení obrázku)

První věc, kterou uděláte, je vytvořit `OcrEngine`. Považujte ho za mozek, který pak bude číst znaky za vás.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Proč vytvořit engine předem? Poskytuje vám jedno místo, kam můžete připojit předzpracovatelské filtry, jazykové balíčky a výstupní možnosti. Pokud tento krok přeskočíte a zavoláte `OcrEngine.Recognize` přímo, ztratíte možnost nejprve vyčistit obrázek, což je přesně důvod, proč nás zajímá oprava zkosení.

---

## Krok 2 – Přidejte filtry pro opravu zkosení a redukci šumu (Jak snížit šum)

Nyní připojíme dva filtry:

| Filter | Co dělá | Proč je důležitý |
|--------|--------------|----------------|
| `AutoDeskewFilter` | Detekuje a opravuje rotaci | Vyrovná řádky textu, aby je OCR engine mohl správně přečíst |
| `NoiseReductionFilterV2` | Odstraňuje skvrny a zrnitý podklad | Čistší pixely znamenají méně chyb v rozpoznání |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Můžete nahradit `NoiseReductionFilterV2` starší verzí, ale algoritmus v2 lépe zvládá moderní skenery. Pokud je váš dokument již dokonale rovný, filtr pro opravu zkosení obrázek prostě projde beze změny – žádné škody.

---

## Krok 3 – Načtěte obrázek ze souboru (Load Image from File)

Aspose poskytuje užitečný pomocník `ImageStream.FromFile`, který načte různé formáty, včetně TIFF, JPEG, PNG a BMP. Zde je, jak načteme soubor do paměti:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Nahraďte `YOUR_DIRECTORY` skutečnou cestou na vašem počítači. Pokud pracujete s relativní cestou, ujistěte se, že soubor leží vedle spustitelného souboru nebo nastavte pracovní adresář odpovídajícím způsobem.

---

## Krok 4 – Spusťte OCR na předzpracovaném obrázku (Rozpoznat text z obrázku)

S filtry na místě a načteným obrázkem nakonec požádáme Aspose, aby přečetl znaky:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Za scénou engine spustí algoritmus pro opravu zkosení, vyhladí šum a poté použije rozpoznávač založený na neuronové síti. Výsledek je zabalen v objektu `OcrResult`, který vám poskytne surový text, skóre důvěry a dokonce i ohraničující rámečky, pokud je později potřebujete.

---

## Krok 5 – Zobrazte nebo uložte extrahovaný text (Extrahovat text z TIFF)

Pro rychlou ukázku jednoduše vypíšeme text do konzole, ale můžete jej zapsat do souboru, databáze nebo předat do následného pracovního postupu.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Očekávaný výstup** (ukázka, bude se lišit podle vašeho dokumentu):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Pokud výstup stále obsahuje poškozené znaky, zkontrolujte, že původní TIFF nemá příliš nízké rozlišení (doporučeno minimálně 300 dpi) a že jazyk je nastaven správně v `ocrEngine.Settings.Language`.

---

## Kompletní funkční příklad (Všechny kroky na jednom místě)

Níže je kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu a okamžitě spustit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Uložte soubor jako `Program.cs`, spusťte `dotnet run` a v terminálu by se měl objevit vyčištěný text.

---

## Často kladené otázky a okrajové případy

### Co když má můj TIFF více stránek?
Aspose OCR může zpracovávat vícestránkové obrázky pomocí smyčky přes `image.GetPages()` (nebo pomocí `image.Pages`). Každá stránka vrátí svůj vlastní `OcrResult`. Pokud potřebujete jeden řetězec, spojte je pomocí `StringBuilder`.

### Funguje filtr pro opravu zkosení na silně natočených obrázcích?
Zvládá rotace až přibližně ±15°. Nad tuto hodnotu možná budete muset obrázek předem otočit ručně pomocí grafické knihovny (např. `System.Drawing` nebo `SkiaSharp`) před předáním Aspose.

### Jak mohu zlepšit přesnost pro text v jiných jazycích než angličtině?
Nastavte jazyk explicitně:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Můžete také načíst vlastní jazykové balíčky, pokud vestavěné neobsahují vaše písmo.

### Můžu to spustit na Linuxu?
Určitě. Aspose OCR je multiplatformní; jen se ujistěte, že jsou přítomny nativní závislosti (obvykle žádné pro čistou .NET verzi). Použijte `dotnet publish -r linux-x64` pro samostatný binární soubor.

---

## Bonus: Vizualizace opraveného obrázku

Pokud chcete vidět opravený obrázek před OCR, můžete jej uložit zpět na disk:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![příklad opravy zkosení obrázku](https://example.com/deskew-demo.png "příklad opravy zkosení obrázku")

*Text alternativního obrázku:* **příklad opravy zkosení obrázku** – ukazuje před/po otočeném TIFF opraveném pomocí AutoDeskewFilter.

---

## Závěr

Probrali jsme **jak opravit zkosení obrázku** souborů, **jak snížit šum**, a celý proces **rozpoznat text z obrázku**, **načíst obrázek ze souboru** a **extrahovat text z tiff** pomocí Aspose OCR v C#. Hlavní výsledek? Přidáním pouhých dvou předzpracovatelských filtrů můžete proměnit roztřesený, zrnitý sken na ostrý, prohledávatelný dokument bez jakýchkoli externích nástrojů.

Jste připraveni na další krok? Zkuste nahradit `AutoDeskewFilter` za `AutoRotateFilter`, pokud jsou vaše dokumenty vzhůru nohama, nebo experimentujte s `ContrastEnhancementFilter` pro vybledlé výtisky. Stejný vzor—engine → filtry → načtení → rozpoznání—platí pro všechny scénáře Aspose OCR, takže můžete tento základ znovu použít pro PDF, PNG nebo i fotografie z kamery.

Šťastné programování a ať je vaše OCR vždy přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}