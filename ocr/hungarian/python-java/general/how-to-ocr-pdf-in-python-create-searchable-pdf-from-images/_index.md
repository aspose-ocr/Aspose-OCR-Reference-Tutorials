---
category: general
date: 2026-06-06
description: Hogyan OCR-elj PDF-et, és hozz létre kereshető PDF-fájlokat képekből
  Python használatával. Tanulj meg kereshető szöveget hozzáadni és képet PDF/A formátumba
  konvertálni percek alatt.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: hu
og_description: Hogyan OCR-elj PDF-et lépésről lépésre. Tanulja meg, hogyan adjon
  hozzá kereshető szöveget, és konvertálja a képet PDF/A formátumba egy egyszerű Python
  szkript segítségével.
og_title: Hogyan OCR-elj PDF-et – Gyors útmutató kereshető PDF-ek létrehozásához
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Hogyan OCR-elj PDF-et Pythonban – Kereshető PDF létrehozása képekből
url: /hu/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan OCR PDF – Szkennelt képek átalakítása kereshető PDF‑ekké

Valaha is elgondolkodtál **hogyan OCR PDF-et** készíthetsz, ha csak egy szkennelt számla‑ vagy nyugta‑kép áll rendelkezésedre? Nem vagy egyedül. Sok irodában a beérkező papírok PNG‑ként vagy JPEG‑ként érkeznek, és a következő lépés – a tartalom kereshetővé tétele – gyakran fekete dobozként jelenik meg.  

A jó hír? Néhány Python‑sorral **kereshető PDF** fájlokat hozhatsz létre, **kereshető szöveget adhatsz hozzá**, sőt **kép‑PDF/A‑vá konvertálhatsz** hosszú távú archiváláshoz. Ebben a tutorialban lépésről lépésre végigvezetünk, elmagyarázzuk, miért fontos, és adunk egy azonnal futtatható szkriptet, amit bármely projektbe beilleszthetsz.

> **Pro tipp:** Ugyanez a megközelítés működik többoldalas szkeneknél is; csak iterálj a fájlokon, és a motor elvégzi a nehéz munkát.

---

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.9 vagy újabb | Modern szintaxis és jobb könyvtár‑támogatás |
| `pdfium`‑alapú OCR motor (pl. `pdfocr` vagy kereskedelmi SDK) | Képfelismerést és PDF/A generálást is kezel |
| Egy kép‑fájl (PNG, JPEG, TIFF), amit kereshető PDF‑é szeretnél alakítani | A szöveg forrása |
| Írási jogosultság a kimeneti mappához | Ahhoz, hogy a szkript el tudja menteni az új PDF‑et |

Ha még nem telepítetted az OCR SDK‑t, futtasd:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Ennyi – nincs bonyolult rendszer‑függőség, csak egy pip install.

---

## Hogyan OCR PDF – Áttekintés

Magas szinten a folyamat három egyszerű lépésből áll:

1. **Felismerni** a képen lévő szöveget, miközben az eredeti grafikát megőrizzük.  
2. **Exportálni** az OCR‑eredményt az eredeti képpel együtt **kereshető PDF/A‑ként** (az archiválásra optimalizált PDF‑változat).  
3. **Érvényesíteni**, hogy a kapott fájl tartalmazza a kiválasztható, kereshető szöveget a kép rétege felett.

Az alábbiakban minden lépést kóddal mutatunk be, a parancsok mögötti *miért* magyarázatával.

---

## 1. lépés: Szöveg felismerése a képből

Először megkérjük az OCR motort, hogy olvassa be a pixeleket, és adjon vissza egy eredményobjektumot, amely a nyers képet és a kinyert szöveget egyaránt tartalmazza. Gondolj rá úgy, mintha a motor „elolvasná” a számlát helyetted.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Miért fontos

- **A grafika megőrzése** azt jelenti, hogy a vizuális elrendezés (táblázatok, logók, pecsétek) pontosan úgy marad, ahogy a szkenner rögzítette.  
- A `result` objektum általában egy rejtett szövegréteget tartalmaz, amelyet később beágyazunk a PDF‑be.  
- A `recognize_image` használata a `recognize_pdf` helyett elkerüli a felesleges konverziós lépést, így gyorsabb a feldolgozás egyoldalas képek esetén.

#### Gyakori variációk

- Ha **többoldalas TIFF**‑ed van, add meg közvetlenül a fájl útvonalát; a legtöbb motor minden oldalt külön képként kezel.  
- PDF‑ek esetén, amelyek már tartalmaznak képeket, meghívhatod a `engine.recognize_pdf("file.pdf")`‑t, és kihagyhatod ezt a lépést teljesen.

---

## 2. lépés: OCR‑eredmény exportálása kereshető PDF/A‑ként

Most a 1. lépésből származó `result`‑ot átadjuk a motornak, hogy egy új fájlt írjon ki. A kulcsfontosságú jelző itt a *PDF/A* – az ISO‑szabványú PDF‑változat, amelyet hosszú távú megőrzésre terveztek.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Miért fontos

