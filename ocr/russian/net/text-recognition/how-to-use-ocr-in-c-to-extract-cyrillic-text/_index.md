---
category: general
date: 2026-09-10
description: Как использовать OCR в C# для извлечения кириллического текста, предобработки
  изображений и конвертации их в PDF или HTML‑файлы в одном исполняемом примере.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: ru
lastmod: 2026-09-10
og_description: Как использовать OCR в C# для извлечения кириллического текста, предобработки
  изображений и экспорта результатов в PDF или HTML. Следуйте этому пошаговому руководству.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Как использовать OCR в C# – извлекать кириллический текст и конвертировать
  изображения
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Как использовать OCR в C# для извлечения кириллического текста
url: /ru/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# для извлечения кириллического текста

Если вам нужно **как использовать OCR** в C# для извлечения кириллического текста из отсканированных документов, это руководство покажет готовое решение, которое можно сразу запустить. Вы также узнаете, как **предобрабатывать изображение для OCR**, а также как **конвертировать изображение в PDF** или **конвертировать изображение в HTML** после распознавания текста.

Проекты по оцифровке документов часто сталкиваются с двумя проблемами: сканы низкого качества и необходимость сохранять результаты в нескольких форматах. Это руководство решает обе задачи с помощью библиотеки Aspose.OCR, которая автоматически загружает недостающие языковые пакеты, предоставляет встроенные вспомогательные средства обработки изображений и может экспортировать результат OCR в PDF или HTML одним вызовом.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 SDK или новее (код также работает с .NET Framework 4.7+).
* Visual Studio 2022 или любой редактор, поддерживающий проекты C#.
* NuGet‑пакет **Aspose.OCR**. Установите его командой:

```bash
dotnet add package Aspose.OCR
```

* Файл изображения, содержащий кириллические символы (например, `sample_cyrillic.jpg`).  
  Поместите файл в папку, которую сможете указать как `YOUR_DIRECTORY`.

Библиотека загрузит языковой пакет Cyrillic при первом выполнении `ocrEngine.Language = Language.Cyrillic;`, поэтому ручная загрузка не требуется.

## Шаг 1 – Инициализация OCR‑движка (how to use OCR)

Создание экземпляра `OcrEngine` подготавливает движок для всех последующих операций.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Почему это важно:** Движок хранит конфигурацию, такую как язык, настройки обработки изображений и параметры вывода. Инициализировав его один раз, вы делаете остальной код чище и потокобезопасным.

## Шаг 2 – Выбор кириллического языка (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Почему это важно:** Точность OCR сильно зависит от правильной языковой модели. Явно указывая `Language.Cyrillic`, движок использует таблицы частот символов, подходящие для русского, украинского, болгарского и т.д.

## Шаг 3 – Предобработка изображения для OCR

Сканы низкого качества могут содержать наклон, шум или неравномерное освещение. Встроенный `ImageProcessor` может улучшить распознавание всего двумя вызовами.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Почему это важно:** Предобработка уменьшает количество ошибочных символов и повышает коэффициент уверенности. Наклонённый текст часто приводит к искажённому выводу; выравнивание (deskew) исправляет это. Удаление шумов (despeckle) устраняет мелкие артефакты, которые OCR‑движок мог бы принять за буквы.

> **Полезный совет:** Если ваши исходные изображения уже чистые, эти вызовы можно пропустить. Для сильно повреждённых сканов рассмотрите дополнительные шаги, такие как `Binarize()` или `ContrastStretch()`.

## Шаг 4 – Выполнение OCR над входным изображением

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Почему это важно:** `Process` запускает конвейер распознавания над переданным битмапом. Метод возвращает `void`; распознанный текст становится доступным через свойство `Text`.

## Шаг 5 – Получение распознанного текста и сохранение его в файл

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Почему это важно:** Сохранение сырого текста позволяет выполнять дальнейшую обработку, такую как поиск, индексацию или передачу в сервисы перевода.

## Шаг 6 – Экспорт результата OCR в другие форматы (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Почему это важно:** Конвертация результата OCR в PDF или HTML сохраняет визуальный контекст оригинального изображения, одновременно предоставляя поисковый текст. Это особенно ценно для юридических или архивных процессов.

### Ожидаемый результат

Запуск программы с чистым кириллическим сканом создаёт три файла:

* `result.txt` – обычный Unicode‑текст, например `Пример текста на кириллице`.
* `result.pdf` – PDF, содержащий изображение с невидимым слоем текста для поиска.
* `result.html` – HTML‑страница, показывающая изображение и выделяемый текст.

Откройте любой из файлов, чтобы убедиться, что кириллические символы извлечены корректно.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если загрузка языкового пакета не удалась?** | Убедитесь, что у машины есть доступ в интернет. Вы также можете предварительно скачать пакет с сайта Aspose и разместить его в папке `bin`. |
| **Можно ли распознавать другие алфавиты в том же запуске?** | Да. Установите `ocrEngine.Language = Language.English;` (или любой поддерживаемый enum) перед вызовом `Process`. При смешанных скриптах может потребоваться отдельный вызов `Process` для каждого языка. |
| **Моё изображение – многостраничный TIFF, будет ли это работать?** | `OcrEngine` обрабатывает один битмап за раз. Загрузите каждую страницу в `Bitmap` и вызывайте `Process` в цикле, объединяя результаты. |
| **Как повысить производительность при больших партиях?** | Переиспользуйте один экземпляр `OcrEngine` и установите `ocrEngine.OptimizeMemory = true;`. Также рассмотрите параллельную обработку с отдельными экземплярами движка для каждого потока. |

## Заключение

Теперь вы знаете **как использовать OCR** в C# для **извлечения кириллического текста**, **предобработки изображения для OCR**, а также **конвертации изображения в PDF** или **конвертации изображения в HTML** в несколько лаконичных шагов. Полный пример демонстрирует готовое к использованию решение для производства.

## Что изучать дальше?

Следующие руководства охватывают близко связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как использовать AspOCR: предобработка фильтров OCR для изображений в .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Как извлечь текст OCR в C# – Полное пошаговое руководство](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Как использовать Aspose OCR для получения результата в JSON при распознавании изображений](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}