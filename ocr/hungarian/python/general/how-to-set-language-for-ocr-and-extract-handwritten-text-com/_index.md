---
category: general
date: 2026-03-26
description: Hogyan állítsuk be a nyelvet egy OCR motorban, és hogyan nyerjünk ki
  kézírásos szöveget képekből – lépésről lépésre útmutató a kép szöveggé konvertálásához.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: hu
og_description: Hogyan állíts be nyelvet egy OCR motorban, és hogyan nyerj ki kézírásos
  jegyzeteket a képekből. Tanuld meg, hogyan konvertálj képet szöveggé percek alatt.
og_title: Hogyan állítsuk be a nyelvet az OCR-hez – Kézírásos szöveg könnyű kinyerése
tags:
- OCR
- Python
- Image Processing
title: Hogyan állítsuk be a nyelvet az OCR-hez és nyerjünk ki kézírásos szöveget –
  Teljes útmutató
url: /hu/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a nyelvet az OCR-hez és vonjuk ki a kézírásos szöveget – Teljes útmutató

Gondolkodtál már azon, **hogyan állítsuk be a nyelvet** az OCR‑motoron, hogy tényleg megértse a szükséges karaktereket? Lehet, hogy van egy fényképed egy bevásárlólistáról, egy megbeszélés jegyzetéről, vagy egy vázlatos diagramról, és egyszerűen nem tudod kinyerni a szöveget. A jó hír? Nem kell PhD‑nek lenned a számítógépes látás területén – csak néhány Python sorra és a megfelelő kapcsolókra van szükség.

Ebben a tutorialban lépésről‑lépésre végigvezetünk a **kézírásos szöveg kinyerésének** pontos lépésein egy PNG‑ből, átalakítjuk a képet egyszerű szöveggé, és elmagyarázzuk a „miért” mögött álló beállításokat. A végére képes leszel kézírásos jegyzeteket felismerni bármely projektben, legyen az jegyzetkészítő alkalmazás vagy egy kötegelt feldolgozó csővezeték.

> **Ami szükséges**  
> • Python 3.8+ (a kód 3.10‑el is működik)  
> • A `ocr` könyvtár (vagy bármely kompatibilis wrapper, amely elérhetővé teszi a `OcrEngine`‑t)  
> • Egy minta kép, például `note_handwritten.png` – bármilyen kép, amely kiterjesztett latin karaktereket tartalmaz, megfelel.

Kezdjük is el.

---

## Hogyan állítsuk be a nyelvet és engedélyezzük a kézírásos felismerést

Az első dolog, amit meg kell tenned, hogy tájékoztasd az OCR‑motort, milyen ábécét várjon. Ha kihagyod ezt a lépést, a motor egy általános karakterkészletet használ, amely gyakran félreérti a diakritikus betűket vagy a speciális szimbólumokat.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Miért fontos ez:**  
- **ExtendedLatin** lefedi az olyan karaktereket, mint a „ñ”, „ø” és „ç”, amelyek sok európai jegyzetben gyakoriak.  
- A `recognize_handwritten` kapcsoló az alapmodellből a nyomtatott szöveg OCR‑ről egy kézírásra kiképzett neurális hálózatba vált. Enélkül a motor a karcokat zajként kezeli.

> **Pro tipp:** Ha több nyelven dolgozol, hozz létre külön motor példányt nyelvenként, vagy dinamikusan állítsd át a `ocr_engine.language`‑t minden hívás előtt. Ez elkerüli a nem használt karakterkészletek betöltésének többletterhelését.

![OCR motor konfigurációjának képernyőképe, amely megmutatja, hogyan állítsuk be a nyelvet](/images/ocr-set-language.png "Hogyan állítsuk be a nyelvet az OCR motoron")

*Kép alternatív szövege: „Hogyan állítsuk be a nyelvet az OCR motor konfigurációs képernyőjén.”*

---

## Kézírásos szöveg kinyerése PNG képből

Most, hogy a motor tudja, mit keressen, ideje egy képet betáplálni. A `recognize_image` metódus egy gazdag eredményobjektust ad vissza; a `text` attribútum tartalmazza a számodra fontos egyszerű sztringet.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

A szkript futtatásakor valami ilyesmit kell látnod:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

Ez a kimenet bizonyítja, hogy sikeresen **képet szöveggé alakítottál** és a motor tiszteletben tartotta a megadott nyelvi beállítást.

**Gyakori buktatók**  
- **Helytelen útvonal** – Ellenőrizd a fájl helyét; egy hiányzó fájl `FileNotFoundError`‑t dob.  
- **Alacsony felbontású kép** – A kézírásos OCR nehezen működik 300 dpi alatt. Nagyíts fel vagy szkenneld újra, ha a kimenet összezavartnak tűnik.  
- **Színinvertálás** – Ha a háttér sötét, a tinta pedig világos, előbb invertáld a színeket (`Pillow` segíthet).

