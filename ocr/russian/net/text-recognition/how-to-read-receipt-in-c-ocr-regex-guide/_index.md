---
category: general
date: 2026-02-13
description: Как быстро считывать чек с помощью Aspose OCR и извлекать сумму с помощью
  регулярных выражений. Узнайте пошаговую обработку чека с помощью OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: ru
og_description: Как считать чек в C# с помощью Aspose OCR и регулярных выражений.
  Это руководство покажет, как обработать чек с помощью OCR и извлечь общую сумму.
og_title: Как считывать чек в C# – Полный учебник по OCR и регулярным выражениям
tags:
- OCR
- C#
- Regex
- Aspose
title: Как считывать чек в C# — руководство по OCR и регулярным выражениям
url: /ru/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как считывать чек в C# – руководство по OCR + Regex

Задумывались ли вы когда‑нибудь **как считывать чек** с изображений без ручного ввода каждой строки? Во многих приложениях для малого бизнеса необходимо извлечь общую сумму из фотографии чека, а делать это вручную противоречит цели автоматизации. Хорошая новость? С Aspose OCR вы можете позволить движку выполнить тяжелую работу, а простое регулярное выражение найдёт общую сумму. В этом руководстве мы пройдём через **process receipt with OCR**, извлечём сумму с помощью regex и получим готовое к использованию значение общей суммы.

Вы увидите полностью готовый к запуску пример, узнаете, почему модель языка receipt имеет значение, и получите советы по обработке граничных случаев, таких как разные символы валют или отсутствие метки «Total». Внешняя документация не требуется — всё, что нужно, находится здесь.

## Что вы узнаете

- Как настроить Aspose OCR для распознавания чеков (модель языка `Receipt` автоматически исправляет наклон и шумы изображения).  
- Как применить регулярное выражение, которое **extract amount using regex** работает для большинства чеков в стиле США.  
- Как обрабатывать распространённые варианты, такие как «TOTAL», «Total:» или «Grand Total – $12.34».  
- Как безопасно вывести результат и что делать, если шаблон не найден.  

**Prerequisites**: .NET 6+ (или .NET Framework 4.7+), действующая лицензия Aspose OCR или пробная версия, и изображение чека, сохранённое локально. Всё — и ничего больше — никаких дополнительных пакетов NuGet, кроме Aspose.OCR.

---

## Шаг 1 – Установить Aspose OCR и подготовить проект

### Почему это важно

Aspose OCR предоставляет специально разработанную модель **process receipt with OCR**, которая умеет выпрямлять смятые листы и игнорировать фоновые шумы. Использование общей текстовой модели даст больше ошибок, особенно на сканах низкого разрешения.

### Code

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

> **Pro tip:** Храните файл лицензии вне папки с исходным кодом, чтобы избежать случайных коммитов.

---

## Шаг 2 – Настроить движок OCR для распознавания чеков

### Почему это важно

Модель языка `Receipt` включает встроенные функции исправления наклона и шумоподавления, что значительно повышает точность на реальных чеках, которые часто сложены или помяты.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Шаг 3 – Распознать текст с изображения чека

### Почему это важно

Сначала нужен «сырой» текст, прежде чем применять любые regex. Метод `RecognizeImage` возвращает `OcrResult`, содержащий полную строку, оценки уверенности и прочее, если понадобится позже.

### Code

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

**Ожидаемый вывод OCR (пример)**  
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

## Шаг 4 – Создать регулярное выражение для **Extract Amount Using Regex**

### Почему это важно

Чеки бывают в разных форматах, но слово «Total» (или близкий к нему вариант), за которым следует сумма в долларах, является надёжным якорем. Нижеуказанный шаблон допускает пробелы, двоеточия, дефисы и необязательный символ `$`.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Объяснение шаблона**

| Часть | Значение |
|------|----------|
| `Total` | Ищет слово «Total» (без учёта регистра). |
| `\s*[:\-]?` | Позволяет любые пробелы, затем необязательное двоеточие или дефис. |
| `\s*\$?` | Необязательные пробелы и необязательный знак доллара. |
| `(\d+(\.\d{2})?)` | Захватывает одну или несколько цифр, опционально с десятичной точкой и двумя знаками после неё. |

---

## Шаг 5 – Вывести найденную сумму или обработать отсутствие данных

### Почему это важно

Даже лучшая OCR может пропустить слово, особенно на размытых чеках. Предоставление «мягкого» fallback‑а предотвращает падения и даёт возможность добавить собственную логику (например, запросить подтверждение у пользователя).

### Code

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

**Пример вывода в консоль**

```
Total: $12.25
```

---

## Полный рабочий пример – все шаги в одном файле

Ниже представлен единый, самодостаточный код, который можно скопировать в консольный проект. В нём есть комментарии, обработка ошибок и опциональная загрузка лицензии.

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

**Запуск программы**

1. Создайте новый консольный проект (`dotnet new console -n ReceiptReader`).  
2. Добавьте пакет Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Замените `YOUR_DIRECTORY/receipt.jpg` на реальный путь к изображению чека.  
4. Скомпилируйте и запустите (`dotnet run`).  

Вы должны увидеть вывод OCR, а затем `Total: $xx.xx`, если всё прошло успешно.

---

## Обработка граничных случаев и распространённых вариантов

### 1. Разные символы валют

Если вы работаете с евро (€) или фунтами (£), расширьте шаблон:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Отсутствует метка «Total»

Некоторые чеки показывают только «Grand Total». Добавьте альтернативу:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Несколько сумм (например, «Subtotal» и «Total»)

Если regex находит первое совпадение, возможно, вам понадобится **последнее** совпадение:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Низкое разрешение изображений

- Увеличьте DPI при сканировании (`300 DPI` — оптимальный вариант).  
- Предобработайте изображение простым фильтром снижения размытия перед передачей в Aspose (вне рамок данного руководства, но стоит изучить).

---

## Советы для реальных проектов

- **Кешируйте результат OCR**, если нужно извлечь несколько полей (налог, позиции и т.д.) — вы платите за OCR только один раз.  
- **Логируйте сырой текст OCR** в базе данных; это ценная аудиторская запись для спорных расходов.  
- При построении веб‑API **выполняйте OCR в фоновом воркере**; он может занимать несколько сотен миллисекунд, что приемлемо асинхронно, но не идеально для синхронного запроса.  
- **Проверяйте извлечённую сумму** согласно бизнес‑правилам (например, сумма должна быть > 0) перед сохранением.

---

## Заключение

Мы рассмотрели, **как считывать чек** в C# с помощью Aspose OCR, а затем **extract amount using regex**, чтобы надёжно находить строку с общей суммой. Используя модель языка `Receipt`, вы получаете выпрямленный и очищенный от шумов текст, а лаконичное регулярное выражение покрывает большинство форматных особенностей. Полный код выше готов к вставке в любой .NET‑консольный или сервисный проект, а дополнительные рекомендации по граничным случаям дают прочную основу для продакшн‑использования.

Готовы к следующему шагу? Попробуйте расширить решение, чтобы извлекать отдельные позиции, автоматически рассчитывать налог или интегрировать с API учёта расходов. И если встретите чек, который ломает шаблон, помните, что подход **regex find total** — лишь отправная точка; вы всегда можете подправить шаблон под свои локальные требования.

Happy coding, and may your receipt‑processing be fast, accurate, and completely automated!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}