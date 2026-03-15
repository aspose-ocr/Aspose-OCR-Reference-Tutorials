---
category: general
date: 2026-03-15
description: Jak použít Aspose OCR k extrakci textu z obrázků a převodu obrázku na
  JSON v C#. Naučte se rozpoznávat text z PNG a rychle získat strukturovaný výstup.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: cs
og_description: Jak použít Aspose OCR k extrakci textu z obrázků a převodu obrázku
  na JSON v C#. Tento průvodce vás provede rozpoznáváním textu z PNG a získáním strukturovaného
  výstupu.
og_title: Jak použít Aspose OCR k převodu obrázku na JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Jak použít Aspose OCR k převodu obrázku na JSON
url: /cs/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

klad (připravený ke zkopírování)"

Then code block: keep unchanged.

But note the code block is truncated: ends with `throw new InvalidOperationException("OCR` and then the content stops. We should keep as is.

After code block, there are closing shortcodes and back button.

We must keep them unchanged.

Now produce final content with translations and unchanged elements.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Aspose OCR pro převod obrázku na JSON

Jak používat Aspose OCR je častá otázka, když vývojáři potřebují získat text z obrázků. Pokud chcete **convert image to JSON** nebo **recognize text from PNG**, tento průvodce vás provede—bez zbytečného balastu, jen praktickým, end‑to‑end řešením.

V následujících několika minutách projdeme vše, co potřebujete: instalaci knihovny, konfiguraci engine pro výstup JSON, načtení PNG účtenky, spuštění OCR a nakonec zápis výsledku do souboru `.json`. Na konci budete schopni **extract text from image** soubory jedním voláním metody a pochopíte, proč je každý krok důležitý.

> **Pro tip:** Aspose OCR funguje s širokou škálou formátů obrázků (PNG, JPEG, BMP, TIFF). Stejný kód níže je zvládne všechny, takže nemusíte psát logiku specifickou pro formát.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)  
- Platný balíček Aspose.OCR NuGet (bezplatná zkušební verze nebo licencovaná)  
- Obrázkový soubor, který chcete zpracovat (např. `receipt.png`)  
- Visual Studio, VS Code nebo jakýkoli C# editor, který preferujete  

To je vše—žádné další závislosti, žádné externí služby. Připravení? Ponořme se.

![how to use aspose OCR engine](image-placeholder.png "how to use aspose OCR engine")

## Jak používat Aspose OCR – Konfigurace výstupu JSON

První věc, kterou musíte udělat, když **how to use aspose** pro OCR, je vytvořit instanci `OcrEngine` a nastavit ji, aby emitovala JSON. Tento malý konfigurační přepínač vás ušetří ruční serializaci výsledku později.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Proč je to důležité:** Nastavení `OutputFormat` na `Json` znamená, že OCR engine již strukturuje text do hierarchie stránek, řádků a slov. Později nemusíte parsovat surové řetězce, což činí následné zpracování—např. vkládání dat do databáze—mnohem čistším.

## Převod obrázku na JSON pomocí Aspose OCR

Nyní, když je engine nakonfigurován, pojďme podrobněji probrat část **convert image to JSON**.

1. **Load the image** – `Image.FromFile` funguje pro jakýkoli podporovaný formát. Pokud pracujete se streamem (např. nahraným souborem), můžete místo toho použít `Image.FromStream`.  
2. **Run `Recognize`** – tato metoda vrací objekt `OcrResult`. Protože jsme nastavili výstup na JSON, `ocrResult.Text` již obsahuje JSON řetězec.  
3. **Write the file** – `File.WriteAllText` je nejjednodušší způsob, jak uložit JSON. Pokud jej potřebujete uložit do cloudového bucketu, stačí tuto řádku vyměnit za odpovídající SDK volání.

### Očekávaný výstup JSON

Typický JSON payload vypadá takto (zkrácený pro stručnost):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Nyní můžete tuto strukturu předat jakémukoli následnému systému— ať už je to nástroj pro reportování, model strojového učení nebo jednoduchý log soubor.

## Extrahování textu z obrázku pomocí Aspose OCR

Pokud potřebujete jen surový řetězec (tj. nevadí vám JSON), jednoduše přepněte výstupní formát zpět na prostý text:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Kdy zvolit prostý text?**  
- Rychlé ladění nebo výstup do konzole.  
- Scénáře, kde budete aplikovat vlastní post‑processing (např. regex extrakce).  

Ale pamatujte, **extract text from image** pomocí JSON vám poskytuje poziční data—užitečná pro zvýraznění textu v UI nebo zarovnání s formulářovými poli.

## Rozpoznání textu z PNG souborů

PNG je bezztrátový formát, který často poskytuje lepší přesnost OCR ve srovnání s silně komprimovanými JPEGy. Zde je rychlý kontrolní seznam, který zajistí nejlepší výsledky při **recognize text from PNG**:

| Kontrolní položka | Proč pomáhá |
|-------------------|-------------|
| Použijte DPI 300+ | Vyšší rozlišení poskytuje engine více pixelů ke zpracování. |
| Udržujte obrázek v odstínech šedi | Snižuje šum; Aspose OCR automaticky konvertuje, ale předzpracování může urychlit. |
| Odstraňte pozadí | Čisté pozadí zlepšuje skóre důvěry. |

Pokud narazíte na nízké skóre důvěry, zkuste zvýšit DPI nebo aplikovat jednoduchý prahový filtr před předáním obrázku Aspose.

## Jak programově extrahovat OCR výsledky

Kromě pouhého uložení JSON můžete chtít programově načíst konkrétní pole—např. celkovou částku na účtence. Protože JSON obsahuje hierarchii, můžete jej deserializovat do objektu C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Nyní můžete dotazovat `ocrData` pomocí LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Proč to funguje:** JSON již říká, kde se každé slovo nachází na stránce, takže můžete spolehlivě najít pole i při mírných změnách rozvržení.

## Hraniční případy a běžné úskalí

- **Null Result:** Pokud `ocrEngine.Recognize` vrátí `null`, obrázek může být nepodporovaný nebo poškozený. Vždy to ošetřete:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** Pro obrázky o velikosti několika megabajtů zvažte streamování obrázku nebo jeho změnu velikosti před OCR, aby nedošlo k nadměrné spotřebě paměti.

- **License Issues:** Zkušební verze přidává vodoznak do výstupu. Ujistěte se, že načtete licenci brzy v programu:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR podporuje mnoho jazyků, ale musíte nastavit vlastnost `Language` odpovídajícím způsobem (např. `ocrEngine.Configuration.Language = Language.English;`).

## Kompletní funkční příklad (připravený ke zkopírování)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}