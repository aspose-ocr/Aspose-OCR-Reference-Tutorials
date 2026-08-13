---
category: general
date: 2026-03-05
description: Быстро преобразуйте TIFF в текст на C# с помощью Aspose OCR. Узнайте,
  как за считанные минуты отображать OCR‑текст из многостраничных TIFF‑файлов.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: ru
og_description: Конвертировать TIFF в текст на C# с помощью Aspose OCR. Это руководство
  покажет, как пошагово отображать OCR‑текст из многостраничных TIFF‑изображений.
og_title: Конвертировать TIFF в текст на C# – Полное руководство по Aspose OCR
tags:
- Aspose
- OCR
- C#
- TIFF
title: Преобразовать TIFF в текст в C# с помощью Aspose OCR
url: /ru/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация TIFF в текст на C# с использованием Aspose OCR

Нужно **конвертировать TIFF в текст** на C#? Вы не одиноки — многие разработчики сталкиваются с извлечением читаемых строк из многостраничных файлов TIFF. Хорошая новость в том, что Aspose OCR C# делает эту задачу почти без усилий, и вы можете **отображать OCR‑текст** в консоли или передавать его в другую систему за секунды.

В этом руководстве мы пройдем полный, готовый к запуску пример, который показывает, как загрузить многостраничный TIFF, выполнить OCR и вывести текст каждой страницы. Никаких скрытых шагов, без «см. документацию». К концу вы получите автономную программу, которую можно добавить в любой проект .NET.

## Что понадобится

- .NET 6.0 или новее (пример ориентирован на .NET 6, но .NET 5 также подходит)  
- Действительный файл лицензии Aspose OCR (`Aspose.OCR.lic`). Библиотека работает без лицензии, но будет показывать 20‑секундный пробный водяной знак.  
- Многостраничный TIFF‑файл, который вы хотите обработать (назовём его `multipage.tif`).  
- Visual Studio 2022 или любой другой редактор — ничего экзотического.

Если все пункты выполнены, давайте приступим.

## Шаг 1: Установите NuGet‑пакет Aspose OCR

Перед тем как любой код выполнится, вам нужна сама библиотека. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Эта однострочная команда скачивает последнюю стабильную версию (на март 2026 года это 23.9).  

> **Pro tip:** Держите пакеты в актуальном состоянии; новые релизы часто включают оптимизации производительности для больших TIFF‑файлов.

## Шаг 2: Настройте лицензию Aspose OCR C# (необязательно, но рекомендуется)

Запуск OCR‑движка без лицензии возможен, но вывод будет предваряться предупреждением о пробной версии. Чтобы избавиться от него, укажите путь к вашему файлу `.lic`:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Если пропустить этот шаг, код всё равно будет работать — просто помните о дополнительном тексте в результатах.

## Шаг 3: Загрузите и распознайте многостраничный TIFF

Теперь мы действительно **конвертируем TIFF в текст**. Вспомогательный метод `ImageStream.FromFile` читает файл в формат, понятный движку. После этого вызываем `Recognize()`, который возвращает объект `OcrResult` с текстом каждой страницы.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Why this matters:** `Recognize()` делает всю тяжёлую работу — анализ пикселей, определение языка и восстановление строк текста — полностью на C#. Объект результата даёт постраничный доступ, что идеально подходит для **отображения OCR‑текста** позже.

## Шаг 4: Перебор страниц и **отображение OCR‑текста**

Получив результат, мы просто проходим по страницам и выводим каждую. Здесь вы действительно видите преобразование изображения в обычный текст.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

Запуск программы выдаёт вывод, похожий на следующий (реальный текст будет отличаться в зависимости от содержимого TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

Вот и всё — вы успешно **конвертировали TIFF в текст** и **отобразили OCR‑текст** для каждой страницы.

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать в новый консольный проект (`dotnet new console`). В ней присутствуют все директивы `using`, обработка лицензии и проверка ошибок.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected output** (сокращённый для наглядности) показан выше. Если видите пробный водяной знак, проверьте правильность пути к лицензии.

## Частые проблемы при конвертации TIFF в текст

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Out‑of‑memory on huge TIFFs** | Движок загружает всё изображение в ОЗУ. | Используйте `ImageStream.FromFile(..., loadOnlyFirstPage: false)` и обрабатывайте страницы партиями, либо увеличьте лимит памяти процесса. |
| **Garbage characters** | Низкое разрешение исходных изображений сбивает OCR‑движок. | Предобработайте TIFF (например, увеличьте DPI до 300) перед передачей в Aspose OCR. |
| **License not applied** | `SetLicense` бросает исключение, которое игнорируется. | Оберните вызов в `try/catch` (как показано) и запишите ошибку в лог. |
| **Missing language data** | По умолчанию OCR предполагает английский язык. | Установите `ocrEngine.Language = OcrLanguage.French;` (или любой поддерживаемый язык) перед `Recognize()`. |

Устранение этих крайних случаев гарантирует стабильную работу конвертации в продакшене.

## Следующие шаги: выход за пределы простого отображения

Теперь, когда вы умеете **конвертировать TIFF в текст** и **отображать OCR‑текст**, вы можете:

- **Сохранить извлечённый текст** в файл `.txt` или базу данных для последующего анализа.  
- **Объединить несколько TIFF‑файлов** в один поисковый PDF с помощью Aspose.PDF.  
- **Применить постобработку** (проверка орфографии, очистка с помощью regex) для повышения точности.  

Все эти расширения строятся на том же базовом шаблоне, который мы только что рассмотрели.

---

### Кратко

Мы прошли полный C#‑решение, которое **конвертирует TIFF в текст** с помощью Aspose OCR C#. Код создаёт `OcrEngine`, при необходимости загружает лицензию, читает многостраничный TIFF, запускает OCR и **отображает OCR‑текст** постранично. С предоставленным полным примером вы можете добавить его в любой проект .NET и сразу начать извлекать текст.

Есть вопросы о производительности, поддержке языков или интеграции с другими продуктами Aspose? Оставляйте комментарий ниже — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}