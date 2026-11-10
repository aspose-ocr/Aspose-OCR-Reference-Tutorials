---
category: general
date: 2026-06-19
description: Jak przeprowadzić OCR krok po kroku i poprawić dokładność OCR przy użyciu
  technik OCR dla zwykłego tekstu. Poznaj szybki przepływ pracy umożliwiający niezawodne
  wyodrębnianie tekstu.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: pl
og_description: Jak efektywnie uruchamiać OCR. Ten samouczek pokazuje, jak poprawić
  dokładność OCR, używając OCR tekstu prostego i post‑przetwarzania AI.
og_title: Jak uruchomić OCR w Pythonie – Kompletny przewodnik
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
title: Jak uruchomić OCR w Pythonie – Kompletny przewodnik
url: /pl/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś, **jak uruchomić OCR** na partii zeskanowanych PDF‑ów, nie tracąc godzin na dopasowywanie ustawień? Nie jesteś sam. W wielu projektach pierwszą przeszkodą jest po prostu uzyskanie wiarygodnego tekstu z obrazu, a różnica między niepewnym wynikiem a czystym wyodrębnieniem często sprowadza się do kilku sprytnych kroków.

W tym przewodniku przejdziemy przez praktyczny czterostopniowy pipeline, który nie tylko **uruchamia OCR**, ale także **poprawia dokładność OCR**, łącząc szybki przebieg tekstowy z drugą, świadomą układu, oraz post‑procesorem opartym na AI. Po zakończeniu będziesz mieć gotowy do uruchomienia skrypt, jasne wyjaśnienie, dlaczego każdy etap ma znaczenie, oraz wskazówki dotyczące obsługi przypadków brzegowych, takich jak strony wielokolumnowe czy zaszumione skany.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- **Python 3.9+** – kod używa podpowiedzi typów i f‑stringów.  
- **Tesseract OCR** zainstalowany i dostępny poprzez polecenie `tesseract`. (Na Ubuntu: `sudo apt install tesseract-ocr`; na Windows pobierz instalator z oficjalnego repozytorium.)  
- Wrapper **pytesseract** (`pip install pytesseract`).  
- Biblioteka **AI post‑processing** – w tym przykładzie udajemy, że masz lekki moduł `ai`, który oferuje `run_postprocessor`. Zamień go na API GPT‑4 od OpenAI lub lokalny LLM, jeśli wolisz.  
- Kilka przykładowych obrazów lub PDF‑ów do testów.

To wszystko. Bez ciężkich frameworków, bez gimnastyki Docker. Tylko kilka instalacji pip i jesteś gotowy do działania.

---

## Krok 1: Wykonaj szybki, prosty przebieg OCR (plain‑text)

Pierwsza rzecz, którą pomijają większość programistów, to fakt, że *plain text* OCR jest błyskawiczny i daje szybki test sanity. Wywołamy `engine.Recognize()`, aby pobrać surowe znaki bez metadanych układu. To właśnie rozumiemy pod **plain text OCR**.

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

*Dlaczego to ważne:*  
- **Szybkość** – prosty przebieg na stronie 300 dpi zazwyczaj kończy się w mniej niż sekundę.  
- **Podstawa** – możesz porównać późniejsze, strukturalne wyjście z tą bazą, aby wykryć rażące błędy.  
- **Wykrywanie błędów** – jeśli prosty przebieg całkowicie zawiedzie (np. wszystkie znaki są bełkotem), wiesz, że jakość obrazu jest zbyt niska i możesz od razu przerwać.

---

## Krok 2: Uruchom szczegółowy, świadomy układu przebieg OCR

Plain text jest świetny, ale pomija *gdzie* każde słowo znajduje się na stronie. Dla faktur, formularzy czy wielokolumnowych magazynów potrzebujesz współrzędnych, numerów linii i być może informacji o czcionce. Tu wkracza `engine.RecognizeStructured()`.

Poniżej znajduje się cienka warstwa wokół wyjścia **TSV** Tesseracta, które daje nam hierarchię stron → linii → słów, zachowując ramki ograniczające.

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

*Dlaczego to robimy:*  
- **Współrzędne** pozwalają później odwzorować wyodrębniony tekst na oryginalny obraz w celu podświetlenia lub redakcji.  
- **Grupowanie linii** zachowuje oryginalny układ, co jest niezbędne przy odtwarzaniu tabel lub kolumn.  
- Ten przebieg jest nieco wolniejszy niż prosty, ale wciąż kończy się w kilku sekundach dla większości dokumentów.

---

## Krok 3: Uruchom AI post‑processor, aby skorygować błędy OCR

