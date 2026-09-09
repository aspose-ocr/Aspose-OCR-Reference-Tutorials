---
category: general
date: 2026-01-04
description: Узнайте, как включить формы и извлекать таблицы из изображений с помощью
  OCR в C#. Этот пошаговый учебник также показывает, как запускать OCR‑изображения
  и обнаруживать таблицы с помощью OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: ru
og_description: Пошаговое руководство по включению форм, извлечению таблиц, запуску
  OCR изображений и обнаружению таблиц OCR с использованием C#.
og_title: Как включить формы и извлекать таблицы с помощью OCR в C#
tags:
- OCR
- C#
- Computer Vision
title: Как включить формы и извлекать таблицы с помощью OCR в C# – Полное руководство
url: /ru/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить распознавание форм и извлекать таблицы с помощью OCR в C# – Полное руководство

Когда‑нибудь задавались вопросом **как включить формы** при сканировании счетов, чеков или любого структурированного документа? Вы не одиноки. Во многих реальных проектах основной проблемой является то, как заставить OCR понимать как поля формы **так и** таблицы без миллионов строк собственного парсинга.  

В этом руководстве мы пройдем практическое решение от начала до конца, показывающее **как включить формы**, **как извлекать таблицы**, а также **как выполнять обработку изображений OCR** в одной программе на C#. К концу вы получите готовый фрагмент кода, который обнаруживает таблицы в стиле OCR, извлекает пары «ключ‑значение» и выводит их в консоль.

> **Prerequisites** – .NET 6+ (или .NET Framework 4.7+), ссылка на используемый OCR SDK (в примере предполагается общий класс `OcrEngine`), и файл изображения (`invoice_table.png`), содержащий таблицу или форму. Других внешних библиотек не требуется.

![как включить формы с OCR C#](image.png)

## Что покрывает это руководство

- **Включить распознавание форм**, чтобы такие поля, как «Invoice Number» или «Date», автоматически определялись.  
- **Извлекать таблицы** из отсканированных документов, получая количество строк/столбцов и содержимое ячеек.  
- **Выполнять обработку изображения OCR** одним вызовом и программно обрабатывать результат.  
- Советы по **detect tables OCR** в сложных случаях, таких как объединённые ячейки или отсутствие границ.  

Приступим.

## Шаг 1: Настройка OCR‑движка – как включить формы

Прежде чем может начаться распознавание, нужен экземпляр OCR‑движка. Большинство SDK предоставляют простой конструктор; мы также укажем, где позже можно изменить параметры конфигурации.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Почему это важно:** Создание экземпляра двигателя выделяет внутренние ресурсы (например, языковые модели). Если пропустить этот шаг, последующий вызов `Recognize` бросит `NullReferenceException`.

## Шаг 2: Включить структурированное извлечение – как извлекать таблицы & detect tables OCR

Теперь включаем две основные функции: распознавание таблиц и извлечение полей формы. Современные OCR‑движки обычно предоставляют булевые флаги или более детальный объект `Config`.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Pro tip:** Если нужна только одна из функций, отключение другой может повысить производительность до 20 %.

## Шаг 3: Выполнить OCR‑изображение и получить результат – run OCR image

После настройки двигателя один метод делает всю тяжёлую работу. Возвращаемый `OcrResult` содержит коллекции таблиц и полей формы.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Ожидаемый вывод в консоль

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

Точные цифры будут отличаться в зависимости от вашего исходного изображения, но вы должны увидеть строку‑резюме для каждой таблицы, затем значения ячеек первой строки и список пар «ключ‑значение» для полей формы.

## Шаг 4: Обработка граничных случаев при detect tables OCR

Даже при `EnableTableRecognition = true` OCR может столкнуться с:

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Merged cells** | The engine treats the merged area as a single cell. | Post‑process rows: look for unusually wide cells and split them based on whitespace. |
| **Missing borders** | Table lines are faint or broken. | Increase image contrast before feeding it to the engine (`ocrEngine.PreprocessImage`). |
| **Rotated tables** | Document scanned at an angle. | Use `ocrEngine.Config.AutoRotate = true` (if available). |

**Tip:** Always validate `table.Rows.Count` and `table.Columns.Count` before accessing indices to avoid `IndexOutOfRangeException`.

## Шаг 5: Собираем всё вместе – полный, готовый к запуску пример

Ниже представлен полный код программы, который можно скопировать в новый консольный проект. Он включает директивы `using`, настройку двигателя и логику обработки, показанную ранее.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Запустите программу (`dotnet run` или `Ctrl+F5` в Visual Studio) — вы увидите описанный выше вывод в консоль.

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это с PDF‑входом?**  
A: Большинство OCR SDK принимают PDF, внутренне растеризуя каждую страницу. Достаточно вызвать `ocrEngine.LoadPdf("file.pdf")` вместо `LoadImage`.

**Q: Что если моё изображение содержит одновременно таблицу *и* подпись?**  
A: Подпись появится как отдельный регион изображения. Её можно игнорировать, проверяя `ocrResult.Images` на низкую уверенность текста.

**Q: Могу ли я экспортировать таблицы в CSV?**  
A: Конечно. После перебора `table.Rows` запишите каждый `cell.Text` в `StringBuilder`, разделяя запятыми, а затем сохраните строку в файл с расширением `.csv`.

## Заключение

Теперь вы знаете **как включить формы**, **как извлекать таблицы** и точные шаги для **run OCR image** обработки с помощью C#. Пример демонстрирует полный рабочий процесс — от создания двигателя, через конфигурацию, до обработки результата — чтобы вы могли сразу скопировать его в свои проекты.  

Далее попробуйте заменить примерное изображение на многостраничный PDF‑счёт, поэкспериментировать с `ocrEngine.Config.AutoRotate` или передать извлечённые данные в базу данных. Эти расширения углубят ваше владение **detect tables OCR** и **use OCR C#** в продакшн‑сценариях.

Если возникнут трудности, оставляйте комментарии ниже. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}