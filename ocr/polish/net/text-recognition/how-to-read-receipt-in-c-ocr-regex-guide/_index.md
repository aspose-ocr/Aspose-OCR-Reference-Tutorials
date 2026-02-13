---
category: general
date: 2026-02-13
description: Jak szybko odczytać paragon za pomocą Aspose OCR i wyodrębnić kwotę przy
  użyciu wyrażeń regularnych. Dowiedz się, jak krok po kroku przetwarzać paragon przy
  użyciu OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: pl
og_description: Jak odczytać paragon w C# przy użyciu Aspose OCR i wyrażeń regularnych.
  Ten przewodnik pokazuje, jak przetworzyć paragon za pomocą OCR i wyodrębnić łączną
  kwotę.
og_title: Jak odczytać paragon w C# – Kompletny samouczek OCR i wyrażeń regularnych
tags:
- OCR
- C#
- Regex
- Aspose
title: Jak odczytać paragon w C# – przewodnik OCR + Regex
url: /pl/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odczytać paragon w C# – przewodnik OCR + Regex

Zastanawiałeś się kiedyś **jak odczytać paragon** ze zdjęcia bez ręcznego przepisywania każdej linii? W wielu aplikacjach dla małych firm trzeba wyciągnąć kwotę całkowitą z fotografii paragonu, a robienie tego ręcznie podważa sens automatyzacji. Dobra wiadomość? Z Aspose OCR możesz pozwolić silnikowi wykonać ciężką pracę, a prosty wyrażenie regularne znajdzie sumę. W tym samouczku przeprowadzimy **process receipt with OCR**, wyodrębnimy kwotę przy użyciu regex i uzyskamy gotową do użycia wartość całkowitą.

Zobaczysz kompletny, działający przykład, dowiesz się, dlaczego model językowy dla paragonów ma znaczenie, oraz otrzymasz wskazówki, jak radzić sobie z przypadkami brzegowymi, takimi jak różne symbole walut czy brak etykiety „Total”. Nie są potrzebne żadne zewnętrzne dokumenty — wszystko, czego potrzebujesz, znajduje się tutaj.

## Czego się nauczysz

- Jak skonfigurować Aspose OCR do rozpoznawania specyficznego dla paragonów (model językowy `Receipt` automatycznie prostuje i odszumia obraz).  
- Jak zastosować wyrażenie regularne, które **extract amount using regex** działa dla większości paragonów w stylu amerykańskim.  
- Jak radzić sobie ze wspólnymi wariantami, takimi jak „TOTAL”, „Total:” lub „Grand Total – $12.34”.  
- Jak bezpiecznie wypisać wynik i co zrobić, gdy wzorzec nie zostanie znaleziony.  

**Prerequisites**: .NET 6+ (lub .NET Framework 4.7+), ważna licencja Aspose OCR lub wersja trial oraz obraz paragonu zapisany lokalnie. To wszystko — nie potrzebujesz dodatkowych pakietów NuGet poza Aspose.OCR.

---

## Krok 1 – Zainstaluj Aspose OCR i przygotuj projekt

### Dlaczego to ważne

Aspose OCR udostępnia dedykowany model **process receipt with OCR**, który potrafi wyprostować pognieciony papier i zignorować szumy tła. Użycie ogólnego modelu tekstowego spowodowałoby więcej błędów, szczególnie przy niskiej rozdzielczości skanów.

### Kod

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tip:** Trzymaj plik licencji poza folderem kontrolowanym przez system kontroli wersji, aby uniknąć przypadkowego zatwierdzenia.

---

## Krok 2 – Skonfiguruj silnik OCR dla rozpoznawania paragonów

### Dlaczego to ważne

Model językowy `Receipt` zawiera wbudowane prostowanie i odszumianie, co znacząco zwiększa dokładność w rzeczywistych przypadkach, gdy paragony są złożone lub pogniecione.

### Kod

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Krok 3 – Rozpoznaj tekst z obrazu paragonu

### Dlaczego to ważne

Musisz najpierw uzyskać surowy tekst, zanim zastosujesz jakikolwiek regex. Metoda `RecognizeImage` zwraca obiekt `OcrResult` zawierający pełny ciąg znaków, wyniki pewności i inne dane, które mogą się przydać później.

### Kod

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Przykładowy wynik OCR (przykład)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Krok 4 – Zbuduj regex do **Extract Amount Using Regex**

### Dlaczego to ważne

