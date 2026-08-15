---
category: general
date: 2026-03-26
description: Naučte se, jak provádět OCR v Pythonu a rozpoznávat text z obrazových
  souborů. Tento průvodce ukazuje, jak rychle extrahovat text z PNG a převést obrázek
  na text.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: cs
og_description: Jak provést OCR v Pythonu? Postupujte podle tohoto návodu, abyste
  rozpoznali text z obrázku, extrahovali text z PNG a převáděli obrázek na text se
  zkušební licencí.
og_title: Jak provést OCR v Pythonu – kompletní tutoriál
tags:
- OCR
- Python
- Image Processing
title: Jak provést OCR v Pythonu – Kompletní krok za krokem tutoriál
url: /cs/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR v Pythonu – Kompletní krok‑za‑krokem tutoriál  

Už jste se někdy zamysleli **jak provést OCR** na obrázku, který jste právě pořízili telefonem? Nejste sami — vývojáři po celém světě potřebují spolehlivý způsob, jak rozpoznat text z obrazových souborů, aniž by se museli potýkat se složitými nativními knihovnami.  

V tomto tutoriálu projdeme praktickým příkladem, který ukazuje **jak provést OCR**, **rozpoznat text z obrázku** a **extrahovat text z PNG** pomocí lehké Pythonové obálky. Na konci budete schopni **převést obrázek na text** během několika řádků kódu a nebudete se muset starat o problémy s licencí, protože použijeme vestavěný zkušební režim.

## Co se naučíte  

* Jak nastavit zkušební licenci pro OCR engine (není potřeba cesta k souboru).  
* Přesné pořadí volání pro **rozpoznání textu z obrázku** objektů.  
* Způsoby, jak **extrahovat text z PNG** souborů a řešit běžné problémy, jako chybějící fonty.  
* Tipy, jak škálovat řešení při přechodu ze zkušební licence na produkční.  

**Požadavky** – potřebujete Python 3.8+ a balíček `ocr` (instalovatelný pomocí `pip install ocr`). Žádné další externí nástroje nejsou vyžadovány.

---  

![příklad provedení OCR](https://example.com/ocr-demo.png "jak provést OCR v Pythonu – zobrazený rozpoznaný text")  

*Alternativní text obrázku: jak provést OCR v Pythonu – ukázkový výstup*  

## Krok 1 – Aktivace zkušební licence (není potřeba cesta k souboru)  

Než engine dokáže něco přečíst, potřebuje platnou licenci. Zkušební režim je ideální pro experimenty a malé projekty.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Proč je to důležité:* Objekt licence informuje OCR knihovnu, že pracujete v sandboxu. Pokud tento krok přeskočíte, engine vyvolá `LicenseError` ve chvíli, kdy zavoláte `recognize()`.  

**Tip:** Když přejdete na placenou licenci, nahraďte výše uvedené dva řádky `ocr.License("path/to/your/license.key").apply()`.

## Krok 2 – Vytvoření instance OCR engine  

Nyní, když je zkušební licence aktivní, vytvoříme hlavní engine. Představte si ho jako „mozek“, který se podívá na obrázek a rozhodne, kde se nacházejí jednotlivé znaky.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Proč je to důležité:* `OcrEngine` obsahuje konfiguraci, jako jsou jazykové balíčky a nastavení DPI. Ty můžete později upravit, ale výchozí nastavení funguje pro většinu PNG souborů pouze v angličtině.

## Krok 3 – Načtení PNG, který chcete zpracovat  

Zde **rozpoznáváme text z obrázku**. Metoda `ocr.Imaging.Image.load()` podporuje PNG, JPEG, BMP a několik dalších formátů.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Hraniční případ:* Pokud vaše PNG používá indexovanou paletu (běžné u screenshotů), načítač ji automaticky převede na 24‑bitový RGB buffer. Tato konverze může mírně zpomalit výkon, ale zaručuje přesné výsledky OCR.

## Krok 4 – Spuštění OCR a získání textu  

Nakonec požádáme engine, aby udělal svou práci, a poté získáme výsledek jako prostý text.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Očekávaný výstup** (příklad pro jednoduchý obrázek obsahující „Hello World“):

```
Hello World
```

Pokud obrázek obsahuje více řádků, výstup zachová zalomení řádků, což usnadňuje předání následným procesům, jako jsou CSV parsery nebo NLP pipeline.

## Volitelné: Doladění pro vyšší přesnost  

* **Jazykové balíčky:** `ocr_engine.set_language("eng")` (výchozí) nebo `"fra"` pro francouzštinu.  
* **Škálování DPI:** `ocr_engine.set_dpi(300)` může zlepšit výsledky u nízkokvalitních skenů.  
* **Předzpracování:** Aplikace binárního prahu (`ocr.Imaging.Image.threshold()`) před `set_image` často poskytne čistší text na špinavých pozadích.

Tyto úpravy jsou užitečné, když přecházíte z rychlé ukázky na produkční úroveň **ocr tutorial python**, která zpracovává stovky souborů denně.

## Kompletní skript – připravený ke kopírování a vložení  

Níže je kompletní spustitelný skript, který kombinuje všechny výše uvedené kroky. Uložte jej jako `run_ocr.py` a nahraďte `YOUR_DIRECTORY/sample1.png` cestou k vašemu vlastnímu PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Spusťte jej z příkazové řádky:

```bash
python run_ocr.py
```

Měli byste vidět extrahovaný text vytištěný v konzoli. Pokud získáte prázdný řetězec, zkontrolujte, že obrázek skutečně obsahuje jasný, vysokokontrastní text a že zkušební licence byla aplikována bez chyb.

## Časté otázky a úskalí  

* **„Funguje to s JPEG?“** – Ano. Metoda `load()` automaticky detekuje formát, takže můžete vyměnit PNG za JPEG bez změny kódu.  
* **„Co když je obrázek otočen?“** – Engine může automaticky detekovat orientaci, ale pro nejlepší výsledky můžete před `set_image` předem otočit pomocí `input_image.rotate(90)`.  
* **„Mohu zpracovávat více obrázků ve smyčce?“** – Ano. Stačí přesunout načítání a volání `recognize()` dovnitř `for` smyčky; stejná instance `ocr_engine` může být znovu použita, což šetří malé množství režie.  

## Další kroky – od ukázky k produkci  

Nyní, když víte **jak provést OCR**, zvažte následující témata:

* **Dávkové zpracování** – Kombinujte tento skript s `os.listdir()`, abyste **extrahovali text z PNG** souborů hromadně.  
* **Integrace s PDF** – Použijte `pdf2image` k převodu stránek PDF na PNG a poté je vložte do stejného pipeline.  
* **Post‑zpracování** – Použijte regex nebo fuzzy matching k vyčištění běžných chyb OCR (např. „0“ vs „O“).  

Každý z těchto kroků staví na základní myšlence **převést obrázek na text** a rozšiřuje užitečnost vašeho OCR workflow.

---  

### TL;DR  

Probrali jsme vše, co potřebujete vědět k **jak provést OCR** v Pythonu: aktivovat zkušební licenci, vytvořit engine, načíst PNG, spustit rozpoznání a vytisknout výsledek. Pouze s několika řádky kódu můžete **rozpoznat text z obrázku**, **extrahovat text z PNG** a **převést obrázek na text** pro jakoukoli následnou aplikaci.  

Vyzkoušejte to, upravte nastavení DPI nebo jazyka a nechte engine udělat těžkou práci. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}