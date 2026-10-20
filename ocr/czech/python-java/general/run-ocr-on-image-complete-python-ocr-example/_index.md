---
category: general
date: 2026-03-18
description: Rychle provádějte OCR na obrázku pomocí Pythonu. Naučte se, jak rozpoznat
  text z PNG, načíst obrázek pro OCR a extrahovat slova z obrázku v podrobném průvodci.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: cs
og_description: Spusťte OCR na obrázku pomocí Pythonu. Tento tutoriál ukazuje, jak
  rozpoznat text z PNG, načíst obrázek pro OCR a extrahovat slova z obrázku s kompletním
  příkladem kódu.
og_title: Spusťte OCR na obrázku – Průvodce Pythonem
tags:
- OCR
- Python
- Image Processing
title: Spusťte OCR na obrázku – Kompletní příklad OCR v Pythonu
url: /cs/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku – Kompletní příklad Python OCR

Už jste někdy potřebovali **spustit OCR na obrázku** a nevedeli jste, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tuto překážku, když poprvé řeší extrakci textu ze skenovaných dokumentů. V tomto tutoriálu projdeme **příkladem Python OCR**, který vám umožní **rozpoznat text z PNG** souborů, **načíst obrázek pro OCR** a **extrahovat slova z obrázku** s ukazateli spolehlivosti – a to vše během několika řádků kódu.

Probereme vše, co potřebujete: požadovanou knihovnu, jak nastavit engine, proč je každý krok důležitý a jak vypadá výstup. Na konci budete schopni vložit tento úryvek do svého projektu a okamžitě začít získávat text z libovolného obrázku. Žádné zbytečnosti, jen praktické, spustitelné řešení.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte:

- Python 3.8 nebo novější nainstalovaný  
- Balíček `ocrengine` (nebo jakoukoli knihovnu, která poskytuje třídu `OcrEngine`). Nainstalujete jej pomocí `pip install ocrengine` – upravte název, pokud používáte jinou OCR knihovnu, např. `pytesseract`.  
- Soubor s obrázkem (PNG, JPG, atd.), který chcete zpracovat – v tomto návodu použijeme `invoice.png`.  

To je vše. Žádné těžké závislosti, žádné externí služby, jen čistý Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: příklad spuštění OCR na obrázku – skenovaná faktura je zpracovávána*

## Krok 1 – Instalace a import OCR knihovny

Nejprve si do prostředí nainstalujeme OCR engine a importujeme jej. Pokud používáte hypotetický balíček `ocrengine`, import vypadá takto:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Proč je to důležité:** Import správné třídy vám poskytne přístup k metodám, které později použijeme, jako `setImageFromFile` a `recognize`. Pokud tento krok přeskočíte, Python vyhodí `ModuleNotFoundError` a už se vám nepodaří načíst obrázek.

## Krok 2 – Vytvoření instance OCR engine

Jakmile je knihovna připravena, potřebujeme objekt engine, který bude držet konfiguraci a stav procesu rozpoznávání.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Tip:* Některé OCR enginy vám umožňují v tomto okamžiku doladit jazykové modely nebo nastavení DPI. Pro základní **python OCR example** fungují výchozí hodnoty, ale pokud pracujete s nízkým rozlišením skenů, zvažte jejich úpravu zde.

## Krok 3 – Načtení obrázku, který chcete zpracovat

Dalším logickým krokem je **načíst obrázek pro OCR**. Ukážete engine cestu k souboru PNG (nebo jinému podporovanému formátu), který chcete analyzovat.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Co se děje pod kapotou?** Engine načte pixelová data, převede je do formátu, který rozpoznávací algoritmus dokáže zpracovat, a uloží je interně. Pokud je cesta k souboru špatná, získáte `FileNotFoundError`, takže si dvakrát ověřte, že obrázek existuje.

## Krok 4 – Spuštění rozpoznávacího algoritmu

S načteným obrázkem konečně **spustíme OCR na obrázku**, abychom získali textový obsah.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

