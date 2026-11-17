---
category: general
date: 2026-03-26
description: Hozzon létre ROI sokszöget az OCR futtatásához a kiválasztott területen.
  Tanulja meg, hogyan definiáljon több régiót, regisztrálja őket, és szöveget nyerjen
  ki egy Python OCR motorral.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: hu
og_description: Hozzon létre ROI-polygonot, és futtassa az OCR-t a kiválasztott területen
  egy Python motorral. Teljes kód, magyarázatok és tippek benne.
og_title: ROI poligon létrehozása – Gyors OCR a kiválasztott területen
tags:
- OCR
- Python
- Image Processing
title: ROI-polygon létrehozása – Lépésről‑lépésre útmutató a kiválasztott területen
  végzett OCR-hez
url: /hu/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI sokszög létrehozása – Teljes útmutató a kiválasztott terület OCR-hez

Szükséged volt már **ROI sokszög** létrehozására, hogy csak a kép azon részén végezz OCR-t, ami tényleg érdekel? Lehet, hogy számlákat szkennelsz, és csak az összeg számít, vagy egy űrlapon csak az aláírás mezőt kell beolvasni. Ilyenkor az **ocr a kiválasztott területen** időt takarít meg és növeli a pontosságot.  

Ebben az útmutatóban lépésről‑lépésre végigvezetünk mindenen: két sokszög definiálásától, azok OCR‑motorba regisztrálásán át, egészen a felismert szöveg egyetlen tiszta hívásban történő kinyeréséig. A végére egy futtatható szkriptet és egy szilárd megértést kapsz arról, miért fontos a érdeklődési területekre (ROI) fókuszálni.

## Mit fogsz megtanulni

- Hogyan **hozz létre ROI sokszög** objektumokat egy tipikus OCR‑könyvtár segítségével.
- A különbség egyetlen régió és több régió definiálása között.
- Hogyan regisztráld ezeket a régiókat a motorban, hogy a `ocr on selected area` végrehajtásra kerüljön.
- Várható kimenet és a gyakori hibák (pl. átfedő ROI‑k, üres eredmények) hibaelhárítása.

### Előfeltételek

- Python 3.8+ telepítve.
- Egy OCR‑könyvtár, amely biztosítja a `Polygon`, `Point` és `add_region_of_interest` metódusokat (a példa egy fiktív `ocr` modult használ; cseréld le a saját SDK‑odra, például a Tesseract‑Python csomagra vagy az EasyOCR‑ra).
- Egy mintakép fájl (`sample.png`), amely a lent látható koordinátákon belül szöveget tartalmaz.

> **Pro tipp:** Ha valós könyvtárat használsz, győződj meg róla, hogy a kép ugyanabban a koordináta‑rendszerben van betöltve (origó a bal‑felső sarok, X jobbra növekszik, Y lefelé növekszik).  

---  

## 1. lépés: Importáld az OCR modult és töltsd be a képet  

Először hozd be az OCR csomagot, majd olvasd be a feldolgozni kívánt képet.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Miért fontos:* A motornak szüksége van a kép adataira, mielőtt **ROI sokszöget** csatolnál. Néhány könyvtár később is engedélyezi a kép átadását, de a korai inicializálás tisztább munkafolyamatot eredményez.

## 2. lépés: Definiáld az első ROI sokszöget  

Most létrehozzuk az első érdeklődési területet. Gondolj rá úgy, mint egy téglalapra, amely a táblázat fejlécét keretezi.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Magyarázat:*  
- `ocr.Point(x, y)` pixel koordinátákat használ.  
- A pontok listája óramutató járásával megegyező sorrendben van, ahogy a legtöbb motor elvárja.  
- Tetszőleges számú pontot hozzáadhatsz, hogy szabálytalan alakzatot hozz létre; egy téglalap csak egy speciális eset.

## 3. lépés: További ROI sokszögek definiálása (opcionális)  

Nem kell megállni egynél. Itt egy második sokszög, amely a lap alján lévő aláírás mezőt ragadja meg.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Miért érdemes több területet hozzáadni?* A **ocr on selected area** több zónára egyszerre futtatva lehetővé teszi, hogy különböző adatdarabokat egyetlen átfutásban nyerj ki, ami sokkal gyorsabb, mint minden szeletet külön-külön kivágni és feldolgozni.

## 4. lépés: Regisztráld a ROI‑kat az OCR motorban  

