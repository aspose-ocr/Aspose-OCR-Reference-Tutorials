---
category: general
date: 2026-06-25
description: Szybko uzyskaj obsługiwane znaki OCR przy użyciu biblioteki aocr. Dowiedz
  się, jak wyświetlić listę znaków OCR, ustawić języki i debugować silnik OCR w Pythonie.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: pl
og_description: Uzyskaj znaki obsługiwane przez OCR za pomocą aocr. Ten przewodnik
  pokazuje, jak wyświetlić znaki OCR, wybrać języki i obsłużyć przypadki brzegowe
  w Pythonie.
og_title: Pobierz obsługiwane znaki OCR w Pythonie – pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Uzyskaj obsługiwane znaki OCR w Pythonie – Kompletny przewodnik
url: /pl/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uzyskaj obsługiwane znaki OCR w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **uzyskać obsługiwane znaki OCR** dla konkretnego języka, gdy bawisz się silnikiem OCR? Nie jesteś sam. Niezależnie od tego, czy tworzysz skaner paragonów, czy wielojęzyczny parser dokumentów, znajomość dokładnie, które glify Twój silnik potrafi rozpoznać, jest nieoceniona. W tym samouczku przeprowadzimy Cię przez cały proces — instalację biblioteki, konfigurację języka i w końcu wypisanie tych znaków — abyś mógł debugować i precyzyjnie dostroić swój potok OCR w kilka minut.

Użyjemy biblioteki **aocr**, lekkiego silnika OCR w Pythonie, który umożliwia łatwe zapytanie o możliwości językowe. Po zakończeniu tego przewodnika będziesz w stanie **wyświetlić listę znaków OCR**, przełączać się między **obsługiwanymi językami OCR** i nawet wykrywać luki w pokryciu, zanim sprawią problemy w produkcji.

---

## Wymagania wstępne

* Python 3.8 lub nowszy (pakiet aocr nie obsługuje już 3.7)
* Terminal lub wiersz poleceń z dostępem do internetu
* Podstawowa znajomość skryptów w Pythonie (jeśli już używałeś `print()`, jesteś w porządku)

Brak ciężkich zewnętrznych zależności — tylko pakiet pip `aocr`.

## Instalacja biblioteki aocr (Silnik OCR w Pythonie)

Pierwszą rzeczą, której potrzebujesz, jest działająca instalacja **OCR engine Python**. Pakiet aocr jest dostępny w PyPI, więc wystarczy jedno polecenie pip, aby to zrobić:

```bash
pip install aocr
```

Jeśli używasz wirtualnego środowiska (bardzo zalecane), najpierw je aktywuj:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Zablokuj wersję (`pip install aocr==1.2.4`), aby uniknąć nieoczekiwanych zmian API w przyszłości.

## Wybór języka (Obsługiwane języki OCR)

aocr dostarcza kilka wbudowanych pakietów językowych. Każdy pakiet definiuje zestaw punktów kodowych Unicode, które silnik może rozpoznać. Aby zapytać o te pakiety, musisz ustawić atrybut `language` w instancji silnika.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Możesz zamienić `aocr.Language.ENGLISH` na dowolną inną wartość wyliczeniową (`FRENCH`, `GERMAN` itp.). Jeśli spróbujesz przypisać język, który nie jest dołączony, aocr zgłosi `ValueError`. Dlatego warto najpierw sprawdzić listę **obsługiwanych języków OCR**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

## Pobranie zestawu znaków (Uzyskaj obsługiwane znaki OCR)

Teraz przechodzi do sedna samouczka: faktycznie **uzyskać obsługiwane znaki OCR**. Silnik udostępnia przydatną metodę `get_supported_characters()`, która zwraca listę jednocząstkowych łańcuchów znaków.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Za kulisami aocr odczytuje plik JSON dołączony do pakietu językowego i konwertuje każdy punkt kodowy Unicode na łańcuch Pythona. Wynik jest deterministyczny, co oznacza, że otrzymasz tę samą listę przy każdym uruchomieniu skryptu na tej samej wersji języka.

## Pokaż, ile znaków jest obsługiwanych

Znajomość liczby pomaga szybko ocenić zakres pokrycia. Dla języka angielskiego zazwyczaj zobaczysz kilka tysięcy znaków (w tym interpunkcję i cyfry).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Wywołanie `len()` jest O(1), ponieważ Python przechowuje długość listy wewnętrznie, więc nie ma spadku wydajności nawet przy dużych alfabetach.

## Podgląd pierwszych 100 obsługiwanych znaków

