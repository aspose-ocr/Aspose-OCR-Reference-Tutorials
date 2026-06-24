---
category: general
date: 2026-06-22
description: Leer hoe je gecachte AI-modellen kunt weergeven met de AI‑SDK in Python.
  Inclusief stappen om de modelcachemap op te halen en lokale AI-modellen efficiënt
  te beheren.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: nl
og_description: Toon gecachte AI-modellen met Python via de AI‑SDK. Volg deze stap‑voor‑stap
  tutorial om de modelcache‑directory op te halen en lokale AI-modellen te beheren.
og_title: Lijst van gecachte AI-modellen in Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Lijst van gecachte AI-modellen in Python – Complete gids
url: /nl/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lijst van gecachte AI-modellen in Python – Complete gids

Heb je je ooit afgevraagd hoe je **gecachte AI-modellen** op je werkstation kunt **opsommen** zonder door obscure mappen te moeten graven? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze moeten verifiëren welke modellen al lokaal zijn opgeslagen, vooral bij beperkte bandbreedte of offline implementaties. In deze tutorial zie je een snelle, zonder poespas manier om de AI SDK te bevragen, de cache‑inhoud af te drukken en precies te ontdekken waar die bestanden zich bevinden.

We zullen ook gerelateerde onderwerpen aanraken zoals **het ophalen van de modelcache‑directory**, het omgaan met lege caches, en best practices voor **het beheren van AI modelcache** in productiescripts. Aan het einde heb je een zelfstandige code‑fragment dat je in elk Python‑project kunt plaatsen.

## Vereisten

- Python 3.8 of nieuwer geïnstalleerd.
- De AI SDK (het `ai`‑pakket) geïnstalleerd via `pip install ai-sdk` of de interne repository van je organisatie.
- Basiskennis van het uitvoeren van scripts vanaf de commandoregel.

Er zijn geen extra bibliotheken nodig, dus het voorbeeld blijft lichtgewicht en draagbaar.

---

## Lijst van gecachte AI-modellen – Snel overzicht

Het eerste dat je moet doen is de SDK importeren en haar hulpfuncties aanroepen. De SDK biedt twee handige methoden:

1. `ai.list_local()` – retourneert een Python‑lijst met model‑identifiers die al gecached zijn.
2. `ai.get_local_path()` – retourneert de absolute map waarin die modelbestanden zich bevinden.

Beide aanroepen zijn synchroon en geven een duidelijke `AIError` als er iets misgaat, waardoor foutafhandeling eenvoudig is.

> **Waarom deze functies gebruiken?**  
> Het kennen van de exacte set gecachte modellen laat je onnodige downloads vermijden, versie‑mismatches debuggen en oude artefacten automatisch opruimen. Het is een klein onderdeel van de grotere **AI SDK Python** workflow, maar het kan je uren handmatig zoeken in het bestandssysteem besparen.

### Stap 1: Importeer de AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Waarom dit belangrijk is:* Het importeren van het pakket registreert de onderliggende C‑extensions en laadt configuratiebestanden (zoals cache‑paden) uit je omgeving. Het overslaan van deze stap zal een `ModuleNotFoundError` veroorzaken op het moment dat je een SDK‑functie aanroept.

### Stap 2: Lijst alle gecachte modellen

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Wat je zult zien:** Als je drie modellen opgeslagen hebt, kan de output er als volgt uitzien:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Als de cache leeg is, krijg je een lege lijst:

```
Cached models: []
```

> **Pro tip:** Wikkel de aanroep in een try/except‑blok als je vermoedt dat de SDK niet correct is geïnitialiseerd.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Stap 3: Haal de modelcache‑directory op

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Typische output op een Unix‑achtig systeem:

```
Model cache directory: /home/you/.cache/ai/models
```

Op Windows zie je misschien iets als `C:\Users\you\AppData\Local\ai\models`. Het kennen van dit pad is essentieel wanneer je **AI modelcache** handmatig moet beheren — bijvoorbeeld om oude versies te verwijderen of bestanden naar een gedeelde schijf te kopiëren.

---

## Visueel overzicht

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt‑tekst:* Diagram dat laat zien hoe je gecachte AI-modellen opsomt, hun namen ophaalt en de cache‑directory lokaliseert.

---

## Omgaan met randgevallen en veelvoorkomende valkuilen

### Lege cache

Als `ai.list_local()` een lege lijst retourneert, kun je je afvragen of de SDK verkeerd geconfigureerd is. Controleer de omgevingsvariabele `AI_CACHE_DIR` (of het configuratiebestand van de SDK) om er zeker van te zijn dat deze naar een schrijfbare locatie wijst.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Machtigingsproblemen

Bij het benaderen van `ai.get_local_path()` kan een `PermissionError` optreden op restrictieve systemen. De oplossing is meestal om het script uit te voeren met de juiste gebruikersrechten of de ACL‑rechten van de map aan te passen.

### Versiemismatches

Soms bevat de cache een oudere versie van een model terwijl je code een nieuwere vraagt. De SDK zal automatisch de nieuwere versie downloaden, maar je kunt dit voorkomen door de versie‑tag in de lijst te inspecteren:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Oude modellen opruimen

Als je ruimte wilt vrijmaken, kun je een specifieke modelmap direct verwijderen:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Het uitvoeren van `purge_model('bert-base-uncased')` zal dat model verwijderen en schijfruimte vrijmaken.

---

## Volledig script dat je kunt kopiëren‑plakken

Hieronder staat een kant‑klaar script dat alle stappen combineert, basisfoutafhandeling toevoegt en een vriendelijke samenvatting afdrukt.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Verwachte output (wanneer de cache gevuld is):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Voer het script uit met `python list_models.py` en je weet direct wat er op de schijf staat.

---

## Veelgestelde vragen

**Q: Werkt dit op alle besturingssystemen?**  
A: Ja. De SDK abstraheert OS‑specifieke paden, dus `ai.get_local_path()` retourneert een geldige string op Linux, macOS en Windows.

**Q: Kan ik modellen uit een externe cache opsommen?**  
A: De ingebouwde `list_local()` rapporteert alleen lokaal opgeslagen artefacten. Voor externe registries zou je `ai.list_remote()` gebruiken (als jouw SDK‑versie dit biedt).

**Q: Wat als de SDK‑naam niet `ai` is?**  
A: Vervang de importregel door de daadwerkelijke pakketnaam, bijv. `import myai as ai`. Alle volgende aanroepen blijven hetzelfde omdat het API‑contract consistent is tussen implementaties.

---

## Conclusie

Je hebt nu een solide, productie‑klare methode om **gecachte AI-modellen** te **list** met de **AI SDK Python**‑bibliotheek, de **modelcache‑directory** op te halen en zelfs oude bestanden op te ruimen. Deze kennis helpt je je omgeving netjes te houden, overbodige downloads te vermijden en versie‑problemen eenvoudig te debuggen.

Klaar voor de volgende stap? Probeer het script uit te breiden om ontbrekende modellen automatisch te downloaden, of integreer het in een CI‑pipeline die de cache‑gezondheid valideert vóór elke build. Het verkennen van **AI modelcache beheren**‑strategieën maakt je AI‑aangedreven applicaties sneller en betrouwbaarder.

Veel plezier met coderen, en moge je caches slank blijven!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe batch OCR‑afbeeldingen te verwerken met List in Aspose.OCR voor .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Afbeeldingstekst extraheren in C# met taalkeuze met behulp van Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hoe tekst uit ZIP‑archieven te extraheren met Aspose.OCR voor .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}