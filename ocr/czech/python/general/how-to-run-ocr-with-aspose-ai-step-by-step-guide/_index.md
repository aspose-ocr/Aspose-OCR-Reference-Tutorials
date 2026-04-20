---
category: general
date: 2026-02-09
description: jak spustit OCR pomocí Aspose AI a modelu Hugging Face – naučte se stáhnout
  model Hugging Face, opravit chyby OCR a uvolnit paměť GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: cs
og_description: Jak spustit OCR s Aspose AI je vysvětleno v prvním odstavci – zjistěte,
  jak stáhnout model Hugging Face, opravit chyby OCR a uvolnit paměť GPU.
og_title: Jak spustit OCR s Aspose AI – kompletní průvodce
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Jak spustit OCR s Aspose AI – krok za krokem průvodce
url: /cs/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak spustit OCR s Aspose AI – Kompletní průvodce

Už jste se někdy zamysleli **jak spustit OCR** na naskenované faktuře a získat naprosto čistá čísla, aniž byste strávili hodiny opravováním překlepů? Nejste v tom sami. V mnoha reálných projektech surový text, který vyjde z klasického OCR enginu, stále obsahuje cizí znaky, poškozené symboly měn nebo zkreslené číslice — obzvláště když je zdrojový obrázek šumivý.

Dobrou zprávou je, že můžete připojit LLM k Aspose OCR, stáhnout model z Hugging Face za běhu a nechat AI vylepšit výstup za vás. V tomto tutoriálu projdeme celým pipeline, od stažení modelu (ano, ukážeme vám, jak **download hugging face model** automaticky) až po uvolnění GPU zdrojů, když skončíte. Na konci budete mít reprodukovatelný skript, který **corrects OCR errors**, běží rychle na skromném GPU a uklízí po sobě, abyste neztráceli paměť.

## Co se naučíte

- Nakonfigurujte Aspose AI tak, aby načetl model **Qwen2.5‑3B‑Instruct‑GGUF** z Hugging Face.
- Spusťte standardní Aspose OCR engine na souboru s obrázkem.
- Použijte vlastní LLM prompt, který zachová čísla a symboly měn beze změny.
- Uvolněte GPU paměť pomocí vestavěné rutiny **free gpu memory**.
- Vyladíte workflow pro okrajové případy, jako jsou vícestránkové PDF nebo nízko výkonné GPU.

> **Prerequisites** – Python 3.9+, balíček `aspose-ocr`, přístup k internetu pro první stažení modelu a GPU s alespoň 4 GB VRAM (volitelné, ale doporučené). Pokud nemáte GPU, skript automaticky přejde na CPU pro zbývající vrstvy.

---

## Jak spustit OCR a vylepšit výsledky

Níže je kompletní, připravený Python skript. Uložte jej jako `ocr_with_ai.py` a nahraďte placeholder cesty svými vlastními soubory.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Parametr `gpu_layers` vám umožní rozhodnout, kolik transformerových vrstev zůstane na GPU. Pokud narazíte na chyby out‑of‑memory, snižte toto číslo a zbytek poběží na CPU — stále budete **free gpu memory** později pomocí `ai.free_resources()`.

### Očekávaný výstup

Spuštění skriptu na ukázkové faktuře vrátí něco jako:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Všimněte si, jak AI opravil „O“ v `$1O0.00` na správnou nulu při zachování dolarového znaku. To je podstata **correct OCR errors** pro finanční dokumenty.

---

## Stáhnout model z Hugging Face – Co se děje pod kapotou?

Když nastavíte `allow_auto_download="true"`, wrapper Aspose AI zkontroluje `directory_model_path`. Pokud modelové soubory nejsou přítomny, kontaktuje Hugging Face Hub, stáhne **int8‑quantized** verzi `Qwen2.5‑3B‑Instruct‑GGUF` a uloží ji lokálně. Toto jednorázové stažení je obvykle pod 2 GB, což je proveditelné i na skromných SSD.

> **Why int8?** Kvantování na 8‑bit výrazně snižuje využití paměti — klíčové, když chcete také **free gpu memory** po zpracování. Kompromis je mírný pokles přesnosti, ale pro post‑processing OCR textu je dopad zanedbatelný.