- **Kereshető PDF**: A kimeneti fájl egy rejtett, kiválasztható szövegréteget tartalmaz. Most már Ctrl + F‑el kereshetsz a dokumentumban.  
- **PDF/A megfelelőség**: Néhány szervezet (jogi, pénzügyi) megköveteli a PDF/A‑t audit‑nyomokhoz; ez a lépés automatikusan teljesíti ezt a szabályt.  
- A metódus **kereshető szöveget ad hozzá** anélkül, hogy a képet laposítaná, így a vizuális hűség tökéletes marad.

#### Szél eset: Normál PDF‑re van szükséged?

Ha nem érdekel a PDF/A, cseréld a `save_as_pdfa`‑t `save_as_pdf`‑re. A munkafolyamat többi része változatlan marad.

---

## 3. lépés: A kereshető PDF ellenőrzése

Egy gyors ellenőrzés megakadályozza a későbbi rejtélyes hibákat. Nyisd meg a generált fájlt bármely PDF‑olvasóval, próbálj ki egy szót kijelölni, és használd a keresőfunkciót.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Várt kimenet

A szkript futtatásakor a konzol a következőt írja ki:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

A fájl megnyitásakor az eredeti számla‑képnek kell látszania egy halvány, láthatatlan szövegréteggel. Jelölj ki bármely szót, és láthatod, hogy kiválasztható – **ez a kereshető szöveg**, amit most hozzáadtál.

---

## Kereshető szöveg hozzáadása meglévő PDF‑ekhez (Bónusz)

Néha már van egy PDF‑ed, de szükséged van **kereshető szöveg** hozzáadására. Ugyanaz a motor képes az OCR‑eredményeket egy meglévő PDF‑re rétegezni:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Itt a `apply_to` egyesíti a rejtett réteget az eredeti oldalakkal, így **kereshető PDF‑et hozhatsz létre** újraszkennelés nélkül.

---

## Gyakori hibák és tippek

| Hiba | Hogyan kerüld el |
|------|-----------------|
| **Alacsony felbontású forrásképek** (< 150 dpi) | Nagyíts fel, vagy kérj magasabb felbontású szkennt; az OCR pontossága drámaian csökken 150 dpi alatt. |
| **Hiányzó nyelvi adatok** | Telepítsd a megfelelő nyelvi csomagokat az OCR motorodhoz (`pip install pdfocr[eng,spa]`). |
| **A kimeneti mappa nem írható** | Futtasd a szkriptet megfelelő jogosultságokkal, vagy válassz másik könyvtárat. |
| **PDF/A validálás sikertelen** | Ügyelj arra, hogy ne ágyazz be nem támogatott betűtípusokat vagy JavaScript‑et; a legtöbb SDK automatikusan kezeli ezt a `save_as_pdfa` használatakor. |

---

## Teljes szkript – Egy‑fájlos megoldás

Az alábbi önálló szkript mindent összekapcsol. Másold be, cseréld ki a helyőrző útvonalakat, és máris **kép‑PDF/A‑vá konvertálhatsz** néhány másodperc alatt.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**A szkript működése:**  
1. Betölti az OCR motort.  
2. Beolvassa a kiválasztott képet, és kinyeri a szöveget.  
3. **Kereshető PDF/A**‑t ír, amelyet azonnal terjeszthetsz vagy archiválhatsz.  

Nyugodtan csomagold a `main` logikát egy függvénybe, amely egy egész mappát dolgoz fel – egyszerűen iterálj az `os.listdir()`‑en, és ismételd meg a három lépést minden fájlra.

---

## Következő lépések és kapcsolódó témák

Miután elsajátítottad, **hogyan OCR PDF-et**, érdemes ezeket a további ötleteket felfedezni:

- **Kötegelt feldolgozás:** Használd a `concurrent.futures`‑t, hogy egyszerre több tucat számlát OCR‑elj párhuzamosan.  
- **Metaadat‑injektálás:** Adj hozzá létrehozási dátumot vagy számlaszámot a PDF metaadataihoz a könnyebb indexelés érdekében.  
- **Hibrid PDF‑ek:** Kombináld a kereshető szöveget az eredeti képekkel, így egy „digitális ikertestet” kapsz a papír dokumentumról.  
- **Alternatív kimenetek:** Exportálj **DOCX**‑be vagy **HTML**‑be, ha a downstream rendszerek szerkeszthető formátumot igényelnek.

Mindegyik a most tanult alapfogalmakra épül – felismerés, export, ellenőrzés.

---

## Összegzés

Röviden, most már tudod, **hogyan OCR PDF-et** készíthetsz úgy, hogy egy egyszerű képet **kereshető PDF/A‑vá** alakítasz néhány Python‑sorral. A szkript elvégzi a nehéz munkát, megőrzi az eredeti grafikát, és egy szabványos, kereshető dokumentumot ad, amelyet archiválhatsz, megoszthatsz vagy tovább feldolgozhatsz.  

Próbáld ki a saját számláiddal, nyugtáiddal vagy szkennelt szerződéseiddel. Ha elakadsz, írj egy megjegyzést alább, vagy nézd meg az SDK hivatalos dokumentációját – általában rengeteg további példát tartalmaz. Boldog kódolást, és élvezd az új képességet, hogy bármely képet azonnal kereshetővé tegyél! 

![How to OCR PDF example showing original image and searchable PDF overlay](placeholder.png "How to OCR PDF example")

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is felfedezhess.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}