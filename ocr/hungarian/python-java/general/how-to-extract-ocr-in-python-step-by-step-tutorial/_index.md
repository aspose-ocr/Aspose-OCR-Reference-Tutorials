---
category: general
date: 2026-04-26
description: hogyan lehet OCR-t kinyerni képekből Python használatával – egy python
  OCR példa, amely bemutatja, hogyan töltsünk be képet OCR-hez, és hogyan nyerjünk
  ki szöveget egy nyugtából.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: hu
og_description: hogyan lehet OCR-t kinyerni képekből Python használatával. Tanulj
  meg egy Python OCR példát, tölts be képet OCR-hez, és percek alatt nyerd ki a szöveget
  egy nyugtáról.
og_title: Hogyan lehet OCR-t kinyerni Pythonban – Teljes útmutató
tags:
- OCR
- Python
- Image Processing
title: Hogyan lehet OCR-t kinyerni Pythonban – Lépésről lépésre útmutató
url: /hu/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan kell OCR-t kinyerni Pythonban – Teljes útmutató

Gondolkodtál már azon, **hogyan kell OCR-t kinyerni** egy elmosódott nyugtából vagy egy beolvasott számlából? Nem vagy egyedül – a fejlesztők gyakran akadnak szembe a problémával, amikor tiszta, gép‑olvasó szöveget kell kinyerniük a képekből. A jó hír? Néhány Python sorral egy nyugta képét magas biztonságú, kereshető szöveggé alakíthatod.

Ebben az útmutatóban egy **python ocr példát** mutatunk be, amely bemutatja, **hogyan kell képet betölteni OCR-hez**, futtatja a motort, és csak azokat a karaktereket tartja meg, amelyek legalább 85 % biztonsági küszöböt érnek el. A végére képes leszel **szöveget kinyerni nyugta** képekből anélkül, hogy dokumentációban keresgélnél vagy API paramétereket tippelnél.

## Amire szükséged lesz

- Python 3.9 vagy újabb (az általunk használt szintaxis 3.8‑on is működik)
- A `aocr` csomag (vagy bármely OCR könyvtár, amely `OcrEngine` osztályt biztosít). Telepítsd a következővel:

```bash
pip install aocr
```

- Egy minta nyugta kép (`receipt.png`), amely egy olyan mappában van, amelyre hivatkozhatsz.
- Egy szövegszerkesztő vagy IDE – VS Code, PyCharm, vagy akár egy egyszerű notebook is megfelel.

Ennyi. Nincs nehéz keretrendszer, nincs külső szolgáltatás, csak tiszta Python.

![Magas‑biztonságú OCR eredmény – hogyan lehet OCR-t kinyerni egy nyugtából](/images/ocr-high-confidence.png)

*Kép alternatív szöveg: hogyan lehet OCR-t kinyerni egy nyugtából Python OCR használatával*

## 1. lépés – OCR motor példány létrehozása (hogyan kell OCR-t kinyerni)

Az első dolog, amit teszünk, egy OCR motor elindítása. Gondolj rá úgy, mint egy agyra, amely a pixeleket olvassa helyettünk.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Miért?** Az `OcrEngine` példányosítása egy friss konfigurációs objektumot ad. Később módosíthatod a nyelvi modelleket, DPI beállításokat vagy az előfeldolgozási lépéseket – mindezt anélkül, hogy a fő feldolgozási ciklust érintenéd.

## 2. lépés – Kép betöltése OCR-hez

Ezután a motort a analizálni kívánt kép felé irányítjuk. Itt jön képbe a **load image for ocr** kulcsszó.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tipp:** Ha a képed egy másik könyvtárban van, használd az `os.path.join`-t egy platform‑független útvonal építéséhez.

**Miért töltsük be a képet így?** A `Image.load` segédfüggvény beolvassa a fájlt egy olyan formátumba, amelyet a motor ért, és automatikusan kezeli a gyakori formátumokat (PNG, JPEG, TIFF). Ennek a lépésnek a kihagyása vagy nyers bájtok átadása `ValueError`-t eredményezne.

## 3. lépés – OCR folyamat futtatása

Most ténylegesen futtatjuk az OCR-t. A `process` metódus egy gazdag eredményobjektust ad vissza, amely tartalmazza a felismert szimbólumokat, a biztonsági pontszámokat és a határoló dobozokat.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Mit tartalmaz az `ocr_result`?** A legtöbb könyvtárban ez a következőket tartalmazza:

- `text`: a nyers összefűzött karakterlánc.
- `symbol_confidences`: egy `(char, confidence)` párokat tartalmazó lista.
- `boxes`: minden karakter koordinátái (hasznos vizuális hibakereséshez).

A karakterenkénti biztonság elérése elengedhetetlen a következő lépéshez.

## 4. lépés – Csak a magas biztonságú szimbólumok megtartása (≥ 85 %)

