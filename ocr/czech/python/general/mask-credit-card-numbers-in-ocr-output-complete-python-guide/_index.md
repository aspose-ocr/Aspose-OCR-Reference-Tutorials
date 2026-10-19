---
category: general
date: 2026-04-26
description: Rychle maskujte čísla kreditních karet pomocí post‑zpracování OCR od
  AsposeAI. Naučte se o shodě s PCI, maskování regulárních výrazů a sanitaci dat v
  tutoriálu krok za krokem.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: cs
og_description: Maskujte čísla kreditních karet ve výsledcích OCR pomocí AsposeAI.
  Tento tutoriál pokrývá dodržování PCI, maskování pomocí regulárních výrazů a sanitaci
  dat.
og_title: Maskování čísel kreditních karet – Kompletní průvodce post‑processingem
  OCR v Pythonu
tags:
- OCR
- Python
- security
title: Maskování čísel kreditních karet v OCR výstupu – Kompletní průvodce v Pythonu
url: /cs/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maskování čísel kreditních karet – Kompletní průvodce v Pythonu

Už jste někdy potřebovali **maskovat čísla kreditních karet** v textu, který pochází přímo z OCR enginu? Nejste v tom sami. V regulovaných odvětvích může odhalení úplného PAN (Primary Account Number) přivést problémy s auditorem PCI compliance. Dobrá zpráva? S několika řádky Pythonu a post‑processing hookem AsposeAI můžete automaticky skrýt prostředních osm číslic a zůstat na bezpečné straně.

V tomto tutoriálu projdeme reálný scénář: spuštění OCR na obrázku účtenky a následné použití vlastní **OCR post‑processing** funkce, která sanitizuje jakákoli PCI data. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného workflow AsposeAI, plus několik praktických tipů pro řešení okrajových případů a škálování řešení.

## Co se naučíte

- Jak zaregistrovat vlastní post‑processor s **AsposeAI**.
- Proč je přístup **regular expression masking** rychlý a spolehlivý.
- Základy **PCI compliance** související s sanitací dat.
- Způsoby, jak rozšířit vzor pro více formátů karet nebo mezinárodní čísla.
- Očekávaný výstup a jak ověřit, že maskování funguje.

> **Předpoklady** – Měli byste mít funkční prostředí Python 3, nainstalovaný balíček Aspose.AI for OCR (`pip install aspose-ocr`) a ukázkový obrázek (např. `receipt.png`), který obsahuje číslo kreditní karty. Žádné další externí služby nejsou vyžadovány.

---

## Krok 1: Definujte post‑processor, který maskuje čísla kreditních karet

Srdce řešení spočívá v malé funkci, která přijímá výsledek OCR, spustí **regular expression masking** rutinu a vrátí sanitizovaný text.

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

**Proč to funguje:**  
- Regulární výraz `(\d{4})\d{8}(\d{4})` odpovídá přesně 16 po sobě jdoucím číslicím, což je běžný formát pro Visa, MasterCard a mnoho dalších.  
- Zachycením prvních a posledních čtyř číslic (`\1` a `\2`) zachováme dostatek informací pro ladění a zároveň dodržujeme pravidla **PCI compliance**, která zakazují ukládání úplného PAN.  
- Náhrada `\1****\2` skryje citlivých osm prostředních číslic a změní `1234567812345678` na `1234****5678`.

> **Pro tip:** Pokud potřebujete podporovat 15‑ciferná čísla American Express, přidejte druhý vzor jako `r'(\d{4})\d{6}(\d{5})'` a spusťte oba nahrazení sekvenčně.

---

## Krok 2: Inicializujte engine AsposeAI

Než můžeme připojit náš post‑processor, potřebujeme instanci OCR enginu. AsposeAI balí OCR model a jednoduché API pro vlastní zpracování.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Proč inicializovat zde?**  
Vytvořením objektu `AsposeAI` jednou a jeho opakovaným použitím napříč více obrázky snižujeme režii. Engine také kešuje jazykové modely, což urychluje následná volání – užitečné při skenování dávky účtenek.

---

## Krok 3: Zaregistrujte vlastní maskovací funkci

