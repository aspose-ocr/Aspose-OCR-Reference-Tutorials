---
category: general
date: 2026-02-09
description: hur man kör OCR med Aspose AI och en Hugging Face-modell – lär dig att
  ladda ner Hugging Face-modellen, korrigera OCR-fel och frigöra GPU-minne.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: sv
og_description: Hur man kör OCR med Aspose AI förklaras i första stycket – upptäck
  hur du laddar ner Hugging Face-modellen, korrigerar OCR-fel och frigör GPU-minne.
og_title: Hur man kör OCR med Aspose AI – komplett guide
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: hur man kör OCR med Aspose AI – steg‑för‑steg‑guide
url: /sv/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man kör OCR med Aspose AI – Komplett guide

Har du någonsin undrat **hur man kör OCR** på en skannad faktura och får perfekt rena siffror utan att spendera timmar på att rätta stavfel? Du är inte ensam. I många verkliga projekt innehåller den råa texten som kommer ut från en klassisk OCR-motor fortfarande lösa tecken, trasiga valutasymboler eller förvrängda siffror—särskilt när källbilden är brusig.  

Den goda nyheten är att du kan koppla en LLM till Aspose OCR, ladda ner en Hugging Face-modell i farten, och låta AI:n polera resultatet åt dig. I den här handledningen går vi igenom hela pipeline:n, från att hämta modellen (ja, vi visar dig hur du **download hugging face model** automatiskt) till att frigöra GPU-resurser när du är klar. I slutet har du ett reproducerbart skript som **corrects OCR errors**, kör snabbt på ett modest GPU, och städar upp efter sig så du inte slösar minne.

## Vad du kommer att lära dig

- Konfigurera Aspose AI för att hämta en **Qwen2.5‑3B‑Instruct‑GGUF**-modell från Hugging Face.
- Kör den standard Aspose OCR-motorn på en bildfil.
- Använd en anpassad LLM-prompt som behåller siffror och valutasymboler intakta.
- Frigör GPU-minne med den inbyggda **free gpu memory**-rutinen.
- Finjustera arbetsflödet för kantfall som flersidiga PDF:er eller lågpresterande GPU:er.

> **Förutsättningar** – Python 3.9+, `aspose-ocr`-paket, internetåtkomst för den första modellnedladdningen, och ett GPU med minst 4 GB VRAM (valfritt men rekommenderat). Om du inte har ett GPU, kommer skriptet automatiskt att falla tillbaka till CPU för de återstående lagren.

---

## Hur man kör OCR och förbättrar resultat

Nedan är det kompletta, färdiga Python‑skriptet. Spara det som `ocr_with_ai.py` och ersätt platshållar‑sökvägarna med dina egna filer.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Parametern `gpu_layers` låter dig bestämma hur många transformer‑lager som stannar på GPU:n. Om du får minnesbrist‑fel, sänk detta tal och resten körs på CPU – du kommer fortfarande att **free gpu memory** senare med `ai.free_resources()`.

### Förväntat resultat

Att köra skriptet på en exempel­faktura ger något i stil med:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Observera hur AI:n korrigerade “O” i `$1O0.00` till en riktig nolla samtidigt som dollartecknet bevarades. Det är kärnan i **correct OCR errors** för finansiella dokument.

---

## Ladda ner Hugging Face-modell – Vad som händer under huven?

När du sätter `allow_auto_download="true"` kontrollerar Aspose AI‑omslaget `directory_model_path`. Om modellfilerna inte finns där, kontaktar det Hugging Face Hub, hämtar den **int8‑quantized** versionen av `Qwen2.5‑3B‑Instruct‑GGUF`, och lagrar den lokalt. Denna engångsnedladdning är vanligtvis under 2 GB, vilket gör den genomförbar även på modest SSD.

> **Varför int8?** Kvantisering till 8‑bit minskar minnesanvändningen dramatiskt—viktigt när du också vill **free gpu memory** efter bearbetning. Kompromissen är en liten förlust i noggrannhet, men för efterbearbetning av OCR‑text är påverkan försumbar.

