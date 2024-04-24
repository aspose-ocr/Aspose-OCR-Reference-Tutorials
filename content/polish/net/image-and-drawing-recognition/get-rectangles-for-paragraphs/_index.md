---
title: Uzyskaj prostokąty dla akapitów w rozpoznawaniu obrazu OCR
linktitle: Uzyskaj prostokąty dla akapitów w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj zaawansowane możliwości OCR dzięki Aspose.OCR dla .NET. Wyodrębnij prostokąty akapitów bez wysiłku.
type: docs
weight: 11
url: /pl/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---
## Wstęp

Witamy w naszym obszernym przewodniku na temat wykorzystania Aspose.OCR dla .NET do wyodrębniania prostokątów akapitów w rozpoznawaniu obrazów OCR. Jeśli chcesz zwiększyć możliwości przetwarzania dokumentów i wykorzystać możliwości optycznego rozpoznawania znaków (OCR) w aplikacjach .NET, jesteś we właściwym miejscu.

## Warunki wstępne

Zanim przejdziemy do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:

- Podstawowa znajomość programowania w C# i .NET.
-  Środowisko programistyczne skonfigurowane za pomocą Aspose.OCR dla .NET. Jeśli jeszcze tego nie zrobiłeś, możesz go pobrać[Tutaj](https://releases.aspose.com/ocr/net/).
- Zrozumienie koncepcji przetwarzania obrazu i znaczenia OCR w wyodrębnianiu tekstu z obrazów.

## Importuj przestrzenie nazw

Upewnij się, że w kodzie C# zaimportowano niezbędne przestrzenie nazw, aby efektywnie korzystać z Aspose.OCR. Umieść następujące informacje na górze pliku:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Skonfiguruj katalog dokumentów

Rozpocznij od zainicjowania ścieżki do katalogu dokumentów, w którym przechowywane są obrazy do przetwarzania OCR:

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Zainicjuj instancję AsposeOcr

Utwórz instancję klasy AsposeOcr, aby uzyskać dostęp do funkcjonalności OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Krok 3: Określ ścieżkę obrazu

Zdefiniuj pełną ścieżkę do obrazu, który chcesz przetworzyć:

```csharp
string fullPath = dataDir + "sample.png";
```

## Krok 4: Rozpoznaj obraz i uzyskaj prostokąty akapitu

 Wywołaj`GetRectangles` metoda uzyskiwania prostokątów dla akapitów w obrazie OCR. Ustawić`detect_areas` Do`true` jeśli chcesz wyodrębnić akapity:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Krok 5: Wydrukuj wyniki

Wydrukuj współrzędne zidentyfikowanych obszarów:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Krok 6: Wniosek

Gratulacje! Pomyślnie wykonałeś proces rozpoznawania obrazu OCR w celu uzyskania prostokątów dla akapitów przy użyciu Aspose.OCR dla .NET.

## Wniosek

W tym samouczku omówiliśmy podstawowe kroki integracji Aspose.OCR dla .NET z aplikacjami, umożliwiając wyodrębnienie prostokątów akapitów z obrazów przetworzonych przez OCR. Aspose.OCR upraszcza wdrażanie OCR, czyniąc go cennym narzędziem do przetwarzania dokumentów i ekstrakcji tekstu.

## Często zadawane pytania

### P1: Czy Aspose.OCR jest kompatybilny z różnymi formatami obrazów?

O1: Tak, Aspose.OCR obsługuje różne formaty obrazów, w tym PNG, JPEG i TIFF.

### P2: Czy mogę używać Aspose.OCR do przetwarzania wsadowego wielu obrazów?

A2: Absolutnie! Aspose.OCR ułatwia przetwarzanie wsadowe, aby płynnie obsługiwać wiele obrazów.

### P3: Czy dostępna jest bezpłatna wersja próbna Aspose.OCR dla .NET?

 Odpowiedź 3: Tak, możesz skorzystać z bezpłatnego okresu próbnego[Tutaj](https://releases.aspose.com/).

### P4: Jak mogę uzyskać tymczasową licencję na Aspose.OCR?

 Odpowiedź 4: Możesz nabyć licencję tymczasową[Tutaj](https://purchase.aspose.com/temporary-license/).

### P5: Gdzie mogę znaleźć dodatkowe wsparcie i dyskusje związane z Aspose.OCR?

 A5: Udaj się do[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie społeczności i dyskusje.