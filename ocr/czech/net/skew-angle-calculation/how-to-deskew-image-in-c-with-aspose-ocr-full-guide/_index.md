---
category: general
date: 2026-03-23
description: Jak vyrovnat obrázek pomocí Aspose OCR v C#. Naučte se, jak odstranit
  šum, opravit rotaci obrázku a rozpoznat text z obrázku během několika minut.
draft: false
keywords:
- how to deskew image
- how to remove noise
- recognize text from image
- remove salt pepper noise
- correct image rotation
language: cs
og_description: Jak rychle vyrovnat sklon obrázku pomocí Aspose OCR. Tento průvodce
  také ukazuje, jak odstranit šum, opravit rotaci obrázku a rozpoznat text z obrázku.
og_title: Jak vyrovnat zkosení obrázku v C# – Kompletní tutoriál Aspose OCR
tags:
- OCR
- C#
- Image Preprocessing
title: Jak vyrovnat obrázek v C# s Aspose OCR – Kompletní průvodce
url: /cs/net/skew-angle-calculation/how-to-deskew-image-in-c-with-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opravit sklon obrazu v C# – Kompletní tutoriál Aspose OCR

Už jste se někdy zamýšleli **jak opravit sklon obrazu** souborů, které pocházejí ze skeneru, jenž je mírně nakřivo? Nejste v tom sami. V mnoha reálných projektech je zdrojový obrázek nakloněn o několik stupňů, posetý šumem typu sůl‑a‑pepř, a přesto je potřeba jej přečíst jako prostý text.

Dobrá zpráva? S Aspose OCR můžete opravit otočení, odstranit šum a poté **rozpoznat text z obrázku**—vše během několika řádků. V tomto tutoriálu projdeme celým procesem, vysvětlíme, proč je každý filtr důležitý, a poskytneme vám připravený C# program.

> *Tip:* Pokud jste ještě nikdy nepoužili Aspose OCR, stáhněte si bezplatnou zkušební verzi z webu Aspose; API funguje hned po instalaci s .NET 6+.

---

## Co budete potřebovat

- **.NET 6 SDK** (nebo jakákoli recentní verze .NET) – kód se kompiluje ve Visual Studio, Rider nebo pomocí `dotnet` CLI.  
- **Aspose.OCR NuGet balíček** – nainstalujte pomocí `dotnet add package Aspose.OCR`.  
- **Ukázkový obrázek**, který je mírně natočený a obsahuje šum (např. `skewed.png`).  
- Základní znalost C# – nemusíte být expert, stačí vám pohodlná práce s `using` příkazy a konzolí.

To je vše. Žádné další OCR enginy, žádné nativní DLL, jen jediná reference na NuGet.

---

## Jak opravit sklon obrazu – Přehled krok za krokem

Níže rozdělíme proces do logických kroků. Každý krok má jasný nadpis, úryvek kódu a krátký odstavec „proč“, abyste pochopili důvod volání.

![příklad jak opravit sklon obrazu](https://example.com/deskew-demo.png "jak opravit sklon obrazu")

### Krok 1: Nastavení OCR enginu

Nejprve vytvoříme instanci `OcrEngine`. Blok `using` zajišťuje správné uvolnění prostředků, čímž okamžitě uvolní nativní zdroje, jakmile skončíme.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Step 1 – instantiate the OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the pipeline goes here...
        }
    }
}
```

*Proč je to důležité:* `OcrEngine` je jádrem Aspose OCR. Uchovává obrázek, řetězec filtrů a nastavení rozpoznávání. Zabalení do `using` zabraňuje únikům paměti, zejména při zpracování desítek stránek v dávkovém úkolu.

### Krok 2: Načtení naskenovaného obrázku

Soubor načteme pomocí `ImageStream.FromFile`. Cesta může být absolutní nebo relativní k pracovnímu adresáři spustitelného souboru.

```csharp
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");
```

*Proč je to důležité:* Engine pracuje s obrazovým proudem v paměti. Poskytnutí správné cesty je jediným místem, kde vás může „kousnout“ `FileNotFoundException`, proto před spuštěním dvakrát zkontrolujte strukturu složek.

### Krok 3: Přidání předzpracovatelských filtrů

Zde odpovídáme na **jak odstranit šum** a **opravit otočení obrázku**. Dva vestavěné filtry vykonají těžkou práci:

```csharp
// DeskewFilter corrects small rotation (usually up to ±5°)
ocrEngine.Filters.Add(new DeskewFilter());

