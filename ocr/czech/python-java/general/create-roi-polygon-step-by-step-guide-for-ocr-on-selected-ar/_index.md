---
category: general
date: 2026-03-26
description: Vytvořte ROI polygon pro spuštění OCR na vybrané oblasti. Naučte se,
  jak definovat více oblastí, zaregistrovat je a extrahovat text pomocí OCR enginu
  v Pythonu.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: cs
og_description: Vytvořte ROI polygon a spusťte OCR na vybrané oblasti pomocí Python
  enginu. Kompletní kód, vysvětlení a tipy jsou zahrnuty.
og_title: Vytvořit polygon ROI – Rychlé OCR ve vybrané oblasti
tags:
- OCR
- Python
- Image Processing
title: Vytvořit ROI polygon – krok‑po‑kroku průvodce pro OCR ve vybrané oblasti
url: /cs/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření ROI polygonu – kompletní tutoriál pro OCR ve vybrané oblasti

Už jste někdy potřebovali **vytvořit ROI polygon**, abyste mohli spustit OCR jen na té části obrázku, která je podstatná? Možná skenujete účtenky a zajímají vás jen součty, nebo máte formulář, kde stačí přečíst pouze pole s podpisem. V takových případech **ocr on selected area** šetří čas a zvyšuje přesnost.  

V tomto průvodci projdeme vše, co potřebujete: od definování dvou polygonů, jejich registraci v OCR enginu, až po získání rozpoznaného textu jedním čistým voláním. Na konci budete mít připravený skript a solidní pochopení, proč je zaměření na oblasti zájmu (ROI) důležité.

## Co se naučíte

- Jak **vytvořit ROI polygon** objekty pomocí typické OCR knihovny.
- Rozdíl mezi definováním jedné oblasti a více oblastí.
- Jak registrovat tyto oblasti v enginu, aby se provedlo `ocr on selected area`.
- Očekávaný výstup a jak řešit běžné problémy (např. překrývající se ROI, prázdné výsledky).

### Předpoklady

- Nainstalovaný Python 3.8+.
- OCR knihovna, která poskytuje třídy `Polygon`, `Point` a metodu `add_region_of_interest` (příklad používá fiktivní modul `ocr`; nahraďte jej vaším skutečným SDK, např. Tesseract‑Python wrappery nebo EasyOCR).
- Ukázkový soubor obrázku (`sample.png`) obsahující text na souřadnicích uvedených níže.

> **Tip:** Pokud používáte skutečnou knihovnu, ujistěte se, že je obrázek načten ve stejném souřadnicovém systému (počátek v levém horním rohu, X roste doprava, Y roste dolů).  

---  

## Krok 1: Import OCR modulu a načtení obrázku  

Nejprve načtěte OCR balíček a přečtěte obrázek, který chcete zpracovat.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Proč je to důležité:* Engine potřebuje data obrázku, než k němu můžete připojit jakýkoli **ROI polygon**. Některé knihovny umožňují předat obrázek později, ale inicializace na začátku udržuje workflow přehledné.

## Krok 2: Definice prvního ROI polygonu  

Nyní vytvoříme první oblast zájmu. Představte si to jako nakreslení obdélníku kolem záhlaví tabulky.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Vysvětlení:*  
- `ocr.Point(x, y)` používá souřadnice v pixelech.  
- Seznam bodů je uspořádán po směru hodinových ručiček, což většina engine očekává.  
- Můžete přidat libovolný počet bodů a vytvořit tak nepravidelné tvary; obdélník je jen speciální případ.

## Krok 3: Definice dalších ROI polygonů (volitelné)  

Nemusíte se zastavit u jednoho. Zde je druhý polygon, který zachytí pole s podpisem níže na stránce.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Proč přidávat další?* Spuštění **ocr on selected area** pro více zón vám umožní extrahovat různé kusy dat v jednom průchodu, což je mnohem rychlejší než ořezávat a zpracovávat každý výřez zvlášť.

