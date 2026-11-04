---
category: general
date: 2026-03-26
description: Naučte se, jak vyrovnat obrázek, rozpoznat text z obrázku a vytvořit
  pipeline pro předzpracování obrázků, která odstraní šum ze skenu a převede naskenovaný
  obrázek na text.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: cs
og_description: Jak vyrovnat obrázek a převést zkosený sken na prohledávatelný text.
  Postupujte podle tohoto návodu, abyste rozpoznali text z obrázku, odstranili šum
  ze skenu a převedli naskenovaný obrázek na text.
og_title: Jak vyrovnat obrázek – krok za krokem průvodce OCR
tags:
- OCR
- image-processing
- Python
title: Jak narovnat obrázek – Kompletní průvodce s OCR
url: /cs/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak narovnat obrázek – Kompletní průvodce s OCR

Už jste se někdy zamýšleli **jak narovnat obrázek**, který vyšel z levného skeneru? Nejste sami. Šikmá stránka vypadá neprofesionálně a navíc může sklon narušit jakýkoli OCR engine, který se snaží **rozpoznat text z obrázku**.  

V tomto tutoriálu projdeme kompletní **pipeline předzpracování obrázku**, která narovná, binarizuje a odstraňuje šum ze skenu, a poté ho předá OCR enginu, abyste mohli **převést naskenovaný obrázek na text** s minimální námahou. Žádná magie, jen čistý Python a malá knihovna, která udělá těžkou práci.

## Co budete potřebovat

- Python 3.9+ (kód funguje i na 3.10 a novějších)
- Balíček `ocr` (nainstalujte pomocí `pip install ocr‑toolkit` – nahraďte skutečným názvem knihovny)
- Naskenovaný JPEG nebo PNG, který je zřetelně nakřivený (např. `skewed_scan.jpg`)
- Trochu zvědavosti, proč každý krok předzpracování má smysl

To je vše. Žádné těžké závislosti jako OpenCV, pokud nechcete jít později hlouběji.

## Krok 1: Načtení naskenovaného obrázku

Prvním krokem je načíst soubor do paměti. Tento krok je jednoduchý, ale zásadní – pokud je cesta špatná, vše ostatní selže.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Proč?**  
> Načtení obrázku nám poskytne manipulovatelný objekt, se kterým může pracovat `ocr.ImagePreprocessor`. Přeskočení tohoto kroku by pipeline nechalo slepou k reálným pixelovým datům.

## Jak narovnat obrázek a připravit ho pro OCR

Nyní, když máme obrázek, narovnáme ho. Metoda `deskew()` odhadne úhel sklonu a otočí obrázek zpět do vodorovné polohy.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Tip:** Pokud jsou vaše skeny jen mírně odchýlené (≤ 3°), výchozí algoritmus je obvykle přesný. Pro extrémní úhly možná budete muset upravit vnitřní parametry – podívejte se do dokumentace knihovny na `max_angle`.

## Binarizace obrázku – Převod na černobílý

OCR enginy milují vstup s vysokým kontrastem. Převod obrázku na binární (černobílou) reprezentaci odstraní jemné odstíny, které mohou zmást rozpoznávání znaků.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Co se děje?**  
> Pixely jasnější než 128 se stanou bílými; vše ostatní se změní na černé. Upravte práh, pokud je váš sken neobvykle tmavý nebo světlý.

## Odstranění šumu ze skenu před OCR

I dokonale narovnaný obrázek může obsahovat skvrny, prach nebo artefakty komprese. Tyto malé tečky jsou nepřítelem každého OCR enginu.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Proč odstraňovat šum?**  
> Šum vytváří falešné hrany, které OCR engine může interpretovat jako znaky. Malý poloměr funguje pro většinu skenů; zvýšte ho u dokumentů s výrazným zrnem.

## Použití pipeline předzpracování obrázku

Všechny nastavení jsou připraveny – nyní spustíme pipeline na původním obrázku.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Výsledek:** `processed_image` je vyčištěná, narovnaná, vysokokontrastní bitmapa připravená k extrakci textu.

## Rozpoznání textu z obrázku pomocí OCR enginu

Přichází čas skutečně přečíst text. Inicializujeme OCR engine, předáme mu náš vylepšený obrázek a požádáme o surový řetězec.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Očekávaný výstup** (příklad):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Pokud vidíte nesmyslné znaky, zkontrolujte krok narovnání nebo experimentujte s jinou hodnotou `threshold`.

## Vytvoření pipeline předzpracování obrázku – Kompletní skript

Sestavením všeho dohromady získáte jeden spustitelný skript, který můžete vložit do souboru `.py` a spustit:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** Zabalte celý proces do funkce (`def ocr_from_file(path): …`), pokud plánujete zpracovávat mnoho souborů najednou.

## Často kladené otázky a okrajové případy

- **Co když je obrázek už ve správné orientaci?**  
  Metoda `deskew()` detekuje úhel blízký nule a nechá obrázek nedotčený, takže jej můžete bezpečně spustit na každém souboru.

- **Můj sken je barevný – mám ho zachovat?**  
  Barva nepřináší žádnou hodnotu pro většinu OCR úloh. Binarizace ji odstraní, urychlí zpracování a sníží využití paměti.

- **Mohu řetězit více kroků předzpracování?**  
  Rozhodně. Třída `ImagePreprocessor` je navržena pro pipeline; můžete před voláním `apply()` přidat `sharpen()`, `contrast_enhance()` nebo vlastní filtry.

- **Výstup OCR obsahuje nadbytečné zalomení řádků – jak to opravit?**  
  Post‑processujte řetězec pomocí `text.replace("\n", " ").strip()` nebo použijte pokročilejší knihovnu pro analýzu rozvržení, jako jsou režimy `--psm` v Tesseractu.

## Další kroky

Nyní, když víte **jak narovnat obrázek** a máte solidní **pipeline předzpracování obrázku**, můžete zkusit:

- Integrovat **rozpoznání textu z obrázku** do Flask API pro nahrávání dokumentů za běhu.
- Použít pipeline k **odstranění šumu ze skenu** historických dokumentů, kde je zachování důležité.
- Škálovat na hromadné zpracování tisíců stránek a vytvořit prohledávatelný PDF pomocí `pdfminer` nebo `PyMuPDF`.

Nebojte se experimentovat s různými prahy, poloměry odstraňování šumu nebo dokonce vyměnit OCR backend za Tesseract, pokud potřebujete vícejazyčnou podporu. Základy zůstávají stejné: narovnat, vyčistit, pak číst.

---

*Šťastné programování! Pokud narazíte na potíže, zanechte komentář níže – rád vám pomohu doladit pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}