Paragony występują w wielu formatach, ale słowo „Total” (lub jego bliska odmiana) po którym następuje kwota w dolarach jest niezawodnym kotwicą. Poniższy wzorzec toleruje opcjonalne spacje, dwukropki, myślniki oraz opcjonalny znak `$`.

### Kod

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Wyjaśnienie wzorca**

| Część | Znaczenie |
|------|-----------|
| `Total` | Szuka słowa „Total” (bez uwzględniania wielkości liter). |
| `\s*[:\-]?` | Zezwala na dowolną ilość białych znaków, a następnie opcjonalny dwukropek lub myślnik. |
| `\s*\$?` | Opcjonalne białe znaki i opcjonalny znak dolara. |
| `(\d+(\.\d{2})?)` | Przechwytuje jedną lub więcej cyfr, opcjonalnie po nich następuje kropka i dwie cyfry centów. |

---

## Krok 5 – Wypisz wyodrębniony total lub obsłuż brak danych

### Dlaczego to ważne

Nawet najlepszy OCR może pominąć słowo, szczególnie na rozmazanych paragonach. Zapewnienie eleganckiego fallbacku zapobiega awariom i daje możliwość własnej logiki (np. poproszenie użytkownika o potwierdzenie).

### Kod

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Przykładowy output w konsoli**

```
Total: $12.25
```

---

## Pełny działający przykład – wszystkie kroki w jednym pliku

Poniżej znajduje się pojedynczy, samodzielny program, który możesz skopiować i wkleić do projektu konsolowego. Zawiera komentarze, obsługę błędów oraz opcjonalne wczytywanie licencji.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

### Uruchamianie programu

1. Utwórz nowy projekt konsolowy (`dotnet new console -n ReceiptReader`).  
2. Dodaj pakiet NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Zamień `YOUR_DIRECTORY/receipt.jpg` na rzeczywistą ścieżkę do obrazu paragonu.  
4. Zbuduj i uruchom (`dotnet run`).  

Powinieneś zobaczyć dump OCR, a następnie `Total: $xx.xx`, jeśli wszystko się zgadza.

---

## Obsługa przypadków brzegowych i typowych wariantów

### 1. Różne symbole walut

Jeśli pracujesz z euro (€) lub funtami (£), rozszerz wzorzec:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Brak etykiety „Total”

Niektóre paragony pokazują tylko „Grand Total”. Dodaj alternatywę:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Wiele sum (np. „Subtotal” i „Total”)

Jeśli regex dopasuje pierwsze wystąpienie, możesz potrzebować **ostatniego** dopasowania:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Obrazy o niskiej rozdzielczości

- Zwiększ DPI przy skanowaniu (`300 DPI` to optymalny punkt).  
- Przetwórz obraz prostym filtrem redukującym rozmycie przed przekazaniem go do Aspose (poza zakresem tego przewodnika, ale warte rozważenia).

---

## Pro Tips for Real‑World Projects

- **Cache the OCR result** jeśli musisz wyodrębnić kilka pól (podatek, pozycje itp.) – płacisz koszt OCR tylko raz.  
- **Log the raw OCR text** do bazy danych; staje się to cennym śladem audytu w przypadku spornych wydatków.  
- Przy budowie API webowego, **run OCR in a background worker**; może to trwać kilkaset milisekund, co jest w porządku asynchronicznie, ale nie idealne w synchronicznym żądaniu.  
- **Validate the extracted amount** względem reguł biznesowych (np. kwota musi być > 0) przed zapisaniem.

---

## Zakończenie

Omówiliśmy **jak odczytać paragon** w C# przy użyciu Aspose OCR, a następnie **extract amount using regex**, aby niezawodnie znaleźć linię sumy. Korzystając z modelu językowego `Receipt` otrzymujesz prostowany i odszumiany tekst, a zwięzłe wyrażenie regularne radzi sobie z większością niuansów formatowania. Pełny fragment kodu powyżej można wkleić do dowolnego projektu .NET (konsolowego lub serwisowego), a dodatkowe sugestie dotyczące przypadków brzegowych dają solidną bazę do użycia w produkcji.

Gotowy na kolejny krok? Spróbuj rozszerzyć rozwiązanie o pobieranie poszczególnych pozycji, automatyczne obliczanie podatku lub integrację z API do śledzenia wydatków. A jeśli napotkasz paragon, który łamie wzorzec, pamiętaj, że podejście **regex find total** to tylko punkt wyjścia — zawsze możesz dostosować wzorzec do specyfiki swojego regionu.

Powodzenia w kodowaniu i niech przetwarzanie paragonów będzie szybkie, dokładne i w pełni zautomatyzowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}