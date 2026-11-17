---
category: general
date: 2026-03-28
description: Leer hoe je PDF's snel kunt OCR'en met Python. Deze gids laat zien hoe
  je tekst uit PDF's kunt extraheren, tekst uit PDF's kunt herkennen en gescande PDF's
  naar tekst kunt converteren met Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: nl
og_description: Beheers hoe je PDF's OCR't met Python. Extraheer tekst uit PDF, herken
  tekst uit PDF en zet gescande PDF's in enkele minuten om naar tekst.
og_title: Hoe PDF OCR'en in Python – Complete gids
tags:
- PDF
- OCR
- Python
- Aspose
title: Hoe PDF OCR'en in Python – Stapsgewijze gids
url: /nl/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF OCR’en in Python – Stapsgewijze Gids

Heb je je ooit afgevraagd **hoe je PDF OCR’t** wanneer het bestand slechts een foto van een pagina is? Je bent niet de enige. In deze tutorial lopen we de exacte stappen door om PDF‑bestanden te OCR’en, tekst uit PDF te extraheren en een gescande PDF om te zetten naar doorzoekbare tekst – allemaal met eenvoudige Python‑code.

We behandelen alles, van het installeren van de Aspose OCR‑bibliotheek tot het ophalen van de herkende tekst van elke pagina. Aan het einde kun je **PDF OCR’en met Python**, **tekst uit PDF extraheren**, en **gescande PDF naar tekst converteren** zonder door verspreide documentatie te hoeven zoeken. Geen poespas, alleen een praktisch, uitvoerbaar voorbeeld dat je kunt copy‑pasten.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

* Python 3.8+ (de nieuwste stabiele release werkt het beste)  
* Een Aspose OCR for Python‑licentie of een gratis proeflicentiesleutel – te verkrijgen op de Aspose‑website.  
* Een gescande PDF die je wilt verwerken (we noemen deze `input.pdf`).  

Als je deze al hebt, prima – laten we beginnen. Zo niet, dan is het installeren van het pakket een fluitje van een cent en laten we je zien hoe.

## Hoe PDF OCR’en – De omgeving opzetten

Het eerste wat je moet doen is het Aspose OCR‑module op je machine krijgen. Het pakket heet `aspose-ocr`, en je kunt het installeren via pip:

```bash
pip install aspose-ocr
```

> **Pro tip:** Gebruik een virtuele omgeving (`python -m venv venv`) zodat je afhankelijkheden netjes blijven.

Zodra het pakket geïnstalleerd is, kun je het importeren en de OCR‑engine starten. Dit vormt de basis voor elke **ocr pdf with python**‑workflow die je later bouwt.

## OCR PDF met Python – Aspose OCR importeren

Nu de bibliotheek beschikbaar is, laten we hem in ons script laden. We stellen de engine ook in op *direct PDF‑mode*, waardoor Aspose de PDF‑bytes rechtstreeks uit het bestand leest in plaats van elke pagina eerst naar een afbeelding te converteren.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Waarom `PdfMode.DIRECT` gebruiken? Omdat het een extra rasterisatiestap overslaat, waardoor het proces sneller gaat en de oorspronkelijke lay‑out behouden blijft – vooral handig wanneer je **recognize text from PDF** nauwkeurig moet uitvoeren.

## Tekst uit PDF herkennen – De engine draaien

Met de engine klaar, wijs je deze op je gescande bestand. De methode `recognize_from_pdf` doet al het zware werk: hij parseert elke pagina, voert het OCR‑algoritme uit en retourneert een `OcrResult`‑object dat een verzameling `Page`‑objecten bevat.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Vraag je je af of dit werkt met versleutelde PDF’s? Ja, zolang je het wachtwoord opgeeft via `ocr_engine.password = "secret"` vóór je `recognize_from_pdf` aanroept. Dat is een randgeval dat veel tutorials overslaan, maar het is nuttig in real‑world pipelines.

## Tekst uit PDF extraheren – Paginaresultaten benaderen

De lijst `ocr_result.pages` bevat één entry per pagina. Elk `Page`‑object heeft een `.text`‑attribuut dat de platte‑tekstrepresentatie van de gescande pagina bevat. Laten we erdoorheen lopen en de resultaten afdrukken zodat je precies ziet wat er is geëxtraheerd.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Het uitvoeren van het script geeft iets als volgt weer:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Die output bewijst dat je succesvol **extract text from PDF** en **recognize text from PDF** hebt uitgevoerd met Aspose OCR. Je kunt de strings nu doorsturen naar een database, een zoekindex, of een downstream NLP‑pipeline.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")
*Afbeeldings‑alt‑tekst:* **voorbeeld van hoe pdf te OCR'en** – toont console‑output van herkende tekst per pagina.

## Gescande PDF naar tekst converteren – Output opslaan

De meeste ontwikkelaars willen de tekst niet alleen in de console zien; ze hebben een persistent bestand nodig. Hieronder staat een kleine helper die de tekst van elke pagina naar een apart `.txt`‑bestand schrijft, waardoor je **convert scanned PDF to text** uitvoert in een map genaamd `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Na afloop van het script heb je een nette directory:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Nu heb je volledig **convert scanned PDF to text** voltooid en kun je die bestanden in elke downstream‑procedure gebruiken – zoeken, analytics, of zelfs een eenvoudige `grep`.

## Veelgestelde vragen & randgevallen

**Wat als mijn PDF afbeeldingen bevat gemengd met echte tekst?**  
Aspose OCR probeert alles te herkennen, maar je kunt de snelheid verhogen door OCR uit te schakelen voor pagina’s die al selecteerbare tekst bevatten. Stel `ocr_engine.auto_detect_page_orientation = True` in en roep vervolgens `ocr_engine.recognize_from_pdf(..., detect_text=False)` aan voor bekende goede pagina’s.

**Kan ik het taalmodel regelen?**  
Zeker. Stel `ocr_engine.language = aocr.Language.English` (of een andere ondersteunde taal) in vóór je `recognize_from_pdf` aanroept. Dit verbetert de nauwkeurigheid voor niet‑Engelse documenten.

**Hoe ga ik om met zeer grote PDF’s (100+ pagina’s)?**  
Verwerk ze in delen. De methode `recognize_from_pdf` accepteert een `page_range`‑argument, bijvoorbeeld `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Loop over reeksen om het geheugenverbruik laag te houden.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is één script dat je kunt opslaan als `ocr_pdf.py` en uitvoeren:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Voer het uit met:

```bash
python ocr_pdf.py
```

Je zou console‑output moeten zien die de tekst van elke pagina bevestigt en de locatie van de opgeslagen `.txt`‑bestanden aangeeft.

## Conclusie

We hebben behandeld **hoe je PDF OCR’t** met Python, een nette manier laten zien om **ocr pdf with python** uit te voeren, laten zien hoe je **extract text from PDF** doet, de werking van **recognize text from PDF** uitgelegd, en tenslotte een kant‑klaar fragment gegeven dat **convert scanned PDF to text** uitvoert. Het volledige proces is nu compleet

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}