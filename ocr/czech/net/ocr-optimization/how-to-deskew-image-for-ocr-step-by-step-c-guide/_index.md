---
category: general
date: 2026-03-04
description: Naučte se, jak vyrovnat zkosení obrázku a rozpoznat text z obrázku pomocí
  úpravy kontrastu pro zlepšení přesnosti OCR a vylepšení obrázku pro OCR.
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: cs
og_description: Jak vyrovnat sklon obrazu a zvýšit výsledky OCR. Naučte se aplikovat
  kontrast, zlepšit přesnost OCR a rozpoznávat text z obrázku pomocí opakovaně použitelných
  pracovních postupů.
og_title: Jak vyrovnat zkosení obrázku – Kompletní C# OCR tutoriál
tags:
- OCR
- C#
- image‑processing
title: Jak vyrovnat obrázek pro OCR – krok za krokem průvodce v C#
url: /cs/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak narovnat obrázek – Kompletní C# OCR tutoriál

Už jste se někdy zamysleli nad tím, **jak narovnat obrázek**, aby váš OCR engine skutečně četl text? Nejste v tom sami. V mnoha reálných projektech – naskenované účtenky, vyfocené smlouvy nebo rozmazané účtenky z fotoaparátu telefonu – není obrázek dokonale svislý. Nakloněná stránka změní rozpoznávač znaků a výsledek je jen chaotický nesmysl.

Dobrá zpráva? Když obrázek narovnáte **a** upravíte kontrast, můžete dramaticky **zlepšit přesnost OCR**. V tomto tutoriálu projdeme kompletním C# příkladem, který vám přesně ukáže, **jak rozpoznat text z obrázku** po aplikaci filtru pro narovnání a zvýšení kontrastu. Také vysvětlíme, **jak správně aplikovat kontrast**, probereme okrajové případy a poskytneme vám znovupoužitelný pipeline, který můžete vložit do jakéhokoli projektu.

## Co získáte z tohoto průvodce

- Jasné vysvětlení, proč jsou pro OCR důležité narovnání a kontrast.
- Připravený C# ukázkový kód, který vytvoří filtr pipeline, připojí jej k OCR engine a načte více obrázků.
- Tipy, jak znovu použít stejný pipeline pro mnoho souborů, jak zacházet s chybovými případy a měřit zvýšení přesnosti.
- Odkazy na související témata jako binarizace obrázku, odstraňování šumu a vícejazykové OCR (vše bez opuštění stránky).

**Požadavky** – potřebujete prostředí .NET 6+, OCR knihovnu, která podporuje filtr pipeline (např. Tesseract‑.NET, IronOCR nebo jakýkoli komerční SDK) a pár ukázkových PNG souborů. Žádné externí služby nejsou vyžadovány.

---

## Krok 1 – Proč je narovnání první věc, kterou byste měli udělat

Pokud je naskenovaná stránka otočena i jen o několik stupňů, OCR engine vidí základní linii každého řádku pod úhlem. Většina rozpoznávačů předpokládá horizontální text; jakýkoli odklon snižuje skóre důvěry a zavádí chyby nahrazení.

> **Tip:** Pokud můžete, pořiďte obrázek na rovné ploše a při dobrém osvětlení; softwarové opravy nemohou plně nahradit kvalitní data.

V programátorských termínech „jak narovnat obrázek“ obvykle znamená detekci dominantní orientace textových řádků a otočení bitmapy zpět na 0°. Většina OCR SDK poskytuje `DeskewFilter`, který to provádí automaticky.

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

Filtr funguje na předpokladu, že stránka obsahuje více textu než pozadí, což platí pro většinu dokumentů. Pokud máte fotografii s velkým množstvím bílého prostoru, můžete potřebovat záložní algoritmus – ale pro většinu naskenovaných PDF výchozí nastavení funguje dobře.

---

## Krok 2 – Zvýšení kontrastu pro lepší viditelnost znaků

Kontrast je rozdíl mezi nejtmavšími a nejjasnějšími pixely. Skeny s nízkým kontrastem vypadají vybledlé a OCR engine nedokáže určit, kde znak začíná a končí. Zvýšením kontrastu „zaostříme“ vizuální oddělení, což **zlepšuje přesnost OCR**.

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

Proč 1.2? V praxi stačí mírné zvýšení (10‑30 %). Pokud to posunete příliš daleko, ztratíte jemné detaily, zejména u tenkých fontů. Klidně experimentujte; pipeline, kterou později vytvoříme, vám umožní upravit úroveň bez nutnosti překladu celé aplikace.

---

## Krok 3 – Vytvoření znovupoužitelného filtr pipeline

Nyní spojíme oba filtry do jedné pipeline. Tímto způsobem **rozpoznáte text z obrázku** se stejným předzpracováním pokaždé, což zajišťuje konzistentní výsledky.

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**Proč pipeline?**  
- **Modularita:** Přidávejte nebo odstraňujte filtry bez zásahu do volání OCR.  
- **Výkon:** Knihovna může provádět operace dávkově, snižuje zatížení paměti.  
- **Znovupoužitelnost:** Připojte stejnou pipeline k více voláním `engine.Recognize`.

