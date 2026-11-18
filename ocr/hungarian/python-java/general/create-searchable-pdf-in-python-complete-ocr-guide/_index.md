---
category: general
date: 2026-06-22
description: Készíts kereshető PDF-et Pythonban OCR-rel – tanuld meg, hogyan konvertálj
  képet PDF-be, hogyan ismerj fel szöveget PDF-ben, és automatizáld a munkafolyamatodat.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: hu
og_description: Készíts kereshető PDF-et Pythonban OCR-rel. Kövesd ezt a lépésről‑lépésre
  útmutatót a kép PDF‑vé konvertáláshoz, a szöveg felismeréséhez PDF-ben, és a dokumentumfeldolgozás
  automatizálásához.
og_title: Kereshető PDF létrehozása Pythonban – Teljes OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Kereshető PDF létrehozása Pythonban – Teljes OCR útmutató
url: /hu/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Pythonban – Teljes OCR útmutató

Valaha is szükséged volt **kereshető PDF** létrehozására egy beolvasott szerződésből, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő ugyanabba a falba ütközik, amikor először próbálja a bitmap képet szöveg‑kereshető dokumentummá alakítani. A jó hír, hogy egy apró Python szkript segítségével **kép PDF‑re konvertálhatod**, az OCR motor minden szót felismert, és egy tökéletesen kereshető fájlt kapsz.

Ebben az útmutatóban végigvezetünk a teljes folyamaton, a megfelelő könyvtár telepítésétől a többoldalas dokumentumok kezeléséig. A végére képes leszel **ocr image to pdf**, **recognize text pdf** műveletekre, és beépítheted a munkafolyamatot nagyobb automatizációs csővezetékekbe.

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következőkkel rendelkezel a gépeden:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.8 vagy újabb | Modern szintaxis és jobb típusjelzések |
| `ocr` Python csomag (vagy bármely kompatibilis OCR SDK) | Biztosítja az `OcrEngine`, `ImageStream` és PDF kimenetet |
| Egy beolvasott kép (JPEG, PNG vagy TIFF) | A forrás, amit konvertálni fogsz |
| Írási jogosultság egy mappára a kimeneti PDF‑hez | Ahhoz, hogy el tudd menteni a generált fájlt |

Ha még nem telepítetted az SDK‑t, futtasd:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Pro tipp:** Használj virtuális környezetet (`python -m venv .venv`), hogy a függőségek rendezettek maradjanak.

## A munkafolyamat áttekintése

1. **OCR motor példány létrehozása** – a felismerés agya.  
2. **A kép betöltése**, amelyet feldolgozni szeretnél.  
3. **A motor konfigurálása**, hogy kereshető PDF‑et állítson elő a sima szöveg helyett.  
4. **Egy memória‑stream előkészítése**, amely a PDF bájtjait tárolja.  
5. **A felismerés futtatása** – a motor beolvassa a képet, kinyeri a szöveget, és megírja a PDF‑et.  
6. **A PDF mentése lemezre**, hogy bármely megjelenítővel megnyithasd.

Ez a teljes történet hat kódsorban. Nézzük meg részletesen az egyes lépéseket.

---

## Kereshető PDF létrehozása – Lépés‑ről‑lépésre Python OCR útmutató

### Lépés 1: Az OCR motor inicializálása

Az első dolog, amit megteszel, egy `OcrEngine` objektum létrehozása. Olyan, mintha bekapcsolnád a szkennert, amely készen áll a képed olvasására.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Miért fontos:** A motor példányosítása belső puffereket foglal le és betölti a nyelvi adatokat. Ennek kihagyása később `NoneType` hibát eredményez, amikor megpróbálod beállítani a képet.

### Lépés 2: A konvertálni kívánt kép betöltése

Ezután a motorhoz egy képadat‑streamet adunk. Az `ImageStream.from_file` segédfüggvény beolvassa a fájlt és olyan formátumba csomagolja, amit az OCR motor ért.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Szélsőséges eset:** Ha a forrásod többoldalas TIFF, használd helyette az `ocr.MultiPageImageStream.from_file`‑t. A motor automatikusan minden oldalt külön PDF‑oldalként kezel.

### Lépés 3: A motor beállítása kereshető PDF kimenetre

Alapértelmezés szerint sok OCR SDK sima szöveget ad vissza. Át kell állítanunk a kimeneti formátumot PDF‑re, hogy a kapott fájl vizuálisan is megjeleníthető és kereshető legyen.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **Mi történik a háttérben?** A motor egy láthatatlan szövegréteget ágyaz be a bitmap mögé, így a szavak kereshetők, mint egy natív PDF‑ben.

### Lépés 4: Memória‑stream előkészítése a PDF adatokhoz

