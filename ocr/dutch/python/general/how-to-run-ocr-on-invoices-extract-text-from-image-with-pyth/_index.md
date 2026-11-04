---
category: general
date: 2026-01-07
description: Hoe OCR uit te voeren en tekst uit een afbeelding te extraheren voor
  factuurverwerking. Leer de OCR‑nauwkeurigheid te verbeteren, een afbeelding te laden
  voor OCR, en factuur‑OCR efficiënt te verwerken.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: nl
og_description: Hoe OCR op facturen stap‑voor‑stap uit te voeren. Tekst uit afbeelding
  extraheren, OCR‑nauwkeurigheid verbeteren en afbeelding laden voor OCR met Aspose
  AI.
og_title: Hoe OCR op facturen uit te voeren – Complete Python-gids
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR op facturen uit te voeren – Tekst uit afbeelding halen met Python
url: /nl/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op facturen – Tekst uit afbeelding halen met Python

Heb je je ooit afgevraagd **hoe je OCR** kunt uitvoeren op een gescande factuur en schone, doorzoekbare tekst kunt krijgen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer de ruwe OCR‑uitvoer vol staat met spelfouten, gebroken regeleinden en ontbrekende interpunctie. In deze tutorial lopen we een full‑stack oplossing door die niet alleen **tekst uit afbeelding** extraheert, maar ook **OCR‑nauwkeurigheid verbetert** door post‑processing met een Aspose AI‑model.

Je zult zien hoe je **afbeelding laadt voor OCR**, de ingebouwde engine uitvoert en vervolgens een lichte spell‑check toepast die het resultaat klaar maakt voor downstream‑analyse. Aan het einde heb je een herbruikbaar script dat je in elke factuur‑verwerkingspipeline kunt plaatsen.

> **Wat je nodig hebt**  
> * Python 3.9 of nieuwer  
> * `aspose-ocr` en `aspose-ai` pakketten (geïnstalleerd via `pip`)  
> * Een factuurafbeelding (PNG, JPEG, of TIFF) – we gebruiken `sample_invoice.png` als voorbeeld  
> * Optioneel: een GPU met minstens 4 GB VRAM voor snellere model‑inference (het script werkt ook op CPU)

---

## Stap 1: Installeer vereiste pakketten en bereid de omgeving voor

