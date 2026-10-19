---
category: general
date: 2026-06-06
description: Kör OCR på en bild med Python och se förtroendesiffror. Lär dig hur du
  filtrerar ord med låg förtroendegrad, sätter tröskelvärden och hanterar kantfall.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: sv
og_description: Kör OCR på en bild i Python, inspektera förtroendenivåer och filtrera
  bort ord med låg förtroendegrad. Den här handledningen guidar dig genom ett komplett,
  körbart exempel.
og_title: Kör OCR på bild med Python – Fullständig guide
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Kör OCR på bild med Python – Komplett steg‑för‑steg‑guide
url: /sv/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på bild med Python – Komplett steg‑för‑steg‑guide

Har du någonsin behövt **köra OCR på bild**‑filer men varit osäker på hur du får pålitlig text ur dem? Du är inte ensam – många utvecklare stöter på samma problem när de extraherade orden ser osäkra ut och förtroendesiffran är ett mysterium.  

I den här guiden dyker vi rakt in i en fungerande lösning: du får se hur du kör OCR på bild, läser av det totala förtroendet och plockar ut eventuella lågt‑förtroendeord som kan behöva manuell granskning. I slutet har du ett återanvändbart skript, förstår varför varje rad är viktig och vet hur du justerar förtroendetröskeln för dina egna projekt.

## Vad den här handledningen täcker

Vi går igenom hela arbetsflödet – från att ladda en bild till att skriva ut en snygg rapport över ord som hamnade under 80 % förtroende. På vägen diskuterar vi:

* Att välja en solid OCR‑motor (vi använder **EasyOCR**, ett populärt Python‑OCR‑bibliotek)  
* Att tolka `confidence`‑attributet som varje OCR‑resultat returnerar  
* Att filtrera ord med ett anpassat **OCR‑förtroendetröskel**  
* Att utöka skriptet för batch‑bearbetning eller alternativa motorer som **pytesseract**  

Ingen tidigare OCR‑erfarenhet krävs, bara en grundläggande kunskap om Python och en fungerande miljö (Python 3.9+ rekommenderas).  

Redo att förvandla suddiga skärmdumpar till ren, sökbar text? Låt oss börja.

---

## ## Så kör du OCR på bild med Python

Kärnan i handledningen är ett tresteg‑kodexempel som speglar koden du redan såg. Nedan bryter vi ner varje rad, förklarar varför, och ger dig sedan ett komplett, copy‑and‑paste‑klart skript.

### Steg 1: Installera och importera OCR‑motorn

Först, se till att OCR‑biblioteket är tillgängligt. **EasyOCR** fungerar direkt för många språk och ger ett förtroendevärde per ord.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Varför EasyOCR?* Det paketera en djupinlärningsmodell som tränats på varierande dataset, så du får vanligtvis högre förtroendevärden än den äldre Tesseract‑motorn, särskilt på bilder med blandad kvalitet.

> **Proffstips:** Om du befinner dig i en begränsad miljö (t.ex. en liten Docker‑container) kan `pytesseract` vara lättare, men du förlorar en del av den moderna noggrannheten som EasyOCR erbjuder.

### Steg 2: Kör OCR på bilden

Nu kör vi faktiskt **OCR på bild**. Metoden `recognize_image` från originalexemplet ersätts med EasyOCR:s `readtext`‑anrop, som returnerar en lista med `(bbox, text, confidence)`‑tupler.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Varje post i `ocr_results` ser ut så här:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Det tredje elementet (`0.92` i exemplet) är förtroendesiffran som varierar från 0 till 1.

### Steg 3: Sammanfatta totalt förtroende

Till skillnad från det tidigare kodexemplet som skrev ut ett enda `confidence`‑attribut, ger EasyOCR ett förtroende per ord. För att få en övergripande bild räknar vi ut medelvärdet:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Varför medelvärde?* Det ger dig en snabb hälsokontroll – om det totala förtroendet är under, säg, 70 % behöver du troligen förbättra bilden (bättre belysning, förbehandling osv.).

