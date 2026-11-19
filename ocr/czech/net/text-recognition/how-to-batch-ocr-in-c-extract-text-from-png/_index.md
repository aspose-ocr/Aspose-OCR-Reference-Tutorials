---
category: general
date: 2026-03-26
description: Jak provádět hromadné OCR v C# usnadňuje extrakci textu z PNG souborů.
  Postupujte podle tohoto krok za krokem C# OCR tutoriálu pro hromadnou extrakci textu
  s Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: cs
og_description: Jak provádět dávkové OCR v C# vám umožní rychle extrahovat text z
  PNG souborů. Tento průvodce vás provede kompletním tutoriálem OCR v C# s dávkovým
  extrahováním textu.
og_title: Jak provádět dávkové OCR v C# – Extrahovat text z PNG
tags:
- OCR
- C#
- Aspose
title: Jak provádět dávkové OCR v C# – Extrahovat text z PNG
url: /cs/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět hromadné OCR v C# – Extrahovat text z PNG

Už jste se někdy zamýšleli **jak provádět hromadné OCR** na hromadě snímků obrazovky, aniž byste museli psát samostatný program pro každý soubor? Nejste v tom sami. V mnoha projektech skončíme s desítkami PNG, ze kterých je potřeba získat text, a dělat to po jednom je otravné.  

Dobrá zpráva? S Aspose OCR můžete spustit malou C# konzolovou aplikaci, která zpracuje všechny tyto obrázky paralelně, což vám poskytne rychlé **hromadné získávání textu** a čistý výstupní soubor. V tomto průvodci projdeme kompletní **c# ocr tutorial**, vysvětlíme, proč je každá část důležitá, a ukážeme vám přesně, jak vypadá výstup.

Na konci tohoto článku budete umět:

* Načíst seznam PNG souborů (nebo jakéhokoli podporovaného obrázku) najednou.  
* Nakonfigurovat sdílený `OcrEngine`, aby nastavení zůstala konzistentní po celou dávku.  
* Spustit frontu rozpoznávání až se čtyřmi paralelními pracovníky.  
* Získat rozpoznaný text pro každou stránku a vypsat jej do konzole.

Žádná magie, jen solidní kód, který můžete dnes vložit do svého řešení.

## Co budete potřebovat

Než se ponoříme dál, ujistěte se, že máte:

* .NET 6 SDK (nebo jakoukoli novější verzi .NET).  
* Platnou licenci Aspose OCR nebo dočasný evaluační klíč.  
* Složku, která obsahuje PNG soubory, jež chcete zpracovat.  
* Visual Studio 2022 nebo váš oblíbený editor.

To je vše — žádné další NuGet balíčky kromě `Aspose.OCR` a standardní `System.Collections.Generic`.

## Jak nastavit projekt pro hromadné OCR

Nejprve vytvořte nový konzolový projekt a přidejte knihovnu Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Po dokončení obnovení otevřete **Program.cs** (nebo vytvořte nový soubor) a přidejte obvyklé `using` direktivy:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Tato jednoduchá struktura nám poskytuje přístup k `OcrEngine`, `RecognitionQueue` a pomocným třídám, které budeme později potřebovat.

## Extrahování textu z PNG — příprava seznamu obrázků

Nyní musíme programu říct, **které PNG** mají projít OCR. Nejsnazší způsob je vytvořit `List<string>`, který bude obsahovat absolutní nebo relativní cesty.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce. Pokud máte dynamickou sadu, můžete také použít `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` a výsledek vložit do seznamu. Klíčové je, že **extrahování textu z PNG** je jen otázka předání správných názvů souborů frontě.

