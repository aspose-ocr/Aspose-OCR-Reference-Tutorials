---
category: general
date: 2026-04-01
description: Как преобразовать вывод OCR в JSON и XML на C# — научитесь извлекать
  текст из изображения и записывать JSON‑файл на C# с использованием Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: ru
og_description: Как преобразовать результаты OCR в структурированные файлы JSON и
  XML с помощью C#. Пошаговое руководство по извлечению текста из изображения и записи
  файла JSON на C#.
og_title: Как преобразовать OCR в JSON и XML на C# – записать JSON‑файл
tags:
- OCR
- C#
- Aspose
title: Как преобразовать OCR в JSON и XML на C# – записать JSON‑файл
url: /ru/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как преобразовать OCR в JSON и XML на C# – запись JSON‑файла

**Как преобразовать результаты OCR** в нечто, что действительно можно использовать, — вопрос, который задают многие разработчики. В этом руководстве мы покажем, как извлечь текст из изображения, превратить вывод OCR в красиво отформатированный JSON и XML, а затем записать эти файлы на диск с помощью C#.

Если вы когда‑нибудь смотрели на «сырой» OCR‑строку и думали: «Нужно лучше хранить эти данные», вы попали по адресу. К концу вы получите полностью готовую программу, которая не только **извлекает текст из файлов‑изображений**, но и умеет **записывать JSON‑файл C#** и **записывать XML‑файл C#** без лишних усилий.

## Что вам понадобится

- **.NET 6.0** или новее (код также работает с .NET Framework 4.6+).  
- NuGet‑пакет **Aspose.OCR** – установите его командой `dotnet add package Aspose.OCR`.  
- Изображение с текстом (например, `invoice.png`).  
- Любая удобная IDE – Visual Studio, Rider или VS Code подойдут.

> **Pro tip:** Храните файлы изображений в отдельной папке (например, `Resources/`), чтобы пути оставались аккуратными.

## Шаг 1: Настройка OCR‑движка – Как преобразовать OCR

Сначала создаём экземпляр `OcrEngine` и указываем, какой язык искать. В большинстве случаев достаточно английского, но вы можете заменить `Language.English` на любой поддерживаемый язык.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Почему это важно:** Инициализация движка с правильным языком существенно повышает точность, особенно для нелатинских скриптов.

## Шаг 2: Распознавание текста – Извлечение текста из изображения

Теперь передаём изображение движку. Метод `Recognize` возвращает объект `OcrResult`, содержащий исходный текст и данные о расположении.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Если изображение не найдено, `Recognize` бросает `FileNotFoundException`. Чтобы упростить демонстрацию, будем считать, что путь правильный, но в продакшене стоит обернуть вызов в блок `try‑catch`.

## Шаг 3: Преобразование результата в JSON – Запись JSON‑файла C#

Aspose.OCR упрощает сериализацию. Метод `ToJson` принимает флаг `indent` для красивого вывода, что идеально, если вы планируете открывать файл в текстовом редакторе.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Пример ожидаемого JSON

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Как извлечь текст:** Свойство `Text` возвращает обычную строку, которую можно передать в другие сервисы (поисковые индексы, базы данных и т.д.).

## Шаг 4: Сохранение JSON – Запись JSON‑файла C# (продолжение)

Получив строку JSON, просто записываем её в файл с помощью `File.WriteAllText`. По умолчанию используется кодировка UTF‑8.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Теперь рядом с изображением находится файл `invoice.json`, готовый к дальнейшей обработке.

## Шаг 5: Преобразование результата в XML – Запись XML‑файла C#

Если вам нужен XML для устаревших систем, метод `ToXml` выполнит всю работу. Как и `ToJson`, он поддерживает красивый вывод.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Пример ожидаемого XML

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Шаг 6: Сохранение XML – Запись XML‑файла C# (продолжение)

Сохранение XML идентично шагу с JSON; просто указываем расширение `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Полный рабочий пример

Объединив всё вместе, получаем полную программу, которую можно скопировать в консольное приложение:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Запустите программу, и вы найдёте два новых файла — `invoice.json` и `invoice.xml` — в указанной директории. Откройте их, чтобы убедиться, что структура соответствует приведённым выше образцам.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|--------|-------|
| **Что делать, если изображение содержит несколько языков?** | Создайте отдельные экземпляры `OcrEngine` для каждого языка или используйте `Language.Multi`, если он поддерживается. |
| **Можно ли контролировать формат вывода (например, исключить данные о регионах)?** | Да. И `ToJson`, и `ToXml` принимают необязательные параметры для фильтрации полей; см. документацию Aspose.OCR по `ExportOptions`. |
| **Как обрабатывать большие PDF‑файлы с множеством страниц?** | Обрабатывайте каждую страницу отдельно, агрегируйте результаты, а затем сериализуйте один раз. |
| **Безопасен ли вывод в UTF‑8?** | Абсолютно — Aspose.OCR работает с Unicode, а `File.WriteAllText` по умолчанию пишет в UTF‑8. |
| **Что насчёт производительности?** | OCR требует значительных ресурсов CPU. Для пакетных задач рассмотрите параллелизацию по ядрам или использование облачного API Aspose. |

## Заключение

Теперь вы знаете, **как преобразовать результаты OCR** в JSON и XML с помощью C#. Следуя описанным шагам, вы сможете **извлекать текст из изображения**, а затем **записывать JSON‑файл C#** и **записывать XML‑файл C#** всего в несколько строк кода. Этот подход быстрый, надёжный и работает с любым типом изображений, поддерживаемым Aspose.OCR.

Готовы к следующему вызову? Попробуйте интегрировать

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}