### Steg 4: Lista lågt‑förtroendeord

Nu kommer delen som direkt svarar på kravet “lista ord vars förtroende är under den önskade tröskeln”. Vi sätter ett **OCR‑förtroendetröskel** på 0.80 (80 %) som standard, men du kan justera det.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Loopen skriver ut varje ord som inte klarade tröskeln, tillsammans med dess procentuella förtroende. Detta är den exakta motsvarigheten till det ursprungliga `for recognized_word in recognition_result.words`‑loopen, men nu anpassad för EasyOCR:s utskriftsformat.

---

## ## Förstå OCR‑förtroendesiffror

Förtroende är inte ett magiskt tal; det är modellens uppskattning av hur säker den är på en viss transkription. Här är några saker att ha i åtanke:

| Situation | Typiskt förtroende | Vad du bör göra |
|-----------|-------------------|-----------------|
| Klar, högupplöst skanning | 0.95 – 1.00 | Ingen extra åtgärd behövs |
| Lätt oskärpa eller ojämn belysning | 0.80 – 0.94 | Överväg lätt förbehandling (kontrastökning) |
| Mycket brus, roterad text | < 0.70 | Använd bildförbehandling (deskew, denoise) eller byt till en annan OCR‑motor |

> **Observera:** Vissa språk (t.ex. kursiv handstil) ger naturligt lägre siffror. Justera tröskeln därefter.

### Edge Cases & Variationer

1. **Batch‑bearbetning** – Om du behöver **köra OCR på bild**‑filer i bulk, paketera logiken i en loop som itererar över en katalog.  
2. **Flera språk** – Skicka en lista som `['en', 'fr']` till `easyocr.Reader` så upptäcker motorn båda.  
3. **Alternativa motorer** – Vill du prova **pytesseract**? Ersätt läsarblocket med:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Du måste då samla per‑tecken‑förtroenden till per‑ord‑värden – lite mer arbete men genomförbart.

4. **Förbehandlingsknep** – Att använda OpenCV‑filter (`cv2.threshold`, `cv2.GaussianBlur`) kan öka förtroendet för brusiga skanningar.  

---

## ## Fullt, kör‑klart skript

Nedan är den kompletta Python‑filen du kan släppa in i ditt projekt. Spara den som `ocr_report.py` och kör `python ocr_report.py`. Se till att bildsökvägen pekar på en riktig fil.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Förväntad utskrift** (dina siffror kommer att variera):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Om varje ord klarar 80 %-gränsen ser du meddelandet “All words meet the confidence threshold.” istället.

---

## ## Vanliga frågor (FAQ)

**Q: Fungerar detta med PDF‑filer?**  
A: Inte direkt. Konvertera varje PDF‑sida till en bild först (t.ex. med `pdf2image`) och mata sedan in PNG/JPEG i skriptet.

**Q: Mina förtroendesiffror är alla låga – vad kan jag göra?**  
A: Prova bildförbehandling: öka kontrast, ta bort bakgrundsbrus eller rotera bilden till en horisontell baslinje. EasyOCR accepterar också en `contrast_ths`‑parameter som du kan justera.

**Q: Kan jag exportera resultaten till CSV?**  
A: Absolut. Efter loopen för lågt‑förtroende, skriv `ocr_results` till en `csv.DictWriter` där varje rad innehåller `text`, `confidence` och koordinater för bounding‑boxen.

**Q: Finns det en GPU‑accelererad version?**  
A: EasyOCR använder automatiskt CUDA om ett kompatibelt GPU och PyTorch är installerade. Verifiera med `torch.cuda.is_available()` innan du kör skriptet.

---

## Slutsats

Vi har precis **kört OCR på bild** med Python, granskat det totala förtroendet och isolerat eventuella lågt‑förtroendeord som behöver en manuell granskning.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}