![Jak probíhá hromadné OCR workflow](https://example.com/placeholder.png "Diagram znázorňující, jak provádět hromadné OCR kolekce PNG souborů")

*Popisek obrázku: diagram workflow hromadného OCR*

## C# OCR tutorial — konfigurace fronty rozpoznávání

Srdcem hromadné operace je `RecognitionQueue`. Představte si ji jako dopravní pás, který předává každý obrázek sdílenému `OcrEngine`. Sdílením engine udržujeme nízkou spotřebu paměti a garantujeme identická nastavení pro každou stránku.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Proč nastavit `MaxDegreeOfParallelism` na 4? Na typickém čtyřjádrovém notebooku to poskytuje nejlepší propustnost, aniž by se OS hladovělo. Pokud běžíte na serveru s více jádry, zvýšte číslo podle potřeby.

### Pro tip

Pokud potřebujete vlastní jazykové balíčky, nastavení DPI nebo ořez oblasti zájmu, udělejte to **jednou** na sdíleném `Engine` před zařazením jakýchkoli obrázků. Například:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Všechny následné rozpoznání automaticky zdědí tyto možnosti — to je podstata **jak vytvořit OCR** pipeline, která zůstává konzistentní.

## Hromadné získávání textu — zařazení obrázků a spuštění fronty

S připravenou frontou je dalším krokem vložit každý obrázek do ní. Metoda `Enqueue` přijímá instanci `OcrImage`, kterou vytvoříme ze cesty k souboru.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Jakmile jsou všechny soubory zařazeny, spustíme zpracování:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blokuje, dokud nedokončí všechny obrázky, a pak vrátí seznam, kde každý prvek odpovídá pořadí vstupu. To zaručuje, že výsledek stránky 1 je na indexu 0, stránky 2 na indexu 1 a tak dále — užitečné, když potřebujete mapovat výsledky zpět na zdrojové soubory.

## Jak vytvořit OCR — zobrazení výsledků

Nakonec vypíšeme rozpoznaný text do konzole. Zde skutečně uvidíte **hromadné získávání textu** v akci.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Když spustíte program (`dotnet run`), měli byste vidět něco jako:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Pokud některý obrázek selže (např. poškozený soubor), odpovídající `OcrResult` bude mít prázdnou vlastnost `Text` a můžete zkontrolovat `ocrResults[i].Exception` pro diagnostiku.

## Jak vytvořit OCR — tipy, okrajové případy a osvědčené postupy

### Zpracování velkých dávek

Zpracování stovek PNG může stále spotřebovávat paměť, pokud držíte všechny objekty `OcrResult` v paměti. V takových případech streamujte výstup do souboru nebo databáze hned, jakmile přijde každý výsledek:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Práce s formáty jinými než PNG

Aspose OCR také podporuje JPEG, BMP a TIFF přímo z krabice. Stačí změnit příponu souboru ve vašem seznamu nebo použít vyhledávání se zástupnými znaky. Stejné kroky **c# ocr tutorial** platí — žádné změny kódu nejsou potřeba.

### Přeskakování prázdných stránek

Pokud máte skenované PDF, které někdy obsahují prázdné stránky, můžete filtrovat výsledky:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Licenční úvahy

Evaluační verze označuje každou stránku vodoznakem. Pro produkční použití se ujistěte, že na začátku `Main` načtete svůj licenční soubor:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Ladění paralelismu

`MaxDegreeOfParallelism` má výchozí hodnotu `Environment.ProcessorCount`. Pokud zaznamenáte vysoké využití CPU nebo tlak na paměť, snižte hodnotu. Naopak, na cloudovém VM s mnoha jádry ji můžete zvýšit, abyste plně využili hardware.

## Shrnutí

Nyní máte kompletní **jak provádět hromadné OCR** řešení v C#, které **extrahuje text z PNG** souborů, spouští je paralelně a poskytuje čisté, seřazené výsledky. Sdílením jediného `OcrEngine` jste se naučili **jak vytvořit OCR** pipeline, která je úsporná na paměť i snadno udržovatelná. Tento **c# ocr tutorial** vám také ukazuje, jak škálovat na **hromadné získávání textu** pro stovky obrázků s jen několika dalšími řádky kódu.

---

### Co dál?

* Vyzkoušejte detekci jazyka (`Engine.Language = Language.AutoDetect`).  
* Experimentujte s výstupními formáty — zapište výsledky do JSON nebo CSV pro následnou analytiku.  
* Spojte toto hromadné OCR s krokem konverze PDF na obrázek, abyste zpracovali celé skenované dokumenty.

Klidně upravte paralelismus, zaměňte zdroje obrázků nebo zapojte výsledky do vyhledávacího indexu. Obloha je limit, když ovládnete **jak provádět hromadné OCR** v C#.

Šťastné kódování a ať jsou vaše OCR běhy rychlé a bez chyb!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}