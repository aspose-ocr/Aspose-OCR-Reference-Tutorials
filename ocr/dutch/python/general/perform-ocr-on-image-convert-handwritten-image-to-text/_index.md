---
category: general
date: 2026-03-18
description: Voer OCR uit op een afbeelding en haal handgeschreven tekst uit een foto.
  Leer hoe je een handgeschreven afbeelding kunt converteren, tekst uit een jpg kunt
  extraheren en tekst uit een foto kunt herkennen.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: nl
og_description: Voer OCR uit op een afbeelding om handgeschreven tekst uit een foto
  te extraheren. Deze tutorial laat zien hoe je een handgeschreven afbeelding kunt
  omzetten en tekst kunt herkennen uit jpg‑bestanden.
og_title: Voer OCR uit op afbeelding – Complete gids voor handgeschreven tekst
tags:
- OCR
- Python
- Handwriting Recognition
title: Voer OCR uit op afbeelding – Converteer handgeschreven afbeelding naar tekst
url: /nl/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding – Full‑Stack handgeschreven tekstextractie

Heb je ooit **perform OCR on image** bestanden nodig gehad maar wist je niet of de engine rommelig handschrift kon lezen? Je bent niet de enige. In veel real‑world apps—denk aan uitgaven‑bon scanners of notitie‑hulpmiddelen—kom je foto’s tegen van krabbels die omgezet moeten worden naar platte tekst.  

In deze gids laten we je zien hoe je **convert handwritten image** bestanden, **extract text from jpg**, en zelfs **recognize text from photo** streams kunt gebruiken met een kleine Python‑achtige bibliotheek genaamd `ocr`. Aan het einde heb je een kant‑klaar script dat elk woord uit een handgeschreven notitie haalt, ongeacht hoe wankel de pen was.

## Wat je nodig hebt

- Python 3.8+ (de code werkt op elke recente interpreter)
- Het hypothetische `ocr` pakket – installeer het met `pip install ocr-lib` (vervang door de echte pakketnaam die je gebruikt)
- Een duidelijke foto van een handgeschreven notitie opgeslagen als `note.jpg` (of een ander afbeeldingsformaat)
- Een bescheiden hoeveelheid nieuwsgierigheid—geen geavanceerde ML‑achtergrond vereist

Dat is alles. Geen externe services, geen API‑sleutels, alleen een lokale engine die **perform OCR on image** gegevens kan verwerken.

![perform OCR on image screenshot die code‑editor met OCR‑script toont](example.png)

*Alt‑tekst: perform OCR on image screenshot die code‑editor met OCR‑script toont.*

## Stapsgewijze implementatie

Hieronder splitsen we het proces op in hapklare brokken. Elke kop bevat een trefwoord zodat je snel kunt scannen, en elk blok legt uit **why** we’re doing what we do—not just **what**.

### Stap 1: Installeer en verifieer de OCR‑bibliotheek

Voordat je **perform OCR on image** bestanden kunt verwerken, moet de bibliotheek aanwezig zijn in je omgeving. Open een terminal en voer uit:

```bash
pip install ocr-lib
```

> **Pro tip:** Als je in een virtuele omgeving werkt (sterk aanbevolen), activeer deze eerst. Dat houdt je afhankelijkheden netjes en voorkomt versieconflicten.

Na de installatie, laten we controleren of Python het pakket kan importeren:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Als je het succesbericht ziet, ben je klaar om **convert handwritten image** gegevens te verwerken.

### Stap 2: Maak een engine‑instantie en kies Handwritten‑modus

De meeste OCR‑engines staan standaard ingesteld op herkenning van gedrukte tekst. Omdat we **extract handwritten text** willen, moeten we de modus expliciet omschakelen. Deze stap is cruciaal omdat handschrift vaak andere voorbewerking vereist (zoals het gladstrijken van streken).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Waarom dit belangrijk is:* Handgeschreven tekens kunnen sterk variëren in grootte en helling. Door `RecognitionMode.HANDWRITTEN` in te stellen, past de engine een model toe dat getraind is op cursieve voorbeelden, waardoor de nauwkeurigheid aanzienlijk stijgt.

### Stap 3: Laad de foto die je wilt analyseren

