---
category: general
date: 2026-03-26
description: Naučte se, jak otočit obrázek a provést OCR v Pythonu. Tento průvodce
  také ukazuje, jak předzpracovat obrázek pro OCR a efektivně z něj extrahovat text.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: cs
og_description: Jak správně otočit obrázek a poté rozpoznat text z obrázku pomocí
  Aspose OCR. Postupujte podle tohoto krok‑za‑krokem tutoriálu, abyste předzpracovali
  obrázek pro OCR a extrahovali text z obrázku.
og_title: Jak otočit obrázek a provést OCR – Kompletní průvodce Pythonem
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Jak otočit obrázek a provést OCR pomocí Aspose v Pythonu
url: /cs/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak otočit obrázek a provést OCR pomocí Aspose v Pythonu

Už jste se někdy zamýšleli **jak otočit obrázek**, aby OCR engine skutečně dokázal přečíst text? Možná jste naskenovali formulář, který skončil na boku, nebo zachycení fotoaparátem se otočilo o 90° po směru hodinových ručiček. V takovém případě text vypadá pro lidské oko v pořádku, ale OCR engine vidí jen nepořádek. Dobrá zpráva? Opravit orientaci, oříznout požadovanou oblast a poté extrahovat text je hračka – stačí jen pár řádků Pythonu a knihovny Aspose.

V tomto tutoriálu projdeme celým pracovním postupem: od načtení otočeného TIFFu, opravy jeho orientace, **předzpracování obrázku pro OCR**, až po **rozpoznání textu z obrázku**. Na konci budete vědět **jak provést OCR** na libovolném obrázku a budete schopni **extrahovat text z obrázku** s jistotou.

## Co budete potřebovat

- Python 3.8+ (kód funguje s jakoukoliv novější verzí)
- Balíčky `asposeocrjava` a `asposeimaging` nainstalované pomocí `pip`
- Ukázkový obrázek, který potřebuje otočení (např. `rotated_form.tif`)
- Trochu zvědavosti ohledně zpracování obrazu

Žádné těžkopádné frameworky nejsou potřeba – stačí jen dva balíčky Aspose a trochu Python logiky.

---

## Krok 1: Instalace balíčků Aspose (Jak provést OCR)

Než budeme moci **otočit obrázek** nebo **rozpoznat text z obrázku**, potřebujeme knihovny, které skutečně odlehčují těžkou práci.

```bash
pip install asposeocrjava asposeimaging
```

> **Tip:** Pokud jste za firemním proxy, přidejte `--proxy http://proxy:port` k příkazu. Balíčky jsou čisté Python obaly kolem jádra Aspose .NET/Java, takže instalace je obvykle okamžitá.

---

## Krok 2: Načtení zdrojového souboru a jeho otočení – Jádro kroku „Jak otočit obrázek“

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Proč otáčet?** Většina OCR engine předpokládá, že text běží zleva doprava a shora dolů. Pokud je bitmapa otočena na bok, engine buď vrátí nesmysly, nebo nic. Otočení zarovná mřížku pixelů s očekávaným pořadím čtení, což dramaticky zvyšuje přesnost.
> 
> **Hraniční případ:** Pokud si nejste jisti, zda obrázek potřebuje otočení o 90°, 180° nebo 270°, můžete zkontrolovat `source_image.width` vs `source_image.height` nebo použít `exif` orientační tagy. Metoda Aspose `rotate_flip` také podporuje `ROTATE_180` a `ROTATE_270_CLOCKWISE`.
> 
> **Náhled obrázku (volitelné):**  
> ![how to rotate image example](/assets/rotate-demo.png "How to rotate image – before and after rotation")

---

## Krok 3: Oříznutí oblasti zájmu – Předzpracování obrázku pro OCR

Často potřebujete jen malou část stránky – například pole pro podpis nebo blok čísel. Oříznutí odstraní šum a urychlí **jak provést OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Proč oříznout?** Zmenšení velikosti obrázku omezuje vyhledávací prostor OCR engine, což snižuje falešná pozitiva a zkracuje dobu zpracování. Pomáhá také, pokud zdrojový soubor obsahuje vodoznaky nebo jiné grafiky, které by mohly engine zmást.
> 
> **Tip:** Pokud pracujete s více poli, opakujte krok oříznutí s různými obdélníky a spusťte OCR na každém úseku zvlášť.

