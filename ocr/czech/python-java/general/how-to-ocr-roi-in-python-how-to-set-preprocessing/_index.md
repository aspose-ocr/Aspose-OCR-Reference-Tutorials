---
category: general
date: 2026-03-28
description: Jak provést OCR ROI v Pythonu – naučte se nastavit možnosti předzpracování
  pro přesné získávání textu z konkrétních oblastí obrázku.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: cs
og_description: Jak provést OCR ROI v Pythonu – Tento průvodce ukazuje, jak nastavit
  předzpracování pro spolehlivé získávání textu z definovaných oblastí obrazu.
og_title: Jak provést OCR ROI v Pythonu – Jak nastavit předzpracování
tags:
- OCR
- Python
- Aspose
title: Jak provést OCR ROI v Pythonu – Jak nastavit předzpracování
url: /cs/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR ROI v Pythonu – Jak nastavit předzpracování

Už jste se někdy zamýšleli **jak provést OCR ROI** v špinavém obrázku faktury, aniž byste načítali celou stránku do paměti? Nejste v tom sami. V mnoha reálných projektech potřebujeme jen několik polí – jméno zákazníka, adresu, součty – takže skenování celého dokumentu je zbytečné.  

Dobrá zpráva? S Aspose OCR můžete motoru přesně říct, **kde hledat**, a dokonce mu říct, aby nejprve obrázek vyčistil. V tomto tutoriálu si projdeme **jak nastavit předzpracování**, definovat oblasti zájmu (ROIs) a získat čistý text během několika řádků Pythonu.

Na konci tohoto průvodce budete mít připravený skript, který vytáhne konkrétní bloky z libovolné faktury, účtenky nebo formuláře. Nepotřebujete žádné další nástroje, jen Aspose OCR a trochu logiky v Pythonu.

---

## Co budete potřebovat

- **Python 3.8+** (kód funguje na jakékoli nedávné verzi)  
- **Aspose OCR for Python via .NET** – nainstalujte pomocí `pip install aspose-ocr`  
- Ukázkový obrázek (např. `invoice.png`) umístěný ve složce, na kterou můžete odkazovat  
- Základní znalost funkcí v Pythonu a objektově orientované syntaxe  

Pokud už to máte, skvělé — přejděme rovnou k óde.

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Alt text: diagram ukazující OCR ROI s boxy ROI na obrázku faktury*

---

## Krok 1 – Inicializace OCR enginu (Jak provést OCR ROI)

Než můžeme motoru říct, *kde* hledat, potřebujeme instanci OCR procesoru. Tento objekt obsahuje veškeré nastavení a spouští rozpoznávací průchod.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Proč je to důležité*: Třída `OcrEngine` abstrahuje těžkou práci (detekce fontů, analýza rozvržení atd.). Vytvořením jediného enginu se vyhnete opakovanému inicializování náročných zdrojů pro každý obrázek, což udržuje výkon svižný.

---

## Krok 2 – Načtení zdrojového obrázku (Jak provést OCR ROI)

Aspose Storage usnadňuje načítání obrázků. Ukážete mu cestu k souboru a získáte objekt `Image` připravený ke zpracování.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tip*: Pokud pracujete se streamy (např. obrázky nahrané přes webové API), můžete předat objekt `BytesIO` metodě `Image.load` místo cesty k souboru.

---

## Krok 3 – Definování oblastí zájmu (ROIs)

