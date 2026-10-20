---
category: general
date: 2026-04-26
description: Hogyan hajtsunk végre OCR-t egy beolvasott űrlapon, tanuljuk meg a kép
  előfeldolgozását a zaj csökkentése érdekében, és gyorsan nyerjünk ki szöveget a
  képből.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: hu
og_description: Hogyan futtass OCR-t beolvasott dokumentumokon, előfeldolgozd a képeket,
  csökkentsd a zajt, és hatékonyan nyerd ki a szöveget.
og_title: Hogyan futtass OCR-t és előfeldolgozd a képeket – Gyors útmutató
tags:
- OCR
- image processing
- Python
title: Hogyan futtassunk OCR-t és előfeldolgozzuk a képeket – Szöveg kinyerése beolvasott
  űrlapokból
url: /hu/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassuk az OCR‑t – Teljes útmutató a képek szövegének kinyeréséhez

Gondolkodtál már azon, **hogyan futtassuk az OCR‑t** egy rendezetlen beolvasott űrlapon, és tiszta, kereshető szöveget kapjunk? Nem vagy egyedül. Sok valós projektben a nyers kép tele van foltokkal, egyenetlen megvilágítással és egyéb sajátosságokkal, amelyek miatt a kész‑out‑of‑the‑box OCR elakadhat.

A jó hír? Néhány Python sorral és egy okos előfeldolgozó csővezetékkel drámaian növelheted a felismerési pontosságot, **csökkentheted a zajt**, és kinyerheted a szükséges szavakat. Ebben az útmutatóban minden lépést végigvezetünk – a kép betöltésétől a végső karakterlánc kiírásáig –, így egy kész, könnyen beilleszthető kódrészletet kapsz, amelyet számlákra, nyugtákra vagy bármely beolvasott dokumentumra adaptálhatsz.

## Mit fogsz építeni

- Egy `OcrEngine` példány, amely a háttérben lévő OCR könyvtárral kommunikál.  
- Egy előfeldolgozó lánc, amely **binarizálja** a képet, és **medián elmosást** alkalmaz a foltok kisimításához.  
- Egy egyszerű hívás a `process()`-ra, amely egy olyan objektumot ad vissza, amely a `text` attribútumon keresztül a kinyert karakterláncot tartalmazza.  

A végére egy önálló szkriptet kapsz, amelyet bármilyen képfájlon futtathatsz, és azonnal láthatod a kinyert szöveget a konzolon.

## Előfeltételek

- Python 3.9+ (a használt szintaxis a legújabb stabil kiadással egyezik).  
- A fiktív `aocr` csomag – tekintsd egy vékony burkolatnak a Tesseract vagy bármely modern OCR motor körül. Telepítsd a `pip install aocr` paranccsal.  
- Egy beolvasott kép (`scanned_form.jpg`) egy olyan mappában, amelyre hivatkozhatsz.  

Ha valós OCR könyvtárat, például `pytesseract`-ot használsz, kicserélheted az `OcrEngine`-t a megfelelő osztályra – minden más változatlan marad.

![](how-to-run-ocr-example.png "hogyan futtassuk az OCR példát, amely egy beolvasott űrlapot és a kinyert szöveget mutatja")

*Alt szöveg: hogyan futtassuk az OCR‑t egy beolvasott dokumentumon, és tekintsük meg a kinyert szöveget.*

---

## 1. lépés: Hogyan futtassuk az OCR‑t – Az motor inicializálása

Mielőtt a motor bármit olvasna, létre kell hoznunk egy példányt. Tekintsd a `OcrEngine`-t egy agynak, amely később értelmezi a vizuális adatokat.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Miért fontos:** A motor példányosítása beállítja a belső modelleket, betölti a nyelvi csomagokat, és előkészíti a futtatási környezetet. Ennek a lépésnek a kihagyása általában `NoneType` hibához vezet, amikor később a `process()`-t hívod.

---

## 2. lépés: Hogyan előfeldolgozzuk a képet – Töltsd be a beolvasott űrlapot

Most, hogy az agy készen áll, betáplálunk egy képet. A kép bármilyen, az `aocr.Image` által támogatott formátumban lehet.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro tipp:** Fejlesztés közben használj abszolút útvonalakat, hogy elkerüld a „file not found” meglepetéseket, amikor a szkript más munkakönyvtárból fut.

---

## 3. lépés: Hogyan csökkentsük a zajt – Binarizálás és medián elmosás alkalmazása

A nyers beolvasások gyakran tartalmaznak szóró pontokat, egyenetlen háttérrel vagy halvány árnyékokkal. Két klasszikus trükk – **binarizálás** és **medián elmosás** – tisztítja a képet anélkül, hogy feláldozná a karaktereket meghatározó éleket.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Mélyebb részletek