Ahelyett, hogy közvetlenül a lemezre írnánk, a PDF‑et egy `MemoryStream`‑ben tartjuk. Ez gyors I/O‑t biztosít, és lehetővé teszi, hogy a bájtokat máshová is továbbítsd (pl. S3‑ra feltöltés).

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Lépés 5: A felismerés futtatása és a PDF írása

Most jön a nehéz munka. A `recognize` hívás beolvassa a képet, futtatja az OCR‑t, és a kereshető PDF‑et a `pdf_stream`‑be streameli.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Gyakori buktató:** Ha elfelejted meghívni az `engine.recognize`‑t, a `pdf_stream` üres marad, és a mentés `ValueError`‑t dob. Mindig ellenőrizd a `pdf_stream.length` értékét, ha biztosra akarsz menni, hogy adat keletkezett.

### Lépés 6: A generált PDF mentése fájlba

Végül a memória‑stream bájtjait a lemezre írjuk. A kapott fájl megnyitható Adobe Reader‑rel, Preview‑vel vagy bármely PDF‑megtekintővel, amely támogatja a teljes‑szöveges keresést.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Eredmény, amit látnod kell:** Nyisd meg a PDF‑et, nyomd meg a `Ctrl+F`‑et, gépeld be egy olyan szó első betűit, ami az eredeti beolvasott dokumentumban is szerepel, és a megjelenítő azonnal kiemeli. Ez a **kereshető PDF** jelképe.

---

## Kép PDF‑re konvertálása – Beállítások finomhangolása a legjobb eredményért

Ha az elsődleges célod egyszerűen **kép PDF‑re konvertálása** OCR nélkül, kihagyhatod a 3. lépést, és beállíthatod a kimeneti formátumot `ocr.OutputFormat.IMAGE_PDF`‑ra. A motor a bitmapet PDF‑oldalként ágyazza be, rejtett szövegréteg nélkül.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Ezt a módot akkor használd, ha egy hű vizuális másolatra van szükséged, de a kereshetőség nem fontos – például archiválási célokra, ahol az OCR nem kötelező.

---

## Szöveg‑PDF felismerése – Nyelvi csomagok és DPI vezérlése

Egy robusztus **recognize text PDF** élményhez fontold meg a következő opcionális finomhangolásokat:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Miért állítsd be a DPI‑t?** A magasabb felbontás több pixelt biztosít az OCR motor számára, ezáltal csökkentve a hibás felismeréseket alacsony minőségű beolvasásoknál.

---

## Python OCR PDF – Integrálás nagyobb csővezetékekbe

Most, hogy néhány sor kóddal **python ocr pdf**‑t tudsz végrehajtani, képzeld el, hogy ezt a logikát egy Flask API‑ba ágyazod:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Ez a kis végpont lehetővé teszi, hogy egy kliens POST‑oljon egy képet, és azonnal kapjon egy **kereshető PDF**‑et – tökéletes SaaS dokumentum‑feldolgozó szolgáltatásokhoz.

---

## Gyakori buktatók, amikor **ocr image to pdf**-t használsz

| Tünet | Valószínű ok | Javítás |
|-------|--------------|---------|
| Üres PDF oldalak | Kép nem lett betöltve (`engine.set_image` rossz úttal hívták) | Ellenőrizd az útvonalat, és használd az `os.path.abspath`‑t |
| Nincs kereshető szöveg | Kimeneti formátum még mindig `IMAGE_PDF`-re van állítva | Kifejezetten hívd meg a `set_output_format(ocr.OutputFormat.PDF)`‑t |
| Torz karakterek | Rossz nyelvi csomag | Töltsd be a megfelelő nyelvet a `settings.set_language("eng")`‑vel |
| Lassú feldolgozás nagy fájloknál | Alapértelmezett DPI (72) használata nagy felbontású képeknél | Növeld a DPI‑t 300-ra, vagy oldalakra bontva batch‑elj |

---

## Teljes, futtatható példa (másolás‑beillesztés kész)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Futtasd a szkriptet, nyisd meg a generált PDF‑et, és próbálj meg keresni egy olyan szót, amely biztosan szerepel az eredeti beolvasott dokumentumban. Ha minden simán ment, most már magabiztosan tudsz **create searchable pdf**‑et készíteni Python segítségével.

---

## Összegzés

Áttekintettük mindent, ami ahhoz kell, hogy **kereshető PDF** fájlokat hozzunk létre egy Python OCR könyvtárral: a motor inicializálása, kép betöltése, PDF kimenet beállítása, az eredmény streamelése, és végül a lemezre mentése. Emellett megmutattuk, hogyan **convert image to PDF**, valamint a finomhangolásokat is.

## Mit érdemes még tanulni?

A következő oktatóanyagok szorosan kapcsolódnak ehhez a témához, és a bemutatott technikákra építenek. Minden forrás komplett, működő kódrészleteket tartalmaz lépés‑ről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhasd.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}