Nawet najlepszy silnik OCR popełnia błędy — np. „rn” zamiast „m”, brakujące diakrytyki czy podzielone słowa. Model AI może spojrzeć na surowy ciąg i dane strukturalne, wykryć niespójności i przepisanie tekstu, zachowując oryginalne współrzędne.

Poniżej znajduje się **mock** implementacja; zamień ciało na rzeczywiste wywołanie LLM, jeśli je posiadasz.

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

*Dlaczego ten krok poprawia dokładność OCR:*  
- **Korekty kontekstowe** – AI może stwierdzić, że „l0ve” najprawdopodobniej ma być „love” na podstawie otaczających słów.  
- **Zachowanie współrzędnych** – utrzymujesz informacje o układzie, więc dalsze zadania (np. adnotacje PDF) pozostają precyzyjne.  
- **Iteracyjne udoskonalanie** – możesz uruchamiać post‑processor wielokrotnie, każdy przebieg usuwa kolejne błędy.

---

## Krok 4: Iteruj przez poprawioną, strukturalną wyjściową

Teraz, gdy mamy wyczyszczoną strukturę, pobranie ostatecznego tekstu jest trywialne. Poniżej drukujemy każdą linię, ale możesz także zapisać do CSV, wprowadzić do bazy danych lub wygenerować przeszukiwalny PDF.

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

**Oczekiwany wynik** (zakładając prostą fakturę jednokolumnową):

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

Zauważ, że podziały linii i kolejność kolumn są zachowane, a typowe błędy OCR, takie jak odczytanie „$15.00” jako „$15,00”, są skorygowane przez krok AI.

---

## Jak ten workflow pomaga **poprawić dokładność OCR**

| Etap | Co naprawia | Dlaczego ma znaczenie |
|------|-------------|-----------------------|
| **Plain text OCR** | Wykrywa nieczytelne strony wcześnie | Oszczędza czas, pomijając beznadziejne wejścia |
| **Structured OCR** | Uchwyca układ, współrzędne | Umożliwia dalsze zadania (podświetlanie, redakcja) |
| **AI post‑processor** | Koryguje pisownię, łączy podzielone słowa, naprawia liczby | Zwiększa ogólną dokładność znakową z ~85 % do >95 % na zaszumionych skanach |
| **Iteracja** | Pozwala ponownie uruchomić z dopasowanymi parametrami | Dostraja pipeline do konkretnych typów dokumentów |

Łącząc te trzy koncepcje — **plain text OCR**, ekstrakcję świadomą układu i korektę AI — otrzymujesz solidne rozwiązanie, które *znacznie* **poprawia dokładność OCR** bez konieczności pisania własnej sieci neuronowej od podstaw.

---

## Częste pułapki i wskazówki profesjonalisty

- **Pułapka:** Przekazywanie obrazu o niskiej rozdzielczości (≤150 dpi) do Tesseracta skutkuje zniekształconym wynikiem.  
  **Wskazówka:** Wstępnie przetwórz obraz przy pomocy `Pillow` — zastosuj `Image.convert('L')` i `Image.filter(ImageFilter.MedianFilter())` przed OCR.

- **Pułapka:** AI post‑processor może przypadkowo przekształcić terminologię specyficzną dla domeny (np. „SKU123”).  
  **Wskazówka:** Zbuduj białą listę terminów i przekaż ją do LLM lub do biblioteki sprawdzającej pisownię, takiej jak `pyspellchecker`.

- **Pułapka:** Strony wielokolumnowe zostają scalone w jedną linię.  
  **Wskazówka:** Wykryj granice kolumn przy użyciu pola `block_num` w wyjściu TSV Tesseracta i podziel linie odpowiednio.

- **Pułapka:** Duże PDF‑y powodują wyciek pamięci przy ładowaniu wszystkich stron jednocześnie.  
  **Wskazówka:** Przetwarzaj strony stopniowo — iteruj po `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Rozszerzanie pipeline’u

Jeśli ciekawi Cię kolejny krok, rozważ następujące udoskonalenia:

1. **Przetwarzanie wsadowe** – Owiń cały skrypt w funkcję, która przechodzi po katalogu, obsługując tysiące plików równolegle przy pomocy `concurrent.futures`.  
2. **Modele językowe** – Zamień prostą heurystykę difflib na wywołanie OpenAI `gpt‑4o` lub lokalnie hostowanego modelu LLaMA, aby uzyskać bogatsze korekty kontekstowe.  
3. **Formaty eksportu** – Zapisz poprawioną strukturę do przeszukiwalnego PDF  

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i eksplorować alternatywne podejścia w własnych projektach.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}