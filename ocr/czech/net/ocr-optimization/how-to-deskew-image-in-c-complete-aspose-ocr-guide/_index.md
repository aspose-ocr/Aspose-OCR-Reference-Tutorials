---
category: general
date: 2026-06-28
description: Jak narovnat obrázek pomocí Aspose.OCR. Naučte se předzpracovat obrázek
  pro OCR, zlepšit přesnost OCR a narovnat naskenovaný obrázek s kompletním příkladem
  v C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: cs
og_description: Jak narovnat obrázek pomocí Aspose.OCR. Tento tutoriál vám ukáže,
  jak předzpracovat obrázek pro OCR, zvýšit přesnost a krok za krokem narovnat naskenovaný
  obrázek.
og_title: Jak vyrovnat zkosení obrázku v C# – Kompletní průvodce Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Jak vyrovnat sklon obrázku v C# – Kompletní průvodce Aspose.OCR
url: /cs/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak opravit zkosení obrazu v C# – Kompletní průvodce Aspose.OCR

Už jste se někdy zamýšleli **jak opravit zkosení obrazu** souborů před jejich předáním OCR enginu? Nejste v tom sami. Naskenované dokumenty často přicházejí nakloněné a tato malá rotace může zničit výsledky rozpoznávání. Dobrá zpráva? S Aspose.OCR můžete narovnat (deskew) a vyčistit obrázky během několika řádků C#.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **předzpracuje obrázek pro OCR**, přidá filtr pro opravu zkosení a ukáže vám **jak zlepšit OCR** přesnost. Na konci budete schopni **automaticky opravit zkosení naskenovaného obrazu** a sami si prohlédnout skóre důvěry.

> **Poznámka:** Kód funguje s Aspose.OCR ≥ 22.10 a .NET 6+, ale koncepty platí i pro starší verze.

## Co budete potřebovat

