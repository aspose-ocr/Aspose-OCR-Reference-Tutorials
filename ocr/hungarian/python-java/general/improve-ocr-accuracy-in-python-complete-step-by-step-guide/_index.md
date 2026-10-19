---
category: general
date: 2026-05-31
description: Javítsd az OCR pontosságát Python segítségével a képek előfeldolgozásával.
  Tanuld meg, hogyan lehet szöveget kinyerni képfájlokból, PNG-ből felismerni, és
  fokozni az eredményeket.
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: hu
og_description: Növelje az OCR pontosságát Pythonban képfeldolgozással a szöveghez.
  Kövesse ezt az útmutatót, hogy könnyedén kinyerje a szöveget képfájlokból, és felismerje
  a PNG-kből a szöveget.
og_title: OCR pontosságának javítása Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR pontosságának javítása Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR pontosság javítása Pythonban – Teljes lépésről‑lépésre útmutató

Próbáltad már **javítani az OCR pontosságát**, csak hogy összezavart kimenetet kapj? Nem vagy egyedül. A legtöbb fejlesztő elakad, amikor a nyers kép zajos, ferde vagy egyszerűen alacsony kontrasztú. A jó hír? Néhány előfeldolgozási trükkel egy homályos képernyőképet tiszta, gép‑olvasható szöveggé alakíthatunk.

Ebben a tutorialban egy valós példán keresztül mutatjuk be, hogyan **előfeldolgozzuk a képet OCR‑hez**, futtatjuk a felismerő motorját, és végül **kivonjuk a szöveget a képfájlból** – konkrétan egy PNG‑ből. A végére pontosan tudni fogod, hogyan **ismerjünk fel szöveget PNG‑ből** magasabb sikerarány mellett, és kapsz egy újrahasználható kódrészletet, amit bármely projektbe beilleszthetsz.

## Mit fogsz megtanulni

- Miért fontos a kép‑előfeldolgozás az OCR motorok számára  
- Mely előfeldolgozási módok (denoise, deskew) adnak a legnagyobb lökést  
- Hogyan konfigurálj egy `OcrEngine` példányt Pythonban  
- A teljes, futtatható szkript, amely **kivonja a szöveget a képfájlból**  
- Tippek a szélhelyzetek kezeléséhez, például elfordított szkennek vagy alacsony felbontású képeknek  

Nem szükséges külső könyvtár az OCR SDK‑n kívül, de Python 3.8+ és egy PNG kép szükséges, amelyet be szeretnél olvasni.

---

![Diagram showing steps to improve OCR accuracy in Python](image.png "Improve OCR accuracy workflow")

*Alt szöveg: OCR pontosság javításának munkafolyamatai, amely bemutatja az előfeldolgozási és felismerési lépéseket.*

## Előfeltételek

- Python 3.8 vagy újabb telepítve  
- Hozzáférés az OCR SDK‑hoz, amely biztosítja az `OcrEngine`, `OcrEngineSettings` és `ImagePreprocessMode` osztályokat (az alábbi kód egy általános API‑t használ; szükség esetén cseréld ki a saját szállítód osztályaira)  
- Egy PNG kép (`input.png`) egy olyan mappában, amelyre hivatkozhatsz  

Ha virtuális környezetet használsz, aktiváld most – semmi bonyolult, csak `python -m venv venv && source venv/bin/activate`.

---

## 1. lépés: OCR motor példány létrehozása – Kezdjük az OCR pontosság javítását

Az első dolog, amire szükséged van, egy OCR motor objektum. Gondolj rá úgy, mint az agyra, amely később a pixeleket olvassa és karaktereket ad ki.

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

Miért fontos: motor nélkül nem tudsz semmilyen előfeldolgozást alkalmazni, és a nyers képet közvetlenül a felismerőnek adod – ami általában a legrosszabb eset a pontosság szempontjából.

---

## 2. lépés: Cél PNG betöltése – A színpad felállítása a „Recognize Text from PNG” számára

Most megmondjuk a motornak, melyik fájlon dolgozzon. A PNG veszteségmentes, ami már egy kis előnyt jelent a JPEG‑hez képest.

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

Ha a kép máshol van, csak módosítsd az elérési utat. A motor bármely támogatott formátumot elfogad, de a PNG gyakran megőrzi a finom részleteket, amelyek a tiszta karakterélekhez szükségesek.

---

## 3. lépés: Előfeldolgozás beállítása – Preprocess Image for OCR

Itt történik a varázslat. Létrehozunk egy beállítási objektumot, engedélyezzük a zajszűrést a foltok eltávolításához, és bekapcsoljuk a ferde szöveg automatikus kiegyenesítését.

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### Miért Denoise + Deskew?

- **Denoise**: A véletlenszerű pixelzaj összezavarja a mintázat‑illesztő algoritmusokat. A zaj eltávolítása élesíti a betűket.  
- **Deskew**: Már egy 2‑fokos ferdeség is drámaian csökkentheti a bizalmi pontszámokat. A deskew kiegyenesíti az alapvonalat, így a felismerő megbízhatóbban tudja párosítani a betűtípusokat.

