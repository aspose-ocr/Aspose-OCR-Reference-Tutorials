---
category: general
date: 2026-07-05
description: Jak vypsat modely pomocí Aspose AI, povolit automatické stahování a stáhnout
  model z Hugging Face v Pythonu. Postupujte podle tohoto krok‑za‑krokem tutoriálu,
  nastavte mezipaměť a začněte ještě dnes používat Aspose AI.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: cs
og_description: Jak vypsat modely pomocí Aspose AI, povolit automatické stahování
  a stáhnout model z Hugging Face. Naučte se nastavit mezipaměť a používat Aspose
  AI během několika minut.
og_title: Jak vypsat modely s Aspose AI – kompletní návod
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Jak vypsat modely s Aspose AI – Kompletní průvodce
url: /cs/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vypsat modely pomocí Aspose AI – Kompletní průvodce

Jak vypsat modely pomocí Aspose AI je otázka, která se objeví, jakmile začnete experimentovat s velkými jazykovými modely v Pythonu. V tomto tutoriálu vás provedeme povolením **auto download**, konfigurací lokální cache a stažením modelu přímo z Hugging Face—aby jste mohli začít pracovat, aniž byste museli ručně hledat soubory.

Pokud jste se někdy ptali *„jak použít Aspose pro OCR‑řízenou AI?“* nebo *„jaký je nejjednodušší způsob, jak nastavit cache pro soubory modelů?“* jste na správném místě. Na konci budete mít plně funkční skript, který vypíše každý model uložený lokálně, automaticky stáhne chybějící a ukáže vám přesně, kde soubory na disku žijí.

---

## Co budete potřebovat

- Python 3.9 nebo novější (knihovna používá typové nápovědy, které vyžadují aktuální interpretátor)
- `pip` přístup k instalaci balíčku **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Internetové připojení pro první stažení z Hugging Face.
- Složka, kde chcete uchovávat cache modelů (např. `./model_cache`).

To je vše—žádné extra Docker kontejnery, žádná těžkopádná virtuální prostředí nad rámec čisté instalace Pythonu.

---

## ## Jak vypsat modely s Aspose AI

Jádrem tohoto průvodce je schopnost **vypsat modely**, které Aspose AI uložil lokálně do cache. Jakmile je cache nastavena, knihovna může vyjmenovat vše, co zná, což usnadňuje ladění a správu verzí.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Proč to funguje:**  
- `AsposeAI()` vytváří vysokou úroveň vstupního bodu, který komunikuje s podkladovým inference engine.  
- `AsposeAIModelConfig()` obsahuje všechna nastavení, která můžete měnit; nastavení `allow_auto_download` na `"true"` říká knihovně, aby automaticky stáhla chybějící soubory z úložiště, které určíte.  
- `directory_model_path` je *adresář cache*—místo, kde jsou uloženy všechny stažené binární soubory.  
- `initialize()` aplikuje konfiguraci a provede první stažení, pokud je cache prázdná.  
- Nakonec `list_local()` prohledá složku cache a vrátí Python seznam identifikátorů modelů, který vytiskneme.

### Očekávaný výstup (první spuštění)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Pokud skript spustíte znovu, knihovna přeskočí stažení a jednoduše vypíše již existující model, což dokazuje, že **nastavení cache** se opravdu vyplatí při dalších spuštěních.

---

## ## Povolit automatické stahování chybějících modelů

Často budete pracovat s několika modely napříč projekty. Ruční stahování každého z Hugging Face může být únavné. Povolením automatického stahování se Aspose AI postará o těžkou práci.

```python
cfg.allow_auto_download = "true"
```

> **Tip:** Nechte `allow_auto_download` nastavený na `"true"` **pouze** v vývojových nebo CI prostředích. V produkci možná budete chtít cache uzamknout, aby se předešlo neočekávanému síťovému provozu.

Pokud se později rozhodnete jej vypnout, stačí nastavit příznak na `"false"` před opětovným voláním `initialize()`.

