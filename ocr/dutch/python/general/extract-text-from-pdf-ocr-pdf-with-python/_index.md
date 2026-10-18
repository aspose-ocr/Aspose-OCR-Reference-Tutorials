---
category: general
date: 2026-04-29
description: Haal tekst uit PDF met Aspose OCR in Python. Leer batch‑OCR‑PDF‑verwerking,
  converteer gescande PDF‑tekst en verwerk pagina’s met een lage vertrouwensscore.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: nl
og_description: Tekst extraheren uit PDF met Aspose OCR in Python. Deze gids laat
  batch‑OCR PDF‑verwerking zien, het converteren van gescande PDF‑tekst en het omgaan
  met resultaten met een lage vertrouwensscore.
og_title: Tekst uit PDF extraheren – OCR PDF met Python
tags:
- OCR
- Python
- PDF processing
title: Tekst extraheren uit PDF – OCR PDF met Python
url: /nl/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PDF – OCR PDF met Python

Heb je ooit **tekst uit PDF** moeten extraheren, maar is het bestand slechts een gescande afbeelding? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan wanneer ze PDF's willen omzetten naar doorzoekbare data. Het goede nieuws? Met Aspose OCR voor Python kun je gescande PDF‑tekst in een paar regels converteren, en zelfs **batch OCR PDF verwerking** uitvoeren wanneer je tientallen bestanden moet verwerken.

In deze tutorial lopen we de volledige workflow door: de bibliotheek installeren, OCR uitvoeren op een enkele PDF, opschalen naar een batch, en omgaan met pagina's met lage vertrouwensscore zodat je weet wanneer een handmatige controle nodig is. Aan het einde heb je een kant‑klaar script dat tekst uit elke gescande PDF extraheert, en begrijp je de reden achter elke stap.

## Wat je nodig hebt

- Python 3.8 of nieuwer (de code gebruikt f‑strings, dus 3.6+ werkt, maar 3.8+ wordt aanbevolen)
- Een Aspose OCR voor Python‑licentie of een gratis proeflicentiesleutel (je kunt er één krijgen op de Aspose‑website)
- Een map met één of meer gescande PDF‑bestanden die je wilt verwerken
- Een bescheiden hoeveelheid schijfruimte voor de gegenereerde *.txt*‑rapporten

Dat is alles—geen zware externe afhankelijkheden, geen OpenCV‑gymnastiek. De Aspose OCR‑engine doet het zware werk voor je.

## De omgeving instellen

Eerst installeer je het Aspose OCR‑pakket van PyPI:

```bash
pip install aspose-ocr
```

Als je een licentiebestand (`Aspose.OCR.lic`) hebt, plaats het dan in de root van je project en activeer het als volgt:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Houd het licentiebestand buiten versiebeheer; voeg het toe aan `.gitignore` om onbedoelde blootstelling te voorkomen.

## OCR uitvoeren op een enkele PDF

Laten we nu tekst extraheren uit een enkele gescande PDF. De kernstappen zijn:

1. Maak een `OcrEngine`‑instantie.
2. Verwijs deze naar het PDF‑bestand.
3. Haal een `OcrResult` op voor elke pagina.
4. Schrijf de platte‑tekstuitvoer naar schijf.
5. Vernietig de engine om native bronnen vrij te geven.

Hier is het volledige, uitvoerbare script:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Wat je zult zien:** Voor elke pagina print het script iets als `Page 1: confidence 97.45%`. Als een pagina onder de 80 % drempel valt, verschijnt er een waarschuwing, zodat je weet dat de OCR mogelijk tekens heeft gemist.

### Waarom dit werkt

- **`OcrEngine`** is de toegangspoort tot de native Aspose OCR‑bibliotheek; hij behandelt alles van beeldvoorbewerking tot tekenherkenning.
- **`extract_from_pdf`** rastert automatisch elke PDF‑pagina, zodat je de PDF niet zelf naar afbeeldingen hoeft te converteren.
- **Vertrouwensscores** stellen je in staat kwaliteitscontroles te automatiseren—cruciaal wanneer je juridische of medische documenten verwerkt waar nauwkeurigheid van belang is.

## Batch OCR PDF verwerking met Python

De meeste projecten in de praktijk omvatten meer dan één bestand. Laten we het script voor één bestand uitbreiden naar een **batch OCR PDF verwerking**‑pipeline die een map doorloopt, elke PDF verwerkt en de resultaten opslaat in een bijbehorende sub‑map.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Hoe dit helpt

- **Schaalbaarheid:** De functie doorloopt de map één keer en maakt een dedicated output‑sub‑map voor elke PDF. Dit houdt alles overzichtelijk wanneer je tientallen documenten hebt.
- **Herbruikbaarheid:** `ocr_pdf_file` kan worden aangeroepen vanuit andere scripts (bijv. een webservice) omdat het een pure functie is.
- **Foutafhandeling:** Het script print een vriendelijke melding als de invoermap leeg is, zodat je niet stilletjes faalt.

## Gescande PDF-tekst converteren – Randgevallen afhandelen

Hoewel de bovenstaande code voor de meeste PDF's werkt, kun je tegen enkele eigenaardigheden aanlopen:

| Situatie | Waarom het gebeurt | Hoe te mitigeren |
|----------|--------------------|------------------|
| **Versleutelde PDF's** | De PDF is met een wachtwoord beveiligd. | Geef het wachtwoord door aan `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Meertalige documenten** | Aspose OCR gaat standaard uit van Engels. | Stel `ocr_engine.language = "spa"` in voor Spaans, of geef een lijst op voor gemengde talen. |
| **Zeer grote PDF's (>500 pagina's)** | Het geheugenverbruik stijgt omdat elke pagina in RAM wordt geladen. | Verwerk de PDF in delen met `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` en herhaal in een lus. |
| **Slechte scankwaliteit** | Lage DPI of veel ruis verlaagt de vertrouwensscore. | Pre‑process de PDF met `engine.image_preprocessing = True` of verhoog de DPI via `engine.dpi = 300`. |

> **Let op:** Het inschakelen van beeldvoorbewerking kan de CPU‑tijd merkbaar verhogen. Als je een nachtelijke batch draait, plan dan voldoende tijd in of start een aparte worker.

## De output verifiëren

Na afloop van het script vind je een mapstructuur zoals:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Open een willekeurig `.txt`‑bestand; je zou schone, UTF‑8‑gecodeerde tekst moeten zien die de oorspronkelijke gescande inhoud weerspiegelt. Als je onleesbare tekens opmerkt, controleer dan de taalinstellingen van de PDF en zorg dat de juiste lettertype‑pakketten op de machine zijn geïnstalleerd.

## Resources opruimen

Aspose OCR maakt gebruik van native DLL's, dus het is essentieel om `engine.dispose()` aan te roepen zodra je klaar bent. Het vergeten van deze stap kan leiden tot geheugenlekken, vooral bij langdurige batch‑taken.

```python
# Always the last line of your script
engine.dispose()
```

## Volledig end‑to‑end voorbeeld

Alles samengevoegd, hier is een enkele

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}