AsposeAI poskytuje metodu `set_post_processor`, která vám umožní připojit libovolný callable. Předáme naši funkci `mask_pci` spolu s volitelným slovníkem nastavení (prozatím prázdným).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Co se děje v pozadí?**  
Když později zavoláte `run_postprocessor`, AsposeAI předá surový výsledek OCR funkci `mask_pci`. Funkce dostane lehký objekt (`data`), který obsahuje rozpoznaný text, a vy vrátíte nový řetězec. Tento design ponechává jádro OCR nedotčené a umožňuje vynutit **data sanitization** politiku na jednom místě.

---

## Krok 4: Spusťte OCR na obrázku účtenky

Nyní, když engine ví, jak vyčistit výstup, předáme mu obrázek. Pro tento tutoriál předpokládáme, že již máte objekt `engine` nakonfigurovaný se správnými jazykovými a rozlišeními.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Pokud nemáte předkonfigurovaný objekt, můžete jej vytvořit pomocí:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Volání `recognize_image` vrací objekt, jehož atribut `text` obsahuje surový, ne‑maskovaný řetězec.

---

## Krok 5: Použijte registrovaný post‑processor

S čistými OCR daty v ruce je předáme instanci AI. Engine automaticky spustí funkci `mask_pci`, kterou jsme dříve zaregistrovali.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Proč použít `run_postprocessor` místo ručního volání funkce?**  
Tím se workflow udrží konzistentní, zejména když máte více post‑processorů (např. kontrola pravopisu, detekce jazyka). AsposeAI je řadí v pořadí, ve kterém je zaregistrujete, a zaručuje deterministický výstup.

---

## Krok 6: Ověřte sanitovaný výstup

Nakonec vytiskneme sanitovaný text a potvrdíme, že všechna čísla kreditních karet jsou správně maskována.

```python
print(final_result.text)
```

**Očekávaný výstup** (úryvek):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Pokud účtenka neobsahovala žádné číslo karty, text zůstane nezměněn – nic k maskování, nic k obavám.

---

## Řešení okrajových případů a běžných variant

### Více čísel karet v jednom dokumentu
Pokud účtenka obsahuje více než jeden PAN (např. věrnostní kartu plus platební kartu), regulární výraz běží globálně a automaticky maskuje všechny shody. Žádný další kód není potřeba.

### Nestandardní formátování
Někdy OCR vloží mezery nebo pomlčky (`1234 5678 1234 5678` nebo `1234-5678-1234-5678`). Rozšiřte vzor, aby ignoroval tyto znaky:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Přidané `[ -]?` toleruje volitelné mezery nebo pomlčky mezi bloky číslic.

### Mezinárodní karty
Pro 19‑ciferné PANy používané v některých regionech můžete rozšířit vzor:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Jen si pamatujte, že **PCI compliance** stále vyžaduje maskování prostředních číslic, bez ohledu na délku.

### Logování maskovaných hodnot (volitelné)
Pokud potřebujete auditní stopy, předávejte příznak přes `custom_settings` a upravte funkci:

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

Pak zaregistrujte pomocí:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Kompletní funkční příklad (připravený ke zkopírování)

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

Spuštěním tohoto skriptu na účtence, která obsahuje `4111111111111111`, získáte:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

To je celý pipeline – od surového OCR až po **data sanitization** – zabalený do několika čistých řádků Pythonu.

---

## Závěr

Právě jsme vám ukázali, jak **maskovat čísla kreditních karet** v OCR výsledcích pomocí post‑processing hooku AsposeAI, stručné rutiny regulárního výrazu a několika tipů pro **PCI compliance**. Řešení je zcela samostatné, funguje s libovolným obrázkem, který OCR engine dokáže přečíst, a lze jej rozšířit o složitější formáty karet nebo požadavky na logování.

Jste připraveni na další krok? Zkuste propojit tuto masku s rutinou **vkládání do databáze**, která ukládá jen poslední čtyři číslice pro referenci, nebo integrujte **batch processor**, který během noci prohledá celý adresář účtenek. Můžete také prozkoumat další **OCR post‑processing** úkoly, jako je standardizace adres nebo detekce jazyka – každý z nich následuje stejný vzor, který jsme zde použili.

Máte otázky ohledně okrajových případů, výkonu nebo toho, jak přizpůsobit kód pro jinou OCR knihovnu? Zanechte komentář níže a pojďme konverzaci posunout dál. Šťastné kódování a zůstaňte v bezpečí!  



![Diagram ilustrující, jak maskování čísel kreditních karet funguje v OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram post‑processing maskování v OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}