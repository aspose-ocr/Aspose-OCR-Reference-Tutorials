---
category: general
date: 2026-07-05
description: Végezz OCR-t képen Python segítségével. Tanuld meg, hogyan konvertálj
  képet szöveggé Pythonban, hogyan tölts be képet OCR-hez, és hogyan nyerj ki cirill
  szöveget a képből percek alatt.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: hu
og_description: Végezz OCR-t képen Pythonban. Ez az útmutató megmutatja, hogyan konvertálj
  képet szöveggé Pythonban, hogyan tölts be képet OCR-hez, és hogyan nyerj ki gyorsan
  cirill szöveget a képből.
og_title: OCR végrehajtása képen Python segítségével – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: OCR végrehajtása képen Python segítségével – Teljes lépésről‑lépésre útmutató
url: /hu/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image with Python – Complete Step‑by‑Step Guide

Gondolkodtál már azon, hogyan **perform OCR on image** fájlokon anélkül, hogy egy harmadik fél szolgáltatására bízod őket? Nem vagy egyedül. Sok projektben—útlevél‑szkennerek, nyugta‑digitalizálók vagy archiváló eszközök—az első akadály a nyers szöveg kinyerése egy képből.  

Ebben az útmutatóban egy gyakorlati példán keresztül vezetünk végig, amely **converts image to text python** stílusban mutatja be, hogyan **load image for OCR**, és végül **extract Cyrillic text from image** a nyílt forráskódú `aocr` könyvtár segítségével. A végére képes leszel **recognize Cyrillic text** bármilyen képen, amit csak bevetel.

> **What you’ll walk away with:** egy azonnal futtatható script, világos magyarázatok minden lépéshez, és tippek a gyakori buktatók kezeléséhez (például homályos beolvasások vagy váratlan betűtípusok). Nincs külső API, csak tiszta Python.

---

## Prerequisites

Mielőtt belevágunk, győződj meg róla, hogy rendelkezel:

- Python 3.8 vagy újabb telepítve.
- Egy terminál vagy parancssor, amivel kényelmesen dolgozol.
- Az `aocr` csomag (telepíthető a `pip install aocr` paranccsal).
- Egy képfájl, amely cirill karaktereket tartalmaz (például egy beolvasott orosz útlevél).  

Ha bármelyik ismeretlennek tűnik, ne aggódj — minden pontot röviden áttekintünk a továbbiakban.

---

## Step 1: Perform OCR on Image – Setting Up the Environment

Az első dolog, amire szükségünk van, egy tiszta Python környezet, ahol az OCR könyvtár él. A virtuális környezet használata elszigeteli a függőségeket és megakadályozza a verzióütközéseket.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Why?**  
Egy dedikált környezet biztosítja, hogy az `aocr` csomag és natív binárisai ne ütközzenek más projektekbe. Emellett a reprodukálhatóság is egyszerűvé válik — valaki más klónozhatja a repódat és futtathatja ugyanazt a `pip install -r requirements.txt` parancsot.

> **Pro tip:** Fagyaszd le a függőségeket a `pip freeze > requirements.txt` paranccsal, hogy mindig tudd, pontosan mely verziók lettek használva.

---

## Step 2: Load Image for OCR – Importing and Preparing the File

Most, hogy a könyvtár készen áll, **load image for OCR**-ra van szükségünk. Az `aocr.Image.from_file` metódus a legtöbb általános formátumot (PNG, JPEG, TIFF) kezeli. Íme, hogyan csináld:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Mi történik itt?**  
`aocr.Image.from_file` beolvassa a bináris adatokat, dekódolja őket, és egy olyan objektumba helyezi, amelyet az OCR motor megért. Ha a fájl nem található, a Python `FileNotFoundError`‑t dob, amelyet később elkapva szép hibakezelést valósíthatsz meg.

> **Edge case:** Néhány szkenner többoldalas TIFF‑eket ad ki. Ilyen esetben előbb szét kell választani az oldalakat — az `aocr` biztosítja az `Image.from_tiff_pages()` metódust erre.

---

## Step 3: Configure the OCR Engine – Forcing Cyrillic Recognition

Alapértelmezés szerint sok OCR motor megpróbálja kitalálni a nyelvet, ami torzuló kimenetet eredményezhet nem‑latin írásrendszerek esetén. A **recognize Cyrillic text** megbízhatóan történő elvégzéséhez kifejezetten állítsuk a nyelvet „cyrillic” értékre.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Miért kényszerítjük a nyelvet?**  
A cirill karakterek vizuálisan hasonlítanak a latin betűkre (pl. „A” vs „А”). Ha a motor tudja, hogy cirillre számít, a félreolvasás drámaian csökken, különösen alacsony felbontású beolvasásoknál.

