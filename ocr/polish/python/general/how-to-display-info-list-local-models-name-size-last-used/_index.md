---
category: general
date: 2026-01-12
description: Dowiedz się, jak wyświetlać informacje z AsposeAI, wymieniając lokalne
  modele, pokazując nazwę modelu, rozmiar i znacznik czasu ostatniego użycia w przejrzystym
  przykładzie w Pythonie.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: pl
og_description: 'Jak wyświetlić informacje z AsposeAI: lista lokalnych modeli, wyświetlenie
  nazwy modelu, rozmiaru i znacznika czasu ostatniego użycia z pełnym przewodnikiem
  w Pythonie.'
og_title: Jak wyświetlić informacje – lista lokalnych modeli, nazwa, rozmiar, ostatnio
  użyty
tags:
- AsposeAI
- Python
- Model Management
title: Jak wyświetlić informacje – lista lokalnych modeli, nazwa, rozmiar, ostatnio
  użyte
url: /pl/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyświetlić informacje – lista lokalnych modeli, nazwa, rozmiar, ostatnie użycie

Zastanawiałeś się kiedyś **jak wyświetlić informacje** z instalacji AsposeAI bez przeszukiwania logów czy interfejsu użytkownika? Nie jesteś jedyny. W wielu pipeline'ach data‑science pierwszą rzeczą, której potrzebujesz, jest szybki podgląd, które modele znajdują się na Twoim komputerze, jak się nazywają, jak duże są i kiedy były ostatnio używane.

Dokładnie to omówimy: zwięzły, kompleksowy fragment Pythona, który **wyświetla listę lokalnych modeli**, a następnie **pokazuje nazwę modelu**, **rozmiar modelu** i **znacznik czasu ostatniego użycia**. Bez zewnętrznych bibliotek, bez ukrytej magii — tylko klient AsposeAI, którego już używasz.

Po zakończeniu tego samouczka będziesz mógł wkleić kod do dowolnego skryptu, uruchomić go i natychmiast uzyskać schludną tabelę lokalnie buforowanych modeli. To idealne rozwiązanie do weryfikacji środowisk, budowania pulpitów kontrolnych lub po prostu zaspokojenia ciekawości, co kryje się na dysku.

## Wymagania wstępne

- Python 3.8 lub nowszy (przykład używa f‑stringów, więc 3.6+ jest konieczne)
- Pakiet `asposeai` zainstalowany (`pip install asposeai`)
- Działająca licencja AsposeAI lub klucz trial (klient pobierze poświadczenia ze zmiennych środowiskowych lub pliku konfiguracyjnego)

Jeśli wszystkie te elementy są już spełnione, świetnie — przejdźmy dalej.

## Krok 1: Jak wyświetlić informacje – inicjalizacja klienta AsposeAI

Zanim będziemy mogli **wyświetlić listę lokalnych modeli**, potrzebujemy obiektu klienta, który komunikuje się z runtime AsposeAI. Ten krok jest fundamentem; bez niego reszta kodu spowodowałaby `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Dlaczego to ważne*: Inicjalizacja klienta ustanawia sesję z lokalnym silnikiem inferencji, ładując niezbędne natywne biblioteki. Dodatkowo weryfikuje, czy Twoja licencja jest aktywna, zapobiegając niejasnym błędom przy późniejszych zapytaniach o modele.

> **Pro tip**: Jeśli uruchamiasz to na serwerze CI, ustaw zmienną `ASPOSEAI_LICENSE` w środowisku, aby klient mógł wystartować bez interaktywnych promptów.

## Krok 2: Lista lokalnych modeli – pobranie dostępnych modeli

Teraz, gdy klient jest gotowy, możemy **wyświetlić listę lokalnych modeli**. Metoda `list_local()` zwraca kolekcję obiektów, z właściwościami takimi jak `name`, `size_mb` i `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Co się dzieje w tle*: `list_local()` skanuje katalog, w którym AsposeAI buforuje pliki modeli (`~/.asposeai/models` domyślnie) i tworzy lekkie obiekty metadanych. Jest to szybkie, ponieważ nie ładuje wag modelu — tylko odczytuje mały manifest JSON.