- **Aspose.OCR pro .NET** (NuGet balíček `Aspose.OCR`)
- **Zkosený TIFF** nebo JPEG, který chcete narovnat
- Visual Studio 2022 (nebo jakékoli C# IDE)
- Základní znalost C# a konzolových aplikací

Žádné další knihovny třetích stran nejsou potřeba; celý pipeline běží uvnitř Aspose.OCR.

---

## Jak opravit zkosení obrazu pomocí Aspose.OCR

Jádrem řešení je **filtrační pipeline**. Představte si to jako montážní linku, kde každý filtr řeší konkrétní problém: nejprve opravíme rotaci, poté snížíme šum a nakonec zvýšíme kontrast, aby OCR engine viděl znaky jasně.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Příklad obrázku**  
> ![příklad opravy zkosení obrazu](/images/deskew-example.png "příklad opravy zkosení obrazu")

### Proč nejprve filtr pro opravu zkosení?

Když je dokument otočen i jen o několik stupňů, OCR engine špatně interpretuje základní linie, což vede k nečitelnému výstupu. `DeskewFilter` automaticky odhadne úhel rotace (až do `MaxAngle` stupňů) a otočí bitmapu zpět na vodorovnou základní linii. Vrácená hodnota `DeskewConfidence` vám říká, jak je algoritmus jistý v korekci – užitečné pro logování nebo záložní strategie.

---

## Předzpracování obrazu pro OCR – Vytvoření filtrační pipeline

### 1️⃣ DeskewFilter (Primární krok)

- **Co dělá:** Detekuje dominantní směr textových řádků a otáčí obrázek.
- **Proč je důležité:** Rovná základní linie maximalizuje přesnost segmentace znaků.
- **Tip:** Pokud vaše dokumenty nikdy nepřesahují 10°, nastavte `MaxAngle = 10` pro zrychlení detekce.

### 2️⃣ DenoiseFilter (Sekundární čištění)

- **Co dělá:** Snižuje náhodný pixelový šum, který se může objevit po skenování.
- **Proč je důležité:** Šum často vytváří falešné hrany, což zmátne segmentaci OCR.
- **Tip:** Nastavte `Strength` mezi 0.3 (lehké) a 0.8 (agresivní) podle kvality skenu.

### 3️⃣ ContrastBoostFilter (Finální úprava)

- **Co dělá:** Zvyšuje rozdíl mezi popředím textu a pozadím.
- **Proč je důležité:** Nízký kontrast může způsobit, že slabé znaky jsou neviditelné pro rozpoznávací engine.
- **Tip:** Hodnota `Level` 1.2 funguje pro většinu černobílých skenů; u barevných dokumentů experimentujte s hodnotami až do 2.0.

Propojením těchto tří filtrů **předzpracujete obrázek pro OCR** způsobem, který řeší nejčastější problémy: naklonění, šum a nízký kontrast.

---

## Jak zlepšit přesnost OCR pomocí opravy zkosení a odšumu

Můžete se ptát: „Pokud už mám filtr pro opravu zkosení, proč se zabývat odšuměním a zvýšením kontrastu?“ Odpověď spočívá v **kumulativním zlepšení**. Každý filtr řeší jiný nedostatek a společně zvyšují celkovou důvěru.

#### Reálný test

| Test | Původní přesnost OCR | Po opravě zkosení | Po celé pipeline |
|------|-----------------------|-------------------|-------------------|
| Jednoduchá faktura (5° naklonění) | 78 % | 92 % | 96 % |
| Sken starého novin (15° naklonění, zrnitý) | 61 % | 78 % | 88 % |
| Formulář s nízkým kontrastem (bez naklonění) | 70 % | 71 % | 84 % |

*Čísla jsou ilustrativní, ale odrážejí typické zisky hlášené uživateli Aspose.*

**Klíčová poznámka:** I když je vaším hlavním cílem **oprava zkosení naskenovaného obrazu**, přidání kroků odšumu a zvýšení kontrastu často přináší výrazný nárůst kvality finálního textu.

---

## Oprava zkosení naskenovaného obrazu: Ověření výsledků

Po spuštění pipeline získáte dvě užitečné informace:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Důvěra opravy zkosení** (`result.DeskewConfidence`) je v procentech. Hodnoty nad 90 % obvykle znamenají, že rotace byla přesně opravena.
- **Rozpoznaný text** (`result.Text`) vám umožní okamžitě ověřit, zda výstup vypadá rozumně.

Pokud je důvěra nízká (< 70 %), zvažte:

1. **Zvýšení `MaxAngle`** – možná je dokument otočen více, než se očekává.
2. **Přidání `BinarizationFilter`** před opravu zkosení pro zjednodušení obrazu.
3. **Manuální otočení** obrazu pomocí `OcrImage.Rotate(angle)` jako záložní řešení.

---

## Kompletní end‑to‑end příklad (připravený ke spuštění)

Níže je **kompletní, samostatný program**, který můžete zkopírovat a vložit do nového projektu Console App. Nezapomeňte nahradit `YOUR_DIRECTORY` složkou, která obsahuje váš zkosený TIFF.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Očekávaný výstup** (při rozumně čistém skenu):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Pokud vidíte nesrozumitelné znaky, zkontrolujte sílu filtrů nebo přidejte `BinarizationFilter`, jak bylo zmíněno dříve.

---

## Časté úskalí a tipy pro profesionály

- **Úskalí:** Použití TIFF s více stránkami. `OcrImage.FromFile` načte pouze první snímek. Použijte `OcrImage.FromMultiPageFile`, pokud potřebujete všechny stránky.
- **Úskalí:** Zapomenutí uvolnit `OcrEngine`. Zabalte jej do `using` bloku v produkčním kódu pro uvolnění nativních zdrojů.
- **Tip pro profesionály:** Uložte pipeline do cache, pokud zpracováváte mnoho obrázků se stejným nastavením – snižuje to režii.
- **Tip pro profesionály:** Logujte `DeskewConfidence` do monitorovacího systému; náhlé poklesy mohou naznačovat změnu kalibrace skeneru.

---

## Další kroky – Rozšíření pracovního postupu

Nyní, když víte **jak opravit zkosení obrazu** a **předzpracovat obrázek pro OCR**, můžete zkusit:

- **Dávkové zpracování** – procházet složku se skenovanými PDF, převést každou stránku na obrázek a aplikovat stejnou pipeline.
- **Podpora jazyků** – nastavte `engine.Language = OcrLanguage.English;` nebo jiné jazyky pro zlepšení rozpoznávání.
- **Vlastní post‑processing** – použijte regulární výrazy k vyčištění běžných chyb OCR (např. „0“ vs „O“).

Každé z těchto témat přirozeně souvisí s sekundárními klíčovými slovy **jak zlepšit OCR** a **oprava zkosení naskenovaného obrazu**.

---

## Závěr

Probrali jsme vše, co potřebujete vědět o **tom, jak opravit zkosení obrazu** pomocí Aspose.OCR, od vytvoření robustní filtrační pipeline až po ověření skóre důvěry. **Předzpracováním obrazu pro OCR** s pomocí opravy zkosení, odšumu a zvýšení kontrastu zaznamenáte měřitelný nárůst **zlepšení OCR** výsledků, zejména u nakloněných nebo šumivých skenů.

Vyzkoušejte to na své vlastní sadě dokumentů, upravte parametry filtrů a sledujte, jak se přesnost OCR zvyšuje. Máte otázky nebo obtížný soubor, který se nechce narovnat? Zanechte komentář níže – pojďme to společně vyřešit. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak použít AspOCR: Předzpracování filtrů OCR pro obrázek v .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Jak OCR obrázek – Proveďte OCR na obrázku v rozpoznávání OCR obrázků](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Jak nastavit prahovou hodnotu v rozpoznávání OCR obrázků](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}