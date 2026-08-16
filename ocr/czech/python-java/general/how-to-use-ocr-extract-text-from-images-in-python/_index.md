---
category: general
date: 2026-03-18
description: Jak používat OCR k extrakci textu z obrázků – rychlý průvodce rozpoznáváním
  textu z PNG souborů a načítáním obrázků pro OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: cs
og_description: Jak používat OCR k extrakci textu z obrázků – naučte se rozpoznávat
  text z PNG, načíst obrázek pro OCR a extrahovat text pomocí jednoduchého Python
  skriptu.
og_title: 'Jak používat OCR: Extrahovat text z obrázků v Pythonu'
tags:
- OCR
- Python
- Image Processing
title: 'Jak používat OCR: Extrahovat text z obrázků v Pythonu'
url: /cs/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR: Extrahování textu z obrázků v Pythonu

Už jste se někdy zamýšleli **jak používat OCR**, když máte nečistý screenshot nebo naskenovaný účtenku? Nejste v tom sami — vývojáři často potřebují vytáhnout čitelný text z obrázků, zejména PNG, které pocházejí z mobilních aplikací nebo webových nahrávek. V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **extrahovat text z obrázku**, **rozpoznat text z PNG** souborů a dokonce **načíst obrázek pro OCR** pomocí několika řádků Pythonu.

Probereme vše od instalace správné knihovny až po zpracování vícejazyčných dokumentů, takže na konci budete přesně vědět, *jak extrahovat text* z jakéhokoli obrázku, který předáte motoru. Žádné vágní odkazy, jen jasné, krok‑za‑krokem řešení, které můžete zkopírovat‑vložit a spustit.

## Co se naučíte

V následujících sekcích:

1. Nastavíte lehký OCR engine (bez těžkopádných závislostí).  
2. Načtete soubor obrázku — konkrétně PNG — do engine.  
3. Povolením automatické detekce jazyka umožníte motoru zpracovat vícejazyčný obsah.  
4. Spustíte proces rozpoznávání a získáte výsledek v prostém textu.  
5. Vyladíte workflow pro okrajové případy, jako chybějící soubory nebo nepodporované formáty.

Pokud ovládáte základní Python, jste připraveni. Předchozí zkušenost s OCR není nutná, i když rychlý pohled do dokumentace knihovny nikdy neškodí.

---

![Jak používat OCR na PNG obrázku](placeholder.png "Jak používat OCR na PNG obrázku – krok za krokem")

## Jak používat OCR – Načtení obrázku a rozpoznání textu {#how-to-use-ocr}

### Krok 1: Instalace OCR knihovny

Nejprve potřebujete Python balíček, který poskytuje třídu `OcrEngine`. Pro tento tutoriál použijeme fiktivní, ale ilustrující **SimpleOCR** balíček, který nainstalujete pomocí pip:

```bash
pip install simple-ocr
```

> **Tip:** Pokud pracujete ve virtuálním prostředí (vřele doporučeno), aktivujte jej před spuštěním instalačního příkazu. Tím udržíte závislosti projektu přehledné.

### Krok 2: Import engine a vytvoření instance

Vytvoření engine je tak jednoduché, jako zavolat jeho konstruktor. Představte si engine jako „mozek“, který později zpracuje obrázek, který mu předáte.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Proč vytváříme novou instanci pokaždé? Izolace. Čerstvý engine zaručuje, že žádný zbylý stav z předchozího běhu neovlivní aktuální rozpoznávání, což je klíčové při zpracování mnoha souborů najednou.

### Krok 3: Načtení obrázku, který chcete zpracovat

Nyní **načteme obrázek pro OCR**. Metoda `setImageFromFile` přijímá cestu k libovolnému rastrovému obrázku; ukážeme si PNG nazvaný `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Pokud soubor není nalezen, `SimpleOCR` vyhodí jasnou výjimku `FileNotFoundError`. Můžete ji zachytit a zobrazit přátelskou chybovou zprávu:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Krok 4: Povolení automatické detekce jazyka

Většina moderních OCR engineů obsahuje jazykové balíčky. Přenesením `"multilingual"` říkáme engine, aby „ucítil“ text a automaticky vybral správný jazykový model. To je zvláště užitečné, když váš PNG obsahuje směs angličtiny a španělštiny, například.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Pokud jazyk znáte dopředu, můžete místo `"multilingual"` použít konkrétní locale jako `"eng"` nebo `"spa"` pro zrychlení zpracování.

### Krok 5: Spuštění procesu rozpoznávání

Tady se děje těžká práce. `recognize()` prohledá obrázek, provede segmentaci, spustí neuronovou síť a interně vytvoří textový buffer.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Za scénou engine provádí:

- **Předzpracování** (odklonování, binarizace)  
- **Analýzu rozvržení** (detekce sloupců, tabulek)  
- **Klasifikaci znaků** (pomocí modelu hlubokého učení)  

Vše je abstrahováno, proto stačí jen jeden řádek.

### Krok 6: Získání a vytištění rozpoznaného textu

Nakonec získáme výstupní objekt a vytáhneme prostý řetězec. Toto je část, kde skutečně **extrahujete text z obrázku**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Pokud obrázek neobsahuje rozpoznatelné znaky, `text` bude prázdný řetězec. Můžete se proti tomu ochránit:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Extrahování textu z obrázku – Řešení běžných okrajových případů

### Více jazyků v jednom souboru

Když dokument míchá jazyky, nastavení `"multilingual"` obvykle funguje správně. Pokud však zaznamenáte chyby v rozpoznávání, můžete ručně zadat záložní seznam:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Formáty jiné než PNG

I když se zaměřujeme na **rozpoznání textu z PNG**, `SimpleOCR` také podporuje JPEG, BMP a TIFF. Stačí změnit příponu souboru v `setImageFromFile`. U TIFF stacků možná budete muset vybrat konkrétní stránku:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Velké soubory a využití paměti

Pokud zpracováváte gigapixelové skeny, zvažte předzmenšení před OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Zmenšení snižuje zatížení paměti a přitom zachovává dostatek detailů pro přesné rozpoznání.

### Ladění neúspěšných načtení

Někdy obrázek vypadá na pohled v pořádku, ale je poškozený uvnitř. Zapněte podrobný log, abyste viděli, co engine „vidí“:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Kompletní, připravený ke spuštění skript

Níže je celý program, který spojuje všechny části dohromady. Zkopírujte jej do souboru pojmenovaného `ocr_demo.py`, upravte placeholder `YOUR_DIRECTORY` a spusťte `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Spuštěním tohoto skriptu by se měl vypsat prostý textový obsah souboru `mixed_doc.png`. Klidně vyměňte soubor za jakýkoli jiný obrázek — **jak extrahovat text** funguje stejným způsobem.

---

## Závěr

Právě jsme prošli **jak používat OCR** v Pythonu k **extrahování textu z obrázku**, konkrétně se zaměřením na **rozpoznání textu z PNG** aktiv a praktické kroky k **načtení obrázku pro OCR**. Výše uvedený úryvek je samostatné řešení: nainstalujete balíček, předáte mu soubor, povolíte vícejazyčnou detekci, spustíte engine a získáte výsledek.  

Od semene můžete:

- Integrovat skript do webové služby, která přijímá uživatelské nahrávky.  
- Hromadně zpracovat složku PDF převedených na PNG.  
- Přidat post‑processing (např. regex čištění, kontrolu pravopisu) pro zvýšení přesnosti.

Pamatujte, kvalita OCR závisí na ostrosti obrázku, správných jazykových balíčcích a někdy i na mírném předzpracování — tak experimentujte.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}