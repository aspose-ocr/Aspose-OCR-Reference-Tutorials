---
description: Dowiedz się, jak określić dozwolone znaki w OCR przy użyciu Aspose.OCR
  dla .NET i skutecznie rozpoznawać obrazy cyfr. Skorzystaj z przewodnika krok po
  kroku, aby ograniczyć OCR wyłącznie do cyfr.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Określ dozwolone znaki OCR – użycie Aspose.OCR dla .NET
url: /pl/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Określanie dozwolonych znaków OCR – użycie Aspose.OCR dla .NET

W tym samouczku dowiesz się, jak **specify allowed characters ocr** przy użyciu Aspose.OCR dla .NET, co pozwala ograniczyć wynik OCR tylko do potrzebnych znaków. Jest to szczególnie przydatne, gdy musisz **recognize digits image** pliki, takie jak numery seryjne, identyfikatory faktur lub ciągi podobne do kodów kreskowych. Przejdziemy przez konfigurację, kod i kilka praktycznych scenariuszy, abyś mógł od razu zastosować tę technikę.

## Szybkie odpowiedzi
- **Co robi “specify allowed characters ocr”?** Ogranicza OCR do zdefiniowanego zestawu znaków, zwiększając dokładność dla określonych danych.  
- **Jakie znaki mogę zezwolić?** Dowolna kombinacja, której potrzebujesz — cyfry, litery lub własne symbole (np. „0123456789”).  
- **Dlaczego ograniczać znaki?** Zmniejsza liczbę błędnych rozpoznawań i przyspiesza przetwarzanie, gdy znany jest oczekiwany zestaw znaków.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w fazie rozwoju; licencja komercyjna jest wymagana w produkcji.  
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Czym jest “specify allowed characters ocr”?
Gdy OCR skanuje obraz, próbuje dopasować każdy wzór wizualny do pełnego alfabetu możliwych znaków. Dzięki **specify allowed characters ocr** informujesz silnik, aby ignorował wszystko poza Twoją białą listą, co znacząco poprawia dokładność rozpoznawania w ograniczonych zestawach danych.

## Dlaczego używać Aspose.OCR do rozpoznawania digits image?
Aspose.OCR oferuje czyste, płynne API dla programistów .NET. Wbudowana opcja `AllowedCharacters` pozwala skupić się na scenariuszach wyłącznie z cyframi, bez konieczności pisania własnej logiki post‑processingowej. Jest to idealne rozwiązanie dla:
- Odczytywania wskazań liczników, numerów faktur lub kodów produktów.  
- Walidacji danych wprowadzonych przez użytkownika, przechwyconych ze skanowanych formularzy.  
- Przyspieszania przetwarzania wsadowego, gdy zestaw znaków jest znany z góry.

## Wymagania wstępne

Przed zanurzeniem się w kod, upewnij się, że masz:

- Podstawową znajomość programowania w .NET.  
- **Aspose.OCR for .NET** library. Możesz pobrać go [tutaj](https://releases.aspose.com/ocr/net/).  
- Visual Studio (lub dowolne preferowane IDE .NET).  

## Importowanie przestrzeni nazw

W swoim projekcie .NET zaimportuj niezbędne przestrzenie nazw, aby wykorzystać funkcjonalność Aspose.OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Teraz podzielimy samouczek na serię szczegółowych kroków:

## Jak określić dozwolone znaki OCR – przewodnik krok po kroku

### Krok 1: Ustaw ścieżkę do folderu z obrazami

Najpierw określ, gdzie przechowywane są Twoje przykładowe obrazy.

```csharp
string dataDir = "Your Document Directory";
```

### Krok 2: Zainicjalizuj Aspose.OCR z białą listą zawierającą tylko cyfry

Utwórz instancję `AsposeOcr` i przekaż znaki, które chcesz zezwolić — w tym przypadku wszystkie cyfry.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Krok 3: Rozpoznaj pojedynczą linię zawierającą cyfry

Użyj metody `RecognizeLine`, aby wyodrębnić tekst z obrazu zawierającego wyłącznie liczby.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Krok 4: Wyświetl rozpoznane cyfry

Wypisz wynik w konsoli, aby móc zweryfikować rezultat.

```csharp
Console.WriteLine(result);
```

### Krok 5: Użyj RecognitionSettings dla większej kontroli

Jeśli potrzebujesz dokładniejszej kontroli — np. wymuszenia rozpoznawania jednej linii — możesz użyć przeciążenia przyjmującego `RecognitionSettings`.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Krok 6: Wyświetl wynik drugiego przypadku

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Krok 7: Potwierdź pomyślne wykonanie

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Postępując zgodnie z tymi krokami, nauczyłeś się, jak **specify allowed characters ocr** i efektywnie **recognize digits image** treść przy użyciu Aspose.OCR dla .NET.

## Typowe pułapki i rozwiązywanie problemów
- **Pusty wynik:** Upewnij się, że jakość obrazu jest wystarczająca (wyraźny kontrast, minimalny szum).  
- **Zwrócono nieprawidłowe znaki:** Sprawdź dokładnie, czy ciąg białej listy dokładnie odpowiada oczekiwanym znakom.  
- **Plik nie znaleziony:** Zweryfikuj, że `dataDir` wskazuje właściwy folder oraz że nazwa pliku jest zgodna z wielkością liter.

## Najczęściej zadawane pytania

### Q1: Czy Aspose.OCR dla .NET jest odpowiedni zarówno dla początkujących, jak i doświadczonych programistów?  
**A:** Zdecydowanie! API jest zaprojektowane tak, aby było intuicyjne dla nowicjuszy, a jednocześnie oferowało zaawansowane opcje dla zaawansowanych użytkowników.

### Q2: Czy mogę używać Aspose.OCR dla .NET do rozpoznawania znaków w wielu językach?  
**A:** Tak, Aspose.OCR obsługuje szeroką gamę języków. Możesz połączyć pakiety językowe z funkcją dozwolonych znaków w scenariuszach wielojęzycznych.

### Q3: Jak często aktualizowany jest Aspose.OCR dla .NET?  
**A:** Aktualizacje są wydawane regularnie, aby dodawać nowe funkcje, poprawiać dokładność i zapewniać kompatybilność. Sprawdź [dokumentację](https://reference.aspose.com/ocr/net/) po najnowsze szczegóły wersji.

### Q4: Czy dostępna jest darmowa wersja próbna Aspose.OCR dla .NET?  
**A:** Tak, możesz zapoznać się z możliwościami, pobierając [darmową wersję próbną](https://releases.aspose.com/).

### Q5: Gdzie mogę uzyskać pomoc lub połączyć się ze społecznością w celu wsparcia?  
**A:** Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby zadawać pytania, dzielić się doświadczeniami i uzyskać pomoc zarówno od inżynierów Aspose, jak i innych programistów.

---

**Ostatnia aktualizacja:** 2026-02-15  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}