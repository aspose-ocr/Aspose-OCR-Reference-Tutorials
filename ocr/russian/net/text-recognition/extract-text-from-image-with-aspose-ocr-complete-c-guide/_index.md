---
category: general
date: 2026-01-07
description: Извлечение текста из изображения с помощью Aspose OCR в C#. Узнайте,
  как распознавать текст с фотографии, улучшать точность OCR, загружать изображение
  для OCR и задавать язык OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: ru
og_description: Извлечение текста из изображения с помощью Aspose OCR. Это руководство
  показывает, как распознавать текст на фотографии, улучшать точность OCR, загружать
  изображение для OCR и задавать язык OCR.
og_title: Извлечение текста из изображения с помощью Aspose OCR – учебник C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Извлечение текста из изображения с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения – полная реализация на C# с Aspose OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не были уверены, какая библиотека даст надёжные результаты? Вы не одиноки. Во многих реальных приложениях — сканерах чеков, проверках удостоверений или просто быстром инструменте для заметок — возможность **распознавать текст с фотографии** является обязательной функцией.

В этом руководстве мы пройдемся по полному, готовому к запуску примеру, который покажет, как **загрузить изображение для OCR**, настроить движок для **установки языка OCR** и применить несколько приёмов предобработки для **повышения точности OCR**. К концу вы получите один файл C#, который выводит извлечённый текст в консоль, и поймёте, почему каждую настройку важно учитывать.

> **Подсказка:** код работает с Aspose.OCR ≥ 23.5, .NET 6+ и любой средой Windows, Linux или macOS, способной запускать .NET Core.

## Необходимые условия

- .NET 6 SDK (или новее) установлен  
- Visual Studio 2022, VS Code или любой предпочитаемый редактор  
- NuGet‑пакет `Aspose.OCR` (установить через `dotnet add package Aspose.OCR`)  
- Файл изображения (JPEG/PNG), содержащий чёткий печатный или наборный текст  

Если всё готово, приступим.

![пример извлечения текста из изображения](/images/ocr-example.png "извлечение текста из изображения – вывод Aspose OCR")

## Шаг 1: Создание и освобождение OCR‑движка – ядро «Извлечение текста из изображения»

Первое, что вам понадобится, — экземпляр `OcrEngine`. Оборачивание его в блок `using` гарантирует корректное освобождение нативных ресурсов.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Почему это важно:** `OcrEngine` хранит неуправляемую память для нативных DLL‑файлов OCR. Своевременное освобождение предотвращает утечки памяти, особенно при пакетной обработке большого количества изображений.

## Шаг 2: Определение настроек распознавания – улучшение точности OCR

Далее создаём объект `RecognitionSettings`. Здесь мы **устанавливаем язык OCR** и добавляем фильтры предобработки, которые часто делают разницу между искажённой строкой и чистым выводом.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Зачем эти фильтры?**  
- **Deskew** исправляет распространённую проблему, когда фото, сделанное телефоном, отклонено на несколько градусов.  
- **Denoise** удаляет пятна, которые могут быть восприняты как символы.  
- **ContrastEnhance** делает бледные чернила более заметными, что необходимо для **повышения точности OCR**.

## Шаг 3: Загрузка изображения – эффективная загрузка изображения для OCR

Aspose предоставляет `ImageStream.FromFile` для быстрой загрузки. При необходимости можно передать `MemoryStream`, если изображение поступает из веб‑запроса или базы данных.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Распространённая ошибка:** указание пути с прямыми слешами в Windows работает, но использование `Path.Combine` безопаснее для кросс‑платформенных проектов.

## Шаг 4: Выполнение распознавания – распознавание текста с фотографии

Теперь вызываем `Recognize`, передавая поток изображения и наши настройки. Метод возвращает обычную строку с извлечённым текстом.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Если изображение содержит несколько блоков текста, Aspose объединяет их с переводами строк, насколько это возможно сохраняя исходную разметку.

## Шаг 5: Вывод результата – проверка извлечения

Наконец, выводим результат в консоль. В реальном приложении вы, вероятно, сохраните его в базе данных, отправите в другой сервис или отобразите в пользовательском интерфейсе.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Ожидаемый вывод в консоль

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Если вы видите искажённые символы, проверьте, что изображение чёткое, язык соответствует тексту и фильтры предобработки подходят.

## Шаг 6: Дополнительные настройки – тонкая настройка для граничных случаев

### a. Смена языков

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Добавление пользовательских фильтров

Aspose также предлагает `PreprocessFilter.Sharpen` или `PreprocessFilter.Binarize`. Поэкспериментируйте с ними, если базовый набор фильтров не даёт нужного результата.

### c. Обработка больших изображений

Для очень высокоразрешённых фотографий сначала уменьшите масштаб, чтобы снизить потребление памяти:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Часто задаваемые вопросы

**Q: Работает ли это с рукописными заметками?**  
A: Aspose OCR оптимизирован для печатного текста. Распознавание рукописного требует другого движка (например, Aspose.OCR for Handwriting или модели машинного обучения).

**Q: Могу ли я обрабатывать несколько изображений в цикле?**  
A: Конечно. Просто вынесите блок `using (var ocrEngine = new OcrEngine())` за пределы цикла и переиспользуйте движок для лучшей производительности.

**Q: Что делать, если изображение — страница PDF?**  
A: Сначала преобразуйте страницу PDF в изображение (Aspose.PDF может рендерить страницы в PNG/JPEG), затем передайте её OCR‑движку.

## Итоги – чего мы достигли

- **Извлекли текст из изображения** с помощью единой, автономной программы на C#.  
- Показали, как **распознавать текст с фотографии** с предобработкой, которая **повышает точность OCR**.  
- Продемонстрировали правильный способ **загрузки изображения для OCR** и **установки языка OCR** для многоязычных сценариев.  

## Следующие шаги и связанные темы

- **Пакетная обработка:** объедините этот фрагмент с `Directory.GetFiles`, чтобы выполнить OCR для всей папки.  
- **Пост‑обработка:** используйте регулярные выражения для очистки дат, сумм или идентификаторов после извлечения.  
- **Интеграции:** передайте извлечённый текст в Azure Cognitive Search или Elastic для создания поисковых документов.  

Экспериментируйте с различными комбинациями фильтров, языков и источников изображений. Основной шаблон остаётся тем же: создайте движок, настройте параметры, загрузите изображение, выполните распознавание и выведите результат. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}