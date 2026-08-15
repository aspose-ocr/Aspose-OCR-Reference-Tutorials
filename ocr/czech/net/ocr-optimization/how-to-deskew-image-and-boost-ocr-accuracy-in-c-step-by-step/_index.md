---
category: general
date: 2026-04-17
description: Jak rychle odstranit šikmost obrázku pomocí Aspose.OCR – naučte se načíst
  obrázek pro OCR, předzpracovat obrázek pro OCR a rozpoznat text na obrázku s vysokou
  přesností.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: cs
og_description: Jak vyrovnat sklon obrázku a zlepšit přesnost OCR v C#. Naučte se
  načíst obrázek pro OCR, předzpracovat jej a rozpoznat text na obrázku pomocí Aspose.OCR.
og_title: Jak narovnat obrázek – Kompletní C# OCR tutoriál
tags:
- Aspose.OCR
- C#
- Image Processing
title: Jak vyrovnat obrázek a zvýšit přesnost OCR v C# – krok za krokem
url: /cs/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak narovnat obrázek a zvýšit přesnost OCR v C#

**How to deskew image** je běžná překážka, když potřebujete získat text z fotografie, která není dokonale zarovnaná. V tomto průvodci si projdeme načtení obrázku, jeho předzpracování a nakonec **recognize text image** pomocí výkonného řetězce filtrů Aspose.OCR.

Pokud jste někdy nasměrovali fotoaparát telefonu na účtenku, ceduli nebo naskenovaný formulář a výsledek byl zkroucený, nečitelné znaky, víte, jak frustrující to může být. Dobrá zpráva? Několik řádků C# kódu může obrázek narovnat, odstranit šum a poskytnout čistý řetězec, který můžete skutečně použít. Dotkneme se také toho, jak **improve OCR accuracy** úpravou kroků předzpracování.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje i s .NET Core)  
- Licence nebo evaluační kopie **Aspose.OCR** (k dispozici přes NuGet)  
- Soubor obrázku, který je mírně natočený nebo šumivý (např. `skewed_photo.png`)  

Žádné složité nástroje třetích stran – jen knihovna Aspose.OCR a trochu znalostí C#.

![Příklad jak narovnat obrázek](/images/deskew-demo.png "How to deskew image – original vs corrected")

---

## Krok 1 – Load Image OCR: Getting the Source File Ready

Než budeme cokoli narovnávat, musíme obrázek načíst do paměti. Metoda `OcrImage.FromFile` to provede přesně.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **Proč je to důležité:** Načtení obrázku jako `OcrImage` poskytuje OCR enginu přímý přístup k pixelovým datům, což je nezbytné pro následné **preprocess image OCR** kroky. Pokud je cesta k souboru špatná, dostanete `FileNotFoundException`, takže zkontrolujte umístění.

## Krok 2 – Preprocess Image OCR: Building a Deskew Filter Chain

Nyní přichází jádro **how to deskew image**. Aspose.OCR dodává kolekci filtrů, které můžete skládat v libovolném pořadí. Pro většinu reálných fotografií budete chtít:

1. **Deskew** – opravit rotaci  
2. **Denoise** – odstranit šum typu sůl‑a‑pepř  
3. **ContrastEnhance** – zvýraznit slabé znaky

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **Tip:** Pokud je váš obrázek již dobře exponovaný, můžete vynechat `ContrastEnhanceFilter`. Méně zpracování znamená rychlejší provedení.

### Okrajové případy

- **Extrémní rotace (>45°):** `DeskewFilter` funguje nejlépe až do cca 30°. Pro větší úhly budete možná muset obrázek nejprve otočit ručně (`filteredImage.Rotate(…)`).
- **Barevné pozadí:** Před denoisingem převést na odstíny šedi pro lepší výsledek (`filteredImage = filteredImage.ToGrayscale();`).

## Krok 3 – Recognize Text Image: Running the OCR Engine

S čistým, narovnaným bitmapovým obrázkem v ruce je čas extrahovat znaky.

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **Co se děje pod kapotou?** `OcrEngine` spouští neuronovou síť, která očekává téměř svislý, vysokokontrastní obrázek. Proto je předchozí **preprocess image OCR** krok klíčový pro **improve OCR accuracy**.

### Očekávaný výstup

Pokud původní foto obsahovalo řádek „Invoice #12345 – Total $89.99“, konzole vypíše něco jako:

```
Invoice #12345 – Total $89.99
```

Pokud vidíte zkreslené znaky, vraťte se k řetězci filtrů – možná obrázek potřebuje další zaostření (`new SharpenFilter()`).

## Krok 4 – Fine‑Tuning for Better OCR Accuracy

I po narovnání může OCR selhat u určitých fontů nebo nízkého rozlišení. Zde je několik rychlých úprav:

| Problém | Řešení |
|-------|-----|
| Malá velikost písma (<10 pt) | Zvětšit obrázek (`filteredImage = filteredImage.Resize(2.0);`) |
| Světle šedý text na bílém pozadí | Dále zvýšit kontrast (`new ContrastEnhanceFilter(1.5)`) |
| Smíšený jazykový text | Nastavit `ocrEngine.Language = OcrLanguage.Multilingual;` |

Tyto úpravy přímo **improve OCR accuracy** aniž by měnily základní strukturu kódu.

## Kompletní funkční příklad

Níže je kompletní, připravený program, který zahrnuje všechny výše uvedené kroky. Zkopírujte jej do nového konzolového projektu a stiskněte **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Spusťte program a měli byste vidět vyčištěný, narovnaný text vytištěný v konzoli.

## Často kladené otázky

**Q: Funguje to i s PDF?**  
A: Ano. Každou stránku PDF převedete na obrázek (např. pomocí `Aspose.PDF`) a předáte vzniklý bitmap do stejného řetězce filtrů.

**Q: Co když je můj obrázek už perfektně zarovnaný?**  
A: `DeskewFilter` detekuje téměř nulový úhel a obrázek nechá beze změny – žádné poškození.

**Q: Můžu zpracovávat více obrázků najednou?**  
A: Rozhodně. Zabalte kód do smyčky `foreach (var path in Directory.GetFiles(...))` a uložte každý `ocrResult.Text` do seznamu nebo souboru.

---

## Závěr

Ukázali jsme **how to deskew image** programově, prošli **load image OCR** krokem, aplikovali robustní **preprocess image OCR** pipeline a nakonec **recognize text image** s Aspose.OCR. Úpravou filtrů a případným škálováním nebo zaostřováním můžete **improve OCR accuracy** pro širokou škálu reálných scénářů.

Jste připraveni na další výzvu? Zkuste integrovat tento pipeline do webového API, nebo experimentujte s rozpoznáváním rukopisných poznámek přidáním `new BinarizationFilter()` před deskewingem. Možnosti jsou neomezené – šťastné kódování!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}