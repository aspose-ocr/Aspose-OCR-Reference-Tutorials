---
category: general
date: 2026-03-26
description: Lär dig hur du roterar en bild och utför OCR i Python. Den här guiden
  visar också hur du förbehandlar en bild för OCR och extraherar text från bilden
  på ett effektivt sätt.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: sv
og_description: Hur man roterar en bild korrekt och sedan känner igen text från bilden
  med Aspose OCR. Följ den här steg‑för‑steg‑handledningen för att förbehandla bilden
  för OCR och extrahera text från bilden.
og_title: Hur man roterar bild och utför OCR – Komplett Python‑guide
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Hur man roterar en bild och utför OCR med Aspose i Python
url: /sv/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man roterar bild och utför OCR med Aspose i Python

Har du någonsin undrat **how to rotate image** så att en OCR-motor faktiskt kan läsa texten? Kanske skannade du ett formulär som blev liggande, eller ett foto som roterades 90° medurs. I så fall ser texten bra ut för det mänskliga ögat, men OCR-motorn ser ett kaos. Den goda nyheten? Det är en barnlek att rätta orienteringen, beskära det område du är intresserad av och sedan extrahera texten—allt med några rader Python och Aspose‑bibliotek.

I den här handledningen går vi igenom hela arbetsflödet: från att ladda en roterad TIFF, korrigera dess orientering, **preprocess image for OCR**, och slutligen **recognize text from image**. I slutet kommer du att veta **how to perform OCR** på vilken bild som helst och kunna **extract text from image**‑filer med förtroende.

## Vad du behöver

- Python 3.8+ (koden fungerar med vilken nyare version som helst)
- `asposeocrjava` och `asposeimaging` paket installerade via `pip`
- En exempelbild som behöver rotation (t.ex. `rotated_form.tif`)
- Lite nyfikenhet på bildbehandling

Inga tunga ramverk krävs—bara de två Aspose‑paketen och lite Python‑logik.

---

## Steg 1: Installera Aspose‑paket (How to Perform OCR)

Innan vi kan **rotate image** eller **recognize text from image**, behöver vi biblioteken som faktiskt utför det tunga arbetet.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Om du sitter bakom en företagsproxy, lägg till `--proxy http://proxy:port` till kommandot. Paketen är rena Python‑wrappers runt Aspose .NET/Java‑kärnan, så installationen är vanligtvis omedelbar.

---

## Steg 2: Ladda källfilen och rotera den – Kärnan “How to Rotate Image”-steget

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Why rotate?** De flesta OCR‑motorer antar att text läses från vänster till höger och uppifrån och ner. Om bitmapen är liggande kommer motorn antingen att returnera nonsens eller inget alls. Att rotera justerar pixelgittret med den förväntade läsordningen, vilket dramatiskt förbättrar noggrannheten.

> **Edge case:** Om du är osäker på om bilden behöver en 90°, 180° eller 270° rotation, kan du inspektera `source_image.width` vs `source_image.height` eller använda `exif`‑orienteringstaggar. Asposes `rotate_flip`‑metod stödjer också `ROTATE_180` och `ROTATE_270_CLOCKWISE`.

> **Bildförhandsgranskning (valfritt):**  
> ![how to rotate image example](/assets/rotate-demo.png "How to rotate image – before and after rotation")

---

## Steg 3: Beskär intresseområdet – Preprocess Image for OCR

Ofta behöver du bara en liten del av sidan—t.ex. ett signaturfält eller ett block med siffror. Beskärning tar bort brus och snabbar upp **how to perform OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Why crop?** Att minska bildstorleken begränsar OCR‑motorns sökrum, vilket minskar falska positiva och kortar ner behandlingstiden. Det hjälper också om källfilen innehåller vattenstämplar eller annan grafik som kan förvirra motorn.

> **Tip:** Om du hanterar flera fält, upprepa beskärningssteget med olika rektanglar och kör OCR på varje del separat.

---

## Steg 4: Initiera OCR‑motorn – “How to Perform OCR”-kärnan

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Behind the scenes:** Aspose OCR använder en kombination av Tesseract och proprietär bildanalys. Att instansiera motorn en gång och återanvända den för flera bilder är mer effektivt än att skapa ett nytt objekt varje gång.

---

## Steg 5: Mata in den beskurna bilden och igenkänn text – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Förväntat resultat

Om ROI innehåller frasen “Invoice #12345 – Paid”, kommer du att se något liknande:

```
Invoice #12345 – Paid
```

Om OCR‑motorn har problem kan du få extra mellanslag eller felaktigt lästa tecken (t.ex. “Invo1ce #I2345 – Pa1d”). Det är då **preprocess image for OCR**‑knep—som att justera kontrast eller applicera binarisering—kommer in i bilden. Aspose erbjuder ytterligare filter som du kan kedja före steg 5, men det grundläggande flödet ovan fungerar för de flesta rena skanningar.

---

## Steg 6: Valfritt – Finjustera OCR‑inställningarna (Advanced “How to Perform OCR”)

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **When to use:** Använd detta när dokumentet innehåller många dekorativa symboler som du inte bryr dig om. Svartlistning minskar falska detekteringar.

---

## Fullt end‑to‑end‑script

När allt sätts ihop, här är ett färdigt skript som **how to rotate image**, **preprocess image for OCR**, och slutligen **recognize text from image**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

När du kör detta skript skrivs den igenkända texten ut till konsolen och en bild av den bearbetade ROI sparas som `processed_roi.png`. Du kan öppna den PNG‑filen för att verifiera att rotationen och beskärningen fungerade som förväntat.

---

## Vanliga frågor & fallgropar

| Question | Answer |
|----------|--------|
| **Vad händer om bilden redan är rätt orienterad?** | Rotationssteget är idempotent—att rotera en korrekt orienterad bild med 90° kommer naturligtvis att förstöra den, så du bör inspektera `source_image.width` vs `height` eller använda EXIF‑orienteringsdata innan du anropar `rotate_flip`. |
| **Mitt OCR‑resultat innehåller extra radbrytningar.** | Använd `result.get_text().replace("\n", " ").strip()` för att rensa upp, eller aktivera `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Kan jag bearbeta PDF‑filer direkt?** | Ja—Aspose Imaging kan läsa in PDF‑sidor som bilder (`Image.load("file.pdf")`), varefter du följer samma rotations‑ och OCR‑steg. |
| **Finns det ett sätt att batch‑processa många filer?** | Placera `ocr_rotated_image` i en loop över en katalog, eller använd Python’s `concurrent.futures` för att parallellisera. |
| **Hur hanterar jag språk annat än engelska?** | Ställ in igenkänningsspråket via `ocr_engine.get_recognition_settings().set_recognition_language("fr")` för franska, osv. |

---

## Slutsats

Vi har gått igenom **how to rotate image** korrekt, **preprocess image for OCR** genom beskärning, och slutligen **how to perform OCR** för att **recognize text from image** och **extract text from image** med Asposes Python‑bibliotek. Det kompletta skriptet visar ett praktiskt, produktionsklart arbetsflöde som du kan lägga in i vilken automationspipeline som helst.

Om du är redo att gå vidare, prova att experimentera med:

- **Image enhancement** (kontrast, binarisering) före OCR
- **Multiple ROI extraction** för formulär med flera fält
- **Batch processing** av hela mappar med skannade dokument
- **Integration** med downstream‑system (t.ex. mata in extraherad data i en databas)

Känn dig fri att anpassa koden till ditt eget användningsfall, och lycka till med kodandet! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}