---
category: general
date: 2026-07-05
description: Hoe je modellen kunt weergeven met Aspose AI, automatisch downloaden
  inschakelt en een Hugging Face‑model downloadt in Python. Volg deze stapsgewijze
  tutorial om de cache in te stellen en vandaag nog met Aspose AI aan de slag te gaan.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: nl
og_description: Hoe modellen te lijsten met Aspose AI, automatische download in te
  schakelen en een Hugging Face‑model te downloaden. Leer cache in te stellen en Aspose
  AI in enkele minuten te gebruiken.
og_title: Hoe modellen te vermelden met Aspose AI – Volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Hoe modellen te vermelden met Aspose AI – Volledige gids
url: /nl/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe modellen te vermelden met Aspose AI – Complete gids

Hoe modellen te vermelden met Aspose AI is een vraag die opkomt zodra je begint te experimenteren met grote taalmodellen in Python. In deze tutorial lopen we door het inschakelen van **auto download**, het configureren van een lokale cache, en het ophalen van een model rechtstreeks van Hugging Face—zodat je meteen aan de slag kunt zonder handmatig naar bestanden te zoeken.

Als je je ooit afvroeg *“hoe gebruik ik Aspose voor OCR‑gedreven AI?”* of *“wat is de gemakkelijkste manier om een cache voor modelbestanden in te stellen?”* dan ben je op de juiste plek. Aan het einde heb je een volledig functioneel script dat elk lokaal opgeslagen model opsomt, automatisch ontbrekende downloadt, en je precies laat zien waar de bestanden op schijf staan.

---

## Wat je nodig hebt

- Python 3.9 of nieuwer (de bibliotheek gebruikt type hints die een recente interpreter vereisen)
- `pip`-toegang om het **Aspose OCR**-pakket (`aocr`) te installeren.  
  ```bash
  pip install aocr
  ```
- Een internetverbinding voor de eerste download van Hugging Face.
- Een map waarin je de modelcache wilt bewaren (bijv. `./model_cache`).

Dat is alles—geen extra Docker-containers, geen zware virtuele omgevingen buiten een schone Python-installatie.

---

## ## Hoe modellen te vermelden met Aspose AI

Het hart van deze gids is het vermogen om **modellen te vermelden** die Aspose AI lokaal heeft gecached. Zodra de cache is ingesteld, kan de bibliotheek alles opsommen waar het van weet, waardoor debugging en versiebeheer een fluitje van een cent worden.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Waarom dit werkt:**  
- `AsposeAI()` creëert het high‑level toegangspunt dat communiceert met de onderliggende inference‑engine.  
- `AsposeAIModelConfig()` bevat alle instellingen die je kunt aanpassen; het instellen van `allow_auto_download` op `"true"` vertelt de bibliotheek om ontbrekende bestanden automatisch op te halen uit de opgegeven repository.  
- `directory_model_path` is de *cache‑directory*—de plek waar alle gedownloade binaries zich bevinden.  
- `initialize()` past de configuratie toe en voert de eerste download uit als de cache leeg is.  
- Ten slotte scant `list_local()` de cache‑map en retourneert een Python‑list met model‑identifiers, die we afdrukken.

### Verwachte output (eerste uitvoering)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Als je het script opnieuw uitvoert, zal de bibliotheek de download overslaan en simpelweg het reeds aanwezige model opsommen, wat bewijst dat **how to set cache** echt loont voor volgende runs.

---

## ## Auto‑download inschakelen voor ontbrekende modellen

Vaak werk je met meerdere modellen over verschillende projecten. Elk model handmatig van Hugging Face ophalen kan tijdrovend zijn. Door auto‑download in te schakelen, neemt Aspose AI het zware werk uit handen.

```python
cfg.allow_auto_download = "true"
```

> **Pro tip:** Houd `allow_auto_download` ingesteld op `"true"` **alleen** in ontwikkelings- of CI‑omgevingen. In productie wil je de cache wellicht vergrendelen om onverwacht netwerkverkeer te vermijden.

Als je later besluit het uit te schakelen, stel dan de vlag in op `"false"` voordat je opnieuw `initialize()` aanroept.

---

