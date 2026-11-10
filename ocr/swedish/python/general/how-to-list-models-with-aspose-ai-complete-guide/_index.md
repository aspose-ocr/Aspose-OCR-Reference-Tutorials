---
category: general
date: 2026-07-05
description: Hur man listar modeller med Aspose AI, aktiverar automatisk nedladdning
  och laddar ner Hugging Face‑modell i Python. Följ den här steg‑för‑steg‑handledningen
  för att konfigurera cache och börja använda Aspose AI idag.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: sv
og_description: Hur man listar modeller med Aspose AI, aktiverar automatisk nedladdning
  och laddar ner en Hugging Face-modell. Lär dig att ställa in cache och använda Aspose
  AI på några minuter.
og_title: Hur man listar modeller med Aspose AI – Fullständig handledning
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
title: Hur man listar modeller med Aspose AI – Komplett guide
url: /sv/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man listar modeller med Aspose AI – Komplett guide

Att lista modeller med Aspose AI är en fråga som dyker upp så snart du börjar experimentera med stora språkmodeller i Python. I den här handledningen går vi igenom hur du aktiverar **auto download**, konfigurerar en lokal cache och hämtar en modell direkt från Hugging Face—så att du kan komma igång utan att manuellt leta efter filer.

Om du någonsin har undrat *“hur använder jag Aspose för OCR‑driven AI?”* eller *“vad är det enklaste sättet att ställa in cache för modellfiler?”* så är du på rätt plats. I slutet kommer du att ha ett fullt fungerande skript som listar varje modell som lagras lokalt, automatiskt laddar ner saknade och visar exakt var filerna finns på disken.

---

## Vad du behöver

- Python 3.9 eller nyare (biblioteket använder typindikatorer som kräver en nyare interpreter)
- `pip`‑åtkomst för att installera **Aspose OCR**‑paketet (`aocr`).  
  ```bash
  pip install aocr
  ```
- En internetanslutning för den första nedladdningen från Hugging Face.
- En mapp där du vill lagra modellcachen (t.ex. `./model_cache`).

Det är allt—inga extra Docker‑behållare, inga tunga virtuella miljöer utöver en ren Python‑installation.

---

## ## Hur man listar modeller med Aspose AI

Kärnan i den här guiden är förmågan att **lista modeller** som Aspose AI har cachat lokalt. När cachen är konfigurerad kan biblioteket enumerera allt det vet om, vilket gör felsökning och versionshantering enkelt.

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

**Why this works:**  
- `AsposeAI()` skapar hög‑nivå‑ingångspunkten som kommunicerar med den underliggande inferensmotorn.  
- `AsposeAIModelConfig()` innehåller alla inställningar du kan justera; att sätta `allow_auto_download` till `"true"` talar om för biblioteket att automatiskt hämta saknade filer från det repository du anger.  
- `directory_model_path` är *cache‑katalogen*—platsen där alla nedladdade binärer lagras.  
- `initialize()` tillämpar konfigurationen och utför den första nedladdningen om cachen är tom.  
- Slutligen skannar `list_local()` cache‑mappen och returnerar en Python‑lista med modellidentifierare, som vi skriver ut.

### Förväntad output (första körning)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Om du kör skriptet igen kommer biblioteket att hoppa över nedladdningen och bara lista den redan närvarande modellen, vilket visar att **hur man ställer in cache** verkligen lönar sig för efterföljande körningar.

---

## ## Aktivera auto download för saknade modeller

Ofta kommer du att arbeta med flera modeller över projekt. Att manuellt hämta varje modell från Hugging Face kan vara tidskrävande. Genom att aktivera auto download tar Aspose AI hand om det tunga arbetet.

```python
cfg.allow_auto_download = "true"
```

> **Proffstips:** Håll `allow_auto_download` satt till `"true"` **endast** i utvecklings‑ eller CI‑miljöer. I produktion kan du vilja låsa cachen för att undvika oväntad nätverkstrafik.

Om du senare bestämmer dig för att stänga av den, sätt bara flaggan till `"false"` innan du anropar `initialize()` igen.

---

## ## Ladda ner Hugging Face-modell i farten

