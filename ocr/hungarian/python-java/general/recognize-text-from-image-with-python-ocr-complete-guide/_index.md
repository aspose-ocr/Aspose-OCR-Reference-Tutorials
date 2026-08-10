---
category: general
date: 2026-06-16
description: Ismerje fel a szöveget a képről egy Python OCR motor segítségével – tanulja
  meg, hogyan nyerjen ki szöveget egy nyugtából, és percek alatt javítsa az OCR pontosságát.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: hu
og_description: Ismerje fel a szöveget a képről gyorsan. Ez az útmutató bemutatja,
  hogyan lehet kinyerni a szöveget egy nyugtáról, és javítani az OCR pontosságát Python
  használatával.
og_title: Képről szöveg felismerése Python OCR-rel – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Szöveg felismerése képről Python OCR-rel – Teljes útmutató
url: /hu/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg felismerése képről Python OCR‑rel – Teljes útmutató

Volt már, hogy **szöveget kellett felismerni egy képről**, de az eredmény csak értelmetlen karakterek voltak? Nem vagy egyedül. Sok kis‑vállalkozási helyzetben – gondolj a nyugták beolvasására, számlák digitalizálására vagy az adatgyűjtésre személyi igazolványokról – a tiszta, megbízható kimenet a zökkenőmentes munkafolyamat és a fejfájás közti különbség.

Ebben a tutorialban egy gyakorlati módszert mutatunk be a **szöveg felismerésére képről** egy könnyű Python OCR könyvtár segítségével. Bemutatjuk, hogyan **nyerhetünk ki szöveget nyugtákból**, és megosztunk trükköket a **OCR pontosság javítására** anélkül, hogy drága szoftvert kellene vásárolni. Készen állsz? Merüljünk el benne.

## Mit fogsz építeni

A útmutató végére egy kész‑futású szkriptet kapsz, amely:

1. Létrehozza az OCR motorját.  
2. Engedélyezi az intelligens előfeldolgozást (kiegyenesítés, zajszűrés, binarizálás).  
3. Betölti a zajos nyugta képet.  
4. Automatikusan lefuttatja a felismerési folyamatot.  
5. Kiírja a tiszta, kereshető szöveget a konzolra.

Nincsenek külső szolgáltatások, nincsenek rejtett API kulcsok – csak tiszta Python kód, amelyet bármilyen projekthez testre szabhatsz.

### Előfeltételek

- Python 3.8+ telepítve a gépeden.  
- Alapvető ismeretek a pip‑ről és a virtuális környezetekről.  
- Egy minta nyugta kép (JPEG vagy PNG), amelyet feldolgozni szeretnél.  
- Az `ocr` csomag (a példa egy fiktív `ocr` modult használ illusztrációként; cseréld le `pytesseract`‑ra, `easyocr`‑ra vagy bármely hasonló API‑t kínáló könyvtárra).

> **Pro tipp:** Ha hiányzó függőségekbe ütközöl, telepítsd őket a `pip install ocr` (vagy a valódi csomagnév) paranccsal, mielőtt folytatnád.

## 1. lépés – Szöveg felismerése képről: Motor beállítása

Először is szükségünk van egy objektumra, amely tudja olvasni a pixeladatokat és karakterekké alakítani őket. Tekintsd a motort a művelet agyának; minden más információt ad neki.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Miért hozunk létre motort manuálisan? Néhány könyvtár egyetlen függvényhívással is működik, de egy explicit példány finomhangolt vezérlést biztosít az előfeldolgozás felett – pontosan ez kell a **OCR pontosság javításához** később.

## 2. lépés – Szöveg kinyerése nyugtából: Előfeldolgozás engedélyezése

Egy telefonkamerával beolvasott nyugta ritkán tökéletes. Lehet, hogy enyhén ferde, porfoltokkal tarkított, vagy egyenetlen megvilágítású. Az előfeldolgozás elvégzi a nehéz munkát, mielőtt a motor még csak a betűket is látná.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*A kiegyenesítés* (deskew) egyenlíti a lapot, a *zajszűrés* (despeckle) eltávolítja a szóró foltokat, a *binarizálás* (binarization) pedig minden pixelt fekete‑fehérre állít. Ezek a három jelző egyedül **20‑30 %‑kal javíthatja az OCR pontosságát** zajos nyugták esetén.

## 3. lépés – A felismerni kívánt kép betöltése

Most a motort a tényleges fájlra irányítjuk. Az útvonal lehet abszolút vagy relatív; csak győződj meg róla, hogy a kép létezik.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Ha azon gondolkodsz, hogy a motor támogatja-e a PDF‑eket vagy a többoldalas TIFF‑eket, a legtöbb modern könyvtár igen – csak nézd meg a dokumentációt. Egy egyoldalas JPEG‑hez a fenti sor minden, amire szükséged van.