---

## ## Stáhnout model z Hugging Face za běhu

Řádek

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

říká Aspose AI, z kterého vzdáleného úložiště má stahovat. Knihovna podporuje jakýkoli veřejný model na Hugging Face, který poskytuje soubor GGUF. Chcete jiný model? Vyměňte ID repozitáře:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Když spustíte skript, Aspose AI kontroluje cache:

- **Pokud model existuje**, načte jej okamžitě.  
- **Pokud neexistuje**, příznak auto‑download spustí stažení, uloží soubor do `directory_model_path` a poté jej zaregistruje pro okamžité použití.

Tento přístup eliminuje dvoustupňový proces „stáhnout‑pak‑spustit“, který vás nutí mnoho tutoriálů.

---

## ## Jak použít Aspose AI po vypsání modelu

Vypsání modelů je jen polovina příběhu. Jakmile víte, že model je přítomen, můžete zahájit inference:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Proč je to důležité:**  
- `run_inference()` abstrahuje tokenizaci, dávkování a správu GPU.  
- Předáním *jména modelu*, které jste získali z `list_local()`, zajistíte, že volání inference odpovídá přesnému souboru na disku.

---

## ## Jak nastavit umístění cache pro více projektů

Pokud spravujete několik projektů, možná budete chtít, aby každý měl vlastní složku cache. Pole `directory_model_path` je jen obyčejný řetězec, takže jej můžete vytvořit dynamicky:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Nyní každý projekt získá izolovanou podsložku (`./model_cache/sentiment_analysis`), což zabraňuje konfliktům verzí a usnadňuje úklid.

---

## ## Časté úskalí a jak se jim vyhnout

| Symptom | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| **`PermissionError` when accessing cache** | Složka cache patří jinému uživateli (běžné na sdílených serverech) | Vytvořte složku ručně s odpovídajícími oprávněními: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` nastaven na `"false"` a model ještě není v cache | Dočasně zapněte příznak, spusťte jednou, poté jej podle potřeby vypněte |
| **Unexpected model version** | Dva různé repozitáře sdílejí stejný název, ale mají různé soubory | Upevněte konkrétní ID repozitáře (včetně tagu/commitu) nebo uzamkněte cache vypnutím auto‑download po prvním úspěšném stažení |
| **Out‑of‑memory errors** | Velké soubory GGUF na stroji bez dostatečné RAM/VRAM | Použijte menší model (např. `Qwen2.5-1.5B`) nebo nastavte `cfg.device = "cpu"` pro vynucení inference na CPU |

---

## ## Kompletní skript, který můžete zkopírovat a vložit

Níže je kompletní, připravený příklad, který zahrnuje všechny výše uvedené koncepty. Uložte jej jako `list_models_demo.py` a spusťte pomocí `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Spuštěním** získáte výstup podobný předchozímu příkladu, následovaný stručnou odpovědí od modelu. Klidně nahraďte prompt čímkoli chcete—toto je nejrychlejší způsob, jak otestovat, že je model skutečně použitelný poté, co jste **vypsali modely**.

---

## ## Shrnutí

Probrali jsme vše, co potřebujete k **vypsání modelů** pomocí Aspose AI, od povolení **auto download** po konfiguraci trvalé **cache** a stažení **modelu z Hugging Face** na vyžádání. Hlavní body:

1. Vytvořte objekt `AsposeAI` a `AsposeAIModelConfig`.  
2. Nastavte `allow_auto_download = "true"` a nasměrujte `directory_model_path` do složky, kterou ovládáte.  
3. Inicializujte AI, poté zavolejte `list_local()`, abyste viděli, co je v cache.  
4. Použijte jméno modelu získané z výpisu pro inference a jste připraveni vytvářet reálné aplikace.

---

## Co dál?

- **Experimentujte s různými modely** – vyměňte `cfg.hugging_face_repo_id` za jiný repozitář a podívejte se, jak se seznam změní.
- **Doladit cache**

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}