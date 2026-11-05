---
category: general
date: 2026-03-28
description: Lär dig snabbt hur du OCR:ar PDF med Python. Den här guiden visar hur
  du extraherar text från PDF, känner igen text i PDF och konverterar skannade PDF-filer
  till text med Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: sv
og_description: Lär dig att OCR:a PDF med Python. Extrahera text från PDF, känna igen
  text i PDF och konvertera skannade PDF-filer till text på några minuter.
og_title: Hur man OCR:ar PDF i Python – Komplett guide
tags:
- PDF
- OCR
- Python
- Aspose
title: Hur man OCR:ar PDF i Python – Steg‑för‑steg guide
url: /sv/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här OCR‑ar du PDF i Python – Steg‑för‑steg‑guide

Har du någonsin funderat **hur man OCR‑ar PDF** när filen bara är en bild av en sida? Du är inte ensam. I den här handledningen går vi igenom exakt vilka steg som krävs för att OCR‑a PDF‑filer, extrahera text från PDF och omvandla en skannad PDF till sökbar text – allt med ren Python‑kod.

Vi täcker allt från installation av Aspose OCR‑biblioteket till att hämta den igenkända texten från varje sida. När du är klar kan du **OCR‑a PDF med Python**, **extrahera text från PDF** och **konvertera skannad PDF till text** utan att leta igenom spridda dokument. Inga onödiga utsvävningar, bara ett praktiskt, körbart exempel som du kan kopiera‑klistra.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* Python 3.8+ (den senaste stabila versionen fungerar bäst)  
* En Aspose OCR för Python‑licens eller en gratis provnyckel – du kan hämta den från Aspose‑webbplatsen.  
* En skannad PDF som du vill bearbeta (vi kallar den `input.pdf`).  

Om du redan har detta, toppen – låt oss sätta igång. Om inte, är installationen ett enkelt steg som vi visar nedan.

## Så här OCR‑ar du PDF – Installera miljön

Det första du måste göra är att få Aspose OCR‑modulen på din maskin. Paketet heter `aspose-ocr`, och du kan installera det via pip:

```bash
pip install aspose-ocr
```

> **Proffstips:** Använd ett virtuellt miljö (`python -m venv venv`) så att dina beroenden hålls organiserade.

När paketet är installerat är du redo att importera det och starta OCR‑motorn. Detta är grunden för varje **ocr pdf with python**‑arbetsflöde du kommer att bygga senare.

## OCR PDF med Python – Importera Aspose OCR

Nu när biblioteket är tillgängligt, låt oss importera det i vårt skript. Vi sätter också motorn att arbeta i *direct PDF mode*, vilket får Aspose att läsa PDF‑bytarna direkt från filen istället för att konvertera varje sida till en bild först.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Varför använda `PdfMode.DIRECT`? För att det hoppar över ett extra rasteriseringssteg, vilket gör processen snabbare och bevarar den ursprungliga layouten – särskilt praktiskt när du behöver **recognize text from PDF** exakt.

## Identifiera text från PDF – Köra motorn

Med motorn klar, peka den mot din skannade fil. Metoden `recognize_from_pdf` sköter allt tungt arbete: den parsar varje sida, kör OCR‑algoritmen och returnerar ett `OcrResult`‑objekt som innehåller en samling `Page`‑objekt.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Undrar du om detta fungerar med krypterade PDF‑filer? Ja, så länge du anger lösenordet via `ocr_engine.password = "secret"` innan du anropar `recognize_from_pdf`. Det är ett kantfall som många handledningar hoppar över, men som är användbart i verkliga pipelines.

## Extrahera text från PDF – Åtkomst till sidresultat

Listan `ocr_result.pages` innehåller ett element per sida. Varje `Page`‑objekt har ett `.text`‑attribut som innehåller den rena textrepresentationen av den skannade sidan. Låt oss loopa igenom och skriva ut resultaten så att du kan se exakt vad som extraherades.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Att köra skriptet ger en utskrift liknande:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Denna utskrift bevisar att du framgångsrikt har **extract text from PDF** och **recognize text from PDF** med Aspose OCR. Du kan nu skicka strängarna till en databas, ett sökindex eller någon annan NLP‑pipeline.

![exempel på hur man OCR:ar PDF](placeholder-image.png "exempel på hur man OCR:ar PDF")

*Bildtext:* **exempel på hur man OCR:ar PDF** – visar konsolutdata av igenkänd text per sida.

## Konvertera skannad PDF till text – Spara resultatet

De flesta utvecklare vill inte bara se texten i konsolen; de behöver en bestående fil. Nedan är en liten hjälpfunktion som skriver varje sidas text till en separat `.txt`‑fil, vilket effektivt **convert scanned PDF to text** i en mapp som heter `output`.

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

När skriptet är klart har du en prydlig katalog:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Nu har du fullständigt **convert scanned PDF to text** och kan mata in dessa filer i vilken efterföljande process som helst – sök, analys eller till och med ett enkelt `grep`.

## Vanliga frågor & specialfall

**Vad händer om min PDF innehåller både bilder och riktig text?**  
Aspose OCR försöker känna igen allt, men du kan snabba upp processen genom att inaktivera OCR för sidor som redan innehåller markerbar text. Sätt `ocr_engine.auto_detect_page_orientation = True` och anropa sedan `ocr_engine.recognize_from_pdf(..., detect_text=False)` för sidor du vet är bra.

**Kan jag styra språkmodellen?**  
Absolut. Sätt `ocr_engine.language = aocr.Language.English` (eller något annat stödjert språk) innan du anropar `recognize_from_pdf`. Detta förbättrar noggrannheten för icke‑engelska dokument.

**Hur hanterar jag väldigt stora PDF‑filer (100+ sidor)?**  
Bearbeta dem i delar. Metoden `recognize_from_pdf` accepterar ett `page_range`‑argument, t.ex. `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Loop över intervall för att hålla minnesanvändningen låg.

## Fullt fungerande exempel

Sätt ihop allt, så har du ett komplett skript du kan spara som `ocr_pdf.py` och köra:

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

Kör det med:

```bash
python ocr_pdf.py
```

Du bör se konsolutdata som bekräftar varje sidas text och platsen för de sparade `.txt`‑filerna.

## Slutsats

Vi har gått igenom **how to OCR PDF** med Python, demonstrerat ett rent sätt att **ocr pdf with python**, visat hur du **extract text from PDF**, förklarat mekaniken bakom **recognize text from PDF**, och slutligen levererat ett färdigt kodexempel som **convert scanned PDF to text**. Hela processen är nu inlindad

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}