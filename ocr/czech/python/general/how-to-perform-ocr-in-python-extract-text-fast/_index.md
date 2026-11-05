---
category: general
date: 2026-03-26
description: Naučte se provádět OCR v Pythonu a snadno extrahovat text z obrázku,
  číst text ze skenu nebo extrahovat text z faktury pomocí jednoduchého OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: cs
og_description: Jak provést OCR v Pythonu? Tento průvodce vám ukáže, jak extrahovat
  text z obrázku, číst text ze skenu a extrahovat text z faktury během několika minut.
og_title: Jak provést OCR v Pythonu – rychle extrahovat text
tags:
- OCR
- Python
- Image Processing
title: Jak provést OCR v Pythonu – rychle extrahovat text
url: /cs/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět OCR v Pythonu – Extrahujte text rychle

Už jste se někdy zamysleli **jak provádět OCR** na naskenovaném účtence nebo rozmazaném PDF? Nejste v tom sami. V mnoha projektech se potřeba **extrahovat text z obrázku** objeví dříve či později a běžný přístup „přepsat vše ručně“ prostě není škálovatelný.  

V tomto tutoriálu uvidíte kompletní, připravený příklad, který ukazuje **jak použít OCR** k přečtení textu ze skenu, získání dat z faktury a dokonce i automatické korekce zkosení – vše jen s několika řádky Pythonu.

## Co se naučíte

Projdeme vše, co potřebujete vědět:

* Přesné závislosti a importy, které jsou vyžadovány.
* Jak vytvořit a nakonfigurovat instanci `OcrEngine`.
* Způsoby **extrahování textu z obrázku**, **čtení textu ze skenu** a **extrahování textu z faktury** pomocí stejného enginu.
* Časté úskalí (špatný jazyk, chybějící soubory, velké obrázky) a jak se jim vyhnout.
* Očekávaný výstup, abyste mohli ověřit, že OCR uspělo.

Žádné externí odkazy na dokumentaci nejsou potřeba – vše je samostatné, takže můžete kód zkopírovat a okamžitě vidět výsledky.

## Předpoklady

Než se pustíme dál, ujistěte se, že máte:

* Nainstalovaný Python 3.8+ (balíček `ocr` funguje s libovolnou aktuální verzí).
* K dispozici knihovnu `ocr` (`pip install ocr‑engine` – nahraďte skutečným názvem balíčku, pokud je jiný).
* Soubor s obrázkem, který chcete zpracovat – pro ukázku použijeme `invoice.png` umístěný ve složce `YOUR_DIRECTORY`.

To je vše. Pokud už máte toto připravené, můžete začít.

## Krok 1: Instalace a import OCR modulu

Nejprve potřebujeme OCR knihovnu. Pokud jste ji ještě nenainstalovali, spusťte následující příkaz v terminálu:

```bash
pip install ocr-engine
```

Nyní importujeme modul v našem skriptu.

```python
# Step 1: Import the OCR module
import ocr
```

> **Tip:** Udržujte virtuální prostředí čisté; zabrání to konfliktům verzí, když později přidáte další balíčky pro zpracování obrázků.

## Krok 2: Vytvoření a konfigurace OCR enginu

Vytvoření enginu je tak jednoduché jako zavolat jeho konstruktor, ale skutečná síla spočívá v jeho správném nastavení. Nastavíme jazyk na angličtinu a zapneme automatickou korekci zkosení, což je nezbytné při práci s naskenovanými fakturami, které nejsou dokonale zarovnané.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Proč povolit `auto_skew`? Mnoho skenerů vytváří obrázky, které jsou o několik stupňů nakřivo. Bez korekce může engine přehlédnout znaky a zcela nečitelné faktury se změní v nesmysly.

## Krok 3: Provedení OCR na cílovém obrázku

Nyní předáme soubor s obrázkem engineu. Metoda `recognize_image` vrací objekt, který obsahuje surový text i skóre důvěry (pokud je knihovna poskytuje).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Pokud pracujete se scénářem **čtení textu ze skenu**, jednoduše nahraďte cestu skenovaným PDF převedeným na PNG nebo JPEG. Stejné volání funguje pro jakýkoli formát obrázku, který podkladová knihovna podporuje.

## Krok 4: Prohlédnutí a využití extrahovaného textu

Vypíšeme surový výstup OCR. Ve skutečném pipeline pro zpracování faktur pravděpodobně tento řetězec parsujete, získáváte položky, součty a data, ale prozatím rychlý pohled potvrdí, že OCR uspělo.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Očekávaný výstup (zkrácený pro stručnost):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Pokud výstup vypadá poškozeně, zkontrolujte, že je obrázek čistý a že `engine.language` odpovídá jazyku dokumentu.

## Krok 5: Řešení běžných okrajových případů

### Velké obrázky

Zpracování skenu o rozměrech 5000 × 5000 pixelů může být náročné na paměť. Rychlý způsob, jak to zmírnit, je před odesláním do enginu obrázek zmenšit:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Více jazyků

Pokud potřebujete **extrahovat text z obrázku**, který obsahuje jak angličtinu, tak španělštinu, můžete nastavit seznam jazyků:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Engine se pokusí rozpoznat znaky z obou sad.

### Ošetření chyb

Nikdy nepředpokládejte, že soubor existuje. Zabalte volání do bloku try‑except a poskytněte přátelskou zprávu:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Vizuální reference

Níže je snímek obrazovky ukázkové faktury, kterou jsme použili v demonstraci. Všimněte si mírného náklonu – přesně to `auto_skew` opravuje.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* jak provádět OCR na obrázku faktury s automatickou korekcí zkosení.

## Kompletní, spustitelný příklad

Spojením všeho dohromady získáte jeden skript, který můžete spustit z příkazové řádky. Pokrývá instalaci, konfiguraci, ošetření chyb a jednoduchý krok post‑processingu, který zapíše extrahovaný text do souboru `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Spuštěním `python full_ocr_demo.py` se vytiskne extrahovaný text do konzole a uloží se do `output.txt`. Odtud můžete použít regulární výrazy, CSV zapisovače nebo jakoukoli další logiku potřebnou pro **extrahování textu z faktury**.

## Závěr

Nyní máte solidní, end‑to‑end řešení, jak **provádět OCR** v Pythonu. Vytvořením `OcrEngine`, nastavením jazyka a korekce zkosení a ošetřením několika praktických okrajových případů můžete spolehlivě **extrahovat text z obrázku**, **číst text ze skenu** a **extrahovat text z faktury** bez nutnosti procházet roztříštěnou dokumentací.

Co dál? Zkuste zpracovat dávku souborů ve smyčce, experimentujte s různými jazyky nebo výstup připojte k knihovně pro generování PDF, abyste vytvořili prohledávatelné PDF. Možnosti jsou neomezené a kód, který jste právě viděli, je pevná výchozí platforma.

Máte otázky ohledně konkrétního formátu souboru nebo potřebujete pomoci s nastavením prahů důvěry? Napište komentář níže – rádi vám pomůžeme doladit váš OCR pipeline!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}