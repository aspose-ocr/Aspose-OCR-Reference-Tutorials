---
category: general
date: 2026-06-28
description: Создайте поисковый PDF из изображений с помощью C#. Узнайте, как преобразовать
  изображение в PDF, извлечь текст из изображения и распознать несколько языков в
  одном процессе.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- how to recognize multiple languages
- how to generate searchable pdf
language: ru
og_description: Создайте PDF с возможностью поиска с помощью C#. Это руководство показывает,
  как преобразовать изображение в PDF, извлечь текст из изображения и программно распознавать
  несколько языков.
og_title: Создание PDF с возможностью поиска в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  headline: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  type: TechArticle
- description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  name: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code compiles with .NET Core as well). - An
      Aspose.OCR license (you can start with a free trial; the API works without a
      license but adds a watermark). - A sample image that contains English, Arabic,
      and Korean text (or any languages you need). - Visual Studio 2022 or yo'
  - name: What If a Language Isn't Recognized?
    text: If you add a language that the engine doesn’t have a model for, it will
      simply ignore it and fall back to the others. To avoid surprises, double‑check
      the supported language list in the Aspose documentation.
  - name: Expected Output
    text: '``` Plain text: Hello World! مرحبا بالعالم! 안녕하세요 세계! Searchable PDF saved.
      ```'
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Создание PDF с возможностью поиска в C# – Полное руководство с Aspose OCR
url: /ru/net/text-recognition/create-searchable-pdf-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в C# – Полное руководство с Aspose OCR

Когда‑нибудь задавались вопросом, как **создать поисковый PDF** напрямую из изображения, не покидая проект на C#? Вы не одиноки. Будь то оцифровка многоязычных документов или создание приложения для сканирования чеков, превращение картинки в PDF, по которому можно искать, меняет правила игры.

В этом руководстве мы пройдём все шаги по **созданию поискового PDF** с помощью Aspose.OCR, начиная от загрузки изображения и заканчивая экспортом полностью поискового документа. По пути мы также покажем, как **конвертировать изображение в PDF**, **извлекать текст из изображения** и **распознавать несколько языков** — всё в одном асинхронном методе.

## Что вы получите в итоге

- Рабочее консольное приложение на C#, которое читает изображение, выполняет OCR в режиме ускорения GPU и записывает поисковый PDF.
- Понимание, почему включение GPU важно для производительности.
- Техники **извлечения текста из изображения** для последующей обработки.
- Чёткий шаблон **как распознавать несколько языков** за один проход.
- Советы по расширению кода для поддержки других форматов или пользовательских настроек OCR.

### Предварительные требования

- .NET 6.0 SDK или новее (код также компилируется с .NET Core).
- Лицензия Aspose.OCR (можно начать с бесплатной пробной версии; API работает без лицензии, но добавляет водяной знак).
- Пример изображения, содержащего английский, арабский и корейский тексты (или любые нужные вам языки).
- Visual Studio 2022 или ваша любимая IDE.

Все готово? Отлично — приступим.

---

## Шаг 1: Создание проекта и установка Aspose.OCR

Сначала создайте новый консольный проект:

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
```

Затем добавьте пакет Aspose.OCR через NuGet:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если планируете запускать OCR на машине с GPU, также установите пакет `Aspose.OCR.Gpu`. Он автоматически подтягивает нативные библиотеки CUDA.

## Шаг 2: Создание OCR‑движка и включение ускорения GPU

Сердцем операции является `OcrEngine`. Включение GPU может сократить время обработки на несколько секунд для изображений высокого разрешения.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// ...

// Step 2: Create an OCR engine and turn on GPU support
var ocrEngine = new OcrEngine();
ocrEngine.Settings.EnableGpu = true;   // ← speeds up large images dramatically
```

Почему включать GPU? Потому что OCR по сути представляет собой огромную задачу умножения матриц; GPU обрабатывает такие параллельные задачи гораздо эффективнее, чем CPU. Если у вас безголовый сервер без GPU, просто оставьте `EnableGpu` как `false` — движок переключится на обработку процессором.

## Шаг 3: Асинхронная загрузка изображения

Асинхронный ввод‑вывод сохраняет отзывчивость UI и предотвращает истощение пула потоков в серверных сценариях. Вспомогательный метод `OcrImage.FromFileAsync` абстрагирует работу со стримом.

```csharp
using Aspose.OCR;

// ...

// Step 3: Load the image to be processed (async)
var imagePath = @"C:\Docs\multilingual_sample.jpg";
var image = await OcrImage.FromFileAsync(imagePath);
```

Если позже понадобится **конвертировать изображение в PDF**, держите этот экземпляр `OcrImage` под рукой; вы передадите его напрямую экспортеру PDF.

## Шаг 4: Распознавание текста на нескольких языках

Aspose.OCR позволяет указать список кодов языков через запятую. Это ответ на вопрос **как распознавать несколько языков** за один проход.

```csharp
using Aspose.OCR;

// ...

