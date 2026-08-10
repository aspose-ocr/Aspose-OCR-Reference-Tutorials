---
category: general
date: 2026-06-22
description: Voer het model uit op de CPU en leer hoe je het GPU-geheugenverbruik
  kunt verminderen door GPU‑lagen te configureren in Aspose AI. Stapsgewijze handleiding
  met codevoorbeelden.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: nl
og_description: Voer het model uit op de CPU en verlaag het GPU‑geheugengebruik door
  GPU‑lagen te configureren. Volledige tutorial voor het opzetten van het Aspose AI‑model.
og_title: Model uitvoeren op CPU – GPU‑geheugengebruik verminderen
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Model op CPU uitvoeren – GPU‑geheugengebruik verminderen met Aspose AI
url: /nl/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Model uitvoeren op CPU – GPU‑geheugengebruik verminderen met Aspose AI

Heb je je ooit afgevraagd hoe je **model op CPU kunt uitvoeren** wanneer je server geen GPU beschikbaar heeft? Of misschien worstel je met out‑of‑memory‑fouten op een bescheiden GPU en moet je **GPU‑geheugengebruik verminderen** zonder te veel snelheid op te offeren. In deze gids lopen we precies dat door: een post‑processor koppelen, Aspose AI op de CPU initialiseren, en het aantal GPU‑lagen fijn afstellen om de geheugenvoetafdruk klein te houden.

We behandelen alles vanaf de allereerste regel code tot het valideren dat het model echt de configuratie gebruikt die je hebt opgegeven. Aan het einde kun je **model op CPU uitvoeren**, **GPU‑lagen beperken**, en **GPU‑lagen configureren** voor elke workload—geen magie, gewoon pure Python.

## Vereisten

- Python 3.8+ geïnstalleerd (de code gebruikt type‑hints maar werkt ook op oudere versies)
- `asposeai`‑pakket (installeren via `pip install asposeai`)
- Basiskennis van neurale‑netwerk inferentieconcepten (je hebt geen PhD nodig, alleen nieuwsgierigheid)
- Optioneel: een GPU‑enabled machine voor het testen van het contrast tussen CPU‑ en GPU‑runs

Als je een van deze mist, installeer dan eerst de SDK; de rest van de tutorial gaat ervan uit dat de import werkt.

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## Stap 1: Koppel de Spell‑Check Post‑Processor (Geen aangepaste instellingen nodig)

Voordat we zelfs maar aan CPU of GPU denken, laten we de spell‑check post‑processor koppelen die bij Aspose AI wordt geleverd. Het is een goede gewoonte om post‑processors vroeg te koppelen zodat ze deel uitmaken van elke inferentie‑aanroep.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Waarom dit belangrijk is:* Post‑processors draaien **na** dat het model ruwe tokens produceert. Door ze nu aan te sluiten, garandeer je dat elke tekst die je later genereert—of die nu op CPU of GPU draait—automatisch wordt opgeschoond. Het is een kleine stap die downstream‑bugs voorkomt.

## Stap 2: Model uitvoeren op CPU – Aspose AI initialiseren zonder GPU

Nu volgt de kern van de tutorial: Aspose AI vertellen om **model op CPU uit te voeren**. De SDK biedt `AsposeAIModelConfig`, waarbij de parameter `gpu_layers` bepaalt hoeveel lagen op de GPU blijven. Deze op `0` zetten dwingt het hele netwerk naar de CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Wat er onder de motorkap gebeurt:* Wanneer `gpu_layers=0`, wijst de runtime alle tensors toe in het host‑geheugen. Dit elimineert de noodzaak voor CUDA‑drivers, waardoor het script op vrijwel elke server kan draaien. Het nadeel is een lagere doorvoer, maar voor batch‑taken of low‑latency‑prototypes weegt de eenvoud vaak zwaarder dan ruwe snelheid.

## Stap 3: Beperk GPU‑lagen om GPU‑geheugengebruik te verminderen

