---
category: general
date: 2026-06-06
description: 'OCR karakterkészlet útmutató: tanulja meg, hogyan használja az OCR motorját
  a latin és cirill írásrendszerek támogatott karaktereinek listázásához teljes Python
  példákkal.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: hu
og_description: 'OCR karakterkészlet útmutató: fedezze fel, hogyan használhatja az
  OCR motorját Pythonban a különböző írásrendszerek támogatott karaktereinek listázásához,
  kóddal és tippekkel együtt.'
og_title: OCR karakterkészlet – OCR motor lekérése és használata
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: OCR karakterkészlet – OCR motor lekérése és használata Pythonban
url: /hu/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR karakterkészlet – OCR motor lekérdezése és használata Pythonban

Szeretnéd tudni, hogy a **ocr karakterkészlet** milyen karaktereket támogat a könyvtárad? Ebben az útmutatóban megmutatjuk, hogyan **használhatod az OCR motort** a támogatott karakterek lekérdezésére különböző írásrendszerekhez, és miért fontos ez a valós projektekben.

Ha már valaha üres képernyőre bámultál, és azon tűnődtél, miért nem jelennek meg bizonyos betűk az OCR feldolgozás után, nem vagy egyedül. A válasz gyakran a motor által ismert karakterkészletben rejlik. A végére a következőket fogod tudni:

* Listázni minden karaktert, amelyet egy OCR motor fel tud ismerni egy adott írásrendszerhez.  
* Kezelni azokat az eseteket, amikor egy írásrendszer nem támogatott.  
* A karakterkészlet információt beépíteni a további validációba vagy UI logikába.

Nincs varázslatos fekete doboz trükk – csak tiszta Python, néhány kódsor, és egy kis magyarázat.

---

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy:

* Python 3.8+ telepítve van (a kód f‑stringeket használ).  
* Az OCR könyvtár, amely biztosítja a `ocr.OcrEngine`‑t – ebben a példában feltételezzük, hogy a `ocr` nevű csomag már telepítve van a `pip install ocr-lib` paranccsal.  
* Alapvető ismereted van a Python import rendszeréről és a kiírásról.

Ha hiányzik a könyvtár, futtasd:

```bash
pip install ocr-lib
```

Ennyi – nincs szükség extra binárisokra vagy natív függőségekre a karakterkészlet lekérdezéséhez, amelyet végrehajtunk.

---

## 1. lépés: Az OCR motor példányának inicializálása

Az motor objektum létrehozása az első dolog, amit meg kell tenned, amikor **használod az OCR motort**. Gondolj rá úgy, mint egy szkenner bekapcsolására; nélküle nem tehetsz fel kérdéseket.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Az `OcrEngine` osztály egy könnyűsúlyú burkoló a mögöttes felismerő motor körül. Nem indít nehéz feldolgozást, amíg valamit nem kérsz, így az indítási költség elhanyagolható.

> **Pro tipp:** Ha az alkalmazásod sok motor példányt hoz létre, használj egyetlen példányt újra. Így memória takarítasz meg és csökkented az inicializációs késleltetést.

---

## 2. lépés: OCR karakterkészlet lekérdezése egy adott írásrendszerhez

Most, hogy van egy motorunk, megkérdezhetjük, mely karaktereket ismer egy adott írásrendszerhez. A `get_supported_characters(script_name)` metódus egy Python `list`‑et ad vissza Unicode karakterekkel.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

A fenti kódrészlet futtatása valami ilyesmit nyomtat:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

A pontos kimenet az OCR könyvtár verziójától függ, de mindig egy lapos karakterlistát kapsz. Ha nagy- és kisbetűkre is szükséged van, egyszerűen kérd le a `"Latin"` írásrendszert, majd alkalmazd a `.lower()`‑t minden elemre, vagy kérdezd le a `"Latin‑lower"` írásrendszert, ha a könyvtár megkülönbözteti őket.

### Miért fontos ez?

Ha egy olyan képet adsz az OCR-nek, amely szokatlan diakritikus jeleket tartalmaz (pl. „ñ” vagy „ø”), a motor csendben helyettesítheti őket egy helykitöltővel vagy teljesen eldobhatja őket. A **ocr karakterkészlet** előzetes ismerete lehetővé teszi a bemenet elővalidálását, a felhasználók figyelmeztetését, vagy egy másik motor használatát.

---

## 3. lépés: Karakterek lekérdezése egy másik írásrendszerhez – Cirill példa

Ugyanaz a metódus minden olyan írásrendszerhez működik, amelyet a motor támogat. Nézzük meg, mi történik a cirill esetén.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Tipikus kimenet:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Ha a motor **nem** támogatja a kért írásrendszert, általában `ValueError`‑t dob (vagy egy üres listát ad vissza a megvalósítástól függően). Védd le ezt a helyzetet.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

---

## 4. lépés: OCR karakterkészlet vizualizálása (opcionális)

Néha egy gyors vizuális ábrázolás segít, különösen, ha a stakeholder‑eknek kell bemutatni, mely karakterek vannak lefedve. Az alábbi egyszerű példa a `matplotlib`‑ot használja egy karakterrács megjelenítésére.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Kép alternatív szöveg:** ![OCR karakterkészlet diagram](ocr_character_set.png){alt="OCR karakterkészlet áttekintése"}

A diagram nem kötelező a megoldáshoz, de bemutatja, hogyan használhatod a **OCR motor** metaadatait a tiszta kiírás mellett is.

---

## 5. lépés: A karakterkészlet integrálása valós munkafolyamatokba

Most, hogy le tudjuk kérni a **ocr karakterkészletet**, nézzünk egy gyakorlati szituációt: az OCR kimenet validálása adatbázisba mentés előtt.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Ez a minta megakadályozza, hogy szemét adatok kerüljenek a downstream csővezetékekbe – gyakori fájdalompont a többnyelvű dokumentumok kezelésekor.

---

## Gyakori hibák és széljegyek

| Hiba | Miért fordul elő | Hogyan kerüld el |
|------|------------------|------------------|
| **Írásrendszer‑név elütés** (pl. `"Cyrillic "` szóközzel a végén) | A motor a karakterláncot szó szerint kezeli, és nem találja az írásrendszert. | Távolítsd el a felesleges szóközöket: `script.strip()` a `get_supported_characters` hívása előtt. |
| **Üres karakterlista** | Egyes motorok kinyilvánítanak egy írásrendszert, de még nem töltötték be a nyelvi modellt. | Hívd meg az `engine.load_language_model(script)`‑t, ha a könyvtár ilyen metódust biztosít, vagy ellenőrizd, hogy a modellfájlok jelen vannak. |
| **Unicode normalizációs problémák** | Olyan karakterek, mint a “é”, megjelenhetnek összeállított (`\u00E9`) vagy szétbontott (`e\u0301`) formában. | Normalizáld a stringeket a `unicodedata.normalize('NFC', text)`‑vel a validálás előtt. |
| **Teljesítmény nagy írásrendszerek esetén** (pl. kínai) | Több ezer karakter lekérdezése lassú lehet. | Cache-eld az eredményt az első hívás után; a legtöbb alkalmazásnak csak egyszer kell a listára. |

---

## Teljes működő példa

Az alábbi egyetlen szkript mindent egyben tartalmaz, amit egyszerűen másolj és futtass:



## Mi legyen a következő tanulnivalód?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}