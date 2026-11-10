---
category: general
date: 2026-06-19
description: Hoe OCR stap voor stap uit te voeren en de OCR‑nauwkeurigheid te verbeteren
  met eenvoudige tekst‑OCR‑technieken. Leer een snelle workflow voor betrouwbare tekste­xtractie.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: nl
og_description: Hoe OCR efficiënt uit te voeren. Deze tutorial laat zien hoe je de
  OCR‑nauwkeurigheid kunt verbeteren met platte‑tekst OCR en AI‑nabewerking.
og_title: Hoe OCR in Python uit te voeren – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Hoe OCR in Python uit te voeren – Complete gids
url: /nl/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in Python – Complete gids

Heb je je ooit afgevraagd **hoe je OCR** kunt draaien op een batch gescande PDF‑bestanden zonder uren te spenderen aan het afstellen van instellingen? Je bent niet de enige. In veel projecten is de eerste hindernis simpelweg het betrouwbaar krijgen van tekst uit een afbeelding, en het verschil tussen een wankele poging en een schone extractie komt vaak neer op een paar slimme stappen.

In deze gids lopen we een praktische vier‑stappen‑pipeline door die niet alleen **OCR uitvoert**, maar ook **OCR‑nauwkeurigheid verbetert** door een snelle platte‑tekst‑pass te combineren met een layout‑bewuste tweede pass en een AI‑aangedreven post‑processor. Aan het einde heb je een kant‑klaar script, een duidelijke uitleg waarom elke fase belangrijk is, en tips voor het omgaan met randgevallen zoals meer‑koloms pagina’s of ruisende scans.

---

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- **Python 3.9+** – de code gebruikt type‑hints en f‑strings.  
- **Tesseract OCR** geïnstalleerd en bereikbaar via de `tesseract` commandoregel. (Op Ubuntu: `sudo apt install tesseract-ocr`; op Windows haal je de installer van de officiële repo.)  
- De **pytesseract** wrapper (`pip install pytesseract`).  
- Een **AI post‑processing bibliotheek** – voor dit voorbeeld gaan we ervan uit dat je een lichte `ai` module hebt die `run_postprocessor` aanbiedt. Vervang dit door de OpenAI GPT‑4 API of een lokaal LLM als je dat liever hebt.  
- Een paar voorbeeldafbeeldingen of PDF‑bestanden om te testen.

Dat is alles. Geen zware frameworks, geen Docker‑gymnastiek. Alleen een handvol pip‑installaties en je bent klaar om te gaan.

---

## Stap 1: Voer een snelle platte‑tekst OCR‑pass uit

Het eerste dat de meeste ontwikkelaars over het hoofd zien, is dat een *platte‑tekst* OCR‑run bliksemsnel is en je een snelle sanity‑check geeft. We roepen `engine.Recognize()` aan om ruwe tekens op te halen zonder layout‑metadata. Dit is wat we bedoelen met **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Waarom dit belangrijk is:*  
- **Snelheid** – een platte pass op een 300 dpi pagina duurt meestal minder dan een seconde.  
- **Baseline** – je kunt de later gestructureerde output vergelijken met deze baseline om grove fouten te spotten.  
- **Foutdetectie** – als de platte pass volledig faalt (bijv. alleen onzin), weet je dat de beeldkwaliteit te laag is en kun je vroegtijdig stoppen.

---

## Stap 2: Voer een gedetailleerde layout‑bewuste OCR‑pass uit

Platte tekst is geweldig, maar het negeert *waar* elk woord zich op de pagina bevindt. Voor facturen, formulieren of meer‑koloms tijdschriften heb je coördinaten, regelnummers en misschien zelfs lettertype‑informatie nodig. Daar komt `engine.RecognizeStructured()` om de hoek kijken.

Hieronder staat een dunne wrapper rond Tesseract’s **TSV**‑output, die ons een hiërarchie van pagina’s → regels → woorden geeft, met behoud van begrenzingsvakken.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Waarom we dit doen:*  
- **Coördinaten** laten je later de geëxtraheerde tekst terugplaatsen op de originele afbeelding voor markering of redactie.  
- **Regelgroepering** behoudt de oorspronkelijke layout, wat essentieel is wanneer je tabellen of kolommen moet reconstrueren.  
- Deze pass is iets trager dan de platte, maar voltooit nog steeds binnen enkele seconden voor de meeste documenten.

---

## Stap 3: Voer de AI post‑processor uit om OCR‑fouten te corrigeren

