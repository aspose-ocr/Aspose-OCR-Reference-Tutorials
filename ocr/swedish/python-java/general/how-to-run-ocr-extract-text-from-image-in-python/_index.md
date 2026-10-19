---
category: general
date: 2026-03-26
description: Hur man kör OCR på en PNG-fil och extraherar text från bilden med en
  anpassad ordlista för förbättrad OCR‑noggrannhet. Lär dig att snabbt ladda bilden
  för OCR.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: sv
og_description: Hur du kör OCR på en PNG‑fil och extraherar text från bilden med en
  anpassad ordlista för förbättrad OCR‑noggrannhet. Steg‑för‑steg‑guide.
og_title: Hur man kör OCR – Extrahera text från bild i Python
tags:
- OCR
- Python
- Image Processing
title: Hur man kör OCR – Extrahera text från bild i Python
url: /sv/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kör OCR – Extrahera text från bild i Python

Har du någonsin undrat **hur man kör OCR** på en skannad faktura eller en skärmdump och får ren, sökbar text? Du är inte ensam. I många projekt är flaskhalsen helt enkelt att ladda bilden för OCR och sedan övertala motorn att förstå domänspecifika ord.  

I den här handledningen går vi igenom ett komplett, färdigt exempel som **extraherar text från bild**‑filer, visar dig hur du **läser av text från PNG**‑tillgångar, och demonstrerar även knep för att **förbättra OCR‑noggrannhet** med anpassade ordböcker och specialtecken. I slutet har du ett självständigt skript som du kan släppa in i vilken Python‑kodbas som helst.

## Vad du behöver

- Python 3.8+ (koden använder typ‑hints men fungerar på tidigare 3.x‑versioner)
- `ocr`‑biblioteket som följer med OCR‑motorn du riktar dig mot (installera via `pip install ocr‑engine` – byt ut mot det faktiska paketnamnet)
- En bildfil (`input.png`) som du vill bearbeta
- Valfritt: en ren‑text‑fil (`invoice_terms.txt`) med domänspecifika ord, ett per rad

Inga tunga externa beroenden, inga moln‑API‑nycklar, bara en lokal OCR‑motor.

---

## Steg 1: Installera och importera OCR‑biblioteket

Först, se till att OCR‑paketet är installerat. Om du använder det hypotetiska `ocr-engine`‑paketet, kör:

```bash
pip install ocr-engine
```

Importera nu klasserna du kommer att behöva:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** Om du använder en virtuell miljö, aktivera den innan du installerar för att hålla din globala Python ren.

## Steg 2: Skapa en OCR‑motorinstans

Att skapa ett motor‑objekt är startpunkten för varje OCR‑uppgift. Tänk på det som att slå på skannings‑hardware i mjukvara.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Varför detta är viktigt: motorn håller konfiguration som språkpaket, igenkänningslägen och eventuella anpassade resurser du kommer att bifoga senare. Utan den kan du inte **ladda bild för OCR** eller köra igenkännings‑pipeline.

## Steg 3: Ladda bilden du vill känna igen

Här **laddar vi faktiskt bild för OCR**. Metoden `Imaging.Image.load()` läser filen och konverterar den till det interna bitmap‑format som motorn förväntar sig.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Om du har en JPEG eller TIFF fungerar samma metod – byt bara filändelsen. Motorn upptäcker automatiskt formatet.

> **Edge case:** Mycket stora bilder (över 5 MP) kan orsaka minnesspikar. Överväg att skala ner med Pillow innan du laddar om du stöter på prestandaproblem.

## Steg 4: Tillhandahåll en anpassad ordbok för att öka noggrannheten

De flesta OCR‑motorer levereras med generiska språkmodeller. För fakturor, kvitton eller juridiska dokument ser du ofta missade ord. Att tillhandahålla en anpassad ordlista säger till motorn “de här termerna är legitima, behandla dem som korrekta”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typiska poster kan vara:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Att lägga till dessa förbättrar **förbättra OCR‑noggrannhet**‑metrik dramatiskt – särskilt för icke‑ASCII‑symboler.

## Steg 5: Lägg till specialtecken som inte täcks av standarduppsättningen

Om din domän använder symboler som Euro‑tecknet (€) eller den skandinaviska Ø, kan du explicit lägga till dem:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Motorn kommer nu att behandla dessa glyfer som giltiga under igenkänningsfasen, vilket minskar risken för “skräp”‑utdata.

## Steg 6: Kör OCR‑processen och hämta texten

Till sist, anropa igenkännaren och hämta ren‑text‑resultatet. Anropet `recognize()` returnerar ett rikt objekt; vi behöver bara den råa strängen för de flesta användningsfall.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Förväntad utdata** (avkortad för korthet):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Om utdata ser förvrängd ut, dubbelkolla att din anpassade ordbok och specialtecken är korrekt laddade.

---

## Visuell översikt

![how to run OCR diagram](ocr-workflow.png){alt="hur man kör OCR-diagram"}

Diagrammet ovan illustrerar flödet från att ladda en bild till att få ren text, och markerar var du kan injicera anpassade ordböcker och teckensätt.

---

## Vanliga frågor & fallgropar

### Fungerar detta med flersidiga PDF-filer?

Ja – konvertera bara varje sida till en PNG (med `pdf2image` eller liknande) och mata in dem sekventiellt i samma `ocr_engine`‑instans. Motorn bearbetar varje bild oberoende, så du får en lista med strängar som du kan sammanfoga.

### Vad händer om bilden är roterad?

De flesta moderna OCR‑motorer upptäcker automatiskt orientering, men du kan tvinga en rotation med:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Hur hanterar man språk annat än engelska?

Byt språkmodell innan du laddar bilden:

```python
ocr_engine.set_language("de")  # German
```

Se till att motsvarande språkpaket är installerat.

## Fullt skript – Klart att kopiera & klistra in

Nedan är hela programmet, klart att köras efter att du ersatt platshållar‑sökvägarna.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Kör det med:

```bash
python run_ocr.py
```

Du bör se den extraherade texten skriven till konsolen. Därefter kan du skriva den till en fil, föra in den i en databas, eller skicka den vidare till efterföljande NLP‑pipelines.

## Sammanfattning & nästa steg

Vi har gått igenom **hur man kör OCR** på en PNG, hur man **extraherar text från bild**, och visat praktiska sätt att **läsa av text från PNG** samtidigt som vi **förbättrar OCR‑noggrannhet** med ordböcker och anpassade tecken.  

Nästa steg, överväg:

- **Batch‑behandling:** Loopa över en katalog med bilder.
- **Efterbehandling:** Använd regex för att plocka ut fakturanummer eller datum.
- **Integration:** Koppla skriptet till ett Flask‑API för OCR‑tjänster på begäran.

Om du är nyfiken på mer avancerade ämnen, kolla in handledningar om **ladda bild för OCR** med OpenCV‑förbehandling, eller dyka ner i djup‑inlärningsbaserade OCR‑modeller som Tesseract 4+ med LSTM‑lager.

### Fortsätt experimentera!

Prova att byta ut `invoice_terms.txt` mot en lista med medicinsk terminologi, lägg till grekiska tecken, eller mata in motorn med ett lågupplöst foto för att se hur långt noggrannheten kan sträcka sig. Ju mer du pysslar, desto bättre förstår du avvägningarna mellan förbehandling, anpassade vokabulärer och motorinställningar.

Lycka till med kodandet, och må dina OCR‑resultat alltid vara skarpa!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}