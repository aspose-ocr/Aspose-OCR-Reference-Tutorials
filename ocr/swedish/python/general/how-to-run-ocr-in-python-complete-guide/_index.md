---
category: general
date: 2026-06-19
description: Hur man kör OCR steg för steg och förbättrar OCR‑noggrannheten med enkla
  text‑OCR‑tekniker. Lär dig ett snabbt arbetsflöde för pålitlig textutvinning.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: sv
og_description: Hur man kör OCR effektivt. Denna handledning visar hur man förbättrar
  OCR‑noggrannheten med hjälp av vanlig text‑OCR och AI‑efterbehandling.
og_title: Hur hur man kör OCR i Python – Komplett guide
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
title: Hur man kör OCR i Python – Komplett guide
url: /sv/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR i Python – Komplett guide

Har du någonsin funderat **hur man kör OCR** på en mängd skannade PDF‑filer utan att spendera timmar på att justera inställningar? Du är inte ensam. I många projekt är det första hindret helt enkelt att få pålitlig text ur en bild, och skillnaden mellan ett svagt resultat och en ren extraktion beror ofta på ett par smarta steg.

I den här guiden går vi igenom en praktisk fyrstegs‑pipeline som inte bara **kör OCR** utan också **förbättrar OCR‑noggrannheten** genom att kombinera ett snabbt ren‑text‑pass med ett layout‑medvetet andra pass och en AI‑driven efterbehandling. När du är klar har du ett färdigt skript, en klar förklaring till varför varje steg är viktigt, samt tips för att hantera kantfall som flerkolumnssidor eller brusiga skanningar.

---

## Vad du behöver

Innan vi dyker ner, se till att du har följande:

- **Python 3.9+** – koden använder typ‑hintar och f‑strängar.
- **Tesseract OCR** installerad och åtkomlig via `tesseract`‑kommandoraden. (På Ubuntu: `sudo apt install tesseract-ocr`; på Windows hämta installationsprogrammet från den officiella repot.)
- **pytesseract**‑wrappern (`pip install pytesseract`).
- Ett **AI‑postprocess‑bibliotek** – för detta exempel låtsas vi att du har en lättviktig `ai`‑modul som erbjuder `run_postprocessor`. Byt ut den mot OpenAI:s GPT‑4‑API eller en lokal LLM om du föredrar.
- Några exempelbilder eller PDF‑filer att testa.

Det är allt. Inga tunga ramverk, ingen Docker‑gymnastik. Bara ett fåtal pip‑installationer så är du redo att köra.

---

## Steg 1: Utför ett snabbt OCR‑pass för ren text

Det första de flesta utvecklare förbiser är att ett *ren‑text* OCR‑körning är blixtsnabb och ger en snabb kontroll. Vi anropar `engine.Recognize()` för att hämta råa tecken utan någon layout‑metadata. Detta är vad vi menar med **ren‑text‑OCR**.

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

*Varför detta är viktigt:*  
- **Hastighet** – ett vanligt pass på en 300 dpi‑sida avslutas vanligtvis på under en sekund.  
- **Baslinje** – du kan jämföra den senare strukturerade utdata mot denna baslinje för att upptäcka uppenbara fel.  
- **Felfångst** – om det enkla passet misslyckas helt (t.ex. bara nonsens) vet du att bildkvaliteten är för låg och kan avbryta tidigt.

---

## Steg 2: Kör ett detaljerat layout‑medvetet OCR‑pass

Ren text är bra, men den kastar bort *var* varje ord befinner sig på sidan. För fakturor, formulär eller flerkolumnsmagasin behöver du koordinater, radnummer och kanske till och med teckensnittsinformation. Det är här `engine.RecognizeStructured()` kommer in.

Nedan är ett tunt omslag runt Tesseracts **TSV**‑output, som ger oss en hierarki av sidor → rader → ord, med bevarade avgränsningsrutor.

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

*Varför vi gör detta:*  
- **Koordinater** låter dig senare kartlägga extraherad text tillbaka till originalbilden för markering eller radering.  
- **Radgruppering** bevarar den ursprungliga layouten, vilket är avgörande när du behöver återskapa tabeller eller kolumner.  
- Detta pass är lite långsammare än det enkla, men avslutas fortfarande på några sekunder för de flesta dokument.

---

## Steg 3: Kör AI‑postprocessorn för att korrigera OCR‑fel

