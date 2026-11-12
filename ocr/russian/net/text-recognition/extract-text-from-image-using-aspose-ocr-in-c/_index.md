---
category: general
date: 2026-08-09
description: Извлеките текст из изображения с помощью Aspose OCR в C#. Узнайте, как
  загрузить изображение для OCR, установить язык OCR, выполнить обработку изображения
  и эффективно преобразовать его в текст.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: ru
lastmod: 2026-08-09
og_description: Извлечение текста из изображения с помощью Aspose OCR на C#. Этот
  учебник показывает, как загрузить изображение для OCR, установить язык OCR, выполнить
  обработку изображения и преобразовать изображение в текст в несколько строк кода.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Извлечение текста из изображения с помощью Aspose OCR – руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Извлечение текста из изображения с помощью Aspose OCR на C#
url: /ru/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения с помощью Aspose OCR на C#

Если вам нужно **извлечь текст из изображения** в .NET‑приложении, это руководство проведёт вас через полное, готовое к запуску решение. Вы увидите, как **загрузить изображение для OCR**, выбрать правильный языковой модуль, запустить OCR‑движок и, наконец, **преобразовать изображение в текст** всего несколькими строками C#.

В руководстве рассматривается всё, что необходимо для получения надёжных результатов с Aspose.OCR, включая распространённые подводные камни, такие как неподдерживаемые форматы изображений и особенности конкретных языков. К концу вы получите автономную программу, выводящую распознанный текст в консоль.

## Что вы достигнете

* Загрузить файл изображения в движок Aspose OCR.  
* **Установить язык OCR** (в примере — кириллица, но любой поддерживаемый язык подходит).  
* **Обработать изображение OCR** и получить его текстовое представление.  
* **Преобразовать изображение в текст** и отобразить его, готовый для дальнейшей обработки или хранения.  

**Требования**

* .NET 6.0 или новее (код также работает на .NET Framework 4.6+).  
* Visual Studio 2022 (или любой IDE, поддерживающий C#).  
* NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Извлечение текста из изображения — полный разбор кода

Ниже представлен полный, исполняемый пример программы. Скопируйте его в новый консольный проект и замените `YOUR_DIRECTORY/sample_cyrillic.jpg` на путь к вашему изображению.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Почему каждый шаг важен

1. **Создать экземпляр OCR‑движка** – `OcrEngine` инкапсулирует всю функциональность OCR. Своевременное освобождение (Dispose) освобождает нативные ресурсы, что критично для длительно работающих сервисов.  
2. **Установить язык OCR** – Выбор правильного языкового модуля значительно повышает точность. Aspose предоставляет более 30 языковых пакетов; по умолчанию — английский. В примере используется кириллица для демонстрации нелатинского скрипта.  
3. **Загрузить изображение для OCR** – Движок работает с `ImageStream`. Предоставление изображения высокого разрешения (≥300 dpi) уменьшает количество ошибок распознавания, особенно для сложных скриптов.  
4. **Обработать изображение OCR** – Здесь происходит основная работа. Метод возвращает `OcrResult`, содержащий извлечённый текст, оценки уверенности и необязательные данные о разметке.  
5. **Преобразовать изображение в текст** – `result.Text` представляет собой обычную `string`. Вы можете записать её в файл, передать в поисковый индекс или использовать в последующих NLP‑конвейерах.  

---

## Загрузка изображения для OCR

Метод `ImageStream.FromFile` поддерживает распространённые растровые форматы. Если вы получаете изображения в виде массивов байтов (например, из веб‑API), используйте `ImageStream.FromBytes(byte[])` вместо этого:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Совет:** Всегда проверяйте, что изображение не повреждено перед передачей его в движок. Быстрая проверка `try { Image.FromFile(...); } catch { ... }` предотвращает исключения во время выполнения.

---

## Установка языка OCR

Aspose.OCR поставляется с языковыми пакетами, которые можно включать во время выполнения. Чтобы вывести список всех доступных языков:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Если необходимо распознавать несколько языков в одном документе, объединяйте их с помощью побитового оператора OR:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Особый случай:** Смешивание языков с написанием справа налево (RTL) (например, арабский) с языками слева направо может потребовать дополнительной обработки разметки. Aspose автоматически определяет направление, но вы можете тонко настроить его через `engine.PageSegmentationMode`.

---

## Обработка изображения OCR

Вызов `Process` синхронный и блокирует выполнение, пока движок не завершит работу. Для больших пакетов или UI‑приложений рассмотрите асинхронную перегрузку:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Распространённая ошибка:** Если не установить `engine.Image` перед вызовом `Process`, будет выброшено `InvalidOperationException`. Всегда сначала назначайте изображение.

---

## Преобразование изображения в текст

Извлечённую строку можно обрабатывать как любой другой .NET `string`. Например, чтобы записать результат в файл:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Если необходимо сохранить переносы строк точно так, как они выглядят на изображении, используйте `result.Text` напрямую. Для пост‑обработки (например, удаления лишних пробелов) применяйте стандартные методы строк:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Итоговый пример

Объединив всё вместе, программа:

1. Создаёт экземпляр `OcrEngine`.  
2. **Устанавливает язык OCR** на кириллицу (или любой выбранный вами язык).  
3. **Загружает изображение для OCR** с диска.  
4. **Обрабатывает изображение OCR**, получая текстовый результат.  
5. **Преобразует изображение в текст** и выводит его.  

Запуск примера с чётким кириллическим изображением выдаёт вывод, похожий на:

```
=== Recognized Text ===
Пример текста на кириллице
```

Если изображение содержит английский текст, просто измените `engine.Language = OcrLanguage.English;`, и тот же код **правильно извлечёт текст из изображения**.

---

## Заключение

Теперь вы знаете, как **извлекать текст из изображения** с помощью Aspose OCR на C#. В руководстве рассмотрены загрузка изображения, выбор соответствующего языка, запуск процесса OCR и **преобразование изображения в текст** для последующего использования.

Далее вы можете:

* Экспериментировать с другими языками (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Интегрировать шаг OCR в более крупный конвейер (например, импорт документов, поисковые PDF).  
* Оптимизировать производительность, обрабатывая изображения пакетами или используя асинхронный API.  

Не стесняйтесь изучать документацию Aspose.OCR для продвинутых возможностей, таких как пользовательские словари, режимы сегментации страниц и настройка точности OCR. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Как выполнить извлечение текста из изображения из потока с использованием Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}