---
category: general
date: 2026-06-06
description: Hur man OCR:ar PDF med Aspose OCR Cloud. Lär dig att extrahera text från
  PDF, konvertera PDF‑sidor till PNG och spara PDF‑sidbilder i Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: sv
og_description: Hur man OCR:ar PDF med Aspose OCR Cloud. Denna guide visar hur man
  extraherar ren text från PDF, konverterar PDF-sidor till PNG och sparar PDF-sidbilder.
og_title: Hur man OCR:ar PDF med Aspose OCR Cloud – Steg för steg
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Hur man OCR:ar PDF med Aspose OCR Cloud – Komplett guide
url: /sv/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man OCR:ar PDF med Aspose OCR Cloud – Komplett guide

Har du någonsin undrat **hur man OCR:ar PDF**-filer utan att kämpa med tunga skrivbordsverktyg? Du är inte ensam—många utvecklare stöter på den muren när de behöver ett snabbt, programatiskt sätt att hämta text från skannade dokument. Den goda nyheten? Med Aspose OCR Cloud kan du **extrahera text från PDF**, omvandla varje sida till en PNG och till och med **spara PDF‑sidbilder** för senare bruk, allt från ett snyggt Python‑skript.

I den här handledningen går vi igenom allt du behöver veta: från att installera SDK:n, licensiera motorn och känna igen flersidiga PDF‑filer, till att extrahera ren text, konvertera sidor till PNG och spara dessa bilder på disk. I slutet har du ett återanvändbart kodsnutt som du kan lägga in i vilket projekt som helst som behöver **hur man OCR:ar PDF**‑funktionalitet.

## Vad du behöver

- **Python 3.8+** (koden fungerar även på 3.10 och nyare)  
- Ett Aspose OCR Cloud‑konto – du får en gratis provlicensfil (`Aspose.OCR.lic`)  
- `asposeocrcloud`‑paketet (`pip install asposeocrcloud`)  
- En skannad, flersidig PDF som du vill bearbeta  

Det är allt. Inga extra binärer, inga inhemska beroenden, bara ren Python.

## Så OCR:ar du PDF – Installation och licens

Innan du kan anropa några OCR‑metoder måste du berätta för SDK:n vem du är. Aspose använder en lättviktig licensfil som du placerar någonstans där ditt skript kan nå den.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Proffstips:* Om du hoppar över licenssteget kommer SDK:n fortfarande att fungera men kommer att lägga in ett litet vattenstämpel i utdata‑bilderna. Inte idealiskt för produktion.

## Steg 2: Installera Aspose OCR Cloud Python‑SDK

Öppna en terminal och kör:

```bash
pip install asposeocrcloud
```

Paketet hämtar alla nödvändiga beroenden (requests, pillow, osv.) så du behöver inte leta efter något annat.

## Steg 3: Skapa en OCR‑motor och välj ett språk

Motorn är hjärtat i operationen. Du kan ange vilket språk som helst som stöds av Aspose; engelska fungerar i de flesta fall.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Varför ange språk? För att OCR‑motorn använder språk‑specifika ordböcker för att förbättra noggrannheten. Om du bearbetar franska PDF‑filer, byt bara `ENGLISH` mot `FRENCH`.

## Steg 4: Peka på din flersidiga PDF

Ge motorn den fullständiga sökvägen till filen du vill bearbeta. Relativa sökvägar fungerar så länge de kan lösas från skriptets arbetskatalog.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Se till att filen är läsbar; annars får du ett `FileNotFoundError`.

## Steg 5: Kör OCR – du får en lista med resultat

Att anropa `recognize_pdf` returnerar en lista där varje element motsvarar en sida i käll‑PDF‑filen.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Varje `OcrResult` innehåller två praktiska egenskaper:

* `text` – den rena textrepresentationen av sidan (perfekt för **extrahera ren text pdf**)  
* `image` – ett Pillow `Image`‑objekt av den renderade sidan (perfekt för **konvertera pdf sida png**)

## Steg 6: Extrahera text från PDF och konvertera sidor till PNG

Nu loopar vi igenom resultaten, skriver ut den extraherade texten och sparar en PNG‑version av varje sida.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Förväntad konsolutdata

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Du kommer också att hitta `page_1.png`, `page_2.png`, … i `YOUR_DIRECTORY`. Det är de rasteriserade sidbilderna som du kan mata in i efterföljande bildbehandlings‑pipelines.

## Steg 7: Spara PDF‑sidbilder (valfri efterbehandling)

Om du bara behöver bilderna och inte texten kan du hoppa över raden `print(res.text)`. Omvänt, om du vill lagra texten i separata `.txt`‑filer, lägg bara till en liten utskrift:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Detta lilla tillägg visar hur enkelt det är att **spara PDF‑sidbilder** samtidigt som du bevarar det extraherade innehållet.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta skriptet som du kan kopiera‑och‑klistra in i `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Kör det med:

```bash
python ocr_pdf.py
```

Du bör se en konsolutskrift av varje sidas text och en serie PNG‑filer

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man OCR:ar PDF i .NET med Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Känn igen PDF‑text – OCR‑operationer med Aspose.OCR för Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Konvertera bilder till PDF C# – Spara flersidig OCR‑resultat](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}