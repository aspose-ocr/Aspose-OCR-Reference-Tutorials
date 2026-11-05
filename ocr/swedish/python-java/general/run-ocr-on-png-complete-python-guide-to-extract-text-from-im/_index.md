---
category: general
date: 2026-01-12
description: Kör OCR på PNG-filer snabbt med Python. Lär dig hur du extraherar text
  från bild och faktura, och laddar bild för OCR med Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: sv
og_description: Kör OCR på PNG direkt. Den här guiden visar hur du extraherar text
  från bild och faktura, laddar bilden för OCR och sparar resultaten som JSON och
  CSV.
og_title: Kör OCR på PNG – Fullständig Python-handledning
tags:
- OCR
- Python
- Image Processing
title: Kör OCR på PNG – Komplett Python-guide för att extrahera text från bilder
url: /sv/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kör OCR på PNG – Komplett Python‑guide för att extrahera text från bilder

Har du någonsin behövt **köra OCR på PNG**‑filer men varit osäker på vilket bibliotek som ger rena, strukturerade resultat? Du är inte ensam. I många verkliga projekt—tänk fakturautomatisk eller kvittoskanning—är första steget att **extrahera text från bild**‑filer, och PNG är ett vanligt format eftersom det bevarar förlustfri kvalitet.

I den här handledningen går vi igenom ett praktiskt exempel med Aspose.OCR‑paketet för Python. I slutet av guiden vet du hur du **laddar bild för OCR**, hämtar varje textrad, omvandlar datan till ett prydligt JSON‑objekt och till och med sparar det som CSV för vidare bearbetning. Inga onödiga detaljer, bara en praktisk, färdig‑att‑köra lösning.

## Vad du kommer att lära dig

- Hur du installerar och importerar Aspose.OCR‑biblioteket.  
- De exakta stegen för att **köra OCR på PNG** och hantera resultatobjektet.  
- Sätt att **extrahera text från faktura**‑filer och formatera utdata som JSON eller CSV.  
- Tips för att hantera lågkontrastbilder, flerspråkiga dokument och förtroendescore.  
- Ett komplett, kopiera‑och‑klistra‑kodexempel som du kan köra idag.

> **Förutsättning:** Python 3.8+ och grundläggande kunskap om pip. Om du aldrig har använt Aspose tidigare, oroa dig inte—denna guide täcker allt du behöver för att komma igång.

---

## Steg 1 – Installera Aspose.OCR och förbered din miljö

Innan vi kan **köra OCR på PNG** måste biblioteket finnas på ditt system.

```bash
pip install aspose-ocr
```

> **Pro tip:** Använd ett virtuellt miljö (`python -m venv venv`) för att hålla beroenden isolerade. Det förhindrar versionskonflikter om du jonglerar flera projekt.

När installationen är klar, importera de moduler vi kommer att behöva:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Här importerar vi `asposeocr` för den tunga lyftningen och det inbyggda `json`‑biblioteket för senare serialisering.

---

## Steg 2 – Skapa OCR‑motorn och ange språk

OCR‑motorn är kärnkomponenten som faktiskt läser pixlarna. För de flesta engelska fakturor vill du använda det engelska språkpaketet:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Varför detta är viktigt:** Att specificera språk begränsar teckenuppsättningen, vilket ökar noggrannheten och snabbar upp bearbetningen. Om du någonsin behöver hantera flerspråkiga fakturor, byt bara ut `ocr.Language.ENGLISH` mot rätt enum.

---

## Steg 3 – Ladda bilden för OCR

Nu **laddar vi bild för OCR**. Metoden `Image.load` accepterar en filsökväg och fungerar med PNG, JPEG, BMP och fler.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Om PNG‑filen är ovanligt stor (över 5 MB), överväg att skala ner den först för att hålla minnesanvändningen rimlig. Pillow kan göra det i en enda rad:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Steg 4 – Kör OCR på PNG och fånga resultatet

