---
category: general
date: 2026-06-22
description: Získejte souřadnice ohraničujícího rámečku z obrázků pomocí Pythonu.
  Naučte se během několika minut extrahovat text z obrázku v Pythonu pomocí Aspose
  OCR a parsování JSON.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: cs
og_description: Získejte souřadnice ohraničujícího rámečku z obrázků pomocí Pythonu.
  Tento průvodce ukazuje, jak extrahovat text z obrázku v Pythonu pomocí Aspose OCR
  a analyzovat data o rozložení.
og_title: Získání souřadnic ohraničujícího rámečku z OCR v Pythonu – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Získání souřadnic ohraničujícího rámečku z OCR v Pythonu – Kompletní průvodce
url: /cs/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání souřadnic ohraničujícího rámečku z OCR v Pythonu – Kompletní průvodce

Už jste někdy potřebovali **získat souřadnice ohraničujícího rámečku** pro každé slovo ve skenované faktuře, ale nevedeli jste, kde začít? Nejste v tom sami. V mnoha automatizačních projektech musíte najít text na obrázku, abyste jej mohli zvýraznit, zakrýt nebo předat do následné analytiky. Dobrá zpráva? Několika řádky Pythonu a Aspose.OCR můžete získat jak text, **tak** i jeho přesnou polohu v jednom kroku.

V tomto tutoriálu vás provedeme praktickým příkladem, který ukazuje, jak **extrahovat text z obrázku v Pythonu**, a poté se ponoříme do JSON dat rozvržení, abychom získali ty ohraničující rámečky. Žádné zbytečnosti, jen funkční skript, vysvětlení, proč je každý krok důležitý, a tipy, jak se vyhnout běžným úskalím.

---

## Co vytvoříte

Na konci tohoto průvodce budete mít připravený spustitelný Python skript, který:

1. Načte obrázek (např. fakturu ve formátu PNG) do Aspose OCR.
2. Nakonfiguruje engine tak, aby vydával informace o rozvržení v JSON.
3. Převede JSON do Python slovníku.
4. Projde každé rozpoznané slovo a vypíše jeho text **a** souřadnice ohraničujícího rámečku.

Také uvidíte, jak přizpůsobit kód pro více‑stránkové PDF, různé formáty obrázků a vlastní souřadnicové systémy.

### Požadavky

- Python 3.8+ nainstalovaný na vašem počítači.  
- Aktivní licence Aspose.OCR pro Python nebo bezplatná zkušební verze (knihovna funguje i bez licence, ale přidá vodoznak).  
- `pip install aspose-ocr` (název balíčku na PyPI).  
- Vzorek obrázku pojmenovaný `invoice.png` umístěný ve složce, na kterou můžete odkazovat.

To je vše—žádné těžké frameworky, žádné externí služby. Pojďme na to.

---

## Krok 1: Instalace a import požadovaných knihoven

Nejprve se ujistěte, že je k dispozici balíček Aspose OCR a vestavěný modul `json`. Modul `json` je součástí Pythonu, takže stačí nainstalovat pouze Aspose.

```bash
pip install aspose-ocr
```

Nyní je importujte ve svém skriptu:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Proč je to důležité:** Importování `aspose.ocr` vám poskytuje přístup k vysoce výkonnému OCR engine, zatímco `json` vám umožňuje převést surový řetězec rozvržení na nativní Python slovník pro snadnou procházení.

---

## Krok 2: Vytvoření OCR engine a načtení obrázku

Engine je srdcem procesu. Vytvoříte jeho instanci a poté ji nasměrujete na obrázek, který chcete skenovat.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Tip:** Nahraďte `"YOUR_DIRECTORY/invoice.png"` absolutní nebo relativní cestou, která ukazuje na váš skutečný soubor. Pokud soubor není nalezen, Aspose vyvolá `FileNotFoundError`, takže zkontrolujte pravopis.

---

## Krok 3: Konfigurace engine pro výstup JSON dat rozvržení