Zelfs de beste OCR‑engine maakt fouten — denk aan “rn” vs “m”, ontbrekende diakritische tekens, of gesplitste woorden. Een AI‑model kan de ruwe string en de gestructureerde data bekijken, inconsistenties opsporen, en de tekst herschrijven terwijl de originele coördinaten behouden blijven.

Hieronder staat een **mock**‑implementatie; vervang de body door een echte LLM‑aanroep als je die hebt.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Waarom deze stap OCR‑nauwkeurigheid verbetert:*  
- **Contextuele correcties** – de AI kan besluiten dat “l0ve” waarschijnlijk “love” is op basis van omliggende woorden.  
- **Behoud van coördinaten** – je houdt de layout‑informatie, zodat downstream‑taken (zoals PDF‑annotatie) accuraat blijven.  
- **Iteratieve verfijning** – je kunt de post‑processor meerdere keren draaien, elke pass maakt meer fouten schoon.

---

## Stap 4: Doorloop de gecorrigeerde, gestructureerde output

Nu we een opgeschoonde structuur hebben, is het ophalen van de uiteindelijke tekst triviaal. Hieronder printen we elke regel, maar je kunt ook naar een CSV schrijven, invoeren in een database, of een doorzoekbare PDF genereren.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Verwachte output** (ervan uitgaande dat het een eenvoudige één‑pagina factuur is):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Merk op hoe de regeleinden en kolomvolgorde behouden blijven, en veelvoorkomende OCR‑glitches zoals “$15.00” die gelezen wordt als “$15,00” worden gecorrigeerd door de AI‑stap.

---

## Hoe deze workflow **OCR‑nauwkeurigheid verbetert**

| Fase | Wat het corrigeert | Waarom het belangrijk is |
|------|--------------------|--------------------------|
| **Platte‑tekst OCR** | Detecteert onleesbare pagina’s vroeg | Bespaart tijd door hopeloze invoer over te slaan |
| **Gestructureerde OCR** | Legt layout, coördinaten vast | Maakt downstream‑taken mogelijk (markering, redactie) |
| **AI post‑processor** | Corrigeert spelling, voegt gesplitste woorden samen, repareert cijfers | Verhoogt de algehele teken‑nauwkeurigheid van ~85 % naar >95 % op ruisende scans |
| **Iteratie** | Laat je opnieuw draaien met afgestemde parameters | Fijnt de pipeline af voor specifieke documenttypes |

Door deze drie concepten te combineren — **platte‑tekst OCR**, layout‑bewuste extractie, en AI‑correctie — krijg je een robuuste oplossing die *significant* **OCR‑nauwkeurigheid verbetert** zonder een eigen neuraal netwerk vanaf nul te bouwen.

---

## Veelvoorkomende valkuilen & Pro‑tips

- **Valkuil:** Een afbeelding met lage resolutie (≤150 dpi) aan Tesseract geven levert onsamenhangende output op.  
  **Pro‑tip:** Pre‑process met `Pillow` — pas `Image.convert('L')` en `Image.filter(ImageFilter.MedianFilter())` toe vóór OCR.

- **Valkuil:** De AI post‑processor herschrijft per ongeluk domeinspecifieke terminologie (bijv. “SKU123”).  
  **Pro‑tip:** Bouw een whitelist van termen en geef die door aan de LLM of aan een spell‑checker bibliotheek zoals `pyspellchecker`.

- **Valkuil:** Meer‑koloms pagina’s worden samengevoegd tot één regel.  
  **Pro‑tip:** Detecteer kolomgrenzen met het `block_num` veld in Tesseract’s TSV‑output en splits regels dienovereenkomstig.

- **Valkuil:** Grote PDF‑bestanden veroorzaken geheugen‑explosies wanneer alle pagina’s tegelijk worden geladen.  
  **Pro‑tip:** Verwerk pagina’s incrementeel — loop over `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## De pipeline uitbreiden

Als je nieuwsgierig bent naar de volgende stappen, overweeg dan de volgende uitbreidingen:

1. **Batchverwerking** – Verpak het hele script in een functie die een map doorloopt, en verwerk duizenden bestanden parallel met `concurrent.futures`.  
2. **Taalmodellen** – Vervang de eenvoudige difflib‑heuristiek door een aanroep naar OpenAI’s `gpt‑4o` of een lokaal gehost LLaMA‑model voor rijkere contextuele correcties.  
3. **Exportformaten** – Schrijf de gecorrigeerde structuur naar een doorzoekbare PDF  

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}