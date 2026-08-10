---
category: general
date: 2026-06-16
description: Tekst extraheren uit TIFF‑bestanden met Python OCR. Leer hoe je TIFF
  naar tekst converteert stap voor stap, en multi‑page‑documenten moeiteloos verwerkt.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: nl
og_description: Haal tekst uit TIFF‑bestanden met Python OCR. Volg deze gids om TIFF
  naar tekst te converteren, multi‑page scans te verwerken en schone resultaten te
  krijgen.
og_title: Tekst extraheren uit TIFF – Complete Python-gids
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Tekst extraheren uit TIFF – Complete Python‑gids
url: /nl/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit TIFF – Complete Python-gids

Heb je ooit **tekst uit TIFF**‑afbeeldingen moeten extraheren, maar wist je niet waar je moest beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan bij het verwerken van gescande archieven of legacy‑documenten. Het goede nieuws? Met een paar regels Python kun je **TIFF naar tekst converteren** in een handomdraai, zelfs wanneer het bestand tientallen pagina's bevat.

In deze tutorial lopen we een praktijkvoorbeeld door: het laden van een multi‑page TIFF, het instellen van de OCR‑taal op Frans, en het ophalen van de herkende tekst van elke pagina. Aan het einde heb je een kant‑klaar script, begrijp je waarom elke stap belangrijk is, en weet je hoe je het kunt aanpassen voor andere talen of afbeeldingsformaten.

## Vereisten

- Python 3.8 of nieuwer geïnstalleerd.
- Het `ocr`‑pakket (of een compatibele OCR‑bibliotheek die een `OcrEngine`‑klasse biedt). Je kunt het installeren met `pip install ocr-lib`—vervang door de daadwerkelijke pakketnaam die je gebruikt.
- Een multi‑page TIFF‑bestand (bijv. `french-scans.tif`) dat je wilt verwerken.
- Basiskennis van Python‑scripting.

Geen zware afhankelijkheden, geen externe services—alleen pure Python en een OCR‑engine.

---

## Stap 1: OCR‑engine instellen om **Tekst uit TIFF extraheren**

Allereerst hebben we een OCR‑engine‑instantie nodig en moeten we aangeven welke taal te gebruiken. In ons geval is het bronmateriaal Frans, dus stellen we de taal dienovereenkomstig in.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Waarom dit belangrijk is:**  
De taalinstelling verbetert de nauwkeurigheid aanzienlijk. Franse tekens zoals “é” of “ç” zouden als generieke symbolen gelezen worden als de engine standaard Engels gebruikt. Door expliciet Frans te selecteren geven we de engine de juiste tekenset.

> **Pro tip:** Als je documenten in meerdere talen verwerkt, kun je `engine.language` dynamisch aanpassen vóór elke `recognize()`‑aanroep.

---

## Stap 2: Laad de multi‑page TIFF die je wilt **TIFF naar tekst converteren**

Een TIFF kan meerdere frames bevatten—beschouw elk frame als een aparte pagina. De OCR‑bibliotheek abstraheert dat voor ons, dus wijzen we simpelweg naar het bestand.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Let op randgeval:**  
Als het bestandspad onjuist is of de TIFF corrupt, zal de `load_from_file`‑methode een uitzondering werpen. Omhul dit in een `try/except`‑blok voor productcode:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Stap 3: OCR uitvoeren op het volledige document – De kern van **Tekst uit TIFF extraheren**

Nu laten we de engine zijn magie doen. De `recognize()`‑aanroep verwerkt elke pagina in één keer en retourneert een rijk resultaatobject.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Wat gebeurt er onder de motorkap?**  
De engine iterereert over elk frame, past voorverwerking toe (kantelen corrigeren, binarisatie), voert het neurale netwerk uit, en aggregeert de output. Omdat we `recognize()` slechts één keer hebben aangeroepen, kan de bibliotheek middelen delen tussen pagina's, wat sneller is dan handmatig te loopen.

---

## Stap 4: Haal de herkende tekst uit het JSON‑resultaat – **TIFF naar tekst converteren** pagina voor pagina

Het resultaatobject kan worden geserialiseerd naar JSON. In die JSON vind je een `pages`‑array, waarbij elk element een `text`‑veld bevat.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Nu hebben we een nette Python‑lijst waarbij elk element overeenkomt met de OCR‑output van een pagina.

