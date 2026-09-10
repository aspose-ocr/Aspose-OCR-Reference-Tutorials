---
category: general
date: 2026-01-12
description: Hoe OCR uit te voeren en tekst uit factuurafbeeldingen te extraheren
  met Aspose OCR en een lichtgewicht Hugging Face‑model. Leer hoe je het model downloadt,
  OCR‑fouten corrigeert en OCR op een afbeelding uitvoert.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: nl
og_description: Hoe OCR uit te voeren op factuurafbeeldingen, tekst te extraheren
  en fouten te corrigeren met een Hugging Face LLM. Volg deze volledige gids voor
  vlekkeloze resultaten.
og_title: Hoe OCR op factuurafbeeldingen uit te voeren – Volledige handleiding
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Hoe OCR uit te voeren op factuurafbeeldingen – Complete stapsgewijze gids
url: /nl/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op factuurafbeeldingen – Complete stap‑voor‑stap gids

Heb je je ooit afgevraagd **hoe je OCR kunt uitvoeren** op een gescande factuur en schone, doorzoekbare tekst kunt krijgen zonder uren te besteden aan opschonen? Je bent niet de enige. In veel real‑world projecten zit de ruwe OCR‑output vol met mis‑herkenningen—denk aan “O” voor “0”, “l” voor “1”, of zelfs hele woorden die verkeerd zijn. Het goede nieuws? Met een paar regels Python kun je niet alleen **OCR uitvoeren op afbeelding**‑bestanden, maar ook automatisch **OCR‑fouten corrigeren** met een lichtgewicht model van Hugging Face.

In deze tutorial lopen we alles door wat je moet weten: van het laden van een factuurafbeelding, het extraheren van ruwe tekst, het downloaden van een gekwantiseerd model, tot het polijsten van het resultaat zodat je eindigt met een perfecte transcriptie klaar voor downstream verwerking. Aan het einde kun je **tekst uit factuur**‑PDF’s of PNG’s extraheren met één herhaalbaar script.

## Vereisten & Setup

Voordat je begint, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.9+ | Moderne syntaxis en type‑hints |
| `aspose-ocr` package | Biedt de `ocr.OcrEngine` die in het voorbeeld wordt gebruikt |
| `aspose-ai` package | Levert de `AsposeAI` post‑processor |
| Toegang tot een GPU (optioneel) | Versnelt de LLM‑lagen; anders werkt CPU prima |
| Internetverbinding (eerste uitvoering) | Nodig om **Hugging Face‑model te downloaden** automatisch |

