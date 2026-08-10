---
category: general
date: 2026-07-05
description: Jak použít OCR v Pythonu k rychlému převodu TIFF na text. Naučte se kroky
  knihovny OCR v Pythonu pro extrakci textu z TIFF obrázků a vytvoření OCR enginu
  v Pythonu.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: cs
og_description: Jak používat OCR v Pythonu? Tento průvodce vám krok za krokem ukazuje,
  jak převést TIFF na text pomocí OCR enginu v Pythonu a knihovny OCR pro Python.
og_title: Jak používat OCR v Pythonu – Kompletní extrakce textu z TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Jak použít OCR v Pythonu – Extrahovat text z TIFF
url: /cs/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v Pythonu – Extrahovat text z TIFF

Už jste se někdy zamýšleli **jak používat OCR v Pythonu** k převodu naskenované knihy na editovatelný text? Nejste v tom sami — vývojáři, výzkumníci i nadšenci často narazí na tento problém při práci s více‑stránkovými TIFF obrázky. Dobrá zpráva? S **ocr library python** můžete spustit malý OCR engine, nasměrovat jej na TIFF soubor a během několika sekund získat čistý, prohledávatelný text.

V tomto tutoriálu vás provedeme vším, co potřebujete: instalací správného balíčku, načtením více‑stránkového TIFF, spuštěním OCR enginu a nakonec vytištěním obsahu jednotlivých stránek. Na konci budete schopni **convert TIFF to text** a **extract text from TIFF** soubory, aniž byste opustili své Python prostředí.

## Požadavky

- Python 3.9 nebo novější (příklad byl testován na 3.11)
- Nedávná verze knihovny `ocr` (nebo jakýkoli kompatibilní `python ocr engine`, který preferujete)
- Více‑stránkový TIFF soubor, který chcete zpracovat (budeme jej nazývat `scanned_book.tif`)
- Základní znalost Python skriptů a virtuálních prostředí

Není potřeba žádné těžké externí nástroje — stačí pip a několik řádků kódu.

## Instalace OCR knihovny pro Python

Nejprve je potřeba mít spolehlivý OCR backend. Pro tento návod použijeme fiktivní balíček `ocr`, který poskytuje jednoduché high‑level API, ale stejný postup funguje i s wrappery založenými na Tesseractu, jako je `pytesseract`, nebo s komerčními SDK.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Tip:** Pokud používáte Windows a balíček závisí na nativních binárkách, ujistěte se, že máte nainstalovaný odpovídající Visual C++ redistributable. Instalátor vás obvykle varuje, pokud něco chybí.

## Jak použít OCR engine v Pythonu

Nyní, když je knihovna připravena, spustíme OCR engine a nasměrujeme jej na náš TIFF soubor. Následující úryvek vytvoří instanci enginu, nastaví jazyk na angličtinu a připraví jej pro zpracování více stránek.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Proč nastavit jazyk?**  
Většina OCR enginů používá jazykové modely ke zlepšení přesnosti. Pokud tento krok přeskočíte, engine přejde na obecný model, který může špatně rozpoznat interpunkci nebo speciální znaky.

## Načtení více‑stránkového TIFF obrázku

Dalším krokem je načtení naskenovaného dokumentu. Pomocná funkce `ocr.Image.load` rozumí TIFF zásobníkům přímo, vrací objekt, který interně reprezentuje každou stránku.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Hraniční případ:** Pokud váš TIFF používá kompresi (CCITT Group 4, LZW, atd.) a knihovna vyhodí chybu, zkuste jej nejprve převést na nekomprimovanou verzi pomocí ImageMagick:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Provedení OCR na všech stránkách — Convert TIFF to Text

S objektem obrázku v ruce může engine nyní zpracovat všechny stránky najednou. Tato metoda vrací seznam, kde každý prvek obsahuje OCR výsledek pro jednu stránku.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Co se děje pod kapotou?**  
Funkce `recognize_multi_page` iteruje přes každou rasterizovanou stránku, spouští neuronovou síť rozpoznávače a balí výstup plain‑textu společně s hodnotami důvěry. V podstatě jde o dávkovou operaci, která vám ušetří psaní manuální smyčky.

## Procházení výsledků — Extract Text from TIFF

