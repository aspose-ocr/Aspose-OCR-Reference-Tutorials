---
category: general
date: 2026-02-09
description: come eseguire OCR usando Aspose AI e un modello Hugging Face – impara
  a scaricare il modello Hugging Face, correggere gli errori OCR e liberare la memoria
  GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: it
og_description: Come eseguire l'OCR con Aspose AI è spiegato nel primo paragrafo –
  scopri come scaricare il modello Hugging Face, correggere gli errori OCR e liberare
  la memoria GPU.
og_title: come eseguire OCR con Aspose AI – Guida completa
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Come eseguire OCR con Aspose AI – Guida passo passo
url: /it/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

-page-section >}} etc.

We need to keep that.

Now produce final output with all translated content and original shortcodes.

Make sure to keep the same number of line breaks.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come eseguire OCR con Aspose AI – Guida completa

Ti sei mai chiesto **come eseguire OCR** su una fattura scansionata e ottenere numeri perfettamente puliti senza passare ore a correggere errori di battitura? Non sei solo. In molti progetti reali il testo grezzo che esce da un motore OCR classico contiene ancora caratteri erranti, simboli di valuta rotti o cifre confuse — soprattutto quando l'immagine di origine è rumorosa.  

La buona notizia è che puoi collegare un LLM ad Aspose OCR, scaricare un modello Hugging Face al volo e lasciare che l'AI perfezioni l'output per te. In questo tutorial percorreremo l'intera pipeline, dal prelevare il modello (sì, ti mostreremo come **download hugging face model** automaticamente) al liberare le risorse GPU quando hai finito. Alla fine avrai uno script riproducibile che **corrects OCR errors**, è veloce su una GPU modesta e si pulisce da solo così non sprechi memoria.

## Cosa imparerai

- Configura Aspose AI per recuperare un modello **Qwen2.5‑3B‑Instruct‑GGUF** da Hugging Face.
- Esegui il motore OCR standard di Aspose OCR su un file immagine.
- Usa un prompt LLM personalizzato che mantiene intatti numeri e simboli di valuta.
- Rilascia la memoria GPU con la routine integrata **free gpu memory**.
- Adatta il flusso di lavoro per casi limite come PDF multi‑pagina o GPU di fascia bassa.

> **Prerequisiti** – Python 3.9+, pacchetto `aspose-ocr`, accesso a Internet per il primo download del modello, e una GPU con almeno 4 GB VRAM (opzionale ma consigliato). Se non hai una GPU, lo script tornerà automaticamente alla CPU per gli strati rimanenti.

---

## Come eseguire OCR e migliorare i risultati

Di seguito trovi lo script Python completo, pronto per l'esecuzione. Salvalo come `ocr_with_ai.py` e sostituisci i percorsi segnaposto con i tuoi file.

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

> **Pro tip:** Il parametro `gpu_layers` ti permette di decidere quante layer del transformer restano sulla GPU. Se incontri errori di out‑of‑memory, riduci questo numero e il resto verrà eseguito sulla CPU – potrai comunque **free gpu memory** più tardi con `ai.free_resources()`.

### Output previsto

Eseguendo lo script su una fattura di esempio ottieni qualcosa di simile:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Nota come l'AI abbia corretto la “O” in `$1O0.00` in uno zero corretto mantenendo il simbolo del dollaro. Questa è l'essenza di **correct OCR errors** per documenti finanziari.

---

## Scarica modello Hugging Face – Cosa succede dietro le quinte?

Quando imposti `allow_auto_download="true"` il wrapper Aspose AI controlla `directory_model_path`. Se i file del modello non sono presenti, si collega a Hugging Face Hub, scarica la versione **int8‑quantized** di `Qwen2.5‑3B‑Instruct‑GGUF` e la salva localmente. Questo download una tantum è tipicamente inferiore a 2 GB, rendendolo fattibile anche su SSD modesti.

> **Perché int8?** La quantizzazione a 8‑bit riduce drasticamente l'uso di memoria — cruciale quando vuoi anche **free gpu memory** dopo l'elaborazione. Il compromesso è una piccola perdita di accuratezza, ma per il post‑processing del testo OCR l'impatto è trascurabile.

