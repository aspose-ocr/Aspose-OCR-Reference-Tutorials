---
category: general
date: 2026-01-15
description: Naučte se, jak pomocí Aspose OCR provádět OCR arabského textu a rozpoznávat
  hindské texty. Tento krok‑za‑krokem průvodce vám ukáže, jak efektivně extrahovat
  text z obrázku a převést obrázek na text.
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: cs
og_description: jak provést OCR arabského textu a rozpoznat hindský text v jednom
  C# programu. Postupujte podle tohoto kompletního návodu k extrakci textu z obrázku
  a převodu obrázku na text.
og_title: Jak provést OCR arabského a hindského textu pomocí Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: jak provést OCR arabského a hindského textu pomocí Aspose OCR
url: /cs/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak OCR-ovat arabský a hindský text pomocí Aspose OCR

Už jste se někdy zamysleli nad tím, **jak OCR-ovat arabské** znaky, které běží zprava doleva, a zároveň získat hindské glyfy z účtenky? Nejste sami. Mnoho vývojářů narazí na stejný problém, když potřebují **rozpoznat arabský text** a **rozpoznat hindský text** ve stejném pracovním postupu.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem v C#, který vám ukáže, jak **extrahovat text z obrázku** souborů, **převést obrázek na text**, a jak pracovat s arabským i hindským skriptem pomocí Aspose OCR. Žádné nejasné odkazy – jen kód, který můžete zkopírovat a vložit, plus vysvětlení každého řádku.

> **Pro tip:** Pokud jste ještě nikdy nepoužili Aspose OCR, nejprve nainstalujte NuGet balíček `Aspose.OCR`. Jedná se o operaci jedním kliknutím ve Visual Studiu a stáhne všechny nativní binární soubory, které potřebujete pro rozpoznávání na CPU.

![jak OCR-ovat arabské – ukázka arabského nápisu](/images/arabic-ocr-sample.png "jak OCR-ovat arabské – ukázka arabského nápisu")

*Text obrázku:* **jak OCR-ovat arabské – ukázka arabského nápisu**  

## jak OCR-ovat arabské – nastavení prostředí

Než se ponoříme do kódu, ujistěme se, že vývojové prostředí je připravené.

1. **Target framework** – .NET 6.0 nebo novější. Starší verze se stále zkompilují, ale omezí vás to na nejnovější jazykové funkce.  
2. **Package** – Spusťte `dotnet add package Aspose.OCR` v terminálu nebo použijte UI NuGet Package Manager.  
3. **Images** – Umístěte dva ukázkové obrázky do složky, na kterou můžete odkazovat, např. `C:\OCRSamples\arabic_sign.jpg` a `C:\OCRSamples\hindi_receipt.png`. Arabský obrázek by měl obsahovat jasné, vysokokontrastní arabské znaky; hindský obrázek může být naskenovaná účtenka nebo fotografie nápisu.  

A to je vše – žádné extra konfigurační soubory, žádné GPU ovladače, jen přímočarý OCR engine založený na CPU.

## Rozpoznat arabský text – načtení a zpracování

Nyní skutečně **rozpoznáme arabský text**. Klíčové je říct enginu, jaký jazyk očekává; jinak engine výchozí nastavení použije latinské znaky a získáte nesmyslný výstup.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Proč to funguje:**  
* `OcrEngine` zajišťuje veškerou těžkou práci – předzpracování, segmentaci a klasifikaci znaků.  
* Předáním `Language.Arabic` aktivujeme engine pro rozložení zprava doleva a arabskou znakovou sadu. Bez toho by engine považoval obrázek za levostranný latinský text, což vede k chybějícím diakritikám a rozbitým slovům.  

**Očekávaný výstup** (váš skutečný text se bude lišit podle obrázku):

```
Arabic: مرحبا بكم في متجرنا
```

Pokud vidíte prázdné řetězce, zkontrolujte, že obrázek není příliš tmavý a že cesta k souboru je správná.  

