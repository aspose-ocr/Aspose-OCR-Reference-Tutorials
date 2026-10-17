---
category: general
date: 2026-06-06
description: Hogyan OCR-eljünk PDF-et Pythonban, szöveget nyerjünk ki PDF-ből, konvertáljuk
  a beolvasott PDF szövegét, és csak néhány kódsorral változtassuk meg az OCR nyelvét.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: hu
og_description: 'Hogyan OCR-elj PDF-et Python-nal: egy gyakorlati útmutató, amely
  megmutatja, hogyan lehet szöveget kinyerni PDF-ből, átalakítani a beolvasott PDF
  szöveget, és könnyedén megváltoztatni az OCR nyelvet.'
og_title: Hogyan OCR-elj PDF-et Pythonban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Hogyan OCR-eljünk PDF-et Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan OCR-elj PDF-et Pythonban – Teljes Lépésről‑Lépésre Útmutató

Gondoltad már valaha, **hogyan OCR-elj PDF** fájlokat anélkül, hogy drága SaaS eszközöket fizetnél? Nem vagy egyedül. Akár régi könyveket digitalizálsz, számlákról nyersz ki adatokat, vagy egyszerűen csak kereshető szöveget szeretnél egy beolvasott jelentésből, a PDF OCR Pythonban való elsajátítása órákat takaríthat meg a kézi másolástól.

Ebben a tutorialban egy tömör, működő példán keresztül vezetünk végig, amely **kivonja a szöveget a PDF-ből**, megmutatja, hogyan **alakítsd át a beolvasott PDF szöveget** szerkeszthető karakterláncokká, és még azt is bemutatja, hogyan **változtasd meg az OCR nyelvet**, ha a dokumentumod nem angol nyelvű. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely projektbe beilleszthetsz.

## Előkövetelmények és Beállítás

- Python 3.8+ telepítve (a kód 3.9, 3.10 és újabb verziókon is működik)
- Az `ocr` csomag, amely biztosítja az `OcrEngine` osztályt (telepítheted a `pip install ocr-lib` paranccsal – cseréld ki a tényleges csomagnévre)
- Egy PDF fájl, amelyet feldolgozni szeretnél; a demóhoz a `high_res_book.pdf` fájlt használjuk, amely a `YOUR_DIRECTORY` nevű mappában van

Ha virtuális környezetet használsz (erősen ajánlott), először aktiváld azt:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tipp:** Tartsd a PDF fájljaidat egy dedikált `data/` könyvtárban, hogy később elkerüld az útvonallal kapcsolatos fejfájást.

## 1. lépés: OCR Engine példány létrehozása (Hogyan OCR-elj PDF – Inicializálás)

Az első dolog, amit meg kell tenned, ha **PDF-en szeretnél OCR-t végezni**, az az engine példányosítása. Gondolj az engine-re úgy, mint az agyra, amely minden oldalt beolvas, értelmezi a glifeket, és egyszerű szöveget ad vissza.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Miért fontos: engine nélkül nincs kontextusod a nyelvi beállításokhoz, renderelési opciókhoz vagy a PDF kezeléséhez. Az `OcrEngine` objektum tartalmazza ezeket az alapértelmezéseket, és később finomhangolhatod őket.

## 2. lépés: Felismerési nyelv beállítása (OCR nyelv megváltoztatása)

A legtöbb OCR könyvtár alapértelmezés szerint angolt használ, de mi van, ha a dokumentumod francia, német vagy akár japán nyelvű? A nyelv megváltoztatása olyan egyszerű, mint a `set_recognition_language` meghívása. Ez teljesíti a **change OCR language** követelményt, és magasabb pontosságot biztosít.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Miért lehet erre szükséged:** Egy többnyelvű archívum gyakran vegyes nyelvű oldalakat tartalmaz. A nyelvek valós időben történő váltása megakadályozza a karakterek, például a “ß” vagy “ñ” helytelen felismerését.

## 3. lépés: PDF renderelési opciók konfigurálása (Beolvasott PDF szöveg hatékony átalakítása)

Beolvasott PDF-ekkel dolgozva a felbontás és a színmód drámaian befolyásolja az OCR minőségét. A 300 DPI-s, szürkeárnyalatos renderelés a legtöbb dokumentum számára ideális – elég magas a részletek rögzítéséhez, de alacsony ahhoz, hogy a memóriahasználat ésszerű maradjon.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

A láncolt hívások talán elegánsnak tűnnek, de valójában egy folyékony API-ról van szó, amely minden alkalommal ugyanazt az opcióobjektumot adja vissza. Ha színt szeretnél (például színes diagramokhoz), cseréld a `"grayscale"`-t `"color"`-ra.

## 4. lépés: PDF felismerése és az első oldal szövegének lekérése (Szöveg kinyerése a PDF-ből)

