---
category: general
date: 2026-01-07
description: Jak uruchomić OCR i wyodrębnić tekst z obrazu do przetwarzania faktur.
  Dowiedz się, jak poprawić dokładność OCR, wczytać obraz do OCR i efektywnie przetwarzać
  OCR faktur.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: pl
og_description: Jak przeprowadzić OCR faktur krok po kroku. Wyodrębnij tekst z obrazu,
  popraw dokładność OCR i wczytaj obraz do OCR przy użyciu Aspose AI.
og_title: Jak uruchomić OCR na fakturach – Kompletny przewodnik Pythona
tags:
- OCR
- Python
- Image Processing
title: Jak przeprowadzić OCR na fakturach – wyodrębnić tekst z obrazu w Pythonie
url: /pl/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR na fakturach – wyodrębnić tekst z obrazu przy użyciu Pythona

Zastanawiałeś się kiedyś **jak uruchomić OCR** na zeskanowanej fakturze i uzyskać czysty, przeszukiwalny tekst? Nie jesteś sam. Wielu programistów napotyka problem, gdy surowy wynik OCR jest pełen błędów ortograficznych, niepoprawnych podziałów linii i brakującej interpunkcji. W tym samouczku przeprowadzimy pełne rozwiązanie, które nie tylko **wyodrębnia tekst z obrazu**, ale także **poprawia dokładność OCR** dzięki post‑procesowaniu modelem AI Aspose.

Zobaczysz, jak **wczytać obraz do OCR**, uruchomić wbudowany silnik i zastosować lekką kontrolę pisowni, która przygotowuje wynik do dalszej analizy. Na koniec będziesz mieć wielokrotnego użytku skrypt, który można wstawić do dowolnego potoku przetwarzania faktur.

> **Czego będziesz potrzebować**  
> * Python 3.9 lub nowszy  
> * pakiety `aspose-ocr` i `aspose-ai` (zainstalowane przez `pip`)  
> * Obraz faktury (PNG, JPEG lub TIFF) – użyjemy `sample_invoice.png` jako przykładu  
> * Opcjonalnie: GPU z co najmniej 4 GB VRAM dla szybszej inferencji modelu (skrypt działa również na CPU)

---

## Krok 1: Zainstaluj wymagane pakiety i przygotuj środowisko

Zanim będziemy mogli **wczytać obraz do OCR**, musimy upewnić się, że niezbędne biblioteki są dostępne. Silnik Aspose OCR jest dostarczany z prostym wrapperem Pythona, natomiast post‑procesor AI opiera się na kwantyzowanym modelu Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Wskazówka:** Jeśli planujesz używać przyspieszenia GPU, zainstaluj `torch` z obsługą CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Krok 2: Wczytaj obraz faktury

Wczytanie obrazu jest proste, ale warto wspomnieć, dlaczego jawnie ustawiamy ścieżkę jako surowy łańcuch (`r"..."`). Zapobiega to przypadkowym problemom z znakami ucieczki w ścieżkach Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Dlaczego to ważne:* Użycie `ocr.Image.load` zapewnia, że obraz jest wstępnie przetwarzany (binarizacja, prostowanie) zgodnie z optymalnymi ustawieniami Aspose, co już **poprawia dokładność OCR** przed jakąkolwiek magią AI.

---

## Krok 3: Uruchom wbudowany silnik OCR

Teraz faktycznie **uruchamiamy OCR** i przechwytujemy surowy tekst. Ten krok pokazuje typowy wynik, jaki uzyskasz z podstawowego uruchomienia OCR — często bałagan podziałów linii i sporadyczne błędy ortograficzne.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typowy surowy wynik** (skrócony dla zwięzłości):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Możesz zauważyć, że „Invoice” pojawia się jako „Invo1ce” lub że brakuje interpunkcji. W tym miejscu wkracza post‑procesor AI.

---

## Krok 4: Skonfiguruj model AI Aspose

Model AI, którego użyjemy, to **Qwen2.5‑3B‑Instruct‑GGUF**, lekki, instrukcyjnie dostrojony LLM, który działa komfortowo na GPU średniej klasy. Poniższa konfiguracja informuje Aspose, skąd pobrać model, ile warstw utrzymać na GPU oraz rozmiar kontekstu do obsługi długich akapitów.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Dlaczego ta konfiguracja?**  
> * `gpu_layers=30` równoważy szybkość i pamięć — większość inferencji odbywa się na GPU, a pozostałe warstwy pozostają na CPU, aby uniknąć błędów OOM.  
> * `context_size=4096` zapewnia, że model może zobaczyć całą fakturę jednocześnie, zapobiegając obcinaniu ważnych pól.

---

## Krok 5: Utwórz prosty post‑procesor sprawdzania pisowni

