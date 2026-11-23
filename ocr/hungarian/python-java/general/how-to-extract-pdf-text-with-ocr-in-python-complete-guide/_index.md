---
category: general
date: 2026-06-19
description: Hogyan lehet PDF-et kinyerni OCR-rel Pythonban – lépésről lépésre útmutató,
  amely lefedi a PDF‑ből szöveg kinyerését, a képről szöveg felismerését, valamint
  egy OCR Python példát.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: hu
og_description: Hogyan lehet PDF-et kinyerni OCR-rel Pythonban. Tanulja meg, hogyan
  nyerjen ki szöveget PDF-ből, hogyan ismerje fel a szöveget képről, és tekintse meg
  a teljes OCR Python példát.
og_title: Hogyan vonjunk ki PDF‑szöveget OCR-rel Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Hogyan lehet PDF szöveget OCR-rel kinyerni Pythonban – Teljes útmutató
url: /hu/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan lehet PDF szöveget kinyerni OCR-rel Pythonban – Teljes útmutató

Gondolkodtál már azon, **hogyan lehet PDF‑et kinyerni**, ha a fájl csak egy beolvasott kép? Nem vagy egyedül. Sok valós projektben – legyen szó szerződésekről, számlákról vagy történelmi archívumokról – a kapott PDF nem tartalmaz választható szöveget. A jó hír? Néhány Python sorral ezeket a csak képet tartalmazó oldalakat kereshető, szerkeszthető szöveggé alakíthatod.

Ebben a tutorialban egy gyakorlati **OCR Python példát** mutatunk be, amely beolvas egy PDF‑et, megjeleníti az első oldalát képként, majd **kivonja a szöveget a PDF‑ből** egy OCR motor segítségével. A végére pontosan tudni fogod, hogyan **olvass PDF‑et OCR‑rel**, miért fontos minden lépés, és hogyan módosíthatod a kódot többoldalas dokumentumokhoz vagy más nyelvekhez.

## Mit fogsz megtanulni

- Megbízható OCR könyvtár telepítése és beállítása Pythonhoz.  
- PDF oldalak képekké konvertálása OCR‑ra alkalmas formátumba.  
- **Szöveg felismerése képről** és tiszta Unicode karakterláncok visszaadása.  
- Gyakori buktatók (alacsony felbontású PDF‑ek, elfordított oldalak) és azok elkerülése.  
- A szkript kiterjesztése több oldal vagy kötegelt feldolgozás kezelésére.

**Előfeltételek**: Python 3.8+, pip, és alapvető ismeretek a virtuális környezetekről. Korábbi OCR tapasztalat nem szükséges – csak kövesd a lépéseket.

---

## ## Hogyan lehet PDF szöveget kinyerni OCR-rel Pythonban

Ez a H2 fejléc tartalmazza a fő kulcsszót pontosan ott, ahol a keresőmotorok szeretik látni. Merüljünk el a kódban.

### 1. lépés – A szükséges csomagok telepítése

Először is szükségünk van egy OCR motorra. Az alábbi példa a népszerű **ocr** csomagot használja (egy könnyű wrapper a Tesseract köré). Ha másik backendet részesítesz előnyben, a koncepciók ugyanazok maradnak.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tipp:** Linuxon a Tesseract binárisra is szükséged lesz: `sudo apt-get install tesseract-ocr`. macOS felhasználók a Homebrew‑en keresztül telepíthetik: `brew install tesseract`.

### 2. lépés – Az OCR motor inicializálása és a nyelv beállítása

Most elindítjuk a motort, és megmondjuk, hogy angol karaktereket keressen. A `ocr.Language.English` helyett bármely támogatott nyelvkódot használhatsz.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Miért fontos:** A nyelv megadása drámaian javítja a pontosságot, mivel a motor nyelvspecifikus szótárakat és karaktermodelleket alkalmaz.

### 3. lépés – PDF oldal betöltése képként

Az OCR raster képeken működik, nem PDF objektumokon. Az `ocr.Image.from_pdf` segédfüggvény a kiválasztott oldalt bitmapre rendereli. Más oldalakhoz állítsd a `page_number` értékét (0‑alapú indexelés).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Különleges eset:** Ha a PDF vektoros grafikát tartalmaz a beolvasott képek helyett, tiszta renderelést kaphatsz. Alacsony felbontású beolvasásoknál fontold meg a DPI növelését: `ocr.Image.from_pdf(..., dpi=300)`.

### 4. lépés – Szöveg felismerése a renderelt képen

Itt van a **ocr python példa** szíve. A motor feldolgozza a bitmapet, és egy objektumot ad vissza, amely a kinyert karakterláncot tartalmazza.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Az `ocr_result.text` attribútum a sima szöveges kimenetet tartalmazza, ahol lehetséges, megőrizve a sortöréseket.