## ## Hugging Face‑model on‑the‑fly downloaden

De regel

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

vertelt Aspose AI van welke externe repository gedownload moet worden. De bibliotheek ondersteunt elk openbaar model op Hugging Face dat een GGUF‑bestand levert. Wil je een ander model? Vervang de repo‑ID:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Wanneer je het script uitvoert, controleert Aspose AI de cache:

- **Als het model bestaat**, laadt het het onmiddellijk.  
- **Als het niet bestaat**, activeert de auto‑download‑vlag een download, slaat het bestand op onder `directory_model_path`, en registreert het vervolgens voor direct gebruik.

Deze aanpak elimineert het “download‑dan‑run” twee‑stappenproces dat veel tutorials je laten volgen.

---

## ## Aspose AI gebruiken nadat het model is opgesomd

Modellen opsommen is slechts de helft van het verhaal. Zodra je weet dat een model aanwezig is, kun je beginnen met inferentie:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Waarom dit belangrijk is:**  
- `run_inference()` abstraheert tokenisatie, batchverwerking en GPU‑afhandeling.  
- Door de *modelnaam* door te geven die je van `list_local()` hebt verkregen, garandeer je dat de inferentie‑aanroep overeenkomt met het exacte bestand op schijf.

---

## ## Cache‑locatie instellen voor meerdere projecten

Als je met meerdere projecten werkt, wil je misschien dat elk zijn eigen cache‑map heeft. Het veld `directory_model_path` is gewoon een string, dus je kunt het dynamisch opbouwen:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Nu krijgt elk project een geïsoleerde sub‑map (`./model_cache/sentiment_analysis`), waardoor versieconflicten worden voorkomen en opruimen eenvoudig is.

---

## ## Veelvoorkomende valkuilen en hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|---------|--------------------------|----------|
| **`PermissionError` when accessing cache** | Cache‑map eigendom van een andere gebruiker (veelvoorkomend op gedeelde servers) | Maak de map handmatig aan met de juiste rechten: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` ingesteld op `"false"` en het model nog niet in de cache staat | Zet de vlag tijdelijk aan, voer één keer uit, schakel daarna uit indien gewenst |
| **Unexpected model version** | Twee verschillende repositories delen dezelfde naam maar verschillende bestanden | Pin de exacte repo‑ID (inclusief tag/commit) of vergrendel de cache door auto‑download uit te schakelen na de eerste succesvolle pull |
| **Out‑of‑memory errors** | Grote GGUF‑bestanden op een machine zonder voldoende RAM/VRAM | Gebruik een kleiner model (bijv. `Qwen2.5-1.5B`) of stel `cfg.device = "cpu"` in om CPU‑inference af te dwingen |

---

## ## Volledig script dat je kunt kopiëren‑plakken

Hieronder staat het volledige, kant‑klaar voorbeeld dat alle bovenstaande concepten bevat. Sla het op als `list_models_demo.py` en voer uit met `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Running it** zal output produceren die lijkt op het eerdere voorbeeld, gevolgd door een beknopt antwoord van het model. Voel je vrij om de prompt te vervangen door iets wat je wilt—dit is de snelste manier om te testen dat het model echt bruikbaar is nadat je **how to list models** hebt.

---

## ## Samenvatting

We hebben alles behandeld wat je nodig hebt om **how to list models** te gebruiken met Aspose AI, van het inschakelen van **auto download** tot het configureren van een persistente **cache** en het on‑the‑fly ophalen van een **Hugging Face model**. De belangrijkste punten:

1. Maak een `AsposeAI`‑object en een `AsposeAIModelConfig`.  
2. Stel `allow_auto_download = "true"` in en wijs `directory_model_path` naar een map die jij beheert.  
3. Initialise de AI, roep vervolgens `list_local()` aan om precies te zien wat er gecached is.  
4. Gebruik de opgesomde modelnaam voor inferentie, en je bent klaar om real‑world toepassingen te bouwen.

---

## Wat is het vervolg?

- **Experiment met verschillende modellen** – vervang `cfg.hugging_face_repo_id` door een andere repo en zie hoe de lijst verandert.  
- **Fine‑tune cache

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}