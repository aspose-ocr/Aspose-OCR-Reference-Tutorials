---
category: general
date: 2026-06-06
description: OCR PNG obrázek s Pythonem – naučte se, jak extrahovat text z obrázku,
  spustit příklad OCR v Pythonu a dokonce snadno číst starořecký text.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: cs
og_description: OCR PNG obrázek v Pythonu vysvětlen. Tento průvodce ukazuje, jak extrahovat
  text z obrázku, spustit příklad OCR v Pythonu a snadno číst starou řečtinu.
og_title: OCR PNG obrázek v Pythonu – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG obrázku v Pythonu – Kompletní krok‑za‑krokem průvodce
url: /cs/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG obrázek v Pythonu – Kompletní krok‑za‑krokem průvodce

Už jste se někdy ptali, jak **OCR PNG image** soubory přímo ze skriptu v Pythonu? Možná máte složku plnou naskenovaných starověkých rukopisů a potřebujete **extract text from image** soubory, aniž byste je museli ručně přepisovat. Dobrou zprávou je, že nepotřebujete PhD v počítačovém vidění – stačí pár řádků kódu a správná knihovna a během několika sekund budete číst starověkou řečtinu.

V tomto tutoriálu projdeme **python OCR example**, který rozpozná text z PNG, nastaví jazyk na řečtinu polytonickou a vytiskne výsledek. Na konci přesně budete vědět, jak **recognize image text**, jak řešit běžné problémy a jak přizpůsobit skript pro jiné jazyky nebo formáty obrázků.

## Co se naučíte

- Nainstalovat a nakonfigurovat Python OCR knihovnu (pytesseract + Tesseract OCR)
- Vytvořit instanci OCR enginu a načíst PNG soubor
- Nastavit rozpoznávací jazyk na řečtinu polytonickou, abyste mohli **read ancient greek**
- Vypsat rozpoznaný text a řešit typické problémy
- Rozšířit skript pro dávkové zpracování více PNG souborů nebo přepnout na jiný jazyk

### Předpoklady

| Požadavek | Proč je důležité |
|-------------|----------------|
| Python 3.8+ | Moderní syntaxe a typové nápovědy |
| `pytesseract` package | Lehký obal kolem Tesseract enginu |
| Tesseract OCR binaries (≥ 5.0) | Skutečný engine, který dělá těžkou práci |
| Greek language data (`grc.traineddata`) | Potřebné pro správné **read ancient greek** |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Naše cílová **ocr png image** ukázka |

Můžete nainstalovat Python část pomocí:

```bash
pip install pytesseract Pillow
```

A na Ubuntu/macOS přidáte samotný engine:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Nezapomeňte stáhnout trénovaná data pro řečtinu polytonickou:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Cesta se může lišit; v případě potřeby upravte `TESSDATA_PREFIX`.)*

---

## OCR PNG obrázek: Vytvoření instance enginu

První věc, kterou potřebujeme, je objekt, který komunikuje s Tesseract. V `pytesseract` je engine přístupný přes funkce na úrovni modulu, ale pro přehlednost jej zabalíme do malé třídy. To odráží koncept „engine“, který jste viděli v původním úryvku.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Proč to zabalit?**  
- Udržuje veřejné API identické s úryvkem, se kterým jste začali, což usnadňuje migraci.  
- Umožňuje později přidat logování nebo ošetření chyb, aniž byste zasahovali do hlavního toku.  
- Demonstruje dobré OOP praktiky – něco, co oceňují zkušení vývojáři.

## Extrahování textu z obrázku: Nastavení jazyka na řečtinu polytonickou

