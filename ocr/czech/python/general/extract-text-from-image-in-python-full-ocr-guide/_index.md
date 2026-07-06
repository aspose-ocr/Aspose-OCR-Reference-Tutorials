---
category: general
date: 2026-06-25
description: Extrahujte text z obrázku pomocí Python OCR. Naučte se, jak načíst obrázek
  pro OCR, provést OCR v Pythonu a převést účtenku do JSON během několika jednoduchých
  kroků.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: cs
og_description: Extrahujte text z obrázku pomocí OCR v Pythonu. Tento tutoriál vás
  provede načtením obrázku pro OCR, provedením OCR v Pythonu a převodem účtenky do
  formátu JSON.
og_title: Extrahování textu z obrázku v Pythonu – Kompletní průvodce OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Extrahovat text z obrázku v Pythonu – Kompletní průvodce OCR
url: /cs/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v Pythonu – Kompletní průvodce OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nevedeli jste, kde začít? V tomto tutoriálu vás provedeme tím, jak **načíst obrázek pro OCR**, **provést OCR v Pythonu** a **převést účtenku do JSON** – vše pomocí několika řádků kódu.

Pokud jste někdy vytvářeli aplikaci pro skenování účtenek, sledovač výdajů nebo jen chcete automatizovat zadávání dat, uvidíte, proč je zvládnutí tohoto postupu průlomové. Na konci budete mít funkční skript, který načte obrázek účtenky a vygeneruje čistý JSON payload připravený pro následné služby.

## Co se naučíte

1. **Vytvořit instanci OCR enginu** – vstupní bod pro veškerou rozpoznávací práci.  
2. **Načíst obrázek pro OCR** – říct enginu, který soubor má načíst.  
3. **Zvolit výstupní formát** – JSON nebo XML, zvolíme JSON, protože je snazší jej použít.  
4. **Spustit rozpoznávání** – skutečně provést OCR v Pythonu.  
5. **Vytisknout nebo uložit výsledek** – převést účtenku do JSON a zobrazit výstup.

Předchozí zkušenost s OCR není vyžadována; stačí základní nastavení Pythonu a soubor s obrázkem (účtenka, leták, cokoliv potřebujete).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="diagram ukazující tok extrahování textu z obrázku pomocí Python OCR"}

## Extrahování textu z obrázku – Krok za krokem Python OCR

Níže je kompletní, připravený ke spuštění skript. Klidně jej zkopírujte do souboru s názvem `receipt_ocr.py` a spusťte `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Proč to funguje

- **Instance enginu** – `aocr.OcrEngine()` zapouzdřuje veškerou těžkou práci (načítání modelu, předzpracování atd.).  
- **Načítání obrázku** – `engine.load_image()` říká knihovně přesně, který bitmap má analyzovat; můžete použít JPEG, PNG nebo i vícestránkové PDF.  
- **Výstupní formát** – Nastavením `engine.export_format` na `aocr.ExportFormat.JSON` získáte strukturovaný řetězec, ideální pro API, která očekávají JSON.  
- **Volání rozpoznání** – `engine.recognize()` spouští inferenci neuronové sítě na pozadí; vrací JSON řetězec, který obsahuje detekované textové bloky, skóre spolehlivosti a informace o rozložení.  

---

## Načtení obrázku pro OCR s aocr

Pokud se ptáte, zda obrázek potřebuje nějaké speciální předzpracování, stručná odpověď je **ne**—`aocr` automaticky zvládne většinu běžných případů (úprava kontrastu, vyrovnání). Přesto můžete přesnost zlepšit takto:

- Zajistit, aby obrázek měl alespoň 300 dpi.  
- Oříznout irelevantní okraje.  
- Převést na odstíny šedi před načtením (volitelné, `engine.load_image()` to udělá za vás).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Tip:* Pokud účtenka obsahuje hodně šumu, výše uvedený krok může výrazně zvýšit přesnost **perform OCR in Python**.

---

## Zvolte výstupní formát a převěďte účtenku do JSON

Možná se ptáte, „Proč ne získat jen prostý text?“ Protože JSON zachovává hierarchickou strukturu (řádky, slova, ohraničující rámečky). To výrazně usnadňuje mapování polí jako *celková částka* nebo *datum* později.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Když spustíte skript, `json_result` bude vypadat zhruba takto (zkráceno pro stručnost):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Nyní máte **convert receipt to JSON** payload, který můžete přímo poslat do databáze, REST endpointu nebo modelu strojového učení.

---

## Spusťte rozpoznávání a získejte výsledky

Poslední krok—skutečné provedení OCR—je tak jednoduchý jako zavolat `recognize()`. Knihovna na pozadí:

1. Odešle obrázek přes předtrénovanou konvoluční síť.  
2. Dekóduje výstup sítě do čitelných znaků.  
3. Zabalí vše do vybraného formátu (JSON v našem případě).  

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Pokud potřebujete výstup uložit místo vytištění, stačí jej zapsat do souboru:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Hraniční případ:* Některé účtenky obsahují ne‑ASCII znaky (např. „€“). Ujistěte se, že soubor otevřete s kódováním UTF‑8, jak je ukázáno výše, aby nedošlo k poškození textu.

---

## Kompletní funkční příklad (všechny kroky v jednom skriptu)

Spojením všeho dohromady, zde je finální skript, který můžete spustit od začátku do konce:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Spusťte jej pomocí:

```bash
python receipt_ocr.py
```

Měli byste vidět potvrzovací řádek a ve stejném adresáři soubor `receipt_output.json` obsahující strukturovaná data.

---

## Závěr

Nyní víte **jak extrahovat text z obrázku** pomocí Pythonu, jak **načíst obrázek pro OCR**, jak **provést OCR v Pythonu** a jak **convert receipt to JSON** pro následnou konzumaci. Tento end‑to‑end postup je nenáročný, vyžaduje pouze balíček `aocr` a lze jej vložit do libovolného automatizačního pipeline.

Co dál? Zkuste změnit výstupní formát na XML, experimentujte s různými technikami předzpracování obrázku nebo vytvořte malou Flask API, která přijme nahranou účtenku a okamžitě vrátí JSON payload. Možnosti jsou neomezené, jakmile ovládnete základy.

Máte otázky nebo narazili na problém? Zanechte komentář níže a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahování textu z obrázku s Aspose OCR – krok za krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrahování textu z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)
- [Jak extrahovat tabulku z obrázku pomocí Aspose.OCR pro .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}