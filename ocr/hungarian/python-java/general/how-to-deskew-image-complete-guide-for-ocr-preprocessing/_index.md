---
category: general
date: 2026-07-05
description: Hogyan javítsuk gyorsan a kép ferdeségét. Tanulja meg, hogyan előkészítsük
  a képet OCR-hez, korrigáljuk a kép forgását, és alakítsuk a beolvasást szöveggé
  Python segítségével.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: hu
og_description: Hogyan korrigáljuk a kép ferdeségét és előkészítsük OCR-hez. Ez az
  útmutató bemutatja, hogyan lehet helyesbíteni a kép forgását, és Python segítségével
  szöveget kinyerni a képből.
og_title: Hogyan korrigáljuk a kép dőlését – Lépésről lépésre az OCR előfeldolgozás
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Hogyan kiegyenesítsünk képet – Teljes útmutató az OCR előfeldolgozáshoz
url: /hu/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan egyenesítsünk ki egy képet – Teljes útmutató az OCR előfeldolgozáshoz

Gondolkodtál már azon, hogy **hogyan egyenesítsünk ki egy képet**, amely úgy néz ki, mintha egy ferde szkennerről származna? Nem vagy egyedül. Sok valós projektben az első dolog, amit meg kell tenni, mielőtt **kivonhatnád a szöveget a képből**, az a dőlésszög kiegyenesítése.

Ebben az útmutatóban egy gyakorlati, végponttól végpontig tartó példán keresztül vezetünk, amely **előfeldolgozza a képet OCR-hez**, kijavítja a forgatást, és végül **szkennelt anyagot szöveggé alakít** egy Python OCR könyvtár segítségével. Nincsenek homályos hivatkozások, csak egy működő szkript, amelyet másolhatsz‑beilleszthetsz, valamint tippek a gyakori buktatókhoz.

## Amit el fogsz érni

* Bármely enyhén ferde szkennelt JPEG vagy PNG betöltése.  
* Egy egyenesítő szűrő és egy binarizációs lépés alkalmazása az OCR pontosságának növelése érdekében.  
* Az OCR motor futtatása és a **kép szövegének kinyerése** megbízhatóan.  
* Megérteni, miért fontos a **helyes képrotáció** a későbbi szövegkinyerésnél.  

### Előfeltételek

* Python 3.9+ telepítve a gépeden.  
* Egy pip‑telepíthető OCR csomag, amely utánozza a példában használt `ocr` névtér struktúráját (például egy vékony wrapper a Tesseract köré).  
* Alapvető ismeretek a Python függvényekkel és a képfeldolgozási fogalmakkal kapcsolatban.  

Ha ezek megvannak, vágjunk bele.

![how to deskew image example](deskew_before_after.png){alt="hogyan egyenesítsünk ki egy képet – javítás előtti és utáni állapot"}

## 1. lépés: Az OCR motor beállítása – Hogyan egyenesítsünk ki egy képet Python használatával

Először is: szükséged van egy OCR motorra, amely megérti a dokumentum nyelvét. Az alábbi kódrészlet mutatja a minimális sablont a motor létrehozásához és ahhoz, hogy jelezd, angol szöveggel dolgozol.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Miért fontos:* A motor nyelvi beállítása befolyásolja a használt karakterkészletet és szótárat. Ennek a lépésnek a kihagyása azt eredményezheti, hogy az OCR gyakori szavakat félreértelmez, különösen miután **helyes képrotációt** alkalmaztál.

## 2. lépés: A kiegyenesíteni kívánt szkennelt kép betöltése

Most betöltjük a fájlt a memóriába. Cseréld ki a `"YOUR_DIRECTORY/skewed_scan.jpg"`-t a saját képed elérési útjára.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Ha a kép már egy NumPy tömbben vagy egy OpenCV `Mat`-ban van, a betöltőt ennek megfelelően módosíthatod – a lényeg, hogy az objektumnak rendelkeznie kell a később használt `apply_filter` metódussal.

## 3. lépés: Kép előfeldolgozása OCR-hez – Egyenesítés és binarizálás

Itt történik a varázslat. Két szűrőt láncolunk egymásra:

1. **Deskew** – automatikusan felismeri a domináns szövegalapot és a képet vízszintesre forgatja vissza.  
2. **Binarize (Otsu)** – a képet tiszta fekete‑fehérre konvertálja, ami drámaian javítja a felismerési arányt.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tipp:* Ha azt veszed észre, hogy a szöveg még mindig elmosódottnak tűnik a binarizálás után, próbáld finomhangolni a kontrasztot vagy egy másik küszöbölési módszert használni. Az `ocr.Filter` modul gyakran tartalmaz `adaptive_threshold()`-t a nehezebb esetekhez.