Miután a sokszögek készen állnak, mondd meg a motornak, mely területeket vizsgálja.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Fontos megjegyzés:* Néhány SDK‑nál a `clear_regions()` metódus meghívása szükséges az új régiók hozzáadása előtt, ha ugyanazt a motort új képre használod.

## 5. lépés: Futtasd az OCR‑t és szerezd meg a szöveget  

Végül indítsd el a felismerést. A motor csak a most hozzáadott sokszögek belsejét fogja átnézni.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Várható kimenet** (feltételezve, hogy a `sample.png` tartalmazza az „Invoice Total: $123.45” szöveget az első ROI‑ban és a „Signature: John Doe” szöveget a másodikban):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Ha a kimenet üres, ellenőrizd, hogy a koordináták ténylegesen szöveget érintenek-e, és hogy a kép felbontása megfelel‑e a koordináta‑rendszernek.

## Szélső esetek és gyakori hibák  

| Helyzet                                 | Mire figyelj                                   | Javítás / megoldás                              |
|----------------------------------------|------------------------------------------------|-------------------------------------------------|
| **Átfedő ROI‑k**                        | A szöveg többször is visszatérhet.             | Tartsd a sokszögeket diszjunkt módon, vagy deduplikáld a kimenetet. |
| **ROI a kép határain kívül**            | A motor hibát dobhat vagy semmit sem ad vissza. | Korládozd a koordinátákat `0 ≤ x < szélesség`, `0 ≤ y < magasság` tartományra. |
| **Nagyon kicsi ROI**                    | Az OCR pontossága csökken a kevés pixel miatt. | Növeld a sokszöget néhány pixellel, vagy előbb nagyítsd fel a képet. |
| **Nem téglalap alakú forma**            | Egyes motorok csak konvex sokszögeket támogatnak. | Bontsd a komplex alakzatot több konvex ROI‑ra. |
| **Kép méretének változása**             | A keménykódolt koordináták érvénytelenek lesznek. | Számítsd ki a ROI koordinátákat a kép méretéhez viszonyítva (pl. százalékban). |

## Teljes működő példa  

Az alábbiakban a teljes szkriptet találod, amelyet egyszerűen másolj‑be és futtass (cseréld le az `ocr`‑t a saját könyvtáradra).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Futtasd a `python ocr_roi_example.py` paranccsal, és a két definiált zónából kinyert karakterláncokat kell látnod.

## Következő lépések  

- **Dinamikus ROI generálás:** A koordináták kézi megadása helyett használj képfeldolgozást (pl. OpenCV kontúr‑detektálás) a táblázatok vagy mezők automatikus megtalálásához.  
- **Utófeldolgozás:** Távolítsd el a felesleges szóközöket, alkalmazz reguláris kifejezéseket, vagy konvertáld a számokat a megfelelő adattípusokra.  
- **Kötegelt feldolgozás:** Egy mappában lévő képeken iterálj, és ha a layout állandó, újrahasználhatod ugyanazokat a ROI definíciókat.  

Ha érdekel a **ocr on selected area** összetettebb dokumentumoknál – gondolj többoldalas PDF‑ekre vagy beolvasott űrlapokra – nézz utána azoknak a könyvtáraknak, amelyek oldalankénti ROI regisztrációt támogatnak.  

---  

### Vizuális áttekintés  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="ROI sokszög példa, amely két kiválasztott területet mutat"}  

A diagram azt szemlélteti, hogyan helyezkednek el a két téglalap (kék és zöld) a háttérképen, és pontosan mely részeket fogja olvasni az OCR motor.

---  

## Összegzés  

Most **ROI sokszögeket** hoztunk létre, regisztráltuk őket egy OCR motorba, és egy tiszta, reprodukálható szkriptben hajtottuk végre a `ocr on selected area` műveletet. Azáltal, hogy a motort csak a számodra fontos zónákra korlátozod, csökkented a feldolgozási időt, javítod a pontosságot, és egyszerűbbé teszed a későbbi adatkezelést.  

Próbáld ki a saját képeiddel – módosítsd a koordinátákat, adj hozzá további sokszögeket, vagy kössd össze a kimenetet egy adatbázissal. A lehetőségek korlátlanok, ha már elsajátítottad a régió‑alapú OCR‑t.  

Van kérdésed vagy szeretnél egy izgalmas felhasználási esetet megosztani? Írj egy kommentet alább, és jó kódolást kívánok!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}