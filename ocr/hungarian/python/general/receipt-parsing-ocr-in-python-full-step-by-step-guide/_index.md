---
category: general
date: 2026-06-28
description: A nyugták feldolgozása OCR-rel Pythonban egyszerű – tanulja meg, hogyan
  lehet kinyerni a nyugta adatokat, betölteni a képet OCR-rel, és megtekinteni egy
  teljes Python OCR példát.
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: hu
og_description: 'Nyugta-feldolgozás OCR Pythonban: tanulja meg, hogyan lehet kinyerni
  a nyugta adatait, betölteni a képet OCR-rel, és percek alatt futtatni egy teljes
  Python OCR példát.'
og_title: Nyugták feldolgozása OCR-rel Pythonban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: Nyugtafeldolgozás OCR Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Számla Feldolgozó OCR Pythonban – Teljes Lépésről‑Lépésre Útmutató

Valaha is elgondolkodtál, hogyan lehet egy homályos szupermarket számlát tiszta, kereshető JSON‑ná alakítani? **Receipt parsing OCR** a megoldás, és nem kell PhD‑nek lenned a számítógépes látás területén, hogy működjön. Ebben az oktatóanyagban egy gyakorlati **python ocr example**‑t mutatunk be, amely betölt egy képet, strukturált szövegfelismerést hajt végre, és szépen formázott JSON‑sztringet ad vissza – tökéletes a könyvelő szoftverekbe vagy elemzési csővezetékekbe való betápláláshoz.

Megválaszoljuk a gyakran felmerülő kérdést is: **how to extract receipt** adatokat megbízhatóan kinyerni, még ha a szken nem is tökéletes. A végére egy újrahasználható szkriptet kapsz, amelyet bármely Python projektbe beilleszthetsz, legyen szó személyes pénzügyi alkalmazásról vagy vállalati szintű költségkövető rendszerről.

## Mit fogsz megtanulni

* Hogyan állítsunk be egy könnyűsúlyú OCR motor-t Pythonban.
* A pontos lépések a **load image OCR** végrehajtásához egy számla fájlhoz.
* Hogyan hívjunk meg egy strukturált felismerési módszert, és alakítsuk az eredményt JSON‑ná.
* Tippek a gyakori szélsőséges esetek kezelésére – elforgatott számlák, alacsony kontraszt és Unicode karakterek.
* Egy teljes, másolás‑beillesztésre kész kódminta, amelyet még ma futtathatsz.

### Előfeltételek

* Python 3.8 vagy újabb telepítve a gépeden.  
* Egy OCR könyvtár, amely biztosítja az `OcrEngine` osztályt és az `Image` segédfüggvényt (számos könyvtár hasonló API‑kat kínál; ebben az útmutatóban egy általános wrapper‑t feltételezünk).  
* Egy számla kép (`receipt.png`) egy olyan mappában, amelyre hivatkozhatsz.  
* Opcionális, de ajánlott: `pip install pillow` a képfeldolgozáshoz és minden további függőség, amelyet az OCR könyvtárad igényel.

Ha valamelyik hiányzik, telepítsd most – semmi gond, a legtöbb csomag esetén egy soros parancs.

---

## Receipt Parsing OCR – 1. lépés: A szükséges modulok telepítése és importálása

Először is, készítsük elő a Python környezetet. Importálni fogjuk a `json`‑t a sorosításhoz és az OCR‑specifikus osztályokat.

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*Miért fontos*: A tetején történő importálás rendezetten tartja a szkriptet, és biztosítja, hogy az OCR motor mindenhol elérhető legyen. Ha elfelejted importálni a `json`‑t, a későbbi `json.dumps` hívás `NameError`‑t fog dobni.

**Pro tipp**: Ha az OCR könyvtárad más névtér alatt található (pl. `easyocr` vagy `pytesseract`), módosítsd ennek megfelelően az import sort. A tutorial többi része változatlan marad.

---

## Hogyan nyerjünk ki számla adatokat – 2. lépés: Az OCR motor példányosítása

Most elindítjuk a motort. Tekintsd a `OcrEngine()`‑t az agynak, amely a számlát olvassa.

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

A legtöbb modern OCR SDK lehetővé teszi itt a nyelvi csomagok vagy detektálási módok beállítását. Egy tipikus számlához az angolt (vagy a számla nyelvét) és egy „structured” módot szeretnél, ha elérhető.

> **Megjegyzés**: Ha a könyvtárad licenckulcsot igényel, add meg argumentumként: `engine = OcrEngine(api_key="YOUR_KEY")`.

## Kép OCR betöltése – 3. lépés: Mutasd a motort a számládra

