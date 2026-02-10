---
category: general
date: 2026-02-09
description: Rychle extrahujte text z obrázků pomocí C# nastavením maximální paralelnosti
  pro dávkové OCR – naučte se převádět naskenované stránky, zpracovávat OCR u více
  obrázků a efektivně číst text z PNG.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: cs
og_description: extrahovat text z obrázků v C# nastavením maximální paralelnosti.
  Tento tutoriál ukazuje, jak převést naskenované stránky, spustit OCR na více obrázcích
  a číst text z PNG pomocí Aspose OCR.
og_title: Extrahujte textové obrázky z PNG pomocí C# – Kompletní průvodce dávkovým
  OCR
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Extrahovat textové obrázky z PNG souborů pomocí C# – Dávkové OCR pomocí Aspose
  OCR
url: /cs/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extrahovat textové obrázky z PNG pomocí C# – Dávkový OCR s Aspose OCR

Už jste někdy potřebovali **extrahovat textové obrázky** ze složky naskenovaných PNG, ale uvízli jste u otázky „jak to udělat rychle?“? Nejste v tom sami. V mnoha reálných projektech musí vývojáři **nastavit maximální paralelismus**, aby se desítky stránek zpracovávaly během sekund místo minut.  

V tomto průvodci projdeme kompletním, spustitelným příkladem, který **převádí naskenované stránky**, provádí **víceobrazový OCR** a nakonec **čte text z PNG** bez potíží. Žádné vágní odkazy „viz dokumentace“ — jen kód, který můžete zkopírovat‑vložit, vysvětlení, proč je každý řádek důležitý, a tipy, jak se vyhnout běžným úskalím.

> **Pro tip:** Pokud už někde používáte Aspose OCR, všimnete si, že se zde objevuje stejná třída `OcrEngine`, ale upravíme její konfiguraci pro skutečné paralelní zpracování.

---

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6+). API funguje stejně, ale novější runtime poskytují lepší správu vláken.  
- **Aspose.OCR for .NET** – nainstalujte přes NuGet: `Install-Package Aspose.OCR`.  
- Složka obsahující několik PNG skenů (`page1.png`, `page2.png`, …).  
- IDE nebo editor, ve kterém se cítíte pohodlně (Visual Studio, Rider, VS Code…).

A to je vše. Žádné extra služby, žádné cloudové klíče, jen čisté lokální zpracování.

---

## extrahovat textové obrázky – Nastavení maximálního paralelismu pro dávkový OCR

Když spustíte OCR na několika souborech, engine ve výchozím nastavení použije jeden vlákno. To je bezpečné, ale bolestivě pomalé. Nastavením `MaxDegreeOfParallelism` řeknete enginu, kolik vláken může současně spustit.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Proč 4?**  
Čtyři je optimální hodnota na většině moderních notebooků — dostatek jader, aby CPU byl vytížený, ale ne tolik, aby se ostatní procesy dusily. Pokud to spouštíte na serveru se 16 jádry, zvyšte číslo na 12 nebo 14 pro znatelný nárůst rychlosti.

---

## Převod naskenovaných stránek – Vytvoření kolekce Image Stream

Aspose očekává každý obrázek jako `ImageStream`. Pomocná metoda `FromFile` načte soubor, uchová jej v paměti a předá OCR enginu. Můžete také použít `MemoryStream`, pokud obrázky pocházejí z databáze nebo HTTP odpovědi.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Hraniční případ:** Pokud některý soubor chybí nebo je poškozený, `FromFile` vyhodí `FileNotFoundException`. Zabalte konstrukci do `try/catch`, pokud očekáváte nespolehlivý vstup.

---

## víceobrazový OCR – Provádění dávkového OCR

Nyní se provádí těžká část. `RecognizeBatch` spustí až tolik vláken, kolik jste dříve nastavili, zpracuje každý obrázek a vrátí seznam objektů `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Za scénou každé vlákno načte svůj obrázek, spustí neuronovou síť a extrahuje čistý text. Pořadí výsledků odpovídá pořadí vstupního seznamu, takže můžete bezpečně mapovat stránka 1 → výsledek 0 a tak dále.

---

## číst text z PNG – Zobrazení extrahovaného obsahu

Nakonec projdeme výsledky a vypíšeme čistý text do konzole. Zde můžete výstup přesměrovat do souboru, databáze nebo dokonce do následné NLP služby.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Očekávaný výstup v konzoli

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Pokud vidíte prázdné sekce, zkontrolujte, že PNG nejsou čistě bílé obrázky — OCR potřebuje určitý kontrast.

---

## Praktické tipy a běžné úskalí

| Situace | Co dělat |
|-----------|------------|
| **Tlak na paměť** při velkých dávkách | Zpracovávejte obrázky po částech po 10‑20 souborech a poté zavolejte `GC.Collect()`, pokud zaznamenáte špičky. |
| **Nesprávná detekce jazyka** | Nastavte `ocrEngine.Configuration.Language = OcrLanguage.English;` (nebo požadovaný jazyk) před voláním `RecognizeBatch`. |
| **Pomalý výkon i přes paralelismus** | Ověřte, že váš SSD neomezuje I/O; načtěte všechny soubory nejprve do paměti (jako děláme s `ImageStream.FromFile`). |
| **Chybějící znaky** | Zvyšte `ocrEngine.Configuration.DPI = 300;` pro zpracování ve vyšším rozlišení. |

---

## Rozšíření příkladu – z PNG na PDF nebo DOCX

Pokud nakonec potřebujete **převést naskenované stránky** do prohledávatelných PDF, jednoduše předáte stejný `ocrResults[i].PlainText` do PDF knihovny (např. Aspose.PDF) a překryjete text jako neviditelnou vrstvu. Stejný trik s paralelismem funguje i zde.

---

## Kompletní zdrojový kód (připravený ke kopírování)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Uložte tento soubor jako `BatchExample.cs`, spusťte `dotnet run` a sledujte, jak se vaše konzole naplní textem, který byl dříve skrytý v těch PNG skenech.

---

## Vizuální shrnutí

![extract text images example](images/ocr-batch.png){alt="extract text images example"}

Diagram ukazuje tok: **PNG soubory → kolekce ImageStream → OcrEngine (max paralelismus) → OCR výsledky → Konzole / následné úložiště**.

---

## Závěr

Nyní máte solidní, end‑to‑end návod, jak **extrahovat textové obrázky** v C# při **nastavení maximálního paralelismu**, **převodu naskenovaných stránek**, zpracování **víceobrazového OCR** a **čtení textu z PNG** efektivně. Kód je samostatný, vysvětlení pokrývají jak „jak“, tak „proč“, a tipy vás chrání před běžnými problémy.

Co dál? Zkuste nahradit seznam PNG dynamickým `Directory.GetFiles` cyklem, experimentujte s různým počtem vláken nebo výstup přesuňte do prohledávatelného PDF. Stejný vzor škáluje na stovky stránek s téměř žádným dalším kódem.

Máte otázky nebo složitý hraniční případ? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}