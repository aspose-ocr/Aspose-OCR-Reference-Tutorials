---
category: general
date: 2026-04-26
description: Maskera kreditkortsnummer snabbt med AsposeAI OCR‑efterbehandling. Lär
  dig PCI‑efterlevnad, maskering med reguljära uttryck och datarengöring i en steg‑för‑steg‑handledning.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: sv
og_description: Maskera kreditkortsnummer i OCR‑resultat med AsposeAI. Denna handledning
  täcker PCI‑efterlevnad, maskering med reguljära uttryck och datarengöring.
og_title: Maskera kreditkortsnummer – Fullständig guide för Python OCR‑efterbehandling
tags:
- OCR
- Python
- security
title: Maskera kreditkortsnummer i OCR‑utdata – Komplett Python‑guide
url: /sv/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maskera kreditkortsnummer – Komplett Python‑guide

Har du någonsin behövt **maskera kreditkortsnummer** i text som kommer direkt från en OCR‑motor? Du är inte ensam. I reglerade branscher kan exponering av ett fullt PAN (Primary Account Number) leda till problem med PCI‑revisorer. Den goda nyheten? Med några rader Python och AsposeAI:s efterbehandlings‑hook kan du automatiskt dölja de åttonde siffrorna i mitten och hålla dig på den säkra sidan.

I den här handledningen går vi igenom ett verkligt scenario: köra OCR på en kvittobild och sedan tillämpa en anpassad **OCR post‑processing**‑funktion som sanerar all PCI‑data. I slutet har du ett återanvändbart kodsnutt som du kan lägga in i vilket AsposeAI‑arbetsflöde som helst, samt ett antal praktiska tips för att hantera kantfall och skala lösningen.

## Vad du kommer att lära dig

- Hur man registrerar en anpassad post‑processor med **AsposeAI**.
- Varför en **regular expression masking**‑metod är både snabb och pålitlig.
- Grunderna i **PCI compliance** relaterat till datasanering.
- Sätt att utöka mönstret för flera kortformat eller internationella nummer.
- Förväntad output och hur man verifierar att maskeringen fungerade.

> **Förutsättningar** – Du bör ha en fungerande Python 3‑miljö, Aspose.AI för OCR‑paketet installerat (`pip install aspose-ocr`), och en exempelbild (t.ex. `receipt.png`) som innehåller ett kreditkortsnummer. Inga andra externa tjänster krävs.

---

## Steg 1: Definiera en post‑processor som maskerar kreditkortsnummer

Kärnan i lösningen finns i en liten funktion som tar emot OCR‑resultatet, kör en **regular expression masking**‑rutin och returnerar den sanerade texten.

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

**Varför detta fungerar:**  
- Regex‑uttrycket `(\d{4})\d{8}(\d{4})` matchar exakt 16 på varandra följande siffror, det vanliga formatet för Visa, MasterCard och många andra.  
- Genom att fånga de första och sista fyra siffrorna (`\1` och `\2`) bevarar vi tillräckligt med information för felsökning samtidigt som vi följer **PCI compliance**‑reglerna som förbjuder lagring av hela PAN.  
- Ersättningen `\1****\2` döljer de känsliga åtta siffrorna i mitten och omvandlar `1234567812345678` till `1234****5678`.

> **Proffstips:** Om du behöver stödja 15‑siffriga American Express‑nummer, lägg till ett andra mönster som `r'(\d{4})\d{6}(\d{5})'` och kör båda ersättningarna sekventiellt.

---

## Steg 2: Initiera AsposeAI‑motorn

Innan vi kan fästa vår post‑processor behöver vi en instans av OCR‑motorn. AsposeAI paketera OCR‑modellen och ett enkelt API för anpassad bearbetning.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Varför initiera här?**  
Att skapa `AsposeAI`‑objektet en gång och återanvända det över flera bilder minskar overhead. Motorn cachar också språkmodeller, vilket snabbar upp efterföljande anrop—praktiskt när du skannar batcher av kvitton.

---

## Steg 3: Registrera den anpassade maskeringsfunktionen

