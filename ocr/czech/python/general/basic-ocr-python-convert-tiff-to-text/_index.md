---
category: general
date: 2026-03-18
description: Základní OCR tutoriál v Pythonu ukazuje, jak převést TIFF na text, načíst
  OCR obrázku, nastavit vrstvy GPU a opravit úvodní nuly pomocí Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: cs
og_description: Základní tutoriál OCR v Pythonu vás provede převodem souborů TIFF
  na čistý text, načítáním obrázků, nastavením GPU vrstev a opravou úvodních nul.
og_title: Základní OCR v Pythonu – převod TIFF na text
tags:
- OCR
- Python
- AI
- Aspose
title: základní OCR v Pythonu – převod TIFF na text
url: /cs/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Převod TIFF na Text s AI Post‑Processingem

Hledáte způsob, jak provést **basic ocr python** na vašich naskenovaných dokumentech? V tomto průvodci vás provedeme převodem souboru TIFF na čistý, prohledávatelný text pomocí Aspose OCR a AI post‑processoru.  

Pokud jste někdy měli potíže **convert TIFF to text**, protože surový výstup je plný překlepů nebo podivných znaků, nejste v tom sami. Ukážeme vám také, jak **load image OCR**, upravit engine pomocí **set GPU layers**, a dokonce **fix leading zeroes**, které se často objevují v číslech faktur.

## Co se naučíte

- Jak inicializovat Aspose OCR engine pro tištěné dokumenty.  
- Přesné kroky k **load image OCR** z TIFF souboru a získání surového textu.  
- Konfigurace AI modelu, jeho automatické stažení a **setting GPU layers** pro rychlejší inferenci.  
- Přidání vestavěného spell‑checku plus vlastní funkce, která **fixes leading zeroes**.  
- Čištění OCR výsledku a správné uvolnění prostředků.  

Na konci tohoto tutoriálu budete mít jeden, znovupoužitelný Python skript, který převádí libovolný TIFF na upravený, prohledávatelný text – bez nutnosti ručního kopírování a vkládání.

### Požadavky

- Python 3.8+ nainstalovaný na vašem počítači.  
- `aspose-ocr` balíček (`pip install aspose-ocr`).  
- Volitelné: GPU s alespoň 4 GB VRAM, pokud chcete **set GPU layers**; jinak kód automaticky přejde na CPU.

---

## basic ocr python – načtení obrazu a rozpoznání textu

Prvním krokem je **load image OCR**, aby engine mohl číst pixely. `OcrEngine` od Aspose podporuje mnoho formátů, ale zde se zaměřujeme na TIFF, protože je nejčastější pro naskenované faktury.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Tip:** Pokud pracujete s multi‑page TIFFy, Aspose je automaticky zpracovává po jedné v sekvenci, takže nepotřebujete další smyčky.

Jakmile je obrázek načten, spustíme základní rozpoznávací průchod.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Uvidíte něco jako:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Všimněte si *nul* před písmeny? To je klasický OCR artefakt, který později vyčistíme.

![basic ocr python workflow](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Krok 2: Convert TIFF to text – připravte AI post‑processor

Surový OCR je užitečný, ale většina produkčních pipeline potřebuje upravenou verzi. Aspose poskytuje `AsposeAI` wrapper, který může stáhnout model z Hugging Face, spustit jej na GPU a automaticky aplikovat spell‑check.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Proč je důležité `set GPU layers`

Parametr `gpu_layers` říká podkladovému GGUF modelu, kolik transformerových vrstev má zůstat na GPU. Více vrstev = rychlejší inference, ale vyšší využití VRAM. Pokud používáte skromný notebook, snižte hodnotu na `10` nebo ji úplně vynechte, aby se model spouštěl na CPU.

---

## Krok 3: Aplikujte spellcheck a **fix leading zeroes**

Aspose AI obsahuje vestavěný spell‑checker, který zachytí většinu anglických překlepů. Nicméně doménově specifické opravy – například změna úvodní `0` na `O` u kódů faktur – vyžadují vlastní post‑processor.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Proč to funguje:** Regulární výraz hledá hranici slova (`\b`), nulu a pak přesně tři velká písmena. Poté nulu nahradí písmenem „O“. Můžete rozšířit vzor pro další zvláštnosti (např. `0[0-9]{2}` pro chybně přečtená čísla).

---

## Krok 4: Vyčistěte OCR výsledek pomocí AI post‑processoru

Nyní spojíme vše: surový řetězec z **basic ocr python**, spell‑check a naši opravu nul. Metoda `run_postprocessor` vrátí vyčištěnou verzi připravenou pro downstream systémy.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typický výstup po post‑processoru:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Můžete vidět, že úvodní nula se změnila na `O` a běžné překlepy jsou opraveny. Text je nyní vhodný pro indexaci ve vyhledávači nebo pro vstup do pipeline pro extrakci dat.

---

## Krok 5: Uvolněte AI zdroje – udržte GPU spokojené

Pokud spouštíte více OCR úloh v dlouhodobé službě, je dobré po dokončení uvolnit GPU paměť modelu.

```python
ocr_ai.free_resources()
```

Přeskočení tohoto kroku může vést k chybám „out‑of‑memory“ při následných voláních, zejména když je **set GPU layers** nastaveno na vysokou hodnotu.

---

## Volitelné varianty a okrajové případy

| Situation | What to change |
|-----------|----------------|
| **Handwritten documents** | Použijte `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` místo `PRINTED`. |
| **No GPU available** | Nastavte `gpu_layers=0` nebo argument vynechte; model poběží na CPU (pomalejší, ale bezpečné). |
| **Different language** | Vyměňte Hugging Face repo ID za model specifický pro jazyk, např. `microsoft/Florence-2-base`. |
| **Batch processing** | Zabalte kroky do smyčky `for file in glob("*.tif"):` a shromažďujte výsledky do seznamu nebo CSV. |
| **More complex zero patterns** | Rozšiřte `invoice_fix` o další regexy, např. `r"\b0+([A-Z]{2,})\b"` pro více úvodních nul. |

---

## Závěr

Právě jsme dokončili **basic ocr python** pipeline, která načte TIFF, extrahuje surový text a poté jej vyčistí pomocí AI modelu při **setting GPU layers** pro výkon. Vlastní post‑processor ukazuje, jak **fix leading zeroes**, což je malý, ale často přehlížený detail, který může narušit downstream analytiku.

Neváhejte experimentovat: vyzkoušejte jinou kvantizaci (`float16` pro vyšší přesnost), vyměňte spell‑check za doménově specifický slovník, nebo propojte více vlastních oprav. Vzor zůstává stejný – načíst, rozpoznat, nakonfigurovat AI, post‑process a vyčistit.

**Další kroky**, které můžete prozkoumat, zahrnují:
- Integraci vyčištěného výstupu s databází nebo Elasticsearch indexem.  
- Použití stejného přístupu k **convert TIFF to text** pro multi‑language PDFy.  
- Přidání UI s Flask nebo FastAPI, aby ne‑technickí uživatelé mohli nahrávat soubory a okamžitě získat vyčištěný text.

Šťastné kódování a ať jsou vaše OCR výsledky vždy ostré a bez nul!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}