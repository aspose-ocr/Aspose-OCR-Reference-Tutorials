---
category: general
date: 2026-01-02
description: Naučte se, jak zaznamenávat AI pomocí Aspose OCR s vlastním loggerem.
  Tento průvodce zahrnuje příklad vlastního loggeru, jak importovat Aspose OCR a nastavit
  vlastní logger.
draft: false
keywords:
- how to log ai
- use custom logger
- custom logger example
- import aspose ocr
- set custom logger
language: cs
og_description: Naučte se, jak zaznamenávat AI pomocí Aspose OCR s vlastním loggerem.
  Postupujte podle podrobného návodu, importujte Aspose OCR, nastavte vlastní logger
  a podívejte se na výstup.
og_title: Jak logovat AI pomocí Aspose OCR – Příklad vlastního loggeru
tags:
- Aspose OCR
- Python
- Logging
title: Jak logovat AI pomocí Aspose OCR – Příklad vlastního loggeru
url: /cs/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zaznamenávat AI s Aspose OCR – Příklad vlastního loggeru

Už jste se někdy zamysleli **jak zaznamenávat AI**, když si hrajete s Aspose OCR? Možná jste vyzkoušeli výchozí konzolový logger a pomysleli si: „To je v pořádku, ale mohu to udělat hezčím nebo posílat logy do souboru?“ Nejste v tom sami. V tomto tutoriálu projdeme kompletní **příklad vlastního loggeru**, ukážeme vám přesný kód, který potřebujete, a vysvětlíme *proč* je každá část důležitá.

Do konce tohoto průvodce budete schopni:

* **Importovat Aspose OCR** v Pythonu bez problémů.  
* **Nastavit vlastní logger**, který zachytí každou zprávu, kterou AI engine vydá.  
* Ověřit výstup a přizpůsobit logger pro vlastní logovací framework.

Není potřeba žádná externí dokumentace – vše, co potřebujete, je zde.

---

## Předpoklady

Než se ponoříme dál, ujistěte se, že máte:

| Požadavek | Důvod |
|-------------|--------|
| Python 3.8+ | Balíček `asposeocr` cílí na moderní Python. |
| `asposeocr` library installed (`pip install asposeocr`) | Poskytuje modul `asposeocr.ai`, který použijeme. |
| Basic familiarity with functions and callables | Potřebné pro vytvoření vlastního loggeru. |

Pokud vám něco chybí, nainstalujte knihovnu nyní:

```bash
pip install asposeocr
```

---

## Krok 1 – Import Aspose OCR a AI modulu

První věc, kterou uděláte, když chcete **importovat Aspose OCR**, je načíst jmenný prostor `asposeocr.ai`. To vám poskytne přístup ke třídě `AsposeAI`, která je vstupním bodem pro všechny AI‑řízené OCR operace.

```python
# Step 1: Import the Aspose OCR AI module
import asposeocr.ai as ai
```

*Proč je to důležité:* Importování správného modulu zajišťuje, že komunikujete se správným backendem. Pokud vynecháte podmodul `.ai`, získáte jen klasické OCR API, které neobsahuje potřebné logovací háčky.

---

## Krok 2 – Vytvořit výchozí AI engine (konzolový logger)

Aspose OCR je dodáván s vestavěným loggerem, který zapisuje přímo do `stdout`. Spusťme ho, abyste viděli výchozí chování.

```python
# Step 2: Create an AI engine that logs to the console by default
default_engine = ai.AsposeAI()
```

Když spustíte jakoukoli OCR operaci s `default_engine`, uvidíte zprávy jako:

```
[INFO] AsposeAI initialized – version 23.10
[DEBUG] Loading language model...
```

Tyto zprávy jsou užitečné pro rychlé ladění, ale nejsou dostatečně flexibilní pro produkční prostředí. Proto přecházíme na další krok.

---

## Krok 3 – Definovat vlastní logger (libovolná volatelná funkce přijímající řetězec)

**Vlastní logger** může být jakákoli volatelná funkce v Pythonu, která přijímá jeden argument typu `str`. Níže je minimální příklad, který přidává předponu `[AI LOG]` ke zprávám. Klidně nahraďte `print` za `logging.info`, zapisujte do souboru nebo posílejte do monitorovací služby.

```python
# Step 3: Define a custom logger (any callable that accepts a string)
def custom_logger(message: str):
    # You could replace this with `logging.info(message)` or any other sink.
    print("[AI LOG]", message)
```

*Proč to funguje:* Konstruktor `AsposeAI` hledá argument `logging`, který implementuje protokol „volání s řetězcem“. Poskytnutím funkce, která odpovídá tomuto podpisu, předáte plnou kontrolu nad tím, jak je každá řádka logu zpracována.

---

## Krok 4 – Vytvořit AI engine, který používá vlastní logger

Nyní vše spojíme. Předáte `custom_logger` konstruktoru `AsposeAI` pomocí parametru `logging`. Engine přepošle každou interní zprávu do vaší funkce.

