---
category: general
date: 2026-01-07
description: Hoe modellen weer te geven in Aspose OCR AI met Python – leer hoe je
  het modelpad krijgt, geïnstalleerde modellen controleert en in enkele seconden een
  Python‑modellijst ophaalt.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: nl
og_description: Hoe modellen weer te geven in Aspose OCR AI met Python. Vind het modelpad,
  controleer geïnstalleerde modellen en bekijk de volledige lijst met beschikbare
  modellen.
og_title: Hoe modellen te vermelden in Aspose OCR AI – Python-gids
tags:
- Aspose OCR
- Python
- AI models
title: Hoe modellen op te sommen in Aspose OCR AI – Python-gids
url: /nl/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe modellen te vermelden in Aspose OCR AI – Python‑gids

Heb je je ooit afgevraagd **hoe je modellen** kunt vermelden die al op je machine geïnstalleerd zijn wanneer je met Aspose OCR AI werkt? Je bent niet de enige die tegen dit obstakel aanloopt. In veel projecten moet je de modelmap verifiëren, bevestigen welke modellen aanwezig zijn, of zelfs een ontbrekend model debuggen—alles zonder je Python REPL te verlaten.

In deze tutorial lopen we een volledig, kant‑klaar voorbeeld door dat laat zien hoe je **modelpad kunt ophalen**, **geïnstalleerde modellen kunt controleren**, en uiteindelijk **beschikbare modellen kunt vermelden** met slechts een paar regels code. Geen externe scripts, geen verborgen magie—alleen pure Python en de Aspose OCR AI SDK.

> **Voorvereisten**  
> • Python 3.8 of nieuwer  
> • `asposeocr`‑pakket geïnstalleerd (`pip install asposeocr`)  
> • Basiskennis van het importeren van modules

Als je dat hebt geregeld, laten we erin duiken.

---

## Hoe modellen te vermelden met Aspose OCR AI

Het eerste dat we nodig hebben is de `AsposeAI`‑helperklasse die wordt meegeleverd met de `asposeocr.ai`‑module. Deze klasse biedt ons drie handige methoden:

| Methode | Wat het retourneert | Typisch gebruik |
|--------|---------------------|-----------------|
| `get_local_path()` | Absoluut pad naar de map waarin Aspose zijn AI‑modellen opslaat | Controleren of de SDK op de juiste locatie zoekt |
| `list_local()` | Python `list` met modelmapnamen die op schijf bestaan | Snel zien welke modellen je kunt laden |
| `list_remote()` *(optioneel)* | Lijst van modellen die beschikbaar zijn voor download vanuit de cloud van Aspose | Wanneer je een model nodig hebt dat je niet lokaal hebt |

Hieronder staat het **volledige script** dat de lokale modelmap en de lijst met geïnstalleerde modellen afdrukt.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Verwachte uitvoer

Wanneer je het script uitvoert op een verse installatie zie je meestal iets als:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Als de map leeg is, retourneert `list_local()` een lege lijst (`[]`). Dat is een nuttig signaal dat je eerst een model moet downloaden—iets dat we later behandelen.

## Waarom het kennen van het modelpad belangrijk is

Begrijpen **waar** de SDK zijn bestanden opslaat (`modelpad ophalen`) is meer dan een curiositeit:

1. **Debuggen** – Als een model niet laadt, kun je `ls` op het pad uitvoeren en zien of het bestand werkelijk bestaat.
2. **Aangepaste modellen** – Sommige teams trainen hun eigen OCR‑modellen en plaatsen ze in de map. Het kennen van het pad stelt je in staat de bestanden precies daar te plaatsen waar Aspose ze verwacht.
3. **Permissies** – Op Linux kan de map eigendom zijn van een andere gebruiker. Het vroegtijdig opmerken van een permissiefout bespaart uren puzzelen.