Om du föredrar att hosta modellen själv, släpp helt enkelt `.gguf`-filerna i `YOUR_DIRECTORY/Models` så plockar Aspose upp dem utan att behöva nå internet igen.

---

## Hur man frigör GPU – Bästa praxis

GPU-resurser är en delad vara på många arbetsstationer. Att låta tensorer leva kvar efter att ditt skript avslutas kan orsaka “CUDA out of memory”-fel för efterföljande jobb. Anropet `ai.free_resources()` gör tre saker:

1. **Disposerar den underliggande transformern** – alla GPU‑residenta vikter frigörs.
2. **Rensar PyTorch‑cachen** – `torch.cuda.empty_cache()` anropas internt.
3. **Tar bort temporära filer** – alla cache‑filer på disk som skapats under nedladdningen tas bort.

Du kan också manuellt anropa `torch.cuda.empty_cache()` om du blandar Aspose AI med andra PyTorch‑arbetsbelastningar, men den inbyggda metoden är vanligtvis tillräcklig.

---

## Steg‑för‑steg genomgång (H2s med sekundära nyckelord)

### Ladda ner Hugging Face-modell automatiskt

`AsposeAIModelConfig`‑konstruktorn döljer komplexiteten i att hantera Hugging Face‑API:n. Se bara till att du har internetåtkomst första gången du kör skriptet. Därefter ligger modellen i `YOUR_DIRECTORY/Models`, och efterföljande körningar startar omedelbart.

### Frigör GPU‑minne efter inferens

Om du kör detta i en långlivad tjänst (t.ex. ett Flask‑API), anropa `ai.free_resources()` efter varje förfrågan. Detta förhindrar minnesläckor och säkerställer att nästa förfrågan kan återanvända samma GPU utan problem.

### Korrigera OCR‑fel med en anpassad prompt

Vår `financial_prompt`‑funktion returnerar en dictionary med en enda nyckel `prompt`. Du kan skräddarsy detta för vilken domän som helst:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Byt ut funktionsnamnet i `ai.set_post_processor(...)` så har du en **correct OCR errors**‑pipeline för medicinska journaler.

### Hur man kör OCR på flersidiga PDF:er

Aspose OCR kan hantera PDF:er direkt:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

När du har fått den råa strängen kommer samma LLM‑post‑processor att rensa varje sidas text. Ingen extra kod behövs.

### När du inte har ett GPU – Hur man frigör GPU (även utan ett)

Även på enbart CPU‑maskiner är anropet `ai.free_resources()` ofarligt. Det rensar helt enkelt interna cachar, vilket fortfarande kan frigöra RAM. Så rådet **how to free gpu** gäller universellt: rensa alltid upp efter dig själv.

---

## Vanliga fallgropar & hur vi löste dem

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory på GPU** | `gpu_layers` är satt för högt för ditt kort | Minska `gpu_layers` till 10 eller 5, låt resten köra på CPU |
| **Modellen laddas aldrig ner** | Företagsbrandväggen blockerar HTTPS till huggingface.co | Ladda ner modellen manuellt på ett annat nätverk, och peka `directory_model_path` till den lokala mappen |
| **Siffror blir korrupta** | Prompten är inte tillräckligt tydlig om att behålla siffror | Lägg till “preserve all numeric values and currency symbols exactly as they appear” i prompten |
| **`free_resources` kastar ett undantag** | Använder en äldre version av Aspose OCR | Uppgradera till den senaste `aspose-ocr`-paketet (pip install --upgrade aspose-ocr) |

---

## Fullt exempel – Sammanfattning

Här är skriptet igen, den här gången med inline‑kommentarer som förklarar varje rad för framtida referens:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Slutsats

Vi har gått igenom **how to run OCR** med Aspose, laddat ner en Hugging Face-modell på begäran, skapat en prompt som **corrects OCR errors**, och slutligen **free gpu memory** så att din arbetsstation förblir responsiv. Hela arbetsflödet får plats i en enda, självständig Python‑fil—inga externa skript, ingen manuell modellhantering och inga kvarvarande GPU‑allokeringar.

Nästa steg? Prova att byta ut `financial_prompt` mot en

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}