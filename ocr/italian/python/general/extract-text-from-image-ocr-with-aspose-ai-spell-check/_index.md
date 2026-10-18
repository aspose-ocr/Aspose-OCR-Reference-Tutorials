---
category: general
date: 2026-05-03
description: estrai il testo da un'immagine usando Aspose OCR e il controllo ortografico
  AI. Scopri come eseguire l'OCR su un'immagine, caricare l'immagine per l'OCR, riconoscere
  il testo da una fattura e rilasciare le risorse GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: it
og_description: estrai il testo da un'immagine con Aspose OCR e il controllo ortografico
  AI. Guida passo‑passo che copre come eseguire l'OCR su un'immagine, caricare l'immagine
  per l'OCR e rilasciare le risorse GPU.
og_title: Estrai testo da immagine – Guida completa a OCR e correzione ortografica
tags:
- OCR
- Aspose
- AI
- Python
title: Estrai testo da immagine – OCR con Aspose AI Spell‑Check
url: /it/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# estrarre testo da immagine – Guida completa OCR & Spell‑Check

Ti è mai capitato di dover **estrarre testo da immagine** ma non eri sicuro quale libreria ti offrisse sia velocità che precisione? Non sei l'unico. In molti progetti reali—pensa all'elaborazione di fatture, alla digitalizzazione di ricevute o alla scansione di contratti—ottenere testo pulito e ricercabile da un'immagine è il primo ostacolo.

La buona notizia è che Aspose OCR, abbinato a un modello leggero Aspose AI, può gestire questo compito in poche righe di Python. In questo tutorial vedremo **come fare OCR su un'immagine**, caricare correttamente la foto, eseguire un correttore ortografico integrato e infine **rilasciare le risorse GPU** affinché la tua app rimanga a basso consumo di memoria.

Alla fine di questa guida sarai in grado di **riconoscere testo da immagini di fatture**, correggere automaticamente gli errori OCR più comuni e mantenere la tua GPU pulita per il prossimo batch.

---

## Di cosa avrai bisogno

- Python 3.9 o versioni successive (il codice usa type hints ma funziona anche su versioni 3.x precedenti)
- Pacchetti `aspose-ocr` e `aspose-ai` (installali con `pip install aspose-ocr aspose-ai`)
- Una GPU abilitata CUDA è opzionale; lo script tornerà alla CPU se non ne trova una.
- Un'immagine di esempio, ad es. `sample_invoice.png`, posizionata in una cartella a cui puoi fare riferimento.

Nessun framework ML pesante, nessun download di modelli enormi—solo un piccolo modello quantizzato Q4‑K‑M che si adatta comodamente alla maggior parte delle GPU.

---

## Passo 1: Inizializzare il motore OCR – estrarre testo da immagine

La prima cosa da fare è creare un'istanza di `OcrEngine` e indicare quale lingua ti aspetti. Qui scegliamo l'inglese e richiediamo un output in plain‑text, ideale per l'elaborazione successiva.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Perché è importante:** Impostare la lingua restringe il set di caratteri, migliorando la precisione. La modalità plain‑text rimuove le informazioni di layout che tipicamente non ti servono quando vuoi solo estrarre testo da immagine.

---

## Passo 2: Caricare l'immagine per OCR – come fare OCR su un'immagine

Ora forniamo al motore un'immagine reale. L'helper `Image.load` riconosce i formati più comuni (PNG, JPEG, TIFF) e astrae le particolarità del file‑IO.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Suggerimento:** Se le tue immagini di origine sono grandi, considera di ridimensionarle prima di inviarle al motore; dimensioni più piccole possono ridurre l'uso di memoria GPU senza compromettere la qualità del riconoscimento.

---

## Passo 3: Configurare il modello Aspose AI – riconoscere testo da fattura

