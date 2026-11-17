---
category: general
date: 2026-03-18
description: Proveďte OCR na obrázku a rychle získejte text z obrázku. Naučte se,
  jak načíst obrázek pro OCR, vytvořit OCR engine a zlepšit přesnost OCR pomocí jazykových
  možností.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: cs
og_description: Proveďte OCR na obrázku s tímto podrobným návodem. Naučte se načíst
  obrázek pro OCR, vytvořit OCR engine a zlepšit přesnost OCR pro spolehlivé získávání
  textu.
og_title: Provést OCR na obrázku – Kompletní programovací tutoriál
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Provést OCR na obrázku – krok za krokem průvodce
url: /cs/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Proveďte OCR na obrázku – Kompletní programovací tutoriál

Už jste někdy potřebovali **perform OCR on image**, ale nebyli jste si jisti, kterou knihovnu zvolit nebo jak získat spolehlivé výsledky? Nejste v tom sami. V tomto průvodci projdeme vše, co potřebujete k **extract text from image**, od načtení obrázku až po ladění jazykových možností, abyste mohli **improve OCR accuracy** v každém kroku.

Probereme, jak **load image for OCR**, jak **create OCR engine**, a proč každé nastavení má význam. Na konci budete mít připravený skript, který vytiskne rozpoznaný text, a pochopíte „proč“ za každým řádkem – žádné vágní zkratky typu „viz dokumentace“. Pojďme na to.

## Co budete potřebovat

- Python 3.8+ (kód používá f‑stringy a typové nápovědy)
- Fiktivní balíček `ocr_lib` – nainstalujte pomocí `pip install ocr_lib`
- Soubor obrázku obsahující jasný, tištěný text (např. `lab_report.png`)
- Základní textový editor nebo IDE (VS Code, PyCharm, nebo cokoli, co máte rádi)

Pokud už to máte, skvělé – jste připraveni. Pokud ne, stáhněte Python z python.org a spusťte příkaz pip; zabere to jen minutu.

![příklad provedení OCR na obrázku](/images/ocr-example.png)

*Alt text: perform OCR on image – ukázkový výstup zobrazující extrahovaný text.*

## Krok 1: Vytvořte OCR engine – Jak **create OCR engine** v Pythonu

Než může dojít k jakémukoli rozpoznání, knihovna potřebuje objekt engine, který drží konfiguraci a stav během běhu. Představte si engine jako mozek operace.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Proč je to důležité:** Vytvoření instance engine brzy vám umožní později připojit jazykové možnosti a také kešuje interní modely pro rychlejší následná volání.

## Krok 2: Načtěte obrázek pro OCR – Správný způsob **load image for OCR**

Nyní, když máme engine, musíme mu poskytnout něco ke čtení. Metoda `setImageFromFile` přijímá cestu v souborovém systému; cesta může být absolutní nebo relativní k pracovnímu adresáři skriptu.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Tip:** Použijte absolutní cestu nebo `os.path.join`, abyste se vyhnuli překvapením typu „soubor nenalezen“, když skript běží z jiného adresáře.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Krok 3: Zlepšete přesnost OCR – Ladění **language options** pro **improve OCR accuracy**

Základní OCR funguje, ale doménově specifické slovníky (např. laboratorní žargon) jej často zaskočí. Poskytnutím vlastního slovníku a blacklistu snížíte chybné rozpoznání, jako je zaměnění „0“ a „O“.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Proč to pomáhá:** Slovník říká OCR modelu, že „HPLC“ je platný token, což zabraňuje rozdělení slova na nesmysl. Blacklist říká modelu, aby považoval nejednoznačné symboly za šum, což přímo **improves OCR accuracy**.

## Krok 4: Proveďte OCR na obrázku – Hlavní volání **perform OCR on image**

S připraveným engine a připojeným obrázkem je čas skutečně rozpoznat text. Tento krok vrací objekt `OcrResult`, který můžete dotazovat na surový text, skóre důvěry nebo ohraničující rámečky.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Pokud je obrázek rozmazaný, uvidíte nižší čísla důvěry ve výsledku. To je signál k předzpracování obrázku (např. zvýšení kontrastu) před jeho předáním engine.

## Krok 5: Extrahujte text z obrázku – Získání finálního řetězce

Nakonec požádáme `OcrResult` o jeho textovou reprezentaci. Metoda `getText()` vrací řetězec prostého textu připravený pro další zpracování (uložení do souboru, vložení do databáze atd.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Očekávaný výstup:** Předpokládáme, že `lab_report.png` obsahuje jednoduchou tabulku, můžete vidět něco jako:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Tím je část **extract text from image** hotová.

## Kompletní funkční příklad – Spojte vše dohromady

Níže je jediný skript, který spojí díly z předchozích sekcí. Můžete jej zkopírovat do `run_ocr.py` a spustit `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Rychlý kontrolní seznam

| ✅ | Položka |
|---|------|
| ✔️ | Engine is created (`create OCR engine`) |
| ✔️ | Image is loaded (`load image for OCR`) |
| ✔️ | Language options are set (`improve OCR accuracy`) |
| ✔️ | OCR is performed (`perform OCR on image`) |
| ✔️ | Text is extracted (`extract text from image`) |

Spusťte skript a sledujte konzoli. Pokud uvidíte blok „OCR Output“ s obsahem vašeho reportu, úspěšně jste **performed OCR on image**.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Rozmazaný vstup** | Model OCR nedokáže rozlišovat znaky | Předzpracujte pomocí OpenCV: `cv2.GaussianBlur` nebo zvýšte DPI |
| **Špatný jazyk** | Výchozí jazyk může být nastaven na něco jiného než angličtinu | Zavolejte `engine.setLanguage("eng")` před `recognize()` |
| **Chybějící termíny ve slovníku** | Doménově specifická slova se zkomolí | Přidejte je pomocí `setDictionary` jak je ukázáno v kroku 3 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}