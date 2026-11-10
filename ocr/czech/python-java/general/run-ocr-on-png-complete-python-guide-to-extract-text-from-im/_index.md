---
category: general
date: 2026-01-12
description: Rychle spusťte OCR na PNG souborech pomocí Pythonu. Naučte se, jak extrahovat
  text z obrázku a faktury a načíst obrázek pro OCR pomocí Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: cs
og_description: Okamžitě spusťte OCR na PNG. Tento průvodce ukazuje, jak extrahovat
  text z obrázku a faktury, načíst obrázek pro OCR a uložit výsledky jako JSON a CSV.
og_title: Spusťte OCR na PNG – Kompletní Python tutoriál
tags:
- OCR
- Python
- Image Processing
title: Spusťte OCR na PNG – Kompletní průvodce v Pythonu pro extrakci textu z obrázků
url: /cs/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na PNG – Kompletní průvodce v Pythonu pro extrakci textu z obrázků

Už jste někdy potřebovali **spustit OCR na PNG** souborech, ale nebyli jste si jisti, která knihovna vám poskytne čisté, strukturované výsledky? Nejste v tom sami. V mnoha reálných projektech—například automatizace faktur nebo skenování účtenek—je první krok **extrahovat text z obrázku** a PNG je běžný formát, protože zachovává bezztrátovou kvalitu.

V tomto tutoriálu projdeme praktickým příkladem pomocí balíčku Aspose.OCR pro Python. Na konci průvodce budete vědět, jak **načíst obrázek pro OCR**, získat každou řádku textu, převést tato data do přehledného JSON objektu a dokonce je uložit do CSV pro následné zpracování. Žádné zbytečnosti, jen praktické, připravené řešení.

## Co se naučíte

- Jak nainstalovat a importovat knihovnu Aspose.OCR.  
- Přesné kroky k **spuštění OCR na PNG** a zpracování výsledného objektu.  
- Způsoby, jak **extrahovat text z faktury** a formátovat výstup jako JSON nebo CSV.  
- Tipy pro práci s nízkokontrastními obrázky, vícejazyčnými dokumenty a skóre důvěry.  
- Kompletní ukázkový kód ke zkopírování a vložení, který můžete spustit ještě dnes.

> **Předpoklad:** Python 3.8+ a základní znalost pip. Pokud jste dosud nepoužívali Aspose, nebojte se—tento průvodce pokrývá vše, co potřebujete k zahájení.

---

## Krok 1 – Instalace Aspose.OCR a příprava prostředí

Než budeme moci **spustit OCR na PNG**, musí být knihovna nainstalována ve vašem systému.

```bash
pip install aspose-ocr
```

> **Tip:** Použijte virtuální prostředí (`python -m venv venv`), aby byly závislosti izolované. Zabrání to konfliktům verzí, pokud pracujete na více projektech.

Po instalaci importujte potřebné moduly:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Zde načteme `asposeocr` pro těžkou práci a vestavěnou knihovnu `json` pro pozdější serializaci.

## Krok 2 – Vytvoření OCR enginu a nastavení jazyka

OCR engine je hlavní komponenta, která skutečně čte pixely. Pro většinu anglických faktur budete chtít balíček anglického jazyka:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Proč je to důležité:** Specifikace jazyka omezuje množinu znaků, což zvyšuje přesnost a urychluje zpracování. Pokud budete potřebovat zpracovávat vícejazyčné faktury, stačí vyměnit `ocr.Language.ENGLISH` za odpovídající enum.

## Krok 3 – Načtení obrázku pro OCR

Nyní **načteme obrázek pro OCR**. Metoda `Image.load` přijímá cestu k souboru a funguje s PNG, JPEG, BMP a dalšími.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Hraniční případ:** Pokud je PNG neobvykle velký (více než 5 MB), zvažte jeho zmenšení, aby byl rozumný spotřeba paměti. Pillow to dokáže v jediném řádku:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## Krok 4 – Spuštění OCR na PNG a zachycení výsledku

