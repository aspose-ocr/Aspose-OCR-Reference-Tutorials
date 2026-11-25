---
category: general
date: 2026-06-16
description: Definujte oblast zájmu v OCR pro extrakci španělského textu z občanských
  průkazů. Naučte se, jak načíst obrázek pro OCR a efektivně specifikovat oblast zájmu.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: cs
og_description: Definujte oblast zájmu v OCR pro extrakci španělského textu z občanských
  průkazů. Průvodce krok za krokem načítáním obrázků a určením ROI.
og_title: Definujte oblast zájmu v OCR – kompletní Python tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Definujte oblast zájmu v OCR – kompletní Python tutoriál
url: /cs/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definování oblasti zájmu v OCR – Kompletní Python tutoriál

Už jste se někdy zamysleli, jak **definovat oblast zájmu v OCR**, abyste četli jen tu část obrázku, kterou skutečně potřebujete? V tomto tutoriálu vás provedeme přesně tímto krokem a také vám ukážeme, jak **načíst obrázek pro OCR** a extrahovat španělský text z občanského průkazu pomocí několika řádků Pythonu.  

Pokud jste někdy zírali na špinavý sken a pomysleli si: „Musí existovat čistší způsob, jak získat pole se jménem“, jste na správném místě. Na konci budete schopni vytáhnout text z občanského průkazu, který vás zajímá, aniž byste se potýkali s pozadím.

## Co se naučíte

- Proč byste měli **definovat oblast zájmu** před spuštěním OCR.  
- Přesné kroky k **načtení obrázku pro OCR** pomocí populárního Python OCR wrapperu.  
- Jak **specifikovat ROI** pomocí pixelových souřadnic.  
- Způsoby, jak **spolehlivě extrahovat text z občanského průkazu**, i když je zdrojový jazyk španělština.  
- Tipy pro řešení okrajových případů, jako jsou otočené karty nebo snímky s nízkým kontrastem.  

Žádná předchozí znalost OCR není vyžadována – stačí funkční prostředí Python 3 a JPEG obrázek občanského průkazu, který chcete otestovat.

---

![Define region of interest illustration](placeholder.png){alt="Příklad definování oblasti zájmu ukazující zvýrazněný obdélník na obrázku občanského průkazu"}

## Krok 1: Instalace a import OCR knihovny

Nejprve potřebujete knihovnu, která poskytuje třídu `OcrEngine` podobnou ukázce, kterou jste viděli. Pro tento návod použijeme fiktivní balíček `ocr`, ale stejné koncepty platí pro `pytesseract`, `easyocr` nebo jakýkoli wrapper, který umožňuje nastavit jazyk a ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Pokud používáte `pytesseract`, třída `Rectangle` se stane jednoduchou n-ticí `(left, top, width, height)`. Zbytek toku zůstává identický.

## Krok 2: Načtení obrázku pro OCR

Nyní **načteme obrázek pro OCR**. Engine očekává objekt `ocr.Image`, takže mu ukážeme soubor, který obsahuje občanský průkaz. Ujistěte se, že cesta je absolutní nebo relativní k pracovnímu adresáři skriptu.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Pokud je obrázek obrovský, zvažte jeho předchozí změnu velikosti; OCR enginy pracují rychleji na obrázcích širších než 1500 px.

## Krok 3: Jak specifikovat ROI (Definování oblasti zájmu)

Tady je jádro tutoriálu: **jak specifikovat ROI**. Oblast zájmu je jednoduše obdélník, který říká OCR enginu: „Podívej se jen dovnitř těchto pixelových hranic.“ Představte si to jako nakreslení rámečku kolem pole se jménem na občanském průkazu.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Proč tyto čísla? V našem ukázkovém obrázku je jméno přibližně 120 px od levého okraje a 80 px od horního. Přizpůsobte je tak, aby odpovídaly rozložení karet, které zpracováváte.  

