---
category: general
date: 2026-01-01
description: Мгновенно распознавайте русский текст с помощью Aspose OCR C#. Узнайте,
  как распознавать китайский текст, определять количество страниц PDF и извлекать
  текст со страниц PDF в одном руководстве.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: ru
og_description: Быстро распознавать русский текст с помощью Aspose OCR C#. Этот учебник
  также охватывает, как распознавать китайский текст, читать количество страниц PDF
  и конвертировать текст страниц PDF.
og_title: Распознавание русского текста с помощью Aspose OCR C# – Полное руководство
tags:
- Aspose OCR
- C#
- PDF processing
title: Распознавание русского текста с помощью Aspose OCR C# – полное руководство
  по многостраничному PDF.
url: /ru/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание русского текста с Aspose OCR C# – Полный учебник по многостраничному PDF

Когда‑нибудь вам нужно было **распознать русский текст** в PDF, который содержит несколько языков, и вы задавались вопросом, как сделать это без использования отдельного инструмента для каждой страницы? Вы не одиноки. Во многих реальных проектах вы получаете один PDF, содержащий английский, русский и даже китайский на разных страницах, и при этом хотите получить единый чистый текстовый вывод.

В этом руководстве мы покажем вам, как именно **распознать русский текст** (и другие языки) с помощью **Aspose OCR C#**, а также продемонстрируем, как **прочитать количество страниц PDF**, **распознать китайский текст** и **преобразовать текст страниц PDF** в удобный вывод в консоль. Никаких внешних сервисов, никаких скрытых шагов — только чистый C# код, который вы можете скопировать и запустить.

> **Что вы получите**  
> * Работоспособное C# консольное приложение, обрабатывающее многостраничный PDF.  
> * Выбор языка для каждой страницы (Russian, Chinese, English).  
> * Техники запроса количества страниц PDF и извлечения текста каждой страницы.  
> * Советы, подводные камни и расширения, которые вы можете применить в своих проектах.

---

## Prerequisites

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
- Пакет NuGet **Aspose.OCR for .NET**, установленный (`dotnet add package Aspose.OCR`).  
- PDF‑файл, содержащий несколько языков; для демонстрации будем использовать `mixed_lang.pdf`.  
- Базовое знакомство с консольными приложениями C#.

Если у вас отсутствует что‑то из перечисленного, скачайте последнюю версию Aspose OCR из NuGet и разместите ваш PDF в доступном для проекта месте.

---

## Step 1 – Initialize the Aspose OCR Engine

Первое, что вам нужно, — это экземпляр `OcrEngine`. Этот объект хранит все настройки (например, язык) и выполняет основную работу.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **Почему это важно:**  
> Движок переиспользуемый, поэтому мы не тратим память, создавая новый экземпляр для каждой страницы. Повторное использование также позволяет менять язык «на лету», что необходимо для **распознавания русского текста** на одной странице и **распознавания китайского текста** на другой.

---

## Step 2 – Load the PDF and Find Out How Many Pages It Has

Прежде чем начать распознавание, нам нужен объект PDF и количество его страниц. Aspose OCR рассматривает каждую страницу как `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **Подсказка:** Если PDF огромный, возможно, стоит сначала прочитать количество страниц и решить, обрабатывать все страницы или только их часть.

---

## Step 3 – Map Each Page to Its Desired Language

Aspose OCR поддерживает множество языков, но вы должны указать, какой использовать для каждой страницы. Ниже мы создаём `Dictionary<int, OcrLanguage>`, где ключ — нулевой индекс страницы.

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **Почему это критично:**  
> Без этой карты OCR‑движок будет пытаться использовать один язык по умолчанию для всех страниц, что приводит к искажённому выводу для русского или китайского текста. Этот шаг напрямую позволяет правильно **распознавать русский текст** и **распознавать китайский текст**.

---

## Step 4 – Loop Through All Pages, Set Language, and Recognize Text

Теперь мы проходим по каждой странице, переключаем язык в соответствии с нашей картой и вызываем `Recognize`. Результат сохраняется в `OcrResult`, из которого мы извлекаем простой текст.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### Expected Console Output

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **Объяснение процесса:**  
> * Цикл учитывает **прочитанное количество страниц PDF**, которое мы вывели ранее.  
> * Меняя `ocrEngine.Settings.Language` на каждой итерации, мы гарантируем точное **распознавание русского текста** на странице 2 и **распознавание китайского текста** на странице 3.  
> * Выражения `Console.WriteLine` эффективно **преобразуют текст страниц PDF** в читаемую строку.

---

## Step 5 – Run, Verify, and Tweak

1. Сборка проекта (`dotnet build`).  
2. Запуск (`dotnet run`).  
3. Сравнение вывода консоли с оригинальным PDF.

Если вы заметили пропущенные символы, рассмотрите:

- **Повышение точности OCR** путем установки `ocrEngine.Settings.DetectTextOrientation = true;`.  
- **Предоставление пользовательского языкового пакета**, если встроенные словари русского или китайского устарели.  
- **Настройку DPI** при загрузке PDF (`OcrImage.FromFile(path, 300)`), что может улучшить распознавание при сканах низкого разрешения.

---

## Bonus: Handling Edge Cases

### What if a page’s language isn’t in the map?

Код уже переходит к английскому, но вы также можете добавить резервный вариант, который будет записывать предупреждение:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### Can we process PDFs with more than three languages?

Конечно. Расширьте `languageMap`, добавив дополнительные индексы и поддерживаемые значения `OcrLanguage` (например, `OcrLanguage.French`). Цикл обработает любое количество страниц.

### How to export the results to a file instead of the console?

Замените вызовы `Console.WriteLine` на `File.AppendAllText("output.txt", …)` или используйте `StringBuilder`, который вы запишете один раз после цикла.

---

## Image Illustration

![recognize russian text example](/images/recognize-russian-text.png "Screenshot showing OCR output for Russian text")

*Изображение выше демонстрирует вывод консоли при выполнении **распознавания русского текста** на PDF с несколькими языками.*

---

## Conclusion

Мы прошли полный пример от начала до конца, показывающий, как **распознать русский текст** (а также **распознать китайский текст**) из многостраничного PDF с помощью **Aspose OCR C#**. Считая количество страниц PDF, сопоставляя каждую страницу с нужным языком и проходя по документу, вы можете **преобразовать текст страниц PDF** в обычные строки, готовые для хранения, индексации или дальнейшего анализа.

In short:

- **Инициализировать** один `OcrEngine`.  
- **Загрузить** PDF и **прочитать количество страниц PDF**.  
- **Сопоставить** страницы с языками (Russian, Chinese и т.д.).  
- **Итерировать**, установить `ocrEngine.Settings.Language` и **распознать** каждую страницу.  
- **Вывести** или сохранить извлечённый текст.

Не стесняйтесь адаптировать этот шаблон для больших документов, добавить обработку ошибок или подключить результаты к поисковому индексу. Основная идея — выбор языка для каждой страницы — остаётся той же, и именно она делает возможным надёжное **распознавание русского текста** в PDF с несколькими языками.

Есть другой сценарий, например сканирование изображений вместо PDF? Тот же движок работает; просто замените `OcrImage.FromFile` на `OcrImage.FromStream` или `FromBitmap`. Приятного кодинга, и пусть ваш OCR всегда будет точным!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}