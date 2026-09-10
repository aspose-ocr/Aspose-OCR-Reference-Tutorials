---
category: general
date: 2026-01-12
description: Jak spustit OCR a extrahovat text z obrázků faktur pomocí Aspose OCR
  a lehkého modelu Hugging Face. Naučte se stáhnout model, opravit chyby OCR a provést
  OCR na obrázku.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: cs
og_description: Jak spustit OCR na obrázcích faktur, extrahovat text a opravit chyby
  pomocí LLM od Hugging Face. Postupujte podle tohoto kompletního průvodce pro bezchybné
  výsledky.
og_title: Jak spustit OCR na obrázcích faktur – kompletní návod
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Jak spustit OCR na obrázcích faktur – Kompletní průvodce krok za krokem
url: /cs/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR na obrázcích faktur – Kompletní krok‑za‑krokem průvodce

Už jste se někdy zamysleli, **jak spustit OCR** na naskenované faktuře a získat čistý, prohledávatelný text, aniž byste strávili hodiny jeho úpravou? Nejste v tom sami. V mnoha reálných projektech je výstup surového OCR plný chyb rozpoznávání – například „O“ místo „0“, „l“ místo „1“ nebo dokonce celé slova zkomolená. Dobrá zpráva? Několika řádky Pythonu můžete nejen **provádět OCR na obrázku** souborů, ale také automaticky **opravit chyby OCR** pomocí lehkého modelu od Hugging Face.

V tomto tutoriálu vás provedeme vším, co potřebujete vědět: od načtení obrázku faktury, extrakce surového textu, stažení kvantovaného modelu až po vylepšení výsledku, abyste získali dokonalou transkripci připravenou pro další zpracování. Na konci budete schopni **extrahovat text z faktury** z PDF nebo PNG v jediném, opakovatelném skriptu.

## Požadavky a nastavení

| Požadavek | Proč je důležité |
|-------------|----------------|
| Python 3.9+ | Moderní syntaxe a typové nápovědy |
| `aspose-ocr` balíček | Poskytuje `ocr.OcrEngine` používaný v příkladu |
| `aspose-ai` balíček | Dodává post‑processor `AsposeAI` |
| Přístup k GPU (volitelný) | Zrychluje vrstvy LLM; jinak CPU funguje dobře |
| Internetové připojení (první spuštění) | Potřebné k automatickému **stažení modelu Hugging Face** |

You can install the required libraries with:

```bash
pip install aspose-ocr aspose-ai
```

> **Tip:** Pokud plánujete spouštět LLM na GPU, nainstalujte `torch` s podporou CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Now that the environment is ready, let’s get into the code.

---

## Krok 1 – Inicializace enginu a načtení obrázku faktury

Prvním krokem je vytvořit instanci OCR enginu od Aspose a nasměrovat ji na soubor, který chcete zpracovat. Tento krok je základem **jak spustit OCR** na libovolném obrázku.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Proč je to důležité:** `load_image` přijímá PNG, JPEG, TIFF a dokonce i stránky PDF, což vám umožní **provádět OCR na obrázku** bez ohledu na formát.

---

## Krok 2 – Spuštění základního OCR pro zachycení surového textu

Jakmile je obrázek načten, engine může vytvořit surovou transkripci. Tento výstup je často hlučný, proto později provedeme krok korekce.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typický surový výstup může vypadat takto:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Všimněte si nul (`0`) tam, kde by měla být číslice „O“? To je přesně ten typ chyby, kterou později opravíme.

---

## Krok 3 – Nastavení AI post‑processoru s lehkým LLM

Nyní přinášíme **stažení modelu Hugging Face**, který je dostatečně malý na běh na skromném hardware, ale zároveň dostatečně výkonný, aby rozuměl jazyku faktur. Příklad používá model Qwen 2.5 3B‑Instruct GGUF, kvantovaný na `int8` pro minimální paměťovou stopu.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Proč tento model?** Kvantizace `int8` zmenší soubor na ~1,2 GB, což je proveditelné na většině notebooků. GPU vrstvy urychlují inferenci, ale kód se elegantně vrátí na CPU, pokud není GPU nalezeno.