---

## Step 4: Perform OCR on Image – Running the Recognition

Miután a kép betöltődött és a motor beállításra került, végre **perform OCR on image**. A `recognize` metódus egy `OcrResult` objektumot ad vissza, amely a kinyert szöveget és a biztonsági pontszámokat tartalmazza.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Mit ad vissza az `ocr_result`?**  
- `text`: a felismert karakterek egyszerű szövege.  
- `confidence`: egy float (0‑1) érték, amely az általános bizonyosságot jelzi.  
- `lines`: egy lista a sorobjektumokról, ha részletes vezérlésre van szükség.

> **Common question:** *Mi van, ha a szöveg fejjel lefelé van?*  
> `aocr` képes automatikusan elforgatni a képeket; csak állítsd be `ocr_engine.auto_rotate = True` a `recognize` hívása előtt.

---

## Step 5: Convert Image to Text Python – Post‑Processing the Output

A nyers karakterlánc tartalmazhat felesleges szóközöket vagy sortörés‑artefaktusokat. A **convert image to text python** stílusban néhány egyszerű lépéssel megtisztítjuk:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Miért érdemes?**  
A megtisztított kimenet könnyebben felhasználható további folyamatokban — legyen szó adatbázisba mentésről, fordító‑API‑hoz való továbbításról vagy regex‑es keresésről útlevél‑számok után.

---

## Step 6: Extract Cyrillic Text from Image – Putting It All Together

Csomagoljuk össze mindent egyetlen, újrahasználható függvénybe. Így a **extract Cyrillic text from image** egyetlen sorban meghívható a saját projektjeidben.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**A várt eredmény (példa):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Ha a kép éles és a betűtípus illeszkedik az OCR modellhez, majdnem tökéletes átírást kapsz.

---

## Hibaelhárítás és tippek

| Probléma | Valószínű ok | Megoldás |
|----------|--------------|----------|
| Torzuló karakterek | Rossz nyelvbeállítás | Győződj meg róla, hogy `ocr_engine.language = "cyrillic"` |
| Üres kimenet | A kép túl sötét vagy alacsony felbontású | Előfeldolgozás `opencv`‑val a kontraszt növeléséhez |
| Helytelen tájolás | A kép 90°‑kal el van forgatva | Állítsd be `ocr_engine.auto_rotate = True` |
| Lassú teljesítmény | Nagy kép (>5 MP) | Méretezés `aocr.Image.resize(width=1024)` használatával a felismerés előtt |

![OCR végrehajtása képen példa](ocr_example.png "OCR végrehajtása képen példa")

*Alt szöveg: “OCR végrehajtása képen példa, amely Python kódot mutat a cirill szöveg kinyeréséről egy útlevél beolvasásból.”*

---

## Következtetés

Most már **perform OCR on image** fájlokon tiszta Python‑mal, megtanultuk, hogyan **load image for OCR**, kényszerítettük a motor **recognize Cyrillic text** beállítását, és végül **extract Cyrillic text from image** egy rendezett segédfüggvénnyel. Az egész folyamat — az `aocr` telepítésétől a kimenet tisztításáig — néhány tucat sor kódban elfér, és bármelyik projektbe beilleszthető, amelynek **convert image to text python** stílusú megoldásra van szüksége.

---

## Mi következik?

- **Kötegelt feldolgozás:** Egy mappában lévő beolvasásokat ciklusba véve tárolja az eredményeket SQLite‑ben.  
- **Nyelvfelismerés:** Kombináld a `langdetect`‑et az `aocr`‑rel, hogy automatikusan váltson a cirill és latin között.  
- **Fejlett előfeldolgozás:** Használd az `opencv`‑t a kép kiegyenesítésére, zajcsökkentésre vagy binarizálásra a nagyobb pontosság érdekében.  
- **Integrálás FastAPI‑val:** Tedd elérhetővé az `extract_cyrillic_text` függvényt REST végpontként webalkalmazásokhoz.  

Nyugodtan kísérletezz — cseréld le a nyelvet „latin”‑ra angol útlevelekhez, vagy próbálj ki egy másik OCR backendet. A koncepciók ugyanazok, a kód pedig elég rugalmas ahhoz, hogy alkalmazkodjon.

Boldog kódolást, és legyenek mindig olvashatóak a képeid!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra építenek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd a további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeidben.

- [Kép szövegének kinyerése Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Kép konvertálása szöveggé – OCR végrehajtása képen URL‑ről](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Kép szövegének kinyerése C#‑ban nyelvválasztással az Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}