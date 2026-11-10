---
category: general
date: 2026-06-28
description: Выполните OCR изображения с помощью Aspose.OCR в C#. Научитесь распознавать
  текст на изображении, извлекать текст из счета, загружать изображение для OCR и
  записывать JSON в файл.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: ru
og_description: Выполните OCR изображения с помощью Aspose.OCR в C#. Это руководство
  показывает, как распознавать текст на изображении, извлекать текст из счета и записывать
  JSON в файл.
og_title: Распознавание текста на изображении в C# – учебник Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: Выполнить OCR изображения в C# – Полное руководство Aspose
url: /ru/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении в C# – Полное руководство Aspose

Когда‑нибудь вам нужно было **perform OCR on image** файлы, но вы не были уверены, какая .NET библиотека даст вам чистые, структурированные результаты? Вы не одиноки — разработчики постоянно спрашивают, как **recognize text from image** ресурсы, особенно при работе со счетами или чеками. В этом руководстве мы пройдем практический пример, который не только **loads image for OCR**, но и **extracts text from invoice** данные и **writes JSON to file** для дальнейшей обработки.

К концу этого руководства у вас будет готовое к запуску консольное приложение, которое:

* Создаёт экземпляр движка Aspose OCR,
* Загружает PNG (или JPG) изображение,
* Распознаёт текстовое содержимое,
* Сериализует результат в красиво отформатированный JSON,
* Сохраняет этот JSON на диск.

Без внешних сервисов, без скрытой магии — просто чистый C# код, который вы можете скопировать, вставить и запустить.

## Предварительные требования

* .NET 6 SDK или новее (код работает как с .NET Core, так и с .NET Framework).
* Действительная лицензия Aspose.OCR или временный оценочный ключ (бесплатная пробная версия подходит для тестирования).
* Visual Studio 2022, VS Code или любой предпочитаемый IDE.
* Файл изображения — например `invoice.png` — размещён где‑нибудь, чтобы вы могли ссылаться на него полным или относительным путём.

> **Pro tip:** Если вы работаете со сканированными счетами, рассмотрите предварительную обработку изображения (выравнивание, повышение контрастности) перед передачей его в OCR‑движок. Aspose.OCR автоматически обрабатывает многие из этих шагов, но чистое исходное изображение всегда даёт лучшие результаты.

---

## Шаг 1: Настройка проекта и установка Aspose.OCR

Сначала создайте новый консольный проект и подключите пакет Aspose.OCR из NuGet.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Почему этот шаг важен:** Сборка `Aspose.OCR` предоставляет класс `OcrEngine`, который мы будем использовать для **perform OCR on image** данных. Без пакета компилятор не распознает типы, связанные с OCR.

---

## Шаг 2: Загрузка изображения для OCR

Теперь мы напишем код, который **load image for OCR**. Метод `OcrImage.FromFile` принимает абсолютный или относительный путь и оборачивает bitmap в формат, понятный движку.

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **Объяснение:** Разделяя путь в отдельную переменную, мы поддерживаем чистоту кода и упрощаем повторное использование того же изображения позже (например, при логировании или отладке). Если файл не найден, `FromFile` бросает `FileNotFoundException`, который вы можете перехватить, чтобы вывести дружелюбное сообщение об ошибке.

---

## Шаг 3: Выполнение OCR на изображении и распознавание текста

Имея изображение, мы создаём экземпляр `OcrEngine` и просим его **recognize text from image**. Этот шаг — сердце руководства, здесь происходит настоящая магия OCR.

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Почему мы используем `using var`:** `OcrEngine` держит неуправляемые ресурсы (нативные библиотеки). Оборачивание его в блок `using` гарантирует корректное освобождение, предотвращая утечки памяти — особенно важно в длительно работающих сервисах.

