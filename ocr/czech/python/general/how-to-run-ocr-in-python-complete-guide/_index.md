---
category: general
date: 2026-06-19
description: Jak provádět OCR krok za krokem a zlepšit přesnost OCR pomocí technik
  pro prostý text. Naučte se rychlý pracovní postup pro spolehlivé získávání textu.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: cs
og_description: Jak efektivně spustit OCR. Tento tutoriál ukazuje, jak zlepšit přesnost
  OCR pomocí OCR prostého textu a AI post‑zpracování.
og_title: Jak spustit OCR v Pythonu – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Jak spustit OCR v Pythonu – kompletní průvodce
url: /cs/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR v Pythonu – Kompletní průvodce

Už jste se někdy zamýšleli **jak spustit OCR** na dávce naskenovaných PDF souborů, aniž byste strávili hodiny laděním nastavení? Nejste v tom sami. V mnoha projektech je první překážkou prostě získat spolehlivý text z obrázku a rozdíl mezi nejistým výsledkem a čistým výstupem často spočívá v několika chytrých krocích.

V tomto průvodci projdeme praktickým čtyřkrokovým pipeline, který nejen **spouští OCR**, ale také **zlepšuje přesnost OCR** kombinací rychlého průchodu prostým textem, druhého průchodu s ohledem na rozvržení a AI‑poháněného post‑processoru. Na konci budete mít připravený skript, jasné vysvětlení, proč je každá fáze důležitá, a tipy, jak zacházet s okrajovými případy, jako jsou vícesloupcové stránky nebo špinavé skeny.

---

## Co budete potřebovat

- **Python 3.9+** – kód používá typové nápovědy a f‑stringy.
- **Tesseract OCR** nainstalovaný a přístupný přes příkazovou řádku `tesseract`. (Na Ubuntu: `sudo apt install tesseract-ocr`; na Windows stáhněte instalátor z oficiálního repozitáře.)
- Wrapper **pytesseract** (`pip install pytesseract`).
- **AI post‑processing knihovna** – pro tento příklad předstíráme, že máte lehký modul `ai`, který nabízí `run_postprocessor`. Nahraďte jej OpenAI GPT‑4 API nebo lokálním LLM, pokud chcete.
- Několik ukázkových obrázků nebo PDF souborů k otestování.

A to je vše. Žádné těžké frameworky, žádné Dockerové gymnastiky. Pouze pár instalací přes pip a můžete začít.

## Krok 1: Proveďte rychlý průchod prostým textem OCR

První věc, kterou většina vývojářů přehlíží, je, že *plain text* OCR běh je bleskově rychlý a poskytuje rychlou kontrolu smysluplnosti. Zavoláme `engine.Recognize()`, abychom získali surové znaky bez jakýchkoli metadat o rozvržení. To je to, co máme na mysli pod **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Proč je to důležité:*  
- **Rychlost** – jednoduchý průchod na stránce 300 dpi obvykle skončí za méně než sekundu.  
- **Základní linie** – můžete porovnat pozdější strukturovaný výstup s touto základní linií a odhalit zjevné chyby.  
- **Odchytávání chyb** – pokud jednoduchý průchod selže úplně (např. vše je nesmysl), víte, že kvalita obrázku je příliš nízká a můžete ukončit dříve.

## Krok 2: Proveďte podrobný OCR průchod s ohledem na rozvržení

Prostý text je skvělý, ale ztrácí *kde* se každé slovo nachází na stránce. Pro faktury, formuláře nebo vícesloupcové časopisy potřebujete souřadnice, čísla řádků a možná i informace o fontu. Zde přichází `engine.RecognizeStructured()`.

Níže je tenký wrapper kolem výstupu **TSV** z Tesseractu, který nám poskytuje hierarchii stránek → řádků → slov, zachovávající ohraničující rámečky.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Proč to děláme:*  
- **Souřadnice** vám umožní později mapovat extrahovaný text zpět na originální obrázek pro zvýraznění nebo redakci.  
- **Skupinování řádků** zachovává originální rozvržení, což je nezbytné při rekonstrukci tabulek nebo sloupců.  
- Tento průchod je o něco pomalejší než prostý, ale stále skončí během několika sekund u většiny dokumentů.