*Okrajový případ:* Pokud je karta otočena o 90°, vyměňte `width` a `height` a upravte `left`/`top` podle toho, nebo předem otočte obrázek pomocí Pillow, než jej předáte enginu.

## Krok 4: Provedení OCR v rámci ROI

S definovaným ROI engine ignoruje vše mimo obdélník. To nejen zrychluje zpracování, ale také snižuje falešně pozitivní výsledky způsobené grafickým pozadím.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

Volání `recognize()` vrací objekt, který obsahuje rozpoznaný text, skóre spolehlivosti a ohraničující rámečky pro každé slovo.

## Krok 5: Extrahování textu z občanského průkazu (a ověření španělského výstupu)

Nakonec **extrahujeme text z občanského průkazu** z výsledku ROI a vytiskneme ho. Protože jsme dříve nastavili jazyk na španělštinu, OCR engine použije jazykově specifické slovníky, což zvyšuje přesnost u znaků s diakritikou jako „ñ“ nebo „á“.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Očekávaný výstup

```
ROI text: JUAN PÉREZ GARCÍA
```

Pokud vidíte poškozené znaky, dvojitě zkontrolujte, že obrázek je skutečně ve španělštině a že jsou nainstalovány jazykové datové soubory OCR knihovny.

## Časté problémy a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Vrácený prázdný řetězec | ROI neprotíná žádný text | Ověřte souřadnice v prohlížeči obrázků; použijte `engine.debug_draw_roi()`, pokud je k dispozici. |
| Mnoho nesmyslných znaků | Špatný jazykový balíček | Přeinstalujte španělská jazyková data nebo přepněte na `ocr.Language.AUTO`. |
| Nízké skóre spolehlivosti | Obrázek je rozmazaný nebo má nízký kontrast | Předzpracujte pomocí OpenCV – použijte `cv2.GaussianBlur` a `cv2.threshold`. |
| OCR běží na celém obrázku i přes ROI | Použití starší verze knihovny | Aktualizujte na nejnovější balíček `ocr`; starší verze ignorovaly ROI. |

## Rozšíření příkladu: Více ROI

Někdy potřebujete získat více polí (např. jméno a číslo ID). Vzorec zůstává stejný: změňte `engine.region_of_interest` a znovu zavolejte `recognize()`.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Můžete také dávkově zpracovat seznam obdélníků, pokud knihovna tuto funkci podporuje, což šetří počet volání OCR engine.

## Kompletní funkční skript

Sestavením všeho dohromady získáte připravený skript, který **definuje oblast zájmu**, **načte obrázek pro OCR** a **extrahuje španělský text** z občanského průkazu.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Spusťte skript a měli byste vidět jméno vytištěné v konzoli. Změňte hodnoty obdélníku pro cílení na jiná pole a budete mít znovupoužitelný nástroj pro jakýkoli dokument typu občanského průkazu.

## Další kroky

- **Dávkové zpracování:** Procházet složku s občanskými průkazy a uložit každé extrahované jméno do CSV souboru.  
- **Detekce jazyka:** Nechat uživatele dynamicky vybrat jazyk; `ocr.Language.AUTO` může být užitečný.  
- **Post‑zpracování:** Použít regex vzory k vyčištění běžných OCR chyb (např. nahradit „0“ za „O“, když se objeví ve jménech).  

Ovládnutím **definování oblasti zájmu** jste získali mocný způsob, jak **extrahovat text z občanského průkazu** rychle a přesně, zejména při práci se španělsky psanými dokumenty.

---

### TL;DR

Ukázali jsme vám, jak **definovat oblast zájmu v OCR**, **načíst obrázek pro OCR** a **jak specifikovat ROI** k **extrahování španělského textu** z obrázku občanského průkazu. Kompletní příklad běží za méně než minutu a lze jej přizpůsobit libovolnému rozložení pomocí několika úprav souřadnic. Vyzkoušejte to, upravte obdélník a sledujte, jak OCR zaměří jako laser.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětlením, aby vám pomohl ovládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}