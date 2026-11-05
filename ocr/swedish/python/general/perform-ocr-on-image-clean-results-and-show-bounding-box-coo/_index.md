---
category: general
date: 2026-03-28
description: Utför OCR på bilden och få ren text med koordinater för avgränsningsrutor.
  Lär dig hur du extraherar OCR, rensar OCR och visar resultaten steg för steg.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: sv
og_description: Utför OCR på en bild, rensa resultatet och visa koordinater för avgränsningsrutor
  i en kortfattad handledning.
og_title: Utför OCR på bild – Rena resultat och avgränsningsrutor
tags:
- OCR
- Computer Vision
- Python
title: Utför OCR på bild – Rensa resultat och visa koordinater för avgränsningsruta
url: /sv/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild – Rensa resultat och visa koordinater för avgränsningsrutor

Har du någonsin behövt **perform OCR on image** filer men fått rörig text och är osäker på var varje ord finns på bilden? Du är inte ensam. I många projekt—fakturadigitalisering, kvittoskanning eller enkel textutvinning—är det råa OCR‑utdata bara det första hindret. Den goda nyheten? Du kan rensa den utdata och omedelbart se varje regions avgränsningsrutekoordinater utan att skriva en massa boilerplate‑kod.

I den här guiden går vi igenom **how to extract OCR**, kör en **how to clean OCR** post‑processor och slutligen **display bounding box coordinates** för varje rensad region. I slutet har du ett enda körbart skript som förvandlar ett suddigt foto till prydlig, strukturerad text redo för vidare bearbetning.

## Vad du behöver

- Python 3.9+ (syntaxen nedan fungerar på 3.8 och nyare)
- En OCR‑motor som stödjer `recognize(..., return_structured=True)` – till exempel ett fiktivt `engine`‑bibliotek som används i kodsnutten. Byt ut det mot Tesseract, EasyOCR eller någon SDK som returnerar regionsdata.
- Grundläggande kunskap om Python‑funktioner och loopar
- En bildfil du vill skanna (PNG, JPG, etc.)

> **Pro tip:** Om du använder Tesseract ger `pytesseract.image_to_data`‑funktionen dig redan avgränsningsrutor. Du kan omsluta dess resultat i en liten adapter som efterliknar `engine.recognize`‑API:t som visas nedan.

---

![utför OCR på bild exempel](image-placeholder.png "utför OCR på bild exempel")

*Alt text: diagram som visar hur man utför OCR på bild och visualiserar avgränsningsrutekoordinater*

## Steg 1 – Utför OCR på bild och hämta strukturerade regioner

Det första är att be OCR‑motorn att returnera inte bara vanlig text utan en strukturerad lista med textregioner. Denna lista innehåller den råa strängen och rektangeln som omsluter den.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Varför detta är viktigt:**  
När du bara ber om vanlig text förlorar du den rumsliga kontexten. Strukturerad data låter dig senare **display bounding box coordinates**, align text with tables, or feed precise locations to a downstream model.

## Steg 2 – Hur man rensar OCR‑utdata med en post‑processor

OCR‑motorer är bra på att identifiera tecken, men de lämnar ofta kvar oönskade mellanslag, radbrytningsartefakter eller felaktigt igenkända symboler. En post‑processor normaliserar texten, rättar vanliga OCR‑fel och tar bort onödigt blanksteg.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Om du bygger din egen rensare, överväg:

- Ta bort icke‑ASCII‑tecken (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Kombinera flera mellanslag till ett enda mellanslag
- Använd en stavningskontroll som `pyspellchecker` för uppenbara stavfel

**Varför du bör bry dig:**  
En prydlig sträng gör sökning, indexering och efterföljande NLP‑pipelines mycket mer pålitliga. Med andra ord är **how to clean OCR** ofta skillnaden mellan en användbar dataset och ett huvudvärk.

## Steg 3 – Visa avgränsningsrutekoordinater för varje rensad region

Nu när texten är prydlig itererar vi över varje region, skriver ut dess rektangel och den rensade strängen. Detta är delen där vi slutligen **display bounding box coordinates**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Exempel på output**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Du kan nu mata in dessa koordinater i ett ritbibliotek (t.ex. OpenCV) för att överlagra rutor på originalbilden, eller lagra dem i en databas för senare frågor.

## Fullt, körklart skript

Nedan är det kompletta programmet som knyter ihop alla tre stegen. Byt ut platshållar‑anropen `engine` mot ditt faktiska OCR‑SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Så kör du

```bash
python perform_ocr.py sample_invoice.jpg
```

Du bör se en lista med avgränsningsrutor ihopparade med rensad text, exakt som exempelutdata ovan.

## Vanliga frågor & kantfall

| Question | Answer |
|----------|--------|
| **What if the OCR engine doesn’t support `return_structured`?** | Write a thin wrapper that converts the engine’s raw output (usually a list of words with coordinates) into objects with `text` and `bounding_box` attributes. |
| **Can I get confidence scores?** | Many SDKs expose a confidence metric per region. Append it to the print statement: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **How to handle rotated text?** | Pre‑process the image with OpenCV’s `cv2.minAreaRect` to deskew before calling `recognize`. |
| **What if I need the output in JSON?** | Serialize `processed_result.regions` with `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Is there a way to visualize the boxes?** | Use OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` inside the loop, then `cv2.imwrite("annotated.jpg", img)`. |

## Avslutning

Du har precis lärt dig **how to perform OCR on image**, rensat den råa utdata och **display bounding box coordinates** för varje region. Det trestegsflödet—recognize → post‑process → iterate—är ett återanvändbart mönster som du kan infoga i vilket Python‑projekt som helst som behöver pålitlig textutvinning.

### Vad blir nästa?

- **Utforska olika OCR‑bakändar** (Tesseract, EasyOCR, Google Vision) och jämför noggrannhet.
- **Integrera med en databas** för att lagra regionsdata för sökbara arkiv.
- **Lägg till språkdetection** för att dirigera varje region genom lämplig stavningskontroll.
- **Överlagra rutor på originalbilden** för visuell verifiering (se OpenCV‑snutten ovan).

Om du stöter på konstigheter, kom ihåg att den största vinsten kommer från ett solidt post‑processing‑steg; en ren sträng är mycket enklare att arbeta med än en rå dump av tecken.

Lycka till med kodandet, och må dina OCR‑pipelines alltid vara prydliga!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}