S připraveným enginem a načteným obrázkem je čas **spustit OCR na PNG** a získat strukturovaný výsledek.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Objekt `ocr_result` obsahuje kolekci položek `OcrRegion`, z nichž každá má rozpoznaný text a skóre důvěry (0‑100). Zde získáte podrobná data potřebná k **extrakci textu z faktury** řádků.

## Krok 5 – Převod výsledku do JSON a pěkný výpis

Většina následných systémů miluje JSON, takže převádíme výstup OCR do hezky naformátovaného řetězce.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Ukázkový výstup

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Všimněte si, že každá řádka obsahuje metriku důvěry—ideální pro filtrování položek s nízkou důvěrou, pokud plánujete **extrahovat text z faktury** automaticky.

## Krok 6 – Uložení OCR dat jako CSV (Jedna řádka na text + důvěru)

CSV je ideální pro tabulky nebo rychlé importy dat. Aspose nabízí jednorázový příkaz, který vše uloží do CSV souboru.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Vygenerovaný CSV bude vypadat takto:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Nyní jej můžete otevřít v Excelu, Google Sheets nebo načíst do databáze.

## Bonus – Zpracování textu s nízkou důvěrou a vícestránkových PDF

### Filtrování podle důvěry

Pokud chcete pouze řádky s vysokou jistotou, před zápisem je potřeba filtrovat JSON:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Vícestránkové dokumenty

Aspose.OCR automaticky vytvoří nový záznam `page` pro každou stránku ve vícestránkovém PNG nebo PDF. Projděte `ocr_data["pages"]`, abyste je všechny zpracovali—žádný další kód není potřeba.

## Kompletní funkční příklad

Níže je **kompletní skript**, který můžete okamžitě zkopírovat, vložit a spustit. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje váš PNG soubor.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Spusťte skript pomocí `python run_ocr.py` a uvidíte výpis JSON v konzoli, CSV soubor na disku a filtrovaný seznam položek s vysokou důvěrou.

## Často kladené otázky

**Q: Můžu to použít k extrakci textu ze skenované účtenky místo faktury?**  
A: Rozhodně. Stejný postup platí—stačí nasměrovat `image_path` na PNG vaší účtenky. Pokud účtenka používá jiný jazyk, přepněte `engine.language` podle toho.

**Q: Co když moje PNG obsahuje natočený text?**  
A: Aspose.OCR automaticky detekuje orientaci, ale v obtížných případech můžete obrázek před předáním enginu ručně otočit pomocí Pillow.

**Q: Potřebuji placenou licenci pro Aspose.OCR?**  
A: Knihovna nabízí bezplatný evaluační režim s vodoznakem na výstupu. Pro produkční použití budete potřebovat licenci, kterou lze získat na webu Aspose.

## Závěr

Probrali jsme vše, co potřebujete k **spuštění OCR na PNG** souborech pomocí Pythonu: instalaci SDK, načtení obrázku, extrakci strukturovaného textu a uložení výsledku jako JSON nebo CSV. Ať už chcete **extrahovat text z obrázku** pro jednoduchý skript nebo **extrahovat text z faktury** pro automatizovaný účetní pipeline, výše uvedené kroky vám poskytnou pevný, připravený základ pro produkci.

Dále můžete zkoumat:

- Integraci CSV výstupu s databází pro hromadné ukládání faktur.  
- Přidání post‑zpracování pomocí regulárních výrazů pro získání dat, částek nebo DIČ.  
- Použití funkce `ocr_engine.recognize_barcode`, pokud vaše faktury obsahují QR kódy.

Vyzkoušejte to, upravte prahy důvěry a sledujte, jak se váš workflow pro zpracování dokumentů stane hračkou. Máte další otázky nebo zajímavý případ použití? Zanechte komentář níže—příjemné OCRování!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}