Nyní odpovídáme na hlavní otázku **jak provést OCR ROI**: řekneme motoru přesné obdélníky, které obsahují data, o která nám jde. Každá ROI je definována levým horním rohem (`x`, `y`) a velikostí (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Proč používat ROIs?*  
- **Rychlost** – Engine přeskočí irelevantní části obrázku.  
- **Přesnost** – Zaměřením na malou oblast se šum jinde nemůže zaměnit rozpoznávač.  
- **Flexibilita** – Můžete přidat libovolný počet ROI; engine vrátí seznam výsledků ve stejném pořadí.

---

## Krok 4 – Jak nastavit předzpracování pro lepší přesnost OCR

Obrázky přímo ze skenerů nebo telefonů často trpí zkosením, nízkým kontrastem nebo nerovnoměrným osvětlením. Aspose OCR nabízí objekt `PreprocessingOptions`, který vám umožní povolit běžné opravy před spuštěním rozpoznávání.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Jak to pomáhá*:  
- **Deskew** odstraňuje sklon, který činí tvary znaků nejasnými.  
- **Binarize** snižuje barevný šum a poskytuje OCR enginu čistý binární obrázek.  
- **Contrast** zesiluje slabé tahy, což je zvláště užitečné u vybledlých účtenek.

Můžete experimentovat s těmito příznaky — vypněte jeden a podívejte se, zda se výstup změní. To je podstata **jak efektivně nastavit předzpracování**.

---

## Krok 5 – Proveďte OCR pouze v rámci definovaných ROI

S připraveným enginem, obrázkem, ROI a předzpracováním je čas zavolat `recognize`. Metoda vrací objekt `OcrResult`, který obsahuje kolekci `regions` — každý záznam odpovídá pořadí ROI, které jsme zadali.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Za scénou*: Engine ořízne každou ROI, aplikuje pipeline předzpracování a spustí model rozpoznávání na vyčištěném úryvku. Protože jsme předali seznam, výsledek zachovává stejné pořadí, což usnadňuje následné zpracování.

---

## Krok 6 – Přečtěte a použijte extrahovaný text (Jak provést OCR ROI)

Nakonec projděte seznam `regions` a vytiskněte — nebo uložte — rozpoznané řetězce. Objekt `Region` poskytuje vlastnost `text`, která obsahuje výsledek v Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Očekávaný výstup (příklad)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Pokud text vypadá poškozeně, vraťte se k **jak nastavit předzpracování**: možná zvýšte `contrast` nebo vypněte `binarize` pro barevná loga.

---

## Časté úskalí a profesionální tipy

| Problém | Proč se to děje | Oprava (Jak nastavit předzpracování) |
|-------|----------------|--------------------------------|
| Zkosený text se zobrazuje jako nesmysl | `deskew` vypnutý nebo obrázek příliš natočený | Povolte `preprocessing_options.deskew = True` |
| Čísla se mění na tečky nebo odlehlé značky | Nízký kontrast nebo agresivní binarizace | Snižte `contrast` (např. `1.2`) nebo nastavte `binarize = False` |
| Souřadnice ROI jsou posunuty o několik pixelů | Různé DPI nebo měřítko skeneru | Použijte nástroj (např. Paint.NET) k měření přesných pixelových pozic, nebo přidejte malý okraj (`+5` pixelů) ke každé ROI |
| Prázdný výsledek pro oblast | ROI mimo hranice obrázku | Ověřte rozměry obrázku: `source_image.width`, `source_image.height` |

---

## Rozšíření řešení (Jak provést OCR ROI v různých scénářích)

- **Dynamické ROI**: Pokud mají vaše faktury proměnlivé rozvržení, můžete nejprve spustit rychlé OCR celé stránky pro vyhledání klíčových slov („Customer:“, „Address:“) a poté dynamicky vypočítat ROI.  
- **Dávkové zpracování**: Zabalte výše uvedené kroky do funkce a projděte složku s obrázky. Pamatujte, že je třeba znovu použít stejnou instanci `ocr_engine`, aby se udržovala nízká spotřeba paměti.  
- **Export do JSON**: Místo tisknutí vytvořte slovník a uložte jej pomocí `json.dumps`; to usnadní následnou integraci (např. napojení na ERP systém).

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

## Závěr

Nyní máte kompletní, spustitelný příklad, který ukazuje **jak provést OCR ROI** v Pythonu a zároveň ovládá **jak nastavit předzpracování** pro optimální přesnost. Omezením enginu na přesné obdélníky, které vás zajímají, a předchozím vyčištěním obrázku získáte rychlejší a čistší výsledky — ideální pro automatizaci faktur, digitalizaci formulářů nebo jakýkoli scénář, kde stačí jen část stránky.

Jste připraveni na další krok? Zkuste upravit souřadnice ROI pro jiný typ dokumentu nebo experimentujte s dalšími příznaky předzpracování, jako jsou `sharpen` nebo `noise_reduction`. Flexibilita Aspose OCR vám umožní přizpůsobit pipeline prakticky jakékoli kvalitě obrázku.

Pokud narazíte na problém, podívejte se na výstup v konzoli pro prázdné oblasti a vraťte se k nastavením předzpracování. Šťastné kódování a ať je vaše OCR vždy přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}