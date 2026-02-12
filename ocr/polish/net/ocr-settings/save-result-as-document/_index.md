---
description: Dowiedz się, jak zapisywać wyniki OCR przy użyciu Aspose.OCR dla .NET
  – konwertuj obraz na PDF, wyodrębniaj tekst z PNG i zapisuj rozpoznany tekst w formatach
  DOCX, TXT, PDF lub XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Jak zapisać wynik OCR jako dokument
url: /pl/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać wynik OCR jako dokument

## Wprowadzenie

W tym samouczku dowiesz się **jak zapisać wynik OCR** przy użyciu Aspose.OCR dla .NET. Przejdziemy przez rozpoznawanie tekstu na obrazie, a następnie konwersję tego tekstu do popularnych formatów dokumentów, takich jak DOCX, TXT, PDF i XLSX. Po zakończeniu będziesz mógł automatyzować wyodrębnianie danych ze zdjęć i przechowywać je jako przeszukiwalne, edytowalne pliki — idealne do archiwizacji, raportowania lub dalszego przetwarzania.

## Szybkie odpowiedzi
- **Co oznacza „how to save ocr”?** Odwołuje się do utrwalenia tekstu rozpoznanego z obrazu w formacie pliku, takim jak DOCX, PDF itp.  
- **Do jakich formatów mogę eksportować?** DOCX, TXT, PDF i XLSX są obsługiwane od razu.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do oceny; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Czy mogę bezpośrednio konwertować obraz do PDF?** Tak — zapisz wynik OCR jako PDF, aby uzyskać przeszukiwalny dokument PDF.  
- **Czy PNG jest obsługiwany?** Oczywiście; możesz **wyodrębnić tekst z obrazów PNG** przy użyciu tego samego API.

## Co to jest OCR i dlaczego warto zapisywać wyniki jako dokumenty?

Optical Character Recognition (OCR) przekształca drukowany lub odręczny tekst znajdujący się na obrazach w ciągi znaków odczytywalne przez maszynę. Zapisanie tych ciągów jako dokumentów pozwala na:

* Tworzenie przeszukiwalnych PDF‑ów dla zgodności.  
* Wypełnianie arkuszy kalkulacyjnych (XLSX) w celu analizy danych.  
* Generowanie edytowalnych raportów (DOCX).  
* Archiwizowanie czystych logów tekstowych (TXT) dla szybkiego wyszukiwania.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- Aspose.OCR dla .NET zainstalowany. Możesz go pobrać **[tutaj](https://releases.aspose.com/ocr/net/)**.  
- Folder na komputerze, w którym będą przechowywane obrazy źródłowe i dokumenty wyjściowe. Zaktualizuj zmienną `dataDir` w kodzie, aby wskazywała na ten folder.

## Importowanie przestrzeni nazw

Potrzebujemy kilku przestrzeni nazw .NET, aby uzyskać dostęp do operacji I/O oraz klas Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Krok 1: Inicjalizacja Aspose.OCR

Ustaw ścieżkę do swojego katalogu roboczego i utwórz instancję silnika OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Krok 2: Rozpoznanie obrazu

Przekaż plik obrazu (np. PNG) do rozpoznawacza. To tutaj **rozpoznajemy obrazy tekstowe** i zamieniamy je na obiekt `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Krok 3: Zapis wyniku w różnych formatach

Teraz eksportujemy rozpoznany tekst. Wybierz format pasujący do Twojego przepływu pracy — niezależnie od tego, czy potrzebujesz **konwertować obraz do PDF**, **wyodrębnić tekst z PNG**, czy wygenerować arkusz kalkulacyjny.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Krok 4: Wyświetlenie komunikatu o sukcesie

Prosty komunikat w konsoli potwierdza, że proces zakończył się bez błędów.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Typowe pułapki i wskazówki

- **Ścieżki plików:** Zawsze używaj ścieżek bezwzględnych lub upewnij się, że `dataDir` kończy się separatorem ścieżki (`\` lub `/`).  
- **Jakość obrazu:** Obrazy o wyższej rozdzielczości zwiększają dokładność; rozważ wstępne przetwarzanie (prostowanie, odszumianie) dla lepszych rezultatów.  
- **Tryb licencji:** W trybie ewaluacyjnym wynik może zawierać znak wodny; zastosuj ważną licencję, aby go usunąć.

## Najczęściej zadawane pytania

**P1. Czy Aspose.OCR jest kompatybilny z różnymi formatami obrazów?**  
Odp.: Tak, Aspose.OCR obsługuje szeroką gamę formatów obrazów, zapewniając elastyczność w zadaniach OCR.

**P2: Czy mogę dostosować ustawienia rozpoznawania w celu uzyskania lepszej dokładności?**  
Odp.: Oczywiście! Aspose.OCR udostępnia `RecognitionSettings`, które pozwalają precyzyjnie dostroić proces OCR do Twoich wymagań.

**P3: Czy dostępna jest darmowa wersja próbna?**  
Odp.: Tak, możesz rozpocząć od darmowej wersji próbnej **[tutaj](https://releases.aspose.com/)**.

**P4: Jak mogę uzyskać tymczasową licencję dla Aspose.OCR?**  
Odp.: Tymczasowe licencje można uzyskać **[tutaj](https://purchase.aspose.com/temporary-license/)**.

**P5: Gdzie mogę uzyskać pomoc lub połączyć się ze społecznością?**  
Odp.: Dołącz do społeczności Aspose.OCR na **[Aspose Forum](https://forum.aspose.com/c/ocr/16)**, aby uzyskać wsparcie i dyskusje.

---

**Ostatnia aktualizacja:** 2026-02-12  
**Testowano z:** Aspose.OCR 24.11 dla .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}