---
category: general
date: 2026-07-05
description: Jak rychle vyrovnat sklon obrázku. Naučte se předzpracovat obrázek pro
  OCR, opravit rotaci obrázku a převést sken na text pomocí Pythonu.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: cs
og_description: Jak vyrovnat obrázek a předzpracovat jej pro OCR. Tento návod ukazuje,
  jak opravit rotaci obrázku a extrahovat text z obrázku pomocí Pythonu.
og_title: Jak vyrovnat obrázek – krok za krokem předzpracování OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Jak narovnat obrázek – Kompletní průvodce pro předzpracování OCR
url: /cs/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak deskewovat obrázek – Kompletní průvodce pro předzpracování OCR

Už jste se někdy zamýšleli **jak deskewovat obrázek** soubory, které vypadají, jako by byly pořízeny zkřiveným skenerem? Nejste v tom sami. V mnoha reálných projektech je první věc, kterou musíte udělat, než **extrahujete text z obrázku**, narovnat ten náklon.  

V tomto tutoriálu projdeme praktickým, kompletním příkladem, který **předzpracuje obrázek pro OCR**, opraví rotaci a nakonec **převede sken na text** pomocí Python OCR knihovny. Žádné vágní odkazy, jen funkční skript, který můžete zkopírovat a vložit, plus tipy na běžné úskalí.  

## Co dosáhnete

* Načtěte libovolný naskenovaný JPEG nebo PNG, který je mírně nakloněný.  
* Použijte filtr deskew a krok binarizace pro zvýšení přesnosti OCR.  
* Spusťte OCR engine a **spolehlivě extrahujte text z obrázku**.  
* Pochopte, proč **správná rotace obrázku** má význam pro následnou extrakci textu.  

### Požadavky

* Python 3.9+ nainstalovaný na vašem počítači.  
* Balíček OCR instalovatelný přes pip, který napodobuje jmenný prostor `ocr` použitý v příkladu (například tenký wrapper kolem Tesseract).  
* Základní znalost Python funkcí a konceptů zpracování obrazu.  

Pokud je máte, pojďme na to.

![how to deskew image example](deskew_before_after.png){alt="jak deskewovat obrázek – před a po korekci"}

## Krok 1: Nastavte OCR engine – Jak deskewovat obrázek pomocí Pythonu

Nejprve: potřebujete OCR engine, který dokáže rozumět jazyku vašeho dokumentu. Níže uvedený úryvek ukazuje minimální boilerplate pro vytvoření engine a nastavení, že pracujete s anglickým textem.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Proč je to důležité:*  Nastavení jazyka engine ovlivňuje použité znaky a slovník. Přeskočení tohoto kroku může způsobit, že OCR špatně interpretuje běžná slova, zejména po **opravení rotace obrázku**.

## Krok 2: Načtěte naskenovaný obrázek, který chcete narovnat

Nyní načteme soubor do paměti. Nahraďte `"YOUR_DIRECTORY/skewed_scan.jpg"` cestou k vašemu vlastnímu obrázku.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Pokud je obrázek již v NumPy poli nebo v OpenCV `Mat`, můžete načítač upravit podle toho – klíčové je, aby objekt poskytoval metodu `apply_filter` používanou později.

## Krok 3: Předzpracujte obrázek pro OCR – Deskew a Binarizace

Zde se děje kouzlo. Spojíme dva filtry:

1. **Deskew** – automaticky detekuje dominantní textovou základnu a otočí obrázek zpět do horizontální polohy.  
2. **Binarize (Otsu)** – převádí obrázek na čistou černobílou verzi, což dramaticky zvyšuje míru rozpoznání.  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Tip:*  Pokud si všimnete, že text po binarizaci stále vypadá rozmazaně, zkuste upravit kontrast nebo použít jinou metodu prahování. Modul `ocr.Filter` často obsahuje `adaptive_threshold()` pro náročnější případy.

## Krok 4: Spusťte OCR – Extrahujte text z obrázku

S čistým, narovnaným plátnem předáme obrázek engine. Objekt výsledku obsahuje rozpoznaný řetězec, skóre důvěry a dokonce i ohraničující rámečky, pokud je budete později potřebovat.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typický výstup vypadá takto:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Všimněte si, jak řádky jsou perfektně zarovnané? To je výhoda **správné rotace obrázku** – OCR už nemusí hádat orientaci řádků.

## Krok 5: Sestavte vše dohromady – Jednosouborový skript pro převod skenu na text

Níže je kompletní spustitelný skript, který kombinuje všechny části, o kterých jsme mluvili. Uložte jej jako `deskew_ocr.py` a spusťte `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Proč to funguje

* **Deskew jako první** – otáčení obrázku před binarizací zajišťuje, že algoritmus prahování pracuje na rovném horizontu.  
* **Binarizace po deskew** – Otsuova metoda předpokládá bimodální histogram; nakloněná stránka by tento předpoklad zničila.  
* **Anglický jazykový model** – říká OCR, jaké znaky očekávat, čímž snižuje falešně pozitivní výsledky.  

Pokud potřebujete zpracovávat jiné jazyky, stačí vyměnit `ocr.Language.ENGLISH` za odpovídající enum.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když je sken vzhůru nohama?* | `deskew()` filtr obvykle detekuje i rotaci o 180°. Pokud selže, zavolejte `apply_filter(ocr.Filter.rotate(180))` před deskewem. |
| *Můj dokument má barevné grafiky – binarizace je smaže?* | Ano. Pro smíšený obsah zvažte použití pouze `ocr.Filter.deskew()`, pak spusťte OCR na barevném obrázku. Stále můžete extrahovat text a zachovat grafiku. |
| *Mohu zpracovat dávku souborů?* | Zabalte logiku do smyčky, načtěte každou cestu k souboru ze seznamu a uložte každý `result.text` do samostatného `.txt` souboru. |
| *Jak zlepšit přesnost u nízkokvalitních skenů?* | Zvětšete obrázek pomocí bikubického filtru **před** deskewem, pak aplikujte filtr pro zaostření. Více pixelů poskytuje OCR engine lepší vodítka. |

## Bonus: Vizuální ověření deskewu

Pokud chcete vidět před‑a‑po vedle sebe, přidejte rychlý Matplotlib úryvek:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## Závěr

Probrali jsme **jak deskewovat obrázek** soubory, proč je **předzpracování obrázku pro OCR** nezbytné, a jak **extrahovat text z obrázku** a nakonec **převést sken na text**. Pracovní postup—načíst → deskew → binarizovat → rozpoznat—zajišťuje, že OCR vidí čistou, rovnou stránku, což se promítá do vyšší přesnosti a méně ručních oprav.

Co bude dál na vaší OCR cestě? Vyzkoušejte:

* Různé jazykové balíčky (`ocr.Language.FRENCH`, atd.).  
* Přidání kroku analýzy rozvržení pro detekci sloupců nebo tabulek.  
* Export výsledků OCR do prohledávatelných PDF pomocí PDF knihovny.

Neváhejte zanechat komentář, pokud narazíte na problém, nebo sdílet své úpravy pro zpracování obzvláště neústupných skenů. Šťastné programování a ať jsou vaše obrázky vždy dokonale rovné!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak použít AspOCR: Předzpracování OCR filtrů pro obrázek v .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak OCR obrázek – Provést OCR na obrázku v OCR rozpoznávání obrázků](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}