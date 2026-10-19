---
category: general
date: 2026-09-13
description: Naučte se, jak převést naskenovanou stránku na PDF v C# pomocí Aspose
  OCR. Tento průvodce ukazuje předzpracování, rozpoznávání korejského textu a vytvoření
  prohledávatelného PDF.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Naučte se, jak převést naskenovanou stránku na PDF v C# s Aspose OCR.
  Tutoriál pokrývá předzpracování obrazu, GPU‑akcelerované OCR pro korejský text a
  vytvoření prohledávatelného PDF během několika minut.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Jak převést naskenovanou stránku na PDF v C# s OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Jak převést naskenovanou stránku na PDF v C# s OCR
url: /cs/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak převést naskenovanou stránku na PDF v C# s OCR

Pokud potřebujete **převést naskenovanou stránku na PDF** a zároveň zachovat text prohledávatelný, jste na správném místě. Tento tutoriál vás provede používáním Aspose OCR k **předzpracování obrázku pro OCR**, **rozpoznání korejského textu na obrázku** a nakonec **vytvoření prohledávatelného PDF obrázku** – vše z jednoduché C# konzolové aplikace.

## Rychlé odpovědi
- **Která knihovna zajišťuje OCR?** Aspose.OCR for .NET  
- **Mohu použít GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Potřebuji korejský jazykový balíček?** It downloads automatically on first use  
- **Bude výstup prohledávatelný?** The generated PDF contains an invisible text layer  
- **Jaké verze .NET jsou podporovány?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Požadavky

- **.NET 6.0 nebo novější** – funguje na .NET Core, .NET Framework a .NET 5/6+  
- **Aspose.OCR pro .NET** NuGet balíček (`Aspose.OCR`) – zkušební klíče jsou zdarma na stránkách Aspose  
- Vzorek obrázku s korejskými znaky, např. `korean_book_page.jpg`  
- Váš oblíbený IDE (Visual Studio 2022, VS Code, Rider, atd.)

> **Tip:** Ukládejte obrázky do složky `Resources/`, aby cesty zůstaly konzistentní napříč počítači.

## Přehled procesu

1. Inicializujte OCR engine s podporou GPU.  
2. Přidejte **preprocess image for OCR** filtry jako deskew a denoise.  
3. Stáhněte a načtěte korejský jazykový model (zpracovává se automaticky).  
4. Spusťte OCR na obrázku.  
5. Exportujte výsledek pomocí **SearchablePdfExporter** k **create searchable PDF image**.  
6. (Volitelné) Serializujte výstup OCR do JSON pro následné pipeline.

Níže rozvedeme každý krok, vysvětlíme *proč* je důležitý a poskytneme vám přesný kód, který můžete zkopírovat‑vložit.

## Jak funguje převod naskenované stránky na PDF?

`OcrEngine` je hlavní třída v Aspose.OCR, která provádí optické rozpoznávání znaků na obrázcích.  
`SearchablePdfExporter` vytváří PDF, které obsahuje původní obrázek a neviditelnou textovou vrstvu pro vyhledávání.  
`RecognitionResult` obsahuje text a data o důvěře vrácená OCR enginem.

Načtěte svůj obrázek pomocí `new OcrEngine()` a zavolejte `engine.Recognize("korean_book_page.jpg")`, poté předáte `RecognitionResult` do `SearchablePdfExporter.Export`. Tento dvoustupňový tok čte bitmapu, extrahuje Unicode text a vloží oba do jednoho PDF, kde je textová vrstva neviditelná, ale prohledávatelná. GPU akcelerace zkrátí dobu rozpoznání přibližně na polovinu, zatímco filtry deskew a denoise zvyšují přesnost až o 15 % u špinavých skenů.

## Převod obrázku na PDF – kompletní workflow

Následující úryvek je *kompletní* program. Vytvořte nový konzolový projekt (`dotnet new console -n OcrPdfDemo`) a nahraďte automaticky vygenerovaný `Program.cs` kódem zobrazeným v zástupci.

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

- **GPU acceleration** zkrátí dobu rozpoznání přibližně na polovinu ve srovnání s režimem pouze CPU.  
- **Deskew** a **Denoise** jsou klasické techniky *preprocess image for OCR*; opravují běžné skenovací vady, které by jinak způsobily, že engine vynechá znaky.  
- **Language model loading** je nezbytné pro **recognize Korean text image** – bez korejského modelu by engine použil obecnou latinskou abecedu a produkoval nesmysly.  
- **SearchablePdfExporter** spojuje původní bitmapu a neviditelný textový překryv, což vám poskytuje výsledek **create searchable pdf image**, který můžete indexovat v libovolném PDF prohlížeči.

## Proč to funguje

