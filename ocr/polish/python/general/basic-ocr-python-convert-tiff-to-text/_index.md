---
category: general
date: 2026-03-18
description: Podstawowy samouczek OCR w Pythonie pokazuje, jak konwertować pliki TIFF
  na tekst, ładować OCR obrazu, ustawiać warstwy GPU oraz naprawiać wiodące zera przy
  użyciu Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: pl
og_description: Podstawowy samouczek OCR w Pythonie prowadzi Cię przez konwersję plików
  TIFF na czysty tekst, ładowanie obrazów, ustawianie warstw GPU oraz naprawianie
  wiodących zer.
og_title: Podstawowy OCR w Pythonie – konwersja TIFF na tekst
tags:
- OCR
- Python
- AI
- Aspose
title: podstawowy OCR w Pythonie – konwersja TIFF na tekst
url: /pl/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Konwersja TIFF na tekst z post‑processingiem AI

Szukasz sposobu na **basic ocr python** w swoich zeskanowanych dokumentach? W tym przewodniku pokażemy, jak przekonwertować plik TIFF na czysty, przeszukiwalny tekst przy użyciu Aspose OCR oraz post‑procesora AI.  

Jeśli kiedykolwiek miałeś problem z **konwersją TIFF na tekst**, ponieważ surowy wynik jest pełen literówek lub dziwnych znaków, nie jesteś sam. Pokażemy także, jak **załadować obraz OCR**, dostroić silnik, aby **ustawić warstwy GPU**, oraz jak **naprawić wiodące zera**, które często pojawiają się w numerach faktur.

## Co się nauczysz

- Jak zainicjalizować silnik Aspose OCR dla dokumentów drukowanych.  
- Dokładne kroki, aby **załadować obraz OCR** z pliku TIFF i uzyskać surowy tekst.  
- Konfigurowanie modelu AI, automatyczne pobieranie go oraz **ustawianie warstw GPU** dla szybszej inferencji.  
- Dodanie wbudowanego sprawdzania pisowni plus własnej funkcji, która **naprawia wiodące zera**.  
- Czyszczenie wyniku OCR i prawidłowe zwalnianie zasobów.  

Po zakończeniu tego samouczka będziesz mieć jeden, wielokrotnego użytku skrypt Pythona, który zamieni dowolny plik TIFF w dopracowany, przeszukiwalny tekst — bez ręcznego kopiowania i wklejania.  

### Wymagania wstępne

- Python 3.8+ zainstalowany na twoim komputerze.  
- Pakiet `aspose-ocr` (`pip install aspose-ocr`).  
- Opcjonalnie: GPU z co najmniej 4 GB VRAM, jeśli chcesz **ustawić warstwy GPU**; w przeciwnym razie kod automatycznie przełączy się na CPU.  

---

## basic ocr python – załaduj obraz i rozpoznaj tekst

Pierwszą rzeczą, którą musimy zrobić, jest **załadowanie obrazu OCR**, aby silnik mógł odczytać piksele. `OcrEngine` Aspose obsługuje wiele formatów, ale tutaj skupiamy się na TIFF, ponieważ jest najczęściej używany do skanowanych faktur.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Jeśli pracujesz z wielostronicowymi plikami TIFF, Aspose automatycznie przetwarza każdą stronę kolejno, więc nie musisz dodawać dodatkowych pętli.

Teraz, gdy obraz jest załadowany, uruchomimy podstawowy przebieg rozpoznawania.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Zobaczysz coś w tym stylu:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Zauważ *zera* przed literami? To klasyczny artefakt OCR, który wyczyścimy później.

![przepływ pracy basic ocr python](/images/ocr-workflow.png "diagram przepływu pracy basic ocr python")

---

## Krok 2: Konwersja TIFF na tekst – przygotowanie post‑procesora AI

Surowe OCR jest przydatne, ale większość produkcyjnych potoków wymaga dopracowanej wersji. Aspose udostępnia wrapper `AsposeAI`, który może pobrać model z Hugging Face, uruchomić go na GPU i automatycznie zastosować sprawdzanie pisowni.

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

### Dlaczego `set GPU layers` ma znaczenie

