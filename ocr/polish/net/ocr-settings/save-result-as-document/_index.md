---
date: 2025-12-27
description: Dowiedz się, jak używać Aspose.OCR dla .NET do wyodrębniania tekstu z
  obrazu, rozpoznawania tekstu na obrazach oraz konwertowania obrazu na PDF w .NET
  w różnych formatach dokumentów.
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Konwertuj obraz na PDF w .NET – Zapisz wynik jako dokument w rozpoznawaniu
  obrazu OCR
url: /pl/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj obraz na PDF .NET – Zapisz wynik jako dokument w rozpoznawaniu obrazu OCR

## Wstęp

Witamy w ekscytującym świecie optycznego rozpoznawania znaków (OCR) z Aspose.OCR dla .NET! W tym samouczku dowiesz się, jak **konwertować obraz na PDF .NET**, wyodrębnić tekst z obrazu oraz zapisać wynik OCR w przeszukiwalnych formatach dokumentów, takich jak PDF, DOCX, TXT i Excel. Niezależnie od tego, czy potrzebujesz stworzyć przeszukiwalny PDF, czy wyeksportować wyniki OCR do Excela, poniższe kroki poprowadzą Cię szybko i sprawnie przez cały proces.

## Szybkie odpowiedzi
- **Co oznacza „image to pdf .net”?** Odnosi się do konwersji plików graficznych na dokumenty PDF przy użyciu bibliotek .NET, w tym przypadku Aspose.OCR.  
- **Do jakich formatów mogę eksportować wyniki OCR?** Obsługiwane są natywnie DOCX, TXT, PDF i XLSX.  
- **Czy potrzebna jest licencja do użytku produkcyjnego?** Tak, do użytku produkcyjnego wymagana jest licencja komercyjna; dostępna jest bezpłatna wersja próbna do oceny.  
- **Czy mogę wyodrębnić przeszukiwalny tekst z PDF?** Oczywiście – generowany PDF jest **ocr to searchable pdf**, który można indeksować.  
- **Jakie wersje .NET są obsługiwane?** Aspose.OCR działa z .NET Framework 4.5+, .NET Core 3.1+, oraz .NET 5/6+.  

## Co to jest „image to pdf .net”?
„Image to PDF .NET” to proces przekształcania obrazów rastrowych (PNG, JPEG, TIFF itp.) w pliki PDF przy użyciu biblioteki .NET. Aspose.OCR nie tylko konwertuje obraz, ale także wykonuje OCR, umożliwiając **rozpoznawanie tekstu w obrazach** i osadzenie tego tekstu w powstałym PDF, czyniąc go przeszukiwalnym.

## Dlaczego warto używać Aspose.OCR do tego zadania?
- **Wysoka dokładność** – zaawansowany silnik OCR obsługujący wiele języków i czcionek.  
- **Jednokrokowa konwersja** – możesz jednocześnie rozpoznać tekst i zapisać go bezpośrednio do PDF, DOCX, TXT lub Excel, bez dodatkowego przetwarzania.  
- **Brak zewnętrznych zależności** – czysta biblioteka .NET, nie wymaga natywnych plików binarnych.  
- **Elastyczność** – łatwo zmienić format wyjściowy, tworząc dokument z OCR lub eksportując OCR do Excela w celu analizy danych.

## Wymagania wstępne

Zanim rozpoczniemy przygodę z OCR, upewnij się, że spełniasz następujące wymagania:

- Aspose.OCR for .NET. Upewnij się, że biblioteka Aspose.OCR jest zainstalowana. Możesz ją pobrać [tutaj](https://releases.aspose.com/ocr/net/).

- Katalog dokumentów: Utwórz wyznaczony katalog dla swoich dokumentów i zaktualizuj zmienną `dataDir` w dostarczonym kodzie odpowiednio.

## Importowanie przestrzeni nazw

Rozpocznij od zaimportowania niezbędnych przestrzeni nazw. Są to elementy budulcowe, które nadadzą Twojemu kodowi możliwości OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Teraz rozbijmy przykład na kilka kroków:

## Jak konwertować obraz na PDF .NET przy użyciu Aspose.OCR

### Krok 1: Inicjalizacja Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Ten krok przygotowuje środowisko, inicjalizując API Aspose.OCR.

### Krok 2: Rozpoznanie obrazu

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Tutaj używamy Aspose.OCR do **rozpoznania tekstu w określonym obrazie** (zamień `"sample.png"` na własny plik obrazu). To właśnie miejsce, w którym odbywa się operacja **extract text from image**.

### Krok 3: Zapis wyniku w różnych formatach

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Dostosuj ten krok do własnych potrzeb. Aspose.OCR pozwala **zapisać rozpoznany tekst w różnych formatach dokumentów, takich jak DOCX, TXT, PDF i XLSX**, efektywnie **creating a document from OCR** lub **exporting OCR to Excel**.

### Krok 4: Wyświetlenie komunikatu sukcesu

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Prosty komunikat potwierdzający, że proces zakończył się pomyślnie.

Postępując zgodnie z tymi krokami, skutecznie wykorzystałeś moc Aspose.OCR dla .NET do rozpoznawania tekstu w obrazach i zapisywania wyników w różnych formatach dokumentów, w tym **ocr to searchable pdf**.

## Typowe problemy i rozwiązania
- **Obraz nie jest rozpoznawany** – Upewnij się, że obraz ma wystarczającą rozdzielczość (co najmniej 300 dpi) i jest w obsługiwanym formacie (PNG, JPEG, TIFF).  
- **Nieprawidłowe wykrycie języka** – Przekaż obiekt `RecognitionSettings` z odpowiednio ustawioną właściwością `Language` (np. `Language = Language.English`).  
- **Plik wyjściowy nie został utworzony** – Sprawdź, czy `dataDir` wskazuje na istniejący, zapisywalny folder oraz czy nazwy plików są unikalne.

## Najczęściej zadawane pytania

**Q: Czy Aspose.OCR obsługuje różne formaty obrazów?**  
A: Tak, Aspose.OCR wspiera szeroką gamę formatów graficznych, zapewniając elastyczność w zadaniach OCR.

**Q: Czy mogę dostosować ustawienia rozpoznawania w celu uzyskania lepszej dokładności?**  
A: Oczywiście! Aspose.OCR udostępnia ustawienia rozpoznawania, które pozwalają precyzyjnie dostroić proces OCR do Twoich wymagań.

**Q: Czy dostępna jest bezpłatna wersja próbna?**  
A: Tak, możesz rozpocząć z darmową wersją próbną [tutaj](https://releases.aspose.com/).

**Q: Jak mogę uzyskać tymczasowe licencje dla Aspose.OCR?**  
A: Tymczasowe licencje można uzyskać [tutaj](https://purchase.aspose.com/temporary-license/).

**Q: Gdzie mogę uzyskać pomoc lub połączyć się ze społecznością?**  
A: Dołącz do społeczności Aspose.OCR na [Aspose Forum](https://forum.aspose.com/c/ocr/16), aby uzyskać wsparcie i dyskusje.

## Zakończenie

Podsumowując, Aspose.OCR dla .NET otwiera przed Tobą szerokie możliwości konwersji **image to pdf .net**, wyodrębniania tekstu oraz generowania dokumentów. Niezależnie od tego, czy wyodrębniasz dane, tworzysz przeszukiwalne PDF‑y, czy eksportujesz wyniki OCR do Excela, Aspose.OCR upraszcza cały proces dzięki intuicyjnemu API i bogatemu zestawowi funkcji.

---

**Ostatnia aktualizacja:** 2025-12-27  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}