Nyní, když máme engine, musíme mu říct, jaký jazyk očekávat. Řečtina polytonická používá diakritiku, která není zahrnuta ve standardních “greek” datech, takže nasměrujeme Tesseract na tréninkový soubor `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Pokud budete chtít **extract text from image** soubory v jiném jazyce, stačí nahradit `"grc"` za `"eng"` pro angličtinu, `"fra"` pro francouzštinu atd. Stejný řádek funguje pro jakýkoli nainstalovaný jazyk.

## Rozpoznání textu z obrázku: Spuštění OCR na PNG

Po nastavení jazyka předáme PNG engine. Původní příklad použil pevně zadanou cestu; uděláme to trochu flexibilnější pomocí objektů `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tipy a okrajové případy**

- **File not found** – obalte volání do `try/except FileNotFoundError`, aby se zobrazila přátelská zpráva.
- **Low‑resolution PNG** – zvažte předzpracování (např. změna velikosti, binarizace) pomocí Pillow před OCR.
- **Non‑Greek text** – Tesseract se stále pokusí dekódovat, ale přesnost výrazně klesá. Vždy odpovídejte jazyku.

## Výstup rozpoznaného textu

Nakonec vytiskneme výsledek. Ve skutečném projektu můžete zapisovat do databáze, CSV nebo ho dokonce předat do překladového pipeline.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Když spustíte skript na čistém skenu starověké řecké nápisu, měli byste vidět něco jako:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Pokud výstup vypadá poškozeně, zkontrolujte, že soubor **greek.traineddata** je ve správné složce a že PNG není příliš šumivý.

## Kompletní funkční příklad (všechny kroky v jednom skriptu)

Níže je kompletní, připravený ke spuštění program. Uložte jej jako `ocr_greek.py` a spusťte `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Pokud vidíte správné řecké znaky, gratulujeme—úspěšně jste provedli operaci **ocr png image** v Pythonu!

## Časté otázky a profesionální tipy

### Jak zlepšit přesnost u šumivého PNG?

- Převést obrázek na odstíny šedi: `img = img.convert('L')`
- Použít binární práh: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Zvětšit rozlišení pomocí `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Tyto kroky často promění **recognize image text** noční můru na čistý výsledek.

### Můžu zpracovat celou složku PNG souborů?

Ano. Zabalte volání `recognize_image` do `for` smyčky přes `Path.glob("*.png")`. Uložte každý výsledek do slovníku nebo jej zapište do CSV pro pozdější analýzu.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Co když potřebuji extrahovat jen čísla?

Předávejte vlastní řetězec **config** funkci `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Tímto způsobem můžete **extract text from image** soubory, které obsahují tabulky, sériová čísla nebo časová razítka.

### Existuje způsob, jak získat skóre důvěry?

Ano—použijte `pytesseract.image_to_data`, který vrací TSV s důvěrou pro každé slovo. Můžete odfiltrovat tokeny s nízkou důvěrou před sestavením finálního řetězce.

## Rozšíření tutoriálu

Nyní, když ovládáte základy, zvažte prozkoumání těchto souvisejících témat:

- **Batch OCR with multiprocessing** – urychlete zpracování velkých korpusů PNG souborů.
- **Hybrid OCR + NLP pipelines** – automaticky přeložte extrahovanou starověkou řečtinu do moderní angličtiny.
- **Alternative engines** – vyzkoušejte `easyocr` nebo metody založené na `opencv` pro specifické případy.
- **Cloud OCR services** – Google Vision, Azure Computer Vision nebo AWS Textract pro serverless škálování.

Každý z nich staví na základním **python ocr example**, který jsme právě prošli, takže se budete cítit jistě při dalším prozkoumávání.

## Závěr

Vezmeme jednoduchý úryvek a proměnili jsme jej v robustní **ocr png image** workflow v Pythonu. Vytvořením `OcrEngine`, nastavením jazyka na řečtinu polytonickou, předáním PNG a vytištěním výsledku nyní víte, jak **extract text from image** soubory, **recognize image text**, a dokonce **read ancient greek**.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – krok‑za‑krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak nastavit hodnotu prahu v OCR rozpoznávání obrázků](/ocr/english/net/ocr-settings/set-threshold-value/)
- [rozpoznat textový obrázek pomocí Aspose OCR pro více jazyků](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}