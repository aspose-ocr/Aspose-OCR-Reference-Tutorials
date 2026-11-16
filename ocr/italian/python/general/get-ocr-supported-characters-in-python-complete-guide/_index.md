---
category: general
date: 2026-06-25
description: Ottieni rapidamente i caratteri supportati dall'OCR usando la libreria
  aocr. Scopri come elencare i caratteri OCR, impostare le lingue e fare il debug
  del tuo motore OCR in Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: it
og_description: Ottieni i caratteri supportati dall'OCR con aocr. Questa guida ti
  mostra come elencare i caratteri OCR, scegliere le lingue e gestire i casi particolari
  in Python.
og_title: Ottieni i caratteri supportati da OCR in Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Ottieni i caratteri supportati da OCR in Python – Guida completa
url: /it/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni i caratteri supportati da OCR in Python – Guida completa

Ti sei mai chiesto come **ottenere i caratteri supportati da OCR** per una lingua specifica mentre sperimenti con un motore OCR? Non sei solo. Che tu stia costruendo uno scanner di ricevute o un parser di documenti multilingue, sapere esattamente quali glifi il tuo motore può riconoscere è una salvezza. In questo tutorial percorreremo l’intero processo—installare la libreria, configurare la lingua e infine elencare quei caratteri—così potrai fare debug e ottimizzare la tua pipeline OCR in pochi minuti.

Useremo la libreria **aocr**, un motore OCR leggero per Python che rende semplice interrogare le capacità linguistiche. Alla fine di questa guida sarai in grado di **elencare i caratteri OCR**, passare tra **lingue OCR supportate** e persino individuare lacune nella copertura prima che ti creino problemi in produzione.

---

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.8 o successivo (il pacchetto aocr non supporta più la 3.7)
* Un terminale o prompt dei comandi con accesso a Internet
* Familiarità di base con la programmazione Python (se hai già scritto un `print()`, sei a posto)

Nessuna dipendenza esterna pesante—solo il pacchetto `aocr` su pip.

---

## Installa la libreria aocr (OCR Engine Python)

La prima cosa di cui hai bisogno è un’installazione funzionante di **OCR engine Python**. Il pacchetto aocr è disponibile su PyPI, quindi un unico comando pip basta:

```bash
pip install aocr
```

Se utilizzi un ambiente virtuale (altamente consigliato), attivalo prima:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Blocca la versione (`pip install aocr==1.2.4`) per evitare cambiamenti inattesi dell’API in futuro.

---

## Scegli una lingua (Supported OCR Languages)

aocr include un piccolo set di pacchetti linguistici integrati. Ogni pacchetto definisce l’insieme di punti di codice Unicode che il motore può riconoscere. Per interrogare questi pacchetti devi impostare l’attributo `language` sull’istanza del motore.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Puoi sostituire `aocr.Language.ENGLISH` con qualsiasi altro valore enum (`FRENCH`, `GERMAN`, ecc.). Se provi ad assegnare una lingua che non è inclusa, aocr solleva un `ValueError`. Per questo è consigliabile controllare prima l’elenco delle **supported OCR languages**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Recupera l’insieme di caratteri (Get OCR Supported Characters)

Ora arriva il cuore del tutorial: **ottenere i caratteri supportati da OCR**. Il motore espone un metodo pratico chiamato `get_supported_characters()` che restituisce una lista di stringhe a singolo carattere.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Dietro le quinte, aocr legge un file JSON incluso nel pacchetto linguistico e converte ogni punto di codice Unicode in una stringa Python. Il risultato è deterministico, il che significa che otterrai la stessa lista ogni volta che esegui lo script sulla stessa versione della lingua.

---

## Mostra quanti caratteri sono supportati

Conoscere il conteggio ti aiuta a valutare rapidamente l’estensione della copertura. Per l’inglese, di solito vedrai qualche migliaio di caratteri (inclusi punteggiatura e cifre).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

La chiamata `len()` è O(1) perché Python memorizza internamente la lunghezza della lista, quindi non c’è alcuna penalità di prestazioni anche per alfabeti di grandi dimensioni.

---

## Anteprima dei primi 100 caratteri supportati

