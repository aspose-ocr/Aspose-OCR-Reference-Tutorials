---
category: general
date: 2026-03-18
description: Javítsd gyorsan az OCR hibákat Pythonban. Tanuld meg, hogyan tisztítsd
  meg az OCR-t, hogyan tisztítsd meg az OCR‑szöveget, cseréld a nullát O‑ra, és alkalmazd
  a Python OCR utófeldolgozást.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: hu
og_description: Javítsd gyorsan az OCR hibákat Pythonban. Tanuld meg, hogyan tisztítsd
  meg az OCR-t, cseréld a nullát O-ra, és használd a Python OCR utófeldolgozást egyetlen
  útmutatóban.
og_title: OCR hibák javítása Pythonban – OCR szöveg tisztítási útmutató
tags:
- OCR
- Python
- Text Cleaning
title: OCR hibák javítása Pythonban – OCR szöveg tisztítási útmutató
url: /hu/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR hibák javítása Pythonban – OCR szöveg tisztítási útmutató

Volt már, hogy egy beolvasott számlát nézve azt gondoltad, *„Hogyan javítsam ki az OCR hibákat, mielőtt az adatbázisba tölteném?”* Nem vagy egyedül. A dokumentumautomatizálás világában egyetlen félreolvasott karakter is tönkreteheti az egész folyamatot, ezért elengedhetetlen megtanulni, **hogyan tisztítsuk meg az OCR** kimenetet.

Ebben az útmutatóban egy gyakorlati, vég‑től‑végig tartó módszert mutatunk be az **OCR hibák javítására**, egy apró utófeldolgozó segítségével, amely a “0” számjegyet az “O” betűre cseréli – ez gyakori probléma a termékkódoknál. A végére képes leszel a megoldást bármely Python OCR munkafolyamatba beilleszteni, és tisztább, megbízhatóbb szöveget kapni.

> **Mit kapsz:** egy teljes, futtatható Python szkript, magyarázatok arra, hogy miért fontos minden sor, tippek a logika kiterjesztéséhez, és egy gyors ellenőrzés a várt kimenetről.

## Előfeltételek — Amire szükséged van a kezdéshez

- Python 3.8 vagy újabb (a szintaxis minden friss kiadáson működik).  
- Egy alap OCR könyvtár (pl. Tesseract a `pytesseract`-on keresztül), amely nyers karakterláncokat ad vissza.  
- Alapvető ismeretek a függvényekről és objektumokról Pythonban.  

Ha már van egy OCR lépésed, amely karakterláncot ad vissza, akkor készen állsz—nem szükséges további telepítés a post‑feldolgozáshoz.

## 1. lépés: Minimalista AI‑szerű Wrapper beállítása (Miért van rá szükség)

Sok projektben az OCR motor egy nagyobb “AI” osztályon belül él, amely a előfeldolgozást, az inferenciát és a post‑feldolgozást kezeli. Az önálló példa érdekében létrehozunk egy apró `AIProcessor` osztályt, amely ezt a mintát utánozza. Ez megkönnyíti a kód beillesztését egy meglévő kódbázisba anélkül, hogy bármit újra kellene írni.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Miért fontos:** a post‑processor elkülönítése az OCR motorból tiszteletben tartja az egyetlen felelősség elvét, és lehetővé teszi a tisztítási logika cseréjét anélkül, hogy az OCR kódot módosítanád.

## 2. lépés: Írd meg a függvényt, amely **javítja az OCR hibákat**

Most elkészítjük az útmutató központi részét: egy függvényt, amely **javítja az OCR hibákat** a “0” számjegy “O” betűre cserélésével. Ez a minta lefedi a termékkódokat, sorozatszámokat és bármely alfanumerikus azonosítót, ahol az OCR motor gyakran összekeveri a két karaktert.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Miért cseréljük a 0‑t O‑ra:** Sok betűtípusban a nulla és a nagy O azonosnak tűnik, így az OCR gyakran a rosszat választja. Ha korán javítjuk, a downstream validáció (például regex ellenőrzések) a várt módon működik.

## 3. lépés: A post‑processor csatolása az AI példányhoz

Miután a wrapper és a tisztító függvény készen áll, összekapcsoljuk őket. Ez tükrözi, hogyan regisztrálnál egy egyedi post‑processzort egy éles pipeline-ban.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