### 5. lépés – A kinyert szöveg kiírása vagy mentése

Végül kiírjuk az eredményt. Egy valódi alkalmazásban valószínűleg fájlba vagy adatbázisba írnád.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

A szkript futtatása valami ilyesmit kell, hogy megjelenítsen:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Ez egy komplett **extract text from pdf** munkafolyamat OCR‑rel.

---

## ## Szöveg felismerése képről – A pontosság finomhangolása

Ha csak a **recognize text from image** érdekel (például egy nyugta JPEG‑je), kihagyhatod a PDF konverziós lépést:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tippek a jobb eredményhez:**

- **Előfeldolgozás**: konvertáld szürkeárnyalatosra, alkalmazz küszöbölést vagy kiegyenesítést. A Pillow ezt egyszerűvé teszi.  
- **DPI növelése** PDF rendereléskor: a magasabb felbontás több részletet ad az OCR motor számára.  
- **OCR motor konfigurációjának engedélyezése** oldal szegmentáláshoz (`ocr_engine.config = "--psm 6"` egységes blokkokhoz).

---

## ## PDF olvasása OCR‑rel – Több oldal kezelése

A legtöbb szerződés több oldalas. Az egyes oldalak ciklusba helyezése egyszerű:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Ez a függvény **reads PDF with OCR**, összefűzi a kimenetet, és egy egyértelmű oldaltörés jelzőt szúr be. Ezután a `full_text` felhasználható keresőindexbe vagy `.txt` fájlként tárolható.

---

## ## Gyakori buktatók és megoldások

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| Elcsúszott karakterek, sok `?` | Rossz nyelv vagy hiányzó nyelvi adatfájlok | Telepítsd a megfelelő Tesseract nyelvi csomagot (`tesseract-ocr-<lang>`) és állítsd be az `ocr_engine.language`‑t. |
| Hiányzó sorok vagy levágott szavak | Alacsony DPI (150 alatti) | Rendereld a PDF‑et 300 DPI vagy magasabb értéken (`dpi=300`). |
| A szöveg elfordítva vagy fejjel lefelé | A beolvasott oldal nem álló helyzetben | Használd az `ocr.Image.deskew(page_image)`‑t a felismerés előtt. |
| Lassú feldolgozás nagy PDF‑eken | Oldalak soros feldolgozása egyetlen szálon | Párhuzamosítsd a `concurrent.futures.ThreadPoolExecutor`‑rel. |

---

## ## Az OCR Python példa kibővítése

- **Exportálás PDF/A‑ba**: Kinyerés után a szöveget visszaágyazhatod egy kereshető PDF‑be a `reportlab` vagy `pypdf2` segítségével.  
- **Nyelvfelismerés**: Használd a `langdetect`‑et az OCR kimeneten, hogy dinamikusan váltsd a `ocr_engine.language`‑t.  
- **Kötegelt feldolgozás**: Járj végig egy könyvtárat az `os.listdir`‑el, és alkalmazd az `extract_all_pages`‑t minden fájlra.

---

## ## Várt kimenet és ellenőrzés

Amikor a szkriptet egy tiszta, angol nyelvű beolvasáson futtatod, egy tiszta szövegrészt kell látnod megfelelő írásjelekkel. Ellenőrizd a következőkkel:

1. Hasonlíts néhány sort az eredeti beolvasott képpel.  
2. Futtass egy egyszerű szószámlálást (`len(ocr_result.text.split())`), hogy megbizonyosodj róla, hogy a kimenet nem üres.  
3. Opcionálisan add át az eredményt egy helyesírás-ellenőrzőnek, például a `pyspellchecker`‑nek, hogy megtaláld az OCR hibákat.

---

## Következtetés

Áttekintettük, **hogyan lehet PDF‑et kinyerni**, amikor a hagyományos elemzés kudarcot vall, bemutattuk a teljes **ocr python példát**, és elmagyaráztuk, hogyan **recognize text from image** és **read PDF with OCR** egy‑ és többoldalas esetekben. A fenti kódrészletekkel most már bármely beolvasott PDF‑et kereshető, szerkeszthető szöveggé alakíthatsz – többé nincs szükség kézi újraírásra.

Mi a következő lépés? Próbáld ki a nyelvet spanyolra (`ocr.Language.Spanish`) vagy kísérletezz képelőfeldolgozási technikákkal a pontosság növelése érdekében. Ha dokumentumkezelő rendszert építesz, gondold meg a kinyert szöveg indexelését Elasticsearch‑szel a villámgyors kereséshez.

Van kérdésed vagy furcsa PDF‑ed? Írj kommentet, és jó kódolást!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")


## Mit érdemes legközelebb megtanulni?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási módok felfedezésében a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}