---
category: general
date: 2026-03-26
description: Skapa ROI‑polygon för att köra OCR på valt område. Lär dig hur du definierar
  flera regioner, registrerar dem och extraherar text med en Python‑OCR‑motor.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: sv
og_description: Skapa ROI-polygon och kör OCR på valt område med en Python-motor.
  Fullständig kod, förklaringar och tips ingår.
og_title: Skapa ROI-polygon – Snabb OCR på markerat område
tags:
- OCR
- Python
- Image Processing
title: Skapa ROI-polygon – Steg‑för‑steg‑guide för OCR på valt område
url: /sv/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ROI-polygon – Fullständig handledning för OCR på valt område

Har du någonsin behövt **create ROI polygon** så att du kan köra OCR på bara den del av en bild som är viktig? Kanske skannar du kvitton och bara totalbeloppen är relevanta, eller så har du ett formulär där bara signaturfältet behöver läsas. I sådana fall sparar **ocr on selected area** tid och ökar noggrannheten.  

I den här guiden går vi igenom allt du behöver: från att definiera två polygoner, registrera dem i en OCR‑motor, till att hämta den igenkända texten i ett enda rent anrop. När du är klar har du ett färdigt skript att köra och en solid förståelse för varför det är viktigt att fokusera på intresseområden.

## Vad du kommer att lära dig

- Hur du **create ROI polygon**‑objekt med ett typiskt OCR‑bibliotek.
- Skillnaden mellan att definiera ett enda område och flera.
- Hur du registrerar dessa områden i motorn så att `ocr on selected area` utförs.
- Förväntad output och hur du felsöker vanliga fallgropar (t.ex. överlappande ROI:er, tomma resultat).

### Förutsättningar

- Python 3.8+ installerat.
- Ett OCR‑bibliotek som exponerar `Polygon`, `Point` och `add_region_of_interest`‑metoder (exemplet använder ett fiktivt `ocr`‑modul; ersätt med ditt faktiska SDK, såsom Tesseract‑Python‑wrappers eller EasyOCR).
- En exempelbildfil (`sample.png`) som innehåller text inom de koordinater som visas nedan.

> **Pro tip:** Om du använder ett riktigt bibliotek, se till att bilden laddas i samma koordinatsystem (ursprung uppe till vänster, X ökar åt höger, Y ökar nedåt).  

---  

## Steg 1: Importera OCR-modulen och ladda din bild  

Först, importera OCR‑paketet och läs in bilden du vill bearbeta.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Varför detta är viktigt:* Motorn behöver bilddata innan du kan fästa någon **ROI polygon**. Vissa bibliotek låter dig också skicka bilden senare, men att initiera tidigt håller arbetsflödet prydligt.

## Steg 2: Definiera den första ROI-polygonen  

Nu skapar vi det första intresseområdet. Tänk dig att du ritar en rektangel runt en tabellrubrik.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Förklaring:*  
- `ocr.Point(x, y)` använder pixelkoordinater.  
- Listan med punkter är ordnad medurs, vilket de flesta motorer förväntar sig.  
- Du kan lägga till hur många punkter du vill för att skapa oregelbundna former; en rektangel är bara ett specialfall.

## Steg 3: Definiera ytterligare ROI-polygoner (valfritt)  

Du behöver inte stanna vid en. Här är en andra polygon som fångar ett signaturfält längre ner på sidan.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Varför lägga till fler?* Att köra **ocr on selected area** för flera zoner låter dig extrahera olika databit i ett enda pass, vilket är mycket snabbare än att beskära och bearbeta varje del separat.

## Steg 4: Registrera ROI:erna med OCR-motorn  

När polygonerna är klara, tala om för motorn vilka områden som ska inspekteras.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Viktigt att notera:* Vissa SDK:er kräver att du anropar en `clear_regions()`‑metod innan du lägger till nya om du återanvänder motorn för en annan bild.

## Steg 5: Kör OCR och hämta texten  

Till sist, starta igenkänningen. Motorn kommer bara att titta inom de polygoner vi just lagt till.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Förväntad output** (förutsatt att `sample.png` innehåller orden “Invoice Total: $123.45” i den första ROI:n och “Signature: John Doe” i den andra):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Om outputen är tom, dubbelkolla att koordinaterna faktiskt skär text och att bildens upplösning matchar koordinatsystemet.

## Kantfall & vanliga fallgropar  

| Situation                               | Vad du bör hålla utkik efter                     | Fix / Work‑around                              |
|----------------------------------------|--------------------------------------------------|-----------------------------------------------|
| **Overlapping ROIs**                    | Text kan returneras två gånger.                 | Håll polygonerna åtskilda eller deduplicera output. |
| **ROI outside image bounds**           | Motorn kan kasta ett fel eller returnera ingenting. | Begränsa koordinater till `0 ≤ x < width`, `0 ≤ y < height`. |
| **Very small ROI**                     | OCR‑noggrannheten sjunker på grund av för få pixlar. | Utöka polygonen några pixlar eller skala upp bilden först. |
| **Non‑rectangular shape**               | Vissa motorer stödjer bara konvexa polygoner.   | Dela upp komplexa former i flera konvexa ROI:er. |
| **Changing image size**                | Hårdkodade koordinater blir ogiltiga.           | Beräkna ROI‑koordinater relativt bildens dimensioner (t.ex. procent). |

## Fullt fungerande exempel  

Nedan är det kompletta skriptet som du kan kopiera‑klistra in och köra (ersätt `ocr` med ditt faktiska bibliotek).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Kör det med `python ocr_roi_example.py` så bör du se de extraherade strängarna från de två definierade zonerna.

## Nästa steg  

- **Dynamic ROI generation:** Istället för att hårdkoda koordinater, använd bildbehandling (t.ex. OpenCV‑konturdetektering) för att automatiskt lokalisera tabeller eller fält.  
- **Post‑processing:** Ta bort onödiga mellanslag, applicera regex‑uttryck, eller konvertera siffror till rätt datatyper.  
- **Batch processing:** Loop över en mapp med bilder och återanvänd samma ROI‑definitioner om layouten är konsekvent.  

Om du är nyfiken på **ocr on selected area** för mer komplexa dokument—tänk flersidiga PDF‑filer eller skannade formulär—undersök bibliotek som stödjer sid‑vis ROI‑registrering.  

---  

### Visuell översikt  

![Diagram som visar två ROI-polygoner på ett exempelbild](roi_diagram.png){alt="exempel på att skapa roi-polygon som visar två valda områden"}

---  

## Slutsats  

Vi har precis **created ROI polygon**‑objekt, registrerat dem i en OCR‑motor och utfört `ocr on selected area` i ett rent, reproducerbart skript. Genom att begränsa motorn till de zoner du bryr dig om, minskar du bearbetningstiden, förbättrar noggrannheten och gör efterföljande datahantering mycket enklare.  

Ge det ett försök med dina egna bilder—justera koordinaterna, lägg till fler polygoner, eller koppla outputen till en databas. Himlen är gränsen när du bemästrar region‑baserad OCR.  

Har du frågor eller vill dela ett coolt användningsfall? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}