AsposeAI exponerar en `set_post_processor`‑metod som låter dig ansluta vilken callable som helst. Vi skickar vår `mask_pci`‑funktion tillsammans med en valfri inställnings‑dictionary (tom för tillfället).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Vad händer bakom kulisserna?**  
När du senare anropar `run_postprocessor` kommer AsposeAI att skicka det råa OCR‑resultatet till `mask_pci`. Funktionen får ett lättviktigt objekt (`data`) som innehåller den igenkända texten, och du returnerar en ny sträng. Denna design håller kärn‑OCR‑delen intakt samtidigt som du kan verkställa **data sanitization**‑policyer på ett ställe.

---

## Steg 4: Kör OCR på kvittobilden

Nu när motorn vet hur den ska rensa outputen, matar vi den med en bild. För denna handledning antar vi att du redan har ett `engine`‑objekt konfigurerat med rätt språk‑ och upplösningsinställningar.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tips:** Om du inte har ett förkonfigurerat objekt kan du skapa ett med:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image`‑anropet returnerar ett objekt vars `text`‑attribut innehåller den råa, omaskerade strängen.

---

## Steg 5: Använd den registrerade post‑processorn

Med den råa OCR‑datan i handen överlämnar vi den till AI‑instansen. Motorn kör automatiskt `mask_pci`‑funktionen som vi registrerade tidigare.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Varför använda `run_postprocessor` istället för att anropa funktionen manuellt?**  
Att göra så håller arbetsflödet konsekvent, särskilt när du har flera post‑processorer (t.ex. stavningskontroll, språkdetection). AsposeAI köar dem i den ordning du registrerar dem, vilket garanterar deterministisk output.

---

## Steg 6: Verifiera den sanerade outputen

Till sist, låt oss skriva ut den sanerade texten och bekräfta att eventuella kreditkortsnummer är korrekt maskerade.

```python
print(final_result.text)
```

**Förväntad output** (excerpt):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Om kvittot inte innehöll något kortnummer förblir texten oförändrad—inget att maskera, inget att oroa sig för.

---

## Hantera kantfall och vanliga variationer

### Flera kortnummer i ett dokument
Om ett kvitto innehåller mer än ett PAN (t.ex. ett lojalitetskort plus ett betalkort) kör regexen globalt och maskerar alla träffar automatiskt. Ingen extra kod behövs.

### Icke‑standardformat
Ibland infogar OCR mellanslag eller bindestreck (`1234 5678 1234 5678` eller `1234-5678-1234-5678`). Utöka mönstret för att ignorera dessa tecken:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Den tillagda `[ -]?` tolererar valfria mellanslag eller bindestreck mellan siffrablok.

### Internationella kort
För 19‑siffriga PAN‑nummer som används i vissa regioner kan du bredda mönstret:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Kom bara ihåg att **PCI compliance** fortfarande kräver maskering av de mellersta siffrorna, oavsett längd.

### Loggning av maskerade värden (valfritt)
Om du behöver revisionsspår, skicka en flagga via `custom_settings` och justera funktionen:

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

Registrera sedan med:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Fullt fungerande exempel (klar att kopiera och klistra in)

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

Att köra detta skript på ett kvitto som innehåller `4111111111111111` kommer att producera:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Det är hela pipeline‑processen—från rå OCR till **data sanitization**—insvept i några rena rader Python.

---

## Slutsats

Vi har just visat hur du **maskerar kreditkortsnummer** i OCR‑resultat med AsposeAI:s efterbehandlings‑hook, en kortfattad regular‑expression‑rutin och ett antal bästa‑praxis‑tips för **PCI compliance**. Lösningen är helt självständig, fungerar med vilken bild som helst som OCR‑motorn kan läsa, och kan utökas för att täcka mer komplexa kortformat eller loggningskrav.

Redo för nästa steg? Prova att kombinera denna mask med en **databasinsättnings**‑rutin som bara lagrar de sista fyra siffrorna för referens, eller integrera en **batch‑processor** som skannar en hel mapp med kvitton över natten. Du kan också utforska andra **OCR post‑processing**‑uppgifter som adressstandardisering eller språkdetection—varje följer samma mönster som vi använde här.

Har du frågor om kantfall, prestanda eller hur du anpassar koden för ett annat OCR‑bibliotek? Lämna en kommentar nedan, så fortsätter vi samtalet. Lycka till med kodandet, och håll dig säker!  

![Diagram som visar hur maskering av kreditkortsnummer fungerar i en OCR‑pipeline](https://example.com/images/ocr-mask-flow.png "Diagram av OCR efterbehandlings‑maskeringsflöde")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}