Aspose OCR může vrátit čistý text, OCR‑pouze JSON, nebo úplný JSON rozvržení, který zahrnuje souřadnice pro slova, řádky a dokonce i jednotlivé znaky. Pro **získání souřadnic ohraničujícího rámečku** potřebujeme JSON rozvržení.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Proč JSON?** JSON je jazykově nezávislý, čitelný pro člověka a snadno se mapuje na Python slovníky. JSON rozvržení obsahuje pole `"words"`, kde každý záznam obsahuje text a pole `boundingBox` s osmi čísly (čtyři rohové body).

---

## Krok 4: Spuštění rozpoznání a získání surového JSON řetězce

Nyní skutečně spustíme OCR. Metoda `recognize()` vrací objekt `OcrResult`, ze kterého můžeme získat JSON řetězec.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Pokud vytisknete `layout_json`, uvidíte něco jako:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Hraniční případ:** Některé obrázky mohou vytvořit prázdná pole `"words"` pokud OCR engine nedokáže detekovat žádný text. V takovém případě ověřte kvalitu obrázku (kontrast, rozlišení) před pokračováním.

---

## Krok 5: Parsování JSON do Python slovníku

Práce s nativními Python strukturami je mnohem jednodušší než manipulace s řetězci. Použijte funkci `json.loads()` k převodu řetězce.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Nyní `layout_data["words"]` je seznam slovníků, z nichž každý představuje slovo a jeho ohraničující rámeček.

---

## Krok 6: Procházení slov a **získání souřadnic ohraničujícího rámečku**

Zde je jádro našeho tutoriálu: iterace přes každé slovo, extrakce textu a výpis souřadnic. Toto je přesně místo, kde **získáváme souřadnice ohraničujícího rámečku**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Ukázkový výstup** (vaše čísla se budou lišit podle obrázku):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Proč formát s osmi body?** Čtyři rohy (vlevo‑nahoře, vpravo‑nahoře, vpravo‑dole, vlevo‑dole) vám umožňují nakreslit polygon kolem slova, i když je text nakřivený. Pokud potřebujete jen jednoduchý obdélník, můžete vypočítat `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` a `height = max(y…) - y_min`.

---

## Volitelné vylepšení

### 1. Převod ohraničujících rámečků na jednoduché obdélníky

Pokud váš následný nástroj očekává `(x, y, šířka, výška)` místo osmi bodů, přidejte pomocnou funkci:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Zpracování více‑stránkových PDF

Aspose OCR může přijímat PDF proudy. Nahraďte řádek načítání obrázku tímto:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterujte `set_page_number` pro každou stránku a sbírejte souřadnice podle stránky.

### 3. Vizualizace ohraničujících rámečků

Pokud chcete vidět rámečky nakreslené na původním obrázku, použijte Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Nyní uvidíte červené obrysy kolem každého rozpoznaného slova—ideální pro ladění nebo UI překrytí.

---

## Časté otázky a úskalí

- **Co když je JSON obrovský?** Pro velké dokumenty zvažte streamování JSON nebo zpracování stránku po stránce, aby se snížila spotřeba paměti.
- **Proč některá slova chybí?** Nízký kontrast nebo ručně psaný text často selhává OCR engine. Před předáním Aspose předzpracujte obrázek (zvyšte kontrast, binarizujte).
- **Mohu získat souřadnice na úrovni znaků?** Ano—nastavte `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`, aby se vrátil pole `"characters"` s vlastním `boundingBox`.
- **Je souřadnicový systém nulový?** Ano. (0, 0) je levý horní roh obrázku.

---

## Kompletní skript – připravený ke zkopírování a spuštění

Níže je kompletní, spustitelný příklad, který kombinuje všechny kroky. Uložte jej jako `extract_bboxes.py` a spusťte `python extract_bboxes.py`.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – krok za krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak použít Aspose OCR pro JSON výsledek při rozpoznávání obrázku](/ocr/english/net/text-recognition/get-result-as-json/)
- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}