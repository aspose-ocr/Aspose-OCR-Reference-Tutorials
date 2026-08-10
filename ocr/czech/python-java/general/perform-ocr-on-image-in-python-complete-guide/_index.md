---
category: general
date: 2026-06-22
description: Proveďte OCR na obrázku pomocí Pythonu během několika řádků. Naučte se,
  jak načíst obrázek pro OCR, rozpoznat text z PNG a efektivně používat OCR engine.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: cs
og_description: Rychle provádějte OCR na obrázku pomocí Pythonu. Tento tutoriál ukazuje,
  jak načíst obrázek pro OCR, rozpoznat text z PNG a použít OCR engine s jistotou.
og_title: Proveďte OCR na obrázku v Pythonu – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Proveďte OCR na obrázku v Pythonu – Kompletní průvodce
url: /cs/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Provádění OCR na obrázku v Pythonu – Kompletní průvodce

Už jste někdy potřebovali **provést OCR na obrázku** souborů, ale zůstali jste uvězněni už v první řádce kódu? Nejste v tom sami. V tomto návodu vám ukážeme přesně, jak **načíst obrázek pro OCR**, nastavit lehký **OCR engine** a nakonec **rozpoznat text z PNG** pomocí několika příkazů.

Probereme vše od instalace knihovny až po ladění whitelistu tak, aby po skenování přežily jen číslice a velká písmena. Na konci budete mít připravený skript, který můžete vložit do jakéhokoli projektu – žádná tajemství, žádné zbytečné doplňky.

## Co se naučíte

- Jak **použít OCR engine** programově v Pythonu.  
- Přesné kroky k **načtení obrázku pro OCR** z lokální složky.  
- Proč a jak omezit rozpoznávání na vlastní sadu znaků.  
- Jak **rozpoznat text z PNG** a bezpečně zacházet s výsledkem.  

**Požadavky:** Python 3.7+ nainstalovaný, terminál, ve kterém se cítíte pohodlně, a obrázek (např. `serial-number.png`), který chcete přečíst. Předchozí zkušenost s OCR není nutná.

---

## Provádění OCR na obrázku – Inicializace OCR engine

První věc, kterou musíte udělat, je vytvořit instanci OCR engine. Přemýšlejte o engine jako o mozku, který analyzuje pixely a převádí je na znaky.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Proč je to důležité:* Bez engine není co zpracovávat obrázek. Třída `OcrEngine` spojuje veškeré těžké operace – předzpracování, segmentaci a klasifikaci znaků – do jediného objektu, který můžete znovu použít.

---

## Načtení obrázku pro OCR – Poskytnutí PNG souboru

Nyní, když engine existuje, musíte mu předat obrázek, který chcete přečíst. Knihovna očekává objekt `ImageStream`, který můžete vytvořit přímo ze souborové cesty.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Tip:* Udržujte obrázek ve vysokokontrastním formátu (černý text na bílém pozadí) a vyhněte se kompresním artefaktům; mohou OCR algoritmus zmást.

---

## Omezení znaků – Whitelist číslic a velkých písmen

Často vás zajímá jen podmnožina znaků – například sériové číslo obsahující jen A‑Z a 0‑9. Nastavením whitelistu řeknete engine, aby ignoroval vše ostatní, což dramaticky zvyšuje přesnost.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Co se děje pod kapotou?* Engine vytvoří filtr, který zahodí jakýkoli glyf, který není ve whitelistu, ještě před finální fází klasifikace. To je zvláště užitečné, když obrázek obsahuje šum nebo dekorativní text, který nepotřebujete.

---

## Rozpoznání textu z PNG – Spuštění OCR procesu

S připraveným engine a načteným obrázkem můžete konečně **provést OCR na obrázku**. Volání `recognize()` spustí celý pipeline a vrátí objekt výsledku.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Pokud vás zajímá výkon, metoda obvykle skončí během několika stovek milisekund pro PNG 300 × 200 px na moderním notebooku.

---

## Výstup a ověření – Získání rozpoznaného textu

Poslední krok je extrahovat čistý text z objektu výsledku. Cokoliv, co neodpovídá whitelistu, je automaticky vynecháno, takže získáte čistý řetězec připravený k dalšímu zpracování.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typický výstup:* `AB12C3D4E5` (předpokládáme, že obrázek obsahoval právě toto sériové číslo).  

Pokud je výstup prázdný nebo poškozený, zkontrolujte kvalitu obrázku a whitelist; častým úskalím je neúmyslné vynechání potřebných znaků.

---

## Hraniční případy a časté problémy

| Situace | Co zkontrolovat | Navrhované řešení |
|-----------|---------------|---------------|
| **Soubor nenalezen** | Chybná cesta nebo chybějící soubor | Použijte `os.path.abspath` k ověření úplné cesty před voláním `set_image`. |
| **Nízký kontrast obrázku** | Text splývá s pozadím | Aplikujte jednoduchý prah (`Pillow` nebo `OpenCV`) před předáním obrázku engine. |
| **Neočekávané znaky** | Whitelist příliš restriktivní | Přidejte chybějící znaky do řetězce whitelistu. |
| **Velké obrázky** | Pomalu rozpoznávání | Zmenšete obrázek na maximální šířku 1024 px; kvalita OCR obvykle zůstane vysoká. |

---

## Kompletní skript – Připravený ke spuštění

Níže je kompletní, samostatný skript, který spojuje všechny části dohromady. Uložte jej jako `ocr_demo.py`, nahraďte `YOUR_DIRECTORY` skutečnou složkou a spusťte `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Očekávaný výstup v konzoli* (když PNG obsahuje `SN12345`):

```
Recognized text: SN12345
```

---

## Závěr

Nyní přesně víte, jak **provést OCR na obrázku** v Pythonu, od **načtení obrázku pro OCR** po **rozpoznání textu z PNG** a nakonec extrahování čistého výsledku pomocí přizpůsobitelného **OCR engine**. Přístup je přímočarý, rozšiřitelný a funguje ihned pro většinu skenů typu sériové číslo.

Co dál? Vyzkoušejte zaměnit whitelist za malá písmena, experimentujte s různými formáty obrázků (JPEG, BMP) nebo integrujte skript do dávkového zpracování. Stejný vzor – engine → obrázek → nastavení → rozpoznání → výstup – platí pro prakticky jakýkoli OCR úkol, na který narazíte.

Máte otázky nebo podivný obrázek, který odmítá spolupracovat? Zanechte komentář níže a šťastné kódování! 

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram ukazující, jak provést OCR na obrázku s Python OCR engineem")


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}