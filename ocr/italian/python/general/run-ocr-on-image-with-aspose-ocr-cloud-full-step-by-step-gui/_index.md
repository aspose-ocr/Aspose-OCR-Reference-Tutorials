---
category: general
date: 2026-03-28
description: Impara come eseguire l'OCR su un'immagine, scaricare automaticamente
  il modello Hugging Face, pulire il testo OCR e configurare il modello LLM in Python
  usando Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: it
og_description: Esegui OCR sull'immagine e pulisci l'output usando un modello Hugging Face
  scaricato automaticamente. Questa guida mostra come configurare il modello LLM in
  Python.
og_title: Esegui OCR su un'immagine – Tutorial completo di Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Esegui OCR su immagine con Aspose OCR Cloud – Guida completa passo‑passo
url: /it/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Tutorial Completo di Aspose OCR Cloud

Hai mai dovuto eseguire OCR su file immagine ma l'output grezzo sembrava un pasticcio? Nella mia esperienza il punto dolente più grande non è il riconoscimento in sé, ma la pulizia. Fortunatamente, Aspose OCR Cloud ti permette di collegare un post‑processore LLM che può *pulire il testo OCR* automaticamente. In questo tutorial vedremo tutto ciò di cui hai bisogno: dal **download di un modello Hugging Face** alla configurazione dell'LLM, all'esecuzione del motore OCR e, infine, alla rifinitura del risultato.

Al termine di questa guida avrai uno script pronto all'uso che:

1. Scarica un modello compatto Qwen 2.5 da Hugging Face (auto‑downloadato per te).  
2. Configura il modello per eseguire parte della rete su GPU e il resto su CPU.  
3. Esegue il motore OCR su un'immagine di una nota scritta a mano.  
4. Usa l'LLM per pulire il testo riconosciuto, fornendoti un output leggibile.

> **Prerequisiti** – Python 3.8+, pacchetto `asposeocrcloud`, una GPU con almeno 4 GB di VRAM (opzionale ma consigliata) e una connessione internet per il primo download del modello.

---

## Cosa Ti Serve

- **Aspose OCR Cloud SDK** – installalo con `pip install asposeocrcloud`.  
- **Un'immagine di esempio** – ad es. `handwritten_note.jpg` posizionata in una cartella locale.  
- **Supporto GPU** – se disponi di una GPU abilitata CUDA, lo script scaricherà 30 layer; altrimenti tornerà automaticamente alla CPU.  
- **Permessi di scrittura** – lo script memorizza nella cache il modello in `YOUR_DIRECTORY`; assicurati che la cartella esista.

---

## Passo 1 – Configura il Modello LLM (download modello Hugging Face)

La prima cosa che facciamo è dire ad Aspose AI dove recuperare il modello. La classe `AsposeAIModelConfig` gestisce l'auto‑download, la quantizzazione e l'allocazione dei layer GPU.

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

**Perché è importante** – Quantizzare a `int8` riduce drasticamente l'uso di memoria (≈ 4 GB vs 12 GB). Dividere il modello tra GPU e CPU ti permette di eseguire un LLM da 3 miliardi di parametri anche su una modesta RTX 3060. Se non hai una GPU, imposta `gpu_layers=0` e l'SDK manterrà tutto sulla CPU.

> **Suggerimento:** La prima esecuzione scaricherà ~ 1,5 GB, quindi concedi qualche minuto e una connessione stabile.

---

## Passo 2 – Inizializza il Motore AI con la Configurazione del Modello

Ora avviamo il motore Aspose AI e gli forniamo la configurazione appena creata.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Cosa succede dietro le quinte?** L'SDK controlla `directory_model_path` per un modello già presente. Se trova una versione corrispondente la carica immediatamente; altrimenti scarica il file GGUF da Hugging Face, lo decomprime e prepara la pipeline di inferenza.

---

## Passo 3 – Crea il Motore OCR e Collega il Post‑Processore AI

Il motore OCR si occupa del riconoscimento dei caratteri. Collegando `ocr_ai.run_postprocessor` abiliti **pulizia automatica del testo OCR** subito dopo il riconoscimento.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Perché usare un post‑processore?** L'OCR grezzo spesso contiene interruzioni di riga nei posti sbagliati, punteggiatura errata o simboli estranei. L'LLM può riscrivere l'output in frasi corrette, correggere l'ortografia e persino inferire parole mancanti—trasformando un dump grezzo in prosa levigata.

---

## Passo 4 – Esegui OCR su un File Immagine

Con tutto collegato, è il momento di fornire un'immagine al motore.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Caso limite:** Se l'immagine è grande (> 5 MP), potresti volerla ridimensionare prima per velocizzare l'elaborazione. L'SDK accetta un oggetto Pillow `Image`, quindi puoi pre‑processare con `PIL.Image.thumbnail()` se necessario.

---

## Passo 5 – Lascia che l'AI Pulisca il Testo Riconosciuto e Mostra Entrambe le Versioni

Infine invochiamo il post‑processore collegato in precedenza. Questo passaggio mostra il contrasto tra *prima* e *dopo* la pulizia.

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

### Output Atteso

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Nota come l'LLM abbia:

- Corretto errori comuni di OCR (`Th1s` → `This`).  
- Rimosso simboli estranei (`&` → `and`).  
- Normalizzato le interruzioni di riga in frasi corrette.

---

## 🎨 Panoramica Visiva (Workflow Esegui OCR su Immagine)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

Il diagramma sopra riassume l'intera pipeline: **download modello Hugging Face → configura LLM → inizializza AI → motore OCR → post‑processore AI → testo OCR pulito**.

---

## Domande Frequenti & Pro Tips

### E se non ho una GPU?

Imposta `gpu_layers=0` in `AsposeAIModelConfig`. Il modello verrà eseguito interamente su CPU, più lentamente ma comunque funzionante. Puoi anche passare a un modello più piccolo (ad es., `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) per mantenere tempi di inferenza ragionevoli.

### Come cambio modello in seguito?

Basta aggiornare `hugging_face_repo_id` e rieseguire `ocr_ai.initialize(model_config)`. L'SDK rileverà il cambiamento di versione, scaricherà il nuovo modello e sostituirà i file nella cache.

### Posso personalizzare il prompt del post‑processore?

Sì. Passa un dizionario a `custom_settings` con la chiave `prompt_template`. Per esempio:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Devo salvare il testo pulito su file?

Assolutamente. Dopo la pulizia puoi scrivere il risultato in un file `.txt` o `.json` per ulteriori elaborazioni:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusione

Ti abbiamo appena mostrato come **eseguire OCR su file immagine** con Aspose OCR Cloud, **scaricare automaticamente un modello Hugging Face**, configurare con maestria le impostazioni del **modello LLM** e infine **pulire il testo OCR** usando un potente post‑processore LLM. L'intero processo è racchiuso in un unico script Python facile da eseguire e funziona sia su macchine con GPU sia su quelle solo CPU.

Se ti trovi a tuo agio con questa pipeline, sperimenta con:

- **LLM diversi** – prova `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` per una finestra di contesto più ampia.  
- **Elaborazione batch** – itera su una cartella di immagini e aggrega i risultati puliti in un CSV.  
- **Prompt personalizzati** – adatta l'AI al tuo dominio (documenti legali, note mediche, ecc.).

Sentiti libero di modificare il valore `gpu_layers`, cambiare modello o inserire il tuo prompt. Il cielo è il limite, e il codice che hai ora è la rampa di lancio.

Buon coding, e che i tuoi output OCR siano sempre puliti! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}