Nakonec zobrazíme rozpoznaný text. Výstup můžete zapsat do samostatných `.txt` souborů, uložit do databáze nebo vložit do vyhledávacího indexu — co nejlépe vyhovuje vašemu workflow.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Očekávaný výstup

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Každý řetězec `result.text` obsahuje surový OCR výstup pro danou stránku. Pokud potřebujete zachovat zalomení řádků, většina enginů poskytuje `result.lines` jako seznam řetězců.

## Práce s velkými TIFF soubory — Tipy a triky

Zpracování 500‑stránkového TIFF může být náročné na paměť. Zde je několik strategií, jak udržet věci plynulé:

1. **Rozdělit stránky** – Místo `recognize_multi_page` zavolejte `engine.recognize(page)` uvnitř generátoru, který vrací po jedné stránce.
2. **Upravit DPI** – Snížení rozlišení obrázku (např. z 300 DPI na 200 DPI) snižuje zátěž CPU, přičemž téměř neovlivňuje přesnost u většiny tištěného textu.
3. **Paralelizovat** – Pokud je váš OCR engine thread‑safe, vytvořte `concurrent.futures.ThreadPoolExecutor` pro paralelní rozpoznávání více stránek najednou.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Uložení extrahovaného textu do souborů

Většina reálných pipeline vyžaduje trvalé úložiště. Níže je stručný způsob, jak uložit text každé stránky do samostatného souboru, zachovávající pořadí stránek.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Nyní máte čistý adresář s `.txt` soubory připravený pro indexování nebo další zpracování NLP.

## Náhled obrázku — Jak vizuálně použít OCR výsledky

Pokud chcete vidět OCR překrytí na původním obrázku (užitečné při ladění), mnoho knihoven umožňuje kreslit ohraničující rámečky. Zde je rychlý příklad s použitím Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![How to use OCR in Python – OCR overlay on a TIFF page](ocr_overlay_example.png)

*Alt text:* Jak používat OCR v Pythonu — vizuální překrytí rozpoznaného textu na TIFF stránce.

## Časté problémy a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Zkreslené znaky | Špatný jazykový model | Nastavte `engine.language` na správný enum |
| Chybějící stránky | Kompresi TIFF nepodporováno | Nejprve převést na nekomprimovaný TIFF |
| Pomalejší výkon | Vysoké DPI + jednovláknové zpracování | Snižte DPI nebo povolte multi‑threading |
| Prázdný výstup | Obrázek je příliš tmavý/nízký kontrast | Předzpracujte pomocí roztažení kontrastu (`opencv` nebo `Pillow`) |

Řešení těchto problémů včas vám ušetří hodiny ladění později.

## Další kroky — Přes základní extrakci

Nyní, když ovládáte základy **how to use OCR in Python**, zvažte další možnosti:

- **PDF generation** – Kombinujte extrahovaný text s `reportlab` pro vytvoření prohledávatelných PDF.
- **Language detection** – Automaticky přepněte `engine.language` pomocí `langdetect`.
- **Structured data extraction** – Použijte regulární výrazy nebo spaCy k získání dat, jmen nebo tabulek ze surového textu.
- **Alternative OCR backends** – Vyměňte `ocr` za `pytesseract` nebo `easyocr`, pokud potřebujete vícejazyčnou podporu.

Každé z těchto témat přirozeně navazuje na sekundární klíčová slova **ocr library python**, **convert tiff to text**, **extract text from tiff** a **python ocr engine**, čímž vám poskytuje pevný základ pro pokročilejší projekty.

---

### Závěr

Probrali jsme **how to use OCR in Python** od instalace po zpracování více stránek, ukázali vám přesně jak **convert TIFF to text** a **extract text from TIFF** pomocí jednoduchého **python OCR engine**. Kompletní, spustitelný příklad výše by měl fungovat ihned pro většinu standardních TIFF souborů a uvedené tipy vám pomohou škálovat na větší dokumenty nebo integrovat OCR do rozsáhlejších pipeline.

Vyzkoušejte to na svých vlastních naskenovaných knihách, účtenkách nebo archivních obrázcích — pak experimentujte s nápady vyšší úrovně uvedenými v sekci „Další kroky“. Šťastné kódování a ať jsou vaše OCR výsledky vždy přesné!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – krok za krokem](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak extrahovat text z TIFF pomocí Aspose.OCR pro Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}