```python
# Step 4: Create an AI engine that uses the custom logger
engine_with_custom_logger = ai.AsposeAI(logging=custom_logger)
```

### Očekávaný výstup

Spuštění jednoduchého OCR volání (např. `engine_with_custom_logger.recognize("sample.png")`) vytvoří výstup podobný:

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.
```

Všimněte si, že každá řádka nyní začíná `[AI LOG]`, přesně tak, jak jsme definovali v `custom_logger`. To dokazuje, že **jak zaznamenávat AI** akce je plně pod vaší kontrolou.

---

## Kompletní funkční příklad – Od importu po spuštění

Níže je kompletní skript, který můžete zkopírovat do souboru s názvem `custom_logger_demo.py`. Ukazuje celý tok, od importu Aspose OCR po provedení jednoduchého OCR požadavku s vlastním loggerem.

```python
# custom_logger_demo.py
# -------------------------------------------------
# Demonstrates how to log AI using Aspose OCR
# with a user‑defined logger.
# -------------------------------------------------

import asposeocr.ai as ai

def custom_logger(message: str):
    """A tiny logger that prefixes messages."""
    print("[AI LOG]", message)

def main():
    # Use the custom logger when creating the AI engine
    ocr_engine = ai.AsposeAI(logging=custom_logger)

    # Path to an image you want to process (replace with your own)
    image_path = "sample.png"

    # Perform OCR – this will trigger the logger
    try:
        result = ocr_engine.recognize(image_path)
        print("\n--- OCR RESULT ---")
        print(result.text)  # Assuming the result object has a `text` attribute
    except Exception as e:
        print("[AI LOG] Error during OCR:", e)

if __name__ == "__main__":
    main()
```

**Co očekávat při spuštění**

```bash
python custom_logger_demo.py
```

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.

--- OCR RESULT ---
Hello world! This is the extracted text.
```

Pokud chcete **nastavit vlastní logger** na soubor, stačí nahradit `print` v `custom_logger` něčím jako:

```python
def file_logger(message: str):
    with open("ocr.log", "a", encoding="utf-8") as f:
        f.write(message + "\n")
```

a předat `logging=file_logger` při konstrukci `AsposeAI`.

---

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Mohu použít standardní modul `logging`?* | Ano. Stačí nakonfigurovat instanci loggeru a ve své volatelné funkci předat `logger.info(message)`. |
| *Co když můj logger vyvolá výjimku?* | SDK zachytí jakoukoli výjimku z loggeru a pokračuje, ale danou řádku logu ztratíte. Držte se jednoduchosti. |
| *Získává logger také zprávy úrovně debug?* | Ano. AI engine přeposílá **všechny** interní zprávy (INFO, DEBUG, WARN). Filtrujte ve své volatelné funkci, pokud chcete jen určité úrovně. |
| *Je argument `logging` volitelný?* | Pokud je vynechán, engine se vrátí k vestavěnému konzolovému loggeru. |
| *Bude to fungovat v async kódu?* | Logger sám je synchronní; pokud potřebujete asynchronní zpracování, zabalte volání do coroutine `asyncio` a použijte `await` tam, kde je to vhodné. |

---

## Pro tipy – Jak připravit logger pro produkci

1. **Dávkové zápisy** – Otevírání a zavírání souboru pro každou zprávu je pomalé. Použijte `logging.FileHandler` s bufferováním.  
2. **Přidejte časová razítka** – Zahrňte `datetime.now().isoformat()` do předpony, aby bylo ladění snazší.  
3. **Úrovně logování** – Pokud potřebujete jemnější granularitu, změňte podpis tak, aby přijímal n‑tici jako `(level, message)` a upravte volání SDK (aktuálně předává jen řetězec, takže byste museli ručně parsovat klíčová slova úrovně).  
4. **Centralizujte konfiguraci** – Uchovávejte definici loggeru v samostatném modulu (`my_logging.py`) a importujte ji všude, kde vytváříte instanci `AsposeAI`.  

---

## Závěr

Probrali jsme **jak zaznamenávat AI** s Aspose OCR od začátku až do konce: import knihovny, vytvoření výchozího engine, napsání **příkladu vlastního loggeru** a nakonec propojení tohoto loggeru s AI engine. Kód je kompletní, spustitelný a přizpůsobitelný libovolnému logovacímu backendu, který preferujete.

Pokud chcete jít dál, zkuste nahradit logger založený na `print` modulem `logging` v Pythonu, posílat logy do cloudové služby jako Datadog, nebo dokonce emitovat strukturovaný JSON pro následnou analýzu. Vzor zůstává stejný — **použijte vlastní logger** a **nastavte vlastní logger** při vytváření instance `AsposeAI`.

Šťastné programování a ať jsou vaše logy vždy tak jasné jako výsledky OCR!

![screenshot jak zaznamenávat AI](image.png "příklad jak zaznamenávat AI")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}