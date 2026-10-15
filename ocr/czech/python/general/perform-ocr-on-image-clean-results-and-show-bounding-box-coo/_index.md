---
category: general
date: 2026-03-28
description: Proveďte OCR na obrázku a získejte čistý text s koordináty ohraničujících
  rámečků. Naučte se, jak extrahovat OCR, vyčistit OCR a zobrazit výsledky krok za
  krokem.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: cs
og_description: Proveďte OCR na obrázku, vyčistěte výstup a zobrazte souřadnice ohraničujícího
  rámečku v stručném tutoriálu.
og_title: Proveďte OCR na obrázku – čisté výsledky a ohraničující rámečky
tags:
- OCR
- Computer Vision
- Python
title: Proveďte OCR na obrázku – čisté výsledky a zobrazte souřadnice ohraničujícího
  rámečku
url: /cs/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Proveďte OCR na obrázku – Vyčistěte výsledek a zobrazte souřadnice ohraničujícího rámečku

Už jste někdy potřebovali **provést OCR na obrázku**, ale dostávali jste nečistý text a nevedeli, kde se každé slovo nachází na obrázku? Nejste v tom sami. V mnoha projektech – digitalizace faktur, skenování účtenek nebo jednoduché získávání textu – je získání surového výstupu OCR jen první překážkou. Dobrá zpráva? Ten výstup můžete vyčistit a okamžitě vidět souřadnice ohraničujících rámečků každého regionu, aniž byste museli psát spoustu boilerplate kódu.

V tomto průvodci si ukážeme **jak extrahovat OCR**, spustíme **post‑processor pro čištění OCR** a nakonec **zobrazíme souřadnice ohraničujících rámečků** pro každý vyčištěný region. Na konci budete mít jeden spustitelný skript, který promění rozmazanou fotografii na úhledný, strukturovaný text připravený pro další zpracování.

## Co budete potřebovat

- Python 3.9+ (syntaxe níže funguje na 3.8 a novějších)
- OCR engine, který podporuje `recognize(..., return_structured=True)` – například fiktivní knihovnu `engine` použité v úryvku. Nahraďte ji Tesseractem, EasyOCR nebo jakýmkoli SDK, které vrací data o regionech.
- Základní znalost funkcí a smyček v Pythonu
- Soubor s obrázkem, který chcete skenovat (PNG, JPG, atd.)

> **Tip:** Pokud používáte Tesseract, funkce `pytesseract.image_to_data` už poskytuje ohraničující rámečky. Můžete výsledek zabalit do malého adaptéru, který napodobuje API `engine.recognize` uvedené níže.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: diagram ukazující, jak provést OCR na obrázku a vizualizovat souřadnice ohraničujících rámečků*

## Krok 1 – Proveďte OCR na obrázku a získejte strukturované regiony

Prvním krokem je požádat OCR engine, aby nevracel jen prostý text, ale strukturovaný seznam textových regionů. Tento seznam obsahuje surový řetězec a obdélník, který jej obklopuje.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Proč je to důležité:**  
Když požadujete jen prostý text, ztratíte prostorový kontext. Strukturovaná data vám později umožní **zobrazit souřadnice ohraničujících rámečků**, zarovnat text s tabulkami nebo předat přesné polohy dalšímu modelu.

## Krok 2 – Jak vyčistit výstup OCR pomocí post‑processoru

OCR engine jsou skvělé v rozpoznávání znaků, ale často zanechávají nadbytečné mezery, artefakty konců řádků nebo špatně rozpoznané symboly. Post‑processor normalizuje text, opravuje běžné OCR chyby a ořezává bílé znaky.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Pokud si vytváříte vlastní čistič, zvažte:

- Odstranění ne‑ASCII znaků (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Sloučení více mezer do jedné mezery
- Použití kontroloru pravopisu jako `pyspellchecker` pro zjevné překlepy

**Proč by vás to mělo zajímat:**  
Úhledný řetězec usnadňuje vyhledávání, indexování a spolehlivost následných NLP pipeline. Jinými slovy, **jak vyčistit OCR** je často rozdíl mezi použitelné datové sadě a hlavou bolesti.

## Krok 3 – Zobrazte souřadnice ohraničujících rámečků pro každý vyčištěný region

Nyní, když je text čistý, projdeme každý region a vypíšeme jeho obdélník a vyčištěný řetězec. To je část, kde konečně **zobrazíme souřadnice ohraničujících rámečků**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Ukázkový výstup**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Nyní můžete tyto souřadnice předat kreslící knihovně (např. OpenCV) a překreslit rámečky na původním obrázku, nebo je uložit do databáze pro pozdější dotazy.

## Kompletní, připravený ke spuštění skript

Níže je kompletní program, který spojuje všechny tři kroky. Vyměňte placeholderové volání `engine` za vaše skutečné OCR SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Jak spustit

```bash
python perform_ocr.py sample_invoice.jpg
```

Měli byste vidět seznam ohraničujících rámečků spárovaných s vyčištěným textem, přesně jako ve výše uvedeném ukázkovém výstupu.

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Co když OCR engine nepodporuje `return_structured`?** | Napište tenký wrapper, který převede surový výstup engine (obvykle seznam slov s koordináty) na objekty s atributy `text` a `bounding_box`. |
| **Mohu získat skóre důvěry?** | Mnoho SDK poskytuje metriku důvěry pro každý region. Přidejte ji do výpisu: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Jak zacházet s otočeným textem?** | Předzpracujte obrázek pomocí OpenCV `cv2.minAreaRect` a deskewujte jej před voláním `recognize`. |
| **Co když potřebuji výstup v JSON?** | Serializujte `processed_result.regions` pomocí `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Existuje způsob, jak vizualizovat rámečky?** | Použijte OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` uvnitř smyčky, pak `cv2.imwrite("annotated.jpg", img)`. |

## Závěr

Právě jste se naučili **jak provést OCR na obrázku**, vyčistit surový výstup a **zobrazit souřadnice ohraničujících rámečků** pro každý region. Tříkrokový tok – rozpoznání → post‑processing → iterace – je znovupoužitelný vzor, který můžete vložit do jakéhokoli Python projektu vyžadujícího spolehlivé získávání textu.

### Co dál?

- **Prozkoumejte různé OCR back‑endy** (Tesseract, EasyOCR, Google Vision) a porovnejte přesnost.
- **Integraujte s databází** pro ukládání dat o regionech a vyhledávat v archivách.
- **Přidejte detekci jazyka** a směrujte každý region přes odpovídající kontrolor pravopisu.
- **Překryjte rámečky na původní obrázek** pro vizuální ověření (viz výše uvedený OpenCV úryvek).

Pokud narazíte na podivnosti, pamatujte, že největší výhoda pochází ze solidního post‑processing kroku; čistý řetězec je mnohem snazší pracovat než surový výpis znaků.

Šťastné kódování a ať jsou vaše OCR pipeline vždy úhledné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}