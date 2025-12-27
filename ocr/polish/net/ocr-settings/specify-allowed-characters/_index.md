---
date: 2025-12-27
description: Dowiedz się, jak używać konwersji obrazu OCR na tekst z Aspose.OCR dla
  .NET, określając dozwolone znaki i precyzyjnie dostosowując ustawienia rozpoznawania
  OCR. Zawiera kod do rozpoznawania obrazu cyfr.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'OCR obraz na tekst: określ dozwolone znaki w OCR'
url: /pl/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: Określenie dozwolonych znaków w OCR

## Wprowadzenie

W ciągle zmieniającym się krajobrazie technologii, rozpoznawanie znaków optycznych (OCR) – lub konwersja **ocr image to text** – stało się przełomowym narzędziem, umożliwiającym maszynom rozumienie tekstu z obrazów. Aspose.OCR for .NET wyróżnia się jako potężne rozwiązanie, zapewniając płynną integrację dla deweloperów poszukujących solidnych możliwości OCR w swoich aplikacjach .NET.

## Szybkie odpowiedzi
- **Co robi „Specify Allowed Characters”?** Ogranicza wynik OCR do określonego zestawu znaków, na przykład tylko cyfr.  
- **Która metoda wyodrębnia pojedynczą linię tekstu?** `RecognizeLine` zwraca pierwszą wykrytą linię.  
- **Czy mogę zmienić ustawienia rozpoznawania OCR w locie?** Tak – użyj `RecognitionSettings`, aby dostosować opcje takie jak `AllowedCharacters`.  
- **Czy dostępna jest wersja próbna?** Oczywiście, pobierz darmową wersję próbną ze strony Aspose.  
- **Jakie wersje .NET są obsługiwane?** Wszystkie współczesne wersje .NET Framework oraz .NET Core/5/6.

## Wymagania wstępne

Zanim zanurzysz się w samouczek, upewnij się, że spełniasz następujące wymagania:

- Praktyczna znajomość programowania w .NET.  
- Biblioteka Aspose.OCR for .NET. Możesz ją pobrać [tutaj](https://releases.aspose.com/ocr/net/).  
- Znajomość Visual Studio lub innego preferowanego środowiska programistycznego .NET.

## Importowanie przestrzeni nazw

W swoim projekcie .NET zaimportuj niezbędne przestrzenie nazw, aby skutecznie wykorzystać funkcje Aspose.OCR for .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Teraz rozbijmy samouczek na serię kompleksowych kroków:

## Krok 1: Określenie dozwolonych znaków w ocr image to text

Aby rozpocząć, ustaw ścieżkę do katalogu z dokumentami:

```csharp
string dataDir = "Your Document Directory";
```

## Krok 2: Inicjalizacja Aspose.OCR z dozwolonymi symbolami (rozpoznawanie obrazu cyfr)

Utwórz instancję `AsposeOcr`, określając dozwolone symbole. W tym przypadku zezwalamy wyłącznie na cyfry (0‑9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Krok 3: Rozpoznanie obrazu

Wykorzystaj instancję `AsposeOcr` do rozpoznania tekstu z obrazu:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Krok 4: Wyświetlenie rozpoznanego tekstu

Wypisz rozpoznany tekst w konsoli:

```csharp
Console.WriteLine(result);
```

## Krok 5: Drugi przypadek – Rozpoznanie obrazu ze specyficznymi ustawieniami rozpoznawania OCR

Zainicjalizuj kolejną instancję `AsposeOcr`, tym razem z bardziej szczegółowymi ustawieniami, które demonstrują użycie **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Krok 6: Wyświetlenie rozpoznanego tekstu z drugiego przypadku

Wypisz rozpoznany tekst z drugiego przypadku w konsoli:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Krok 7: Udane wykonanie

Na koniec potwierdź pomyślne wykonanie samouczka **SpecifyAllowedCharacters**:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Postępując zgodnie z tymi krokami, odblokowałeś możliwość **określenia dozwolonych znaków** w rozpoznawaniu obrazu OCR przy użyciu Aspose.OCR for .NET, umożliwiając precyzyjną konwersję **ocr image to text** dla scenariuszy tylko z cyframi.

## Dlaczego stosować filtrowanie dozwolonych znaków?

- **Wyższa dokładność:** Ograniczenie zestawu znaków zmniejsza liczbę błędnych rozpoznań, szczególnie w szumnych obrazach.  
- **Zwiększenie wydajności:** Silnik OCR pomija nieistotne glify, przyspieszając przetwarzanie.  
- **Zgodność:** Wymusza formaty danych (np. numery faktur, kody seryjne) już na etapie OCR.

## Częste pułapki i wskazówki

- **Pułapka:** Podanie pustego ciągu dla dozwolonych znaków wyłącza filtrowanie.  
  **Wskazówka:** Zawsze podawaj niepusty ciąg lub użyj wyliczenia `CharactersAllowedType`.  
- **Pułapka:** Użycie `RecognizeLine` w dokumentach wieloliniowych może pominąć dane.  
  **Wskazówka:** Przejdź na `RecognizeImage` z `RecognizeSingleLine = false`, aby wyodrębnić całą stronę.  
- **Pułapka:** Nieprawidłowe łączenie ścieżki katalogu może spowodować `FileNotFoundException`.  
  **Wskazówka:** Użyj `Path.Combine(dataDir, "file.jpg")` dla ścieżek niezależnych od platformy.

## Najczęściej zadawane pytania

**P:** Czy Aspose.OCR for .NET jest odpowiedni zarówno dla początkujących, jak i doświadczonych deweloperów?  
**O:** Zdecydowanie! API jest intuicyjne dla nowicjuszy, a jednocześnie oferuje zaawansowane ustawienia dla zaawansowanych użytkowników.

**P:** Czy mogę używać Aspose.OCR for .NET do rozpoznawania znaków w wielu językach?  
**O:** Tak, Aspose.OCR obsługuje szeroką gamę języków; możesz także łączyć pakiety językowe w projektach wielojęzycznych.

**P:** Jak często aktualizowany jest Aspose.OCR for .NET?  
**O:** Aktualizacje są wydawane regularnie, aby nadążać za nowymi wersjami .NET i ulepszeniami OCR. Sprawdź [dokumentację](https://reference.aspose.com/ocr/net/) pod kątem najnowszej wersji.

**P:** Czy dostępna jest darmowa wersja próbna Aspose.OCR for .NET?  
**O:** Tak, możesz zapoznać się z możliwościami, pobierając [darmową wersję próbną](https://releases.aspose.com/).

**P:** Gdzie mogę uzyskać pomoc lub połączyć się ze społecznością w celu wsparcia?  
**O:** Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby skontaktować się z ekspertami i innymi deweloperami.

---

**Ostatnia aktualizacja:** 2025-12-27  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}