Aspose AI include un piccolo modello GGUF che puoi scaricare automaticamente. L'esempio utilizza il repository `Qwen2.5‑3B‑Instruct‑GGUF`, quantizzato a `q4_k_m`. Indichiamo inoltre al runtime di allocare 20 layer sulla GPU, bilanciando velocità e utilizzo della VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Dietro le quinte:** Il modello quantizzato occupa circa 1,5 GB su disco, una frazione di un modello a piena precisione, ma cattura comunque abbastanza sfumature linguistiche da segnalare gli errori tipici dell'OCR.

---

## Passo 4: Inizializzare AsposeAI e collegare il post‑processore di correzione ortografica

Aspose AI include un post‑processore di correzione ortografica pronto all'uso. Collegandolo, ogni risultato OCR verrà pulito automaticamente.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Perché usare il post‑processore?** I motori OCR spesso leggono “Invoice” come “Invo1ce” o “Total” come “T0tal”. La correzione ortografica esegue un modello linguistico leggero sulla stringa grezza e corregge quegli errori senza che tu debba scrivere un dizionario personalizzato.

---

## Passo 5: Eseguire il post‑processore di correzione ortografica sul risultato OCR

Con tutto collegato, una singola chiamata restituisce il testo corretto. Stampiamo anche entrambe le versioni, originale e pulita, così puoi vedere il miglioramento.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Un output tipico per una fattura potrebbe apparire così:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Nota come “Invo1ce” sia diventato la parola corretta “Invoice”. Questa è la potenza del correttore ortografico AI integrato.

---

## Passo 6: Rilasciare le risorse GPU – rilasciare le risorse GPU in modo sicuro

Se esegui questo in un servizio a lungo termine (ad esempio un'API web che elabora decine di fatture al minuto), devi liberare il contesto GPU dopo ogni batch. Altrimenti vedrai perdite di memoria e alla fine otterrai errori “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Consiglio professionale:** Chiama `free_resources()` all'interno di un blocco `finally` o di un context manager affinché venga sempre eseguito, anche in caso di eccezione.

---

## Esempio completo funzionante

Unire tutti i componenti ti fornisce uno script autonomo che puoi inserire in qualsiasi progetto.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Salva il file, regola il percorso della tua immagine ed esegui `python extract_text_from_image.py`. Dovresti vedere il testo della fattura pulito stampato sulla console.

---

## Domande frequenti (FAQ)

**Q: Funziona su macchine solo CPU?**  
**A:** Assolutamente. Se non viene rilevata alcuna GPU, Aspose AI ricade sull'esecuzione CPU, anche se sarà più lenta. Puoi forzare la CPU impostando `model_cfg.gpu_layers = 0`.

**Q: E se le mie fatture sono in una lingua diversa dall'inglese?**  
**A:** Cambia `ocr_engine.language` al valore enum appropriato (ad es., `aocr.Language.Spanish`). Il modello di correzione ortografica è multilingue, ma potresti ottenere risultati migliori con un modello specifico per la lingua.

**Q: Posso elaborare più immagini in un ciclo?**  
**A:** Sì. Sposta semplicemente i passaggi di caricamento, riconoscimento e post‑processing all'interno di un ciclo `for`. Ricorda di chiamare `ocr_ai.free_resources()` dopo il ciclo o dopo ogni batch se riutilizzi la stessa istanza AI.

**Q: Quanto è grande il download del modello?**  
**A:** Circa 1,5 GB per la versione quantizzata `q4_k_m`. Viene memorizzato nella cache dopo la prima esecuzione, quindi le esecuzioni successive sono istantanee.

---

## Conclusione

In questo tutorial abbiamo mostrato come **estrarre testo da immagine** usando Aspose OCR, configurare un piccolo modello AI, applicare un post‑processore di correzione ortografica e rilasciare in modo sicuro le **risorse GPU**. Il flusso di lavoro copre tutto, dal caricamento dell'immagine alla pulizia finale, fornendoti una pipeline affidabile per scenari di **riconoscimento testo da fattura**.

Passi successivi? Prova a sostituire il correttore ortografico con un modello personalizzato di estrazione di entità

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}