---
category: general
date: 2026-03-28
description: Hur man OCR:ar ROI i Python – Lär dig att ställa in förbehandlingsalternativ
  för exakt textutvinning från specifika bildregioner.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: sv
og_description: Hur man OCR:ar ROI i Python – Denna guide visar hur man ställer in
  förbehandling för pålitlig textutvinning från definierade bildregioner.
og_title: Hur man OCR:ar ROI i Python – Hur man ställer in förbehandling
tags:
- OCR
- Python
- Aspose
title: Hur man OCR:ar ROI i Python – Hur man ställer in förbehandling
url: /sv/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man OCR ROI i Python – Hur man ställer in förbehandling

Har du någonsin undrat **hur man OCR ROI** i en brusig fakturabild utan att ladda hela sidan i minnet? Du är inte ensam. I många verkliga projekt behöver vi bara ett fåtal fält—kundnamn, adress, totalsummor—så att skanna hela dokumentet är överdrivet.  

Den goda nyheten? Med Aspose OCR kan du tala om för motorn exakt **var den ska leta** och till och med be den att rensa upp bilden först. I den här handledningen går vi igenom **hur man ställer in förbehandling**-alternativ, definierar Regions of Interest (ROIs) och extraherar ren text på bara några rader Python.

I slutet av den här guiden har du ett färdigt skript som extraherar specifika block från vilken faktura, kvitto eller formulär som helst. Inga extra verktyg behövs, bara Aspose OCR och lite Python‑logik.

---

## Vad du behöver

- **Python 3.8+** (koden fungerar på alla nyare versioner)  
- **Aspose OCR for Python via .NET** – installera med `pip install aspose-ocr`  
- En exempelbild (t.ex. `invoice.png`) placerad i en mapp du kan referera till  
- Grundläggande kunskap om Python‑funktioner och objekt‑orienterad syntax  

Om du redan har detta, bra—låt oss hoppa rakt in i koden.

---

![hur man OCR ROI-diagram som visar ROI-rutor på en fakturabild](ocr-roi.png "Exempel på hur man OCR ROI")

*Alt text: hur man OCR ROI-diagram som visar ROI-rutor på en fakturabild*

---

## Steg 1 – Initiera OCR‑motorn (Hur man OCR ROI)

Innan vi kan tala om för motorn *var* den ska leta, behöver vi en instans av OCR‑processorn. Detta objekt innehåller all konfiguration och kör igenkänningspasset.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Varför detta är viktigt*: `OcrEngine`‑klassen abstraherar det tunga arbetet (teckensnittsdetektion, layout‑analys, etc.). Genom att skapa en enda motor undviker du att återinitiera tunga resurser för varje bild, vilket håller prestandan snabb.

---

## Steg 2 – Ladda din källbild (Hur man OCR ROI)

Aspose Storage gör det enkelt att ladda bilder. Peka den på filsökvägen, så får du ett `Image`‑objekt redo för bearbetning.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tips*: Om du arbetar med strömmar (t.ex. bilder uppladdade via ett webb‑API), kan du skicka ett `BytesIO`‑objekt till `Image.load` istället för en filsökväg.

---

## Steg 3 – Definiera Regions of Interest (ROIs)