Med motorn redo och bilden laddad är det dags att **köra OCR på PNG** och hämta det strukturerade resultatet.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result`‑objektet innehåller en samling `OcrRegion`‑objekt, var och en med den igenkända texten och ett förtroendescore (0‑100). Här får du den granulära data som behövs för att **extrahera text från faktura**‑rader.

---

## Steg 5 – Konvertera resultatet till JSON och pretty‑printa det

De flesta downstream‑system älskar JSON, så vi omvandlar OCR‑utdata till en snyggt formaterad sträng.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Exempel på utdata

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Lägg märke till hur varje rad innehåller ett förtroendemått—perfekt för att filtrera bort lågt förtroende om du planerar att **extrahera text från faktura** automatiskt.

---

## Steg 6 – Spara OCR‑data som CSV (En rad per text + förtroende)

CSV är idealiskt för kalkylblad eller snabba dataimporter. Aspose erbjuder en end‑liner för att dumpa allt till en CSV‑fil.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Den genererade CSV‑filen kommer att se ut så här:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Du kan nu öppna den i Excel, Google Sheets eller mata in den i en databas.

---

## Bonus – Hantera låg‑förtroende‑text och flersidiga PDF‑er

### Filtrering efter förtroende

Om du bara vill ha rader med hög säkerhet, filtrera JSON innan du skriver ut den:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Flersidiga dokument

Aspose.OCR skapar automatiskt ett nytt `page`‑objekt för varje sida i en flersidig PNG eller PDF. Loopa igenom `ocr_data["pages"]` för att bearbeta dem alla—ingen extra kod behövs.

---

## Fullt fungerande exempel

Nedan är **det kompletta skriptet** som du kan kopiera, klistra in och köra omedelbart. Ersätt `YOUR_DIRECTORY` med mappen som innehåller din PNG‑fil.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Kör skriptet med `python run_ocr.py` så ser du JSON‑dumpen i konsolen, en CSV‑fil på disk och en filtrerad lista med hög‑förtroende‑poster.

---

## Vanliga frågor

**Q: Kan jag använda detta för att extrahera text från ett skannat kvitto istället för en faktura?**  
A: Absolut. Samma arbetsflöde gäller—pek bara `image_path` på ditt kvitto‑PNG. Om kvittot använder ett annat språk, byt `engine.language` därefter.

**Q: Vad händer om min PNG innehåller roterad text?**  
A: Aspose.OCR upptäcker automatiskt orientering, men för envisa fall kan du manuellt rotera bilden med Pillow innan du skickar den till motorn.

**Q: Behöver jag en betald licens för Aspose.OCR?**  
A: Biblioteket erbjuder ett gratis utvärderingsläge med ett vattenstämpel på utdata. För produktionsbruk behöver du en licens, som du kan skaffa från Aspose‑webbplatsen.

---

## Slutsats

Vi har gått igenom allt du behöver för att **köra OCR på PNG**‑filer med Python: installera SDK, ladda bilden, extrahera strukturerad text och spara resultatet som JSON eller CSV. Oavsett om du vill **extrahera text från bild** för ett enkelt skript eller **extrahera text från faktura** för en automatiserad bokföringspipeline, ger stegen ovan en solid, produktionsklar grund.

Nästa steg kan vara att:

- Integrera CSV‑utdata med en databas för masslagring av fakturor.  
- Lägga till efterbehandling med reguljära uttryck för att plocka ut datum, belopp eller skatte‑ID.  
- Använda `ocr_engine.recognize_barcode`‑funktionen om dina fakturor innehåller QR‑koder.

Prova, justera förtroendetrösklarna och se ditt dokument‑bearbetningsflöde bli en barnlek. Har du fler frågor eller ett coolt användningsfall att dela? Kommentera nedan—lycka till med OCR!  

![Kör OCR på PNG‑exempel](run-ocr-on-png.png "Kör OCR på PNG – visuell exempel på OCR‑resultat")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}