Ha valaha **hogyan tisztítsuk meg az OCR** kimenetet egy másik nyelv vagy adatformátum esetén, csak írj egy újabb függvényt, és hívd meg újra a `set_post_processor`-t – nem kell a pipeline többi részét módosítani.

## 4. lépés: Nyers OCR szöveg betáplálása és a tisztított eredmény lekérése

Szimuláljunk egy nyers OCR karakterláncot, amely a rettegett “0” karaktert tartalmazza egy termékkódban. Valós esetben a helyőrzőt a `pytesseract.image_to_string(image)` vagy hasonló hívással cserélnéd.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**Várt kimenet**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

Vedd észre, hogy a nullák nagy O‑kká változtak, így egy olyan karakterláncot kapunk, amely a legtöbb készletkezelő rendszer elvárt formátumának megfelel.

## 5. lépés: A logika kibővítése – Valós világ variációk

Az egyszerű fenti csere egy szűk esetet old meg, de a gyártásban más sajátosságokkal is találkozhatsz:

| Gyakori hiba | OCR példa | Kívánt javítás | Hozzáadás módja |
|--------------|-----------|----------------|-----------------|
| “1” olvasva “I”‑ként | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” olvasva “S”‑ként | `S9` | `59` | `text = text.replace('S', '5')` |
| Felesleges szóköz | `  ABC  ` | `ABC` | `text = text.strip()` |
| Kevert kis‑nagy betű zavar | `oRder` | `Order` | `text.title()` |

Kiterjesztheted a `correct_ocr_errors` függvényt bármelyik ilyen szabállyal. Csak ügyelj arra, hogy minden átalakítás **idempotens** legyen (kétszer futtatva ne változzon az eredmény), hogy elkerüld a véletlen adatkorruptiót.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**Pro tipp:** Ha van egy ismert katalógusod az érvényes kódokról, fontold meg a tisztított karakterlánc ellenőrzését regex vagy keresőtábla segítségével. Ez a plusz lépés elkapja a maradék OCR hibákat, amelyeket az egyszerű karaktercserék nem észlelnek.

## 6. lépés: Integrálás egy valós OCR motorral (Opcionális)

Az alábbi gyors illusztráció bemutatja, hogyan illesztheted be a post‑processzort egy valós OCR folyamatba a `pytesseract` használatával. Ez a rész opcionális, de bemutatja a vég‑től‑végig pipeline-t.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Megjegyzés:** A `pytesseract` azt várja, hogy a Tesseract OCR telepítve legyen a rendszereden. A fenti kódrészlet Windows, macOS és Linux rendszereken is működik, amíg a bináris a PATH‑ban van.

## 7. lépés: Az eredmények programozott ellenőrzése

Amikor nagy kötegelt feladatokat automatizálsz, hasznos ellenőrizni, hogy a tisztítási lépés a várt módon működött-e. Egy gyors egységteszt órákat takaríthat meg a későbbi hibakeresésben.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

A teszt futtatása megerősíti, hogy a függvény **konzisztensen javítja az OCR hibákat**, még akkor is, ha extra szóközök csúsznak be.

## Képi illusztráció

Az alábbiakban egy vizuális vázlat látható a pipeline-ról (a fő kulcsszó az alt szövegben jelenik meg SEO céljából).

![OCR hibák javítása folyamatábra – mutatja a nyers OCR-t, amely egy post‑processzorba kerül, amely a nullát O‑ra cseréli]()

## Összegzés – Amit elértünk

Végigvettünk egy teljes, futtatható példát, amely megmutatja, **hogyan tisztítsuk meg az OCR** kimenetet Pythonban, különösen hogyan **cseréljük a nullát O‑ra** és **javítsuk ki az OCR hibákat** egy moduláris post‑processzor segítségével. A tisztítási logika az OCR motorból való szétválasztásával rugalmasságot, tesztelhetőséget és egy világos helyet kapsz a jövőbeni szabályok hozzáadásához, például *hogyan tisztítsuk meg az OCR*-t más karakterzavarok esetén.

Készen állsz a következő lépésre? Próbálj meg egy regex validátort hozzáadni a termékkódokhoz, kísérletezz fuzzy egyezéssel zajos szövegekhez, vagy fedezd fel a `ocrmypdf`-hez hasonló teljes funkcionalitású könyvtárat, amely már tartalmaz post‑processing hook-okat. A bemutatott minta jól skálázható, legyen szó néhány számláról vagy millió beolvasott dokumentumról.

---

*Boldog kódolást, és legyenek az OCR pipeline-jaid hibamentesek!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}