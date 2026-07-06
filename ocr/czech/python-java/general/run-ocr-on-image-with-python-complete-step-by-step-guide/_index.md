---
category: general
date: 2026-06-06
description: Spusťte OCR na obrázku pomocí Pythonu a zobrazte skóre důvěryhodnosti.
  Naučte se, jak filtrovat slova s nízkou důvěrou, nastavit prahy a řešit okrajové
  případy.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: cs
og_description: Spusťte OCR na obrázku v Pythonu, zkontrolujte úrovně spolehlivosti
  a odfiltrujte slova s nízkou spolehlivostí. Tento tutoriál vás provede kompletním,
  spustitelným příkladem.
og_title: Spusťte OCR na obrázku pomocí Pythonu – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Spusťte OCR na obrázku pomocí Pythonu – Kompletní krok‑za‑krokem průvodce
url: /cs/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku pomocí Pythonu – Kompletní krok‑za‑krokem průvodce

Už jste někdy potřebovali **spustit OCR na obrázku** soubory, ale nebyli jste si jisti, jak z nich získat spolehlivý text? Nejste sami – mnoho vývojářů narazilo na stejný problém, když extrahovaná slova vypadají nejistě a skóre důvěry je záhadou.  

V tomto průvodci se ponoříme přímo do fungujícího řešení: uvidíte, jak **spustit OCR na obrázku**, přečíst celkovou důvěru a vybrat slova s nízkou důvěrou, která mohou vyžadovat ruční kontrolu. Na konci budete mít znovupoužitelný skript, pochopíte, proč je každý řádek důležitý, a budete vědět, jak upravit prahovou hodnotu důvěry pro své vlastní projekty.

## Co tento tutoriál pokrývá

Provedeme vás celým pracovním postupem – od načtení obrázku po vytištění přehledné zprávy o slovech, která spadla pod 80 % hranici důvěry. Během toho si probereme:

* Výběr spolehlivého OCR enginu (použijeme **EasyOCR**, populární Python OCR knihovnu)  
* Interpretaci atributu `confidence`, který vrací každý OCR výsledek  
* Filtrování slov pomocí vlastního **práhu důvěry OCR**  
* Rozšíření skriptu pro dávkové zpracování nebo alternativní enginy jako **pytesseract**  

Předchozí zkušenost s OCR není vyžadována, stačí základní znalost Pythonu a funkční prostředí (doporučeno Python 3.9+).  

Připraveni proměnit rozmazané snímky obrazovky na čistý, prohledávatelný text? Pojďme na to.

---

## ## Jak spustit OCR na obrázku pomocí Pythonu

Jádrem tutoriálu je tříkrokový úryvek, který odráží kód, který jste již viděli. Níže rozložíme každý řádek, vysvětlíme proč, a poté vám poskytneme kompletní skript připravený ke kopírování a vložení.

### Krok 1: Instalace a import OCR enginu

Nejprve se ujistěte, že je OCR knihovna k dispozici. **EasyOCR** funguje ihned pro mnoho jazyků a poskytuje skóre důvěry pro každé slovo.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Proč EasyOCR?* Obsahuje model hlubokého učení, který byl trénován na různorodých datech, takže obvykle získáte vyšší hodnoty důvěry než u staršího enginu Tesseract, zejména u obrázků smíšené kvality.

> **Tip:** Pokud pracujete v omezeném prostředí (např. malý Docker kontejner), `pytesseract` může být lehčí, ale ztratíte část moderní přesnosti, kterou EasyOCR poskytuje.

### Krok 2: Spustit OCR na obrázku

