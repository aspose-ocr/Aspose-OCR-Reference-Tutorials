---
category: general
date: 2026-11-20
description: Как использовать OCR в C# для распознавания текста на изображении. Узнайте,
  как загрузить изображение в OCR, установить язык OCR и извлечь текст из файлов JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: ru
lastmod: 2026-11-20
og_description: Как использовать OCR в C# для извлечения текста из изображений. Это
  руководство показывает загрузку изображения, настройку языка OCR и распознавание
  текста из файлов JPEG.
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: Как использовать OCR в C# – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: Как использовать OCR в C# с распознаванием изображений
url: /ru/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# с распознаванием изображений

Если вам нужно **как использовать OCR** в приложении на C#, это руководство проведёт вас через весь процесс. Независимо от того, оцифровываете ли вы отсканированные контракты или извлекаете информацию из фотографий, вы быстро и надёжно научитесь **распознавать текст на изображениях**.

В руководстве рассматривается загрузка изображения, настройка OCR‑движка и получение распознанного текста из JPEG‑файлов. К концу вы получите автономный, готовый к запуску пример, который можно вставить в любой проект .NET.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен.
* Доступ к OCR‑библиотеке, предоставляющей `OcrEngine`, `ImageStream` и языковые модули (например, **Leadtools**, **Aspose.OCR** или любой совместимый пакет).
* Пример изображения с именем `sample.jpg` в известном каталоге.

Дополнительные внешние сервисы не требуются — OCR‑движок автоматически загрузит недостающие языковые пакеты.

## Шаг 1: Загрузка изображения для OCR

Загрузка изображения — первый шаг в любом процессе OCR. Ниже приведён код, создающий `ImageStream` из JPEG‑файла на диске.

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*Почему это важно:* Объект `ImageStream` абстрагирует работу с файлом и предоставляет пиксельные данные, которые потребляет OCR‑движок. Если файл не найден, `FromFile` бросает понятное исключение, что упрощает отладку.

## Шаг 2: Создание экземпляра OCR‑движка (авто‑освобождение)

Использование блока `using` гарантирует, что неуправляемые ресурсы будут освобождены сразу после завершения работы OCR.

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*Совет профессионала:* Оператор `using` предпочтительнее ручных вызовов `Dispose()`, так как исключает риск забыть освободить нативную память, что может привести к утечкам в длительно работающих сервисах.

## Шаг 3: Установка языка OCR (необязательно, но рекомендуется)

Если вы знаете язык исходного документа, его указание повышает точность и ускоряет обработку. В примере язык установлен на кириллицу; вы можете заменить его на любой поддерживаемый enum языка.

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*Зачем задавать язык?* OCR‑движки содержат языково‑специфичные модели символов. Выбирая правильную модель, вы уменьшаете количество ложных срабатываний и избегаете ненужных замен символов.

## Шаг 4: Выполнение OCR над загруженным изображением

Теперь движок обрабатывает bitmap и возвращает распознанный текст в виде строки.

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*Особый случай:* Если изображение имеет низкое разрешение или сильно сжато, движок может вернуть частичные результаты. Рассмотрите предобработку (например, бинаризацию) для лучшего результата.

## Шаг 5: Вывод распознанного текста

Наконец, отобразите извлечённый текст в консоли или передайте его другому компоненту.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**Ожидаемый вывод**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

Точное содержание зависит от исходного изображения, но в консоли будет показана полная строка, обнаруженная OCR‑движком.

## Полный, готовый к запуску пример

Объединение всех шагов даёт компактную программу, которую можно сразу собрать и запустить.

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Скопируйте код в новый консольный проект, замените `YOUR_DIRECTORY` на путь к вашему изображению и выполните `dotnet run`. Программа выведет распознанный текст в консоль.

## Часто задаваемые вопросы и устранение неполадок

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если языковой пакет не загружен?** | OCR‑библиотека попытается загрузить его автоматически. Убедитесь, что у машины есть доступ к интернету, либо предварительно установите языковой пакет согласно документации библиотеки. |
| **Можно ли распознавать текст из PNG или BMP файлов?** | Да. `ImageStream.FromFile` работает с любым форматом, поддерживаемым базовой библиотекой изображений. Просто измените расширение файла. |
| **Как улучшить точность при шумных сканах?** | Выполните предобработку изображения (регулировка контраста, удаление шума) перед передачей его в `Recognize`. Многие библиотеки предоставляют классы `ImageProcessor` для этой цели. |
| **Безопасно ли запускать OCR над загруженными пользователями файлами?** | Проверяйте размер и тип файла, а также запускайте OCR в изолированной (sandbox) среде, чтобы избежать выполнения вредоносных payload‑ов. |

## Заключение

Теперь вы знаете **как использовать OCR** в C# для **распознавания текста на изображениях**, **загрузки изображения в OCR**, **установки языка OCR** и **распознавания текста из JPEG** надёжно. Полный пример демонстрирует чистый, освобождаемый процесс, который можно расширять дополнительной предобработкой, поддержкой нескольких языков или интеграцией в более крупные конвейеры обработки документов.

### Следующие шаги

* Исследуйте пакетную обработку, перебирая каталог JPEG‑файлов.  
* Сочетайте OCR с обработкой естественного языка (NLP) для извлечения структурированных данных.  
* Поэкспериментируйте с другими языковыми модулями, например `OcrLanguage.English` или `OcrLanguage.Arabic`.  

Не стесняйтесь адаптировать код под ваш конкретный сценарий, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Use Windows.Media.Ocr to recognize text image in C# – Full OCR Guide](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [How to Use OCR in C# – Extract Text from Image Asynchronously](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [How to Use OCR in C# – Extract Text from Image with Aspose OCR](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}