Most következik a **hogyan OCR-elj PDF** lényeges része: a motor átadása egy fájlútnak, és a felismert szöveg kinyerése. A metódus egy oldal eredmények listáját adja vissza; minden eredmény egy `text` attribútumot tartalmaz.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Ha az egész dokumentumra szükséged van, iterálj a `results`-en:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Mi van, ha a PDF titkosított?

Néhány PDF jelszóval védett. Ebben az esetben átadhatod a jelszót a `recognize_pdf`-nek:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Az engine a futás közben feloldja a titkosítást, mielőtt az OCR-t elvégezné – nincs szükség további lépésekre.

## 5. lépés: Kinyert szöveg utófeldolgozása (Finomhangolás a PDF szöveg kinyeréséhez)

A nyers OCR kimenet gyakran tartalmaz sortöréseket, felesleges szóközöket vagy időnként hibásan felismert karaktereket. Egy gyors tisztító rutin a kinyert karakterláncot készen áll a további feldolgozásra (kereső indexelés, adatbázis tárolás, stb.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Most már biztonságosan **kivonhatod a szöveget a PDF-ből**, és betáplálhatod bármely NLP csővezetékbe, keresőmotorba vagy egyszerű `open(...).write()` műveletbe.

## Bónusz: Több PDF kötegelt feldolgozása (OCR skálázása PDF-eken)

Ha egy mappád tele van beolvasott PDF-ekkel, csomagold a logikát egy ciklusba:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Ez a kódrészlet megmutatja, hogyan **perform OCR on PDF** fájlokat kötegelt módon, ami gyakori igény a digitalizációs projektekben.

## Várható kimenet

A egyoldalas példa (4. lépés) futtatása valami ilyesmit kell, hogy kiírjon:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Ha többoldalas könyvet dolgoztál fel, a konzol minden oldal tisztított szövegét megjeleníti, és a kötegelt szkript minden PDF mellé egy `.txt` fájlt hagy.

## Gyakori hibák és elkerülésük módja

| Probléma | Tünetek | Megoldás |
|----------|----------|----------|
| Alacsony felbontású forrás PDF | Torzuló karakterek, hiányzó szavak | Növeld a DPI-t (`set_dpi(400)` vagy magasabb) |
| Helytelen nyelv beállítva | Sok ismeretlen szimbólum, különösen ékezetes karakterek | Használd a `engine.set_recognition_language(ocr.Language.FRENCH)`-t vagy a megfelelő enumot |
| Nagy PDF memóriahibát okoz | `MemoryError` vagy összeomlás néhány oldal után | Dolgozd fel az oldalakat darabokban (`engine.recognize_pdf(..., max_pages=10)`) |
| Hiányzó betűkészletek a PDF-ben | Üres kimenet bizonyos oldalakon | Győződj meg róla, hogy a PDF valóban raszteres képeket tartalmaz; egyes PDF-ek csak vektorosak, és más kezelést igényelnek |

## Képi illusztráció

Alább egy gyors vizuális ábra a munkafolyamatról. Az alt szöveg szándékosan SEO‑barát.

![hogyan OCR-elj pdf munkafolyamat diagram, amely mutatja az engine inicializálását, nyelv beállítását, renderelési opciókat, felismerést és szöveg kinyerést](/images/ocr-workflow.png)

*A diagram nem szükséges a kód futtatásához, de segít a vizuális tanulóknak látni, hogy melyik lépés hova illeszkedik.*

## Következtetés

Áttekintettük, hogyan **OCR-elj PDF** fájlokat Pythonban a kezdetektől a végéig: OCR engine létrehozása, **OCR nyelv megváltoztatása**, a renderelés konfigurálása a **beolvasott PDF szöveg átalakításához**, és végül a **szöveg kinyerése a PDF-ből** további felhasználásra. A teljes, futtatható példa készen áll bármely projektbe beilleszteni, és a opcionális kötegelt szkript megmutatja, hogyan skálázható a megoldás.

Következő lépésként érdemes lehet:

- Többnyelvű archívumokhoz **perform OCR on PDF** hozzáadása nyelvlistán való iterálással.
- A kinyert szöveg integrálása Elasticsearch-be a teljes szöveges kereséshez.
- OCR használata kereshető PDF-ek létrehozásához, a szövegréteg visszaágyazásával az eredeti fájlba (számos könyvtár biztosít `save_as_searchable_pdf` metódust).

Nyugodtan kísérletezz, finomhangold a DPI beállításokat, vagy válts másik OCR backendre. Az alapok változatlanok, és most már szilárd alapod van a további fejlesztéshez.

Boldog kódolást, és legyenek a beolvasott dokumentumaid végre kereshetők!

## Mit érdemes következőként megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF szöveg felismerése – OCR műveletek Aspose.OCR-rel Java-hoz](/ocr/english/java/ocr-operations/)
- [Hogyan OCR-elj képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Hogyan OCR-elj PDF-et .NET-ben az Aspose.OCR-rel](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}