Jeśli kiedykolwiek zastanawiałeś się, czy konkretny model jest już zbuforowany, to wywołanie jest najszybszym sposobem, aby to potwierdzić.

## Krok 3: Wyświetlenie nazwy modelu, rozmiaru i ostatniego użycia

Mając modele w ręku, w końcu **wyświetlamy informacje** iterując po kolekcji i drukując każde pole. To miejsce, w którym **wyświetlamy nazwę modelu**, **pokazujemy rozmiar modelu** oraz **pokazujemy ostatnie użycie** w jednej schludnej linii.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Oczekiwany wynik** (Twoje znaczniki czasu będą się różnić):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Dlaczego formatujemy w ten sposób*: Myślnik (`–`) oddziela pola dla czytelności, a linia nagłówka sprawia, że wyjście w konsoli jest przyjazne do skanowania. Jeśli później potrzebujesz formatu maszynowego (CSV, JSON), możesz łatwo zamienić wywołanie `print` na `writer.writerow` lub `json.dump`.

### Obsługa przypadków brzegowych

- **Brak zbuforowanych modeli** – `list_local()` zwraca pustą listę. Pętla po prostu nie wykona się, pozostawiając jedynie nagłówek. Warto dodać zabezpieczenie:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Brakujące atrybuty** – W rzadkich przypadkach manifest może być uszkodzony. Dostęp do `model_info.last_used` może wywołać `AttributeError`. Owiń `print` w `try/except`, jeśli przewidujesz takie problemy.

- **Duże katalogi modeli** – Jeśli masz setki modeli, rozważ stronicowanie wyjścia lub zapis do pliku zamiast drukowania w konsoli.

## Wizualne podsumowanie (opcjonalnie)

Jeśli wolisz szybki podgląd wizualny, poniższy diagram ilustruje przepływ od inicjalizacji klienta do finalnego wyświetlenia.

![Diagram showing how to display info from AsposeAI client](/images/how-to-display-info.png "how to display info diagram")

*Alt text*: **how to display info** – schematic of AsposeAI client initialization, model listing, and info display.

## Pełny działający skrypt

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia skrypt:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Zapisz go jako `list_models.py`, nadaj uprawnienia wykonywalne (`chmod +x list_models.py`) i uruchom:

```bash
./list_models.py
```

Zobaczysz schludną listę przedstawioną wcześniej.

## Zakończenie

Przeprowadziliśmy **wyświetlanie informacji** z AsposeAI poprzez **listowanie lokalnych modeli**, a następnie **wyświetlenie nazwy modelu**, **pokazanie rozmiaru modelu** i **pokazanie ostatniego użycia**. Podejście jest lekkie, wymaga tylko standardowego pakietu `asposeai` i może być wstawione do dowolnego pipeline'u automatyzacji lub sesji debugowania.

Od tego momentu możesz:

- Eksportować wynik do CSV dla analizy w arkuszu kalkulacyjnym (moduł `csv`).
- Przekazywać znaczniki czasu do pulpitu monitorującego, aby alarmować o przestarzałych modelach.
- Połączyć ten skrypt z `aspose_ai.download()`, aby automatycznie odświeżać modele, które nie były używane od pewnego czasu.

Pamiętaj, że przejrzysta widoczność Twojego zasobu modeli oszczędza czas, zmniejsza nadmiarowe zużycie dysku i utrzymuje Twoje usługi AI w płynnym działaniu. Wypróbuj skrypt, dopasuj formatowanie do własnych upodobań i niech stanie się stałym elementem Twojego zestawu narzędzi.

Miłego kodowania i niech Twoje modele zawsze będą aktualne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}