Nu svarar vi på kärnfrågan **hur man OCR ROI**: vi talar om för motorn de exakta rektanglarna som innehåller den data vi är intresserade av. Varje ROI definieras av dess övre‑vänstra hörn (`x`, `y`) och dess storlek (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Varför använda ROIs?*  
- **Hastighet** – Motorn hoppar över irrelevanta delar av bilden.  
- **Noggrannhet** – Genom att fokusera på ett litet område kan brus på andra ställen inte förvirra igenkännaren.  
- **Flexibilitet** – Du kan lägga till så många ROIs som behövs; motorn returnerar en lista med resultat i samma ordning.

---

## Steg 4 – Hur man ställer in förbehandling för bättre OCR‑noggrannhet

Bilder direkt från skannrar eller telefoner lider ofta av snedvridning, låg kontrast eller ojämn belysning. Aspose OCR erbjuder ett `PreprocessingOptions`‑objekt som låter dig aktivera vanliga korrigeringar innan igenkänning körs.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Hur detta hjälper*:  
- **Deskew** tar bort den lutning som gör teckenformer otydliga.  
- **Binarize** minskar färgbrus och ger OCR‑motorn en ren binär bild.  
- **Contrast** förstärker svaga streck, vilket är särskilt användbart för blekta kvitton.

Du kan experimentera med dessa flaggor—stäng av en och se om utdata förändras. Det är andan i **hur man ställer in förbehandling** på ett effektivt sätt.

---

## Steg 5 – Utför OCR endast inom de definierade ROIs

Med motorn, bilden, ROIs och förbehandling redo är det dags att anropa `recognize`. Metoden returnerar ett `OcrResult`‑objekt som innehåller en `regions`‑samling—varje post matchar den ROI‑ordning vi angav.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Bakom kulisserna*: Motorn beskär varje ROI, tillämpar förbehandlingspipeline och kör igenkänningsmodellen på det rengjorda utdraget. Eftersom vi skickade en lista behåller resultatet samma ordning, vilket gör efterbehandling enkel.

---

## Steg 6 – Läs och använd den extraherade texten (Hur man OCR ROI)

Till sist, iterera över `regions`‑listan och skriv ut—eller lagra—de igenkända strängarna. `Region`‑objektet exponerar en `text`‑egenskap som innehåller Unicode‑resultatet.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Förväntad utdata (exempel)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Om texten ser förvrängd ut, gå tillbaka till **hur man ställer in förbehandling**: kanske öka `contrast` eller inaktivera `binarize` för färgade logotyper.

---

## Vanliga fallgropar och pro‑tips

| Problem | Varför det händer | Lösning (Hur man ställer in förbehandling) |
|-------|----------------|--------------------------------|
| Snedvriden text visas som nonsens | `deskew` inaktiverad eller bilden för roterad | Aktivera `preprocessing_options.deskew = True` |
| Siffror blir punkter eller spretiga märken | Låg kontrast eller aggressiv binarisering | Sänk `contrast` (t.ex. `1.2`) eller sätt `binarize = False` |
| ROI‑koordinater är fel med några pixlar | Olika DPI eller skanningsskalning | Använd ett verktyg (t.ex. Paint.NET) för att mäta exakta pixelpositioner, eller lägg till ett litet marginal (`+5` pixlar) till varje ROI |
| Tomt resultat för en region | ROI utanför bildens gränser | Verifiera bildens dimensioner: `source_image.width`, `source_image.height` |

---

## Utöka lösningen (Hur man OCR ROI i olika scenarier)

- **Dynamiska ROIs**: Om dina fakturor har variabla layouter kan du först köra en snabb helsidig OCR för att hitta nyckelord (“Customer:”, “Address:”) och sedan beräkna ROIs i farten.  
- **Batch‑bearbetning**: Packa in stegen ovan i en funktion och loopa över en mapp med bilder. Kom ihåg att återanvända samma `ocr_engine`‑instans för att hålla minnesanvändningen låg.  
- **Export till JSON**: Istället för att skriva ut, bygg en dictionary och dumpa den med `json.dumps`; detta gör efterföljande integration (t.ex. mata in i ett ERP‑system) trivial.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Slutsats

Du har nu ett komplett, körbart exempel som visar **hur man OCR ROI** i Python samtidigt som du behärskar **hur man ställer in förbehandling** för optimal noggrannhet. Genom att begränsa motorn till de exakta rektanglarna du är intresserad av och rensa bilden i förväg får du snabbare, renare resultat—perfekt för fakturautomatisering, formulärdigitalisering eller vilket scenario som helst där bara en del av sidan är relevant.

Redo för nästa steg? Prova att justera ROI‑koordinaterna för en annan dokumenttyp, eller experimentera med ytterligare förbehandlingsflaggor som `sharpen` eller `noise_reduction`. Flexibiliteten i Aspose OCR innebär att du kan anpassa pipeline:n till praktiskt taget vilken bildkvalitet som helst.

Om du stöter på problem, kontrollera konsolutdata för tomma regioner och gå tillbaka till förbehandlingsinställningarna. Lycka till med kodningen, och må din OCR alltid vara exakt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}