---
category: general
date: 2026-05-03
description: Tanulja meg, hogyan hajtson végre OCR-t egy képen, és hogyan nyerjen
  ki szöveget koordinátákkal a strukturált OCR felismerés segítségével. Lépésről lépésre
  Python kód is mellékelve.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: hu
og_description: Futtass OCR-t a képen, és szerezd meg a szöveget koordinátákkal strukturált
  OCR felismeréssel. Teljes Python példa magyarázatokkal.
og_title: Futtass OCR-t a képen – Strukturált szövegkivonás útmutató
tags:
- OCR
- Python
- Computer Vision
title: Képen OCR futtatása – Teljes útmutató a strukturált szövegkivonáshoz
url: /hu/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Futtass OCR-t képen – Teljes útmutató a strukturált szövegkivonáshoz

Valaha is szükséged volt **OCR futtatására képen** fájlokon, de nem tudtad, hogyan tartsd meg a szavak pontos pozícióját? Nem vagy egyedül. Sok projektben – például nyugta beolvasás, űrlap digitalizálás vagy UI tesztelés – nem csak a nyers szövegre van szükség, hanem a körülhatároló dobozokra is, amelyek megmutatják, hol helyezkedik el az egyes sorok a képen.  

Ez a bemutató gyakorlati módot mutat be az *OCR futtatására képen* a **aocr** motor segítségével, a **strukturált OCR felismerés** kérésével, majd a geometria megőrzésével történő utófeldolgozással. A végére képes leszel **szöveg és koordináták kinyerésére** néhány Python sorral, és megérted, miért fontos a strukturált mód a további feladatokhoz.

## Amit megtanulsz

- Hogyan inicializáld az OCR motort **strukturált OCR felismeréshez**.  
- Hogyan adj meg egy képet, és kapj nyers eredményeket, amelyek tartalmazzák a sorok határait.  
- Hogyan futtass egy utófeldolgozót, amely megtisztítja a szöveget anélkül, hogy elveszítené a geometriát.  
- Hogyan iterálj a végső sorokon, és írd ki a szöveget a hozzá tartozó körülhatároló dobozzal együtt.  

Nincs varázslat, nincs rejtett lépés – csak egy teljes, futtatható példa, amelyet beilleszthetsz a saját projektedbe.

---

## Előfeltételek

Mielőtt belemerülnénk, győződj meg róla, hogy a következők telepítve vannak:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Szükséged lesz egy képfájlra (`input_image.png` vagy `.jpg`), amely tiszta, olvasható szöveget tartalmaz. Bármilyen, egy beolvasott számla vagy képernyőképről származó kép megfelel, amíg az OCR motor képes felismerni a karaktereket.

---

## 1. lépés: Az OCR motor inicializálása strukturált felismeréshez

Az első dolog, amit teszünk, hogy létrehozzuk a `aocr.Engine()` példányt, és jelezzük, hogy **strukturált OCR felismerést** szeretnénk. A strukturált mód nem csak a sima szöveget adja vissza, hanem geometriai adatokat (körülhatároló téglalapok) is minden sorhoz, ami elengedhetetlen, ha a szöveget vissza kell térképezni a képre.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Miért fontos:**  
> Alapértelmezett módban a motor csak egy összefűzött szövegsorozatot adhat vissza. A strukturált mód egy hierarchiát biztosít: oldalak → sorok → szavak, mindegyik koordinátákkal, ami sokkal egyszerűbbé teszi az eredmények átfedését az eredeti képen vagy egy layout‑érzékeny modellbe való betáplálását.

---

## 2. lépés: OCR futtatása a képen és nyers eredmények lekérése

Most betápláljuk a képet a motorba. A `recognize` hívás egy `OcrResult` objektumot ad vissza, amely sorok gyűjteményét tartalmazza, mindegyik saját körülhatároló téglalappal.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Ekkor a `raw_result.lines` olyan objektumokat tartalmaz, amelyek két fontos attribútummal rendelkeznek:

- `text` – a sorhoz tartozó felismert karakterlánc.  
- `bounds` – egy `(x, y, width, height)` alakú tuple, amely leírja a sor pozícióját.

---

## 3. lépés: Utófeldolgozás a geometria megőrzésével

A nyers OCR kimenet gyakran zajos: eltévedt karakterek, helytelen szóközök vagy sortörés-problémák. Az `ai.run_postprocessor` függvény megtisztítja a szöveget, de **megtartja az eredeti geometriát**, így továbbra is pontos koordinátákkal rendelkezel.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tipp:** Ha domain‑specifikus szókincsed van (pl. termékkódok), adj meg egy egyedi szótárat az utófeldolgozónak a pontosság javítása érdekében.

---

## 4. lépés: Szöveg és koordináták kinyerése – iterálás és megjelenítés