- **GPU acceleration** zkrátí dobu rozpoznání přibližně na polovinu ve srovnání s režimem pouze CPU.  
- **Deskew** a **Denoise** jsou klasické techniky *preprocess image for OCR*; opravují běžné skenovací vady, které by jinak způsobily, že engine vynechá znaky.  
- **Language model loading** je nezbytné pro **recognize Korean text image** – bez korejského modelu by engine použil obecnou latinskou abecedu a produkoval nesmysly.  
- **SearchablePdfExporter** spojuje původní bitmapu a neviditelný textový překryv, což vám poskytuje výsledek **create searchable pdf image**, který můžete indexovat v libovolném PDF prohlížeči.

## Preprocess image for OCR – tipy a triky

`DeskewFilter` koriguje rotaci naskenovaných stránek.  
`ContrastFilter` upravuje kontrast obrázku pro zlepšení přesnosti OCR.  
`BinarizationFilter` převádí obrázek na černobílý na základě prahu, čímž snižuje šum na pozadí.  
`OrientationFilter` detekuje a koriguje smíšené portrétní/landscape stránky.  

| Problém | Další filtr | Jak přidat |
|-------|-------------------|------------|
| Nízký kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Silný šum na pozadí | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Smíšená orientace (portrét a krajina) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Poznámka:** Přidání příliš mnoha filtrů může zpomalit zpracování. Otestujte každou změnu na jedné stránce před rozšířením.

## Recognize Korean text image – běžné úskalí

Korejské písmo obsahuje Hangul slabiky, které jsou vizuálně husté. Pokud zaznamenáte poškozený výstup:

1. **Ujistěte se, že jazykový model je plně stažen** – zkontrolujte konzoli na zprávu jako „Downloading Korean model…“.  
2. **Zvyšte `MaxAngle`** v `DeskewFilter`, pokud jsou vaše skeny natočeny více než 12°.  
3. **Zvyšte paměť GPU** nastavením `ocrEngine.GpuMemoryLimit = 2048;` (hodnota v MB).  

`LanguageModel.Korean` načítá korejská jazyková data pro OCR, což umožňuje přesné rozpoznání Hangul.  

Tyto úpravy přímo ovlivňují úspěšnost **recognize Korean text image**.

## Create searchable PDF image – ověření výsledku

Po dokončení programu otevřete `korean_page.pdf` v libovolném PDF prohlížeči (Adobe Acrobat Reader, Foxit, dokonce Chrome). Měli byste být schopni:

- **Vybrat text** myší, jako by šlo o nativní PDF.  
- **Vyhledávat** korejská slova pomocí vestavěného vyhledávacího pole.  

Pokud se textová vrstva zobrazí prázdná, zkontrolujte, že metoda `Export` obdržela správnou cestu k obrázku a že výsledek OCR obsahuje ne‑prázdný `RecognitionResult.Text`.

## Kompletní JSON výstup – co očekávat

Konzole vypíše pěkně formátovaný JSON payload. Oříznutý příklad vypadá takto:

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

## Řešení problémů a FAQ

**Q: Mé PDF je velké ve srovnání s původním obrázkem.**  
A: Exportér vloží původní bitmapu v její nativní rozlišení. Pokud je velikost problém, zmenšete obrázek *před* rozpoznáním:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR vrací prázdné řetězce.**  
A: Ověřte, že cesta k obrázku je správná a soubor není poškozený. Také se ujistěte, že ovladač GPU je aktuální; starší ovladače mohou způsobovat tiché selhání.

**Q: Mohu zpracovávat více stránek ve smyčce?**  
A: Rozhodně. Zabalte kroky 4‑6 do smyčky `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` a podle toho změňte výstupní cestu PDF.

## Závěr

Právě jsme **převzeli obrázek na PDF** při zachování prohledávatelného textu, vše díky výkonnému pipeline Aspose OCR. **Preprocess image for OCR** zvyšuje přesnost; **recognize Korean text image** umožňuje zpracování složitých skriptů; a **create searchable pdf image** vám poskytuje přenosný, indexovatelný dokument.

Získejte kód, nasměrujte jej na své vlastní skeny a experimentujte s dalšími filtry nebo jazykovými modely. Stejný vzor funguje pro čínštinu, japonštinu nebo jakýkoli jazyk založený na latině – stačí vyměnit `LanguageModel.Korean` za odpovídající enum.

Máte další otázky? Zanechte komentář a šťastné kódování!

---

**Poslední aktualizace:** 2026-09-13  
**Testováno s:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose

## Související tutoriály

- [Vytvořit prohledávatelné PDF ze skenovaných souborů pomocí Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR předzpracovací pipeline – jak rozpoznat text z obrázku](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Rozpoznat text z obrázku s Aspose Ocr – kompletní C průvodce](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}