## 4. lépés – OCR futtatása – A motor elvégzi a többit

Az előfeldolgozás beállítva és a kép betöltve, a következő hívás mindent elvégez: előfeldolgozza, futtatja a felismerési algoritmust, és visszaad egy eredményobjektumot.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

A háttérben a motor használhat Tesseract‑ot, neurális hálót vagy egy saját fejlesztésű megoldást. Nem kell ismerned a belső működést; csak egy tiszta eredményt kapsz.

## 5. lépés – A felismert szöveg kiírása

Végül kinyerjük a sima szöveget az eredményből és kiírjuk. Egy valós alkalmazásban elmentheted adatbázisba, CSV‑fájlba, vagy akár egy downstream analitikai csővezetékbe is továbbíthatod.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Várt kimenet

Egy tipikus élelmiszerbolt nyugtán a szkript valahogy ilyesmit ad:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Ha a kimenet értelmetlennek tűnik, ellenőrizd, hogy az előfeldolgozási jelzők be vannak‑e kapcsolva, és hogy a kép nem túl sötét. A binarizálási küszöb finomhangolása (néhány könyvtár engedélyezi egy egyedi érték beállítását) további **OCR pontosság javítást** eredményezhet.

## Haladó: Finomhangolás a nyugták gyorsabb kinyeréséhez

Míg az öt lépéses folyamat a legtöbb esetben működik, előfordulhat, hogy éjszakánként több száz nyugtát kell feldolgozni. Íme néhány opcionális trükk:

### H3 – Kivágás a nyugta területére

Ha a képed sok háttérrel rendelkezik (pl. egy asztal fotója), előbb vágd le:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Egyedi nyelvi csomag használata

Ha a nyugták idegen karaktereket tartalmaznak (pl. “€” vagy “¥”), töltsd be a megfelelő nyelvi adatot:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Mindkét trükk segít a motor **szöveg felismerésében képről** megbízhatóbban, különösen ha a forrásanyag változatos.

## Gyakori hibák és elkerülésük módja

- **Hiányzó betűkészletek:** Egyes OCR motorok speciális nyugta betűtípusokhoz szükségük van a betűkészlet fájlokra. Telepítsd a megfelelő nyelvi csomagokat.  
- **Túl sok zaj:** Még a `despeckle=True` beállítás mellett is zavarhatják a nagyon szemcsés beolvasások a motort. Egy gyors manuális szűrő a Pillow‑ban (`Image.filter(ImageFilter.MedianFilter)`) segíthet.  
- **Helytelen DPI:** Az OCR motorok körülbelül 300 dpi‑t várnak. Ha a képed alacsonyabb, előbb méretezd át: `engine.image = engine.image.resize((width*2, height*2))`.

Ezeknek a problémáknak a közvetlen kezelése **javítja az OCR pontosságát** anélkül, hogy költséges harmadik fél szolgáltatásokhoz kellene fordulni.

## Teljes szkript – Kész a futtatásra

Az alábbiakban megtalálod a teljes, futtatható Python programot, amely mindent tartalmaz, amit eddig megbeszéltünk. Mentsd el `receipt_ocr.py` néven, majd futtasd `python receipt_ocr.py` paranccsal.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Ez a szkript **szöveget felismer képről**, és szép formázott nyugta adatblokkot nyomtat. Nyugodtan módosítsd a vágási koordinátákat, nyelvi beállításokat vagy előfeldolgozási jelzőket, hogy a saját nyugta elrendezésedhez illeszkedjenek.

## Összegzés

Bemutattuk, hogyan lehet egyszerűen **szöveget felismerni képről** Python segítségével, megmutattuk a **szöveg kinyerését nyugtákból**, és számos gyakorlati tippet adtunk a **OCR pontosság javítására**. Az alapgondolat egyszerű: állíts be egy OCR motort, engedélyezd az intelligens előfeldolgozást, adj neki egy tiszta képet, és hagyd, hogy a könyvtár végezze a nehéz munkát.

Mi a következő lépés? Próbálj meg egy köteg nyugtát egy ciklusban feldolgozni, minden eredményt CSV‑be menteni, vagy a kimenetet egy könyvelési rendszerbe integrálni. Kísérletezhetsz mélytanulás‑alapú OCR könyvtárakkal, például `easyocr`‑ral, hogy még nagyobb pontosságot érj el komplex betűtípusok esetén.

Van kérdésed egy adott nyugta formátummal kapcsolatban, vagy szeretnéd látni, hogyan kezeljünk többoldalas PDF‑eket? Írj egy megjegyzést alább, és boldog kódolást!


## Mit érdemes még tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}