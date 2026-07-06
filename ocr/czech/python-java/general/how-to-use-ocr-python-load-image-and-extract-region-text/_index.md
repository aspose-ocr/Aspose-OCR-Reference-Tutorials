---
category: general
date: 2026-06-25
description: Jak používat OCR v Pythonu – naučte se, jak načíst obrázek pro OCR, rozpoznat
  text v oblasti a rychle extrahovat text z oblasti.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: cs
og_description: Jak používat OCR v Pythonu – krok za krokem návod, jak načíst obrázek,
  rozpoznat text v konkrétní oblasti a získat číslo faktury.
og_title: 'Jak používat OCR v Pythonu: Načíst obrázek a extrahovat text oblasti'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Jak používat OCR v Pythonu: Načíst obrázek a extrahovat text z oblasti'
url: /cs/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít OCR v Pythonu: Načíst obrázek a extrahovat text z oblasti

**Jak používat OCR v Pythonu** je jednodušší, než si myslíte. Už jste někdy zírali na naskenovanou fakturu a přemýšleli, jak získat jen číslo faktury, aniž byste museli parsovat celou stránku? Nejste v tom sami — mnoho vývojářů narazí na tento problém, když poprvé experimentují s optickým rozpoznáváním znaků. V tomto průvodci si ukážeme, jak načíst obrázek pro OCR, definovat obdélník, rozpoznat text v této oblasti a nakonec extrahovat text z oblasti. Na konci budete mít připravený skript, který izoluje libovolný kus textu, který potřebujete.

> *Pro tip:* Pokud pracujete s PDF, nejprve každou stránku převedete na obrázek — většina OCR knihoven nejlépe pracuje s PNG/JPEG.

## Co budete potřebovat

- Python 3.8+ (doporučujeme nejnovější stabilní verzi)  
- OCR knihovnu, která poskytuje třídu `OcrEngine` (např. **ocr** z `pip install ocr-lib`)  
- Ukázkový obrázek — v našem příkladu použijeme `invoice.png` umístěný ve složce, kterou ovládáte  
- Základní znalost obdélníků (x, y, šířka, výška)  

Žádné těžké závislosti, žádná GPU — pouze čistě CPU, což zajišťuje přenositelnost.

---

## Jak použít OCR: Inicializace engine (Krok 1)

Než bude možné číst jakýkoli text, potřebujete instanci OCR engine. Představte si ji jako mozek, který bude analyzovat pixelové vzory.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Proč je to důležité:* Inicializace engine načte jazykové modely a nastaví výchozí konfigurace. Vynechání tohoto kroku vyvolá výjimku ve chvíli, kdy zavoláte `recognize_region`.

---

## Načtení obrázku pro OCR (Krok 2)

Jakmile je engine připraven, předáme mu obrázek. Metoda `Image.load` knihovny zvládne běžné formáty a normalizuje bitmapu.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Pokud soubor není nalezen, Python vyhodí `FileNotFoundError`. Ujistěte se, že cesta je absolutní nebo relativní k pracovnímu adresáři skriptu.  

*Hraniční případ:* Některé OCR engine očekávají obrázek ve stupních šedi. Pokud zaznamenáte špatnou přesnost, nejprve obrázek převedete:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Rozpoznání textu v oblasti (Krok 3)

Definování oblasti je moment, kdy řeknete engine, *kde* má hledat. `Rectangle` přijímá hodnoty s plovoucí desetinnou čárkou pro subpixelovou přesnost, což se hodí u vysoce rozlišených skenů.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – levý horní roh obdélníku (v pixelech)  
- **width, height** – rozměry rámečku  

Možná se ptáte, jak tato čísla získat. Jednoduchý způsob je otevřít obrázek v libovolném editoru (např. GIMP nebo Paint.NET) a pomocí nástroje pro výběr přečíst souřadnice.  

*Proč neprovádět OCR celé stránky?* Omezení oblasti snižuje šum, zrychluje zpracování a výrazně zvyšuje přesnost u malých polí, jako jsou čísla faktur.

---

## Jak extrahovat text z oblasti (Krok 4)

Po nastavení oblasti požádejte engine, aby rozpoznal jen tento výřez. Výsledný objekt obsahuje surový text a skóre důvěry.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Pokud OCR engine podporuje více jazyků, můžete předat volitelný kód jazyka:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Častý úskalí:* Některé engine vracejí seznam slov místo jedné řetězce. V takovém případě je spojte:

```python
text = " ".join(region_result.words)
```

---

## Výpis extrahovaného čísla faktury (Krok 5)

Nakonec vytiskněte — nebo uložte — extrahovaný text. Můžete také provést post‑processing, abyste odstranili nadbytečné mezery nebo ne‑číselné znaky.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Spuštěním skriptu s správně zarovnaným obdélníkem byste měli získat něco jako:

```
Invoice number: 20231578
```

Pokud se zobrazí nesmyslné znaky, zkontrolujte souřadnice obdélníku nebo zvažte zvýšení rozlišení obrázku.

---

## Kompletní funkční příklad

Spojením všech částí získáte samostatný skript, který můžete zkopírovat a spustit:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Uložte soubor jako `extract_invoice.py`, nahraďte `YOUR_DIRECTORY` skutečnou složkou a spusťte:

```bash
python extract_invoice.py
```

Měli byste vidět číslo faktury vytištěné v konzoli.

---

## Často kladené otázky

**Q: Co když je číslo faktury vytištěno v ozdobném fontu?**  
A: Většina moderních OCR engine zvládá širokou škálu fontů, ale můžete zvýšit přesnost trénováním vlastního jazykového modelu nebo předzpracováním obrázku (např. aplikací prahového filtru).

**Q: Můžu extrahovat více polí najednou?**  
A: Rozhodně. Definujte seznam objektů `Rectangle` — jeden pro každé pole — a projděte je v cyklu, přičemž každý výsledek uložíte do slovníku.

**Q: Funguje to na vícestránkových PDF?**  
A: Nejprve každou stránku převedete na obrázek (pomocí `pdf2image` nebo podobného nástroje) a poté použijete stejný region‑based extraction na každou stránku.

---

## Závěr

V tomto tutoriálu jsme si ukázali **jak použít OCR** v Pythonu k načtení obrázku, rozpoznání textu v konkrétní oblasti a extrahování textu z této oblasti — ideální pro získání čísel faktur, ID objednávek nebo jakýchkoli malých úryvků z naskenovaných dokumentů. Izolací oblasti zájmu získáte rychlost, přesnost a méně následné úpravy.

Jste připraveni na další krok? Zkuste rozšířit skript tak, aby **načítal obrázek pro OCR** z adresáře s hromadnými fakturami, nebo experimentujte s **rozpoznáním textu v oblasti** pro různá pole jako datum a celkovou částku. Princip je stejný — stačí změnit souřadnice obdélníku.

Pokud jste narazili na problémy nebo máte nápady na vylepšení, zanechte komentář níže. Šťastné programování a ať jsou vaše OCR pipeline vždy přesné!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}