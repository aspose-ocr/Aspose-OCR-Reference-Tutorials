---
date: 2026-02-22
description: Dowiedz się, jak przeprowadzić analizę układu OCR, rozpoznając linie
  tekstu na obrazie i wyodrębniając prostokąty linii przy użyciu Aspose.OCR dla .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Analiza układu OCR – Pobierz prostokąty linii z obrazów
url: /pl/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analiza układu OCR – Pobieranie prostokątów linii z obrazów

## Wprowadzenie

W tym samouczku odkryjesz **jak uzyskać prostokąty linii OCR** przy użyciu Aspose.OCR dla .NET. Po zakończeniu przewodnika będziesz w stanie **rozpoznawać linie tekstu na obrazie** oraz **wyodrębniać współrzędne linii** dla każdej wykrytej linii — idealne do dalszego przetwarzania, takiego jak **analiza układu OCR**, ekstrakcja danych lub renderowanie niestandardowe.

## Szybkie odpowiedzi
- **Co oznacza „pobieranie prostokątów linii OCR”?** Zwraca ramki ograniczające każdą wykrytą linię tekstu na obrazie.  
- **Która metoda API jest używana?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Obsługiwane formaty obrazów?** PNG, JPEG, BMP, TIFF i inne.  
- **Czy mogę uruchomić to na .NET Core?** Tak, Aspose.OCR w pełni obsługuje .NET Core oraz .NET 5/6.

## Wymagania wstępne

Zanim zagłębisz się w samouczek, upewnij się, że spełniasz następujące wymagania:

- Podstawowa znajomość C# i programowania w .NET.  
- Zintegrowane środowisko programistyczne (IDE), takie jak Visual Studio.  
- Zainstalowana biblioteka Aspose.OCR dla .NET. Możesz ją pobrać [tutaj](https://releases.aspose.com/ocr/net/).  
- Przykładowy obraz zawierający tekst do rozpoznania OCR.

## Importowanie przestrzeni nazw

Upewnij się, że w projekcie zaimportowano niezbędne przestrzenie nazw. Dodaj następujące wiersze na początku pliku C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Teraz rozbijmy proces pobierania prostokątów linii w rozpoznawaniu obrazu OCR na łatwe do śledzenia kroki.

## analiza układu ocr – Przewodnik krok po kroku

### Krok 1: Ustaw katalog dokumentu

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Zastąp `"Your Document Directory"` rzeczywistą ścieżką do folderu, w którym znajduje się Twój przykładowy obraz.

### Krok 2: Zainicjalizuj Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Utwórz instancję klasy `AsposeOcr`, aby uzyskać dostęp do funkcji OCR.

### Krok 3: Określ ścieżkę do obrazu

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Zdefiniuj pełną ścieżkę do obrazu, na którym chcesz wykonać OCR.

### Krok 4: Rozpoznaj obraz i pobierz prostokąty

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metoda `GetRectangles` zwraca listę obiektów `Rectangle`, z których każdy reprezentuje współrzędne wykrytej linii tekstu. To jest sedno **pobierania prostokątów linii OCR** i umożliwia **analizę układu OCR**.

### Krok 5: Wypisz wynik

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Wypisz współrzędne wykrytych obszarów na konsolę. Zobaczysz wartości, które później możesz użyć do **wyodrębniania współrzędnych linii** w przetwarzaniu niestandardowym.

## Dlaczego używać Aspose.OCR do prostokątów linii?

- **Wysoka dokładność** – Zaawansowane algorytmy wykrywają linie nawet w zaszumionych lub przechylonych obrazach.  
- **Cross‑platform** – Działa na .NET Framework, .NET Core oraz .NET 5/6.  
- **Brak zewnętrznych zależności** – Czysta biblioteka .NET, bez natywnych plików DLL do dystrybucji.  
- **Bogaty wynik** – Oprócz prostokątów linii możesz także pobrać słowa, znaki i wyniki pewności.

## Typowe problemy i rozwiązania

| Problem | Rozwiązanie |
|-------|----------|
| **Brak zwróconych prostokątów** | Upewnij się, że obraz zawiera wyraźny, poziomy tekst oraz że określono `AreasType.LINES`. |
| **Nieprawidłowe współrzędne** | Sprawdź DPI obrazu; obrazy o niskiej rozdzielczości mogą powodować nieprecyzyjne granice. |
| **Wąskie gardło wydajności przy dużych obrazach** | Zmień rozmiar obrazu do rozsądnej rozdzielczości przed wywołaniem `GetRectangles`. |
| **Wyjątek licencyjny** | Użyj licencji próbnej do testów; zastosuj pełną licencję w produkcji, aby uniknąć ograniczeń wersji testowej. |

## Najczęściej zadawane pytania

**P: Czy mogę wyodrębnić pojedyncze słowa zamiast całych linii?**  
O: Tak, użyj `AreasType.WORDS` z tą samą metodą `GetRectangles`, aby uzyskać ramki ograniczające na poziomie słów.

**P: Czy API obsługuje wielostronicowe pliki PDF?**  
O: Najpierw przekonwertuj każdą stronę PDF na obraz, a następnie wywołaj `GetRectangles` dla każdego obrazu.

**P: Jak obsłużyć obrócony tekst?**  
O: Włącz opcję auto‑obrotu w ustawieniach OCR lub wstępnie obróć obraz przed przetwarzaniem.

**P: Czy istnieje sposób na uzyskanie wyników pewności dla każdej linii?**  
O: Po uzyskaniu prostokątów wywołaj `api.RecognizeImage(...).Lines`, aby uzyskać obiekty linii zawierające wartości pewności.

**P: Jakie wersje .NET są kompatybilne?**  
O: Biblioteka działa z .NET Framework 4.5+, .NET Core 3.1+ oraz .NET 5/6.

## Przykłady zastosowań w rzeczywistym świecie

- **Analiza układu dokumentu OCR** – Przekaż prostokąty linii do silnika układu, aby odtworzyć struktury kolumn.  
- **Automatyczna ekstrakcja danych** – Użyj współrzędnych do wycięcia poszczególnych linii dla dalszych potoków NLP.  
- **Renderowanie niestandardowe** – Nałóż ramki ograniczające na oryginalny obraz w celu wizualnej weryfikacji lub nakładek UI.

## Podsumowanie

Gratulacje! Pomyślnie **uzyskałeś prostokąty linii OCR** dla obrazu przy użyciu Aspose.OCR dla .NET. Mając ramki ograniczające, możesz teraz przekazać współrzędne linii do dalszych przepływów pracy, takich jak renderowanie niestandardowe, ekstrakcja danych lub **analiza układu OCR**.

---

**Ostatnia aktualizacja:** 2026-02-22  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}