Owinąśmy wywołanie AI w małą funkcję o nazwie `simple_spell_check`. Prompt jest celowo zwięzły: „Correct spelling and punctuation:” (Popraw pisownię i interpunkcję:) po którym następuje surowy tekst OCR. Model zwraca wyczyszczoną wersję.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Jak to działa:** `ai.run_prompt` wysyła prompt do lokalnie załadowanego LLM, który następnie zwraca pojedynczy ciąg znaków z poprawioną pisownią, właściwą interpunkcją i bardziej naturalnym układem podziałów linii.

---

## Krok 6: Zastosuj post‑procesor do surowego tekstu OCR

Teraz dzieje się magia. Przekazujemy surowy wynik OCR do naszego post‑procesora i drukujemy ulepszony rezultat.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Przykładowy ulepszony wynik**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Zauważ poprawioną pisownię „Invoice”, właściwe użycie dwukropka i spójne podziały linii — dokładnie to, czego potrzebujesz do niezawodnego dalszego parsowania.

---

## Krok 7: Zwolnij zasoby

Zarówno silnik OCR, jak i model AI przydzielają natywne zasoby. Dobrą praktyką jest ich zwolnienie po zakończeniu, szczególnie w długotrwale działających usługach.

```python
ai.free_resources()
engine.dispose()
```

---

## Pełny skrypt – gotowy do wklejenia

Poniżej znajduje się kompletny, uruchamialny skrypt, który łączy wszystkie kroki. Zapisz go jako `invoice_ocr.py`, zamień `YOUR_DIRECTORY` na folder zawierający obraz faktury i uruchom poleceniem `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Uruchom skrypt, a zobaczysz zarówno hałaśliwy surowy zrzut OCR, jak i wypolerowaną wersję z **poprawioną dokładnością OCR** obok siebie.

---

## Najczęściej zadawane pytania i przypadki brzegowe

### 1. Co zrobić, jeśli mój obraz faktury jest wielostronicowym PDF-em?

Aspose OCR może bezpośrednio wczytywać strony PDF. Zastąp linię wczytywania obrazu następującym kodem:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Iteruj `page_index`, aby przetwarzać każdą stronę kolejno.

### 2. Mój GPU kończy pamięć — czy mogę używać tylko CPU?

Oczywiście. Ustaw `gpu_layers=0` w `AsposeAIModelConfig`. Model będzie działał w pełni na CPU, co jest wolniejsze, ale bezpieczne dla słabszego sprzętu.

### 3. Jak obsłużyć faktury w językach innych niż angielski?

Zamień identyfikator repozytorium modelu na model specyficzny dla języka, np. `"mistralai/Mistral-7B-Instruct-v0.2"` dla wsparcia wielojęzycznego. Reszta potoku pozostaje niezmieniona.

### 4. Czy mogę łączyć wiele post‑procesorów (np. formatowanie dat, wyodrębnianie sum)?

Tak. `ai.set_post_processor` przyjmuje listę wywoływalnych obiektów. Na przykład:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

Wynik najpierw zostanie poddany sprawdzeniu pisowni, a następnie zostaną wyodrębnione sumy.

---

## Wskazówki dotyczące wydajności i najlepsze praktyki

| Tip | Why it Helps |
|-----|---------------|
| **Przetwarzaj wiele faktur jednocześnie** – wczytaj je do listy i przetwarzaj w pętli. | Zmniejsza obciążenie interpretera Pythona i utrzymuje model AI w pamięci, gotowy do użycia. |
| **Cache'uj model** – unikaj wielokrotnego wywoływania `initialize` w usłudze webowej. | Ładowanie modelu może trwać ~30 sekund; cache'owanie zapewnia natychmiastowe odpowiedzi. |
| **Zmieniaj rozmiar dużych obrazów** do szerokości 1500 px przed OCR. | Mniejsze obrazy przyspieszają zarówno OCR, jak i inferencję AI, nie tracąc na dokładności. |
| **Ustaw `allow_auto_download="false"` w produkcji** – dostarcz model wraz z wdrożeniem. | Gwarantuje deterministyczny czas uruchomienia i unika problemów sieciowych. |

---

## Podsumowanie

Omówiliśmy **jak uruchomić OCR** na fakturach, od wczytania obrazu po dopracowanie wyniku za pomocą AI‑napędzanego sprawdzania pisowni. Postępując zgodnie z tymi krokami, możesz niezawodnie **wyodrębnić tekst z obrazu**, **poprawić dokładność OCR** i płynnie **przetwarzać OCR faktur** w dowolnym przepływie pracy opartym na Pythonie.

Wypróbuj to na kilku różnych układach faktur — może to być ręcznie pisany paragon lub zeskanowany kontrakt. Ten sam potok dostosowuje się przy minimalnych zmianach, co dowodzi, że dobrze skonstruowane połączenie OCR + AI jest wszechstronnym narzędziem dla każdego projektu automatyzacji dokumentów.

Jeśli ten przewodnik okazał się pomocny, rozważ podzielenie się nim z zespołem lub oznaczenie gwiazdką repozytorium, które hostuje pakiety Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}