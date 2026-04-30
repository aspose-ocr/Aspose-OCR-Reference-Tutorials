---
category: general
date: 2026-04-29
description: Extrahera text från PDF med Aspose OCR i Python. Lär dig batch‑OCR PDF‑behandling,
  konvertera skannad PDF‑text och hantera sidor med låg förtroendegrad.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: sv
og_description: Extrahera text från PDF med Aspose OCR i Python. Denna guide visar
  batch‑OCR PDF‑bearbetning, konvertering av skannad PDF‑text och hantering av resultat
  med låg förtroendegrad.
og_title: Extrahera text från PDF – OCR PDF med Python
tags:
- OCR
- Python
- PDF processing
title: Extrahera text från PDF – OCR PDF med Python
url: /sv/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PDF – OCR PDF med Python

Har du någonsin behövt **extrahera text från PDF** men filen är bara en skannad bild? Du är inte ensam—många utvecklare stöter på detta när de försöker göra PDF-filer sökbara. Den goda nyheten? Med Aspose OCR för Python kan du konvertera skannad PDF‑text på några rader, och till och med köra **batch OCR PDF‑behandling** när du har dussintals filer att hantera.

I den här handledningen går vi igenom hela arbetsflödet: installera biblioteket, köra OCR på en enskild PDF, skala upp till en batch, och hantera sidor med låg förtroendegrad så att du vet när en manuell granskning krävs. I slutet har du ett färdigt skript som extraherar text från vilken skannad PDF som helst, och du förstår varför varje steg behövs.

## Vad du behöver

- Python 3.8 eller nyare (koden använder f‑strings, så 3.6+ fungerar, men 3.8+ rekommenderas)
- En Aspose OCR för Python-licens eller en gratis provnyckel (du kan skaffa en från Aspose webbplats)
- En mapp med en eller flera skannade PDF‑filer du vill bearbeta
- En måttlig mängd diskutrymme för de genererade *.txt*-rapporterna

Det är allt—inga tunga externa beroenden, ingen OpenCV‑gymnastik. Aspose OCR‑motorn sköter det tunga arbetet åt dig.

## Ställa in miljön

Först, installera Aspose OCR‑paketet från PyPI:

```bash
pip install aspose-ocr
```

Om du har en licensfil (`Aspose.OCR.lic`), placera den i projektets rot och aktivera den så här:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Proffstips:** Håll licensfilen utanför versionskontrollen; lägg till den i `.gitignore` för att undvika oavsiktlig exponering.

## Utföra OCR på en enskild PDF

Låt oss nu extrahera text från en enskild skannad PDF. De grundläggande stegen är:

1. Skapa en `OcrEngine`‑instans.
2. Peka den på PDF‑filen.
3. Hämta ett `OcrResult` för varje sida.
4. Skriv ut textutdata till disk.
5. Frigör motorn för att släppa inhemska resurser.

Här är det kompletta, körbara skriptet:

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

**Vad du kommer att se:** För varje sida skriver skriptet ut något i stil med `Page 1: confidence 97.45%`. Om en sida hamnar under 80 %-gränsen visas en varning som informerar dig om att OCR kan ha missat tecken.

### Varför detta fungerar

- **`OcrEngine`** är porten till det inhemska Aspose OCR‑biblioteket; det hanterar allt från bildförbehandling till teckenigenkänning.
- **`extract_from_pdf`** rasteriserar automatiskt varje PDF‑sida, så du behöver inte konvertera PDF‑en till bilder själv.
- **Förtroendescore** låter dig automatisera kvalitetskontroller—kritiskt när du bearbetar juridiska eller medicinska dokument där noggrannhet är viktigt.

## Batch OCR PDF‑behandling med Python

De flesta verkliga projekt involverar mer än en fil. Låt oss utöka en‑fil‑skriptet till en **batch OCR PDF‑behandlings**‑pipeline som går igenom en katalog, bearbetar varje PDF och lagrar resultaten i en motsvarande underkatalog.

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

#### Hur detta hjälper

- **Skalbarhet:** Funktionen går igenom mappen en gång och skapar en dedikerad utdata‑underkatalog för varje PDF. Detta håller ordning när du har dussintals dokument.
- **Återanvändbarhet:** `ocr_pdf_file` kan anropas från andra skript (t.ex. en webbtjänst) eftersom den är en ren funktion.
- **Felhantering:** Skriptet skriver ut ett vänligt meddelande om inmatningsmappen är tom, vilket sparar dig från ett tyst fel.

## Konvertera skannad PDF‑text – Hantera kantfall

Även om koden ovan fungerar för de flesta PDF‑filer kan du stöta på några egenheter:

| Situation | Varför det händer | Hur man mildrar |
|-----------|-------------------|-----------------|
| **Krypterade PDF‑filer** | PDF‑filen är lösenordsskyddad. | Skicka lösenordet till `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Flerspråkiga dokument** | Aspose OCR använder engelska som standard. | Ställ in `ocr_engine.language = "spa"` för spanska, eller ange en lista för blandade språk. |
| **Mycket stora PDF‑filer (>500 sidor)** | Minnesanvändningen skjuter i höjden eftersom varje sida laddas in i RAM. | Bearbeta PDF‑en i delar med `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` och loopa. |
| **Dålig skanningskvalitet** | Låg DPI eller mycket brus minskar förtroendet. | Förbehandla PDF‑en med `engine.image_preprocessing = True` eller öka DPI via `engine.dpi = 300`. |

> **Observera:** Att slå på bildförbehandling kan märkbart öka CPU‑tiden. Om du kör en nattlig batch, schemalägg tillräckligt med tid eller starta en separat arbetare.

## Verifiera utdata

Efter att skriptet har avslutats hittar du en mappstruktur som:

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

Öppna någon `.txt`‑fil; du bör se ren, UTF‑8‑kodad text som speglar det ursprungliga skannade innehållet. Om du märker förvrängda tecken, dubbelkolla PDF‑ens språkinställningar och se till att rätt teckensnittspaket är installerade på maskinen.

## Rensa upp resurser

Aspose OCR förlitar sig på inhemska DLL‑filer, så det är viktigt att anropa `engine.dispose()` när du är klar. Att glömma detta steg kan leda till minnesläckor, särskilt i långvariga batch‑jobb.

```python
# Always the last line of your script
engine.dispose()
```

## Fullt end‑to‑end‑exempel

Genom att samla allt, här är en enskild

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}