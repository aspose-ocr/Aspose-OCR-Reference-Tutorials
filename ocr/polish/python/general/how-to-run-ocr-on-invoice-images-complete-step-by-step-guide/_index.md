---
category: general
date: 2026-01-12
description: Jak uruchomić OCR i wyodrębnić tekst z obrazów faktur przy użyciu Aspose
  OCR oraz lekkiego modelu Hugging Face. Dowiedz się, jak pobrać model, poprawić błędy
  OCR i wykonać OCR na obrazie.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: pl
og_description: Jak przeprowadzić OCR na zdjęciach faktur, wyodrębnić tekst i naprawić
  błędy przy użyciu modelu LLM Hugging Face. Postępuj zgodnie z tym kompletnym przewodnikiem,
  aby uzyskać bezbłędne wyniki.
og_title: Jak uruchomić OCR na obrazach faktur – pełny poradnik
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Jak przeprowadzić OCR na zdjęciach faktur – Kompletny przewodnik krok po kroku
url: /pl/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR na obrazach faktur – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś, **jak uruchomić OCR** na zeskanowanej fakturze i uzyskać czysty, przeszukiwalny tekst bez spędzania godzin na jego czyszczeniu? Nie jesteś jedyny. W wielu projektach w rzeczywistym świecie surowe wyniki OCR są pełne błędów rozpoznawania — np. „O” zamiast „0”, „l” zamiast „1”, a nawet całe słowa są zniekształcone. Dobra wiadomość? Kilka linii Pythona pozwala nie tylko **wykonywać OCR na obrazie**, ale także automatycznie **korygować błędy OCR** przy użyciu lekkiego modelu z Hugging Face.

W tym samouczku przeprowadzimy Cię przez wszystko, co musisz wiedzieć: od wczytania obrazu faktury, wyodrębnienia surowego tekstu, pobrania modelu kwantyzowanego, po dopracowanie wyniku, tak abyś otrzymał idealną transkrypcję gotową do dalszego przetwarzania. Po zakończeniu będziesz w stanie **extract text from invoice** PDF‑ów lub PNG w jednym, powtarzalnym skrypcie.

## Wymagania wstępne i konfiguracja

Before diving in, make sure you have:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| Python 3.9+ | Nowoczesna składnia i wskazówki typów |
| `aspose-ocr` package | Udostępnia `ocr.OcrEngine` używany w przykładzie |
| `aspose-ai` package | Dostarcza post‑procesor `AsposeAI` |
| Access to a GPU (optional) | Przyspiesza warstwy LLM; w przeciwnym razie CPU działa wystarczająco |
| Internet connection (first run) | Wymagane do **download Hugging Face model** automatycznie |

Możesz zainstalować wymagane biblioteki za pomocą:

```bash
pip install aspose-ocr aspose-ai
```

> **Wskazówka:** Jeśli planujesz uruchomić LLM na GPU, zainstaluj `torch` z obsługą CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Teraz, gdy środowisko jest gotowe, przejdźmy do kodu.

---

## Krok 1 – Inicjalizacja silnika OCR i wczytanie obrazu faktury

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji silnika OCR firmy Aspose i skierowanie go na plik, który chcesz przetworzyć. Ten krok jest podstawą **how to run OCR** na dowolnym obrazie.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Dlaczego to ważne:** `load_image` akceptuje PNG, JPEG, TIFF, a nawet strony PDF, pozwalając Ci **perform OCR on image** dane niezależnie od formatu.

---

## Krok 2 – Uruchom podstawowy OCR, aby uzyskać surowy tekst

Po wczytaniu obrazu silnik może wygenerować surową transkrypcję. Ten wynik jest często zaszumiony, dlatego później uruchomimy krok korekcji.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typowy surowy wynik może wyglądać tak:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Zauważasz zera (`0`) tam, gdzie powinna być litera „O”? To dokładnie taki błąd, który naprawimy później.

---

## Krok 3 – Skonfiguruj post‑procesor AI z lekkim LLM

