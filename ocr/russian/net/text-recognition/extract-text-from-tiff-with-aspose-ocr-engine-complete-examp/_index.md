---
category: general
date: 2026-04-04
description: Узнайте, как извлекать текст из файлов TIFF с помощью примера OCR‑движка
  на C#. Пошаговое руководство с выводом в форматах JSON и XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: ru
og_description: 'Извлечение текста из файлов TIFF с использованием OCR‑движка: пример
  на C#. Подробные шаги, полный код и рекомендации по выводу в JSON/XML.'
og_title: Извлечение текста из TIFF с помощью OCR‑движка Aspose – полное руководство
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Извлечение текста из TIFF с помощью OCR‑движка Aspose – полный пример
url: /ru/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из TIFF – Полный пример OCR‑движка на C#

Когда‑нибудь вам нужно было **извлечь текст из TIFF** изображений, но вы не знали, какая библиотека может обрабатывать многостраничные файлы без кучи обходных решений? Вы не одиноки. Во многих устаревших системах документы поступают в виде многостраничных сканов TIFF, и извлечение сырого текста является обязательной функцией для поиска, соответствия требованиям или автоматизации ввода данных.

Хорошая новость? С Aspose OCR вы можете сделать это в паре строк — без возни с низкоуровневыми буферами пикселей. Этот учебник проведёт вас через **полный пример OCR‑движка**, который загружает многостраничный TIFF, распознаёт каждую страницу и выводит красиво отформатированный JSON и опциональный XML. К концу вы получите готовое к запуску консольное приложение C#, которое извлекает текст из TIFF‑файлов за секунды.

## Что вы узнаете

- Как настроить OCR‑движок Aspose OCR в проекте .NET.  
- Точный код, необходимый для **извлечения текста из TIFF** файлов, включая обработку многостраничных документов.  
- Почему может потребоваться вывод в JSON вместо XML и как сгенерировать оба формата.  
- Советы по устранению распространённых проблем (например, DPI изображения, использование памяти).  

### Предварительные требования

- .NET 6.0 SDK или новее (код работает с .NET Core и .NET Framework).  
- Действующая лицензия Aspose OCR (или бесплатный пробный ключ).  
- Visual Studio 2022 или любой другой редактор C#.  
- Пример многостраничного TIFF‑файла (в примере называется `multi-page.tiff`).  

> **Pro tip:** Если у вас ограниченный бюджет, бесплатная пробная версия всё равно позволяет извлекать текст из до 100 страниц в месяц — идеально для тестов.

---

## Шаг 1 – Инициализация OCR‑движка (ocr engine example)

Прежде чем мы сможем **извлечь текст из TIFF**, нам нужен экземпляр OCR‑движка. Этот объект хранит всю конфигурацию, которую вы можете менять позже (язык, разрешение и т.д.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Почему это важно:* Класс `OcrEngine` скрывает всю тяжёлую работу. Создать его один раз и переиспользовать для нескольких изображений гораздо эффективнее по памяти, чем создавать новый движок для каждой страницы.

---

## Шаг 2 – Загрузка многостраничного TIFF (extract text from TIFF)

Теперь указываем движку наш исходный файл. `ImageStream.FromFile` поддерживает TIFF, JPEG, PNG и многие другие форматы, но в этом учебнике мы сосредоточимся на TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Note:** Замените `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.  
> **Tip:** Если ваш TIFF имеет низкое DPI (меньше 150), рассмотрите предварительную обработку для повышения точности OCR.

---

## Шаг 3 – Распознавание всех страниц

Вызов `Recognize()` запускает OCR‑алгоритм для **каждой страницы** в TIFF. Объект результата содержит сырой текст, оценки уверенности и сегментацию по страницам.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Что вы получаете:* `ocrResult` содержит коллекцию объектов `PageResult`. Текст каждой страницы доступен через `ocrResult.Pages[i].Text`. Движок также предоставляет уровни уверенности, что может быть полезно для контроля качества.

---

## Шаг 4 – Сохранение результатов в JSON (и опциональный XML)

Большинство современных конвейеров предпочитают JSON, но унаследованные системы всё ещё работают с XML. Вот как сгенерировать оба формата, красиво отформатированных.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Пример вывода JSON (усечённый)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON читаем человеком, что упрощает отладку. XML отражает ту же структуру, если он вам нужен.

---

## Шаг 5 – Проверка извлечения (extract text from TIFF)

После записи файлов быстрый sanity‑check помогает убедиться, что всё прошло без ошибок.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Если вы видите выводимый фрагмент, вы успешно **извлекли текст из TIFF** и сохранили его. Далее вы можете передать JSON в поисковый индекс, базу данных или любой другой сервис.

---

## Почему использовать Aspose OCR для извлечения текста из TIFF?

- **Поддержка многостраничных файлов из коробки** — нет необходимости вручную разбивать TIFF.  
- **Высокая точность** благодаря проприетарным нейронным моделям.  
- **Кросс‑платформенность** — работает на Windows, Linux и macOS в средах .NET.  
- **Богатые форматы вывода** (JSON, XML, plain text), подходящие как для современных, так и для устаревших стеков.  

Если вы всё ещё сомневаетесь, попробуйте бесплатную пробную версию на образце документа. Вы заметите скорость и простоту по сравнению с открытыми альтернативами, которые часто требуют дополнительной предобработки изображений.

---

## Распространённые проблемы и как их избежать

| Проблема | Симптом | Решение |
|----------|---------|---------|
| Низкое разрешение TIFF | Отсутствуют символы, низкая уверенность | Увеличьте изображение до ≥150 DPI перед OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Неправильный язык | Искаженность слов, особенно для неанглийского текста | Установите `ocrEngine.Language = Language.Spanish` (или соответствующий) перед `Recognize()` |
| Недостаток памяти при больших файлах | `OutOfMemoryException` | Обрабатывайте страницы пакетами: перебирайте `ocrEngine.Image.Pages` и вызывайте `RecognizePage(i)` |
| Лицензия не применена | Водяной знак “Evaluation” в выводе | Зарегистрируйте лицензию: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Полный рабочий пример (готовый к копированию)

Ниже представлен полный код программы, который можно сразу вставить в новый консольный проект. Он включает все обсуждённые части — инициализацию, загрузку, распознавание и сохранение.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet run` и наблюдайте, как консоль сообщает, где находятся JSON и XML. Всё — вы только что завершили **ocr engine example**, который извлекает текст из TIFF.

---

## Следующие шаги и связанные темы

- **Пакетная обработка:** Оберните вышеописанную логику в цикл `foreach`, чтобы автоматически обрабатывать десятки TIFF‑файлов.  
- **Интеграция с поиском:** Передайте JSON в Elasticsearch или Azure Cognitive Search для полнотекстового поиска по отсканированным документам.  
- **Предобработка изображений:** Исследуйте API `ImageProcessing` от Aspose для исправления наклона, удаления шумов или регулировки контраста перед OCR.  
- **Альтернативный вывод:** Используйте `ocrResult.ToPlainText()`, если нужны только чистые строки без метаданных.  

Если вам интересны другие форматы изображений, тот же шаблон работает и для PDF (просто замените исходный файл) или PNG. Главное, что после настройки движка всё становится повторяемым конвейером.

---

## Заключение

Мы прошли через **полный пример OCR‑движка**, который позволяет **извлекать текст из TIFF** файлов с помощью Aspose OCR, выводя чистый JSON и опциональный XML для любой последующей обработки. Код автономный, объяснения раскрывают «почему» каждого шага.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}