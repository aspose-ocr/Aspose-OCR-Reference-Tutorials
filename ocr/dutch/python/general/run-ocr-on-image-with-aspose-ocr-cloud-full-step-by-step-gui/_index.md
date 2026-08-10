---
category: general
date: 2026-03-28
description: Leer hoe je OCR op een afbeelding uitvoert, automatisch een Hugging Face‑model
  downloadt, OCR‑tekst opschoont en een LLM‑model configureert in Python met Aspose OCR
  Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: nl
og_description: Voer OCR uit op een afbeelding en reinig de output met een automatisch
  gedownload Hugging Face‑model. Deze gids laat zien hoe je een LLM‑model configureert
  in Python.
og_title: OCR uitvoeren op afbeelding – Complete Aspose OCR Cloud Tutorial
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Voer OCR uit op afbeelding met Aspose OCR Cloud – Volledige stapsgewijze handleiding
url: /nl/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding – Complete Aspose OCR Cloud Tutorial

Heb je ooit OCR moeten uitvoeren op afbeeldingsbestanden, maar zag de ruwe uitvoer eruit als een warboel? Naar mijn ervaring is het grootste pijnpunt niet de herkenning zelf—het is de opschoning. Gelukkig laat Aspose OCR Cloud je een LLM‑post‑processor koppelen die *OCR‑tekst automatisch kan opschonen*. In deze tutorial lopen we alles door wat je nodig hebt: van **het downloaden van een Hugging Face‑model** tot het configureren van de LLM, het uitvoeren van de OCR‑engine en uiteindelijk het polijsten van het resultaat.

Aan het einde van deze gids heb je een kant‑klaar script dat:

1. Een compact Qwen 2.5‑model van Hugging Face ophaalt (automatisch voor je gedownload).  
2. Het model configureert om een deel van het netwerk op GPU en de rest op CPU te draaien.  
3. De OCR‑engine uitvoert op een afbeelding van een handgeschreven notitie.  
4. De LLM gebruikt om de herkende tekst op te schonen, zodat je mens‑leesbare output krijgt.

> **Prerequisites** – Python 3.8+, `asposeocrcloud`‑package, een GPU met minimaal 4 GB VRAM (optioneel maar aanbevolen), en een internetverbinding voor de eerste model‑download.

---

## Wat je nodig hebt

- **Aspose OCR Cloud SDK** – installeren via `pip install asposeocrcloud`.  
- **Een voorbeeldafbeelding** – bijv. `handwritten_note.jpg` in een lokale map geplaatst.  
- **GPU‑ondersteuning** – als je een CUDA‑enabled GPU hebt, zal het script 30 lagen offloaden; anders valt het automatisch terug op CPU.  
- **Schrijfrechten** – het script cachet het model in `YOUR_DIRECTORY`; zorg dat de map bestaat.

---

## Stap 1 – Configureer het LLM‑model (download Hugging Face model)

Het eerste wat we doen is Aspose AI vertellen waar het model vandaan moet halen. De `AsposeAIModelConfig`‑klasse behandelt auto‑download, kwantisatie en GPU‑laag‑allocatie.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Why this matters** – Kwantiseren naar `int8` bespaart het geheugen drastisch (≈ 4 GB vs 12 GB). Het model splitsen tussen GPU en CPU laat je een 3‑billion‑parameter LLM draaien zelfs op een bescheiden RTX 3060. Als je geen GPU hebt, stel `gpu_layers=0` in en de SDK houdt alles op CPU.

> **Tip:** De eerste uitvoering downloadt ~ 1,5 GB, dus geef het een paar minuten en een stabiele verbinding.

---

## Stap 2 – Initialiseer de AI‑engine met de modelconfiguratie

Nu starten we de Aspose AI‑engine en voeren we de configuratie die we net hebben gemaakt in.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**What’s happening under the hood?** De SDK controleert `directory_model_path` op een bestaand model. Als er een overeenkomende versie wordt gevonden, wordt deze direct geladen; anders downloadt hij het GGUF‑bestand van Hugging Face, pakt het uit en bereidt de inferentie‑pipeline voor.

---

## Stap 3 – Maak de OCR‑engine en koppel de AI‑post‑processor