Pokud raději hostujete model sami, jednoduše vložte soubory `.gguf` do `YOUR_DIRECTORY/Models` a Aspose je načte bez dalšího přístupu k internetu.

---

## Jak uvolnit GPU – Nejlepší postupy

GPU zdroje jsou na mnoha pracovních stanicích sdíleným komoditním zdrojem. Nezrušení tensorů po dokončení skriptu může způsobit chyby „CUDA out of memory“ pro následné úlohy. Volání `ai.free_resources()` provádí tři věci:

1. **Disposes the underlying transformer** – všechny váhy residentní na GPU jsou uvolněny.
2. **Clears the PyTorch cache** – interně se volá `torch.cuda.empty_cache()`.
3. **Deletes temporary files** – všechny dočasné soubory vytvořené během stahování jsou odstraněny.

Můžete také ručně vyvolat `torch.cuda.empty_cache()`, pokud kombinujete Aspose AI s jinými PyTorch úlohami, ale vestavěná metoda je obvykle dostačující.

---

## Krok‑za‑krokem průvodce (H2 s sekundárními klíčovými slovy)

### Automaticky stáhnout model z Hugging Face

Konstruktor `AsposeAIModelConfig` skrývá složitost práce s Hugging Face API. Jen se ujistěte, že máte přístup k internetu při prvním spuštění skriptu. Poté model žije v `YOUR_DIRECTORY/Models` a následná spuštění startují okamžitě.

### Uvolnit GPU paměť po inferenci

Pokud to spouštíte uvnitř dlouho běžící služby (např. Flask API), zavolejte `ai.free_resources()` po každém požadavku. To zabraňuje únikům paměti a zajišťuje, že další požadavek může znovu použít stejný GPU bez problémů.

### Opravit OCR chyby pomocí vlastního promptu

Naše funkce `financial_prompt` vrací slovník s jediným klíčem `prompt`. Můžete ji přizpůsobit pro jakýkoli obor:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Zaměňte název funkce v `ai.set_post_processor(...)` a získáte pipeline **correct OCR errors** pro lékařské záznamy.

### Jak spustit OCR na vícestránkových PDF

Aspose OCR může zpracovávat PDF přímo:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Po získání surového řetězce stejný LLM post‑processor vyčistí text každé stránky. Není potřeba žádný další kód.

### Když nemáte GPU – Jak uvolnit GPU (i bez něj)

I na strojích pouze s CPU je volání `ai.free_resources()` neškodné. Jednoduše vyčistí interní cache, což může stále uvolnit RAM. Takže rada **how to free gpu** platí univerzálně: vždy po sobě uklízejte.

---

## Časté úskalí a jak jsme je vyřešili

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory na GPU** | `gpu_layers` nastaveno příliš vysoko pro vaši kartu | Snižte `gpu_layers` na 10 nebo 5, zbytek nechte běžet na CPU |
| **Model se nikdy nestáhne** | Firewally ve firmě blokují HTTPS na huggingface.co | Stáhněte model ručně na jiné síti a poté nastavte `directory_model_path` na lokální složku |
| **Čísla se poškozují** | Prompt není dostatečně explicitní ohledně zachování číslic | Přidejte do promptu „preserve all numeric values and currency symbols exactly as they appear“ |
| **`free_resources` raises an exception** | Používáte starší verzi Aspose OCR | Aktualizujte na nejnovější balíček `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## Kompletní přehled příkladu

Zde je skript znovu, tentokrát s inline komentáři, které vysvětlují každý řádek pro budoucí referenci:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Závěr

Probrali jsme **how to run OCR** s Aspose, stažení modelu z Hugging Face na vyžádání, vytvoření promptu, který **corrects OCR errors**, a nakonec **free gpu memory**, aby vaše pracovní stanice zůstala responzivní. celý workflow se vejde do jediného, samostatného Python souboru — žádné externí skripty, žádná ruční manipulace s modelem a žádné zbylé alokace GPU.

Další kroky? Zkuste vyměnit `financial_prompt` za

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}