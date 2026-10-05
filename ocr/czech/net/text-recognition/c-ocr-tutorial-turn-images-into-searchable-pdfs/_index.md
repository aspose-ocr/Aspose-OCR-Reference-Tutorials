---
category: general
date: 2026-01-12
description: c# OCR tutoriál, který vám ukáže, jak rozpoznat textový obrázek, extrahovat
  text z obrázku v C# a vytvořit soubor OCR z obrázku do PDF s ukazateli spolehlivosti.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: cs
og_description: Naučte se kompletní tutoriál OCR v C#, jak rozpoznat textový obrázek,
  extrahovat text z obrázku v C# a vytvořit OCR dokument z obrázku do PDF s ukazateli
  důvěryhodnosti.
og_title: c# OCR tutoriál – Převod obrázků na prohledávatelné PDF
tags:
- OCR
- C#
- PDF
title: c# OCR tutoriál – Převést obrázky na prohledávatelné PDF
url: /cs/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Převod obrázků na prohledávatelné PDF

Už jste se někdy zamysleli, jak **rozpoznat textové obrázky** v C# projektu, aniž byste museli hledat služby třetích stran? Nejste v tom sami. V mnoha reálných aplikacích – například skenery faktur, sledovače účtenek nebo vícejazyčné archivy dokumentů – vývojáři potřebují spolehlivý OCR engine provozovaný lokálně, který také poskytuje skóre důvěry.

Tento **c# ocr tutorial** vás provede vším, co potřebujete: od načtení obrázku, výběru jazykových modelů, přepínání GPU akcelerace až po uložení výsledku jako prohledávatelné PDF. Na konci budete mít připravený ukázkový kód, který extrahuje text, hlásí OCR důvěru a volitelně vytvoří soubor *image to pdf ocr* – vše během méně než minuty kódování.

## Co vytvoříte

- Načtěte vícejazyčný obrázek (`sample_multi_lang.jpg` je použit jako zástupný).  
- Vyberte jazykové modely pro arabštinu, hindštinu a ruštinu (můžete přidat další).  
- Zapněte zpracování na GPU, pokud to váš počítač podporuje.  
- Získejte surový OCR výsledek **s důvěryhodnostními skóre**.  
- Serializujte výsledek do hezky formátovaného JSON **nebo** vytvořte prohledávatelné PDF.

Žádné externí webové služby, žádná skrytá magie – jen Aspose.OCR pro .NET, několik řádků C# a jasné vysvětlení **proč** má každý řádek smysl.

## Požadavky

- .NET 6.0 nebo novější (kód se kompiluje na .NET Core i .NET Framework).  
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete).  
- Licence Aspose.OCR pro .NET (bezplatná zkušební verze funguje pro testování).  
- Volitelné: GPU kompatibilní s CUDA, pokud chcete urychlit rozpoznávání.

> **Tip:** Pokud nemáte GPU, stačí nastavit `UseGpu = false` a engine se automaticky přepne na CPU bez jakýchkoli změn kódu.

## Krok 1: Nainstalujte požadované NuGet balíčky

Open the **Package Manager Console** and run:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Tyto tři balíčky vám poskytují OCR engine, GPU akceleraci a pěkný JSON serializer pro výstup důvěryhodnostních skóre.

## Krok 2: Nastavte strukturu projektu

Vytvořte nový konzolový projekt (`dotnet new console -n AsposeOcrDemo`) a nahraďte vygenerovaný soubor `Program.cs` kódem níže.  
Veškerá logika žije ve třídě `Program`; jediným dalším typem je malá rozšiřující metoda, která formátuje OCR výsledek do JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Proč tento kód funguje

1. **GPU přepínač** – `GpuOcrEngine` využívá CUDA jádra; ternární operátor usnadňuje přepínání.  
2. **Automatické stažení jazyků** – `AutoDownloadResources = true` zajišťuje, že modely pro arabštinu, hindštinu a ruštinu jsou staženy při prvním spuštění aplikace.  
3. **Skóre důvěry** – `result.Words` obsahuje `Confidence` pro každé rozpoznané slovo; rozšiřující metoda je formátuje do čistého JSON objektu.  
4. **Prohledávatelné PDF** – `result.Pdf` je již plně prohledávatelné PDF, takže jen zapíšeme pole bajtů na disk. Žádné další knihovny nejsou potřeba.

## Krok 6: Spusťte ukázku

Otevřete terminál, přejděte do složky projektu a spusťte:

```bash
dotnet run
```

Pokud jste zvolili výstup **JSON**, uvidíte něco jako:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Pokud jste přepnuli na **PDF**, konzole vypíše cestu a prohledávatelné PDF najdete vedle zdrojového obrázku.

## Časté otázky a okrajové případy

- **Co když není jazykový model k dispozici?**  
  OCR engine vyhodí jasnou výjimku `ResourceNotFoundException`. Protože máme nastaveno `AutoDownloadResources = true`, chybějící model se automaticky stáhne při prvním spuštění, takže výjimka se v produkci zřídka objeví.

- **Mohu zpracovat dávku obrázků?**  
  Určitě. Zabalte volání `engine.Recognize` do smyčky `foreach` přes adresář souborů. Stejný `OcrResultExtensions` funguje pro každý obrázek.

- **Potřebuji licenci pro GPU?**  
  Ne. Bezplatná zkušební verze funguje jak pro CPU, tak pro GPU. Plná licence odstraní vodoznak zkušební verze a zruší omezení počtu stránek.

- **Jak přesná jsou skóre důvěry?**  
  Skóre se pohybují od 0,0 (žádná důvěra) do 1,0 (dokonalá důvěra). V praxi je vše nad 0,90 spolehlivé pro následné zpracování; můžete filtrovat slova s nižší důvěrou, pokud potřebujete přísnější validaci.

## Krok 7: Další kroky (rozšiřte svůj OCR nástroj)

1. **Přidejte více jazyků** – stačí připojit `LanguageModel.French` (nebo jakýkoli podporovaný model) do pole `Languages`.  
2. **Kombinujte OCR s konverzí PDF/A** – Aspose.PDF může vložit OCR vrstvu do PDF/A‑2b kompatibilního dokumentu pro archivaci.  
3. **Integrujte s Azure Functions** – zabalte logiku do serverless endpointu pro zpracování nahrávek za běhu.  
4. **Doladění prahů důvěry** – použijte `result.Words.Where(w => w.Confidence < 0.85)` k označení nejistých slov pro manuální revizi.

---

### TL;DR

Tento **c# ocr tutorial** vám ukáže, jak:

- Načíst obrázek a vybrat více jazykových modelů.  
- Zapnout GPU akceleraci jedním boolean flagem.  
- Získat OCR výsledky **s důvěryhodnostními skóre** a serializovat je do JSON.  
- Volitelně vytvořit prohledávatelné PDF (**image to pdf ocr**).

Vše je možné dosáhnout jen několika řádky kódu, bezplatnou zkušební verzí Aspose.OCR a výše uvedeným kódem. Vyzkoušejte to, upravte seznam jazyků a budete mít produkčně připravený OCR pipeline během minut.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}