Teraz wprowadzamy **download Hugging Face model**, który jest wystarczająco mały, aby działać na skromnym sprzęcie, ale jednocześnie wystarczająco potężny, by rozumieć język faktur. Przykład używa modelu Qwen 2.5 3B‑Instruct GGUF, kwantyzowanego do `int8` dla niewielkiego zużycia pamięci.

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

> **Dlaczego ten model?** Kwantyzacja `int8` zmniejsza plik do ~1,2 GB, co czyni go wykonalnym na większości laptopów. Warstwy GPU przyspieszają wnioskowanie, ale kod elegancko przełącza się na CPU, gdy nie wykryto GPU.

---

## Krok 4 – Uruchom korekcję opartą na LLM na surowym wyniku OCR

Gdy model jest gotowy, podajemy surowy tekst do post‑procesora. LLM przepisze transkrypcję, naprawiając typowe błędy OCR i normalizując liczby.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Oczekiwany wyczyszczony wynik:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Widzisz, że zera zamieniły się z powrotem w literę „O”, a „Am0unt” jest teraz „Amount”. To jest sedno **correct OCR errors** automatycznie.

---

## Krok 5 – Zwolnij zasoby i posprzątaj

Duże modele językowe mogą zajmować pamięć GPU, więc dobrą praktyką jest zwolnienie zasobów po zakończeniu.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Jeśli planujesz przetwarzać wiele faktur w partii, możesz pozostawić model załadowany i zwolnić go dopiero na samym końcu skryptu.

---

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy skrypt, który możesz wkleić do pliku `.py` i uruchomić:

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

Uruchomienie skryptu powinno wygenerować wyjście podobne do bloku „AI‑corrected” pokazanego wcześniej. Śmiało zamień ścieżkę obrazu na dowolną inną fakturę lub paragon, aby **extract text from invoice** pliki masowo.

---

## Najczęściej zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli nie mam GPU?

Parametr `gpu_layers` jest opcjonalny. Ustaw go na `0` lub pomiń, a model będzie działał w pełni na CPU. Oczekuj wolniejszego wnioskowania — około 2–3 sekund na stronę na nowoczesnym laptopie.

### Moje faktury to wielostronicowe PDF‑y. Jak je obsłużyć?

Convert each page to a separate image (e.g., using `pdf2image`) and loop over the pages with the same script. The OCR engine can process each image independently, and the LLM will correct each block of text.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Pobieranie modelu nie powodzi się za zaporą sieciową?

Download the model manually from the Hugging Face model hub, unzip it into a local folder, and point `hugging_face_repo_id` to the local path:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Jak dokładna jest korekcja?

For typical English‑language invoices, the LLM fixes >95 % of common OCR mis‑recognitions. Complex handwritten notes may still need manual review.

---

## Wskazówki i triki dla zastosowań produkcyjnych

- **Batch processing:** Wrap steps 2‑4 in a function and feed a list of file paths. Re‑use the same `AsposeAI` instance to avoid re‑loading the model.
- **Logging:** Replace `print` with Python’s `logging` module to capture both raw and corrected outputs for audit trails.
- **Error handling:** Surround the OCR call with `try/except` blocks. If an image fails, log the filename and continue.
- **Performance tuning:** Experiment with `gpu_layers`. More layers on GPU speed up inference but increase VRAM usage.

## Zakończenie

We’ve covered **how to run OCR** on invoice images from start to finish, showing you how to **perform OCR on image**, **download Hugging Face model**, and **correct OCR errors** automatically. The complete script demonstrates a practical workflow that you can drop into any Python‑based automation pipeline.

Next steps? Try extending the pipeline to **extract key fields** (invoice number, date, total) using regular expressions on the corrected text, or feed the cleaned output into a database for searchable records. You could also experiment with other lightweight LLMs from Hugging Face if you need a different language or domain‑specific knowledge.

Szczęśliwego kodowania i niech wyniki OCR zawsze będą krystalicznie czyste! 

![jak uruchomić OCR na obrazie faktury](ocr_invoice_example.png "jak uruchomić OCR na fakturze")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}