- **Binarizálás**: A `threshold=180` érték azt mondja az algoritmusnak: „Minden, ami 180-nál világosabb, fehér lesz; minden más fekete.” Állítsd ezt a számot, ha a beolvasás túl sötét vagy túl világos.  
- **Medián elmosás**: A `2` sugár azt jelenti, hogy a szűrő egy 5×5 pixeles ablakot vizsgál, és a középső pixelt a medián értékkel helyettesíti. Ez kisimítja az elszigetelt foltokat, miközben a betűk vonalai érintetlenek maradnak.

> **Szélsőséges eset:** Ha a dokumentum színes kiemeléseket tartalmaz, egy egyszerű bináris küszöb eltávolíthatja őket. Ebben az esetben fontold meg a `aocr.ImageFilters.adaptive_threshold()` használatát – ez a küszöböt helyileg alkalmazza a képen.

---

## 4. lépés: Hogyan nyerjünk ki szöveget – Futtassuk az OCR folyamatot

Egy tiszta képpel a kezünkben végül hagyjuk, hogy a motor elvégezze a varázslatát.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Mi történik a háttérben?** A motor egy neurális hálózatot (vagy régi mintakeresőt) futtat a pixelmátrixon, minden felismert glifet Unicode karakterekké alakít, és sorokba, bekezdésekbe rendezi őket.

---

## 5. lépés: Hogyan nyerjünk ki szöveget – Az eredmény kiírása

Az `ocr_result` objektum egy kényelmes `text` attribútumot biztosít. Nézzük meg, mit kaptunk.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Várható kimenet

Ha a beolvasott űrlap tartalmazza:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Valami ilyesmit kell látnod:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Vedd észre, hogy az előfeldolgozó lépés eltávolította a szóró pontokat, amelyek korábban az „Amount” szót „Am0unt”‑ra változtatták. Ez a **zajcsökkentés** ereje az OCR előtt.

---

## Gyakori hibák és megoldások

| Tünet | Valószínű ok | Gyors megoldás |
|---------|--------------|-----------|
| Széttört karakterek (pl. “@#%”) | A kép túl sötét vagy túl világos | Finomítsd a `threshold` értékét a `binarize()`-ban; próbáld ki az `adaptive_threshold`-ot. |
| Hiányzó szavak | Még mindig zaj van | Növeld a `radius` értékét a `median_blur`-nél vagy adj hozzá egy `gaussian_blur` szűrőt. |
| Rossz nyelv (pl. az angol betűk kínai karakterekké válnak) | Hibás nyelvi csomag betöltve | Adj meg `language="eng"`-et az `OcrEngine()` létrehozásakor, ha a könyvtár támogatja. |
| Lassú feldolgozás nagy fájloknál | Magas felbontás | Először méretezd le a képet: `aocr.ImageFilters.resize(width=1200)` a binarizálás előtt. |

---

## Továbbfejlesztés – Következő lépések és kapcsolódó témák

- **Kötegelt feldolgozás**: Csomagold a fenti logikát egy ciklusba, hogy automatikusan több tucat fájlt kezelj.  
- **Strukturált kimenet**: Használj reguláris kifejezéseket az `ocr_result.text`-en, hogy kinyerd a mezőket, például dátumokat vagy összegeket.  
- **Alternatív könyvtárak**: Cseréld le az `aocr`-t `pytesseract`-ra – a kód csak a motor inicializálásánál változik.  
- **Hogyan előfeldolgozzuk a képet PDF-ekhez**: Konvertáld minden PDF oldalt képpé, majd alkalmazd ugyanazt a csővezetéket.  

Ezek a kiegészítések lehetővé teszik, hogy a megoldást egyetlen űrlapról egy vállalati szintű dokumentumbeviteli csővezetékre skálázd.

---

## Összegzés

Áttekintettük, **hogyan futtassuk az OCR‑t** a kezdetektől a végéig, bemutattuk, **hogyan előfeldolgozzuk a képet** a **zajcsökkentés** érdekében, és demonstráltuk, **hogyan nyerjünk ki szöveget a képből** egy tiszta, reprodukálható szkripttel. A fő tanulság? Néhány egyszerű szűrő – a binarizálás és a medián elmosás – egy zajos beolvasást megbízható adatforrássá alakíthat, órákat takarítva meg a kézi tisztítást.

Próbáld ki a szkriptet a saját dokumentumaiddal, finomítsd a küszöböket, és figyeld, ahogy a pontosság nő. Amikor készen állsz, fedezd fel a kötegelt feldolgozást vagy integráld a kimenetet egy adatbázisba a kereshető archívumokhoz. Boldog kódolást, és legyen az OCR mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}