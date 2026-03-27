---
category: general
date: 2026-01-12
description: Leer hoe je informatie van AsposeAI kunt weergeven door lokale modellen
  te vermelden, waarbij je de modelnaam, grootte en laatst‑gebruik tijdstempel toont
  in een duidelijk Python‑voorbeeld.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: nl
og_description: 'Hoe informatie van AsposeAI weer te geven: lijst lokale modellen,
  toon modelnaam, grootte en laatste gebruikstijdstempel met een volledige Python‑handleiding.'
og_title: Hoe informatie weergeven – Lijst lokale modellen, naam, grootte, laatst
  gebruikt
tags:
- AsposeAI
- Python
- Model Management
title: Hoe informatie weergeven – Lijst lokale modellen, naam, grootte, laatst gebruikt
url: /nl/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Info Weergeven – Lijst Lokale Modellen, Naam, Grootte, Laatst Gebruikt

Heb je je ooit afgevraagd **hoe je info weergeeft** vanuit je AsposeAI‑installatie zonder door logbestanden of de UI te hoeven graven? Je bent niet de enige. In veel data‑science‑pijplijnen is het eerste wat je nodig hebt een snelle blik op welke modellen op je machine staan, hoe ze heten, hoe groot ze zijn en wanneer je ze voor het laatst hebt aangeraakt.

Dat is precies wat we gaan behandelen: een beknopte, end‑to‑end Python‑snippet die **lokale modellen opsomt**, vervolgens **modelnaam weergeeft**, **modelgrootte toont**, en **laatst gebruikte** tijdstempels laat zien. Geen externe bibliotheken, geen verborgen magie—alleen de AsposeAI‑client die je al hebt.

Aan het einde van deze tutorial kun je de code in elk script plaatsen, uitvoeren, en direct een nette tabel krijgen van je lokaal gecachte modellen. Het is perfect voor het controleren van omgevingen, het bouwen van health‑dashboards, of gewoon om een nieuwsgierigheid te stillen over wat er op de schijf schuilt.

## Vereisten

- Python 3.8 of nieuwer (het voorbeeld gebruikt f‑strings, dus 3.6+ is vereist)
- `asposeai`‑pakket geïnstalleerd (`pip install asposeai`)
- Een werkende AsposeAI‑licentie of proef‑sleutel (de client haalt inloggegevens op uit omgevingsvariabelen of een configuratiebestand)

Als je die punten al hebt afgevinkt, prima—laten we erin duiken.

## Stap 1: Hoe Info Weergeven – Initialiseert de AsposeAI‑Client

Voordat we **lokale modellen kunnen opsommen**, hebben we een client‑object nodig dat met de AsposeAI‑runtime communiceert. Deze stap is de basis; zonder deze zou de rest van de code een `NameError` veroorzaken.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Waarom dit belangrijk is*: Het initialiseren van de client legt een sessie vast met de lokale inference‑engine, waarbij eventuele benodigde native libraries worden geladen. Het valideert ook dat je licentie actief is, waardoor cryptische fouten later bij het opvragen van modellen worden voorkomen.

> **Pro tip**: Als je dit op een CI‑server uitvoert, stel `ASPOSEAI_LICENSE` in de omgeving in zodat de client kan starten zonder interactieve prompts.

## Stap 2: Lijst Lokale Modellen – Haal de Beschikbare Modellen Op

Nu de client klaar is, kunnen we **lokale modellen opsommen**. De `list_local()`‑methode retourneert een collectie objecten, elk met eigenschappen zoals `name`, `size_mb` en `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Wat er onder de motorkap gebeurt*: `list_local()` scant de map waar AsposeAI modelbestanden cachet (`~/.asposeai/models` standaard) en bouwt lichtgewicht metadata‑objecten. Dit is snel omdat het de modelgewichten niet laadt—het leest alleen een klein JSON‑manifest.

Als je ooit wilt weten of een bepaald model al is gecached, is deze oproep de snelste manier om dat te bevestigen.

## Stap 3: Modelnaam Weergeven, Modelgrootte Tonen, en Laatst Gebruikt Tonen

Met de modellen in de hand, **weergeven we eindelijk info** door over de collectie te itereren en elk attribuut af te drukken. Hier **geeft we de modelnaam weer**, **tonen we de modelgrootte**, en **tonen we de laatst gebruikte** tijdstempel, allemaal in één nette regel.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Verwachte output** (je tijdstempels zullen verschillen):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Waarom we het op deze manier formatteren*: Het streepje (`–`) scheidt velden voor leesbaarheid, en de kopregel maakt de console‑output scan‑vriendelijk. Als je later een machine‑leesbaar formaat nodig hebt (CSV, JSON), kun je de `print`‑aanroep eenvoudig vervangen door een `writer.writerow` of `json.dump`.

### Randgevallen Afhandelen

- **Geen modellen gecached** – `list_local()` retourneert een lege lijst. De lus zal simpelweg overslaan, waardoor je alleen de header overhoudt. Je wilt misschien een guard toevoegen:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Ontbrekende attributen** – In zeldzame gevallen kan een manifest corrupt zijn. Toegang tot `model_info.last_used` kan een `AttributeError` veroorzaken. Omring de print met een `try/except` als je dergelijke problemen verwacht.

- **Grote modelmappen** – Als je honderden modellen hebt, overweeg dan om de output te pagineren of naar een bestand te schrijven in plaats van naar de console te printen.

## Visuele Samenvatting (Optioneel)

Als je een snelle visuele hint prefereert, illustreert het diagram hieronder de stroom van client‑initialisatie tot de uiteindelijke weergave.  

![Diagram dat laat zien hoe je info weergeeft vanuit AsposeAI client](/images/how-to-display-info.png "diagram hoe info weergeven")

*Alt‑tekst*: **hoe info weergeven** – schema van AsposeAI clientinitialisatie, modeloplist, en info‑weergave.

## Volledig Werkend Script

Alles samenvoegend, hier is het volledige, kant‑klaar script:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Sla dit op als `list_models.py`, maak het uitvoerbaar (`chmod +x list_models.py`), en voer het uit:

```bash
./list_models.py
```

Je zult de nette lijst zien die eerder werd getoond.

## Conclusie

We hebben stap voor stap **hoe je info weergeeft** vanuit AsposeAI behandeld door **lokale modellen op te sommen**, vervolgens **modelnaam weer te geven**, **modelgrootte te tonen**, en **laatst gebruikte** tijdstempels te laten zien. De aanpak is lichtgewicht, vereist alleen het standaard `asposeai`‑pakket, en kan in elke automatiserings‑pipeline of debug‑sessie worden geplaatst.

Van hieruit kun je:

- Export de output naar CSV voor spreadsheet‑analyse (`csv`‑module).
- Stuur de tijdstempels naar een monitoring‑dashboard om te waarschuwen voor verouderde modellen.
- Combineer dit script met `aspose_ai.download()` om modellen die een tijdje niet zijn gebruikt automatisch te vernieuwen.

Onthoud dat duidelijke zichtbaarheid op je modelinventaris tijd bespaart, opslagopbouw vermindert, en je AI‑services soepel laat draaien. Probeer het script, pas de opmaak naar wens aan, en laat het een vaste waarde in je gereedschapskist worden.

Veel plezier met coderen, en moge je modellen altijd vers blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}