---

## Stap 5: Print of sla de tekst op voor elke pagina – Het laatste stuk van **Tekst uit TIFF extraheren**

Laten we door de pagina's loopen en de geëxtraheerde tekst weergeven. Je kunt ook elke pagina naar een apart `.txt`‑bestand schrijven als je dat liever hebt.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Verwachte output (voorbeeld)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Als de OCR geslaagd is, zie je een nette blok Franse zinnen voor elke pagina. Als je onduidelijke tekens ziet, controleer dan de taalinstelling opnieuw of overweeg de beeldresolutie te verhogen vóór OCR.

---

## Veelvoorkomende valkuilen behandelen bij het **TIFF naar tekst converteren**

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|--------------------|------------------|
| **Lege `pages`‑array** | De TIFF is niet correct geladen of bevat geen frames. | Controleer het bestandspad en zorg ervoor dat de TIFF geen enkel‑pagina PNG is die zich voordoet als TIFF. |
| **Garbage‑tekens** | Taal‑mismatch of lage beeldkwaliteit. | Stel de juiste `engine.language` in en verwerk de afbeelding vooraf (bijv. verhoog DPI). |
| **Geheugen‑explosie bij enorme TIFF’s** | Alle pagina's tegelijk laden verbruikt RAM. | Verwerk in delen: laad één frame, herken, en verwijder het vervolgens voordat je naar de volgende gaat. |
| **Unicode‑fouten bij het afdrukken** | Console‑codering ondersteunt geen accenttekens. | Gebruik `print(page[\"text\"].encode('utf-8').decode('utf-8'))` of configureer je terminal voor UTF‑8. |

---

## Script uitbreiden: Van **Tekst uit TIFF extraheren** naar batchverwerking

Nu je een solide basis hebt, overweeg je de volgende stappen:

1. **Batch‑conversie** – Plaats de volledige workflow in een functie `def ocr_tiff(path):` en iterate over een map met TIFF‑bestanden.
2. **Uitvoer naar bestanden** – In plaats van af te drukken, schrijf de tekst van elke pagina naar `page_{i}.txt` of concateneer alles in één enkel document.
3. **Alternatieve OCR‑engines** – Als je hogere nauwkeurigheid nodig hebt, vervang `ocr.OcrEngine()` door Tesseract (`pytesseract`) of Azure Cognitive Services—behoud gewoon dezelfde “tekst uit TIFF extraheren”‑logica.
4. **Post‑processing** – Voer spell‑check, taaldetectie of regex‑opschoning uit om de ruwe OCR‑output op te schonen.

---

## Volledig, kant‑klaar script

Hieronder staat de volledige code, klaar om te kopiëren en plakken. Het bevat basis‑foutafhandeling en optioneel opslaan van de tekst van elke pagina naar afzonderlijke bestanden.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Voer dit script uit, wijs `tiff_file` op je document, en zie de console vullen met nette Franse zinnen. Als je `out_folder` hebt opgegeven, vind je ook een reeks `page_#.txt`‑bestanden klaar voor verdere verwerking.

---

## Conclusie

We hebben zojuist **tekst uit TIFF**‑bestanden geëxtraheerd met een eenvoudige Python‑OCR‑workflow, en je weet nu hoe je **TIFF naar tekst kunt converteren** op een betrouwbare manier. Van het initialiseren van de engine met de juiste taal tot het loopen over het JSON‑resultaat van elke pagina, elke stap is uitgelegd met het “waarom” erachter, zodat je het patroon kunt aanpassen aan andere talen, afbeeldingsformaten of grotere batch‑taken.

Wat is het volgende? Probeer de OCR‑backend te vervangen door Tesseract, experimenteer met verschillende taal‑pakketten, of integreer de output in een doorzoekbare database. De mogelijkheden zijn eindeloos wanneer je gescande afbeeldingen betrouwbaar kunt omzetten naar doorzoekbare tekst.

Voel je vrij om een reactie achter te laten als je tegen problemen aanloopt of ideeën hebt voor verdere verbeteringen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst extraheren uit afbeeldingen met OCR‑bewerking op mappen](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Afbeelding naar tekst converteren – OCR uitvoeren op afbeelding vanuit URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}