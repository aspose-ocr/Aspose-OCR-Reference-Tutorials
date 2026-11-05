---
category: general
date: 2026-04-26
description: hur man använder OCR på skannade PDF-filer, extraherar text från PDF,
  kör OCR på PDF och konverterar skannad PDF till sökbara filer på några få steg
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: sv
og_description: 'hur man använder OCR i Python: lär dig hur du extraherar text från
  PDF, kör OCR på PDF och konverterar skannade PDF-filer till sökbara dokument.'
og_title: hur man använder OCR – Snabbguide för att extrahera text från PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: hur man använder OCR – Extrahera text från PDF med Python
url: /sv/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man använder OCR – Extrahera text från PDF med Python

Har du någonsin funderat **hur man använder OCR** för att dra ut text ur ett skannat kontrakt, kvitto eller e‑bok? Du är inte ensam. I många verkliga projekt är PDF‑filen du får bara en bild, och utan OCR kan du varken söka, indexera eller analysera innehållet.  

I den här handledningen går vi igenom ett komplett, körbart exempel som visar **hur man använder OCR**, hur man **extraherar text från PDF**, och varför du kanske vill **konvertera skannad PDF** till sökbara dokument. Vi täcker också den subtila konsten att **ladda PDF som bild** så att OCR‑motorn kan se varje sida tydligt.

> **Snabb förhandsgranskning:** I slutet har du ett skript som laddar en flersidig PDF, kör OCR på varje sida och skriver ut den igenkända texten – utan externa tjänster.

## Vad du behöver

- Python 3.9+ (vilken som helst nyare version fungerar)
- `aocr`‑paketet (eller något kompatibelt OCR‑bibliotek som tillhandahåller `OcrEngine` och `Image.load`)
- En skannad PDF‑fil du vill bearbeta (t.ex. `contract.pdf`)
- En måttlig mängd RAM (≈ 200 MB per 100‑sidig PDF brukar räcka)

Om du ännu inte har installerat OCR‑biblioteket, kör:

```bash
pip install aocr
```

> **Proffstips:** Använd en virtuell miljö för att hålla dina beroenden organiserade.

## Steg 1: Ladda PDF som bild – Den första delen av pusslet

Innan någon OCR kan ske måste PDF‑filen representeras som en bild. Här kommer det sekundära nyckelordet **load pdf as image** in i bilden.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Varför detta är viktigt:* `aocr.Image.load` rasteriserar internt varje PDF‑sida till en bitmap som OCR‑motorn kan förstå. Om du hoppar över detta steg och matar in den råa PDF‑filen, kommer motorn att ge ett fel eftersom den förväntar sig pixeldata, inte vektordata.

> **Obs:** Sökvägen kan vara absolut eller relativ. Se till att filen är läsbar; annars får du ett `FileNotFoundError`.

## Steg 2: Kör OCR på PDF – Omvandla pixlar till tecken

Nu när PDF‑filen lever som en bild kan vi äntligen **köra OCR på PDF**. Följande kodsnutt bearbetar varje sida i ett svep:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Vad händer under huven?* `process_all_pages` loopar igenom de rasteriserade sidorna, applicerar OCR‑modellen och returnerar en lista med resultatobjekt – ett per sida. Varje resultat innehåller den igenkända texten, förtroendescore och avgränsningsrutor (om du behöver dem senare).

## Steg 3: Extrahera text från PDF – Dra ut strängarna

Med OCR‑resultaten i handen blir extrahering av ren text trivialt. Vi itererar över sidorna och skriver ut resultatet, vilket demonstrerar det sekundära nyckelordet **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Förväntad utskrift** (avkortad för korthet):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Om du vill ha texten i en enda sträng, konkatenera helt enkelt:

```python
full_text = "\n".join(r.text for r in page_results)
```

Nu har du framgångsrikt **extraherat text från PDF** med OCR.

## Steg 4: Konvertera skannad PDF – Gör den sökbar

Många efterföljande verktyg (som Elasticsearch eller SharePoint) förväntar sig en sökbar PDF snarare än en ren‑textdump. Du kan bädda in OCR‑utdata tillbaka i den ursprungliga PDF‑filen och på så sätt **konvertera skannad PDF** till en sökbar version.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Varför göra det?* En sökbar PDF behåller den ursprungliga layouten och bilderna samtidigt som den möjliggör textmarkering och indexering – en win‑win för både människor och maskiner.

## Vanliga fallgropar och specialfall

### Flersidiga PDF:er större än minnet

Om din PDF har hundratals sidor kan det bli för mycket RAM att ladda allt på en gång. `aocr`‑biblioteket stödjer lazy loading:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Bearbeta sedan sidorna en i taget:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Lågt kvalitetskanningar

OCR‑noggrannheten sjunker dramatiskt på suddiga eller lågkontrast‑skanningar. Innan du matar in bilden i motorn, överväg förbehandling:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Språkstöd

Som standard antar motorn engelska. För att **köra OCR på PDF** på ett annat språk, ange språk‑koden:

```python
ocr_engine.language = "spa"  # Spanish
```

Se till att motsvarande språkmodell är installerad.

## Fullt fungerande exempel

Sätter vi ihop allt får du ett självständigt skript som du kan spara som `ocr_pdf.py` och köra direkt:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Kör det så här:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Du kommer att se texten skriven till konsolen, och om du angav `-o` kommer en sökbar PDF att dyka upp bredvid originalfilen.

## Proffstips & bästa praxis

- **Batch‑bearbetning:** När du hanterar dussintals PDF‑filer, slå in logiken ovan i en loop och logga varje fils framgång/misslyckande.
- **Förtroendefiltrering:** Varje `page_result` innehåller ett förtroendemått. Kasta eller flagga sidor med låg förtroendegrad för manuell granskning.
- **Parallellism:** Om din CPU har flera kärnor, överväg att använda `concurrent.futures` för att bearbeta sidor parallellt – men håll ett öga på minnesanvändningen.
- **Versionslås:** `aocr`‑API:t kan förändras. Lås versionen i `requirements.txt` (t.ex. `aocr==2.3.1`) för att undvika brytande förändringar.

## Slutsats

Vi har gått igenom **hur man använder OCR** för att **extrahera text från PDF**, **köra OCR på PDF**, **ladda PDF som bild**, och även **konvertera skannad PDF** till ett sökbart format. Koden är komplett, förklaringarna täcker både *vad* och *varför*, och du har nu ett återanvändbart mönster för alla projekt som hanterar bild‑baserade PDF‑filer.

Vad blir nästa steg? Prova att mata in den extraherade texten i en naturlig språk‑pipeline, indexera de sökbara PDF‑erna med Elasticsearch, eller experimentera med olika OCR‑bakgrunder som Tesseract eller Azure Computer Vision. Himlen är gränsen, och verktygen finns inom räckhåll.

Lycklig kodning, och må dina PDF:er alltid vara sökbara! 

![exempel på hur man använder OCR](/images/ocr_workflow.png "how to use OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}