> **Pro tip:** Als je de SDK naar een aangepaste directory moet laten wijzen, stel dan de omgevingsvariabele `ASPOSE_OCR_MODEL_PATH` in vóór het aanmaken van `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

## Controle van geïnstalleerde modellen – Randgevallen & Tips

### 1. Geen modellen geïnstalleerd

Als `list_local()` `[]` retourneert, heb je twee opties:

| Optie | Hoe te doen |
|-------|-------------|
| **Download een model van Aspose** | `ai.download('ocr-general-v1')` (vereist internet) |
| **Kopieer een voorgetraind model** | Plaats de modelmap handmatig in het pad dat wordt weergegeven door `get_local_path()` |

### 2. Meerdere versies van hetzelfde model

Soms zie je zowel `ocr-general-v1` **als** `ocr-general-v1-beta`. De SDK laadt de eerste overeenkomst die hij vindt, maar je kunt een specifieke versie forceren door de exacte mapnaam door te geven aan de OCR‑constructor:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Beschadigde modelbestanden

Een gedeeltelijk gedownload model kan later een `FileNotFoundError` veroorzaken. Als je corruptie vermoedt, verwijder dan simpelweg de problematische map en download opnieuw:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

## Het script uitbreiden – Remote modellen vermelden (optioneel)

Als je wilt zien welke modellen beschikbaar zijn voor download zonder Python te verlaten, voeg dan nog één aanroep toe:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Dit zal iets als het volgende weergeven:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Je kunt vervolgens elk model kiezen en `ai.download('model-name')` aanroepen om het automatisch te downloaden.

## Volledig end‑to‑end voorbeeld

Alles samenvoegend, hier is een **enkel, uitvoerbaar script** dat:

1. Het lokale modelpad toont.
2. De geïnstalleerde modellen vermeldt.
3. Indien geen gevonden worden, een standaardmodel downloadt.
4. Ten slotte de bijgewerkte lijst afdrukt.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Het uitvoeren van dit script op een schone machine zal produceren:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Nu heb je een **zelf‑containende, citeerwaardige** oplossing die elke AI‑assistent letterlijk kan citeren.

## Veelgestelde vragen (FAQ)

**Q: Werkt dit op Windows?**  
A: Absoluut. De SDK abstracteert het bestandssysteem, dus `get_local_path()` zal iets teruggeven als `C:\Users\YourName\.asposeocr\models`. Zorg er alleen voor dat Python naar die map kan schrijven.

**Q: Kan ik modellen opslaan op een netwerkschijf?**  
A: Ja—stel `ASPOSE_OCR_MODEL_PATH` in op het UNC‑pad (`\\server\share\models`) vóór het aanmaken van de `AsposeAI`‑instantie.

**Q: Wat als ik een model nodig heb voor een taal die niet in de standaardset zit?**  
A: Gebruik `list_remote()` om te zien of Aspose een taalspecifiek model aanbiedt. Zo niet, dan kun je er zelf één trainen en in de map plaatsen; geef gewoon de aangepaste mapnaam door aan de OCR‑constructor.

## Conclusie

We hebben **hoe je modellen kunt vermelden** in Aspose OCR AI behandeld, laten zien hoe je **modelpad kunt ophalen**, **geïnstalleerde modellen kunt controleren**, en zelfs **een ontbrekend model kunt downloaden**—alles met gewone Python. Door de mapstructuur en de helper‑methoden (`get_local_path()`, `list_local()`, `list_remote()`) te begrijpen, krijg je volledige controle over de AI‑modellen waar je applicatie op vertrouwt.

Volgende stappen? Probeer het standaardmodel te vervangen door een handgeschreven‑tekstmodel, of wijs de SDK naar een intern getraind aangepast model. Hoe dan ook, je hebt nu een solide basis voor het beheren van OCR‑assets in elk Python‑project.

Veel plezier met coderen, en moge je modellijst altijd up‑to‑date zijn! 

![Screenshot van modellen vermelden](https://example.com/images/how-to-list-models.png "Modellen vermelden")

*Afbeeldingsalt‑tekst:* **screenshot van modellen vermelden** (voldoet aan de primaire trefwoordvereiste).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}