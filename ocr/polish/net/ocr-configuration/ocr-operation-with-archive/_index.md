---
date: 2025-12-19
description: Dowiedz się, jak wykonywać OCR na obrazach archiwów, konwertować obrazy
  na tekst i wyodrębniać tekst z plików archiwów przy użyciu Aspose.OCR dla .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Jak przeprowadzić OCR na obrazach archiwalnych przy użyciu Aspose.OCR dla .NET
url: /pl/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na obrazach w archiwum przy użyciu Aspose.OCR dla .NET

## Wprowadzenie

W tym obszernej tutorialu odkryjesz **jak wykonać OCR** na zarchiwizowanych plikach graficznych przy użyciu biblioteki Aspose.OCR dla .NET. Niezależnie od tego, czy potrzebujesz **konwertować obrazy na tekst** czy **wyodrębniać tekst z archiwum**, poniższy przewodnik krok po kroku przeprowadzi Cię przez wszystko — od skonfigurowania środowiska programistycznego po pobranie rozpoznanego tekstu z każdego obrazu wewnątrz archiwum ZIP.

## Szybkie odpowiedzi
- **Co obejmuje tutorial?** Przeprowadzanie OCR na obrazach w archiwum (ZIP) przy użyciu Aspose.OCR dla .NET.  
- **Jakie główne słowo kluczowe jest celem?** *how to perform ocr*.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w celach ewaluacyjnych; licencja komercyjna jest wymagana w produkcji.  
- **Jakie wersje .NET są wspierane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Czy mogę dostosować ustawienia rozpoznawania?** Tak — użyj `RecognitionSettings`, aby dopasować dokładność.

## Czym jest OCR i dlaczego używać go w archiwach?

Optical Character Recognition (OCR) przekształca zeskanowane obrazy lub pliki PDF w przeszukiwalny, edytowalny tekst. Gdy obrazy są zgrupowane w archiwum (np. pliku ZIP), wyodrębnianie i rozpoznawanie każdego zdjęcia jednocześnie oszczędza czas i zmniejsza złożoność kodu. Metoda `RecognizeMultipleImages` z Aspose.OCR upraszcza ten proces.

## Wymagania wstępne

- Visual Studio 2019 lub nowszy (lub dowolne IDE zgodne z .NET).  
- .NET Framework 4.5 + lub .NET Core 3.1 + zainstalowany.  
- Dostęp do biblioteki Aspose.OCR dla .NET (link do pobrania poniżej).  
- Ważna licencja Aspose.OCR do użytku produkcyjnego (dostępna wersja próbna).

## Importowanie przestrzeni nazw

W swoim projekcie .NET upewnij się, że zaimportowałeś niezbędne przestrzenie nazw, aby uzyskać dostęp do funkcjonalności udostępnianej przez Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Pobierz i zainstaluj Aspose.OCR dla .NET

Pobierz najnowszy pakiet ze strony wydania **[tutaj](https://releases.aspose.com/ocr/net/)** i postępuj zgodnie ze standardowymi krokami instalacji przez NuGet lub ręcznie.

## Uzyskaj licencję

Uzyskaj licencję ze **[strony zakupu](https://purchase.aspose.com/buy)** lub wypróbuj **[darmową wersję próbną](https://releases.aspose.com/)**. Umieść plik licencji w katalogu głównym projektu i załaduj go w czasie wykonywania, zgodnie z opisem w dokumentacji Aspose.

## Krok 1: Skonfiguruj katalog dokumentów

Rozpocznij od zainicjowania ścieżki do katalogu dokumentów:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Wskazówka:** Użyj `Path.Combine` do obsługi ścieżek wieloplatformowych.

## Krok 2: Zainicjalizuj Aspose.OCR

Utwórz instancję klasy Aspose.OCR, aby rozpocząć operacje OCR:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Krok 3: Określ ścieżkę do obrazu

Zdefiniuj pełną ścieżkę do obrazu archiwum (plik ZIP zawierający obrazy, które chcesz odczytać):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Krok 4: Rozpoznaj obraz

Wykonaj rozpoznawanie OCR na określonym archiwum, używając ustawień domyślnych lub niestandardowych. To wywołanie automatycznie wyodrębnia każdy obraz z pliku ZIP i uruchamia na nim OCR:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Możesz dostosować `RecognitionSettings`, aby poprawić dokładność dla konkretnych języków lub jakości obrazu.

## Krok 5: Wyświetl wyniki

Iteruj po wynikach i wypisz rozpoznany tekst dla każdego obrazu w archiwum:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Wyjście pokazuje indeks każdego obrazu, po którym następuje wyodrębniony ciąg znaków, skutecznie **konwertując obrazy na tekst** i **wyodrębniając tekst z plików archiwum**.

## Typowe problemy i rozwiązywanie

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| Brak zwróconego tekstu | Jakość obrazu zbyt niska | Wstępnie przetwórz obrazy (np. binaryzacja) lub dostosuj `RecognitionSettings.Dpi` |
| Wyjątek podczas odczytu ZIP | Nieprawidłowa ścieżka archiwum | Sprawdź, czy `fullPath` wskazuje na prawidłowy plik `.zip` oraz czy aplikacja ma uprawnienia do odczytu |
| Licencja nie została zastosowana | Brak pliku licencji lub nie został załadowany | Wywołaj `License license = new License(); license.SetLicense("Aspose.OCR.lic");` przed utworzeniem instancji `AsposeOcr` |

## Najczęściej zadawane pytania

**Q: Czy mogę używać Aspose.OCR dla .NET bez licencji?**  
A: Tak, dostępna jest darmowa wersja próbna do oceny, ale wersja licencjonowana jest wymagana w środowiskach produkcyjnych.

**Q: Czy biblioteka obsługuje archiwa ZIP chronione hasłem?**  
A: Obecnie `RecognizeMultipleImages` działa z standardowymi plikami ZIP. W przypadku zaszyfrowanych archiwów najpierw wyodrębnij obrazy przy użyciu biblioteki zewnętrznej, a następnie przekaż tablicę obrazów do silnika OCR.

**Q: Jak mogę poprawić dokładność rozpoznawania odręcznego tekstu?**  
A: Włącz flagę `RecognitionSettings.EnableHandwritingRecognition` i ustaw wyższą wartość DPI (np. 300).

**Q: Czy istnieje sposób na uzyskanie wskaźników pewności dla każdej rozpoznanej linii?**  
A: Każdy `RecognitionResult` zawiera właściwość `Confidence`, którą możesz logować lub używać do filtrowania wyników o niskiej pewności.

## Zakończenie

Masz teraz kompletny, gotowy do produkcji przepływ pracy, aby **wykonywać OCR na obrazach w archiwum**, **konwertować obrazy na tekst** i **wyodrębniać tekst z plików archiwum** przy użyciu Aspose.OCR dla .NET. Zintegruj to w swoich aplikacjach, aby umożliwić przeszukiwalne repozytoria dokumentów, automatyczne wprowadzanie danych lub dowolny scenariusz wymagający masowego wyodrębniania tekstu z obrazów.

## Dodatkowe zasoby

- **Aspose.OCR Forum:** Wsparcie społeczności i zaawansowane scenariusze, odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).  
- **Temporary License:** Jeśli potrzebujesz krótkoterminowej oceny, zamów [tymczasową licencję](https://purchase.aspose.com/temporary-license/).  
- **Official Documentation:** Bądź na bieżąco z najnowszymi zmianami API, przeglądając [dokumentację](https://reference.aspose.com/ocr/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ostatnia aktualizacja:** 2025-12-19  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose