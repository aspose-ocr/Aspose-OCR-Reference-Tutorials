---
category: general
date: 2026-04-26
description: Jak rychle a spolehlivě vytvořit OCR. Naučte se extrahovat text z obrázku,
  načíst obrázek pro OCR a spustit OCR na PNG s vlastním slovníkem.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: cs
og_description: Jak vytvořit OCR v Pythonu a extrahovat text z obrázku. Tento průvodce
  ukazuje, jak načíst obrázek pro OCR, spustit OCR na PNG a použít vlastní slovník.
og_title: Jak vytvořit OCR v Pythonu – Rychlé získávání textu
tags:
- OCR
- Python
- Image Processing
title: Jak vytvořit OCR v Pythonu – Extrahovat text z obrázku
url: /cs/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit OCR v Pythonu – krok za krokem průvodce

Už jste se někdy zamýšleli **jak vytvořit OCR**, které dokáže číst vaše naskenované PDF, snímky obrazovky nebo ručně psané poznámky? Nejste v tom sami. V mnoha reálných projektech potřebujeme *extrahovat text z obrázku* souborů, ale výchozí enginy často selhávají u slov specifických pro danou doménu.

V tomto tutoriálu uvidíte kompletní, spustitelný příklad, který načte obrázek pro OCR, použije vlastní slovník a nakonec **spustí OCR na PNG** souborech. Na konci budete schopni extrahovat text z libovolného obrázku a přizpůsobit engine vaší vlastní terminologii.

## Co tento tutoriál pokrývá

* Instalace malého, ale výkonného balíčku `aocr` (nebo jakékoli kompatibilní knihovny).  
* Konfigurace **vlastního slovníku**, aby byly rozpoznány termíny jako `aspocorp` nebo `licensekey`.  
* **Načtení obrázku pro OCR**, ať už jde o PNG, JPEG nebo naskenovanou stránku PDF.  
* Spuštění OCR procesu a vytištění výsledku.

Žádné externí odkazy na dokumentaci, jen samostatné řešení, které můžete dnes zkopírovat a spustit.

### Požadavky

* Python 3.8 nebo novější (kód používá f‑stringy).  
* Základní znalost příkazové řádky – budete zadávat několik příkazů `pip install`.  
* Soubor s obrázkem (`technical_doc.png` v příkladu) umístěný na místě, na které můžete odkazovat.

Pokud splňujete tyto tři položky, můžete začít.

---

## Krok 1: Instalace OCR knihovny

Nejprve potřebujeme OCR engine, který podporuje programovatelný konfigurační objekt. Balíček `aocr` je lehký wrapper kolem nativního OCR engine a dobře se hodí pro ukázky.

```bash
# Install the library (run once)
pip install aocr
```

> **Tip:** Pokud používáte Windows a narazíte na chybu při kompilaci, zkuste `pip install aocr‑binary`, který poskytuje předkompilované balíčky.

### Proč instalovat tuto knihovnu?

`aocr` nám poskytuje přímý přístup k objektu `config`, kde můžeme vložit **vlastní slovník**. To je tajná ingredience pro zlepšení přesnosti u specifických slovníků.

---

## Krok 2: Vytvoření instance OCR engine a přidání vlastního slovníku

Nyní spustíme engine a řekneme mu, která slova má považovat za známá.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Proč je vlastní slovník důležitý

Standardní OCR modely jsou trénovány na obecných korpusech. Když model uvidí „aspocorp“, může jej rozdělit na „aspo corp“ nebo úplně vynechat písmena. Poskytnutím vlastního seznamu nasměrujeme rozpoznávač k přesnému pravopisu, který potřebujeme, a výrazně snížíme úsilí při post‑zpracování.

---

## Krok 3: Načtení obrázku, který chcete zpracovat

Zde **načteme obrázek pro OCR**. Metoda `Image.load` přijímá řetězec cesty a automaticky určuje typ souboru.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Hraniční případ:** Pokud je vaším zdrojem více‑stránkový PDF, nejprve převeďte každou stránku na PNG (např. pomocí `pdf2image`) a podávejte je po jedné engine.

