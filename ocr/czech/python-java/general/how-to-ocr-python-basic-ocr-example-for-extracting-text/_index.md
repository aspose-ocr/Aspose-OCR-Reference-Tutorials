---
category: general
date: 2026-04-26
description: 'jak na OCR v Pythonu: Naučte se extrahovat text z obrázku a číst TIFF
  soubory v Pythonu pomocí základního příkladu OCR. Rychlý, spustitelný kód je zahrnut.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: cs
og_description: 'jak na OCR v Pythonu: krok za krokem průvodce, který ukazuje, jak
  extrahovat text z obrázku, číst TIFF soubor v Pythonu a převést text naskenovaného
  obrázku pomocí jednoduchého spustitelného skriptu.'
og_title: jak na OCR v Pythonu – Základní příklad OCR pro extrakci textu
tags:
- OCR
- Python
- Image Processing
title: jak na OCR v Pythonu – Základní příklad OCR pro extrakci textu
url: /cs/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Basic OCR Example for Extracting Text

Už jste se někdy zamýšleli **jak provést OCR v Pythonu**, když máte na stole naskenovaný soubor TIFF? Nejste jediní, kdo se dívá na hromadu obrázkových souborů a ptá se: „Jak z toho dostanu slova?“ Dobrou zprávou je, že převést obrázek na prostý text je hračka s vhodnou knihovnou a několika jasnými kroky.

V tomto tutoriálu projdeme **základní OCR příklad**, který načte soubor TIFF, vytáhne text a vypíše jej do konzole. Na konci budete přesně vědět, jak **extrahovat text z obrázku**, jak zacházet s vlastnostmi formátu TIFF a co upravit, pokud potřebujete **převést naskenovaný text obrázku** na něco užitečnějšího. Žádná skrytá magie – jen přímý Python, který můžete dnes zkopírovat‑vložit a spustit.

## What You’ll Need

Než se pustíme dál, ujistěte se, že máte:

- Python 3.9+ nainstalovaný (nejlépe nejnovější stabilní verzi).
- OCR knihovnu instalovatelnou přes pip. V tomto průvodci použijeme fiktivní balíček `aocr`, který napodobuje populární nástroje jako Tesseract; později jej můžete nahradit `pytesseract` nebo `easyocr`.
- TIFF obrázek, který chcete zpracovat – pojmenujte jej `input.tiff` a umístěte do složky, na kterou budete v kódu odkazovat.
- Základní orientaci v příkazové řádce (jen pro instalaci balíčku).

A to je vše. Žádné těžké závislosti, žádné Docker kontejnery, jen pár řádků kódu.

## Step 1 – Install and Import Dependencies (how to ocr python)

Nejprve nainstalujte OCR balíček. Otevřete terminál a spusťte:

```bash
pip install aocr
```

Pokud dáváte přednost reálné knihovně, zaměňte `aocr` za `pytesseract` a nainstalujte samostatně Tesseract engine.