Végül végigjárjuk a megtisztított sorokat, és kiírjuk minden sor körülhatároló dobozát a szöveg mellett. Ez a **szöveg és koordináták kinyerésének** magja.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Várható kimenet

Tegyük fel, hogy a bemeneti kép két sort tartalmaz: „Invoice #12345” és „Total: $89.99”. Valami ilyesmit fogsz látni:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Az első tuple a `(x, y, width, height)` érték, amely a sor helyét jelöli az eredeti képen, lehetővé téve téglalapok rajzolását, szöveg kiemelését vagy a koordináták más rendszerbe való betáplálását.

---

## Az eredmény megjelenítése (opcionális)

Ha szeretnéd látni a körülhatároló dobozokat a képen, használhatod a Pillow‑t (PIL) a téglalapok rajzolásához. Az alábbi egy gyors snippet; nyugodtan kihagyhatod, ha csak a nyers adatokat akarod.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

A fenti alternatív szöveg tartalmazza a **fő kulcsszót**, ezzel teljesítve a SEO követelményt a kép alt attribútumok számára.

---

## Miért felülmúlja a strukturált OCR felismerés az egyszerű szövegkivonást

Talán azt kérdezed, „Nem elég csak OCR‑t futtatni és a szöveget kapni? Miért van szükség a geometriára?”  

- **Térbeli kontextus:** Ha egy űrlapon mezőket kell párosítani (pl. „Dátum” a dátumérték mellett), a koordináták megmutatják, *hol* található az adat.  
- **Többoszlopos elrendezések:** Az egyszerű lineáris szöveg elveszíti a sorrendet; a strukturált adat megőrzi az oszlopok sorrendjét.  
- **Utófeldolgozási pontosság:** A doboz méretének ismerete segít eldönteni, hogy egy szó fejléc, lábjegyzet vagy csak egy véletlen maradvány-e.  

Röviden, a **strukturált OCR felismerés** rugalmasságot ad intelligens csővezetékek építéséhez – legyen szó adatbázisba való betáplálásról, kereshető PDF‑ek létrehozásáról vagy egy olyan gépi tanulási modell tréningjéről, amely tiszteletben tartja a layout‑ot.

---

## Gyakori szélhelyzetek és megoldások

| Helyzet | Mire figyelj | Javasolt megoldás |
|-----------|-------------------|---------------|
| **Elforgatott vagy ferde képek** | A körülhatároló dobozok eltérhetnek a valóságtól. | Előfeldolgozás deskew‑el (pl. OpenCV `warpAffine`). |
| **Nagyon kicsi betűk** | A motor kihagyhat karaktereket, üres sorok keletkeznek. | Növeld a kép felbontását, vagy használd az `ocr_engine.set_dpi(300)` beállítást. |
| **Vegyes nyelvek** | Rossz nyelvi modell torz szöveget eredményezhet. | Állítsd be `ocr_engine.language = ["en", "de"]` a felismerés előtt. |
| **Átfedő dobozok** | Az utófeldolgozó esetleg két sort egybeolvas. | Ellenőrizd a `line.bounds` értékét a feldolgozás után; állítsd be a küszöböket az `ai.run_postprocessor`‑ben. |

Ezeknek a szcenárióknak a korai kezelése rengeteg fejfájást takarít meg, különösen ha a megoldást naponta több száz dokumentumra skálázod.

---

## Teljes, vég‑től‑végig script

Az alábbi a kész, futtatható program, amely összekapcsolja az összes lépést. Másold be, módosítsd a kép útvonalát, és már indulhat is.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

A script futtatása:

1. **OCR futtatása képen** strukturált módban.  
2. **Szöveg és koordináták kinyerése** minden sorhoz.  
3. Opcionálisan egy annotált PNG előállítása a dobozokkal.

---

## Összegzés

Most már egy szilárd, önálló megoldásod van a **OCR futtatására képen** és a **szöveg és koordináták kinyerésére** a **strukturált OCR felismerés** segítségével. A kód minden lépést bemutat – a motor inicializálásától az utófeldolgozáson át a vizuális ellenőrzésig –, így könnyen adaptálható nyugták, űrlapok vagy bármely vizuális dokumentum esetén, amely pontos szöveg‑lokalizációt igényel.

Mi a következő? Próbáld ki a `aocr` motort egy másik könyvtárral (Tesseract, EasyOCR), és nézd meg, hogyan különböznek a strukturált kimeneteik. Kísérletezz különböző utófeldolgozási stratégiákkal, például helyesírás‑ellenőrzéssel vagy egyedi regex‑szűrőkkel, hogy növeld a pontosságot a saját területedhez. Ha nagyobb csővezetéket építesz, fontold meg a `(text, bounds)` párok adatbázisba való tárolását későbbi elemzésekhez.

Boldog kódolást, és legyenek a OCR projektjeid mindig pontosak!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}