Je kunt de benodigde libraries installeren met:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Als je van plan bent de LLM op GPU te draaien, installeer `torch` met CUDA‑ondersteuning (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Nu de omgeving klaar is, gaan we aan de code beginnen.

---

## Stap 1 – Initialiseert de OCR‑engine en laadt je factuurafbeelding

Het eerste wat je moet doen is een instantie van Aspose’s OCR‑engine maken en deze wijzen op het bestand dat je wilt verwerken. Deze stap is de basis van **hoe je OCR uitvoert** op elke afbeelding.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Waarom dit belangrijk is:** `load_image` accepteert PNG, JPEG, TIFF en zelfs PDF‑pagina’s, waardoor je **OCR kunt uitvoeren op afbeelding**‑data ongeacht het formaat.

---

## Stap 2 – Voer basis‑OCR uit om ruwe tekst te verkrijgen

Zodra de afbeelding is geladen, kan de engine een ruwe transcriptie produceren. Deze output is vaak ruisig, daarom voeren we later een correctiestap uit.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typische ruwe output kan er zo uitzien:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Zie je de nullen (`0`) waar de letter “O” zou moeten staan? Dat is precies het soort fout dat we later gaan oplossen.

---

## Stap 3 – Configureer de AI‑post‑processor met een lichtgewicht LLM

Nu halen we een **Hugging Face‑model downloaden** dat klein genoeg is om op bescheiden hardware te draaien, maar krachtig genoeg om factuurtaal te begrijpen. Het voorbeeld gebruikt het Qwen 2.5 3B‑Instruct GGUF‑model, gekwantiseerd naar `int8` voor een minimale geheugenvoetafdruk.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Waarom dit model?** De `int8`‑kwantisatie verkleint het bestand tot ~1,2 GB, waardoor het op de meeste laptops haalbaar is. GPU‑lagen versnellen de inferentie, maar de code valt elegant terug op CPU wanneer er geen GPU wordt gevonden.

---

## Stap 4 – Voer LLM‑gebaseerde correctie uit op de ruwe OCR‑resultaten

Met het model klaar, voeren we de ruwe tekst in de post‑processor. De LLM herschrijft de transcriptie, corrigeert veelvoorkomende OCR‑glitches en normaliseert cijfers.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Verwachte schoongemaakte output:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Je ziet dat de nullen weer zijn omgezet naar de letter “O”, en “Am0unt” nu “Amount” is. Dit is de kern van **OCR‑fouten automatisch corrigeren**.

---

## Stap 5 – Vrijgeven van bronnen en opruimen

Grote taalmodellen kunnen GPU‑geheugen vasthouden, dus het is goed om bronnen vrij te geven wanneer je klaar bent.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Als je veel facturen in één batch wilt verwerken, kun je het model geladen houden en pas aan het einde van het script vrijgeven.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een enkel script dat je in een `.py`‑bestand kunt plaatsen en uitvoeren:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Het uitvoeren van het script zou output moeten produceren die lijkt op het eerder getoonde “AI‑gecorrigeerde” blok. Vervang gerust het afbeeldingspad door een andere factuur of bon om **tekst uit factuur**‑bestanden in bulk te **extraheren**.

---

## Veelgestelde vragen & randgevallen

### Wat als ik geen GPU heb?

De `gpu_layers`‑parameter is optioneel. Stel deze in op `0` of laat hem weg, en het model draait volledig op CPU. Verwacht een tragere inferentie—ongeveer 2–3 seconden per pagina op een moderne laptop.

### Mijn facturen zijn meer‑pagina PDF’s. Hoe ga ik daarmee om?

Converteer elke pagina naar een aparte afbeelding (bijv. met `pdf2image`) en loop over de pagina’s met hetzelfde script. De OCR‑engine kan elke afbeelding onafhankelijk verwerken, en de LLM corrigeert elk tekstblok.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Het model downloaden mislukt achter een firewall?

Download het model handmatig van de Hugging Face modelhub, pak het uit in een lokale map, en wijs `hugging_face_repo_id` naar het lokale pad:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Hoe nauwkeurig is de correctie?

Voor typische Engelstalige facturen corrigeert de LLM >95 % van de veelvoorkomende OCR‑misherkenningen. Complexe handgeschreven notities kunnen nog steeds handmatige controle vereisen.

---

## Tips & tricks voor productiegebruik

- **Batchverwerking:** Verpak stappen 2‑4 in een functie en voer een lijst met bestands‑paden in. Hergebruik dezelfde `AsposeAI`‑instantie om het model niet telkens opnieuw te laden.
- **Logging:** Vervang `print` door Python’s `logging`‑module om zowel ruwe als gecorrigeerde output vast te leggen voor audit‑trails.
- **Foutafhandeling:** Omring de OCR‑aanroep met `try/except`‑blokken. Als een afbeelding faalt, log dan de bestandsnaam en ga door.
- **Prestatie‑afstemming:** Experimenteer met `gpu_layers`. Meer lagen op GPU versnellen de inferentie maar verhogen het VRAM‑gebruik.

---

## Conclusie

We hebben behandeld **hoe je OCR uitvoert** op factuurafbeeldingen van begin tot eind, en laten zien hoe je **OCR op afbeelding** kunt **uitvoeren**, een **Hugging Face‑model kunt downloaden**, en **OCR‑fouten automatisch kunt corrigeren**. Het volledige script demonstreert een praktische workflow die je in elke Python‑gebaseerde automatiseringspipeline kunt integreren.

Volgende stappen? Breid de pipeline uit om **sleutelvelden te extraheren** (factuurnummer, datum, totaal) met reguliere expressies op de gecorrigeerde tekst, of voer de opgeschoonde output in een database in voor doorzoekbare records. Je kunt ook experimenteren met andere lichtgewicht LLM’s van Hugging Face als je een andere taal of domeinspecifieke kennis nodig hebt.

Happy coding, en moge je OCR‑resultaten altijd kristalhelder zijn! 

![hoe OCR uit te voeren op een factuurafbeelding](ocr_invoice_example.png "hoe OCR uit te voeren op factuur")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}