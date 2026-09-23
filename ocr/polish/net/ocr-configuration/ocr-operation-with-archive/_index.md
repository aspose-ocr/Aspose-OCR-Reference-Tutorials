---
date: 2026-04-12
description: Dowiedz się, jak wyodrębniać tekst z plików zip, wykonując OCR na obrazach
  archiwum przy użyciu Aspose.OCR dla .NET, włączając konfigurację, kod i rozwiązywanie
  problemów.
keywords:
- extract text from zip
- read images from zip
- Aspose OCR .NET
linktitle: Jak wyodrębnić tekst z archiwów ZIP przy użyciu Aspose.OCR dla .NET
second_title: Aspose.OCR .NET API
title: Jak wyodrębnić tekst z archiwów ZIP przy użyciu Aspose.OCR dla .NET
url: /pl/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z archiwów ZIP przy użyciu Aspose.OCR dla .NET

## Wprowadzenie

## Szybkie odpowiedzi
- **Co obejmuje ten tutorial?** Wyodrębnianie tekstu z archiwów ZIP przy użyciu Aspose.OCR dla .NET.  
- **Jakie jest główne słowo kluczowe?** *extract text from zip*.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w celach oceny; licencja komercyjna jest wymagana w produkcji.  
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Czy mogę dostosować ustawienia rozpoznawania?** Tak — użyj `RecognitionSettings`, aby dostroić dokładność dla różnych języków lub jakości obrazu.

## Co to jest OCR i dlaczego używać go w archiwach ZIP?

Rozpoznawanie znaków optycznych (OCR) przekształca zeskanowane obrazy lub pliki PDF w tekst przeszukiwalny i edytowalny. Gdy te obrazy są spakowane w pliku ZIP, wyodrębnianie i rozpoznawanie każdego obrazu w jednym przebiegu oszczędza czas i zmniejsza złożoność kodu. Metoda `RecognizeMultipleImages` Aspose.OCR upraszcza ten proces, umożliwiając **read images from zip** i natychmiastowe uzyskanie treści tekstowej.

## Wymagania wstępne

- Visual Studio 2019 lub nowszy (lub dowolne IDE zgodne z .NET).  
- .NET Framework 4.5 + lub .NET Core 3.1 + zainstalowany.  
- Dostęp do biblioteki Aspose.OCR dla .NET (link do pobrania poniżej).  
- Ważna licencja Aspose.OCR do użytku produkcyjnego (dostępna wersja próbna).

## Importowanie przestrzeni nazw

W swoim projekcie .NET zaimportuj niezbędne przestrzenie nazw, aby uzyskać dostęp do funkcjonalności udostępnianej przez Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Pobierz i zainstaluj Aspose.OCR dla .NET

Pobierz najnowszy pakiet ze strony wydania **[here](https://releases.aspose.com/ocr/net/)** i postępuj zgodnie ze standardowymi krokami instalacji przez NuGet lub ręcznie.

## Uzyskaj licencję

Uzyskaj licencję ze **[purchase page](https://purchase.aspose.com/buy)** lub wypróbuj **[free trial](https://releases.aspose.com/)**. Umieść plik licencji w katalogu głównym projektu i załaduj go w czasie wykonywania, jak opisano w dokumentacji Aspose.

## Krok 1: Skonfiguruj katalog dokumentów

Rozpocznij od zainicjowania ścieżki do katalogu dokumentów. Ten folder będzie zawierał archiwum ZIP, które chcesz przetworzyć:

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

## Krok 3: Określ ścieżkę do archiwum ZIP

Zdefiniuj pełną ścieżkę do obrazu archiwum (plik ZIP zawierający obrazy, które chcesz odczytać):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Krok 4: Rozpoznaj obrazy wewnątrz ZIP

Wykonaj rozpoznawanie OCR na określonym archiwum, używając domyślnych lub niestandardowych ustawień. To wywołanie automatycznie wyodrębnia każdy obraz z ZIP i uruchamia na nim OCR:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Możesz dostosować `RecognitionSettings`, aby poprawić dokładność dla konkretnych języków, DPI lub włączyć rozpoznawanie pisma odręcznego.

## Krok 5: Wydrukuj wyodrębniony tekst

Iteruj po wynikach i wypisz rozpoznany tekst dla każdego obrazu w archiwum. To jest miejsce, w którym faktycznie **extract text from zip**:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Wyjście pokazuje indeks każdego obrazu, po którym następuje wyodrębniony ciąg znaków, skutecznie **converting images to text** i **extracting text from archive** w jednej operacji.

## Dlaczego to podejście ma znaczenie

- **Przetwarzanie wsadowe:** Obsługuje dowolną liczbę obrazów w ZIP bez ręcznego wyodrębniania.  
- **Wydajność:** Zmniejsza obciążenie I/O poprzez bezpośrednie odczytywanie z archiwum.  
- **Skalowalność:** Działa z dużymi plikami ZIP i może być łączone z wzorcami async dla scenariuszy wysokiej przepustowości.  

## Typowe problemy i rozwiązywanie

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|----------|
| Brak zwróconego tekstu | Zbyt niska jakość obrazu | Wstępnie przetwórz obrazy (np. binaryzacja) lub dostosuj `RecognitionSettings.Dpi` |
| Wyjątek podczas odczytu ZIP | Nieprawidłowa ścieżka archiwum | Sprawdź, czy `fullPath` wskazuje na prawidłowy plik `.zip` oraz czy aplikacja ma uprawnienia do odczytu |
| Licencja nie zastosowana | Brak pliku licencji lub nie został załadowany | Wywołaj `License license = new License(); license.SetLicense("Aspose.OCR.lic");` przed utworzeniem instancji `AsposeOcr` |

## Najczęściej zadawane pytania

**Q: Czy mogę używać Aspose.OCR dla .NET bez licencji?**  
A: Tak, dostępna jest darmowa wersja próbna do oceny, ale wersja licencjonowana jest wymagana w środowiskach produkcyjnych.

**Q: Czy biblioteka obsługuje archiwa ZIP chronione hasłem?**  
A: Obecnie `RecognizeMultipleImages` działa z standardowymi plikami ZIP. W przypadku zaszyfrowanych archiwów najpierw wyodrębnij obrazy przy użyciu biblioteki zewnętrznej, a następnie przekaż tablicę obrazów do silnika OCR.

**Q: Jak mogę poprawić dokładność rozpoznawania tekstu odręcznego?**  
A: Włącz flagę `RecognitionSettings.EnableHandwritingRecognition` i ustaw wyższą wartość DPI (np. 300).

**Q: Czy istnieje sposób na uzyskanie współczynników pewności dla każdej rozpoznanej linii?**  
A: Każdy `RecognitionResult` zawiera właściwość `Confidence`, którą możesz logować lub używać do filtrowania wyników o niskiej pewności.

## Dodatkowe zasoby

- **Forum Aspose.OCR:** W celu uzyskania wsparcia społeczności i zaawansowanych scenariuszy, odwiedź [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).  
- **Licencja tymczasowa:** Jeśli potrzebujesz krótkoterminowej oceny, poproś o [temporary license](https://purchase.aspose.com/temporary-license/).  
- **Oficjalna dokumentacja:** Bądź na bieżąco z najnowszymi zmianami API, przeglądając [documentation](https://reference.aspose.com/ocr/net/).

---

**Ostatnia aktualizacja:** 2026-04-12  
**Testowano z:** Aspose.OCR 24.11 dla .NET  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}