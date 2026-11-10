---
category: general
date: 2026-03-26
description: Jak spustit OCR na souboru PNG a extrahovat text z obrázku pomocí vlastního
  slovníku pro zlepšení přesnosti OCR. Naučte se rychle načíst obrázek pro OCR.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: cs
og_description: Jak spustit OCR na souboru PNG a extrahovat text z obrázku pomocí
  vlastního slovníku pro zlepšení přesnosti OCR. Krok‑za‑krokem průvodce.
og_title: Jak spustit OCR – extrahovat text z obrázku v Pythonu
tags:
- OCR
- Python
- Image Processing
title: Jak spustit OCR – Extrahovat text z obrázku v Pythonu
url: /cs/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR – Extrahovat text z obrázku v Pythonu

Už jste se někdy zamýšleli **jak spustit OCR** na naskenované faktuře nebo snímku obrazovky a získat čistý, prohledávatelný text? Nejste v tom sami. V mnoha projektech je úzkým místem prostě načtení obrázku pro OCR a následné přimlouvání enginu, aby rozuměl specifickým slovům domény.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který **extrahuje text z obrázku** souborů, ukáže vám, jak **rozpoznat text z PNG** aktiv, a dokonce předvede triky, jak **zlepšit přesnost OCR** pomocí vlastních slovníků a speciálních znaků. Na konci budete mít samostatný skript, který můžete vložit do libovolné Python kódu.

## Co budete potřebovat

- Python 3.8+ (kód používá typové nápovědy, ale funguje i na starších verzích 3.x)
- Knihovnu `ocr`, která je součástí OCR enginu, který cílíte (nainstalujte pomocí `pip install ocr‑engine` – nahraďte skutečným názvem balíčku)
- Soubor s obrázkem (`input.png`), který chcete zpracovat
- Volitelně: textový soubor (`invoice_terms.txt`) s doménově specifickými slovy, jedno na řádek

Žádné těžké externí závislosti, žádné cloudové API klíče, jen lokální OCR engine.

---

## Krok 1: Instalace a import OCR knihovny

Nejprve se ujistěte, že je OCR balíček nainstalován. Pokud používáte hypotetický balíček `ocr-engine`, spusťte:

```bash
pip install ocr-engine
```

Nyní importujte třídy, které budete potřebovat:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Tip:** Pokud používáte virtuální prostředí, aktivujte jej před instalací, aby byl váš globální Python čistý.

## Krok 2: Vytvoření instance OCR enginu

Vytvoření objektu engine je vstupním bodem pro každý OCR úkol. Představte si to jako zapnutí skenerového hardwaru v softwaru.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Proč je to důležité: engine uchovává konfiguraci, jako jsou jazykové balíčky, režimy rozpoznávání a jakékoli vlastní zdroje, které později přidáte. Bez něj nemůžete **načíst obrázek pro OCR** ani spustit rozpoznávací pipeline.

## Krok 3: Načtení obrázku, který chcete rozpoznat

Zde skutečně **načteme obrázek pro OCR**. Metoda `Imaging.Image.load()` načte soubor a převede jej do interního bitmapového formátu, který engine očekává.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Pokud máte JPEG nebo TIFF, stejná metoda funguje – stačí změnit příponu. Engine automaticky detekuje formát.

> **Okrajový případ:** Velmi velké obrázky (více než 5 MP) mohou způsobit špičky v paměti. Zvažte zmenšení pomocí Pillow před načtením, pokud narazíte na problémy s výkonem.

## Krok 4: Poskytnutí vlastního slovníku pro zvýšení přesnosti

Většina OCR engineů je dodávána s obecnými jazykovými modely. Pro faktury, účtenky nebo právní dokumenty často chybí slova. Poskytnutí vlastního seznamu slov říká engine „toto jsou platné výrazy, považujte je za správné“.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typické položky mohou být:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Přidání těchto položek dramaticky zlepšuje metriku **zlepšení přesnosti OCR** – zejména pro ne‑ASCII symboly.

## Krok 5: Přidání speciálních znaků, které nejsou v základní sadě

Pokud vaše doména používá symboly jako znak eura (€) nebo skandinávské Ø, můžete je explicitně přidat:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Engine nyní bude během fáze rozpoznávání považovat tyto glyfy za platné, čímž se sníží pravděpodobnost výstupu „odpadků“.

## Krok 6: Spuštění OCR procesu a získání textu

Nakonec zavolejte rozpoznávač a získáte výsledek jako prostý text. Volání `recognize()` vrací bohatý objekt; pro většinu případů potřebujeme jen surový řetězec.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Pokud výstup vypadá poškozeně, zkontrolujte, že váš vlastní slovník a speciální znaky jsou správně načteny.

---

## Vizualizovaný přehled

![how to run OCR diagram](ocr-workflow.png){alt="how to run OCR diagram"}

Diagram výše ilustruje tok od načtení obrázku po získání čistého textu a zdůrazňuje, kde můžete vložit vlastní slovníky a sady znaků.

---

## Časté otázky a úskalí

### Funguje to s vícestránkovými PDF?

Ano – stačí převést každou stránku na PNG (pomocí `pdf2image` nebo podobného) a předat je postupně stejné instanci `ocr_engine`. Engine zpracuje každý obrázek nezávisle, takže získáte seznam řetězců, které můžete spojit.

### Co když je obrázek otočený?

Většina moderních OCR engineů automaticky detekuje orientaci, ale můžete vynutit otočení pomocí:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Jak zacházet s jazyky jinými než angličtina?

Vyměňte jazykový model před načtením obrázku:

```python
ocr_engine.set_language("de")  # German
```

Ujistěte se, že odpovídající jazykový balíček je nainstalován.

---

## Kompletní skript – připravený ke kopírování a vložení

Níže je celý program, připravený ke spuštění po nahrazení placeholderových cest.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Spusťte jej pomocí:

```bash
python run_ocr.py
```

Měli byste vidět extrahovaný text vytištěný v konzoli. Odtud jej můžete zapsat do souboru, vložit do databáze nebo předat do následných NLP pipeline.

---

## Shrnutí a další kroky

Probrali jsme **jak spustit OCR** na PNG, jak **extrahovat text z obrázku**, a ukázali praktické způsoby **rozpoznat text z PNG** při **zlepšování přesnosti OCR** pomocí slovníků a vlastních znaků.  

Poté zvažte:

- **Dávkové zpracování:** Procházet adresář s obrázky.
- **Post‑zpracování:** Použít regex k získání čísel faktur nebo dat.
- **Integrace:** Připojit skript k Flask API pro OCR služby na vyžádání.

Pokud vás zajímají pokročilejší témata, podívejte se na tutoriály o **načtení obrázku pro OCR** s předzpracováním pomocí OpenCV, nebo se ponořte do modelů OCR založených na deep‑learningu, jako je Tesseract 4+ s LSTM vrstvami.

### Pokračujte v experimentování!

Zkuste vyměnit `invoice_terms.txt` za seznam lékařské terminologie, přidejte řecké znaky nebo dejte engine nízké rozlišení fotografie, abyste viděli, jak daleko může přesnost sahat. Čím více budete experimentovat, tím lépe pochopíte kompromisy mezi předzpracováním, vlastními slovníky a nastavením engine.

Šťastné programování a ať jsou vaše OCR výsledky vždy ostré!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}