Egy nyugtán gyakran vannak foltok, halvány nyomtatás vagy háttérzaj. Az alacsony biztonságú szimbólumok kiszűrésével jelentősen javítható a további feldolgozás.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Miért 85 %?** Empirikusan a 0,85 körüli küszöb a legtöbb nyomtatott nyugtán a visszahívás és a pontosság egyensúlyát biztosítja. Ha hiányzó számokat látsz, csökkentsd a küszöböt; ha értelmetlen szöveget kapsz, emeld.

## 5. lépés – A magas biztonságú kinyert szöveg kiírása

Végül kiírjuk (vagy elmentjük) a megtisztított karakterláncot. Ez a **extract text from receipt** munkafolyamatunk középpontja.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

A tipikus kimenet így néz ki:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Most már ezt a karakterláncot átadhatod egy CSV írónak, egy adatbázisnak vagy bármely további elemzési csővezetéknek.

## Teljes, azonnal futtatható szkript

Az alábbiakban a teljes kódrészlet található, amelyet beilleszthetsz a `ocr_receipt.py` fájlba, és azonnal futtathatsz.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Mentsd el a fájlt, győződj meg róla, hogy a `receipt.png` létezik, és futtasd:

```bash
python ocr_receipt.py
```

A konzolon meg kell jelennie a megtisztított nyugta szövegnek.

## Szélsőséges esetek és „Mi lenne ha” szcenáriók

| Helyzet | Javasolt megoldás |
|-----------|----------------|
| **Nagyon alacsony biztonság mindenhol** | Előfeldolgozd a képet: növeld a kontrasztot, konvertáld szürkeárnyalatosra, vagy alkalmazz zajszűrő szűrőt (`cv2.GaussianBlur`). |
| **Nem latin karakterek** | Adj át egy nyelvi modellt az `OcrEngine`-nek (pl. `ocr_engine.language = "spa"` a spanyolhoz). |
| **Több nyugta egy képen** | Futtasd az OCR-t a teljes képen, majd oszd szét az eredményt reguláris kifejezésekkel, amelyek a `\n\n+` (dupla sortörés) mintát észlelik. |
| **Szükség van a nyers OCR szövegre is** | Tartsd meg az `ocr_result.text`-et a szűrt verzió mellett a hibakereséshez. |

Ezek a változatok biztosítják, hogy a **how to use OCR** tudásod túlmutasson a legegyszerűbb eseten.

## Gyakori buktatók (és hogyan kerüld el őket)

- **Elfelejted telepíteni a könyvtárat** – a `pip install aocr`-nek sikeresnek kell lennie, mielőtt importálnád.
- **Rossz útvonal-elválasztó használata** Windows-on (`\` vs `/`). Használd az `os.path.join`-t.
- **A biztonsági küszöb hard‑kódolása** tesztelés nélkül – mindig végezz egy gyors vizuális ellenőrzést néhány nyugtán először.
- **Az Unicode normalizáció figyelmen kívül hagyása** – egyes nyugták speciális kötőjeleket tartalmaznak; futtasd a `unicodedata.normalize('NFKC', text)`-et, ha a kimenetet tárolni szeretnéd.

## Következő lépések – Túl a alapokon

Most, hogy tudod, **hogyan kell OCR-t kinyerni** egyetlen nyugtából, lehet, hogy szeretnéd:

1. **Kötegelt feldolgozása egy nyugták mappájának** – iterálj minden PNG/JPG fájlon, és írd az egyes eredményeket egy CSV-be.
2. **Integrálás adatbázissal** – tárold a `high_confidence_text`-et SQLite-ben a gyors lekérdezésekhez.
3. **Természetes nyelvi feldolgozás alkalmazása** – használj regex-et vagy `dateutil`-t a dátumok, összegek és adóösszegek kinyeréséhez.
4. **Kísérletezz alternatív könyvtárakkal** – `pytesseract`, `easyocr`, vagy felhőszolgáltatások (Google Vision, Azure OCR), ha többnyelvű támogatásra vagy nagyobb pontosságra van szükséged.

Ezek a témák természetesen beépítik a másodlagos kulcsszavainkat: *python ocr example*, *extract text from receipt*, *load image for ocr*, és *how to use OCR*.

## Következtetés

Most egy teljes **python ocr example**-t vettünk át, amely bemutatja, **hogyan kell OCR-t kinyerni** egy nyugta képből, kiszűri az alacsony biztonságú szimbólumokat, és tiszta eredményt ad. A lépések egyszerűek, a kód önálló, és a megközelítés elég rugalmas ahhoz, hogy nagyobb projektekhez is alkalmazkodjon.

Próbáld ki a saját nyugtáiddal, állítsd be a biztonsági küszöböt, majd méretezz fel kötegelt feldolgozásra. Ha furcsaságokba ütközöl – például halvány logó vagy szokatlan betűtípus – emlékezz a fenti szélsőséges esetek tippeire. Boldog kódolást, és legyen az OCR csővezeted mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}