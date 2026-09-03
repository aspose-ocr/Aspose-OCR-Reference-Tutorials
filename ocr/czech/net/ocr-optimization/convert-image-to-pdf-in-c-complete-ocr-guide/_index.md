---
category: general
date: 2025-12-30
description: Převést obrázek na PDF pomocí Aspose OCR v C#. Naučte se, jak předzpracovat
  obrázek pro OCR, rozpoznat korejský textový obrázek a rychle vytvořit prohledávatelný
  PDF obrázek.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: cs
og_description: Převod obrázku na PDF pomocí Aspose OCR. Tento tutoriál ukazuje, jak
  předzpracovat obrázek pro OCR, rozpoznat korejský text na obrázku a vytvořit prohledávatelný
  PDF obrázek.
og_title: Převod obrázku na PDF v C# – Kompletní průvodce OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Převod obrázku na PDF v C# – Kompletní průvodce OCR
url: /cs/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod obrázku na PDF v C# – Kompletní průvodce OCR

Už jste někdy potřebovali **convert image to PDF**, ale zároveň chtěli, aby byl text uvnitř prohledávatelný? Nejste v tom sami. Mnoho vývojářů narazí na stejný problém při práci s naskenovanými stránkami, zejména těmi psanými v korejštině. Dobrou zprávou je, že s Aspose OCR můžete **preprocess image for OCR**, **recognize Korean text image** a nakonec **create searchable PDF image** během několika řádků.

V tomto tutoriálu projdeme celým procesem – od načtení surového JPEG korejské knihy, jeho vyčištění, extrahování textu a zabalení všeho do prohledávatelného PDF. Na konci budete mít připravenou spustitelnou C# konzolovou aplikaci, kterou můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- **.NET 6.0 nebo novější** (kód funguje jak na .NET Core, tak na .NET Framework)  
- **Aspose.OCR for .NET** NuGet balíček (`Aspose.OCR`) – klíče pro bezplatnou zkušební verzi jsou k dispozici na stránkách Aspose.  
- Vzorový obrázek obsahující korejský text (např. `korean_book_page.jpg`).  
- Vývojové prostředí podle vašeho výběru (Visual Studio, VS Code, Rider – já používám VS 2022).

> **Pro tip:** Ukládejte své soubory obrázků do vyhrazené složky jako `Resources/`, aby cesta zůstala konzistentní napříč stroji.

## Přehled procesu

1. **Inicializujte OCR engine** s podporou GPU pro rychlost.  
2. **Přidejte předzpracovatelské filtry** (deskew, denoise) pro zlepšení přesnosti rozpoznání.  
3. **Stáhněte a načtěte korejský jazykový model** – Aspose to provede automaticky, pokud je potřeba.  
4. **Spusťte rozpoznávání** na vstupním obrázku.  
5. **Exportujte výsledek jako prohledávatelné PDF** pomocí vestavěného exportéru.  
6. **Volitelně serializujte výsledek do JSON** pro další analýzu nebo logování.

Níže rozložíme každý krok, vysvětlíme *proč* je důležitý a poskytneme vám přesný kód, který můžete zkopírovat‑vložit.

---

## ## Převod obrázku na PDF – Kompletní workflow

Následující úryvek je *kompletní* program. Klidně vytvořte nový konzolový projekt (`dotnet new console -n OcrPdfDemo`) a nahraďte automaticky vygenerovaný `Program.cs` tímto kódem.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Proč to funguje

- **GPU acceleration** zkracuje čas rozpoznání přibližně na polovinu oproti režimu pouze CPU.  
- **Deskew** a **Denoise** jsou klasické techniky *preprocess image for OCR*; opravují běžné skenovací vady, které by jinak způsobily, že engine vynechá znaky.  
- **Language model loading** je nezbytné pro **recognize Korean text image** – bez korejského modelu by engine použil obecnou latinskou abecedu a produkoval nesmysly.  
- **SearchablePdfExporter** spojí původní bitmapu a neviditelnou textovou vrstvu, čímž vám poskytne výsledek **create searchable pdf image**, který můžete indexovat v libovolném PDF prohlížeči.

---

## ## Předzpracování obrázku pro OCR – Tipy & Triky

Zatímco dva filtry, které jsme přidali, jsou obvykle dostačující, můžete narazit na obtížné obrázky. Zde je několik dalších kroků, které můžete vyzkoušet:

| Problém | Další filtr | Jak přidat |
|-------|-------------------|------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Poznámka:** Přidání příliš mnoha filtrů může zpomalit zpracování. Otestujte každou změnu na jedné stránce před rozšířením.

---

## ## Rozpoznání korejského textu na obrázku – Časté úskalí

Korejské písmo obsahuje Hangul slabiky, které jsou vizuálně husté. Pokud zaznamenáte nesrozumitelný výstup:

1. **Ujistěte se, že jazykový model je plně stažen** – zkontrolujte konzoli pro zprávu typu “Downloading Korean model…”.  
2. **Zvyšte `MaxAngle`** v `DeskewFilter`, pokud jsou vaše skeny natočeny více než 12°.  
3. **Zvyšte GPU paměť** nastavením `ocrEngine.GpuMemoryLimit = 2048;` (hodnota v MB).

Tyto úpravy přímo ovlivňují úspěšnost **recognize Korean text image**.

---

## ## Vytvoření prohledávatelného PDF obrázku – Ověření výsledku

Po dokončení programu otevřete `korean_page.pdf` v libovolném PDF čtečce (Adobe Acrobat Reader, Foxit, dokonce Chrome). Měli byste být schopni:

- **Vybrat text** myší, jako by šlo o nativní PDF.  
- **Vyhledávat** korejská slova pomocí vestavěného vyhledávacího pole.

Pokud se textová vrstva zobrazí prázdná, dvojitě zkontrolujte, že metoda `Export` obdržela správnou cestu k obrázku a že výsledek OCR obsahuje ne‑prázdný `RecognitionResult.Text`.

---

## ## Kompletní JSON výstup – Co očekávat

Konzole vypíše pěkně formátovaný JSON payload. Zkrácený příklad vypadá takto:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

---

## ## Řešení problémů & FAQ

**Q: Mé PDF je obrovské ve srovnání s původním obrázkem.**  
A: Exportér vkládá původní bitmapu v její nativní rozlišení. Pokud je velikost problém, zmenšete obrázek *před* rozpoznáním:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR vrací prázdné řetězce.**  
A: Ověřte, že cesta k obrázku je správná a soubor není poškozený. Také se ujistěte, že ovladač GPU je aktuální; starší ovladače mohou způsobit tiché selhání.

**Q: Můžu zpracovávat více stránek ve smyčce?**  
A: Rozhodně. Zabalte kroky 4‑6 do smyčky `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` a podle toho změňte výstupní cestu PDF.

---

## ## Závěr

Právě jsme **convert image to PDF** při zachování prohledávatelného textu, vše díky výkonnému pipeline Aspose OCR. **preprocess image for OCR** zvyšuje přesnost; **recognize Korean text image** umožňuje zpracovat složité skripty; a **create searchable pdf image** vám poskytuje přenosný, indexovatelný dokument.

Vezměte kód, nasměrujte ho na své vlastní skeny a experimentujte s dalšími filtry nebo jazykovými modely. Stejný vzor funguje pro čínštinu, japonštinu nebo jakýkoli jazyk založený na latině – stačí vyměnit `LanguageModel.Korean` za příslušný enum.

Máte další otázky? Zanechte komentář a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}