Miután a motor készen áll, be kell táplálnunk a képfájlt. Itt jön képbe a **load image OCR**.

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*Mi történik*: Az `Image.from_file` beolvassa a PNG‑t (vagy JPG, TIFF, stb.) és olyan formátumba csomagolja, amelyet az OCR motor ért. Ha a számlád PDF, először konvertáld az első oldalt képpé – számos könyvtár biztosít `pdf2image` segédfüggvényt.

**Szélsőséges eset**: Ha a számlát fejjel lefelé szkennelték, még mindig olvasható lesz, ha elforgatod:

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

## Hogyan OCR‑eljük a számlát – 4. lépés: Strukturált szövegfelismerés futtatása

Most történik a varázslat. A motort arra kérjük, hogy strukturált beolvasást végezzen, amely megpróbálja csoportosítani a tételeket, összegeket és dátumokat.

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

Ha az OCR könyvtárad csak egy egyszerű `recognize()` metódust kínál, akkor is manuálisan kinyerheted a mezőket, de a `recognize_structured()` gyakran egy szótárat ad vissza olyan kulcsokkal, mint `items`, `total` és `date`.

## Python OCR példa – 5. lépés: Az eredmény JSON‑ná konvertálása

A nyers eredményobjektum általában egy egyedi osztály. Átalakítása egyszerű Python dict‑é megkönnyíti a sorosítást.

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*Miért `ensure_ascii=False`?* A számlák tartalmazhatnak pénznem szimbólumokat (€, £) vagy ékezetes karaktereket. Ez a flag megőrzi őket a `\u00e9`‑re való escape‑elés helyett.

## Hogyan nyerjünk ki számlát – 6. lépés: A JSON reprezentáció kiírása

Végül kiírjuk (vagy mentjük) a JSON‑t, hogy egy adatbázisba, táblázatba vagy API‑ba továbbíthasd.

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**Várható kimenet** (szép formázott a könnyebb olvashatóságért):

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

Ha üres dict‑ot vagy hiányzó mezőket látsz, ellenőrizd, hogy a számla kép tiszta-e, és hogy az OCR motor a megfelelő nyelvre van-e beállítva.

---

## Pro tippek és gyakori buktatók (Bónusz szekció)

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Homályos vagy alacsony kontrasztú kép** | Az OCR nehezen dolgozik a zajjal | Előfeldolgozás OpenCV‑vel: `cv2.threshold` vagy `cv2.bilateralFilter` |
| **Elforgatott számla** | A motor feltételezi, hogy a szöveg függőleges | Orientáció felismerése `engine.detect_orientation()`‑val vagy manuális forgatás (lásd 3. lépés) |
| **Nem latin karakterek** | Rossz nyelvi csomag | Motor inicializálása `language="spa"`‑val spanyolhoz, stb. |
| **Nagy számlák memóriahibát okoznak** | Az egész kép egyszerre betöltődik | Kivágás a releváns területre: `engine.set_image(image.crop((x, y, w, h)))` |

---

## Mi a következő? A munkafolyamat kibővítése

Most már elsajátítottad a **receipt parsing OCR**‑t Pythonban. Íme néhány ötlet a lendület fenntartásához:

* **Kötegelt feldolgozás** – iterálj egy mappán a számla képekkel, és minden JSON‑t fűzz hozzá egy fő fájlhoz.  
* **Adatbázisba illesztés** – használj `sqlite3` vagy `SQLAlchemy`‑t, hogy minden számlát sorként tárolj.  
* **Gépi tanulás kiegészítés** – add a kinyert tételeket egy kategorizáló modellnek a költségtagoláshoz.  

Ezek mind a lefedett alaplépésekre épülnek, és mindegyik a ugyanazt a **python ocr example** mintát követi: betöltés → felismerés → sorosítás → tárolás.

---

## Következtetés

Ebben az útmutatóban végigvettük a teljes **receipt parsing OCR** munkafolyamatot Pythonban, pontosan bemutatva, **how to extract receipt** információkat, hogyan **load image OCR**, és egy működő **python ocr example**‑t, amelyet ma már futtathatsz. A hat lépés – telepítés, importálás, példányosítás, betöltés, felismerés és sorosítás – követésével most egy szilárd alapod van bármely számlafeldolgozó projekthez.

Nyugodtan kísérletezz: próbálj ki különböző OCR motorokat, finomítsd az előfeldolgozást, vagy adj hozzá hibakezelést a hiányzó mezőkhöz. A határ csak a képzeleted, ha megbízható OCR‑t kombinálsz a Python rugalmasságával. Van kérdésed vagy egy izgalmas változatod a recepthez? Írj egy megjegyzést alább, és folytassuk a beszélgetést.

Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből az Aspose OCR‑rel – Lépésről‑Lépésre Útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hogyan OCR‑eljünk képet – OCR képfelismerés végrehajtása](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Hogyan használjuk az AspOCR‑t: Kép OCR szűrők előfeldolgozása .NET‑hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}