V tomto okamžiku engine prohledá bitmapu, aplikuje vzorové porovnání a vrátí objekt, který obsahuje každé detekované slovo, řádek a metriku spolehlivosti.

## Krok 5 – Procházení rozpoznaných slov a zobrazení spolehlivosti

Nejužitečnější částí každého OCR workflow je vidět **spolehlivost** pro každý extrahovaný token. Říká vám, jak si engine jistý je každým slovem, a umožňuje filtrovat výsledky s nízkou spolehlivostí, pokud je to potřeba.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Očekávaný výstup** (ukázka):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Nyní můžete přesně vidět **která slova byla z obrázku extrahována** a jak spolehlivá je každá detekce. To je jádro každého **extrahování slov z obrázku** pipeline.

## Řešení běžných okrajových případů

### Co když je obrázek ve stupních šedi?

Některé OCR enginy fungují lépe s barevnými obrázky. Pokud zaznamenáte nízkou spolehlivost napříč všemi výsledky, zkuste převést PNG na kontrastnější černobílou verzi před předáním engine. K tomu pomůže Pillow:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Práce s více jazyky

Pokud dokument obsahuje jak angličtinu, tak španělštinu, budete chtít **rozpoznat text z PNG** pomocí vícejazykového modelu. Většina engine umožňuje nastavit seznam jazyků během inicializace:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrování slov s nízkou spolehlivostí

Někdy potřebujete jen slova s spolehlivostí nad, řekněme, 90 %. Rychlý filtr vypadá takto:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Kompletní, připravený skript

Spojením všech částí získáte jeden skript, který můžete zkopírovat a spustit okamžitě (jen nahraďte cestu k vašemu PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Spusťte jej pomocí:

```bash
python run_ocr_on_image.py
```

Měli byste vidět seznam slov a procenta spolehlivosti vytištěné do konzole, přesně tak, jak bylo ukázáno dříve.

## Často kladené otázky

**Funguje to i s JPG nebo TIFF soubory?**  
Ano. Metoda `setImageFromFile` přijímá jakýkoli formát, který podkladová knihovna dokáže dekódovat, takže můžete **spustit OCR na obrázku** souborech typu JPG, TIFF, BMP atd.

**Mohu zpracovávat více obrázků v cyklu?**  
Samozřejmě. Zabalte kroky načtení a rozpoznání do `for` smyčky přes seznam cest k souborům. Jen nezapomeňte znovu inicializovat engine, pokud knihovna vyžaduje čerstvou instanci pro každý obrázek.

**Co když potřebuji text jako jeden řetězec místo jednotlivých slov?**  
Většina OCR výstupních objektů poskytuje metodu `getText()`, která vrací celý dokument. Příklad:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Další kroky a související témata

Nyní, když víte, jak **spustit OCR na obrázku**, můžete zkoumat:

- **Post‑processing**: Použijte regulární výrazy k vyčištění dat, jako jsou data, částky nebo ID extrahovaná z faktur.  
- **Dávkové zpracování**: Kombinujte skript s `os.listdir()` pro zpracování celých složek skenovaných dokumentů.  
- **Alternativní knihovny**: `pytesseract` je populární open‑source volba; workflow je podobné – jen zaměňte volání engine.  
- **Export výsledků**: Zapište extrahovaná slova a skóre spolehlivosti do CSV pro další analýzu.

Každé z těchto rozšíření staví přímo na základech, které jsme zde vytvořili, a umožňuje vám proměnit surová OCR data v použitelné informace.

---

### TL;DR

Ukázali jsme stručný **python OCR example**, který demonstruje, jak **načíst obrázek pro OCR**, **spustit OCR na obrázku** a **extrahovat slova z obrázku** s reportováním spolehlivosti. Kompletní skript je připraven k běhu a nyní máte znalosti, jak jej přizpůsobit libovolnému projektu, který potřebuje **rozpoznat text z PNG** (nebo jiných formátů). Vyzkoušejte ho, upravte prahové hodnoty spolehlivosti a sledujte, jak se vaše aplikace během minut stane textově uvědomělou. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}