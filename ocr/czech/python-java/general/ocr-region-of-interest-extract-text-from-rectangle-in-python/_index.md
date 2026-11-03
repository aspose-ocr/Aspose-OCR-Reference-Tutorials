---
category: general
date: 2026-05-31
description: Naučte se, jak použít oblast zájmu OCR k načtení obrázku pro OCR a extrahování
  textu z obdélníku, ideální pro rozpoznání částky na faktuře.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: cs
og_description: Ovládněte oblast zájmu OCR pro načtení obrázku, extrahujte text z
  obdélníku a rozpoznávejte text z faktury v jednom tutoriálu.
og_title: OCR oblast zájmu – krok za krokem průvodce v Pythonu
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR oblast zájmu – extrahovat text z obdélníku v Pythonu
url: /cs/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR oblast zájmu – Extrahování textu z obdélníku v Pythonu

Už jste se někdy zamýšleli, jak **ocr region of interest** konkrétní část naskenované faktury, aniž byste do enginu nahrávali celou stránku? Nejste první, kdo se dívá na rozmazaný účtenku a přemýšlí: “Jak získat částku, která je někde v pravém dolním rohu?” Dobrou zprávou je, že můžete OCR knihovně přesně říct, kde má hledat, což dramaticky zvyšuje jak rychlost, tak přesnost.

V tomto průvodci projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **load image for OCR**, definovat **region of interest**, a pak **extract text from rectangle**, abyste nakonec **recognize text from invoice** a odpověděli na klasickou otázku „jak extrahovat částku“. Žádné vágní odkazy – jen konkrétní kód, jasná vysvětlení a několik tipů, které byste si přáli vědět dříve.

---

## Co si vytvoříte

Na konci tohoto tutoriálu budete mít malý Python skript, který:

1. Načte obrázek faktury z disku.  
2. Označí obdélníkovou ROI, kde se nachází celková částka.  
3. Spustí OCR pouze uvnitř této ROI.  
4. Vytiskne vyčištěný řetězec částky.  

Vše funguje s libovolnou OCR knihovnou, která podporuje ROI – zde použijeme fiktivní, ale reprezentativní balíček `SimpleOCR`, který napodobuje populární nástroje jako Tesseract nebo EasyOCR. Klidně jej zaměňte; koncepty zůstávají stejné.

## Požadavky

- Python 3.8+ nainstalovaný (`python --version` by měl ukazovat ≥3.8).  
- Pip‑instalovatelný OCR balíček (např. `pip install simpleocr`).  
- Obrázek faktury (PNG nebo JPEG) umístěný ve složce, na kterou můžete odkazovat.  
- Základní znalost funkcí a tříd v Pythonu (nic složitého).

Pokud už to máte, skvělé – ponořme se dál. Pokud ne, nejprve stáhněte obrázek; zbytek kroků je nezávislý na skutečném obsahu souboru.

## Krok 1: Načtení obrázku pro OCR

První věc, kterou jakýkoli OCR workflow potřebuje, je bitmapa, ze které může číst. Většina knihoven poskytuje jednoduchou metodu `load_image`, která přijímá cestu k souboru. Zde je, jak to udělat s naším `SimpleOCR` enginem:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Používejte absolutní cesty nebo `os.path.join`, abyste se vyhnuli překvapením typu „soubor nenalezen“ při spouštění skriptu z jiného pracovního adresáře.

## Krok 2: Definování OCR oblasti zájmu

Místo toho, aby engine skenoval celou stránku, řekneme mu *přesně*, kde se částka nachází. Toto je krok **ocr region of interest** a je klíčem k spolehlivému extrahování, zejména když dokument obsahuje šumivé hlavičky nebo patičky.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Proč tyto čísla? `x` a `y` jsou pixelové offsety od levého horního rohu, zatímco `width` a `height` popisují velikost boxu. Pokud si nejste jisti, otevřete obrázek v libovolném editoru, zapněte pravítko a poznamenejte si souřadnice. Mnoho IDE dokonce umožňuje zobrazit pozici kurzoru při najetí.

## Krok 3: Extrahování textu z obdélníku