// Step 4: Run OCR with English, Arabic, and Korean support
var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
{
    Language = "en,ar,ko"   // ← multiple languages, order doesn’t matter
});
```

Свойство `ocrResult.Text` теперь содержит простую текстовую репрезентацию всего, что Aspose смог расшифровать. Это ядро **извлечения текста из изображения**.

```csharp
Console.WriteLine("Plain text extracted:");
Console.WriteLine(ocrResult.Text);
```

### Что делать, если язык не распознан?

Если добавить язык, для которого у движка нет модели, он просто будет проигнорирован, а распознавание продолжится для остальных. Чтобы избежать сюрпризов, проверьте список поддерживаемых языков в документации Aspose.

## Шаг 5: Прямой экспорт поискового PDF

Вместо ручного создания PDF и наложения текста, Aspose.OCR предоставляет однострочник для **как сгенерировать поисковый pdf**. Метод встраивает OCR‑текст как невидимый слой, делая PDF поисковым, сохраняя оригинальное изображение.

```csharp
using Aspose.OCR.Output;

// ...

// Step 5: Export the recognized content as a searchable PDF
await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
{
    Language = "en,ar,ko",               // keep language consistency
    OutputPath = @"C:\Docs\sample_searchable.pdf"
});

Console.WriteLine("Searchable PDF saved at C:\\Docs\\sample_searchable.pdf");
```

За кулисами Aspose создаёт страницу PDF с оригинальным битмапом в качестве видимого фона и добавляет скрытый текстовый слой, совпадающий с координатами изображения. Открыв файл в Adobe Reader и нажав **Ctrl + F**, вы сможете находить слова на любом из трёх языков.

## Шаг 6: Собираем всё вместе — полный асинхронный `Main`

Ниже полностью готовая к запуску программа. Вставьте её в `Program.cs`, замените пути к файлам и нажмите **F5**.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Output;

class AllInOne
{
    static async Task Main()
    {
        // Step 2: Create an OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.EnableGpu = true;

        // Step 3: Load the image to be processed (async)
        var image = await OcrImage.FromFileAsync(@"C:\Docs\multilingual_sample.jpg");

        // Step 4: Recognize text in the image using multiple languages
        var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
        {
            Language = "en,ar,ko"
        });

        Console.WriteLine("Plain text:");
        Console.WriteLine(ocrResult.Text);

        // Step 5: Export the recognized content as a searchable PDF
        await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
        {
            Language = "en,ar,ko",
            OutputPath = @"C:\Docs\sample_searchable.pdf"
        });

        Console.WriteLine("Searchable PDF saved.");
    }
}
```

### Ожидаемый вывод

```
Plain text:
Hello World!
مرحبا بالعالم!
안녕하세요 세계!
Searchable PDF saved.
```

Когда откроете `sample_searchable.pdf` и выполните поиск по словам “Hello”, “العالم” или “세계”, движок найдёт соответствующие слова, даже если они отрисованы как часть изображения.

## Шаг 7: Распространённые подводные камни и их решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **GPU не обнаружен** | На машине отсутствуют драйверы CUDA или пакет `Aspose.OCR.Gpu` не установлен. | Установите драйверы NVIDIA, проверьте версию CUDA или задайте `EnableGpu = false`. |
| **Отсутствует поддержка языка** | Код языка не входит в набор встроенных моделей. | Скачайте дополнительный языковой пакет с сайта Aspose или ограничьтесь поддерживаемыми кодами. |
| **PDF пустой** | Неверный путь вывода или процесс не имеет прав записи. | Используйте абсолютный путь с нужными правами, например `C:\Temp\output.pdf`. |
| **Снижение производительности** | Большие изображения (>5 МП) создают нагрузку на память. | Уменьшите размер изображения перед OCR или увеличьте лимит памяти процесса. |

## Расширение примера

- **Пакетная обработка:** Оберните основную логику в цикл `foreach`, проходящий по папке с изображениями.
- **Пользовательские настройки OCR:** Настройте `ocrEngine.Settings.PageSegMode` для одноколоночных или многоколоночных макетов.
- **Внедрение метаданных:** Используйте `PdfExportOptions` для добавления автора, названия или даты создания в поисковый PDF.

---

## Заключение

Теперь у вас есть надёжный сквозной рецепт для **создания поискового pdf** напрямую из изображений с помощью C#. Следуя описанным шагам, вы научились **конвертировать изображение в pdf**, **извлекать текст из изображения** и **распознавать несколько языков** — всё при чистом и асинхронном коде.

Дальше вы можете экспериментировать с различными языковыми пакетами, добавить пост‑обработку OCR (например, проверку орфографии) или интегрировать процесс в веб‑API, который будет выдавать поисковые PDF‑файлы по запросу. Возможности безграничны, а написанный вами код — прочная основа для любого проекта автоматизации документов.

Есть вопросы о настройке производительности или лицензировании? Оставляйте комментарий, и давайте продолжать обсуждение. Счастливого кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}