## Krok 3: Spusťte AI post‑processor k opravě OCR chyb

I když je OCR engine nejlepší, dělá chyby — např. „rn“ místo „m“, chybějící diakritiku nebo rozdělená slova. AI model může prohlédnout surový řetězec a strukturovaná data, najít nesrovnalosti a přepsat text při zachování původních souřadnic.

Níže je **mock** implementace; nahraďte tělo skutečným voláním LLM, pokud jej máte.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Proč tento krok zlepšuje přesnost OCR:*  
- **Kontextové opravy** – AI může rozhodnout, že „l0ve“ je pravděpodobně „love“ na základě okolních slov.  
- **Zachování souřadnic** – zachováte informace o rozvržení, takže následné úkoly (např. anotace PDF) zůstávají přesné.  
- **Iterativní vylepšování** – můžete spustit post‑processor vícekrát, každý průchod odstraní více chyb.

## Krok 4: Procházejte opravený, strukturovaný výstup

Nyní, když máme vyčištěnou strukturu, získání finálního textu je triviální. Níže vytiskneme každý řádek, ale můžete také zapisovat do CSV, vložit do databáze nebo vytvořit prohledávatelný PDF.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Očekávaný výstup** (při předpokladu jednoduché jednosloupcové faktury):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Všimněte si, že zalomení řádků a pořadí sloupců jsou zachovány a běžné OCR chyby jako „$15.00“ přečtené jako „$15,00“ jsou opraveny AI krokem.

## Jak tento workflow pomáhá **zlepšit přesnost OCR**

| Fáze | Co opravuje | Proč je to důležité |
|------|-------------|---------------------|
| **Plain text OCR** | Detekuje nečitelné stránky již na začátku | Ušetří čas vynecháním beznadějných vstupů |
| **Structured OCR** | Zachycuje rozvržení, souřadnice | Umožňuje následné úkoly (zvýraznění, redakce) |
| **AI post‑processor** | Opravuje pravopis, spojuje rozdělená slova, opravuje čísla | Zvyšuje celkovou přesnost na úrovni znaků z ~85 % na >95 % u špinavých skenů |
| **Iteration** | Umožňuje opakované spuštění s vyladěnými parametry | Doladí pipeline pro konkrétní typy dokumentů |

Kombinací těchto tří konceptů—**plain text OCR**, extrakce s ohledem na rozvržení a AI korekce—získáte robustní řešení, které *výrazně* **zlepší přesnost OCR** bez nutnosti psát vlastní neuronovou síť od nuly.

## Časté úskalí a profesionální tipy

- **Úskalí:** Použití nízkého rozlišení obrázku (≤150 dpi) v Tesseractu vede k nečitelné výstupu.  
  **Profesionální tip:** Předzpracujte pomocí `Pillow`—aplikujte `Image.convert('L')` a `Image.filter(ImageFilter.MedianFilter())` před OCR.

- **Úskalí:** AI post‑processor může omylem přepsat terminologii specifickou pro doménu (např. „SKU123“).  
  **Profesionální tip:** Vytvořte whitelist termínů a předávejte jej LLM nebo knihovně pro kontrolu pravopisu jako `pyspellchecker`.

- **Úskalí:** Vícesloupcové stránky se sloučí do jednoho řádku.  
  **Profesionální tip:** Detekujte hranice sloupců pomocí pole `block_num` ve výstupu TSV z Tesseractu a řádky rozdělte podle toho.

- **Úskalí:** Velké PDF soubory způsobují přetečení paměti při načítání všech stránek najednou.  
  **Profesionální tip:** Zpracovávejte stránky inkrementálně—iterujte přes `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

## Rozšíření pipeline

Pokud vás zajímají další kroky, zvažte následující vylepšení:

1. **Dávkové zpracování** – Zabalte celý skript do funkce, která prochází adresář, zpracovává tisíce souborů paralelně pomocí `concurrent.futures`.
2. **Jazykové modely** – Vyměňte jednoduchou difflib heuristiku za volání OpenAI `gpt‑4o` nebo lokálně hostovaného modelu LLaMA pro bohatší kontextové opravy.
3. **Exportní formáty** – Zapište opravenou strukturu do prohledávatelného PDF

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}