---

## Krok 4 – Připojení pipeline k OCR engine

Většina OCR engine nabízí vlastnost `Filters` nebo metodu `SetFilters`. Při přiřazení naší pipeline zde projde každá následující obrázek procesem narovnání + kontrastu, než začne samotná analýza znaků.

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

Pokud potřebujete změnit jazykový model (např. English → Spanish), můžete to udělat **před** připojením filtrů; pořadí není pro fázi předzpracování důležité.

---

## Krok 5 – Rozpoznání textu z prvního obrázku

Vyzkoušme pipeline v praxi. Načteme PNG, spustíme OCR a vytiskneme výsledek. Všimněte si, že používáme stejnou instanci `engine` – není potřeba znovu vytvářet filtry.

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**Co byste měli vidět:** Čistý, správně orientovaný text s mnohem méně zkreslenými znaky než by poskytl surový sken. Pokud stále vidíte chyby, zvažte přidání `BinarizeFilter` (převod na čistou černobílou) po kroku kontrastu.

---

## Krok 6 – Znovupoužití stejné pipeline pro další soubory

Jednou z největších výhod filtr pipeline je, že ji můžete znovu použít napříč desítkami souborů bez dalšího zatížení.

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

Pokud máte složku plnou naskenovaných PDF, stačí projít `Directory.GetFiles(...)` a volat `engine.Recognize` pokaždé. Kroky narovnání a kontrastu zůstávají konzistentní, což je klíčové pro **vylepšení obrázku pro OCR** v dávkových úlohách.

---

## Kompletní funkční příklad – Sestavte vše dohromady

Níže je kompletní, samostatný program. Zkopírujte a vložte jej do nového konzolového projektu, přidejte odpovídající NuGet balíček pro vaše OCR SDK a spusťte. Vypíše rozpoznaný text pro dva ukázkové obrázky.

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### Očekávaný výstup

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

Pokud porovnáte tento výstup s během **bez** filtr pipeline, pravděpodobně uvidíte chybějící znaky, nesprávně umístěná čísla nebo úplně zkreslené řádky. To je měřitelný dopad správného **narovnání obrázku** a **aplikace kontrastu**.

---

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Co když je obrázek již svislý?* | `DeskewFilter` detekuje rotaci 0° a vrátí původní bitmapu, takže téměř žádné zatížení nepřináší. |
| *Mohu to použít s PDF?* | Ano. Většina OCR SDK umožňuje načíst stránku PDF jako `ImageInfo`. Stejná pipeline funguje, protože podkladová bitmapa je zpracována identicky. |
| *Moje dokumenty mají barevný text – zničí kontrast barvy?* | Kontrastní filtr pracuje s luminancí, takže barvy jsou zachovány, ale stávají se výraznějšími. Pokud potřebujete čistou černobílou, přidejte `BinarizeFilter` po kroku kontrastu. |
| *Jak změřím zlepšení přesnosti?* | Spusťte OCR na testovací sadě před a po pipeline a vypočítejte míru chyb znaků (CER) nebo slov (WER). Obvykle uvidíte pokles chyb o 10‑30 %. |
| *Má to dopad na výkon?* | Narovnání přidává malou zátěž CPU (obvykle < 100 ms na stránku). Kontrast je jednoduchá operace po jednotlivých pixelech, takže celkový dopad je minimální ve srovnání s samotným krokem OCR. |

---

## Další kroky – Posuňte své OCR na vyšší úroveň

Nyní, když víte **jak narovnat obrázek**, **jak aplikovat kontrast** a **jak rozpoznat text z obrázku** pomocí znovupoužitelné pipeline, zvažte prozkoumání těchto souvisejících témat:

- **Redukce šumu** – přidejte `MedianFilter` před narovnáním pro odstranění špiček.
- **Binarizace** – převod na čistou černobílou pro jazyky s komplexními skripty.
- **Zpracování více stránek** – projděte stránky PDF a uložte výsledky do prohledávatelného indexu.
- **Jazykové modely** – přepínejte mezi `OcrLanguage.English` a `OcrLanguage.French` za běhu.
- **Post‑zpracování** – použijte kontrolu pravopisu nebo regex pro opravu běžných OCR chyb (např. „0“ vs „O“).

Každý z nich lze vložit do stejného řetězce `FilterBuilder`, čímž získáte modulární, udržovatelný řešení, které **vylepšuje obrázek pro OCR** v jakémkoli produkčním pipeline.

---

## Závěr

Probrali jsme vše, co potřebujete vědět o **tom, jak narovnat obrázek** pro OCR, proč úprava kontrastu je levný, ale výkonný způsob, jak **zlepšit přesnost OCR**, a jak **rozpoznat text z obrázku** pomocí čistého, znovupoužitelného

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}