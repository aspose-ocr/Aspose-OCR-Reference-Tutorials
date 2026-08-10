---
category: general
date: 2026-04-26
description: Maschera rapidamente i numeri delle carte di credito usando il post‑processing
  OCR di AsposeAI. Impara la conformità PCI, il mascheramento con espressioni regolari
  e la sanitizzazione dei dati in un tutorial passo‑passo.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: it
og_description: Maschera i numeri delle carte di credito nei risultati OCR con AsposeAI.
  Questo tutorial copre la conformità PCI, la mascheratura con espressioni regolari
  e la sanitizzazione dei dati.
og_title: Mascherare i numeri delle carte di credito – Guida completa al post‑processing
  OCR in Python
tags:
- OCR
- Python
- security
title: Mascherare i numeri delle carte di credito nell'output OCR – Guida completa
  Python
url: /it/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mascherare i numeri delle carte di credito – Guida completa Python

Hai mai dovuto **mascherare i numeri delle carte di credito** in un testo proveniente direttamente da un motore OCR? Non sei l'unico. Nei settori regolamentati, esporre un PAN completo (Primary Account Number) può metterti nei guai con gli auditor della conformità PCI. La buona notizia? Con poche righe di Python e il hook di post‑processing di AsposeAI, puoi nascondere automaticamente le otto cifre centrali e rimanere al sicuro.

In questo tutorial seguirà uno scenario reale: eseguire l'OCR su un'immagine di una ricevuta, quindi applicare una funzione personalizzata di **post‑processing OCR** che sanifica qualsiasi dato PCI. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi workflow AsposeAI, oltre a una serie di consigli pratici per gestire i casi limite e scalare la soluzione.

## Cosa imparerai

- Come registrare un post‑processor personalizzato con **AsposeAI**.
- Perché un approccio di **mascheramento con espressioni regolari** è sia veloce che affidabile.
- Le basi della **conformità PCI** relative alla sanificazione dei dati.
- Modi per estendere il pattern a più formati di carte o numeri internazionali.
- Output previsto e come verificare che il mascheramento abbia funzionato.

> **Prerequisiti** – Dovresti avere un ambiente Python 3 funzionante, il pacchetto Aspose.AI for OCR installato (`pip install aspose-ocr`), e un'immagine di esempio (ad es. `receipt.png`) che contenga un numero di carta di credito. Non sono richiesti altri servizi esterni.

---

## Passo 1: Definire un Post‑Processor che Maschera i Numeri delle Carte di Credito

Il cuore della soluzione risiede in una piccola funzione che riceve il risultato OCR, esegue una routine di **mascheramento con espressioni regolari** e restituisce il testo sanificato.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Perché funziona:**  
- L'espressione regolare `(\d{4})\d{8}(\d{4})` corrisponde esattamente a 16 cifre consecutive, il formato comune per Visa, MasterCard e molte altre.  
- Catturando le prime quattro e le ultime quattro cifre (`\1` e `\2`) preserviamo informazioni sufficienti per il debug rispettando le regole di **conformità PCI** che vietano la memorizzazione del PAN completo.  
- La sostituzione `\1****\2` nasconde le otto cifre sensibili al centro, trasformando `1234567812345678` in `1234****5678`.

> **Suggerimento professionale:** Se devi supportare numeri American Express a 15 cifre, aggiungi un secondo pattern come `r'(\d{4})\d{6}(\d{5})'` ed esegui entrambe le sostituzioni in sequenza.

---

## Passo 2: Inizializzare il Motore AsposeAI

Prima di poter collegare il nostro post‑processor, ci serve un'istanza del motore OCR. AsposeAI include il modello OCR e una semplice API per l'elaborazione personalizzata.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Perché inizializzare qui?**  
Creare l'oggetto `AsposeAI` una sola volta e riutilizzarlo su più immagini riduce l'overhead. Il motore inoltre memorizza nella cache i modelli linguistici, accelerando le chiamate successive—utile quando si scansionano lotti di ricevute.

---

## Passo 3: Registrare la Funzione di Mascheramento Personalizzata

