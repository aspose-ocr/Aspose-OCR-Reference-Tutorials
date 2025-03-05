---
title: Uzyskaj prostokąty dla linii w rozpoznawaniu obrazu OCR
linktitle: Uzyskaj prostokąty dla linii w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Poznaj Aspose.OCR dla .NET, Twój klucz do precyzyjnego rozpoznawania obrazów OCR. Uwolnij moc ekstrakcji tekstu bez wysiłku.
type: docs
weight: 10
url: /pl/net/image-and-drawing-recognition/get-rectangles-for-lines/
---
## Wstęp

Witamy w świecie Aspose.OCR dla .NET, potężnego narzędzia, które pozwala wykorzystać potencjał optycznego rozpoznawania znaków (OCR) w aplikacjach .NET. Niezależnie od tego, czy jesteś doświadczonym programistą, czy ciekawskim entuzjastą, ten przewodnik przeprowadzi Cię przez proces uzyskiwania prostokątów dla linii w rozpoznawaniu obrazów OCR przy użyciu Aspose.OCR.

## Warunki wstępne

Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:

- Podstawowa znajomość programowania w C# i .NET.
- Zintegrowane środowisko programistyczne (IDE), takie jak Visual Studio.
-  Zainstalowana biblioteka Aspose.OCR dla .NET. Możesz go pobrać[Tutaj](https://releases.aspose.com/ocr/net/).
- Przykładowy obraz zawierający tekst do rozpoznawania OCR.

## Importuj przestrzenie nazw

Upewnij się, że do projektu zaimportowano niezbędne przestrzenie nazw. Dodaj następujące wiersze na górze pliku C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Podzielmy teraz proces uzyskiwania prostokątów dla linii w rozpoznawaniu obrazu OCR na łatwe do wykonania kroki.

## Krok 1: Skonfiguruj katalog dokumentów

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// RozwińKoniec:3
```

 Zastępować`"Your Document Directory"` z rzeczywistą ścieżką do katalogu dokumentów.

## Krok 2: Zainicjuj Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// RozwińKoniec:4
```

 Utwórz instancję`AsposeOcr` class, aby uzyskać dostęp do funkcjonalności OCR.

## Krok 3: Określ ścieżkę obrazu

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// RozwińKoniec:5
```

Zdefiniuj pełną ścieżkę do obrazu, na którym chcesz wykonać OCR.

## Krok 4: Rozpoznaj obraz i uzyskaj prostokąty

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// RozwińKoniec:6
```

 Skorzystaj z`GetRectangles` metoda pobierania prostokątów dla linii w określonym obrazie.

## Krok 5: Wydrukuj wynik

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// RozwińKoniec:7
```

Wydrukuj współrzędne wykrytych obszarów na konsoli.

## Wniosek

Gratulacje! Pomyślnie uzyskałeś prostokąty dla linii w rozpoznawaniu obrazu OCR przy użyciu Aspose.OCR dla .NET. To wszechstronne narzędzie otwiera świat możliwości wyodrębniania tekstu z aplikacji.

## Często zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla .NET z dowolnym typem obrazu?

Odpowiedź 1: Aspose.OCR obsługuje szeroką gamę formatów obrazów, zapewniając elastyczność w aplikacjach OCR.

### P2: Jak dokładne jest rozpoznawanie OCR?

Odpowiedź 2: Aspose.OCR wykorzystuje zaawansowane algorytmy zapewniające wysoką dokładność, dzięki czemu nadaje się do różnych scenariuszy rozpoznawania tekstu.

### P3: Czy dostępna jest wersja próbna?

 O3: Tak, możesz poznać możliwości Aspose.OCR dla .NET za pomocą[bezpłatna wersja próbna](https://releases.aspose.com/).

### P4: Gdzie mogę znaleźć obszerną dokumentację?

 A4: Patrz[dokumentacja](https://reference.aspose.com/ocr/net/) szczegółowe informacje i wskazówki dotyczące użytkowania.

### P5: Potrzebujesz pomocy lub masz konkretne pytania?

 A5: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie społeczności i dyskusje.