Nyní skutečně **spustíme OCR na obrázku**. Metoda `recognize_image` z původního příkladu je nahrazena voláním `readtext` z EasyOCR, které vrací seznam n-tic `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Každý záznam v `ocr_results` vypadá takto:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Třetí prvek (`0.92` v příkladu) je skóre důvěry v rozmezí 0 a 1.

### Krok 3: Shrnutí celkové důvěry

Na rozdíl od předchozího úryvku, který vytiskl jediný atribut `confidence`, EasyOCR poskytuje důvěru pro každé slovo. Pro získání celkového dojmu je zprůměrujeme:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Proč průměrovat?* Poskytuje rychlou kontrolu zdraví – pokud je celková důvěra pod, řekněme, 70 %, pravděpodobně budete muset vylepšit obrázek (lepší osvětlení, předzpracování atd.).

### Krok 4: Seznam slov s nízkou důvěrou

Nyní přichází část, která přímo odpovídá požadavku „seznam slov, jejichž důvěra je pod požadovaným prahem“. Výchozí **práh důvěry OCR** nastavíme na 0.80 (80 %), ale můžete jej upravit.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Smyčka vytiskne každé slovo, které neprošlo, spolu s procentuální důvěrou. Jedná se o přesný ekvivalent původní smyčky `for recognized_word in recognition_result.words`, ale nyní funguje s výstupním formátem EasyOCR.

---

## ## Porozumění skóre důvěry OCR

Důvěra není magické číslo; je to odhad modelu, jak si je jistý konkrétní transkripcí. Zde je několik věcí, na které je třeba pamatovat:

| Situace | Typická důvěra | Co dělat |
|-----------|-------------------|------------|
| Čistý, vysoce rozlišený sken | 0.95 – 1.00 | Není potřeba žádná další práce |
| Mírné rozmazání nebo nerovnoměrné osvětlení | 0.80 – 0.94 | Zvažte mírné předzpracování (zvýšení kontrastu) |
| Silný šum, natočený text | < 0.70 | Použijte předzpracování obrazu (odklon, odstranění šumu) nebo přepněte na jiný OCR engine |

> **Pozor:** Některé jazyky (např. kurzívní ruční psaní) přirozeně produkují nižší skóre. Přizpůsobte prahovou hodnotu podle toho.

### Okrajové případy a varianty

1. **Dávkové zpracování** – Pokud potřebujete **spustit OCR na obrázku** soubory hromadně, zabalte výše uvedenou logiku do smyčky, která prochází adresář.  
2. **Více jazyků** – Předávejte seznam jako `['en', 'fr']` do `easyocr.Reader` a engine detekuje oba.  
3. **Alternativní enginy** – Chcete vyzkoušet **pytesseract**? Nahraďte blok čtečky tímto:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Pak budete muset agregovat důvěry na úrovni znaků do důvěry na úrovni slov – trochu více práce, ale proveditelné.

4. **Triky předzpracování** – Použití filtrů OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) může zvýšit důvěru u šumivých skenů.  

---

## ## Kompletní, připravený skript

Níže je kompletní soubor Python, který můžete vložit do svého projektu. Uložte jej jako `ocr_report.py` a spusťte `python ocr_report.py`. Ujistěte se, že cesta k obrázku ukazuje na existující soubor.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Očekávaný výstup** (vaše čísla se mohou lišit):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Pokud každé slovo překročí 80 % práh, uvidíte přátelskou zprávu „All words meet the confidence threshold.“ místo toho.

---

## ## Často kladené otázky (FAQ)

**Q: Funguje to s PDF soubory?**  
A: Ne přímo. Nejprve převěďte každou stránku PDF na obrázek (např. pomocí `pdf2image`) a poté vložte PNG/JPEG do skriptu.

**Q: Moje čísla důvěry jsou všechna nízká – co mohu udělat?**  
A: Zkuste předzpracování obrazu: zvýšte kontrast, odstraňte šum pozadí nebo otočte obrázek do vodorovné osy. EasyOCR také přijímá parametr `contrast_ths`, který můžete ladit.

**Q: Můžu exportovat výsledky do CSV?**  
A: Rozhodně. Po smyčce s nízkou důvěrou zapište `ocr_results` do `csv.DictWriter`, kde každý řádek obsahuje `text`, `confidence` a souřadnice ohraničujícího rámečku.

**Q: Existuje verze akcelerovaná GPU?**  
A: EasyOCR automaticky používá CUDA, pokud je nainstalován kompatibilní GPU a PyTorch. Ověřte pomocí `torch.cuda.is_available()` před spuštěním skriptu.

---

## Závěr

Právě jsme **spustili OCR na obrázku** pomocí Pythonu, prozkoumali celkovou důvěru a izolovali jakákoli slova s nízkou důvěrou, která potřebují

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou ovládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak nastavit hodnotu prahu v OCR rozpoznávání obrazu](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Jak použít Aspose OCR pro JSON výsledek v rozpoznávání obrazu](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}