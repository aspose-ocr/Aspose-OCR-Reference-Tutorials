---
category: general
date: 2026-09-19
description: Python OCR tutoriál ukazuje, jak převést PNG na text pomocí Aspose OCR.
  Naučte se extrahovat text pomocí OCR v Pythonu a získávejte text ze skenovaných
  obrázků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: cs
lastmod: 2026-09-19
og_description: Python OCR tutoriál vás provede převodem PNG na text pomocí Aspose
  OCR. Ovládněte extrakci textu OCR v Pythonu a získávejte text ze skenovaných obrázků.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Python OCR tutoriál – převod PNG na text pomocí Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Python OCR tutoriál: převod PNG na text pomocí Aspose'
url: /cs/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutoriál: převod PNG na text pomocí Aspose

Pokud potřebujete **python OCR tutorial**, který převádí PNG obrázek na editovatelný text, tento průvodce vám poskytne kompletní, připravené‑k‑spuštění řešení. Uvidíte, jak nainstalovat knihovnu Aspose OCR, načíst obrázek, spustit rozpoznávací engine a vytisknout výsledky — v několika stručných krocích.

Skenování dokumentu a získání textu může být obtížné, zejména když se potýkáte s různými formáty obrázků a nastavením jazyků. Tento tutoriál odstraňuje hádání tím, že vám ukáže přesně, které metody zavolat a proč jsou důležité, takže se můžete soustředit na integraci OCR do vlastních aplikací.

Také se naučíte, jak **převést PNG na text**, zvládat běžné úskalí a přizpůsobit kód pro jiné typy obrázků, jako jsou JPEG nebo TIFF. Na konci budete schopni s jistotou extrahovat text z jakéhokoli naskenovaného obrázku.

## Požadavky

* Nainstalovaný Python 3.8 nebo novější.
* Internetové připojení pro stažení balíčku Aspose OCR.
* PNG obrázek (nebo jakýkoli podporovaný formát) obsahující čitelný text.

Nemusíte mít samostatný OCR engine ani externí binární soubory — Aspose OCR obsahuje vše, co potřebujete.

## Krok 1: Instalace balíčku Aspose OCR

Prvním krokem je přidání knihovny do vašeho prostředí. Aspose poskytuje čistě‑Python balíček, který lze nainstalovat pomocí pip.

```bash
pip install aspose-ocr
```

> **Tip:** Použijte virtuální prostředí (`python -m venv venv`), aby byly závislosti izolovány od ostatních projektů.

Instalace balíčku zpřístupní modul `aspose.ocr`, který obsahuje třídu `OcrEngine` používanou v celém tomto tutoriálu.

## Krok 2: Import třídy OCR engine

Nyní, když je balíček k dispozici, importujte třídu, která řídí proces rozpoznávání.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` zapouzdřuje veškerou logiku pro načítání obrázků, nastavení jazyka a extrakci textu. Importování na začátku odpovídá standardní praxi v Pythonu a udržuje skript přehledný.

## Krok 3: Vytvoření instance OCR engine

Vytvoření instance vám poskytne čistý engine s výchozím nastavením. Později můžete přizpůsobit vlastnosti, jako je jazyk nebo předzpracování obrázku.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Nový objekt `engine` představuje jednu OCR relaci. Opětovné použití stejné instance pro více obrázků může zlepšit výkon, protože interní zdroje jsou kešovány.

## Krok 4: Načtení obrázku, který chcete zpracovat

Zadejte cestu k PNG souboru, který chcete převést. Metoda `load_image` přijímá jakýkoli formát, který Aspose OCR podporuje, takže můžete také předat soubory JPEG, BMP nebo TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Pokud soubor nelze najít, `load_image` vyvolá `FileNotFoundError`. Pro produkční kód obalte volání do try/except bloku, aby se zobrazila přátelská chybová zpráva.

## Krok 5: Provedení OCR pro extrakci textu z obrázku

Volání `recognize` spustí rozpoznávací pipeline a vrátí extrahovaný řetězec. Metoda automaticky provádí analýzu rozvržení, segmentaci znaků a detekci jazyka (výchozí je angličtina).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Můžete změnit jazyk před voláním `recognize`:

```python
engine.language = "fr"   # for French text
```

Tato flexibilita je užitečná, když potřebujete **OCR text extraction python** pro vícejazyčné dokumenty.

## Krok 6: Výstup rozpoznaného textu

Nakonec výsledek vytiskněte nebo uložte. Pro rychlou kontrolu `print` zobrazí surový řetězec v konzoli.

```python
# Step 6: Output the recognized text
print(text)
```

### Očekávaný výstup

Pokud `sample.png` obsahuje větu „Hello, world!“, konzole zobrazí:

```
Hello, world!
```

Výstup může obsahovat zalomení řádků nebo nadbytečné mezery v závislosti na původním rozvržení. Můžete řetězec následně zpracovat pomocí `str.strip()` nebo regulárních výrazů, abyste jej vyčistili.

## Řešení běžných okrajových případů

### 1. Formáty jiné než PNG

I když se tento tutoriál zaměřuje na **convert PNG to text**, můžete obdržet soubory JPEG nebo TIFF. Stejný kód funguje; stačí změnit příponu souboru v `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Obrázky s nízkým rozlišením

Přesnost OCR klesá pod 150 dpi. Pokud narazíte na špatné výsledky, nejprve zvětšete obrázek pomocí Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extrakce textu ze skenovaného obrázku s více jazyky

Nastavte čárkou oddělený seznam jazykových kódů:

```python
engine.language = "en,es,de"
```

Aspose OCR se pokusí rozpoznat znaky ze všech uvedených jazyků.

### 4. Velké dokumenty

Zpracování mnoha stránek v jednom běhu může vyčerpat paměť. Zpracovávejte každou stránku samostatně:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Kompletní, spustitelný skript

Spojením všech kroků dohromady získáte samostatný program, který můžete zkopírovat, vložit a spustit.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Spusťte skript pomocí:

```bash
python python_ocr_tutorial.py
```

Měli byste vidět extrahovaný text vytištěný v konzoli.

## Závěr

Tento **python OCR tutorial** ukázal, jak **convert PNG to text** pomocí Aspose OCR, zahrnující instalaci, načítání obrázku, rozpoznávání a zpracování výstupu. Nyní máte spolehlivý vzor pro **OCR text extraction python** a můžete kód přizpůsobit pro **extract text image python** z libovolného skenovaného dokumentu.

Dále zvažte:

* Integraci skriptu do webové služby (např. Flask) pro poskytování OCR jako API.
* Ukládání extrahovaného textu do databáze pro prohledávatelné archivy.
* Experimentování s různými jazykovými nastaveními pro zpracování vícejazyčných skenů.

Šťastné programování a užívejte si převod obrázků na prohledávatelný, editovatelný text!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Extract Table Text from Images](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}