De OCR‑engine doet het zware werk van het herkennen van tekens. Door `ocr_ai.run_postprocessor` te koppelen, schakelen we **clean OCR text** automatisch in na herkenning.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Why use a post‑processor?** Ruwe OCR bevat vaak regeleinden op de verkeerde plaatsen, fout‑gedetecteerde interpunctie of vreemde symbolen. De LLM kan de output herschrijven naar correcte zinnen, spelling verbeteren en zelfs ontbrekende woorden afleiden—feitelijk een ruwe dump omzetten in gepolijste proza.

---

## Stap 4 – Voer OCR uit op een afbeeldingsbestand

Met alles aangesloten is het tijd om een afbeelding aan de engine te voeren.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Edge case:** Als de afbeelding groot is (> 5 MP), wil je deze eerst verkleinen om de verwerking te versnellen. De SDK accepteert een Pillow `Image`‑object, dus je kunt vooraf verwerken met `PIL.Image.thumbnail()` indien nodig.

---

## Stap 5 – Laat de AI de herkende tekst opschonen en toon beide versies

Tot slot roepen we de post‑processor aan die we eerder hebben gekoppeld. Deze stap toont het contrast tussen *voor* en *na* opschoning.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Verwachte uitvoer

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Let op hoe de LLM:

- Veelvoorkomende OCR‑mis‑herkenningen heeft gecorrigeerd (`Th1s` → `This`).  
- Vreemde symbolen heeft verwijderd (`&` → `and`).  
- Regeleinden heeft genormaliseerd naar correcte zinnen.

---

## 🎨 Visueel overzicht (OCR uitvoeren op afbeelding workflow)

![OCR uitvoeren op afbeelding workflow](run_ocr_on_image_workflow.png "Diagram dat de OCR‑uitvoeren‑op‑afbeelding‑pipeline toont, van model‑download tot opgeschoonde output")

Het diagram hierboven vat de volledige pipeline samen: **download Hugging Face model → configureer LLM → initialiseer AI → OCR‑engine → AI‑post‑processor → clean OCR text**.

---

## Veelgestelde vragen & Pro‑tips

### Wat als ik geen GPU heb?

Stel `gpu_layers=0` in de `AsposeAIModelConfig`. Het model draait volledig op CPU, wat langzamer is maar nog steeds functioneel. Je kunt ook overschakelen naar een kleiner model (bijv. `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) om de inferentietijd redelijk te houden.

### Hoe wijzig ik later het model?

Werk simpelweg `hugging_face_repo_id` bij en voer `ocr_ai.initialize(model_config)` opnieuw uit. De SDK detecteert de versie‑wijziging, downloadt het nieuwe model en vervangt de gecachete bestanden.

### Kan ik de post‑processor prompt aanpassen?

Ja. Geef een dictionary door aan `custom_settings` met een `prompt_template`‑sleutel. Bijvoorbeeld:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Moet ik de opgeschoonde tekst opslaan in een bestand?

Zeker. Na het opschonen kun je het resultaat wegschrijven naar een `.txt`‑ of `.json`‑bestand voor downstream verwerking:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusie

We hebben je net laten zien hoe je **OCR uitvoert op afbeelding**‑bestanden met Aspose OCR Cloud, automatisch **een Hugging Face‑model downloadt**, vakkundig **LLM‑modelinstellingen configureert**, en uiteindelijk **OCR‑tekst opschoont** met een krachtige LLM‑post‑processor. Het hele proces past in één eenvoudig uit te voeren Python‑script en werkt zowel op GPU‑enabled als CPU‑only machines.

Als je vertrouwd bent met deze pipeline, overweeg dan te experimenteren met:

- **Verschillende LLM‑modellen** – probeer `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` voor een groter context‑venster.  
- **Batch‑verwerking** – loop over een map met afbeeldingen en verzamel opgeschoonde resultaten in een CSV.  
- **Aangepaste prompts** – stem de AI af op jouw domein (juridische documenten, medische notities, enz.).

Voel je vrij om de `gpu_layers`‑waarde aan te passen, het model te wisselen, of je eigen prompt te gebruiken. De mogelijkheden zijn eindeloos, en de code die je nu hebt is de lanceerbasis.

Veel plezier met coderen, en moge je OCR‑uitvoer altijd schoon zijn! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}