AsposeAI espone un metodo `set_post_processor` che consente di collegare qualsiasi callable. Passiamo la nostra funzione `mask_pci` insieme a un dizionario di impostazioni opzionale (vuoto per ora).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Cosa succede dietro le quinte?**  
Quando in seguito invochi `run_postprocessor`, AsposeAI passerà il risultato OCR grezzo a `mask_pci`. La funzione riceve un oggetto leggero (`data`) che contiene il testo riconosciuto, e restituisci una nuova stringa. Questo design mantiene intatto il core OCR consentendoti di applicare le politiche di **sanificazione dei dati** in un unico punto.

---

## Passo 4: Eseguire l'OCR sull'Immagine della Ricevuta

Ora che il motore sa come pulire l'output, gli forniamo un'immagine. Per il tutorial assumiamo che tu abbia già un oggetto `engine` configurato con le impostazioni di lingua e risoluzione corrette.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Suggerimento:** Se non hai un oggetto pre‑configurato, puoi crearne uno con:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

La chiamata `recognize_image` restituisce un oggetto il cui attributo `text` contiene la stringa grezza, non mascherata.

---

## Passo 5: Applicare il Post‑Processor Registrato

Con i dati OCR grezzi a disposizione, li passiamo all'istanza AI. Il motore esegue automaticamente la funzione `mask_pci` che abbiamo registrato in precedenza.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Perché usare `run_postprocessor` invece di chiamare la funzione manualmente?**  
In questo modo il flusso di lavoro rimane coerente, soprattutto quando hai più post‑processor (ad es., correzione ortografica, rilevamento della lingua). AsposeAI li accoda nell'ordine in cui li registri, garantendo un output deterministico.

---

## Passo 6: Verificare l'Output Sanificato

Infine, stampiamo il testo sanificato e confermiamo che tutti i numeri delle carte di credito siano correttamente mascherati.

```python
print(final_result.text)
```

**Output previsto** (estratto):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Se la ricevuta non contiene alcun numero di carta, il testo rimane invariato—nulla da mascherare, nulla di cui preoccuparsi.

---

## Gestione dei Casi Limite e delle Variazioni Comuni

### Più Numeri di Carta in un Documento
Se una ricevuta include più di un PAN (ad es., una carta fedeltà più una carta di pagamento), l'espressione regolare viene eseguita globalmente, mascherando automaticamente tutte le corrispondenze. Nessun codice aggiuntivo necessario.

### Formattazione Non Standard
A volte l'OCR inserisce spazi o trattini (`1234 5678 1234 5678` o `1234-5678-1234-5678`). Estendi il pattern per ignorare questi caratteri:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Il `[ -]?` aggiunto tollera spazi o trattini opzionali tra i blocchi di cifre.

### Carte Internazionali
Per PAN a 19 cifre usati in alcune regioni, puoi ampliare il pattern:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Ricorda solo che la **conformità PCI** richiede comunque di mascherare le cifre centrali, indipendentemente dalla lunghezza.

### Registrare i Valori Mascherati (Opzionale)
Se hai bisogno di tracciamenti di audit, passa un flag tramite `custom_settings` e adatta la funzione:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Quindi registra con:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Esempio Completo (Pronto per Copia‑Incolla)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Eseguendo questo script su una ricevuta che contiene `4111111111111111` otterrai:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Questo è l'intero pipeline—dal OCR grezzo alla **sanificazione dei dati**—racchiuso in poche linee pulite di Python.

---

## Conclusione

Ti abbiamo appena mostrato come **mascherare i numeri delle carte di credito** nei risultati OCR usando il hook di post‑processing di AsposeAI, una routine concisa di espressioni regolari e una serie di consigli di best practice per la **conformità PCI**. La soluzione è completamente autonoma, funziona con qualsiasi immagine che il motore OCR può leggere e può essere estesa per coprire formati di carta più complessi o requisiti di registrazione.

Pronto per il passo successivo? Prova a combinare questo mascheramento con una routine di **inserimento nel database** che memorizzi solo le ultime quattro cifre per riferimento, oppure integra un **processore batch** che scansioni un'intera cartella di ricevute durante la notte. Potresti anche esplorare altri compiti di **post‑processing OCR** come la standardizzazione degli indirizzi o il rilevamento della lingua—ognuno segue lo stesso pattern che abbiamo usato qui.

Hai domande sui casi limite, sulle prestazioni o su come adattare il codice a una libreria OCR diversa? Lascia un commento qui sotto e continuiamo la discussione. Buon coding e rimani al sicuro!  



![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}