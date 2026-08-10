---
category: general
date: 2026-05-06
description: Узнайте, как выполнять OCR на PDF‑файлах с помощью Aspose OCR в C#. Этот
  учебник также показывает, как извлекать текст из PDF и загружать PDF для OCR.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: ru
og_description: Узнайте, как выполнять OCR в PDF с помощью Aspose OCR на C#. Пошаговый
  код, объяснения и советы по эффективному извлечению текста из PDF.
og_title: Выполнить OCR в PDF с помощью Aspose OCR – Полное руководство
tags:
- Aspose OCR
- C#
- PDF processing
title: Выполните OCR в PDF с помощью Aspose OCR — Полное руководство
url: /ru/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR в PDF с Aspose OCR – Полное руководство

Когда‑нибудь вам нужно было **выполнить OCR в PDF** файлах, но вы не знали, с чего начать? Вы не одиноки. Во многих реальных проектах — например, автоматическая обработка счетов или оцифровка архивных отчетов — возможность извлекать текст из отсканированного PDF является обязательной.  

В этом руководстве мы пошагово рассмотрим практическое решение, которое не только **выполняет OCR в PDF** с использованием библиотеки Aspose OCR, но и показывает, как **извлекать текст из PDF**, **загружать PDF для OCR** и даже работать с многоязычными документами. К концу вы получите готовую к запуску программу на C#, которая преобразует любой отсканированный PDF в поисковый, редактируемый текст.

## Что вы узнаете

- Как настроить Aspose OCR в .NET‑проекте.  
- Точные шаги для **загрузки PDF для OCR** и передачи его в движок.  
- Как сопоставлять разные языки отдельным страницам — полезно, когда PDF содержит английский, французский и немецкий.  
- Способы проверки результата и устранения распространённых проблем.  

> **Pro tip:** Если вы работаете с большими PDF, рассмотрите возможность параллельной обработки страниц, чтобы сократить время выполнения на несколько минут. Мы коснёмся этого позже.

## Требования

- .NET 6.0 или новее (код работает также с .NET Core и .NET Framework).  
- Действующая лицензия Aspose OCR или временный оценочный ключ.  
- Отсканированный PDF с именем `multilang.pdf`, размещённый в папке, к которой ваш код может получить доступ.  

Никакие другие сторонние пакеты не требуются.

---

## Шаг 1 – Установить Aspose OCR и создать движок

Сначала добавьте пакет Aspose.OCR из NuGet в ваш проект:

```bash
dotnet add package Aspose.OCR
```

После установки пакета вы можете создать экземпляр OCR‑движка. Этот объект — сердце операции; он умеет читать изображения, PDF и преобразовывать их в текст.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Почему это важно:** Инициализация движка один раз и повторное его использование на разных страницах уменьшает нагрузку на память и ускоряет обработку.

---

## Шаг 2 – Загрузить PDF‑документ для OCR

Движок может открывать PDF напрямую, но вы должны указать, какой файл обрабатывать. Это шаг **загрузки PDF для OCR**, который многие разработчики упускают из виду.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

Замените `YOUR_DIRECTORY` фактическим путём на вашем компьютере. Если файл встроен как ресурс, его также можно загрузить из потока.

> **Edge case:** Если PDF защищён паролем, вызовите `ocrEngine.LoadPdf(path, password)`, чтобы передать пароль расшифровки.

---

## Шаг 3 – Сопоставить языки страницам (необязательно, но мощно)

Часто отсканированный PDF содержит страницы на разных языках. По умолчанию Aspose OCR предполагает английский, что приводит к плохим результатам на французских или немецких страницах. Мы создадим простой словарь, который укажет движку, какой язык использовать для каждой страницы.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Почему это делается:** Указание правильного языка существенно повышает точность, особенно для символов с диакритическими знаками и специфической пунктуации.

---

## Шаг 4 – Запустить OCR и получить результат

Теперь происходит основная работа. Вызов `Recognize()` обрабатывает *все* страницы согласно заданной карте языков.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

Объект `recognitionResult` содержит свойство `Text`, которое агрегирует распознанный текст со всех страниц.

---

## Шаг 5 – Вывести извлечённый текст

Наконец, мы просто выводим объединённый текст в консоль — либо можете записать его в файл, базу данных или любую другую систему.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

Если предпочитаете файл:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Verification tip:** Откройте полученный `extracted_text.txt` и найдите известные слова каждого языка. Если французские акценты отображаются некорректно, проверьте карту языков.

---

## Полный рабочий пример

Собрав все части вместе, получаем полностью готовую к запуску программу. Скопируйте её в новый консольный проект и нажмите **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**Ожидаемый вывод** (усечённый для краткости):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## Обработка больших PDF и оптимизация производительности

Если ваш PDF содержит сотни страниц, рассмотрите следующие настройки:

1. **Chunked processing** – Обрабатывать по 50 страниц за раз, затем записывать промежуточные результаты на диск.  
2. **Parallelism** – Использовать `Parallel.ForEach` с отдельными экземплярами `OcrEngine` (каждый движок потокобезопасен после инициализации).  
3. **Memory management** – Вызывать `ocrEngine.Dispose()` после каждой части, чтобы освободить нативные ресурсы.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## Распространённые проблемы и их решения

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Искажённые символы на французских страницах | Указан неверный язык | Убедитесь, что `PageLanguageProvider` возвращает `OcrLanguage.French` для этих страниц. |
| Пустой файл вывода | PDF не загружен (неправильный путь) | Проверьте путь и убедитесь, что файл не заблокирован другим процессом. |
| Исключение Out‑of‑memory при огромных PDF | Движок загружает весь PDF сразу | Используйте перегрузку `LoadPdf` для одной страницы или обрабатывайте документ частями. |
| Медленная обработка (> 5 минут для 100 страниц) | Однопоточная работа | Включите параллельную обработку, как показано выше. |

---

## Следующие шаги – выход за пределы базового OCR

Теперь, когда вы умеете **выполнять OCR в PDF** и **извлекать текст из PDF**, вы можете:

- **Создание поискового PDF** – Использовать Aspose.PDF для внедрения OCR‑текста обратно в оригинальный PDF, делая его поисковым.  
- **Извлечение данных** – Применять регулярные выражения для получения номеров счетов, дат или сумм из извлечённого текста.  
- **Интеграция с ИИ** – Передавать результат OCR в языковую модель (например, Azure OpenAI) для суммирования или классификации.  

Все эти расширения по‑прежнему опираются на базовую возможность **загрузки PDF для OCR**, так что фундамент уже готов.

---

## Заключение

Мы рассмотрели всё, что необходимо для **выполнения OCR в PDF** файлов с помощью Aspose OCR на C#. От установки библиотеки, загрузки PDF, назначения языков по страницам, запуска движка распознавания до окончательного **извлечения текста из PDF** и его сохранения — руководство предоставляет автономное, готовое к продакшн решениe.  

Экспериментируйте с параллельной обработкой, различными комбинациями языков или комбинируйте OCR‑текст с другими библиотеками обработки документов. Если возникнут сложности, обратитесь к таблице устранения проблем выше или оставьте комментарий — удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}