## 4. lépés: OCR futtatása – Kép szövegének kinyerése

Egy tiszta, kiegyenesített vászonnal átadjuk a képet a motornak. Az eredményobjektum tartalmazza a felismert karakterláncot, a megbízhatósági pontszámokat, és akár a körülhatároló dobozokat is, ha később szükséged van rájuk.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

A tipikus kimenet így néz ki:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Észrevetted, hogy a sortörések tökéletesen illeszkednek? Ez a **helyes képrotáció** előnye – az OCR már nem kell, hogy kitalálja a sorok irányát.

## 5. lépés: Összeállítás – Egyetlen fájlból álló szkript a szkennelés szöveggé alakításához

Az alábbiakban a teljes, futtatható szkript található, amely egyesíti a megbeszélt összes lépést. Mentsd el `deskew_ocr.py` néven, és futtasd a `python deskew_ocr.py` paranccsal.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Miért működik ez

* **Először egyenesítés** – a kép forgatása a binarizálás előtt biztosítja, hogy a küszöbölő algoritmus egy sík horizonton dolgozzon.  
* **Binarizálás egyenesítés után** – az Otsu módszer bimodális hisztogramot feltételez; egy ferde oldal felborítaná ezt a feltételezést.  
* **Angol nyelvi modell** – megmondja az OCR-nek, milyen karakterekre számítson, csökkentve a hamis pozitív eredményeket.

Ha más nyelveket kell kezelni, egyszerűen cseréld le a `ocr.Language.ENGLISH`-t a megfelelő enumra.

## Gyakori kérdések és szélhelyzetek

| Question | Answer |
|----------|--------|
| *Mi van, ha a szkennelés fejjel lefelé van?* | A `deskew()` szűrő általában észleli a 180°-os forgatást is. Ha ez nem sikerül, hívd meg a `apply_filter(ocr.Filter.rotate(180))`-t az egyenesítés előtt. |
| *A dokumentumom színes grafikákat tartalmaz – a binarizálás törli őket?* | Igen. Vegyes tartalom esetén fontold meg, hogy csak a `ocr.Filter.deskew()`-t használd, majd futtasd az OCR-t a színes képen. Így a szöveget kinyerheted, miközben a grafikákat megőrzöd. |
| *Feldolgozhatok egy csomó fájlt egyszerre?* | Tegyük a logikát egy ciklusba, olvassuk be a fájlútvonalakat egy listából, és minden `result.text`-et egy külön `.txt` fájlba mentsünk. |
| *Hogyan javíthatom a pontosságot alacsony felbontású szkenneléseknél?* | Nagyítsd fel a képet egy bikubikus szűrővel **az** egyenesítés **előtt**, majd alkalmazz egy élesítő szűrőt. Több pixel jobb információt ad az OCR motor számára. |

## Bónusz: A képek egyenesítésének vizuális ellenőrzése

Ha szeretnéd egymás mellett látni a javítás előtti és utáni állapotot, adj hozzá egy gyors Matplotlib kódrészletet:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## Összegzés

Áttekintettük, **hogyan egyenesítsünk ki egy képet**, miért elengedhetetlen a **kép előfeldolgozása OCR-hez**, és hogyan **kivonjuk a szöveget a képből**, hogy végül **szkennelt anyagot szöveggé alakítsunk**. A munkafolyamat – betöltés → egyenesítés → binarizálás → felismerés – biztosítja, hogy az OCR egy tiszta, egyenes oldalt lásson, ami magasabb pontosságot és kevesebb manuális javítást eredményez.

Mi a következő lépés az OCR útján? Próbálj ki a következőket:

* Különböző nyelvi csomagok (`ocr.Language.FRENCH`, stb.).  
* Elrendezés-elemzési lépés hozzáadása oszlopok vagy táblázatok felismeréséhez.  
* Az OCR eredmények exportálása kereshető PDF-ekbe egy PDF könyvtár segítségével.

Nyugodtan hagyj megjegyzést, ha elakadsz, vagy oszd meg a saját trükkjeidet a különösen makacs szkennelések kezeléséhez. Boldog kódolást, és legyenek a képeid mindig tökéletesen egyenesek!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan használjuk az AspOCR-t: Kép OCR szűrők előfeldolgozása .NET-hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Kép szövegének kinyerése C#-ban nyelvválasztással az Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hogyan OCR-eljünk képet – OCR végrehajtása képen az OCR Képfelismerésben](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}