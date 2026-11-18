---
category: general
date: 2026-06-19
description: Leer hoe je OCR op een afbeelding uitvoert met Aspose OCR en AI‑postprocessor
  in Python. Inclusief automatisch gedownload model, spellingscontrole en GPU‑versnelling.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: nl
og_description: Voer OCR uit op een afbeelding met Aspose OCR en AI-nabewerking. Stapsgewijze
  handleiding met automatisch gedownload model, spellingscontrole en GPU-versnelling.
og_title: Voer OCR uit op afbeelding – Complete Python Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: OCR uitvoeren op afbeelding met Aspose AI – Volledige Python‑gids
url: /nl/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# voer OCR uit op afbeelding – Complete Python Tutorial

Heb je je ooit afgevraagd hoe je **OCR op afbeelding**‑bestanden kunt uitvoeren zonder te worstelen met tientallen bibliotheken? Naar mijn ervaring ligt de pijnpunt meestal in het jongleren met een ruwe OCR‑engine, en vervolgens proberen de ruisige output op te schonen. Gelukkig maakt Aspose OCR voor Python, gecombineerd met zijn AI‑post‑processor, de hele pijplijn een fluitje van een cent.

In deze gids lopen we een praktisch, end‑to‑end voorbeeld door dat precies laat zien hoe je **OCR op afbeelding**‑gegevens kunt uitvoeren, de nauwkeurigheid kunt verhogen met een automatisch gedownload model, spellcheck kunt inschakelen, en zelfs GPU‑versnelling kunt benutten wanneer die beschikbaar is. Tegen de tijd dat je klaar bent, heb je een herbruikbaar script dat je in elk facturatie‑, bon‑scan‑ of document‑digitaliseringsproject kunt plaatsen.

## Wat je gaat bouwen

We maken een klein Python‑programma dat:

1. De Aspose OCR‑engine initialiseert en een voorbeeld‑factuurafbeelding laadt.  
2. Een basis‑OCR‑run uitvoert en de ruwe tekst afdrukt.  
3. **Aspose AI** configureert met een **automatisch gedownload model** van Hugging Face.  
4. De **AI‑post‑processor** (inclusief een **spellcheck‑post‑processor**) uitvoert om de OCR‑output op te schonen.  
5. Alle bronnen netjes vrijgeeft.

Geen externe services, geen API‑sleutels—slechts een paar regels Python en de kracht van Aspose.

> **Pro tip:** Als je op een machine met een degelijke GPU werkt, kan het instellen van `gpu_layers` seconden schelen bij de post‑processing stap.

## Vereisten