Un rapido controllo visivo può rivelare se il motore include i simboli di cui hai bisogno (pensa al simbolo dell’Euro o alle virgolette tipografiche). Stampiamo i primi cento caratteri:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

L’operazione `join` concatena la porzione in una singola stringa, più leggibile rispetto alla stampa di una lista Python.

---

## Script completo – Tutti i passaggi in un unico posto

Di seguito trovi l’esempio completo e eseguibile che collega tutto. Salvalo come `list_supported_chars.py` ed esegui `python list_supported_chars.py` dal tuo terminale.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Output previsto (troncato per brevità):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Il conteggio esatto può variare leggermente a seconda della versione di aocr, ma vedrai sempre un lungo alfabeto più la punteggiatura comune.

---

## Gestione dei casi limite

### Cosa succede se il pacchetto linguistico è mancante?

Se richiedi una lingua che non è inclusa, `aocr.Language` non conterrà l’enum e otterrai un `AttributeError`. Proteggi il tuo codice con un semplice controllo:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Lista di caratteri vuota

Alcune lingue di nicchia potrebbero restituire una lista vuota se i dati di addestramento sottostanti sono incompleti. In tal caso, puoi ricorrere a un valore predefinito (ad es. l’inglese) o lanciare un avviso:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalizzazione Unicode

La lista può contenere caratteri combinati (ad es. “é” come `e` + accento acuto). Se il tuo downstream processing si aspetta glifi pre‑composti, esegui un passaggio di normalizzazione:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro Tips per progetti reali

* **Cache della lista di caratteri** – Se elabori migliaia di immagini, chiamare `get_supported_characters()` ad ogni iterazione aggiunge overhead inutile. Conserva la lista in una variabile a livello di modulo o serializzala in JSON per riutilizzi futuri.
* **Validazione cross‑lingua** – Quando supporti più lingue in una singola app, interseca i set di caratteri per trovare un sottoinsieme comune. Questo ti aiuta a progettare elementi UI coerenti tra le varie localizzazioni.
* **Debug dei fallimenti OCR** – Se il motore classifica erroneamente un glifo, confronta il carattere problematico con l’output di `list_supported_chars`. Se manca, hai identificato una lacuna di copertura che potrebbe richiedere un addestramento personalizzato.
* **Combina con font personalizzati** – aocr rispetta l’intervallo Unicode, ma la qualità del rendering può variare a seconda del font. Testa i tuoi caratteri supportati con il font esatto che userai in produzione per evitare sorprese.

---

## Domande frequenti

**D: Funziona con aocr versione 2.x?**  
R: Sì, il metodo `get_supported_characters()` è stabile sia nella 1.x che nella 2.x. L’unica modifica è che gli enum delle lingue sono stati spostati in `aocr.languages`.

**D: Posso ottenere il punto di codice Unicode per ogni carattere?**  
R: Assolutamente. Usa `ord(ch)` all’interno di una list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**D: E per le scritture da destra a sinistra come l’Arabo?**  
R: aocr include un enum `ARABIC`. La lista di caratteri conterrà glifi arabi, ma potresti dover abilitare il rendering RTL nella tua UI downstream.

---

## Conclusione

Ora sai **come ottenere i caratteri supportati da OCR** usando la libreria aocr in Python, come passare tra **lingue OCR supportate** e perché **elencare i caratteri OCR** è fondamentale per pipeline di riconoscimento testo robuste. Con lo script completo e i consigli sopra, potrai verificare rapidamente la copertura linguistica, fare debug dei glifi mancanti e costruire applicazioni OCR più intelligenti.

Pronto per il passo successivo? Prova a combinare questa lista di caratteri con un filtro di parole personalizzato, o sperimenta con un motore OCR diverso (Tesseract, EasyOCR) e confronta i risultati. Più esplori, migliori saranno le tue soluzioni OCR.

Buon coding, e che i tuoi set di caratteri siano sempre completi!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Specifica i caratteri consentiti OCR – Utilizzando Aspose.OCR per .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Come eseguire OCR su testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Post‑processing OCR – Ottenere le scelte dei caratteri](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}