---
category: general
date: 2026-06-25
description: Szerezd meg gyorsan az OCR által támogatott karaktereket az aocr könyvtár
  segítségével. Tanuld meg, hogyan listázhatod az OCR karaktereket, állíthatsz be
  nyelveket, és hibakeresheted az OCR motorodat Pythonban.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: hu
og_description: Szerezze be az OCR által támogatott karaktereket az aocr-rel. Ez az
  útmutató megmutatja, hogyan listázhatja az OCR karaktereket, választhat nyelveket,
  és kezelheti a szélsőséges eseteket Pythonban.
og_title: OCR által támogatott karakterek lekérése Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR által támogatott karakterek lekérése Pythonban – Teljes útmutató
url: /hu/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR által támogatott karakterek lekérése Pythonban – Teljes útmutató

Gondoltad már, hogyan **kaphatod meg az OCR által támogatott karaktereket** egy adott nyelvre, amikor egy OCR motorral kísérletezel? Nem vagy egyedül. Legyen szó nyugtavásárló szkenner vagy többnyelvű dokumentumfeldolgozó építéséről, a motor által felismert glifek pontos ismerete igazi életmentő. Ebben a tutorialban végigvezetünk a teljes folyamaton – a könyvtár telepítése, a nyelv beállítása, majd a karakterek listázása – hogy percek alatt hibakeresni és finomhangolni tudd az OCR pipeline‑odat.

A **aocr** könyvtárat használjuk, egy könnyű Python OCR motort, amely egyszerűvé teszi a nyelvi képességek lekérdezését. A végére képes leszel **listázni az OCR karaktereket**, váltani a **támogatott OCR nyelvek** között, és még a lefedettségi hiányokat is időben észrevenni, mielőtt a termelésben problémát okoznának.

---

## Prerequisites

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel a következőkkel:

* Python 3.8 vagy újabb (az aocr csomag már nem támogatja a 3.7‑et)
* Terminál vagy parancssor internetkapcsolattal
* Alapvető Python szkriptek ismerete (ha már írtál `print()`‑t, készen állsz)

Nincsenek nehéz külső függőségek – csak a `aocr` pip csomag.

---

## Install the aocr Library (OCR Engine Python)

Az első dolog, amire szükséged van, egy működő **OCR engine Python** telepítés. Az aocr csomag a PyPI‑n elérhető, így egyetlen pip parancs elég:

```bash
pip install aocr
```

Ha virtuális környezetet használsz (erősen ajánlott), előbb aktiváld azt:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Rögzítsd a verziót (`pip install aocr==1.2.4`), hogy később elkerüld a váratlan API változásokat.

---

## Choose a Language (Supported OCR Languages)

Az aocr néhány beépített nyelvi csomaggal érkezik. Minden csomag meghatározza azt a Unicode kódpontkészletet, amelyet a motor fel tud ismerni. Ezek lekérdezéséhez állítsd be a `language` attribútumot a motor példányán.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

A `aocr.Language.ENGLISH` helyett bármely más enum értéket (`FRENCH`, `GERMAN`, stb.) használhatsz. Ha olyan nyelvet próbálsz beállítani, amely nincs a csomagban, az aocr `ValueError`‑t dob. Ezért érdemes először ellenőrizni a **támogatott OCR nyelvek** listáját:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Retrieve the Set of Characters (Get OCR Supported Characters)

Most jön a tutorial szíve: ténylegesen **get OCR supported characters**. A motor egy kényelmes `get_supported_characters()` metódust kínál, amely egyetlen karakteres stringek listáját adja vissza.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

A háttérben az aocr egy a nyelvi csomaggal együtt szállított JSON fájlt olvas be, és minden Unicode kódpontot Python stringgé konvertál. Az eredmény determinisztikus, vagyis minden egyes futtatásnál ugyanazt a listát kapod ugyanarról a nyelvverzióról.

---

## Show How Many Characters Are Supported

A darabszám ismerete gyorsan segít felmérni a lefedettség mértékét. Angol esetén általában néhány ezer karaktert látsz (beleértve az írásjeleket és számjegyeket is).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

A `len()` hívás O(1), mivel a Python a lista hosszát belsőleg tárolja, így nagy ábécék esetén sincs teljesítménybeli hátrány.

---

## Preview the First 100 Supported Characters

