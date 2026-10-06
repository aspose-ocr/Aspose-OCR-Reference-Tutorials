---
category: general
date: 2026-02-22
description: Leer hoe je gecachte modellen kunt opsommen en snel de cachemap op je
  computer kunt weergeven. Inclusief stappen om de cachemap te bekijken en lokale
  AI‑modelopslag te beheren.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: nl
og_description: Ontdek hoe je gecachte modellen kunt opsommen, de cachemap kunt tonen
  en de cachefolder kunt bekijken in een paar eenvoudige stappen. Volledig Python‑voorbeeld
  inbegrepen.
og_title: lijst met gecachte modellen – snelle gids om cachemap te bekijken
tags:
- AI
- caching
- Python
- development
title: lijst van gecachte modellen – hoe de cachemap te bekijken en de cachemap weer
  te geven
url: /nl/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# lijst gecachte modellen – snelle gids om cache‑map te bekijken

Heb je je ooit afgevraagd hoe je **gecachte modellen** op je werkstation kunt **lijsten** zonder door obscure mappen te graven? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze moeten verifiëren welke AI‑modellen al lokaal zijn opgeslagen, vooral wanneer schijfruimte schaars is. Het goede nieuws? Met slechts een handvol regels kun je zowel **gecachte modellen** **lijsten** als de **cache‑map tonen**, waardoor je volledige zichtbaarheid krijgt op je cache‑folder.

In deze tutorial lopen we een zelfstandige Python‑script door die precies dat doet. Aan het einde weet je hoe je de cache‑map kunt bekijken, waar de cache zich bevindt op verschillende besturingssystemen, en zie je een nette afgedrukte lijst van elk model dat is gedownload. Geen externe docs, geen giswerk—alleen duidelijke code en uitleg die je nu kunt copy‑pasten.

## Wat je gaat leren

- Hoe je een AI‑client (of een stub) initialiseert die caching‑hulpmiddelen biedt.  
- De exacte commando’s om **gecachte modellen** te **lijsten** en de **cache‑map te tonen**.  
- Waar de cache zich bevindt op Windows, macOS en Linux, zodat je er handmatig naartoe kunt navigeren als je wilt.  
- Tips voor het omgaan met randgevallen zoals een lege cache of een aangepast cache‑pad.  

**Prerequisites** – je hebt Python 3.8+ en een via pip installeerbare AI‑client nodig die `list_local()`, `get_local_path()` en eventueel `clear_local()` implementeert. Als je er nog geen hebt, gebruikt het voorbeeld een mock‑klasse `YourAIClient` die je kunt vervangen door de echte SDK (bijv. `openai`, `huggingface_hub`, etc.).  

Klaar? Laten we beginnen.

## Stap 1: Zet de AI‑client op (of een mock)

Als je al een client‑object hebt, sla dit blok dan over. Maak anders een klein stand‑in dat de caching‑interface nabootst. Dit maakt het script uitvoerbaar zelfs zonder een echte SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** Als je al een echte client hebt (bijv. `from huggingface_hub import HfApi`), vervang dan de aanroep `YourAIClient()` door `HfApi()` en zorg dat de methoden `list_local` en `get_local_path` bestaan of dienovereenkomstig worden omwikkeld.

## Stap 2: **gecachte modellen** – ophalen en weergeven

Nu de client klaar is, kunnen we hem vragen om alles wat lokaal bekend is op te sommen. Dit is de kern van onze **gecachte modellen**‑operatie.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Verwachte output** (met de dummy‑data uit stap 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Als de cache leeg is zie je simpelweg:

```
Cached models:
```

Die lege regel geeft aan dat er nog niets is opgeslagen—handig bij het schrijven van opruimscripts.

## Stap 3: **cache‑map tonen** – waar leeft de cache?

Het pad kennen is vaak al de helft van de strijd. Verschillende besturingssystemen plaatsen caches op verschillende standaardlocaties, en sommige SDK’s laten je dit overschrijven via omgevingsvariabelen. Het onderstaande fragment print het absolute pad zodat je er `cd` naartoe kunt doen of het kunt openen in een bestandsverkenner.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Typische output** op een Unix‑achtig systeem:

```
Cache directory: /home/youruser/.ai_cache
```

Op Windows zie je mogelijk iets als:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Nu weet je precies **hoe je de cache‑folder kunt bekijken** op elk platform.

## Stap 4: Alles samenvoegen – één uitvoerbaar script

Hieronder staat het volledige, kant‑klaar script dat de drie stappen combineert. Sla het op als `view_ai_cache.py` en voer `python view_ai_cache.py` uit.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Voer het uit en je ziet onmiddellijk zowel de lijst van gecachte modellen **als** de locatie van de cache‑map.

## Randgevallen & Variaties

| Situatie | Wat te doen |
|-----------|------------|
| **Lege cache** | Het script print “Cached models:” zonder entries. Je kunt een voorwaardelijke waarschuwing toevoegen: `if not models: print("⚠️ No models cached yet.")` |
| **Aangepast cache‑pad** | Geef een pad mee bij het construeren van de client: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. De aanroep `get_local_path()` zal dat aangepaste pad weergeven. |
| **Permissiefouten** | Op machines met beperkte rechten kan de client een `PermissionError` werpen. Plaats de initialisatie in een `try/except`‑blok en val terug op een map waar de gebruiker wel schrijfrechten heeft. |
| **Gebruik van echte SDK** | Vervang `YourAIClient` door de daadwerkelijke client‑klasse en zorg dat de methodenamen overeenkomen. Veel SDK’s bieden een `cache_dir`‑attribuut dat je direct kunt uitlezen. |

## Pro‑tips voor het beheren van je cache

- **Periodieke opruiming:** Als je vaak grote modellen downloadt, plan dan een cron‑job die `shutil.rmtree(ai.get_local_path())` aanroept nadat je hebt bevestigd dat je ze niet meer nodig hebt.  
- **Schijfruimte monitoren:** Gebruik `du -sh $(ai.get_local_path())` op Linux/macOS of `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` in PowerShell om de grootte in de gaten te houden.  
- **Geversioneerde mappen:** Sommige clients maken subfolders per modelversie. Wanneer je **gecachte modellen** **lijstet**, zie je elke versie als een aparte entry—gebruik dit om oudere revisies te verwijderen.  

## Visueel overzicht

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Alt‑tekst:* *list cached models – console‑output die namen van gecachte modellen en het pad van de cache‑directory toont.*

## Conclusie

We hebben alles behandeld wat je nodig hebt om **gecachte modellen** te **lijsten**, de **cache‑map te tonen**, en in het algemeen **hoe je de cache‑folder kunt bekijken** op elk systeem. Het korte script toont een complete, uitvoerbare oplossing, legt **waarom** elke stap belangrijk is, en biedt praktische tips voor gebruik in de echte wereld.  

Vervolgens kun je **hoe je de cache programmeermatig kunt wissen** verkennen, of deze aanroepen integreren in een grotere deployment‑pipeline die modelbeschikbaarheid valideert vóór het starten van inference‑taken. Hoe dan ook, je hebt nu de basis om lokale AI‑modelopslag met vertrouwen te beheren.

Heb je vragen over een specifieke AI‑SDK? Laat een reactie achter hieronder, en happy caching!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}