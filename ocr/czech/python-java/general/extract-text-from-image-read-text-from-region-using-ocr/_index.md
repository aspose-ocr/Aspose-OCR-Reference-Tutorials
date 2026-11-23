---
category: general
date: 2026-07-05
description: Extrahujte text z obrázku pomocí Python OCR. Naučte se, jak načíst obrázek
  pro OCR, přečíst text z oblasti a extrahovat text z faktury pomocí několika řádků
  kódu.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: cs
og_description: Extrahujte text z obrázku pomocí Python OCR. Tento průvodce ukazuje,
  jak načíst obrázek pro OCR, přečíst text z oblasti a rychle extrahovat text z faktury.
og_title: Extrahovat text z obrázku – Číst text z oblasti pomocí OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extrahovat text z obrázku – Číst text z oblasti pomocí OCR
url: /cs/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku – číst text z oblasti pomocí OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale zajímá vás jen konkrétní část – například celková částka na faktuře? Nejste v tom sami. V mnoha reálných projektech budete potřebovat **číst text z oblasti** místo parsování celého obrázku. Naštěstí s několika řádky Pythonu můžete načíst obrázek pro OCR, definovat oblast zájmu (ROI) a získat přesně ty znaky, které potřebujete.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje, jak **načíst obrázek pro OCR**, nastavit ROI a nakonec **extrahovat text z faktury**. Na konci budete mít připravený úryvek k okamžitému použití, který funguje s libovolnou populární OCR knihovnou podporující rozpoznávání podle oblasti.

---

## Co budete potřebovat

- Python 3.8+ (kód funguje i na 3.10)  
- OCR balíček, který poskytuje třídu `OcrEngine` (pro ukázku použijeme fiktivní modul `ocr`; nahraďte jej `pytesseract`, `easyocr` nebo libovolnou knihovnou, která podporuje ROI)  
- Ukázkový obrázek – např. `invoice.png` – který obsahuje jasně tištěný text  
- Základní znalost Python funkcí a tříd (není potřeba hluboké znalosti strojového učení)

Pokud už máte vše připravené, skvěle – pojďme na to. Pokud ne, stáhněte si nejnovější Python z python.org a nainstalujte OCR balíček pomocí `pip install your-ocr-lib`.

---

![Příklad extrakce textu z obrázku](extract-text-from-image.png "Extrahování textu z obrázku – ukázka OCR podle oblasti")

*Obrázek výše ilustruje oblast (červený obdélník), na kterou se zaměříme pro **extrahování textu z obrázku**.*

---

## Krok 1: Instalace a import OCR knihovny

Nejprve se ujistěte, že OCR knihovna je ve vašem prostředí dostupná. Níže uvedený import funguje pro většinu balíčků, které poskytují vysokou úroveň třídy `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Tip:** Pokud používáte `pytesseract`, musíte nainstalovat binární soubor Tesseract zvlášť a nastavit `pytesseract.pytesseract.tesseract_cmd` na jeho cestu.

---

## Krok 2: Vytvoření OCR enginu a nastavení jazyka

Vytvoření enginu je jednoduché, ale nastavení jazyka výrazně zvyšuje přesnost, zejména u faktur, které obsahují čísla a anglická slova.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Proč to děláme? OCR engine používá jazykové modely k predikci znaků; když mu řeknete, že očekává angličtinu, snížíte falešně pozitivní rozpoznání, např. zaměnění “0” za “O”.

---

## Krok 3: Načtení obrázku pro OCR

Nyní skutečně **načteme obrázek pro OCR**. Většina knihoven přijímá cestu k souboru nebo Pillow objekt obrázku. Zde používáme vestavěný načítač knihovny pro jednoduchost.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Ujistěte se, že cesta ukazuje na správný adresář; častá chyba je zapomenutí relativní cesty, když skript běží z jiného pracovního adresáře.

---

## Krok 4: Definování oblasti zájmu (ROI)

Definování ROI je jádrem **čtení textu z oblasti**. Představte si to jako nakreslení obdélníku kolem části faktury, kde je uvedena celková částka.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` a `top` představují X a Y souřadnice levého horního rohu obdélníku.  
- `width` a `height` určují velikost boxu.  
- Můžete experimentovat s různými hodnotami pomocí prohlížeče obrázků, který zobrazuje pixelové souřadnice.

> **Proč je ROI důležitá:** Spuštění OCR na celé stránce plýtvá CPU cykly a často zavádí šum z nesouvisejícího textu, tabulek nebo grafiky. Zaměřením se na oblast získáte čistší výsledek a rychlejší zpracování.

---

## Krok 5: Provedení OCR na zadané oblasti

S veškerým nastavením konečně **extrahujeme text z obrázku** – ale jen v rámci definované ROI.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Metoda `recognize` vrací objekt, který typicky obsahuje surový řetězec, skóre důvěry a někdy i ohraničující boxy pro každé slovo. Pro naše účely potřebujeme jen prostý text.

---

## Krok 6: Výpis extrahovaného textu

Vytiskněme výsledek a podívejme se, co jsme získali. Tento krok demonstruje **extrahování textu z faktury** v reálném scénáři.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Očekávaný výstup

```
Text inside ROI:
Total Amount: $1,245.67
```

Pokud má vaše faktura jiný rozvrh, uvidíte text, který se nachází uvnitř obdélníku – možná číslo faktury, datum nebo referenci PO.

---

## Krok 7: Zabalit vše do znovupoužitelné funkce (volitelné)

Aby bylo řešení použitelné napříč více fakturami, zabalte logiku do funkce. To také ilustruje **ocr na oblasti** jako obecný nástroj.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Nyní můžete funkci zavolat s libovolnou fakturou:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Časté problémy a jak se jim vyhnout

| Problém | Proč se vyskytuje | Řešení |
|---------|-------------------|--------|
| **Prázdný výstup** | ROI ve skutečnosti neobsahuje žádný text (špatné souřadnice). | Ověřte pixelové hodnoty v editoru obrázků; přidejte vizuální ladící překryv. |
| **Špatné znaky** | Nízké rozlišení obrázku nebo špatný kontrast. | Předzpracujte obrázek: převod na odstíny šedi, aplikace prahování (`cv2.threshold`). |
| **Nesprávný jazyk** | Engine používá výchozí jazyk bez potřebné znakové sady. | Explicitně nastavte `ocr_engine.language` na `ENGLISH` nebo vhodnou lokalizaci. |
| **Zpomalení** | Opakované spouštění OCR na velkých obrázcích. | Zmenšete obrázek před načtením, nebo nejprve ořízněte ROI. |

---

## Rozšíření příkladu: Více ROI

Někdy faktura obsahuje několik polí, která potřebujete – například **extrahovat text z faktury** jak pro celkovou částku, tak pro datum faktury. Můžete iterovat přes seznam obdélníků:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Tento vzor udržuje kód přehledný a usnadňuje pozdější přidání dalších oblastí.

---

## Závěr

Právě jsme prošli kompletním workflow od začátku do konce pro **extrahování textu z obrázku** pomocí Python OCR, zaměřené na konkrétní oblast. Tím, že **načtete obrázek pro OCR**, definujete **oblast zájmu** a spustíte engine, můžete spolehlivě **číst text z oblasti** – ideální pro získávání částek z faktur, dat z účtenek nebo jakýchkoli jiných lokalizovaných informací.  

Klidně experimentujte


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}