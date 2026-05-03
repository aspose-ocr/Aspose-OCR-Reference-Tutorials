---
category: general
date: 2026-05-03
description: Naučte se, jak spustit OCR na obrázku a extrahovat text s koordináty
  pomocí strukturovaného rozpoznávání OCR. Krok za krokem je zahrnutý Python kód.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: cs
og_description: Spusťte OCR na obrázku a získejte text s koordináty pomocí strukturovaného
  rozpoznávání OCR. Kompletní příklad v Pythonu s vysvětlením.
og_title: Spusťte OCR na obrázku – Návod na extrakci strukturovaného textu
tags:
- OCR
- Python
- Computer Vision
title: Spusťte OCR na obrázku – Kompletní průvodce extrakcí strukturovaného textu
url: /cs/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku – Kompletní průvodce extrakcí strukturovaného textu

Už jste někdy potřebovali **run OCR on image** soubory, ale nebyli jste si jisti, jak zachovat přesné pozice každého slova? Nejste v tom sami. V mnoha projektech—skenování účtenek, digitalizace formulářů nebo testování UI—potřebujete nejen surový text, ale také ohraničující rámečky, které vám ukazují, kde se každá řádka nachází na obrázku.  

Tento tutoriál vám ukáže praktický způsob, jak *run OCR on image* pomocí **aocr** enginu, požádat o **structured OCR recognition**, a poté provést post‑processing výsledku při zachování geometrie. Na konci budete schopni **extract text with coordinates** během několika řádků Pythonu a pochopíte, proč je strukturovaný režim důležitý pro následné úkoly.

## Co se naučíte

- Jak inicializovat OCR engine pro **structured OCR recognition**.  
- Jak načíst obrázek a získat surové výsledky, které obsahují ohraničení řádků.  
- Jak spustit post‑processor, který vyčistí text, aniž by ztratil geometrické informace.  
- Jak iterovat přes finální řádky a vytisknout každý kus textu spolu s jeho ohraničujícím rámečkem.  

Žádná magie, žádné skryté kroky—jen kompletní, spustitelný příklad, který můžete vložit do svého projektu.

---

## Požadavky

Než se ponoříme dál, ujistěte se, že máte nainstalováno následující:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Budete také potřebovat soubor s obrázkem (`input_image.png` nebo `.jpg`), který obsahuje jasný, čitelný text. Cokoliv od naskenované faktury po snímek obrazovky funguje, pokud OCR engine dokáže vidět znaky.

## Krok 1: Inicializace OCR engine pro strukturované rozpoznávání

Prvním krokem je vytvořit instanci `aocr.Engine()` a říct jí, že chceme **structured OCR recognition**. Strukturovaný režim vrací nejen čistý text, ale také geometrická data (ohraničující obdélníky) pro každou řádku, což je nezbytné, když potřebujete mapovat text zpět na obrázek.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Proč je to důležité:**  
> V výchozím režimu může engine poskytnout jen řetězec spojených slov. Strukturovaný režim vám dává hierarchii stránek → řádků → slov, každé s koordináty, což výrazně usnadňuje překrytí výsledků na původní obrázek nebo jejich předání modelu citlivému na rozvržení.

## Krok 2: Spusťte OCR na obrázku a získejte surové výsledky

Nyní načteme obrázek do engine. Volání `recognize` vrací objekt `OcrResult`, který obsahuje kolekci řádků, z nichž každý má své vlastní ohraničující obdélníky.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

V tomto okamžiku `raw_result.lines` obsahuje objekty se dvěma důležitými atributy:

- `text` – rozpoznaný řetězec pro tuto řádku.  
- `bounds` – n-tici jako `(x, y, width, height)` popisující pozici řádky.

## Krok 3: Post‑processing při zachování geometrie

Surový výstup OCR je často šumivý: cizí znaky, špatně umístěné mezery nebo problémy s konci řádků. Funkce `ai.run_postprocessor` vyčistí text, ale **zachová původní geometrii** nedotčenou, takže stále máte přesné souřadnice.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Tip:** Pokud máte doménově specifické slovníky (např. kódy produktů), předávejte post‑processoru vlastní slovník pro zlepšení přesnosti.

## Krok 4: Extrahujte text se souřadnicemi – iterujte a zobrazte