Raden

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

anger för Aspose AI vilket fjärr‑repository som ska hämtas från. Biblioteket stödjer alla offentliga modeller på Hugging Face som tillhandahåller en GGUF‑fil. Vill du ha en annan modell? Byt ut repo‑ID:n:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

När du kör skriptet kontrollerar Aspose AI cachen:

- **Om modellen finns**, laddas den omedelbart.  
- **Om den inte finns**, triggar auto‑download‑flaggan en nedladdning, lagrar filen under `directory_model_path` och registrerar den för omedelbar användning.

Detta tillvägagångssätt eliminerar den tvåstegsprocess “ladda ner‑sen‑kör” som många handledningar tvingar dig att följa.

---

## ## Så använder du Aspose AI efter att modellen har listats

Att lista modeller är bara halva historien. När du vet att en modell finns kan du börja inferens:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Varför detta är viktigt:**  
- `run_inference()` abstraherar bort tokenisering, batchning och GPU‑hantering.  
- Genom att skicka *modellnamnet* du fick från `list_local()` säkerställer du att inferensanropet matchar den exakta filen på disken.

---

## ## Hur man ställer in cache‑plats för flera projekt

Om du jonglerar flera projekt kan du vilja att varje får sin egen cache‑mapp. Fältet `directory_model_path` är bara en vanlig sträng, så du kan bygga den dynamiskt:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Nu får varje projekt en isolerad undermapp (`./model_cache/sentiment_analysis`), vilket förhindrar versionskonflikter och gör städning enkel.

---

## ## Vanliga fallgropar och hur man undviker dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| **`PermissionError` när du får åtkomst till cache** | Cache‑mappen ägs av en annan användare (vanligt på delade servrar) | Skapa mappen manuellt med rätt behörigheter: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Modellen visas aldrig i `list_local()`** | `allow_auto_download` är satt till `"false"` och modellen är ännu inte cachad | Sätt flaggan på tillfälligt, kör en gång, och stäng av den igen om så önskas |
| **Oväntad modellversion** | Två olika repository delar samma namn men olika filer | Fäst exakt repo‑ID (inklusive tag/commit) eller lås cachen genom att inaktivera auto‑download efter första lyckade hämtning |
| **Out‑of‑memory‑fel** | Stora GGUF‑filer på en maskin utan tillräckligt RAM/VRAM | Använd en mindre modell (t.ex. `Qwen2.5-1.5B`) eller sätt `cfg.device = "cpu"` för att tvinga CPU‑inferens |

---

## ## Fullt skript du kan kopiera‑klistra in

Nedan är det kompletta, färdiga att köra‑exemplet som inkluderar alla koncept ovan. Spara det som `list_models_demo.py` och kör med `python list_models_demo.py`.

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

**Att köra det** kommer att producera output liknande det tidigare exemplet, följt av ett koncist svar från modellen. Känn dig fri att ersätta prompten med vad du vill—detta är det snabbaste sättet att testa att modellen verkligen är användbar efter att du har **listat modeller**.

---

## ## Sammanfattning

Vi har gått igenom allt du behöver för att **lista modeller** med Aspose AI, från att aktivera **auto download** till att konfigurera en beständig **cache** och hämta en **Hugging Face-modell** på begäran. De viktigaste punkterna:

1. Skapa ett `AsposeAI`‑objekt och en `AsposeAIModelConfig`.  
2. Sätt `allow_auto_download = "true"` och peka `directory_model_path` till en mapp du kontrollerar.  
3. Initiera AI:n, anropa sedan `list_local()` för att se exakt vad som är cachat.  
4. Använd det listade modellnamnet för inferens, så är du redo att bygga verkliga applikationer.

---

## Vad blir nästa?

- **Experimentera med olika modeller** – byt ut `cfg.hugging_face_repo_id` mot ett annat repository och se hur listan förändras.  
- **Finjustera cache**

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man batchar OCR‑bilder med lista i Aspose.OCR för .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Hur man ställer in Aspose OCR‑licens och verifierar den i Java](/ocr/english/java/ocr-basics/set-license/)
- [Hur man extraherar text från bild med Aspose.OCR för .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}