Szybka kontrola wizualna może ujawnić, czy silnik zawiera potrzebne Ci symbole (np. znak euro lub inteligentne cudzysłowy). Wydrukujmy pierwsze sto znaki:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

## Pełny skrypt – wszystkie kroki w jednym miejscu

Poniżej znajduje się kompletny, działający przykład, który łączy wszystkie elementy. Zapisz go jako `list_supported_chars.py` i uruchom `python list_supported_chars.py` w terminalu.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Oczekiwany wynik (skrócony dla zwięzłości):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Dokładna liczba może nieco się różnić w zależności od wersji aocr, ale zawsze zobaczysz długi alfabet plus typową interpunkcję.

## Obsługa przypadków brzegowych

### Co zrobić, gdy pakiet językowy jest brakujący?

Jeśli zażądasz języka, który nie jest dołączony, `aocr.Language` nie będzie zawierał tego wyliczenia i otrzymasz `AttributeError`. Zabezpiecz się przed tym prostym sprawdzeniem:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Pusta lista znaków

Niektóre niszowe języki mogą zwrócić pustą listę, jeśli podstawowe dane treningowe są niekompletne. W takim przypadku możesz przejść do domyślnego (np. angielskiego) lub zgłosić ostrzeżenie:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalizacja Unicode

Lista może zawierać znaki złożone (np. „é” jako `e` + akcent ostróży). Jeśli dalsze przetwarzanie oczekuje znaków prekomponowanych, wykonaj krok normalizacji:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

## Pro tipy dla projektów w rzeczywistym środowisku

* **Cache the character list** – Jeśli przetwarzasz tysiące obrazów, wywoływanie `get_supported_characters()` w każdej iteracji dodaje niepotrzebny narzut. Przechowuj listę w zmiennej na poziomie modułu lub serializuj ją do JSON w celu późniejszego ponownego użycia.
* **Cross‑language validation** – Gdy obsługujesz wiele języków w jednej aplikacji, przeciąć zestawy znaków, aby znaleźć wspólny podzbiór. Pomaga to projektować elementy UI, które pozostają spójne w różnych lokalizacjach.
* **Debugging OCR failures** – Jeśli silnik błędnie klasyfikuje glif, porównaj problematyczny znak z wynikiem `list_supported_chars`. Jeśli go brakuje, zidentyfikowałeś lukę w pokryciu, która może wymagać niestandardowego etapu treningowego.
* **Combine with custom fonts** – aocr respektuje zakres Unicode, ale jakość renderowania może się różnić w zależności od czcionki. Przetestuj obsługiwane znaki przy użyciu dokładnej czcionki, którą będziesz używać w produkcji, aby uniknąć niespodzianek.

## Najczęściej zadawane pytania

**Q: Czy to działa z wersją aocr 2.x?**  
**A:** Tak, metoda `get_supported_characters()` jest stabilna w wersjach 1.x i 2.x. Jedyną zmianą jest to, że wyliczenia języków zostały przeniesione do `aocr.languages`.

**Q: Czy mogę uzyskać kod Unicode dla każdego znaku?**  
**A:** Absolutnie. Użyj `ord(ch)` w wyrażeniu listowym:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Co z językami pisanymi od prawej do lewej, takimi jak arabski?**  
**A:** `aocr` zawiera wyliczenie `ARABIC`. Lista znaków będzie zawierać glify arabskie, ale może być konieczne włączenie renderowania RTL w dalszym interfejsie użytkownika.

## Zakończenie

Teraz wiesz, **jak uzyskać obsługiwane znaki OCR** przy użyciu biblioteki aocr w Pythonie, jak przełączać się między **obsługiwanymi językami OCR** oraz dlaczego **wyświetlanie listy znaków OCR** jest niezbędne dla solidnych potoków rozpoznawania tekstu. Mając pełny skrypt i powyższe wskazówki, możesz szybko zweryfikować pokrycie językowe, debugować brakujące glify i budować inteligentniejsze aplikacje oparte na OCR.

Gotowy na kolejny krok? Spróbuj połączyć tę listę znaków z własnym filtrem listy słów lub eksperymentuj z innym silnikiem OCR (Tesseract, EasyOCR) i porównaj wyniki. Im więcej eksplorujesz, tym lepsze będą Twoje rozwiązania OCR.

Szczęśliwego kodowania i niech Twoje zestawy znaków zawsze będą kompletne!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i eksplorować alternatywne podejścia implementacyjne w własnych projektach.

- [Określ dozwolone znaki OCR – używając Aspose.OCR dla .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Jak wykonać OCR tekstu obrazu z językiem przy użyciu Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Postprocessing OCR – uzyskaj wybory znaków](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}