---

## Krok 4: Inicializace OCR engine – Jádro „Jak provést OCR“

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Za scénou:** Aspose OCR používá kombinaci Tesseract a proprietární analýzy obrazu. Vytvoření instance engine jednou a její opakované používání pro více obrázků je efektivnější než vytváření nového objektu pokaždé.

---

## Krok 5: Předání oříznutého obrázku a rozpoznání textu – Jak extrahovat text z obrázku

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Očekávaný výstup

Pokud ROI obsahuje frázi „Invoice #12345 – Paid“, uvidíte něco jako:

```
Invoice #12345 – Paid
```

Pokud OCR selže, můžete získat nadbytečné mezery nebo špatně rozpoznané znaky (např. „Invo1ce #I2345 – Pa1d“). Zde přicházejí na řadu **předzpracování obrázku pro OCR** triky – jako úprava kontrastu nebo aplikace binarizace. Aspose nabízí další filtry, které můžete řetězit před krokem 5, ale základní tok výše funguje pro většinu čistých skenů.

---

## Krok 6: Volitelné – Doladění nastavení OCR (Pokročilé „Jak provést OCR“)

Pokud potřebujete vyšší přesnost pro konkrétní jazyk nebo chcete ignorovat určité znaky, můžete engine vyladit:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Kdy použít:** Použijte, když dokument obsahuje spoustu dekorativních symbolů, které vás nezajímají. Blacklistování snižuje počet falešných detekcí.

---

## Kompletní skript od začátku do konce

Spojením všeho dohromady získáte připravený skript, který **jak otočit obrázek**, **předzpracovat obrázek pro OCR** a nakonec **rozpoznat text z obrázku**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Spuštěním tohoto skriptu se rozpoznaný text vypíše do konzole a uloží vizuální podoba zpracovaného ROI jako `processed_roi.png`. Tento PNG můžete otevřít a ověřit, že otočení a oříznutí proběhlo podle očekávání.

---

## Časté otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Co když je obrázek už ve správné orientaci?** | Krok otáčení je idempotentní – otočení správně orientovaného obrázku o 90° jej samozřejmě rozbije, takže byste měli zkontrolovat `source_image.width` vs `height` nebo použít EXIF orientační data před voláním `rotate_flip`. |
| **Můj OCR výstup obsahuje nadbytečné zalomení řádků.** | Použijte `result.get_text().replace("\n", " ").strip()` k vyčištění, nebo povolte `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Mohu zpracovávat PDF přímo?** | Ano – Aspose Imaging může načíst PDF stránky jako obrázky (`Image.load("file.pdf")`), poté postupujete stejným způsobem s otáčením a OCR. |
| **Existuje způsob, jak hromadně zpracovat mnoho souborů?** | Zabalte `ocr_rotated_image` do smyčky přes adresář, nebo použijte `concurrent.futures` v Pythonu pro paralelizaci. |
| **Jak zacházet s jazyky jinými než angličtinou?** | Nastavte rozpoznávací jazyk pomocí `ocr_engine.get_recognition_settings().set_recognition_language("fr")` pro francouzštinu atd. |

---

## Závěr

Probrali jsme **jak otočit obrázek** správně, **předzpracovat obrázek pro OCR** oříznutím a nakonec **jak provést OCR** k **rozpoznání textu z obrázku** a **extrahování textu z obrázku** pomocí Python knihoven Aspose. Kompletní skript ukazuje praktický, připravený workflow, který můžete vložit do jakéhokoliv automatizačního pipeline.

Pokud chcete jít dál, zkuste experimentovat s:

- **Vylepšením obrazu** (kontrast, binarizace) před OCR
- **Extrahováním více ROI** pro formuláře s několika poli
- **Hromadným zpracováním** celých složek naskenovaných dokumentů
- **Integrací** s downstream systémy (např. ukládání extrahovaných dat do databáze)

Neváhejte kód přizpůsobit svému vlastnímu případu a šťastné programování! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}