---
category: general
date: 2026-06-22
description: Végezzen OCR-t egy képen Pythonban néhány sor kóddal. Tanulja meg, hogyan
  töltsön be képet OCR-hez, hogyan ismerje fel a szöveget PNG-ből, és hogyan használja
  hatékonyan az OCR-motort.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: hu
og_description: Végezzen gyors OCR-t képen Python segítségével. Ez az útmutató bemutatja,
  hogyan töltsön be képet OCR-hez, hogyan ismerje fel a szöveget PNG-ből, és hogyan
  használja az OCR-motort magabiztosan.
og_title: OCR végrehajtása képen Pythonban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR végrehajtása képen Pythonban – Teljes útmutató
url: /hu/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása képen Pythonban – Teljes útmutató

Valaha is szükséged volt **OCR végrehajtására képfájlokon**, de már az első kódsornál elakadtál? Nem vagy egyedül. Ebben az útmutatóban pontosan megmutatjuk, hogyan **tölts be képet OCR-hez**, állíts be egy könnyű **OCR motor**-t, és végül **szöveget ismerj fel PNG‑ből** néhány parancs segítségével.

Mindent lefedünk a könyvtár telepítésétől a whitelist finomhangolásáig, hogy csak a számjegyek és nagybetűk maradjanak a felismerésben. A végére egy azonnal futtatható szkriptet kapsz, amelyet bármely projektbe beilleszthetsz – semmi rejtély, semmi felesleges.

## Mit fogsz megtanulni

- Hogyan **használj OCR motort** programozottan Pythonban.  
- A pontos lépések a **kép betöltéséhez OCR-hez** egy helyi mappából.  
- Miért és hogyan korlátozd a felismerést egy egyedi karakterkészletre.  
- Hogyan **szöveget ismerj fel PNG‑ből**, és kezeld biztonságosan az eredményt.  

**Előfeltételek:** Python 3.7+ telepítve, egy kényelmesen használható terminál, és egy kép (pl. `serial-number.png`), amelyet be szeretnél olvasni. Korábbi OCR tapasztalat nem szükséges.

---

## OCR végrehajtása képen – Az OCR motor inicializálása

Az első dolog, amit tenned kell, egy OCR motor példányának létrehozása. Gondolj a motorra úgy, mint egy agyra, amely a pixeleket elemzi és karakterekké alakítja.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Miért fontos:* Motor nélkül nincs semmi, ami feldolgozná a képet. Az `OcrEngine` osztály egyetlen objektumba csomagolja a nehéz feladatokat – előfeldolgozás, szegmentálás és karakterosztályozás –, amelyet újra felhasználhatsz.

---

## Kép betöltése OCR-hez – PNG fájl megadása

Miután a motor létezik, be kell táplálnod a beolvasni kívánt képet. A könyvtár egy `ImageStream` objektumot vár, amelyet közvetlenül egy fájlútról hozhatsz létre.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tipp:* Tartsd a képet magas kontrasztú formátumban (fekete szöveg fehér háttéren), és kerüld a tömörítési artefaktusokat; ezek megzavarhatják az OCR algoritmust.

---

## Karakterek korlátozása – Számjegyek és nagybetűk whitelistje

Gyakran csak egy karakterhalmaz érdekel – például egy sorozatszám, amely csak A‑Z és 0‑9 karaktereket tartalmaz. A whitelist beállításával azt mondod a motornak, hogy hagyja figyelmen kívül a többit, ami drámaian javítja a pontosságot.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Mi történik a háttérben?* A motor egy szűrőt épít, amely a végső osztályozási szakasz előtt eldobja az összes olyan glifet, amely nincs a whitelistben. Ez különösen hasznos, ha a kép zajt vagy díszítő szöveget tartalmaz, amire nincs szükséged.

---

## Szöveg felismerése PNG‑ből – OCR folyamat futtatása

Miután a motor előkészített és a kép betöltött, végre **végrehajthatod az OCR‑t a képen**. A `recognize()` hívás lefuttatja a teljes folyamatot és egy eredményobjektumot ad vissza.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Ha érdekel a teljesítmény, a metódus általában néhány száz milliszekundum alatt befejeződik egy 300 × 200 px PNG‑n egy modern laptopon.

---

## Kimenet és ellenőrzés – A felismert szöveg lekérése

Az utolsó lépés a tiszta szöveg kinyerése az eredményobjektumból. Minden, ami nem egyezett a whitelistben, automatikusan eldobásra kerül, így egy tiszta karakterláncot kapsz, amely készen áll a további feldolgozásra.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Tipikus kimenet:* `AB12C3D4E5` (feltételezve, hogy a kép pontosan ezt a sorozatszámot tartalmazta).  

Ha a kimenet üres vagy torz, ellenőrizd újra a kép minőségét és a whitelistet; gyakori hiba, hogy véletlenül kihagyod a szükséges karaktereket.

---

## Szélsőséges esetek és gyakori buktatók

| Helyzet | Mit ellenőrizz | Javasolt megoldás |
|-----------|---------------|---------------|
| **Fájl nem található** | Útvonal elírás vagy hiányzó fájl | Használd az `os.path.abspath`-t a teljes útvonal ellenőrzéséhez a `set_image` hívása előtt. |
| **Alacsony kontrasztú kép** | Szöveg beleolvad a háttérbe | Alkalmazz egyszerű küszöböt (`Pillow` vagy `OpenCV`) a kép motorhoz való betáplálása előtt. |
| **Váratlan karakterek** | A whitelist túl szigorú | Add hozzá a hiányzó karaktereket a whitelist szöveghez. |
| **Nagy képek** | Lassú felismerés | Méretezd át a képet legfeljebb 1024 px szélességre; az OCR minősége általában magas marad. |

---

## Teljes szkript – Kész a futtatásra

Az alábbiakban a teljes, önálló szkript látható, amely összekapcsolja az összes részt. Mentsd el `ocr_demo.py` néven, cseréld le a `YOUR_DIRECTORY`-t a tényleges mappára, és futtasd a `python ocr_demo.py` parancsot.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Várható konzolkimenet* (ha a PNG `SN12345`‑öt tartalmaz):

```
Recognized text: SN12345
```

---

## Összegzés

Most már pontosan tudod, hogyan **végezz OCR‑t képfájlokon** Pythonban, a **kép betöltésétől OCR‑hez** a **szöveg felismeréséig PNG‑ből**, és végül egy tiszta eredmény kinyeréséig egy testreszabható **OCR motor** segítségével. A megközelítés egyszerű, bővíthető, és a legtöbb sorozatszám‑stílusú beolvasáshoz azonnal működik.

Mi a következő? Próbáld meg a whitelistet kisbetűkre cserélni, kísérletezz különböző képformátumokkal (JPEG, BMP), vagy integráld a szkriptet egy kötegelt feldolgozási csővezetékbe. Ugyanaz a minta – motor → kép → beállítások → felismerés → kimenet – szinte minden OCR feladatra érvényes.

Van kérdésed vagy egy makacs kép, ami nem akar együttműködni? Hagyj egy megjegyzést alább, és jó kódolást!

![Diagram, amely bemutatja az OCR képen végrehajtásának lépéseit Python használatával](https://example.com/ocr-flow.png "Diagram, amely megmutatja, hogyan hajtsunk végre OCR‑t képen egy Python OCR motorral")

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Kép konvertálása szöveggé – OCR végrehajtása képen URL‑ről](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Hogyan használjuk az AspOCR‑t: Kép OCR szűrők előfeldolgozása .NET‑hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hogyan nyerjünk ki szöveget képből téglalapok előkészítésével OCR‑ben](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}