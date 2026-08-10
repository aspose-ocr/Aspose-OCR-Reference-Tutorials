---
category: general
date: 2026-01-12
description: Lär dig hur du visar information från AsposeAI genom att lista lokala
  modeller, visa modellnamn, storlek och senast använda tidsstämpel i ett tydligt
  Python‑exempel.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: sv
og_description: 'Hur man visar information från AsposeAI: lista lokala modeller, visa
  modellnamn, storlek och senast använda tidsstämpel med en komplett Python‑genomgång.'
og_title: Hur man visar info – Lista lokala modeller, namn, storlek, senast använda
tags:
- AsposeAI
- Python
- Model Management
title: Hur man visar info – Lista lokala modeller, namn, storlek, senast använda
url: /sv/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man visar info – Lista lokala modeller, namn, storlek, senast använda

Har du någonsin undrat **hur man visar info** från din AsposeAI‑installation utan att gräva igenom loggar eller UI? Du är inte ensam. I många data‑science‑pipelines är det första du behöver en snabb överblick över vilka modeller som finns på din maskin, vad de heter, hur stora de är och när du senast rörde dem.

Det är exakt vad vi kommer att gå igenom: ett kortfattat, end‑to‑end Python‑snutt som **listar lokala modeller**, sedan **visar modellnamn**, **visar modellstorlek** och **visar senast använda** tidsstämplar. Inga externa bibliotek, ingen gömd magi—bara AsposeAI‑klienten du redan har.

I slutet av den här handledningen kan du klistra in koden i vilket skript som helst, köra det och omedelbart få en prydlig tabell över dina lokalt cachade modeller. Det är perfekt för att kontrollera miljöer, bygga hälsodashboards eller helt enkelt tillfredsställa nyfikenheten kring vad som gömmer sig på disken.

## Förutsättningar

- Python 3.8 eller nyare (exemplet använder f‑strings, så 3.6+ är ett måste)
- `asposeai`‑paketet installerat (`pip install asposeai`)
- En fungerande AsposeAI‑licens eller provnyckel (klienten hämtar autentiseringsuppgifter från miljövariabler eller en konfigurationsfil)

Om du redan har kryssat i dessa, toppen—låt oss dyka in.

## Steg 1: Hur man visar info – Initiera AsposeAI‑klienten

Innan vi kan **lista lokala modeller** behöver vi ett klientobjekt som kommunicerar med AsposeAI‑runtime. Detta steg är grunden; utan det skulle resten av koden ge ett `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Varför detta är viktigt*: Initiering av klienten etablerar en session med den lokala inferensmotorn, laddar eventuella nödvändiga native‑bibliotek. Den validerar också att din licens är aktiv, vilket förhindrar kryptiska fel senare när du försöker fråga modeller.

> **Proffstips**: Om du kör detta på en CI‑server, sätt `ASPOSEAI_LICENSE` i miljön så att klienten kan starta utan interaktiva frågor.

## Steg 2: Lista lokala modeller – Hämta de tillgängliga modellerna

Nu när klienten är klar kan vi **lista lokala modeller**. Metoden `list_local()` returnerar en samling objekt, där varje objekt har egenskaper som `name`, `size_mb` och `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Vad som händer under huven*: `list_local()` skannar katalogen där AsposeAI cachar modellfiler (`~/.asposeai/models` som standard) och bygger lätta metadata‑objekt. Detta är snabbt eftersom det inte laddar modellvikterna—det läser bara ett litet JSON‑manifest.

Om du någonsin undrar om en viss modell redan är cachad, är detta anrop det snabbaste sättet att bekräfta det.

## Steg 3: Visa modellnamn, visa modellstorlek och visa senast använda

Med modellerna i handen kan vi äntligen **visa info** genom att iterera över samlingen och skriva ut varje attribut. Här **visar vi modellnamn**, **visar modellstorlek** och **visar senast använda** i en prydlig rad.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Förväntad output** (dina tidsstämplar kommer att skilja sig):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Varför vi formaterar så här*: Bindestrecket (`–`) separerar fält för läsbarhet, och rubrikraden gör konsolutdata lätt att skanna. Om du senare behöver ett maskinläsbart format (CSV, JSON) kan du enkelt byta `print`‑anropet mot ett `writer.writerow` eller `json.dump`.

### Hantera kantfall

- **Inga modeller cachade** – `list_local()` returnerar en tom lista. Loopen hoppar helt enkelt över, så du får bara rubriken. Du kanske vill lägga till en skyddsmekanism:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Saknade attribut** – I sällsynta fall kan ett manifest vara korrupt. Att komma åt `model_info.last_used` kan ge ett `AttributeError`. Omslut utskriften i ett `try/except` om du förväntar dig sådana problem.

- **Stora modellkataloger** – Om du har hundratals modeller, överväg att paginera utskriften eller skriva till en fil istället för att skriva ut i konsolen.

## Visuell sammanfattning (valfritt)

Om du föredrar en snabb visuell ledtråd visar diagrammet nedan flödet från klientinitiering till slutlig visning.  

![Diagram som visar hur man visar info från AsposeAI‑klienten](/images/how-to-display-info.png "diagram för hur man visar info")

*Alt‑text*: **how to display info** – schematisk bild av AsposeAI‑klientinitiering, modelluppräkning och informationsvisning.

## Fullt fungerande skript

När vi sätter ihop allt, här är det kompletta, färdiga skriptet:

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

Spara detta som `list_models.py`, gör det körbart (`chmod +x list_models.py`), och kör:

```bash
./list_models.py
```

Du kommer att se den prydliga listan som demonstrerades tidigare.

## Slutsats

Vi har gått igenom **hur man visar info** från AsposeAI genom att **lista lokala modeller**, sedan **visa modellnamn**, **visa modellstorlek** och **visa senast använda** tidsstämplar. Metoden är lättviktig, kräver bara standardpaketet `asposeai` och kan slängas in i vilken automatiseringspipeline eller felsökningssession som helst.

Härifrån kan du:

- Exportera utskriften till CSV för kalkylbladsanalys (`csv`‑modulen).
- Skicka tidsstämplarna till en övervakningsdashboard för att varna om föråldrade modeller.
- Kombinera detta skript med `aspose_ai.download()` för att automatiskt uppdatera modeller som inte har använts på ett tag.

Kom ihåg att tydlig insyn i ditt modellinventarium sparar tid, minskar lagringsbloat och håller dina AI‑tjänster igång smidigt. Prova skriptet, justera formateringen efter din smak, och låt det bli ett grundläggande verktyg i din verktygslåda.

Lycka till med kodningen, och må dina modeller alltid vara färska!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}