### Tipy pro lepší kvalitu obrázku

* Udržujte rozlišení alespoň 300 dpi.  
* Zajistěte, aby byl obrázek ve správné orientaci; v případě potřeby otočte pomocí `Pillow`.  
* Převádějte barevné skeny na odstíny šedi, aby se snížil šum.

---

## Krok 4: Spuštění OCR procesu na PNG souboru

S nakonfigurovaným engine a načteným obrázkem konečně **spustíme OCR na PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

Volání `process()` vrací objekt, který obsahuje rozpoznaný text, skóre důvěry a ohraničující rámečky pro každé slovo.

---

## Krok 5: Výstup rozpoznaného textu

Nejjednodušší způsob, jak zjistit, co engine našel, je vytisknout atribut `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Očekávaný výstup

Pokud `technical_doc.png` obsahuje větu *„The Aspocorp licensekey expires on 2025‑12‑31.“*, měla by konzole zobrazit:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Všimněte si, jak vlastní slovník zachoval název značky beze změny – něco, co by základní OCR mohlo zkomolit.

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý skript, připravený k uložení jako `run_ocr.py`. Stačí nahradit zástupnou cestu umístěním vašeho obrázku.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Run it from the terminal:

```bash
python run_ocr.py
```

Měli byste vidět extrahovaný text vytištěný v konzoli, přesně tak, jak je uvedeno v předchozím příkladu.

---

## Často kladené otázky (FAQ)

| Question | Answer |
|----------|--------|
| **Mohu extrahovat text ze skenovaného PDF?** | Ano. Nejprve převeďte každou stránku na PNG (nebo TIFF) a poté načtěte obrázky do stejného skriptu. |
| **Co když je můj obrázek JPEG místo PNG?** | Metoda `Image.load` podporuje JPEG, BMP, TIFF i PNG přímo. Stačí změnit příponu souboru. |
| **Jak zlepšit přesnost u skenů s nízkým kontrastem?** | Předzpracujte pomocí `Pillow` – zvýšte kontrast, aplikujte binarizaci nebo použijte `opencv` k vyrovnání. |
| **Je možné získat skóre důvěry pro každé slovo?** | `ocr_result` obsahuje `words` – každé slovo má atribut `confidence`, který můžete iterovat. |
| **Mohu to spustit na serveru bez grafického rozhraní?** | Rozhodně. `aocr` nemá žádné GUI závislosti, což ho činí ideálním pro CI pipeline. |

---

## Další kroky a související témata

Nyní, když víte **jak vytvořit OCR** a **extrahovat text z obrázku**, zvažte prozkoumání:

* **Techniky předzpracování** – `load image for OCR` je jen první krok; použijte `opencv` k odšumu nebo zaostření.  
* **Dávkové zpracování** – projděte adresář PNG souborů a vytvořte prohledávatelný archiv.  
* **Podpora více jazyků** – přidejte jazykové balíčky do engine, pokud potřebujete číst francouzské nebo německé dokumenty.  
* **Integrace s Elasticsearch** – indexujte extrahovaný text pro full‑textové vyhledávání napříč skenovanými zdroji.

Každé z těchto rozšíření staví na základním vzoru, který jsme právě pokryli, takže přechod bude bezproblémový.

---

## Závěr

Během několika minut jsme odpověděli na otázku **jak vytvořit OCR**, které spolehlivě **extrahuje text z obrázku**, zejména PNG, a ukázali jsme vám, jak **načíst obrázek pro OCR**, použít **vlastní slovník** a **spustit OCR na PNG** bez jakýchkoli externích služeb.

Vyzkoušejte skript, upravte slovník tak, aby odpovídal vašemu vlastnímu žargonu, a získáte pevný základ pro jakýkoli projekt digitalizace dokumentů.

Pokud narazíte na problémy, zanechte komentář níže – rádi pomůžeme. A nezapomeňte sdílet své úspěšné příběhy; komunita se nejlépe učí z reálných příkladů.

**Připravení automatizovat papírování?** Vezměte si kód, upravte ho a začněte dnes převádět pixely na prohledávatelný text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}