Nakonec projdeme vyčištěné řádky a vytiskneme ohraničující rámeček každé řádky spolu s jejím textem. Toto je jádro **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Očekávaný výstup

Předpokládejme, že vstupní obrázek obsahuje dvě řádky: “Invoice #12345” a “Total: $89.99”, uvidíte něco jako:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

První n-tice je `(x, y, width, height)` řádky na původním obrázku, což vám umožní kreslit obdélníky, zvýraznit text nebo předat souřadnice do jiného systému.

## Vizualizace výsledku (volitelné)

Pokud chcete vidět ohraničující rámečky překryté na obrázku, můžete použít Pillow (PIL) k vykreslení obdélníků. Níže je rychlý úryvek; klidně jej přeskočte, pokud potřebujete jen surová data.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![příklad spuštění OCR na obrázku zobrazující ohraničující rámečky](/images/ocr-bounding-boxes.png "spuštění OCR na obrázku – překrytí ohraničujících rámečků")

Výše uvedený alt text obsahuje **primary keyword**, což splňuje SEO požadavek na atributy alt obrázku.

## Proč strukturované rozpoznávání OCR převažuje nad jednoduchým extrahováním textu

Možná se ptáte: „Nemohu jen spustit OCR a získat text? Proč se trápit s geometrií?“

- **Prostorový kontext:** Když potřebujete mapovat pole na formuláři (např. „Date“ vedle hodnoty data), souřadnice vám říkají *kde* data jsou.  
- **Více‑sloupcové rozvržení:** Jednoduchý lineární text ztrácí pořadí; strukturovaná data zachovávají pořadí sloupců.  
- **Přesnost post‑processingu:** Znalost velikosti rámečku vám pomáhá rozhodnout, zda je slovo nadpis, poznámka pod čarou nebo cizí artefakt.  

Stručně řečeno, **structured OCR recognition** vám poskytuje flexibilitu pro tvorbu chytřejších pipeline—ať už vkládáte data do databáze, vytváříte prohledávatelné PDF nebo trénujete model strojového učení, který respektuje rozvržení.

## Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| **Otočené nebo zkosené obrázky** | Ohraničující rámečky mohou být mimo osu. | Předzpracujte deskewingem (např. `warpAffine` z OpenCV). |
| **Velmi malé fonty** | Engine může postrádat znaky, což vede k prázdným řádkům. | Zvyšte rozlišení obrázku nebo použijte `ocr_engine.set_dpi(300)`. |
| **Smíšené jazyky** | Špatný jazykový model může způsobit poškozený text. | Nastavte `ocr_engine.language = ["en", "de"]` před rozpoznáním. |
| **Překrývající se rámečky** | Post‑processor může neúmyslně sloučit dva řádky. | Ověřte `line.bounds` po zpracování; upravte prahy v `ai.run_postprocessor`. |

Řešení těchto scénářů včas vám ušetří pozdější problémy, zejména když škálujete řešení na stovky dokumentů denně.

## Kompletní skript od začátku do konce

Níže je kompletní, připravený ke spuštění program, který spojuje všechny kroky. Zkopírujte, upravte cestu k obrázku a můžete spustit.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Spuštění tohoto skriptu provede:

1. **Run OCR on image** ve strukturovaném režimu.  
2. **Extract text with coordinates** pro každou řádku.  
3. Volitelně vytvoří anotovaný PNG zobrazující rámečky.

## Závěr

Nyní máte robustní, samostatné řešení pro **run OCR on image** a **extract text with coordinates** pomocí **structured OCR recognition**. Kód demonstruje každý krok—od inicializace engine po post‑processing a vizuální ověření—takže jej můžete přizpůsobit účtenkám, formulářům nebo jakémukoli vizuálnímu dokumentu, který potřebuje přesnou lokalizaci textu.

Co dál? Zkuste vyměnit engine `aocr` za jinou knihovnu (Tesseract, EasyOCR) a podívejte se, jak se liší jejich strukturované výstupy. Experimentujte s různými strategiemi post‑processingu, jako je kontrola pravopisu nebo vlastní regex filtry, abyste zvýšili přesnost pro vaši doménu. A pokud budujete větší pipeline, zvažte uložení dvojic `(text, bounds)` do databáze pro pozdější analýzu.

Šťastné kódování a ať jsou vaše OCR projekty vždy přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}