- Python 3.8 of nieuwer (de code gebruikt type‑hints, maar die zijn optioneel).  
- `aspose-ocr` en `aspose-ai` pakketten geïnstalleerd via `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Een voorbeeldafbeelding (PNG, JPG of TIFF) ergens geplaatst die je kunt refereren, bv. `sample_invoice.png`.  
- (Optioneel) Een CUDA‑enabled GPU en de juiste drivers als je **GPU‑versnelling** wilt.

Nu de basis is gelegd, duiken we in de code.

![voer OCR uit op afbeelding voorbeeld](image.png)

## voer OCR uit op afbeelding – Stap 1: Initialiseert de OCR‑engine en laadt de afbeelding

Het eerste wat we nodig hebben is een OCR‑engine‑instantie. Aspose OCR biedt een nette, object‑georiënteerde API die de low‑level beeld‑preprocessing abstraheert.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Waarom dit belangrijk is:**  
Het vroeg instellen van de taal vertelt de engine welke tekenset verwacht wordt, wat de herkenningssnelheid en nauwkeurigheid kan verbeteren. Als je met meertalige documenten werkt, wijzig dan simpelweg `"en"` naar `"fr"` of `"de"` naar behoefte.

## Stap 2: Voer basis‑OCR uit en bekijk de ruwe tekst

Nu voeren we de herkenning daadwerkelijk uit. Het resultaatobject bevat de ruwe tekst, confidence‑scores, en zelfs bounding boxes als je die later nodig hebt.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Typische output kan er zo uitzien (let op de af en toe fout gelezen tekens):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Je ziet de nullen (`0`) waar de engine een “O” dacht te zien. Daar komt de **AI‑post‑processor** goed van pas.

## Configureer Aspose AI – automatisch gedownload model en spellcheck

Voordat we het ruwe OCR‑resultaat aan de AI‑laag geven, moeten we Aspose AI vertellen welk model te gebruiken. De bibliotheek kan automatisch een model van Hugging Face downloaden, zodat je niet zelf met grote `.bin`‑bestanden hoeft te jongleren.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Uitleg van de instellingen**

| Instelling | Wat het doet | Wanneer aan te passen |
|------------|--------------|-----------------------|
| `allow_auto_download` | Laat Aspose het model automatisch ophalen bij de eerste uitvoering. | Houd `true` tenzij je vooraf downloadt voor offline gebruik. |
| `hugging_face_repo_id` | Identifier van het model op Hugging Face. | Vervang door een ander model als je een domeinspecifiek model nodig hebt. |
| `hugging_face_quantization` | Kies het quantisatieniveau (`int8`, `float16`, etc.). | Gebruik `int8` voor omgevingen met weinig geheugen; `float16` voor hogere nauwkeurigheid. |
| `gpu_layers` | Aantal transformer‑lagen uitgevoerd op de GPU. | Zet op `0` voor CPU‑only, of een waarde tot het totale aantal lagen van het model (20 voor Qwen2.5‑3B). |

## Voer de AI‑post‑processor uit op het OCR‑resultaat

Met de engine klaar, voeren we simpelweg de ruwe OCR‑output in de AI‑pipeline. De ingebouwde **spellcheck‑post‑processor** corrigeert duidelijke typefouten, terwijl het taalmodel kan herformuleren of ontbrekende informatie kan aanvullen als je later extra processors inschakelt.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Verwachte output na de spellcheck‑stap:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Merk op hoe de nullen zijn gecorrigeerd naar juiste letters, en de verkeerd gespelde “Am0unt” is omgezet naar “Amount”. De **AI‑post‑processor** werkt door de ruwe tekst door het geselecteerde model te sturen, dat vervolgens een verfijnde versie teruggeeft op basis van zijn training.

### Randgevallen & Tips

- **Laag‑resolutie afbeeldingen**: Als de OCR‑engine moeite heeft, overweeg dan de afbeelding eerst up‑scalen (`Pillow` kan helpen) of verhoog `ocr_engine.ImagePreprocessingOptions`.  
- **Niet‑Latijnse scripts**: Wijzig `ocr_engine.Language` naar de juiste ISO‑code (`"zh"` voor Chinees, `"ar"` voor Arabisch).  
- **GPU niet gedetecteerd**: De `gpu_layers`‑instelling valt stilletjes terug op CPU als er geen compatibele GPU wordt gevonden, dus extra foutafhandeling is niet nodig.  
- **Model‑grootte limieten**: Het Qwen2.5‑3B model is ~4 GB gecomprimeerd; zorg dat je schijf genoeg ruimte heeft voor de automatische download.

## Vrijgeven van bronnen – nette afsluiting

Aspose‑objecten houden native handles, dus het is goed om ze vrij te geven wanneer je klaar bent. Dit voorkomt geheugenlekken, vooral in langdurige services.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Je kunt het hele script in een `try…finally`‑blok plaatsen als je expliciete opruiming verkiest.

## Volledig script – klaar om te kopiëren en plakken

Hieronder staat het volledige programma, klaar om te draaien nadat je `YOUR_DIRECTORY` vervangt door het pad naar je afbeelding.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Voer het uit met:

```bash
python perform_ocr_on_image.py
```

Je zou de ruwe en opgeschoonde outputs in de console moeten zien.

## Conclusie


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}