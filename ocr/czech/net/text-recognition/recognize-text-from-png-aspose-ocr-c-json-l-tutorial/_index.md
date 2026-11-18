---
category: general
date: 2026-03-26
description: Rozpoznat text z PNG a extrahovat data z účtenky pomocí Aspose OCR v
  C#. Převést obrázek na JSON‑L a zpracovat účtenku pomocí OCR v kompletním příkladu.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: cs
og_description: Rozpoznat text z PNG a převést účtenky do JSON‑L pomocí Aspose OCR
  v C#. Kompletní krok‑za‑krokem kód a tipy.
og_title: Rozpoznání textu z PNG – Průvodce Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: rozpoznat text z PNG – Aspose OCR C# JSON‑L tutoriál
url: /cs/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznání textu z png – Kompletní průvodce Aspose OCR pro C#

Už jste někdy potřebovali **rozpoznat text z png** souborů, ale nebyli jste si jisti, která knihovna vám poskytne čisté výsledky po řádcích? Nejste sami. V mnoha malých firemních aplikacích je účtenka uložena jako PNG obrázek a získání částky, data nebo názvu obchodníka je každodenní problém.  

Dobrá zpráva? Několik řádků C# a knihovna **Aspose OCR** vám umožní **extrahovat text z účtenky**, pak **převést obrázek na jsonl** pro následnou analytiku. V tomto tutoriálu projdeme celým procesem – načtení PNG, spuštění OCR a zápis každého řádku do souboru JSON‑L – takže můžete **zpracovat účtenku pomocí OCR** okamžitě.

Probereme vše, co potřebujete: požadované NuGet balíčky, kompletní spustitelný program, vysvětlení, proč je každý krok důležitý, a několik praktických tipů, které oceníte, když se účtenky stanou nečitelné. Žádná externí dokumentace není potřeba; stačí zkopírovat, spustit a upravit.

---

## Co se naučíte

- Jak **rozpoznat text z png** pomocí `Aspose.OCR`.
- Jak **extrahovat text z účtenky** jako objekty řádků a zachytit skóre důvěry.
- Jak **převést obrázek na jsonl**, aby se každý OCR řádek stal samostatným JSON objektem.
- Jak **zpracovat účtenku pomocí OCR** end‑to‑end, včetně ošetření okrajových případů jako prázdné obrázky nebo řádky s nízkou důvěrou.
- Tipy pro řešení běžných problémů OCR a zvyšování přesnosti.

### Předpoklady

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework).
- Visual Studio 2022 nebo jakékoli IDE, které preferujete.
- Platná licence Aspose OCR (můžete začít s bezplatnou dočasnou licencí z Aspose.com).
- Ukázková účtenka uložena **jako `receipt.png`** ve složce, ke které máte přístup.

---

## Krok 1: Rozpoznání textu z png pomocí Aspose OCR

Prvním, co potřebujeme, je inicializovaný `OcrEngine`. Tento objekt obsahuje nastavení OCR enginu (jazyk, režim detekce atd.). Ve výchozím nastavení používá angličtinu a automaticky detekuje rozvržení stránky, což funguje dobře pro většinu účtenek.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Proč je to důležité:**  
`OcrEngine` je komponenta provádějící těžkou práci; vytvoření jedné instance a **její opakované používání** napříč mnoha obrázky snižuje **paměťové** zatížení. Pokud **potřebujete** jiný **jazyk** (např. španělské účtenky), můžete před voláním `Recognize` nastavit `ocrEngine.Language = OcrLanguage.Spanish;`.

---

## Krok 2: Extrahování textu z řádků účtenky