> **Что вы получаете:** `ocrResult` содержит необработанный текст, оценки уверенности и информацию о раскладке (строки, слова, ограничивающие рамки). Для большинства конвейеров обработки счетов свойства `Text` достаточно, но дополнительные метаданные могут помочь в валидации или визуальной отладке.

---

## Шаг 4: Преобразование результата в красиво отформатированный JSON

Aspose.OCR упрощает **write JSON to file**, так как `OcrResult` предоставляет метод `ToJson`. Передавая `indent: true`, мы получаем читаемый человеком вывод, что удобно, когда позже нужно **extract text from invoice** записи.

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **Пример фрагмента JSON** (усечён для краткости):

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **Примечание о граничных случаях:** Если OCR‑движок не обнаружит текст, `ocrResult.Text` будет пустой строкой, но JSON всё равно будет содержать метаданные, такие как размеры изображения. Вы можете проверять пустые результаты перед записью файла.

---

## Шаг 5: Запись JSON в файл

Теперь мы наконец **write JSON to file**. Использование `File.WriteAllText` гарантирует, что вся строка будет записана на диск одной атомарной операцией.

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **Советы для продакшна:** Рассмотрите возможность добавления метки времени к имени файла (`invoice_20260628_1500.json`), чтобы избежать перезаписи предыдущих запусков. Также оберните операцию записи в блок try/catch, чтобы корректно обрабатывать проблемы с правами доступа.

---

## Шаг 6: Полный рабочий пример

Собрав все части вместе, вот полный код программы, который вы можете сразу же скомпилировать и запустить. Замените `YOUR_DIRECTORY` на папку, содержащую `invoice.png`.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**Ожидаемый вывод** при запуске программы:

```
JSON saved to C:\Invoices\invoice.json
```

Откройте `invoice.json`, и вы увидите красиво отформатированное представление данных OCR, готовое для дальнейшего разбора или хранения.

---

## Часто задаваемые вопросы и граничные случаи

### Что если изображение содержит несколько языков?

Aspose.OCR автоматически определяет язык по набору символов. Если необходимо принудительно задать конкретный язык (например, английский для большинства счетов), установите свойство `Language` у движка:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### Как обрабатывать большие PDF‑файлы с множеством страниц?

Сначала преобразуйте каждую страницу в изображение (используя библиотеку PDF‑to‑image), а затем пройдитесь по изображениям, применяя ту же процедуру **perform OCR on image**. Сведите результаты JSON в один массив, если нужен консолидированный вывод.

### Можно ли потоково передавать JSON вместо записи целого файла?

Да. Если вы создаёте веб‑API, вы можете вернуть `json` напрямую в теле ответа:

```csharp
return Results.Json(ocrResult);
```

### Что насчёт производительности?

В примере выше OCR‑движок работает синхронно. Для сценариев с высокой пропускной способностью оберните вызов распознавания в `Task.Run` или используйте асинхронные версии (если доступны), чтобы UI оставался отзывчивым или чтобы параллелить пакетную обработку.

---

## Заключение

Мы прошли через лаконичное решение от начала до конца, которое **perform OCR on image** файлы, **recognize text from image**, **extract text from invoice**, и в конце **write JSON to file** с использованием Aspose.OCR в C#. Код преднамеренно прост, чтобы вы могли адаптировать его к более сложным рабочим процессам — будь то добавление предобработки изображений, передача JSON в базу данных или публикация результата через REST‑endpoint.

Готовы к следующему шагу? Попробуйте заменить PNG на JPEG, поэкспериментировать с различными настройками OCR (например, `ocrEngine.Dpi`), или интегрировать шаг конвертации PDF в изображение для обработки целых пакетов счетов. Возможности безграничны, как только вы освоите основы.

Счастливого кодинга, и пусть ваши результаты OCR всегда будут чёткими и точными!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как использовать Aspose OCR для получения результата в JSON при распознавании изображений](/ocr/english/net/text-recognition/get-result-as-json/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Извлечение текста из изображения — распознавание строки с Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}