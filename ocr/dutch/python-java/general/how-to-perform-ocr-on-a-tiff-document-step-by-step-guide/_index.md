---
category: general
date: 2026-01-12
description: Hoe OCR snel en nauwkeurig uit te voeren. Leer OCR op een document uit
  te voeren, tekst uit TIFF te extraheren, een afbeelding voor OCR te laden en de
  OCR-taal in Python in te stellen.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: nl
og_description: Hoe OCR uit te voeren in Python. Deze tutorial laat zien hoe je OCR
  op een document uitvoert, tekst uit een tiff extraheert, een afbeelding laadt voor
  OCR en de OCR-taal instelt.
og_title: Hoe OCR op een TIFF-document uit te voeren – Complete gids
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR uit te voeren op een TIFF‑document – Stapsgewijze handleiding
url: /nl/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op een TIFF‑document – Complete gids

Heb je je ooit afgevraagd **hoe je OCR** kunt uitvoeren op een gescande TIFF‑bestand zonder uren te verspillen aan het zoeken naar de juiste bibliotheek? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze tekst uit TIFF‑afbeeldingen moeten extraheren, vooral wanneer prestaties en taalinstellingen belangrijk zijn.

In deze tutorial lopen we alles door wat je moet weten: van het installeren van het OCR‑pakket, het laden van de afbeelding voor OCR, het instellen van de OCR‑taal, tot uiteindelijk **OCR uitvoeren op document** en schone tekst ophalen. Aan het einde heb je een kant‑klaar script dat je in elk project kunt gebruiken.

> **Pro tip:** Terwijl het voorbeeld een generieke `ocr`‑module gebruikt, zijn dezelfde concepten van toepassing op Tesseract, EasyOCR, of elke moderne OCR‑engine die een Python‑API biedt.

---

## Wat je nodig hebt

- Python 3.8+ (elke recente versie werkt)
- Een OCR‑bibliotheek die een `OcrEngine`‑klasse biedt (het voorbeeld gebruikt een fictief `ocr`‑pakket; vervang dit door je eigen)
- Een multi‑page TIFF‑bestand dat je wilt verwerken (we noemen het `big_document.tif`)
- Een machine met minimaal 4 CPU‑kernen als je het aantal threads wilt instellen

Geen externe services, geen cloud‑sleutels — alleen lokale code die in seconden draait.

![voorbeeld van OCR uitvoeren](/images/ocr-example.png "hoe OCR uit te voeren op een TIFF‑document")

*Afbeeldings‑alt‑tekst: hoe OCR uit te voeren op een TIFF‑document – voorbeeld van geëxtraheerde tekst.*

---

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Allereerst: haal de bibliotheek op je machine. De meeste OCR‑pakketten staan op PyPI, dus een simpele `pip install` doet het werk.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Importeer nu de klassen die je nodig hebt. Als je Tesseract gebruikt, ziet de import‑regel er anders uit, maar de rest van de code blijft hetzelfde.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Waarom dit belangrijk is:* Het vroegtijdig importeren van de juiste symbolen voorkomt later naamconflicten en maakt het script makkelijker leesbaar.

---

## Stap 2: Maak en configureer de OCR‑engine (Set OCR Language)

Het configureren van de engine is waar je **OCR‑taal instelt** voor nauwkeurige herkenning. Engels is de standaard, maar je kunt met één regel overschakelen naar Frans, Duits of zelfs een meertalige modus.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Waarom 4 threads?** De meeste moderne laptops hebben minstens vier kernen, en het beperken van het aantal threads voorkomt dat het OCR‑proces de hele machine opeet — dit is vooral handig wanneer het script op een gedeelde server draait.

Als je een andere taal nodig hebt, vervang je simpelweg `ocr.Language.ENGLISH` door `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, enzovoort.

---

## Stap 3: Laad afbeelding voor OCR (Load Image for OCR)

Nu **laden we de afbeelding voor OCR**. De `Image.load`‑methode leest het TIFF‑bestand in het geheugen en verwerkt multi‑page documenten automatisch.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Randgeval:* Als het bestand enorm is, kun je zonder RAM komen te zitten. Overweeg in dat scenario om één pagina per keer te laden met `Image.load_page(page_number)` (als de bibliotheek dat ondersteunt).

---

## Stap 4: OCR uitvoeren op document

Met de engine klaar en de afbeelding geladen, is het tijd om **OCR uit te voeren op document**. De `process`‑methode doet het zware werk en geeft een result‑object terug.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Achter de schermen splitst de engine de afbeelding in tekstblokken, voert het herkenningsmodel uit en voegt de resultaten samen. De oproep is blokkerend, wat betekent dat het script wacht tot de volledige TIFF is verwerkt — perfect voor batch‑taken.

---

## Stap 5: Tekst extraheren uit TIFF en output verifiëren

Tot slot **extraheren we tekst uit TIFF** door de `text`‑attribuut van het resultaat te benaderen. Laten we de eerste 200 tekens afdrukken als snelle sanity‑check.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Verwachte output (voorbeeld):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Als je de volledige tekst nodig hebt, gebruik je simpelweg `ocr_result.text`. Voor verdere verwerking wil je het misschien naar een `.txt`‑bestand schrijven:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een kant‑klaar script. Vervang de placeholder‑pakketnaam door de naam die je daadwerkelijk hebt geïnstalleerd.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Voer het script uit met:

```bash
python ocr_tiff_example.py
```

Je zou een preview in de console moeten zien en een bestand genaamd `extracted_text.txt` met de volledige transcriptie.

---

## Veelgestelde vragen & randgevallen

- **Wat als de TIFF meerdere pagina's bevat?**  
  De meeste OCR‑engines behandelen elke pagina intern als een aparte afbeelding. `ocr_result.text` bevat een regeleinde tussen pagina's. Als je per pagina wilt verwerken, itereer dan met `Image.load_page(page_number)`.

- **Kan ik een PNG of JPEG verwerken in plaats van TIFF?**  
  Zeker. De `Image.load`‑methode accepteert doorgaans elk formaat dat Pillow of de onderliggende bibliotheek ondersteunt. Verander gewoon de bestandsextensie.

- **Mijn tekst is onleesbaar — moet ik de taal wijzigen?**  
  Ja. De stap **OCR‑taal instellen** is cruciaal voor niet‑Engelse documenten. Zorg ervoor dat het taalpakket geïnstalleerd is (bijv. `tesseract‑lang‑fra` voor Frans).

- **Geen geheugen meer?**  
  Verlaag de `set_memory_limit` of verwerk pagina's één voor één. Sommige engines laten je ook de afbeelding verkleinen vóór herkenning.

---

## Conclusie

Daar heb je het — een beknopte, volledig functionele gids over **hoe OCR uit te voeren** op een TIFF‑bestand met Python. We hebben alles behandeld, van het installeren van de bibliotheek, het configureren van de engine (inclusief **OCR‑taal instellen**), **afbeelding laden voor OCR**, **OCR uitvoeren op document**, en uiteindelijk **tekst extraheren uit TIFF**.

Voel je vrij om te experimenteren: pas het aantal threads aan, wissel van taal, of voer de OCR‑output in een natural‑language‑pipeline. De mogelijkheden zijn eindeloos zodra je de basis onder de knie hebt.

Heb je meer vragen? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}