---

## Kép szöveggé alakítása segédfüggvénnyel

Ha tucatnyi fájlon szeretnél OCR‑t futtatni, érdemes a logikát újrahasználható függvénybe csomagolni. Ez megkönnyíti a tesztelést és az integrációt más folyamatokkal.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

A segédfüggvény izolálja a **kézírásos kinyerés módját**, így meghívhatod Flask végpontról, CLI‑eszközből vagy kötegelt feladatból anélkül, hogy minden alkalommal újra beállítanád a konfigurációt.

---

## Kézírásos jegyzetek felismerése a valós életben

Az alábbiakban néhány tipikus helyzetet mutatunk be, ahol valószínűleg **kézírásos jegyzetek felismerésére** lesz szükséged, és hogy ez a beállítás hogyan alkalmazkodik:

| Szituáció | Miért fontos a nyelv | Javasolt módosítás |
|-----------|----------------------|--------------------|
| **Többnyelvű bevásárlólisták** | Az elemek gyakran tartalmaznak ékezetes betűket (pl. „crème”) | Válts `ocr_engine.language`‑t listánként, vagy használd a `ocr.Language.AutoDetect`‑et, ha támogatott |
| **Osztálytermi táblaképek** | A kréta gyakran gyenge vonalakat eredményez | Növeld a kép kontrasztját, mielőtt a motorba táplálnád |
| **Orvosi receptek** | A kézírás híresen rendezetlen | Párosítsd az OCR‑t egy helyesírás‑javító szótárral a gyógyszernevekre |

Minden esetben az alaplépések – **hogyan állítsuk be a nyelvet**, a kézírásos mód engedélyezése, és a `recognize_image` hívása – azonosak. Ez a konzisztencia teszi a megközelítést robusztussá és könnyen karbantarthatóvá.

---

## Szélsőséges esetek és haladó finomhangolások

1. **Kötegelt feldolgozás** – Töltsd be a motort egyszer, iterálj a fájlokon, és csak akkor módosítsd a `language` attribútumot, amikor szükséges. Ez csökkenti a inicializálási terhet.  
2. **Nem latin írásrendszerek** – Ha cirill vagy arab szöveget kell feldolgozni, cseréld le az `ExtendedLatin`‑t a megfelelő enumra (pl. `ocr.Language.Cyrillic`). Ugyanez a minta alkalmazandó.  
3. **Részleges felismerés** – Néha a motor üres stringet ad nagyon rövid vonalakra. Egy gyors ellenőrzés (`if not result.text.strip(): …`) lehetővé teszi, hogy visszatérj egy másodlagos modellhez vagy kérd a felhasználót az újraszkennelésre.  
4. **Teljesítményprofilozás** – Nagy adathalmazok esetén mérd az `recognize_image` hívás idejét. Ha szűk keresztmetszet lesz, fontold meg a párhuzamosítást a `concurrent.futures.ThreadPoolExecutor`‑rel.

---

## Teljes működő példa

Az alábbi teljes szkriptet másold be egy `handwritten_ocr.py` nevű fájlba. Argumentum‑feldolgozást is tartalmaz, így a parancssorból bármely képre mutathatsz.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Futtasd így:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

Ugyanazt a kimenetet kell látnod, mint a korábbi kódrészletben, ami megerősíti, hogy **képet szöveggé alakítottál** és **kézírásos jegyzeteket ismerél fel**.

---

## Összegzés

Áttekintettük, **hogyan állítsuk be a nyelvet** egy OCR‑motoron, bekapcsoltuk a kézírásos szöveg kapcsolót, és felépítettünk egy újrahasználható függvényt, amely **kézírásos szöveget nyer ki** bármely képből. A fenti lépéseket követve megbízhatóan **képet szöveggé alakíthatsz**, akár egyetlen jegyzetet, akár egy hatalmas szkennelt dokumentumarchívumot kezelsz.

Most próbálj ki különböző nyelvi csomagokat, kötegeld egy mappát képekkel, vagy integráld ezt a logikát egy webszolgáltatásba, amely JSON eredményt ad vissza. A alapelvek változatlanok, és az `ocr` könyvtár rugalmassága lehetővé teszi, hogy szinte bármilyen felhasználási esethez alkalmazkodj.

Van kérdésed a szélsőséges esetekkel, a teljesítménnyel vagy a script más nyelvekre való kiterjesztésével kapcsolatban? Írj kommentet vagy üzenj a GitHub‑on – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}