// DenoiseFilter removes salt‑and‑pepper noise
ocrEngine.Filters.Add(new DenoiseFilter());
```

*Proč tyto filtry?*  
- **DeskewFilter** analyzuje základní linie textu, vypočítá úhel sklonu a otočí bitmapu zpět do vodorovné polohy. Bez něj může OCR engine špatně interpretovat znaky (např. „l“ vs. „i“).  
- **DenoiseFilter** používá medianový algoritmus, který vyhlazuje izolované černé/bílé pixely – přesně to, co v žargonu zpracování obrazu znamená „odstranit šum typu sůl‑a‑pepř“. To výrazně zvyšuje skóre důvěry.

Pokud máte silně rozmazaný sken, můžete předtím přidat `SharpenFilter`, ale to je volitelná úprava.

### Krok 4: Spuštění OCR rozpoznání

Nyní požádáme Aspose OCR, aby odvedl svou práci. Metoda `Recognize` vrací boolean indikující úspěch.

```csharp
if (ocrEngine.Recognize())
{
    // Step 5 – output the cleaned text
    Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed – check the image and filter configuration.");
}
```

*Proč kontrolujeme výsledek:* Občas engine nenajde žádný text (např. prázdná stránka). Ošetření případu `false` zabraňuje tichému selhání, které by bylo později těžko laditelné.

### Krok 5: Ověření výstupu

Když spustíte program, měli byste vidět něco jako:

```
Cleaned text:
The quick brown fox jumps over the lazy dog.
```

Pokud text stále vypadá poškozeně, zvažte:
- **Zvýšení tolerance deskew** – `new DeskewFilter(0.1)` umožní filtru akceptovat větší úhly.  
- **Přidání `BinarizeFilter`** před denoisingem pro převod obrázku na čistou černobílou verzi.  
- **Kontrola DPI** – skeny s nízkým rozlišením (< 150 dpi) často potřebují před OCR upscale.

## Jak odstranit šum – Pokročilé možnosti

Základní `DenoiseFilter` funguje dobře pro typické skvrny skeneru, ale někdy se setkáte s **odstraněním šumu typu sůl‑a‑pepř** na starších filmových skenech. V takových případech:

```csharp
// Apply a stronger median filter (kernel size 3x3)
ocrEngine.Filters.Add(new DenoiseFilter { KernelSize = 3 });
```

Nebo řetězte **GaussianBlurFilter** před denoisingem:

```csharp
ocrEngine.Filters.Add(new GaussianBlurFilter { Sigma = 0.8 });
ocrEngine.Filters.Add(new DenoiseFilter());
```

Tyto úpravy vymění malé množství ostrosti za čistší binární obrázek, což obvykle zvýší skóre důvěry OCR o 5‑10 %.

## Rozpoznání textu z obrázku – Tipy na post‑processing

Po získání `ocrEngine.Text` můžete chtít:
- **Oříznout mezery** – `ocrEngine.Text = ocrEngine.Text.Trim();`  
- **Normalizovat konce řádků** – `ocrEngine.Text = ocrEngine.Text.Replace("\r\n", "\n");`  
- **Spustit kontrolu pravopisu** pomocí `System.Globalization` nebo knihovny třetí strany, pokud zdrojový jazyk není angličtina.

Všechny tyto kroky připraví extrahovaný řetězec pro následné zpracování, například pro naplnění vyhledávacího indexu nebo formuláře pro zadávání dat.

## Hraniční případy a běžné úskalí

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| Obrázek otočený > 10° | `DeskewFilter` zastavuje při svém výchozím limitu | Předat vlastní maximální úhel: `new DeskewFilter { MaxAngle = 15 }` |
| Velmi tmavé pozadí | Filtry mohou interpretovat pozadí jako text | Přidat `InvertColorsFilter` nebo zvýšit kontrast |
| Vícestránkový PDF | `OcrEngine` pracuje s jedním obrázkem najednou | Iterovat přes každou stránku, vytvářet nový `OcrEngine` v každé iteraci |
| Neliterní skript | Výchozí jazyk je angličtina | Nastavit `ocrEngine.Language = OcrLanguage.Thai;` (nebo jakýkoli podporovaný jazyk) |

Mít tyto věci na paměti vám ušetří klasický noční můru „Proč je můj OCR výstup prázdný?“.

## Kompletní funkční příklad

Zkopírujte níže uvedený kód do nového konzolového projektu (`dotnet new console -n OcrDemo`). Obnovte balíček Aspose OCR, nahraďte `YOUR_DIRECTORY/skewed.png` cestou k vašemu testovacímu obrázku a spusťte.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Initialize OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Load the image that may be slightly rotated
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");

            // Add preprocessing filters
            //   - DeskewFilter corrects small rotation
            //   - DenoiseFilter removes salt‑and‑pepper noise
            ocrEngine.Filters.Add(new DeskewFilter());
            ocrEngine.Filters.Add(new DenoiseFilter());

            // Perform OCR recognition
            if (ocrEngine.Recognize())
            {
                // Output the cleaned text
                Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – verify the image and filters.");
            }
        }
    }
}
```

Spuštěním tohoto programu se na konzoli vypíše vyčištěný, opravený text. To je celý **workflow jak opravit sklon obrazu** zabalený do méně než 50 řádků kódu.

## Závěr

Právě jsme pokryli **jak opravit sklon obrazu** pomocí Aspose OCR, ukázali **jak odstranit šum**, vysvětlili **správné otočení obrázku** a předvedli spolehlivý způsob **rozpoznání textu z obrázku**. Řetězením `DeskewFilter` a `DenoiseFilter` získáte ostrý, narovnaný bitmap, který OCR engine může číst s vysokou důvěrou.

Zde můžete dále zkoumat:
- Dávkové zpracování desítek skenů paralelně.  
- Export výsledku OCR do PDF/A pro archivaci.  
- Integraci detekce jazyka pro vícejazyčné dokumenty.

Vyzkoušejte tyto nápady a nebojte se upravit parametry filtrů podle vašich konkrétních skenů. Šťastné programování a ať jsou vaše obrázky vždy dokonale rovné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}