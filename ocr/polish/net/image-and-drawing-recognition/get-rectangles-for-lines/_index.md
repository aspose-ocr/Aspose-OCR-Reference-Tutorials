---
date: 2025-12-17
description: Dowiedz się, jak uzyskać prostokąty linii OCR przy użyciu Aspose.OCR
  dla .NET, aby rozpoznawać linie tekstu na obrazach i łatwo wyodrębniać współrzędne
  linii.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Pobierz prostokąty linii OCR dla linii tekstu na obrazie
url: /pl/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uzyskaj prostokąty linii OCR dla tekstu na obrazie

## Wprowadzenie

W tym samouczku odkryjesz **jak uzyskać prostokąty linii OCR** przy użyciu Aspose.OCR dla .NET. Po zakończeniu przewodnika będziesz w stanie **rozpoznawać linie tekstu na obrazie** i **wyodrębniać współrzędne linii** dla każdej wykrytej linii — idealne do dalszego przetwarzania, takiego jak analiza układu, ekstrakcja danych lub własne renderowanie.

## Szybkie odpowiedzi
- **Co oznacza „uzyskać prostokąty linii OCR”?** Zwraca ramki ograniczające każdą wykrytą linię tekstu na obrazie.  
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

Upewnij się, że w projekcie zaimportowano niezbędne przestrzenie nazw. Dodaj następujące linie na początku pliku C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Teraz rozbijmy proces uzyskiwania prostokątów linii w rozpoznawaniu obrazu OCR na łatwe do wykonania kroki.

## Krok 1: Skonfiguruj katalog dokumentów

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Zastąp `"Your Document Directory"` rzeczywistą ścieżką do folderu zawierającego Twój przykładowy obraz.

## Krok 2: Zainicjalizuj Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Utwórz instancję klasy `AsposeOcr`, aby uzyskać dostęp do funkcjonalności OCR.

## Krok 3: Określ ścieżkę do obrazu

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Zdefiniuj pełną ścieżkę do obrazu, na którym chcesz wykonać OCR.

## Krok 4: Rozpoznaj obraz i uzyskaj prostokąty

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metoda `GetRectangles` zwraca listę obiektów `Rectangle`, z których każdy reprezentuje współrzędne wykrytej linii tekstu. To jest sedno **uzyskiwania prostokątów linii OCR**.

## Krok 5: Wypisz wynik

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Wypisz współrzędne wykrytych obszarów na konsolę. Zobaczysz wartości, które później możesz użyć do **wyodrębniania współrzędnych linii** w niestandardowym przetwarzaniu.

## Dlaczego warto używać Aspose.OCR do prostokątów linii?

- **Wysoka dokładność** – Zaawansowane algorytmy wykrywają linie nawet w zaszumionych lub przechylonych obrazach.  
- **Wieloplatformowość** – Działa na .NET Framework, .NET Core oraz .NET 5/6.  
- **Brak zewnętrznych zależności** – Czysta biblioteka .NET, bez natywnych DLL do dystrybucji.  
- **Bogaty wynik** – Oprócz prostokątów linii możesz także pobrać słowa, znaki i wyniki pewności.

## Typowe problemy i rozwiązania

| Problem | Rozwiązanie |
|---------|-------------|
| **Brak zwróconych prostokątów** | Upewnij się, że obraz zawiera wyraźny, poziomy tekst i że określono `AreasType.LINES`. |
| **Nieprawidłowe współrzędne** | Sprawdź DPI obrazu; obrazy o niskiej rozdzielczości mogą powodować nieprecyzyjne granice. |
| **Wąskie gardło wydajności przy dużych obrazach** | Zmień rozmiar obrazu do rozsądnej rozdzielczości przed wywołaniem `GetRectangles`. |
| **Wyjątek licencyjny** | Użyj licencji próbnej do testów; zastosuj pełną licencję w produkcji, aby uniknąć limitów wersji ewaluacyjnej. |

## FAQ

### P1: Czy mogę używać Aspose.OCR dla .NET z dowolnym typem obrazu?

O1: Aspose.OCR obsługuje szeroką gamę formatów obrazów, zapewniając elastyczność w Twoich aplikacjach OCR.

### P2: Jak dokładne jest rozpoznawanie OCR?

O2: Aspose.OCR wykorzystuje zaawansowane algorytmy zapewniające wysoką dokładność, co czyni go odpowiednim dla różnych scenariuszy rozpoznawania tekstu.

### P3: Czy dostępna jest wersja próbna?

O3: Tak, możesz zapoznać się z możliwościami Aspose.OCR dla .NET korzystając z [darmowej wersji próbnej](https://releases.aspose.com/).

### P4: Gdzie mogę znaleźć pełną dokumentację?

O4: Odwołaj się do [dokumentacji](https://reference.aspose.com/ocr/net/) po szczegółowe informacje i wytyczne dotyczące użycia.

### P5: Potrzebujesz pomocy lub masz konkretne pytania?

O5: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) w celu uzyskania wsparcia społeczności i dyskusji.

## Najczęściej zadawane pytania

**P: Czy mogę wyodrębnić pojedyncze słowa zamiast całych linii?**  
O: Tak, użyj `AreasType.WORDS` z tą samą metodą `GetRectangles`, aby uzyskać ramki ograniczające na poziomie słów.

**P: Czy API obsługuje wielostronicowe pliki PDF?**  
O: Najpierw skonwertuj każdą stronę PDF na obraz, a następnie wywołaj `GetRectangles` dla każdego obrazu.

**P: Jak radzić sobie z obróconym tekstem?**  
O: Włącz opcję auto‑obrotu w ustawieniach OCR lub wstępnie obróć obraz przed przetwarzaniem.

**P: Czy istnieje sposób na uzyskanie współczynników pewności dla każdej linii?**  
O: Po uzyskaniu prostokątów wywołaj `api.RecognizeImage(...).Lines`, aby uzyskać obiekty linii zawierające wartości pewności.

**P: Z jakimi wersjami .NET jest kompatybilna?**  
O: Biblioteka działa z .NET Framework 4.5+, .NET Core 3.1+, oraz .NET 5/6.

## Zakończenie

Gratulacje! Pomyślnie **uzyskałeś prostokąty linii OCR** dla obrazu przy użyciu Aspose.OCR dla .NET. Mając ramki ograniczające, możesz teraz przekazywać współrzędne linii do dalszych procesów, takich jak własne renderowanie, ekstrakcja danych lub analiza układu.

---

**Ostatnia aktualizacja:** 2025-12-17  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}