Als je wel een GPU hebt maar die krap zit qua geheugen, kun je **GPU‑lagen beperken** in plaats van alles naar de CPU te verplaatsen. Door slechts een handvol vroege lagen op de GPU te houden, profiteer je nog steeds van hardware‑versnelling terwijl je het geheugenverbruik drastisch verlaagt.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Waarom het beperken van GPU‑lagen helpt:* Moderne transformer‑modellen wijzen het grootste deel van hun geheugen per laag toe. Het weglaten van zelfs een paar lagen van de GPU kan honderden megabytes vrijmaken. Deze aanpak is perfect voor “geheugen‑beperkte taken” waarbij je toch een snelheidsboost wilt voor de zwaarste berekeningen.

## Stap 4: GPU‑lagen configureren voor flexibel geheugengebruik

Soms heb je een meer granulaire aanpak nodig—misschien wil je **GPU‑lagen configureren** op basis van de specifieke taakgrootte. De SDK laat je het totale aantal lagen van het model lezen en een veilig aantal GPU‑lagen berekenen tijdens runtime.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Pro tip:* Wanneer je op een gedeelde server draait, vraag dan eerst het beschikbare GPU‑geheugen op (`torch.cuda.get_device_properties(0).total_memory`) en pas `desired_gpu_layers` dienovereenkomstig aan. Deze extra stap zorgt ervoor dat je de GPU nooit overbelast, wat anders OOM‑crashes zou veroorzaken.

## Stap 5: Verifieer de configuratie en test inferentie

Na het instellen van de configuratie is het verstandig om dubbel te controleren waar elke laag zich bevindt. Aspose AI biedt een diagnostische methode die een mapping van lagen naar apparaten retourneert.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Zodra je tevreden bent, voer een snelle inferentie uit om alles in actie te zien:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Als het script de verwachte tekst afdrukt en het plaatsingsrapport overeenkomt met je configuratie, heb je succesvol **model op CPU uitgevoerd**, **GPU‑geheugengebruik verminderd**, en **GPU‑lagen geconfigureerd** voor jouw scenario.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|---------|--------------|-----|
| `CUDA out of memory` error | Te veel GPU‑lagen | Verlaag `gpu_layers` of schakel over naar `gpu_layers=0` |
| No output from `ai.process` | Model niet geïnitialiseerd | Zorg ervoor dat `ai.initialize` wordt aangeroepen **na** het koppelen van post‑processors |
| Slow inference on GPU | Alle lagen nog steeds op CPU | Controleer dat `gpu_layers` > 0 is en dat de apparaat‑map GPU‑gebruik aangeeft |
| Unexpected spelling errors | Post‑processor niet gekoppeld | Roep `set_post_processor` aan vóór `initialize` |

## Bonus: Dynamisch schakelen tussen CPU en GPU

Omdat de SDK het model opnieuw initialiseert elke keer dat je `initialize` aanroept, kun je schakelen tussen CPU en GPU zonder je script opnieuw te starten.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Roep gewoon `switch_to_cpu()` aan wanneer je een low‑memory‑run nodig hebt, en `switch_to_gpu(12)` wanneer je klaar bent voor een snelheidsboost.

## Conclusie

We hebben een volledig, hands‑on voorbeeld doorlopen van hoe je **model op CPU kunt uitvoeren**, **GPU‑geheugengebruik kunt verminderen**, **GPU‑lagen kunt beperken**, en **GPU‑lagen kunt configureren** met Aspose AI. De stappen zijn eenvoudig:

1. Koppel eventuele vereiste post‑processors.  
2. Kies een configuratie (`gpu_layers=0` voor pure CPU, of een bescheiden aantal voor gemengde modus).  
3. Initialiseer het model met die configuratie.  
4. Verifieer de plaatsing en voer een test‑inferentie uit.  

Gewapend met deze technieken kun je je inferentie‑pijplijnen lichtgewicht houden, dure OOM‑crashes vermijden, en toch prestaties uit een bescheiden GPU halen wanneer die beschikbaar is. Vervolgens kun je batching‑strategieën, kwantisatie, of zelfs het off‑loaden van delen van het model naar de CPU verkennen terwijl je de attention‑heads op de GPU houdt—elk van deze onderwerpen bouwt direct voort op de **GPU‑lagen configureren** basis die je zojuist hebt beheerst.

Heb je vragen over een specifieke modelarchitectuur of heb je hulp nodig bij het afstemmen van het aantal lagen voor een

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose OCR Tutorial – Optische tekenherkenning](/ocr/english/)
- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hoe OCR‑tekst van afbeelding met taal te gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}