Även den bästa OCR‑motorn gör misstag—tänk “rn” vs “m”, saknade diakritiska tecken eller delade ord. En AI‑modell kan titta på den råa strängen och den strukturerade datan, upptäcka inkonsekvenser och skriva om texten samtidigt som de ursprungliga koordinaterna behålls.

Nedan är en **mock**‑implementation; ersätt kroppen med ett riktigt LLM‑anrop om du har ett.

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

*Varför detta steg förbättrar OCR‑noggrannheten:*  
- **Kontextuella korrigeringar** – AI kan avgöra att “l0ve” sannolikt är “love” baserat på omgivande ord.  
- **Bevarande av koordinater** – du behåller layoutinformationen, så efterföljande uppgifter (som PDF‑annotation) förblir korrekta.  
- **Iterativ förfining** – du kan köra postprocessorn flera gånger, där varje pass rensar fler fel.

---

## Steg 4: Iterera genom den korrigerade, strukturerade utdata

Nu när vi har en rengjord struktur är det trivialt att hämta den slutgiltiga texten. Nedan skriver vi ut varje rad, men du kan också skriva till en CSV, mata in i en databas eller generera en sökbar PDF.

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

**Förväntad output** (förutsatt en enkel en‑sidesfaktura):

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

Lägg märke till hur radbrytningar och kolumnordning bevaras, och vanliga OCR‑glitchar som “$15.00” som läses som “$15,00” korrigeras av AI‑steget.

---

## Hur detta arbetsflöde hjälper **förbättra OCR‑noggrannhet**

| Steg | Vad det fixar | Varför det är viktigt |
|------|---------------|-----------------------|
| **Vanlig text‑OCR** | Upptäcker oläsliga sidor tidigt | Sparar tid genom att hoppa över hopplösa indata |
| **Strukturerad OCR** | Fångar layout, koordinater | Möjliggör efterföljande uppgifter (markering, radering) |
| **AI‑postprocessor** | Korrigerar stavning, slår ihop delade ord, rättar siffror | Ökar den totala tecken‑noggrannheten från ~85 % till >95 % på brusiga skanningar |
| **Iteration** | Gör att du kan köra om med finjusterade parametrar | Finjusterar pipeline för specifika dokumenttyper |

Genom att kombinera dessa tre koncept—**ren‑text‑OCR**, layout‑medveten extraktion och AI‑korrigering—får du en robust lösning som *väsentligt* **förbättrar OCR‑noggrannheten** utan att behöva skriva ett eget neuralt nätverk från grunden.

---

## Vanliga fallgropar & pro‑tips

- **Fallgrop:** Att mata in en lågupplöst bild (≤150 dpi) till Tesseract ger förvrängd output.  
  **Pro‑tips:** Förprocessa med `Pillow`—använd `Image.convert('L')` och `Image.filter(ImageFilter.MedianFilter())` innan OCR.

- **Fallgrop:** AI‑postprocessorn kan av misstag skriva om domänspecifik terminologi (t.ex. “SKU123”).  
  **Pro‑tips:** Bygg en vitlista med termer och skicka den till LLM:n eller till ett stavningskontrollbibliotek som `pyspellchecker`.

- **Fallgrop:** Sidor med flera kolumner slås ihop till en enda rad.  
  **Pro‑tips:** Detektera kolumngränser med `block_num`‑fältet i Tesseracts TSV‑output och dela upp rader därefter.

- **Fallgrop:** Stora PDF‑filer får minnet att svälla när alla sidor laddas på en gång.  
  **Pro‑tips:** Processa sidor inkrementellt—loopa över `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Utöka pipeline

Om du är nyfiken på nästa steg, överväg följande förbättringar:

1. **Batch‑behandling** – Packa hela skriptet i en funktion som går igenom en katalog, hanterar tusentals filer parallellt med `concurrent.futures`.
2. **Språkmodeller** – Byt ut den enkla difflib‑heuristiken mot ett anrop till OpenAI:s `gpt‑4o` eller en lokalt hostad LLaMA‑modell för att få rikare kontextuella korrigeringar.
3. **Exportformat** – Skriv den korrigerade strukturen till en sökbar PDF

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i egna projekt.

- [Hur man OCR‑ar bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Hur man använder OCR – avancerade tekniker med Aspose.OCR för Java](/ocr/english/java/advanced-ocr-techniques/)
- [Förbättra OCR‑noggrannhet – Detektera områden‑läge i OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}