`OcrResult` obsahuje kolekci nazvanou `Lines`. Každý řádek obsahuje surový text a skóre důvěry (0‑100). Vytažením těchto informací získáte detailní kontrolu – můžete zahodit řádky s nízkou důvěrou nebo je označit k ruční kontrole.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Proč escapovat JSON:**  
Text účtenky může obsahovat uvozovky (`"`) nebo zpětná lomítka (`\`), která by rozbila naivní JSON řetězec. Metoda `EscapeJson` zaručuje platný JSON řádek.

**Jak výstup vypadá:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Každý řádek je samostatný záznam, ideální pro streamování do datového jezera nebo pro napájení modelu strojového učení.

---

## Krok 3: Převod obrázku na JSONL – ošetření okrajových případů

Když zpracováváte dávku účtenek, může se stát, že některé obrázky jsou prázdné, poškozené nebo mají extrémně nízké skóre důvěry. Udělejme pipeline robustnější.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Proč filtrovat:**  
Účtenky tištěné na vybledlém papíře mohou generovat znaky s nízkou důvěrou. Odstraněním všeho pod 80 % obvykle odstraníte šum a zachováte užitečná data.

---

## Krok 4: Zpracování účtenky pomocí OCR – kompletní příklad

Spojením všeho dohromady získáte **kompletní, připravený ke spuštění** program. Nahraďte `YOUR_DIRECTORY` složkou, ve které máte PNG soubor.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Spuštění kódu:**  
1. Otevřete terminál ve složce projektu.  
2. `dotnet add package Aspose.OCR` – nainstaluje knihovnu.  
3. `dotnet run` – měli byste vidět zprávu o úspěchu a objeví se soubor `receipt.jsonl`.

**Očekávaný výsledek:** Řádkově oddělený JSON soubor, kde každý řádek odpovídá řádku z účtenky, včetně skóre důvěry. Nyní můžete tento soubor poslat do Power BI, Elastic nebo jakéhokoli analytického nástroje, který rozumí JSON‑L.

---

## Časté úskalí a profesionální tipy

| Problém | Proč se vyskytuje | Rychlé řešení |
|---------|-------------------|---------------|
| **Prázdný výstup** | Špatná cesta k souboru nebo soubor není PNG. | Zkontrolujte cestu, použijte `File.Exists(imagePath)`. |
| **Nečitelné znaky** | Nízké DPI nebo silně komprimovaný PNG. | Používejte skeny alespoň 300 dpi; vyhněte se agresivní kompresi JPEG. |
| **Příliš mnoho řádků s nízkou důvěrou** | Účtenka tištěná na termopapíru s vyblednutím. | Zvyšte práh `minConfidence` nebo předzpracujte obrázek (kontrast/práh). |
| **Chyby při parsování JSON** | Neescapované uvozovky v textu účtenky. | Používejte pomocnou funkci `EscapeJson` nebo přejděte na `System.Text.Json` pro robustní serializaci. |

**Profesionální tip:** Pokud potřebujete extrahovat konkrétní pole (např. celkovou částku), spusťte jednoduchý regex na každém `line.Text` po vytvoření souboru JSON‑L. Tím oddělíte OCR od obchodní logiky a usnadníte ladění.

---

## Rozšíření řešení

- **Dávkové zpracování:** Zabalte logiku v `Main` do `foreach` přes všechny PNG soubory ve složce.
- **Podpora více jazyků:** Nastavte `ocrEngine.Language = OcrLanguage.Spanish;` (nebo jakýkoli podporovaný jazyk) před `Recognize`.
- **Strukturovaný výstup:** Místo řádkového JSON vytvořte objekt `Receipt` s vlastnostmi `Date`, `Merchant`, `Total` a serializujte jej najednou.

Všechny tyto varianty stále **převádějí obrázek na jsonl** v jádru, takže můžete měnit downstream spotřebitele bez zásahu do OCR části.

---

## Závěr

Ukázali jsme vám, jak **rozpoznat text z png** souborů pomocí Aspose OCR, **extrahovat text z účtenky** a **převést obrázek na jsonl** pro snadné následné zpracování. Kompletní, samostatný C# program demonstruje celý workflow – od načtení PNG, přes ošetření okrajových případů, až po zápis čistého JSON‑L souboru – takže můžete okamžitě **zpracovat účtenku pomocí OCR** ve svých projektech.

Vyzkoušejte to na několika ukázkových účtenkách, upravte práh důvěry a uvidíte, jak rychle se špinavý stack obrázků promění ve strukturovaná data připravená k analytice. Jakmile budete mít jistotu, prozkoumejte dávkové zpracování nebo přidejte malý ML model pro automatickou klasifikaci kategorií výdajů.

Máte otázky nebo jste objevili chytrý trik? Zanechte komentář níže – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}