---

## Krok 4 – Spuštění korekce založené na LLM na surový OCR výsledek

S připraveným modelem předáme surový text do post‑processoru. LLM přepíše transkripci, opraví běžné OCR chyby a normalizuje čísla.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Očekávaný vyčištěný výstup:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Vidíte, že nuly se změnily zpět na písmeno „O“ a „Am0unt“ je nyní „Amount“. Toto je jádro **automatické opravy OCR chyb**.

---

## Krok 5 – Uvolnění prostředků a úklid

Velké jazykové modely mohou držet GPU paměť, takže je dobré po dokončení uvolnit prostředky.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Pokud plánujete zpracovávat mnoho faktur najednou, můžete model nechat načtený a uvolnit jej až na konci skriptu.

---

## Kompletní funkční příklad

Spojením všeho dohromady, zde je jediný skript, který můžete vložit do souboru `.py` a spustit:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Spuštěním skriptu by měl být výstup podobný bloku „AI‑opravený“ zobrazenému dříve. Klidně zaměňte cestu k obrázku za jakoukoli jinou fakturu nebo účtenku, abyste **extrahovali text z faktur** souborů hromadně.

---

## Často kladené otázky a okrajové případy

### Co když nemám GPU?

`gpu_layers` parametr je volitelný. Nastavte jej na `0` nebo jej vynechejte a model poběží kompletně na CPU. Očekávejte pomalejší inferenci – přibližně 2–3 sekundy na stránku na moderním notebooku.

### Moje faktury jsou více‑stránkové PDF. Jak je zpracovat?

Převěďte každou stránku na samostatný obrázek (např. pomocí `pdf2image`) a projděte stránky ve stejném skriptu. OCR engine může zpracovat každý obrázek nezávisle a LLM opraví každý blok textu.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Stahování modelu selže za firewallem?

Stáhněte model ručně z Hugging Face model hub, rozbalte jej do lokální složky a nastavte `hugging_face_repo_id` na lokální cestu:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Jak přesná je korekce?

Pro typické faktury v angličtině LLM opraví >95 % běžných OCR chyb. Komplexní ručně psané poznámky mohou stále vyžadovat ruční kontrolu.

## Tipy a triky pro produkční použití

- **Dávkové zpracování:** Zabalte kroky 2‑4 do funkce a předávejte seznam cest k souborům. Znovu použijte stejnou instanci `AsposeAI`, abyste se vyhnuli opětovnému načítání modelu.
- **Logování:** Nahraďte `print` Pythonovým modulem `logging`, abyste zachytili jak surové, tak opravené výstupy pro auditní záznamy.
- **Zpracování chyb:** Obalte volání OCR bloky `try/except`. Pokud selže obrázek, zaznamenejte název souboru a pokračujte.
- **Ladění výkonu:** Experimentujte s `gpu_layers`. Více vrstev na GPU urychlí inferenci, ale zvýší využití VRAM.

## Závěr

Probrali jsme **jak spustit OCR** na obrázcích faktur od začátku do konce, ukázali vám, jak **provádět OCR na obrázku**, **stáhnout model Hugging Face** a **automaticky opravit OCR chyby**. Kompletní skript demonstruje praktický workflow, který můžete vložit do libovolného Python‑založeného automatizačního pipeline.

Další kroky? Zkuste rozšířit pipeline o **extrakci klíčových polí** (číslo faktury, datum, celková částka) pomocí regulárních výrazů na opraveném textu, nebo vložte vyčištěný výstup do databáze pro prohledávatelné záznamy. Můžete také experimentovat s dalšími lehkými LLM z Hugging Face, pokud potřebujete jiný jazyk nebo doménově specifické znalosti.

Šťastné kódování a ať jsou vaše OCR výsledky vždy krystalicky čisté! 

![jak spustit OCR na obrázku faktury](ocr_invoice_example.png "jak spustit OCR na faktuře")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}