Se preferisci ospitare il modello tu stesso, basta inserire i file `.gguf` in `YOUR_DIRECTORY/Models` e Aspose li rileverà senza dover accedere di nuovo a Internet.

---

## Come liberare la GPU – Best Practices

Le risorse GPU sono una merce condivisa su molte workstation. Lasciare tensori vivi dopo che lo script termina può causare errori “CUDA out of memory” per i lavori successivi. La chiamata `ai.free_resources()` fa tre cose:

1. **Disposes the underlying transformer** – tutti i pesi residenti sulla GPU vengono rilasciati.
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` viene invocato internamente.
3. **Deletes temporary files** – tutte le cache su disco create durante il download vengono rimosse.

Puoi anche invocare manualmente `torch.cuda.empty_cache()` se stai mescolando Aspose AI con altri carichi di lavoro PyTorch, ma il metodo integrato è solitamente sufficiente.

---

## Guida passo‑passo (H2 con parole chiave secondarie)

### Download Hugging Face Model Automatically

Il costruttore `AsposeAIModelConfig` nasconde la complessità di interagire con l'API Hugging Face. Assicurati solo di avere accesso a Internet la prima volta che esegui lo script. Dopo di che, il modello risiede in `YOUR_DIRECTORY/Models`, e le esecuzioni successive partono istantaneamente.

### Free GPU Memory After Inference

Se esegui questo all'interno di un servizio a lungo termine (ad esempio un'API Flask), chiama `ai.free_resources()` dopo ogni richiesta. Questo previene perdite di memoria e garantisce che la prossima richiesta possa riutilizzare la stessa GPU senza intoppi.

### Correct OCR Errors with a Custom Prompt

La nostra funzione `financial_prompt` restituisce un dizionario con una singola chiave `prompt`. Puoi adattarla a qualsiasi dominio:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Cambia il nome della funzione in `ai.set_post_processor(...)` e avrai una pipeline **correct OCR errors** per cartelle cliniche.

### How to Run OCR on Multi‑Page PDFs

Aspose OCR può gestire i PDF direttamente:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Dopo aver ottenuto la stringa grezza, lo stesso post‑processor LLM pulirà il testo di ogni pagina. Nessun codice aggiuntivo necessario.

### When You Don’t Have a GPU – How to Free GPU (Even Without One)

Anche su macchine solo CPU, chiamare `ai.free_resources()` non causa problemi. Semplicemente pulisce le cache interne, liberando RAM. Quindi il consiglio **how to free gpu** è valido universalmente: pulisci sempre dopo aver finito.

---

## Common Pitfalls & How We Solved Them

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Out‑of‑Memory on GPU** | `gpu_layers` impostato troppo alto per la tua scheda | Riduci `gpu_layers` a 10 o 5, lascia che il resto venga eseguito sulla CPU |
| **Model never downloads** | Il firewall aziendale blocca HTTPS verso huggingface.co | Scarica il modello manualmente su una rete diversa, poi punta `directory_model_path` alla cartella locale |
| **Numbers get corrupted** | Prompt non sufficientemente esplicito sul mantenere le cifre | Aggiungi “preserve all numeric values and currency symbols exactly as they appear” al prompt |
| **`free_resources` raises an exception** | Uso di una versione più vecchia di Aspose OCR | Aggiorna al pacchetto più recente `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## Full Example Recap

Ecco di nuovo lo script, questa volta con commenti in linea che spiegano ogni riga per riferimento futuro:

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

## Conclusione

Abbiamo coperto **how to run OCR** con Aspose, scaricato un modello Hugging Face su richiesta, creato un prompt che **corrects OCR errors**, e infine **free gpu memory** così la tua workstation rimane reattiva. L'intero flusso di lavoro sta in un unico file Python auto‑contenuto — nessuno script esterno, nessuna gestione manuale del modello e nessuna allocazione GPU persistente.

Passi successivi? Prova a sostituire `financial_prompt` con un

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}