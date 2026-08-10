---
category: general
date: 2026-06-16
description: Extrahujte text z TIFF souborů pomocí Python OCR. Naučte se, jak krok
  za krokem převést TIFF na text a snadno zpracovávat více stránkové dokumenty.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: cs
og_description: Extrahujte text z TIFF souborů pomocí Python OCR. Postupujte podle
  tohoto návodu, jak převést TIFF na text, zpracovat vícestránkové skeny a získat
  čisté výsledky.
og_title: Extrahování textu z TIFF – Kompletní průvodce Pythonem
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Extrahování textu z TIFF – Kompletní průvodce Pythonem
url: /cs/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z TIFF – Kompletní průvodce v Pythonu

Už jste někdy potřebovali **extrahovat text z TIFF** obrázků, ale nevedeli jste, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tento problém při práci s naskenovanými archivy nebo staršími dokumenty. Dobrá zpráva? Několika řádky Pythonu můžete **převést TIFF na text** během okamžiku, i když soubor obsahuje desítky stránek.

V tomto tutoriálu projdeme reálný příklad: načtení více‑stránkového TIFF, nastavení jazyka OCR na francouzštinu a získání rozpoznaného textu z každé stránky. Na konci budete mít připravený skript, pochopíte, proč je každý krok důležitý, a budete vědět, jak jej přizpůsobit pro jiné jazyky nebo formáty obrázků.

## Požadavky

Než se pustíme do práce, ujistěte se, že máte:

- Python 3.8 nebo novější.
- Balíček `ocr` (nebo jakoukoli kompatibilní OCR knihovnu, která poskytuje třídu `OcrEngine`). Nainstalujete jej pomocí `pip install ocr-lib` — nahraďte skutečným názvem balíčku, který používáte.
- Více‑stránkový TIFF soubor (např. `french-scans.tif`), který chcete zpracovat.
- Základní znalosti skriptování v Pythonu.

Žádné těžké závislosti, žádné externí služby — pouze čistý Python a OCR engine.

---

## Krok 1: Nastavení OCR engineu pro **extrahování textu z TIFF**

Nejprve potřebujeme instanci OCR engineu a musíme mu říct, jaký jazyk má použít. V našem případě je zdrojový materiál ve francouzštině, takže nastavíme jazyk odpovídajícím způsobem.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Proč je to důležité:**  
Nastavení jazyka dramaticky zvyšuje přesnost. Francouzské znaky jako „é“ nebo „ç“ by byly při výchozím nastavení na angličtinu přečteny jako obecné symboly. Výslovným výběrem francouzštiny poskytneme engine správnou mapu znaků.

> **Tip:** Pokud zpracováváte dokumenty v několika jazycích, můžete `engine.language` měnit za běhu před každým voláním `recognize()`.

---

## Krok 2: Načtení více‑stránkového TIFF, který chcete **převést TIFF na text**

TIFF může obsahovat několik rámců — každý rámec představuje samostatnou stránku. OCR knihovna to pro nás abstrahuje, takže stačí ukázat na soubor.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Upozornění na okrajové případy:**  
Pokud je cesta k souboru špatná nebo je TIFF poškozený, metoda `load_from_file` vyvolá výjimku. Pro produkční kód ji obalte do `try/except` bloku:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Krok 3: Spuštění OCR na celém dokumentu — Jádro **extrahování textu z TIFF**

Nyní necháme engine udělat svou magii. Volání `recognize()` zpracuje všechny stránky najednou a vrátí bohatý objekt výsledku.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Co se děje pod kapotou?**  
Engine iteruje přes každý rámec, provádí předzpracování (odklon, binarizaci), spouští neuronovou síť a agreguje výstup. Protože jsme volali `recognize()` jen jednou, knihovna může sdílet zdroje mezi stránkami, což je rychlejší než ruční smyčka.

---

## Krok 4: Vytažení rozpoznaného textu z JSON výsledku — **převod TIFF na text** stránka po stránce