Voordat we **afbeelding kunnen laden voor OCR**, moeten we ervoor zorgen dat de benodigde bibliotheken beschikbaar zijn. De Aspose OCR‑engine wordt geleverd met een eenvoudige Python‑wrapper, terwijl de AI‑post‑processor afhankelijk is van een gekwantiseerd model van Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Als je GPU‑versnelling wilt gebruiken, installeer dan `torch` met CUDA‑ondersteuning (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Stap 2: Laad de factuurafbeelding

Het laden van de afbeelding is eenvoudig, maar het is het vermelden waard waarom we het pad expliciet als een raw string (`r"..."`) instellen. Dit voorkomt onbedoelde escape‑character fouten op Windows‑paden.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Waarom dit belangrijk is:* Het gebruik van `ocr.Image.load` garandeert dat de afbeelding vooraf wordt verwerkt (binarisatie, deskew) volgens de optimale standaardinstellingen van Aspose, die al **OCR‑nauwkeurigheid verbetert** voordat er AI‑magie plaatsvindt.

---

## Stap 3: Voer de ingebouwde OCR‑engine uit

Nu voeren we daadwerkelijk **OCR uit** en vangen we de ruwe tekst op. Deze stap toont de typische output die je zou krijgen van een standaard OCR‑run—vaak een rommel van regeleinden en af en toe spelfouten.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typische ruwe output** (afgekapt voor beknoptheid):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Je merkt misschien dat “Invoice” verschijnt als “Invo1ce” of dat interpunctie ontbreekt. Daar komt de AI‑post‑processor in beeld.

---

## Stap 4: Configureer het Aspose AI‑model

Het AI‑model dat we gaan gebruiken is **Qwen2.5‑3B‑Instruct‑GGUF**, een lichtgewicht instruction‑tuned LLM die comfortabel draait op een mid‑range GPU. De onderstaande configuratie vertelt Aspose waar het model moet ophalen, hoeveel lagen op de GPU moeten blijven, en de context‑grootte voor het verwerken van lange alinea's.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Waarom deze configuratie?**  
> * `gpu_layers=30` balanceert snelheid en geheugen—de meeste inferentie gebeurt op de GPU, terwijl de resterende lagen op de CPU blijven om OOM‑fouten te voorkomen.  
> * `context_size=4096` zorgt ervoor dat het model de hele factuur in één keer kan zien, waardoor het voorkomen wordt dat belangrijke velden worden afgekapt.

---

## Stap 5: Maak een eenvoudige spell‑check post‑processor

We zullen de AI‑aanroep verpakken in een kleine functie genaamd `simple_spell_check`. De prompt is opzettelijk beknopt: “Correct spelling and punctuation:” gevolgd door de ruwe OCR‑tekst. Het model retourneert een opgeschoonde versie.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Hoe het werkt:** `ai.run_prompt` stuurt de prompt naar de lokaal geladen LLM, die vervolgens een enkele string teruggeeft met gecorrigeerde spelling, juiste interpunctie en een meer natuurlijke regeleindeling.

---

## Stap 6: Pas de post‑processor toe op de ruwe OCR‑tekst

Nu gebeurt de magie. We voeren de ruwe OCR‑output in onze post‑processor en printen het verbeterde resultaat.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Voorbeeld van verbeterde output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Let op de gecorrigeerde spelling van “Invoice”, correct gebruik van dubbele punten en consistente regeleinden—precies wat je nodig hebt voor betrouwbare downstream‑parsing.

---

## Stap 7: Ruim bronnen op

Zowel de OCR‑engine als het AI‑model reserveren native resources. Het is een goede gewoonte om ze vrij te geven wanneer je klaar bent, vooral in langdurige services.

```python
ai.free_resources()
engine.dispose()
```

---

## Volledig script – Klaar om te plakken

Hieronder staat het volledige, uitvoerbare script dat elke stap met elkaar verbindt. Sla het op als `invoice_ocr.py`, vervang `YOUR_DIRECTORY` door de map die je factuurafbeelding bevat, en voer uit met `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Voer het script uit en je ziet zowel de rommelige ruwe OCR‑dump als de gepolijste, **verbeterde OCR‑nauwkeurigheid** versie naast elkaar.

---

## Veelgestelde vragen & randgevallen

### 1. Wat als mijn factuurafbeelding een meer‑pagina PDF is?

Aspose OCR kan PDF‑pagina's direct laden. Vervang de afbeeldings‑laadregel door:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Itereer over `page_index` om elke pagina opeenvolgend te verwerken.

### 2. Mijn GPU raakt zonder geheugen—kan ik alleen CPU gebruiken?

Zeker. Stel `gpu_layers=0` in de `AsposeAIModelConfig`. Het model draait volledig op CPU, wat trager is maar veilig voor low‑end hardware.

### 3. Hoe ga ik om met niet‑Engelse facturen?

Vervang de model‑repository‑ID door een taalspecifiek model, bijv. `"mistralai/Mistral-7B-Instruct-v0.2"` voor meertalige ondersteuning. De rest van de pipeline blijft ongewijzigd.

### 4. Kan ik meerdere post‑processors ketenen (bijv. datums formatteren, totalen extraheren)?

Ja. `ai.set_post_processor` accepteert een lijst van callables. Bijvoorbeeld:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

---

## Prestatie‑tips & best practices

| Tip | Waarom het helpt |
|-----|-------------------|
| **Batch meerdere facturen** – laad ze in een lijst en verwerk ze in een lus. | Vermindert de overhead van de Python‑interpreter en houdt het AI‑model warm in het geheugen. |
| **Cache het model** – vermijd herhaaldelijk `initialize` aanroepen in een webservice. | Model laden kan ~30 seconden duren; cachen levert directe responsen op. |
| **Resize grote afbeeldingen** tot 1500 px breedte vóór OCR. | Kleinere afbeeldingen versnellen zowel OCR als AI‑inference zonder nauwkeurigheid te verliezen. |
| **Stel `allow_auto_download="false"` in productie** – lever het model mee met je deployment. | Garandeert deterministische opstarttijden en voorkomt netwerkonderbrekingen. |

---

## Conclusie

We hebben behandeld **hoe je OCR uitvoert** op facturen, van het laden van de afbeelding tot het polijsten van het resultaat met een AI‑gedreven spell‑check. Door deze stappen te volgen kun je betrouwbaar **tekst uit afbeelding extraheren**, **OCR‑nauwkeurigheid verbeteren**, en naadloos **factuur‑OCR verwerken** in elke Python‑gebaseerde workflow.

Probeer het met een paar verschillende factuur‑lay-outs—misschien een handgeschreven bon of een gescande overeenkomst. dezelfde pipeline past zich met minimale aanpassingen aan, wat bewijst dat een goed gestructureerde OCR + AI‑combinatie een veelzijdig hulpmiddel is voor elk document‑automatiseringsproject.

Als je deze gids nuttig vond, overweeg dan om hem te delen met teamgenoten of de repository die de Aspose‑pakketten host een ster te geven.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}