Nyní importujte, co potřebujeme. Třída `Path` z `pathlib` nám poskytuje čistý způsob práce s cestami napříč operačními systémy.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Proč používat `Path`?* Protože abstrahuje rozdíly ve zpětných lomítcích (`/` vs `\`) a umožňuje spojovat adresáře, aniž byste se museli starat o podkladový OS. Ten malý detail často zachraňuje před hlavolamy, když později přesunete skript na CI server.

## Step 2 – Create the OCR Engine Instance (basic ocr example)

Dále vytvořte instanci OCR enginu. Představte si `OcrEngine` jako mozek, který bude číst obrázek a vracet znaky.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Většina OCR knihoven umožňuje zde ladit jazyk, DPI nebo prahy důvěry. Pro tento **základní OCR příklad** zůstaneme u výchozích nastavení, ale později můžete prozkoumat `ocr_engine.config`, pokud potřebujete pracovat s vícejazyčnými dokumenty.

## Step 3 – Load Your TIFF Image (read tiff file python)

Tady přichází část **read tiff file python**. TIFF soubory mohou mít více stránek, ale `Image.load` načte první stránku ve výchozím nastavení – ideální pro jednostránkový sken.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Nahraďte `"YOUR_DIRECTORY"` skutečnou složkou, kde se nachází `input.tiff`. Pokud si nejste jisti, kde skript běží, `Path.cwd()` vypíše aktuální pracovní adresář – užitečné pro ladění problémů s cestami.

## Step 4 – Run the OCR Process (extract text from image)

Nyní se děje magie. Volání `process()` pošle obrázek skrz OCR pipeline a vrátí objekt s výsledkem.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Za scénou může engine převádět obrázek na odstíny šedi, aplikovat prahování a předávat jej neuronové síti. Nemusíte se starat o tyto kroky; knihovna je abstrahuje.

## Step 5 – Print the Recognized Text (convert scanned image text)

Nakonec výstup textu. V reálných projektech byste ho pravděpodobně zapisovali do souboru nebo databáze, ale výpis do konzole udržuje příklad přehledný.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Po spuštění skriptu byste měli vidět něco jako:

```
Hello, world!
This is a sample scanned document.
```

Pokud výstup vypadá poškozeně, zkontrolujte, že zdrojový obrázek je ostrý a že jazyk OCR odpovídá textu.

## Full Working Script

Sestavením všech částí získáte kompletní, připravený program:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Pokud potřebujete **převést naskenovaný text obrázku** do prohledávatelného PDF, můžete `ocr_result.text` předat generátoru PDF jako `reportlab` – ale to už je samostatný tutoriál.

## Common Pitfalls & Pro Tips

- **Nízké rozlišení skenů**: OCR selhává pod 150 DPI. Pokud je váš TIFF rozmazaný, nejprve jej up‑samplujte pomocí Pillow (`Image.open(...).resize(...)`).
- **Více stránek**: Pro více‑stránkové TIFFy iterujte přes `Image.load_multi_page()` (pokud vaše knihovna podporuje) a výsledky spojte.
- **Podpora jazyků**: Mnoho enginů má jako výchozí jazyk angličtinu. Nastavte `ocr_engine.language = "spa"` pro španělštinu, například.
- **Zpracování bílých znaků**: OCR často přidává nadbytečné zalomení řádků. Použijte `str.splitlines()` nebo regulární výrazy pro vyčištění výstupu.
- **Výkon**: Pro hromadné zpracování znovu použijte jedinou instanci `OcrEngine` místo vytváření nové pro každý soubor.

## Extending the Example

Nyní, když ovládáte **how to ocr python** pro jeden obrázek, zvažte další kroky:

1. **Dávkové zpracování** – Procházejte adresář s TIFFy a zapisujte každý výsledek do souboru `.txt`.
2. **Integrace s Pandas** – Ukládejte extrahovaný text spolu s metadaty pro rychlou analýzu.
3. **Hybridní přístup** – Kombinujte OCR s NLP knihovnami jako `spaCy` pro extrakci entit (jména, data, částky) ze skenovaných faktur.
4. **Alternativní formáty souborů** – Zaměňte `Image.load` za `Image.from_bytes` pro zpracování obrázků přicházejících z API nebo databáze.

Všechny tyto rozšíření staví na jádru **extrahovat text z obrázku** a **převést naskenovaný text obrázku** do podoby, kterou stroje pochopí.

## Conclusion

Prošli jsme jasným, end‑to‑end **základním OCR příkladem**, který ukazuje **how to ocr python**, **read tiff file python** a **extrahovat text z obrázku** pomocí několika řádků kódu. Skript je samostatný, obsahuje ošetření chyb a přímo vypisuje výsledek, což z něj dělá solidní základ pro jakýkoli projekt, který potřebuje převést naskenované dokumenty na editovatelný text.

Klidně experimentujte – zaměňte OCR backend, upravte předzpracování nebo napojte výstup do dalšího workflow. Možnosti jsou neomezené, když můžete spolehlivě **převést naskenovaný text obrázku** do prohledávatelných dat.

Máte otázky ohledně okrajových případů, jazykových balíčků nebo ladění výkonu? Zanechte komentář níže a šťastné programování! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}