Egy gyors vizuális ellenőrzés megmutathatja, hogy a motor tartalmazza-e a szükséges szimbólumokat (például az eurójelet vagy az okos idézőjeleket). Írjuk ki az első száz karaktert:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

A `join` művelet a szeletet egyetlen stringgé fűzi össze, ami olvashatóbb, mint egy Python lista kiírása.

---

## Full Script – All Steps in One Place

Az alábbiakban a teljes, futtatható példát láthatod, amely mindent összekapcsol. Mentsd el `list_supported_chars.py` néven, majd futtasd `python list_supported_chars.py`‑vel a terminálodban.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Várható kimenet (rövidítve):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

A pontos darabszám a aocr verziójától függően kissé eltérhet, de mindig egy hosszú ábécét és a gyakori írásjeleket fogod látni.

---

## Handling Edge Cases

### What if the language pack is missing?

Ha olyan nyelvet kérsz, amely nincs a csomagban, a `aocr.Language` nem tartalmazza az enumot, és `AttributeError`‑t kapsz. Ezt egyszerű ellenőrzéssel elkerülheted:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Empty character list

Néhány ritka nyelv esetén előfordulhat, hogy üres listát ad vissza, ha az alapul szolgáló tanító adat hiányos. Ilyenkor visszaállhatsz egy alapértelmezett nyelvre (pl. angolra), vagy figyelmeztetést dobhatod:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode normalization

A lista tartalmazhat kombinált karaktereket (pl. „é” mint `e` + ékezet). Ha a downstream feldolgozásod előre összeállított glifeket vár, futtass egy normalizációs lépést:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro Tips for Real‑World Projects

* **Cache the character list** – Ha több ezer képet dolgozol fel, a `get_supported_characters()` minden iterációban való meghívása felesleges overheadet jelent. Tárold a listát modul‑szintű változóban vagy sorosítsd JSON‑ba későbbi újrahasználathoz.
* **Cross‑language validation** – Ha egy alkalmazásban több nyelvet támogatsz, vágd össze a karakterkészleteket, hogy megtaláld a közös részhalmazt. Ez segít konzisztens UI elemeket tervezni a különböző locale‑ok között.
* **Debugging OCR failures** – Ha a motor hibásan osztályoz egy glifet, hasonlítsd össze a problémás karaktert a `list_supported_chars` kimenetével. Ha hiányzik, egy lefedettségi részről van szó, amelyhez egyedi tréningre lehet szükség.
* **Combine with custom fonts** – Az aocr tiszteletben tartja a Unicode tartományt, de a megjelenítés minősége betűtípustól függ. Teszteld a támogatott karaktereket a pontosan ugyanazzal a betűtípussal, amit a termelésben használsz, hogy elkerüld a meglepetéseket.

---

## Frequently Asked Questions

**Q: Does this work with aocr version 2.x?**  
A: Igen, a `get_supported_characters()` metódus stabil mind az 1.x, mind a 2.x verziókban. Az egyetlen változás, hogy a nyelvi enumok átkerültek a `aocr.languages`‑ba.

**Q: Can I get the Unicode code point for each character?**  
A: Természetesen. Használd az `ord(ch)`‑t egy listakomprehenszióban:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: What about right‑to‑left scripts like Arabic?**  
A: Az aocr tartalmaz egy `ARABIC` enumot. A karakterlista arab glifeket fog tartalmazni, de a downstream UI‑ban engedélyezned kell a RTL megjelenítést.

---

## Conclusion

Most már tudod, **hogyan kaphatod meg az OCR által támogatott karaktereket** a Python aocr könyvtár segítségével, hogyan válthatsz a **támogatott OCR nyelvek** között, és miért **fontos a karakterek listázása** a robusztus szövegfelismerő pipeline‑okhoz. A teljes szkript és a fenti tippek birtokában gyorsan ellenőrizheted a nyelvi lefedettséget, hibakeresheted a hiányzó glifeket, és intelligensebb OCR‑alapú alkalmazásokat építhetsz.

Készen állsz a következő lépésre? Próbáld ki a karakterlistát egy egyedi szólista szűrővel, vagy kísérletezz egy másik OCR motorral (Tesseract, EasyOCR) és hasonlítsd össze az eredményeket. Minél többet fedezel fel, annál jobb lesz az OCR megoldásod.

Boldog kódolást, és legyenek a karakterkészleteid mindig teljesek!

## What Should You Learn Next?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra építenek. Minden forrás tartalmaz teljesen működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}