Parametr `gpu_layers` informuje podstawowy model GGUF, ile warstw transformera ma pozostać na GPU. Więcej warstw = szybsza inferencja, ale wyższe zużycie VRAM. Jeśli pracujesz na skromnym laptopie, zmniejsz wartość do `10` lub całkowicie ją pomiń, aby pozostać przy CPU.

---

## Krok 3: Zastosuj sprawdzanie pisowni i **napraw wiodące zera**

Aspose AI dostarcza wbudowany sprawdzacz pisowni, który łapie większość angielskich literówek. Jednak specyficzne dla domeny poprawki — takie jak zamiana wiodącego `0` na `O` w kodach faktur — wymagają własnego post‑procesora.

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

> **Dlaczego to działa:** Wyrażenie regularne szuka granicy słowa (`\b`), zera, a następnie dokładnie trzech wielkich liter. Następnie zamienia zero na literę „O”. Możesz rozszerzyć wzorzec o inne przypadki (np. `0[0-9]{2}` dla błędnie odczytanych liczb).

---

## Krok 4: Oczyść wynik OCR przy pomocy post‑procesora AI

Teraz łączymy wszystko: surowy ciąg z **basic ocr python**, sprawdzanie pisowni i naszą naprawę zer. Metoda `run_postprocessor` zwraca wyczyszczoną wersję gotową dla dalszych systemów.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Typowy wynik po post‑procesorze:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Widzisz, że wiodące zero zamieniło się w `O`, a typowe literówki zostały skorygowane. Tekst jest teraz gotowy do indeksowania w wyszukiwarce lub przekazania do potoku ekstrakcji danych.

---

## Krok 5: Zwolnij zasoby AI – dbaj o swój GPU

Jeśli uruchamiasz wiele zadań OCR w długotrwałej usłudze, dobrą praktyką jest zwolnienie pamięci GPU modelu po zakończeniu.

```python
ocr_ai.free_resources()
```

Pomijanie tego kroku może prowadzić do błędów „out‑of‑memory” przy kolejnych wywołaniach, szczególnie gdy **set GPU layers** jest ustawione na wysoką wartość.

---

## Opcjonalne warianty i przypadki brzegowe

| Sytuacja | Co zmienić |
|-----------|----------------|
| **Dokumenty odręczne** | Użyj `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` zamiast `PRINTED`. |
| **Brak GPU** | Ustaw `gpu_layers=0` lub pomiń argument; model będzie działał na CPU (wolniej, ale bezpiecznie). |
| **Inny język** | Zamień ID repozytorium Hugging Face na model specyficzny dla języka, np. `microsoft/Florence-2-base`. |
| **Przetwarzanie wsadowe** | Owiń kroki w pętlę `for file in glob("*.tif"):` i gromadź wyniki w liście lub pliku CSV. |
| **Bardziej złożone wzorce zer** | Rozszerz `invoice_fix` o dodatkowe wyrażenia regularne, takie jak `r"\b0+([A-Z]{2,})\b"` dla wielu wiodących zer. |

---

## Zakończenie

Właśnie ukończyliśmy **basic ocr python** pipeline, który ładuje TIFF, wyodrębnia surowy tekst, a następnie czyści go przy użyciu modelu AI, jednocześnie **ustawiając warstwy GPU** dla wydajności. Własny post‑procesor pokazuje, jak **naprawić wiodące zera**, mały, ale często pomijany szczegół, który może zepsuć dalszą analizę.

Śmiało eksperymentuj: wypróbuj inną kwantyzację (`float16` dla wyższej dokładności), zamień sprawdzanie pisowni na słownik specyficzny dla domeny lub połącz wiele własnych poprawek. Schemat pozostaje ten sam — ładowanie, rozpoznawanie, konfiguracja AI, post‑processing i sprzątanie.

**Kolejne kroki**, które możesz rozważyć:

- Integracja wyczyszczonego wyniku z bazą danych lub indeksem Elasticsearch.  
- Zastosowanie tego samego podejścia do **konwersji TIFF na tekst** w wielojęzycznych PDF‑ach.  
- Dodanie interfejsu UI przy użyciu Flask lub FastAPI, aby użytkownicy nietechniczni mogli wgrywać pliki i natychmiast otrzymywać wyczyszczony tekst.  

Miłego kodowania i niech twoje wyniki OCR zawsze będą wyraźne i pozbawione zer!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}