Nyní, když je ROI nastavená, požádáme engine o **recognize text from invoice**, ale omezený na obdélník, který jsme právě přidali. Volání vrací objekt výsledku, který typicky obsahuje surový řetězec, skóre důvěry a někdy i ohraničující boxy.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Za scénou `recognize()` iteruje přes každou ROI, ořízne daný výřez, spustí OCR model a spojí výsledky dohromady. Proto definování úzké **extract text from rectangle** oblasti může ušetřit sekundy při zpracování dávkových úloh.

## Krok 4: Jak extrahovat částku – vyčistit výstup

OCR není dokonalé; často získáte nadbytečné mezery, konce řádků nebo dokonce špatně přečtené znaky (např. “S” místo “5”). Rychlé `strip()` a malý regex obvykle stačí pro peněžní hodnoty.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Proč je to důležité:** Pokud plánujete částku vložit do databáze nebo platební brány, potřebujete předvídatelný formát. Odstranění bílých znaků a filtrování ne‑číselných znaků zabraňuje chybám v dalším zpracování.

## Krok 5: Rozpoznání textu z faktury – Kompletní skript

Sestavíme vše dohromady, zde je kompletní, připravený ke spuštění skript. Uložte jej jako `extract_amount.py` a spusťte `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Očekávaný výstup

```
Amount: 1,245.67
```

Pokud je ROI špatně zarovnaná, můžete vidět něco jako `Amount: 1245.6S` – všimněte si nadbytečného “S”. Upravit souřadnice obdélníku a znovu spustit, dokud výstup nebude čistý.

## Běžné problémy a okrajové případy

| Problém | Proč k tomu dochází | Řešení |
|---------|----------------------|--------|
| **ROI příliš malý** | Text částky je oříznutý, což vede k částečnému rozpoznání. | Zvětšete `width`/`height` o ~10‑20 % a znovu otestujte. |
| **Nesprávné DPI** | Nízké rozlišení skenů (≤150 dpi) snižuje přesnost OCR. | Převzorkujte obrázek na 300 dpi před načtením, nebo požádejte skener o vyšší DPI. |
| **Více měn** | Regex vybere první číselnou skupinu, která může být číslem faktury. | Upravte regex tak, aby hledal měnové symboly (`$`, `€`, `£`) před číslicemi. |
| **Otočené faktury** | OCR enginy předpokládají svislý text; otočené stránky narušují rozpoznání. | Aplikujte korekci rotace (`ocr_engine.rotate(90)`) před přidáním ROI. |
| **Šum na pozadí** | Stíny nebo razítka zmatení model. | Předzpracujte jednoduchým prahem (`cv2.threshold`) nebo použijte filtr na odstranění šumu. |

Řešení těchto okrajových případů včas vám ušetří hodiny ladění později.

## Pro tipy pro reálné projekty

- **Batch Processing:** Procházejte složku s fakturami, dynamicky vypočítejte ROI (např. na základě detekce šablony) a uložte výsledky do CSV.  
- **Template Matching:** Pokud pracujete s několika rozvrženími faktur, udržujte JSON mapu `template_id → ROI coordinates`. Přepínejte ROI podle rychlého klasifikátoru rozvržení.  
- **Parallel Execution:** Použijte `concurrent.futures.ThreadPoolExecutor` k souběžnému spuštění více OCR instancí – skvělé pro vysokovýkonné back‑office pipeline.  
- **Confidence Filtering:** Většina OCR výsledků obsahuje skóre důvěry. Odmítněte výsledky pod určitým prahem (např. 85 %) a označte je k ruční kontrole.

## Závěr

Probrali jsme vše, co potřebujete k **ocr region of interest**, **load image for OCR**, **extract text from rectangle** a nakonec **recognize text from invoice**, abyste odpověděli na klasickou otázku **how to extract amount**. Skript je kompaktní, ale dostatečně flexibilní, aby se přizpůsobil různým formátům dokumentů, jazykům i OCR backendům.

Nyní, když ovládáte základy, zvažte rozšíření workflow: přidejte skenování čárových kódů, integraci s PDF parserem nebo odeslání extrahované částky do účetního API. Možnosti jsou neomezené a s dobře definovanou ROI získáte vždy rychlejší a čistší výsledky.

Pokud narazíte na problém, zanechte komentář níže – šťastné OCRování!

![příklad oblasti zájmu OCR](https://example.com/ocr_roi_example.png "příklad oblasti zájmu OCR")


## Co byste se měli naučit dál?

- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahování textu z obrázku v Javě s Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extrahování textu z obrázku – OCR optimalizace s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}