Kísérletezhetsz további flag‑ekkel (pl. `ImagePreprocessMode.CONTRAST_ENHANCE`), ha a képeid különösen sötétek. Az SDK dokumentációja általában felsorolja az összes elérhető módot.

---

## 4. lépés: Beállítások alkalmazása a motorra – Tie Preprocessing to OCR

Rendeld hozzá a beállítási objektumot a motorhoz, hogy a következő felismerési futtatás a most definiált transzformációkat használja.

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

Ha kihagyod ezt a lépést, a motor az alapértelmezett beállításokra (gyakran „nincs előfeldolgozás”) tér vissza, és **alacsonyabb OCR pontosságot** fogsz tapasztalni.

---

## 5. lépés: A felismerési folyamat indítása – Extract Text from Image

Miután mindent összekapcsoltunk, végül megkérjük a motort, hogy végezze el a feladatát. A hívás szinkron, egy eredményobjektumot ad vissza, amely a felismert szöveget tartalmazza.

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

A motor a háttérben most:

1. Betölti a PNG‑t a memóriába  
2. Alkalmazza a denoise‑t és a deskew‑et a beállításaink alapján  
3. Fut a neurális háló vagy a klasszikus mintázat‑illesztő  
4. Az eredményt a `recognition_result`‑ba csomagolja  

---

## 6. lépés: A felismert szöveg kiírása – Verify the Improvement

Nyomtassuk ki a kinyert karakterláncot. Egy valós alkalmazásban fájlba, adatbázisba vagy egy másik szolgáltatásba is továbbíthatod.

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### Várható kimenet

Ha a kép a „Hello, OCR World!” mondatot tartalmazza, a következőt kell látnod:

```
Hello, OCR World!
```

Figyeld meg, hogy a szöveg tiszta – nincsenek idegen szimbólumok vagy törött karakterek. Ez a megfelelő **image preprocessing for text** eredménye.

---

## Pro tippek & szélhelyzetek

| Szituáció | Mit kell módosítani | Miért |
|-----------|---------------------|-------|
| Nagyon alacsony felbontású PNG (≤ 72 dpi) | Add hozzá az `ImagePreprocessMode.SUPER_RESOLUTION` flag‑et, ha elérhető | Az upsampling több pixelt ad a felismerőnek, így jobb eredményt érhet el |
| A szöveg > 5°‑kal elfordult | Növeld a deskew toleranciát vagy előbb manuálisan forgasd el a képet a `Pillow`‑al, mielőtt a motorhoz adnád | A szélsőséges szögek néha megkerülik az automatikus deskew‑et |
| Erős háttérminták | Engedélyezd az `ImagePreprocessMode.BACKGROUND_REMOVAL` flag‑et | Eltávolítja a nem‑szöveges zajt, amely egyébként félreolvasásra késztethet |
| Többnyelvű dokumentum | Állítsd be `ocr_engine.language = "eng+spa"` (vagy hasonló) | A motor a megfelelő karakterkészletet választja, ezáltal javítva a teljes pontosságot |

Ne feledd, a **improve OCR accuracy** nem egy mindenki számára egyforma megoldás; a saját adatkészletedhez valószínűleg iterálni kell a előfeldolgozási flag‑eken.

---

## Teljes szkript – Kész a másolásra és beillesztésre

Az alábbiakban megtalálod a teljes, futtatható példát, amely tartalmazza a megbeszélt minden lépést. Mentsd el `improve_ocr_accuracy.py` néven, és futtasd a `python improve_ocr_accuracy.py` paranccsal.

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

Futtasd, figyeld a konzolt, és azonnal látnod kell a **extract text from image** eredményt. Ha a kimenet nem megfelelő, finomhangold a `preprocess_mode` flag‑eket a “Pro tippek” táblázatban leírtak szerint.

---

## Összegzés

Átmentünk egy gyakorlati recepten, amely **javítja az OCR pontosságát** Python segítségével. Létrehoztunk egy `OcrEngine`‑t, betöltöttünk egy PNG‑t, **előfeldolgoztuk a képet OCR‑hez**, és végül **szöveget ismerünk fel PNG‑ből**, így megbízhatóan **kivonjuk a szöveget a képfájlból**, még ha a forrás nem is tökéletes.  

Mi a következő lépés? Próbálj meg egy képcsomagot egy ciklusban feldolgozni, az eredményeket CSV‑be menteni, vagy kísérletezni további előfeldolgozási módokkal, például kontrasztjavítással. Ugyanez a minta PDF‑ekhez, beolvasott számlákhoz vagy kézírásos jegyzetekhez is működik – csak cseréld ki a bemenetet és állítsd be a paramétereket.

Van kérdésed egy konkrét kép típussal kapcsolatban, vagy szeretnéd tudni, hogyan integráld ezt egy webszolgáltatásba? Írj kommentet, és együtt vizsgáljuk meg a szcenáriókat. Boldog kódolást, és legyen a OCR eredményed mindig kristálytiszta!

## Mit érdemes még tanulni?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}