---
date: 2025-12-17
description: Dowiedz się, jak wyodrębniać prostokąty dla akapitów w obrazach OCR przy
  użyciu Aspose.OCR dla .NET – kompleksowy przewodnik, jak wyodrębniać prostokąty
  i współrzędne akapitów.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Jak wyodrębnić prostokąty dla akapitów w rozpoznawaniu obrazu OCR
url: /pl/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić prostokąty dla akapitów w rozpoznawaniu obrazu OCR

## Wprowadzenie

Witamy w naszym kompleksowym przewodniku po **wyodrębnianiu prostokątów** dla akapitów w rozpoznawaniu obrazu OCR przy użyciu Aspose.OCR dla .NET. Jeśli chcesz usprawnić swój proces przetwarzania dokumentów, wyodrębnić granice akapitów i zautomatyzować ekstrakcję danych, jesteś we właściwym miejscu. Przeprowadzimy Cię przez każdy krok — od konfiguracji środowiska po wypisanie współrzędnych prostokątów — abyś mógł od razu korzystać z wyników OCR.

## Szybkie odpowiedzi
- **Co oznacza „wyodrębnić prostokąty”?** Zwraca ramki ograniczające (x, y, szerokość, wysokość) wykrytych obszarów tekstowych.  
- **Która metoda API dostarcza prostokąty?** `AsposeOcr.GetRectangles` z `AreasType.PARAGRAPHS`.  
- **Czy potrzebna jest licencja do rozwoju?** Darmowa wersja próbna wystarczy do testów; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę przetwarzać wiele obrazów jednocześnie?** Tak — iteruj listę obrazów i wywołuj `GetRectangles` dla każdego pliku.  
- **Jakie formaty są obsługiwane?** PNG, JPEG, TIFF, BMP i wiele innych.

## Co oznacza „wyodrębnić prostokąty” w OCR?
W terminologii OCR wyodrębnianie prostokątów oznacza identyfikację geometrycznych granic otaczających każdy akapit lub linię tekstu na obrazie. Te współrzędne pozwalają podświetlić, przyciąć lub dalej analizować konkretne fragmenty zeskanowanego dokumentu.

## Dlaczego wyodrębniać współrzędne akapitów?
- **Precyzyjne przetwarzanie końcowe** – możesz przekazać każdy prostokąt do kolejnych etapów (np. tłumaczenie, redakcja).  
- **Ulepszone UI/UX** – nakładaj ramki ograniczające na oryginalny obraz, aby pokazać użytkownikom, gdzie znaleziono tekst.  
- **Automatyzacja wsadowa** – szybko lokalizuj i izoluj akapity w dużych zestawach dokumentów.

## Wymagania wstępne

- Podstawowa znajomość C# i programowania w .NET.  
- Środowisko programistyczne z zainstalowanym Aspose.OCR dla .NET – możesz je pobrać [tutaj](https://releases.aspose.com/ocr/net/).  
- Znajomość koncepcji przetwarzania obrazu oraz roli OCR w wyodrębnianiu tekstu ze skanów.

## Importowanie przestrzeni nazw

W swoim pliku C# zaimportuj wymagane przestrzenie nazw, aby klasy OCR były dostępne:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Skonfiguruj katalog dokumentów

Zdefiniuj folder zawierający obrazy, które chcesz analizować:

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Zainicjalizuj instancję AsposeOcr

Utwórz obiekt `AsposeOcr` – zapewnia on dostęp do wszystkich funkcji OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Krok 3: Określ ścieżkę do obrazu

Wskaż dokładny plik obrazu, który ma zostać przetworzony:

```csharp
string fullPath = dataDir + "sample.png";
```

## Krok 4: Rozpoznaj obraz i pobierz prostokąty akapitów

Wywołaj metodę `GetRectangles`. Ustawienie `detect_areas` na `true` instruuje silnik, aby zwrócił **prostokąty akapitów**:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Krok 5: Wyświetl wyniki

Wypisz współrzędne, aby zobaczyć **wyodrębnione współrzędne akapitów**, które zostały wykryte:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|--------------|
| Brak zwróconych prostokątów | Zbyt niska jakość obrazu lub niewłaściwy `AreasType` | Upewnij się, że obraz jest wyraźny i użyj `AreasType.PARAGRAPHS`. |
| Współrzędne są przesunięte o jeden | Niezgodność skalowania DPI | Ustaw prawidłowe DPI przy ładowaniu obrazu lub użyj `api.Config.Dpi`. |
| Wyjątek licencyjny | Uruchamianie bez ważnej licencji w produkcji | Zastosuj tymczasową lub stałą licencję poprzez `api.SetLicense`. |

## Najczęściej zadawane pytania

**Q: Czy Aspose.OCR jest kompatybilny z różnymi formatami obrazów?**  
A: Tak, Aspose.OCR obsługuje PNG, JPEG, TIFF, BMP i wiele innych popularnych formatów.

**Q: Czy mogę używać Aspose.OCR do wsadowego przetwarzania wielu obrazów?**  
A: Oczywiście! Przejdź przez kolekcję ścieżek plików i wywołaj `GetRectangles` dla każdego obrazu.

**Q: Czy dostępna jest darmowa wersja próbna Aspose.OCR dla .NET?**  
A: Tak, darmową wersję próbną możesz sprawdzić [tutaj](https://releases.aspose.com/).

**Q: Jak mogę uzyskać tymczasową licencję dla Aspose.OCR?**  
A: Tymczasową licencję możesz nabyć [tutaj](https://purchase.aspose.com/temporary-license/).

**Q: Gdzie znajdę dodatkowe wsparcie i dyskusje związane z Aspose.OCR?**  
A: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) dla wsparcia społeczności i dyskusji.

## Podsumowanie

W tym samouczku pokazaliśmy **jak wyodrębnić prostokąty** dla akapitów przy użyciu Aspose.OCR dla .NET, przeanalizowaliśmy każdy fragment kodu i wyjaśniliśmy, jak interpretować zwrócone współrzędne. Integrując te kroki w swojej aplikacji, możesz niezawodnie wyodrębniać granice akapitów, usprawniać przepływy dokumentów i tworzyć inteligentniejsze rozwiązania oparte na OCR.

---

**Ostatnia aktualizacja:** 2025-12-17  
**Testowano z:** Aspose.OCR 24.11 dla .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}