## extrahovat text z obrázku – zpracování skriptů zprava doleva

Arabština není jediný skript, který vyžaduje speciální zpracování. Jazyky zprava doleva (RTL) vyžadují, aby OCR engine po rozpoznání obrázek vizuální pořadí obrátil. Aspose to provádí automaticky, když specifikujete `Language.Arabic`, ale stojí za zmínku pro budoucí rozšíření (např. hebrejština).

*Tip:* Když později zobrazujete výsledek OCR v UI, ujistěte se, že ovládací prvek podporuje RTL vykreslování; jinak se text zobrazí rozmazaně.

## převést obrázek na text – práce s hindštinou

Přepínáme, pojďme **převést obrázek na text** pro hindskou účtenku. Proces je podobný arabskému, ale použijeme `Language.Hindi`.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Proč znovu používáme stejnou instanci `ocrEngine`:**  
Vytvoření nového engine pro každý jazyk by plýtvalo pamětí a časem inicializace. Engine Aspose je vlákny‑bezpečný pro sekvenční volání, takže jeho opětovné použití je jak efektivní, tak čisté.

**Ukázkový výstup v konzoli** (opět závisí na vašem obrázku):

```
Hindi: कुल राशि: ₹ 1,250.00
```

Pokud hindský text vypadá jako nesmyslné latinské znaky, pravděpodobně jste vynechali jazykový enum nebo je rozlišení obrázku příliš nízké (<300 dpi). Zvětšení obrázku nebo aplikace jednoduchého binarizačního filtru může výrazně zlepšit přesnost.

## rozpoznat hindský text – běžné úskalí a okrajové případy

I přesto, že máte správný jazykový příznak, může vás pár potíží zaskočit:

| Issue | Symptom | Fix |
|-------|---------|-----|
| Nízký kontrast | Mnoho znaků se změní na „?“ nebo jsou vynechány | Předzpracujte pomocí `OcrImage.AdjustContrast(1.5)` |
| Šikmý obrázek | Text se zobrazí otočený, OCR vrátí prázdný řetězec | Zavolejte `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| Smíšené jazyky | Arabská řádka následovaná anglickými čísly | Spusťte dva průchody: nejprve s `Language.Arabic`, poté s `Language.English` na stejném obrázku a výsledek spojte |
| Velký soubor | Pomalé rozpoznávání nebo chyby nedostatku paměti | Zmenšete na maximální šířku 2000 px pomocí `OcrImage.Resize(2000, 0)` |

Tyto tipy vám pomohou **extrahovat text z obrázku** souborů, které nejsou dokonale naskenované, což je běžné v reálných projektech.

## Složení všeho dohromady – kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat přímo do nového konzolového projektu. Žádné skryté závislosti, žádná extra konfigurace – jen čistý C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Spuštění programu** vytiskne jak arabské, tak hindské řetězce do konzole, což potvrdí, že jste úspěšně **rozpoznali arabský text** a **rozpoznali hindský text** v jednom běhu.  

## Závěr

Nyní máte solidní, end‑to‑end odpověď na otázku **jak OCR-ovat arabské** a zároveň zpracovat hindštinu. Vytvořením jediné instance `OcrEngine`, načtením každého obrázku a předáním příslušného enumu `Language` můžete **extrahovat text z obrázku**, **převést obrázek na text** a **rozpoznat arabský text** i **rozpoznat hindský text** bez jakýchkoli extra knihoven.

From here you might explore:

* **Batch processing** – procházet složku s obrázky a ukládat výsledky do databáze.  
* **Post‑processing** – použít regulární výrazy k vyčištění symbolů měny v hindských účtenkách.  
* **Hybrid language detection** – poslat surový bitmap do modelu pro detekci jazyka před výběrem enumu.  

Vyzkoušejte to, upravte kroky předzpracování a uvidíte, jak rychle se přesnost OCR zvyšuje. Pokud narazíte na nějaké problémy, dejte

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}