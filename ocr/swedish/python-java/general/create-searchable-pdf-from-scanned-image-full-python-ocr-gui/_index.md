---
category: general
date: 2026-07-05
description: Skapa en sökbar PDF med Python. Lär dig hur du OCR:ar en skannad PNG,
  konverterar en skannad bild‑PDF och får en sökbar PDF på några minuter.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: sv
og_description: Skapa sökbar PDF snabbt. Den här guiden visar hur du OCR:ar en PNG,
  konverterar en skannad bild‑PDF och producerar en sökbar PDF med Python.
og_title: Skapa sökbar PDF från skannad bild – Python OCR-handledning
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Skapa sökbar PDF från skannad bild – Fullständig Python OCR-guide
url: /sv/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF från skannad bild – Fullständig Python OCR-guide

Har du någonsin undrat hur man **skapar sökbar PDF** från en skannad bild utan att betala för dyr programvara? Du är inte ensam. På många kontor kommer PDF-filer som platta bilder—svåra att söka i, omöjliga att kopiera‑klistra, och en mardröm för efterlevnadsgranskningar. De goda nyheterna? Med några rader Python kan du förvandla den statiska PNG-filen till en fullt sökbar PDF, och processen är enklare än du tror.

I den här handledningen går vi igenom ett komplett **OCR‑igenkänningsexempel**, som täcker allt från att installera rätt bibliotek till att skriva den slutgiltiga PDF-filen. När du är klar vet du exakt hur man **konverterar skannade bild‑PDF**‑filer, hur man **how to ocr pdf** programatiskt, och du har ett återanvändbart skript som du kan lägga in i vilket projekt som helst.

## Vad du kommer att lära dig

- Installera och konfigurera ett Python OCR‑bibliotek (vi använder `pytesseract` och `pdf2image`).
- Initiera OCR‑motorn och ange språket.
- Läs in en skannad PNG (eller någon bild) och kör OCR på den.
- Konvertera OCR‑resultatet till en **searchable PDF** (byte‑array) och spara den.
- Tips för att hantera flersidiga dokument, olika språk och vanliga fallgropar.

Ingen tidigare erfarenhet av OCR krävs—bara en fungerande Python 3‑miljö och lite nyfikenhet.

---

## Skapa sökbar PDF – Översikt

![Flödesdiagram för att skapa sökbar PDF](https://example.com/flowchart.png "Flödesdiagram för att skapa sökbar PDF")

*Alt text: Flödesdiagram för att skapa sökbar PDF som visar motorinitiering, bildladdning, OCR‑igenkänning, PDF‑konvertering och filskrivning.*

---

## Steg 1: Initiera OCR‑motorn (how to ocr pdf)

Varför behöver vi initiera någonting alls? OCR‑motorn är hjärnan som tolkar pixelmönster som tecken. Genom att skapa en motorinstans och uttryckligen ange språket, talar vi om för biblioteket vilket alfabet som förväntas, vilket dramatiskt förbättrar noggrannheten.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** Om du behöver OCR‑dokument på flera språk, installera motsvarande språkpaket för Tesseract och skicka en lista som `"eng+spa"` till `ocr_language`.

---

## Steg 2: Ladda den skannade bilden (convert scanned image pdf)

Nästa pusselbit är att få bilddata in i Python. Oavsett om du har en enskild PNG eller en flersidig TIFF, kan klassen `PIL.Image` öppna den. Om du startar från en PDF som redan innehåller skannade bilder, kommer `pdf2image` att konvertera varje sida till en bild åt oss.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Why this matters:** Att ladda bilden som ett Pillow‑objekt ger oss tillgång till dess råa pixeldatat, vilket OCR‑motorn behöver. Att hoppa över detta steg och mata in råa bytes direkt skulle orsaka fel.

---

## Steg 3: Utför OCR‑igenkänning på bilden (ocr recognition example)

Nu kommer den roliga delen—att låta motorn läsa texten. `pytesseract.image_to_pdf_or_hocr` returnerar en PDF‑bytesträmm som redan innehåller ett osynligt textlager, vilket är exakt vad vi behöver för en **searchable PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** Om din bild har låg kontrast, överväg att applicera ett enkelt tröskelvärde före OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Detta lilla förbehandlingssteg kan öka noggrannheten dramatiskt.

---

## Steg 4: Skriv PDF‑byten till en fil (convert png searchable pdf)

OCR‑biblioteket ger oss en byte‑array—tänk på den som det råa innehållet i en PDF‑fil. Allt vi behöver göra nu är att skriva dessa bytes till disk.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** Öppna den resulterande filen i någon PDF‑visare och försök söka efter ett ord du vet finns i originalbilden. Markeringen bör hoppa direkt till platsen, vilket bevisar att det osynliga textlagret fungerar.

---

## Steg 5: Utöka till flersidiga dokument (convert scanned image pdf)

Verkliga kontrakt sträcker sig ofta över flera sidor. För att **convert scanned image pdf**‑filer som innehåller flera sidor, loopa igenom varje sida, OCR:a den och sammanfoga de resulterande PDF‑erna.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Why merge?** Varje anrop till `image_to_pdf_or_hocr` producerar en fristående PDF. Att sammanfoga dem säkerställer att det slutgiltiga dokumentet bevarar den ursprungliga sidordningen.

---

## Vanliga fallgropar & hur man åtgärdar dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-------|
| Ingen sökbar text efter att PDF:en öppnats | Tesseract hittar inga tecken (tomt resultat) | Kontrollera bildkvaliteten, öka DPI eller tillämpa förbehandling (kontrast, binarisering). |
| förvrängda tecken (t.ex., �) | Fel språkpaket eller saknade typsnitt | Installera rätt språkdata (`tesseract‑lang‑eng`) och säkerställ att `ocr_language` matchar. |
| PDF‑filstorlek enorm (>10 MB för en enkelsidig bild) | Använder förlustfri PNG som källa; OCR lägger till en bild i full upplösning | Skala ner bilden före OCR (`image.thumbnail((1240, 1754))` för A4). |
| Skript kraschar på Windows med “tesseract.exe not found” | Tesseract‑binär inte i PATH | Lägg till `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (justera sökvägen). |

---

## Fullt, färdigt‑att‑köra‑script

Sätter vi ihop allt, här är en enda fil som du kan kopiera‑klistra in och köra:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Spara detta som `create_searchable_pdf.py`, ersätt platshållarna med riktiga sökvägar, och kör:

```bash
python create_searchable_pdf.py
```

Du bör se en

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man OCR‑PDF i .NET med Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konvertera bilder till PDF C# – Spara flersidigt OCR‑resultat](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR‑igenkänning av PDF‑dokument i Aspose.OCR för Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}