## Krok 4: Registrace ROI v OCR enginu  

S připravenými polygony řekněte enginu, které oblasti má kontrolovat.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Důležitá poznámka:* Některá SDK vyžadují volání metody `clear_regions()` před přidáním nových oblastí, pokud engine znovu používáte pro jiný obrázek.

## Krok 5: Spuštění OCR a získání textu  

Nakonec spustíme rozpoznání. Engine bude hledat jen uvnitř polygonů, které jsme právě přidali.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Očekávaný výstup** (předpokládáme, že `sample.png` obsahuje slova „Invoice Total: $123.45“ v první ROI a „Signature: John Doe“ ve druhé):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Pokud je výstup prázdný, zkontrolujte, že souřadnice skutečně protínají text a že rozlišení obrázku odpovídá souřadnicovému systému.

## Hraniční případy a běžné úskalí  

| Situace                                 | Na co si dát pozor                              | Oprava / řešení                                 |
|----------------------------------------|------------------------------------------------|-----------------------------------------------|
| **Překrývající se ROI**                | Text může být vrácen dvakrát.                  | Udržujte polygony disjunktní nebo deduplikujte výstup. |
| **ROI mimo hranice obrázku**            | Engine může vyhodit chybu nebo nic nevrátit.   | Ořízněte souřadnice na `0 ≤ x < šířka`, `0 ≤ y < výška`. |
| **Velmi malý ROI**                     | Přesnost OCR klesá kvůli nedostatku pixelů.   | Rozšiřte polygon o několik pixelů nebo nejprve zvětšete obrázek. |
| **Nerektangulární tvar**               | Některé enginy podporují jen konvexní polygony. | Rozdělte složité tvary na více konvexních ROI. |
| **Změna velikosti obrázku**            | Hard‑coded souřadnice přestanou platit.        | Vypočítejte souřadnice ROI relativně k rozměrům obrázku (např. procenta). |

## Kompletní funkční příklad  

Níže je celý skript, který můžete zkopírovat a spustit (nahraďte `ocr` vaší skutečnou knihovnou).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Spusťte jej pomocí `python ocr_roi_example.py` a měli byste vidět extrahované řetězce ze dvou definovaných zón.

## Další kroky  

- **Dynamické generování ROI:** Místo pevně zakódovaných souřadnic použijte zpracování obrazu (např. OpenCV detekci kontur) k automatickému nalezení tabulek nebo polí.  
- **Post‑processing:** Odstraňte bílé znaky, aplikujte regulární výrazy nebo převádějte čísla na správné datové typy.  
- **Dávkové zpracování:** Procházejte složku s obrázky a opakovaně používejte stejné definice ROI, pokud je rozložení konzistentní.  

Pokud vás zajímá **ocr on selected area** pro složitější dokumenty – např. více‑stránkové PDF nebo skenované formuláře – podívejte se na knihovny, které podporují registraci ROI po stránkách.  

---  

### Vizuální přehled  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="příklad vytvoření ROI polygonu ukazující dvě vybrané oblasti"}

Diagram ilustruje, jak se dva obdélníky (modrý a zelený) mapují na podkladový obrázek a přesně ukazují, co OCR engine přečte.

---  

## Závěr  

Právě jsme **vytvořili ROI polygon** objekty, zaregistrovali je v OCR enginu a provedli `ocr on selected area` v čistém, reprodukovatelném skriptu. Omezením enginu na zóny, které vás zajímají, zkrátíte dobu zpracování, zlepšíte přesnost a zjednodušíte následnou manipulaci s daty.  

Vyzkoušejte to na vlastních obrázcích – upravit souřadnice, přidat další polygony nebo napojit výstup do databáze. Možnosti jsou neomezené, jakmile ovládnete OCR založené na regionech.  

Máte otázky nebo chcete sdílet zajímavý případ užití? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}