Nu voeren we daadwerkelijk **perform OCR on image** content uit. De `load_image`‑methode accepteert een pad of een bestand‑achtig object. Voor demonstratie laden we een JPEG, maar dezelfde aanroep werkt voor PNG, BMP, of zelfs PDF‑pagina's.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Als je afbeelding zich in een cloud‑bucket bevindt, download deze dan eerst of geef een `BytesIO`‑stream door—`ocr` is flexibel genoeg om beide te verwerken.

### Stap 4: Voer het herkenningsproces uit

Met de engine klaar en de afbeelding in het geheugen, voeren we eindelijk **perform OCR on image** uit en halen we de ruwe tekst op.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

De `recognize()`‑aanroep retourneert een gewone Unicode‑string. Voor de meeste toepassingen kun je deze direct naar een `.txt`‑bestand schrijven, doorgeven aan een natural‑language‑pipeline, of weergeven in een GUI.

### Stap 5: Optioneel – Schoonmaken of post‑processen van de output

Handgeschreven OCR is niet perfect; je zult vaak vreemde regeleinden of verkeerd gelezen tekens zien. Een snelle schoonmaakstap kan de resultaten verderop verbeteren.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Voel je vrij om spell‑checkers, taalmodellen, of aangepaste regexes toe te voegen, afhankelijk van je domein.

### Volledig script – Klaar om te kopiëren & plakken

Door alles samen te voegen, hier is het volledige, uitvoerbare programma dat **extracts handwritten text** uit een JPEG haalt en een net resultaat afdrukt.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Verwachte output** (je daadwerkelijke tekst zal uiteraard verschillen):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Als je onzin ziet, controleer dan de beeldkwaliteit (goede belichting, minimale onscherpte) en zorg dat je in `HANDWRITTEN`‑modus bent. Deze twee factoren verklaren de meeste herkenningsfouten.

## Veelgestelde vragen (FAQ)

| Vraag | Antwoord |
|----------|--------|
| **Kan ik dit gebruiken om tekst uit een PNG te extraheren?** | Zeker. `engine.load_image("scan.png")` werkt op dezelfde manier. |
| **Wat als mijn afbeelding een PDF‑pagina is?** | Converteer de pagina eerst naar een afbeelding (bijv. met `pdf2image`) en geef deze vervolgens aan de engine. |
| **Is de bibliotheek thread‑safe?** | Ja, je kunt aparte `OcrEngine`‑objecten per thread instantieren. |
| **Hoe verschilt dit van `pytesseract`?** | `ocr` abstraheert de Tesseract‑binary en bevat een ingebouwd handgeschreven model, zodat je geen externe uitvoerbare bestanden hoeft te installeren. |
| **Wat als ik **extract text from JPG** bestanden in bulk moet verwerken?** | Plaats het script in een lus, of gebruik `engine.load_image` op elk bestand en verzamel de resultaten in een lijst of CSV. |

## Randgevallen & best practices

1. **Low‑contrast photos** – Verhoog het contrast programmatisch vóór het laden, of gebruik `engine.apply_preprocessing('contrast', level=2)`.
2. **Mixed printed & handwritten** – Voer twee passes uit: eerst met `HANDWRITTEN`, daarna met `PRINTED`, en voeg de resultaten samen.
3. **Large images** – Schaal down tot ongeveer 1500 px breedte; OCR‑engines werken meestal sneller met kleinere buffers zonder nauwkeurigheid te verliezen.
4. **Unicode characters** – De bibliotheek retourneert UTF‑8‑strings, zodat je emojis, letters met accenten, of wiskundige symbolen direct kunt verwerken.

## Samenvatting

We hebben zojuist een concreet voorbeeld doorgelopen van hoe je **perform OCR on image** bestanden kunt verwerken, specifiek gericht op handgeschreven notities. Door het `ocr`‑pakket te installeren, de engine te configureren voor `HANDWRITTEN`‑modus, een foto te laden, en `recognize()` aan te roepen, kun je **convert handwritten image** gegevens omzetten naar schone, doorzoekbare tekst.  

Vanaf hier kun je **extract text from jpg** bestanden in bulk verwerken, de output invoeren in een notitie‑app, of combineren met spraaksynthese voor toegankelijkheid. De mogelijkheden zijn eindeloos, en de bovenstaande code biedt een solide basis om mee te experimenteren.

Heb je een eigen draai die je wilt delen—misschien een ander bestandsformaat of een eigenzinnige voorbewerkings‑truc? Laat een reactie achter, en laten we het gesprek voortzetten. Veel plezier met coderen, en geniet van het omzetten van die krabbels naar digitale goud!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}