Objekt výsledku lze serializovat do JSON. V tomto JSON najdete pole `pages`, kde každá položka obsahuje pole `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Nyní máme čistý Python seznam, kde každý prvek odpovídá OCR výstupu jedné stránky.

---

## Krok 5: Výpis nebo uložení textu pro každou stránku — Poslední krok **extrahování textu z TIFF**

Projdeme stránky a zobrazíme extrahovaný text. Můžete také každou stránku zapsat do samostatného souboru `.txt`, pokud vám to vyhovuje více.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Očekávaný výstup (ukázka)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Pokud OCR uspěje, uvidíte čistý blok francouzských vět pro každou stránku. Pokud narazíte na poškozené znaky, zkontrolujte nastavení jazyka nebo zvažte zvýšení rozlišení obrázku před OCR.

---

## Řešení běžných problémů při **převodu TIFF na text**

| Problém | Proč se vyskytuje | Rychlé řešení |
|---------|-------------------|---------------|
| **Prázdné pole `pages`** | TIFF nebyl načten správně nebo neobsahuje žádné rámy. | Ověřte cestu k souboru a ujistěte se, že TIFF není jednorázový PNG maskovaný jako TIFF. |
| **Špatné znaky** | Nesprávný jazyk nebo nízká kvalita obrazu. | Nastavte správný `engine.language` a předzpracujte obrázek (např. zvýšte DPI). |
| **Přetečení paměti u velkých TIFF** | Načtení všech stránek najednou spotřebuje RAM. | Zpracovávejte po částech: načtěte jeden rámec, rozpoznávejte, pak uvolněte před načtením dalšího. |
| **Unicode chyby při výpisu** | Kódování konzole nepodporuje diakritické znaky. | Použijte `print(page["text"].encode('utf-8').decode('utf-8'))` nebo nastavte terminál na UTF‑8. |

---

## Rozšíření skriptu: Od **extrahování textu z TIFF** k dávkovému zpracování

Nyní, když máte pevný základ, zvažte následující kroky:

1. **Dávková konverze** — zabalte celý tok do funkce `def ocr_tiff(path):` a iterujte přes adresář TIFF souborů.
2. **Výstup do souborů** — namísto výpisu zapisujte text každé stránky do `page_{i}.txt` nebo vše spojte do jednoho dokumentu.
3. **Alternativní OCR engine** — pokud potřebujete vyšší přesnost, vyměňte `ocr.OcrEngine()` za Tesseract (`pytesseract`) nebo Azure Cognitive Services — stačí zachovat stejnou logiku „extrahování textu z TIFF“.
4. **Post‑processing** — spusťte kontrolu pravopisu, detekci jazyka nebo regex čištění, aby byl surový OCR výstup hezčí.

---

## Kompletní, připravený ke spuštění skript

Níže je celý kód, připravený ke zkopírování. Obsahuje základní ošetření chyb a volitelné ukládání textu každé stránky do samostatných souborů.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Spusťte tento skript, nasměrujte `tiff_file` na svůj dokument a sledujte, jak se konzole zaplní čistými francouzskými větami. Pokud zadáte `out_folder`, najdete také sérii souborů `page_#.txt` připravených k dalšímu zpracování.

---

## Závěr

Právě jsme **extrahovali text z TIFF** souborů pomocí jednoduchého Python OCR workflow a nyní víte, jak **převést TIFF na text** spolehlivě. Od inicializace engine s správným jazykem po iteraci přes JSON výstup každé stránky, každý krok byl vysvětlen s „proč“, takže můžete vzor přizpůsobit jiným jazykům, formátům obrázků nebo větším dávkám.

Co dál? Vyzkoušejte výměnu OCR backendu za Tesseract, experimentujte s různými jazykovými balíčky nebo integrujte výstup do prohledávatelné databáze. Možnosti jsou neomezené, když dokážete spolehlivě převést naskenované obrázky na prohledávatelný text.

Neváhejte zanechat komentář, pokud narazíte na problémy nebo máte nápady na další vylepšení. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}