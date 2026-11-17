---
category: general
date: 2026-04-26
description: Извлекайте текст из изображения в C# с помощью Aspose.OCR и узнайте,
  как за считанные минуты преобразовать изображение в форматы JSON и XML.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: ru
og_description: Извлекайте текст из изображения в C# с помощью Aspose.OCR. Узнайте
  пошагово, как мгновенно преобразовать результат в JSON и XML.
og_title: Извлечение текста из изображения на C# – конвертация в JSON и XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Извлечение текста из изображения в C# – конвертация в JSON и XML
url: /ru/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – Конвертация в JSON и XML

Когда‑нибудь вам нужно было **извлечь текст из изображения** в проекте .NET, но вы застряли на вопросе «как же действительно получить данные?». Вы не одиноки. Во многих реальных приложениях — например, обработка счетов, сканирование чеков или проверка бейджей — извлечение символов из картинки является первым, критически важным шагом.  

Хорошая новость? С Aspose.OCR вы можете сделать это в паре строк кода, а затем мгновенно **конвертировать изображение в JSON** или **конвертировать изображение в XML** для последующих систем. В этом руководстве мы пройдемся по полностью готовому к запуску коду, объясним, почему каждый элемент важен, и покажем несколько приёмов, чтобы избежать распространённых подводных камней.

---

## Что понадобится

- **.NET 6+** (любой современный SDK подойдет; пример ориентирован на .NET 6)
- **Aspose.OCR for .NET** NuGet‑пакет  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Файл изображения (PNG, JPG и т.д.), содержащий печатный текст; в примере используется `invoice.png`.
- Редактор кода — Visual Studio, VS Code или Rider — что вам больше нравится.

Вот и всё. Никаких дополнительных OCR‑движков, внешних сервисов, только один NuGet‑пакет.

---

## Шаг 1: Настройка OCR‑движка – Как извлечь текст из изображения

Сначала мы создаём экземпляр `OcrEngine` и указываем ему файл изображения. Этот шаг — фундамент; без правильно загруженного изображения движок ничего не распознает.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Почему это важно:**  
- `OcrEngine` инкапсулирует всю низкоуровневую предобработку изображения (бинаризация, выравнивание).  
- Загрузка изображения через `ImageStream.FromFile` гарантирует, что движок читает точные байты, сохраняя DPI и глубину цвета — оба параметра могут влиять на точность распознавания.  

> **Pro tip:** Если ваши исходные изображения находятся в потоке (например, загружены через веб‑API), используйте `ImageStream.FromStream(yourStream)` вместо `FromFile`.

---

## Шаг 2: Указать язык, который ожидает движок – точное извлечение текста из изображения

Aspose.OCR поддерживает множество алфавитов. Указание правильного языка сужает набор символов и повышает точность.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Почему:**  
Когда вы задаёте `Language.Latin`, OCR‑движок игнорирует кириллические или азиатские глифы, уменьшая количество ложных срабатываний. Если позже понадобится обрабатывать многоязычные документы, можно переключиться на `Language.Multilingual` или комбинировать языки.

---

## Шаг 3: Запуск процесса распознавания – извлечение текста из изображения одним вызовом

Теперь мы действительно распознаём текст. Метод `Recognize` возвращает объект `RecognitionResult`, содержащий исходный текст, оценки уверенности и даже данные о макете.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Почему:**  
Одного вызова `Recognize` достаточно, потому что движок внутри выполняет предобработку, сегментацию и классификацию символов. Свойство `Text` даёт вам простую строку, идеальную для логирования или быстрой проверки.

---

## Шаг 4: Преобразование результата в JSON – легко конвертировать изображение в JSON

Во многих современных сервисах предпочитают JSON‑payload. Aspose.OCR предоставляет удобный метод `ToJson`, который сериализует весь `RecognitionResult`, включая значения уверенности и ограничивающие рамки.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Почему может понадобиться JSON:**  
- **Совместимость:** Front‑end приложения (React, Angular) могут напрямую потреблять JSON.  
- **Отладка:** JSON содержит уверенность для каждого символа, позволяя помечать слова с низкой уверенностью для ручной проверки.  

> **Edge case:** Если вашей последующей системе нужен только простой текст, вы можете взять `recognitionResult.Text` и обернуть его в собственный JSON‑объект вместо полного payload от Aspose.

---

## Шаг 5: Преобразование результата в XML – конвертировать изображение в XML для устаревших систем

Некоторые компании всё ещё используют XML‑схемы для обмена данными. Метод `ToXml` аналогичен `ToJson`, но выводит XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Почему XML:**  
- **Валидация по схеме:** Вы можете определить XSD, соответствующий структуре, которую генерирует Aspose, гарантируя соблюдение контракта.  
- **Интеграция:** Старые ERP‑ или системы управления документами часто умеют парсить XML «из коробки».

---

## Полный рабочий пример – единый код

Ниже представлен полный пример программы, который связывает всё вместе. Скопируйте‑вставьте его в новый консольный проект (`dotnet new console`) и запустите.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Ожидаемый вывод (консоль):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Файлы JSON и XML будут содержать более богатую структуру, например:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение размытое или повернуто?

Aspose.OCR автоматически выравнивает большинство изображений, но в экстремальных случаях может потребоваться предобработка с помощью `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Добавление небольшого повышения контраста (`ImageProcessor.AdjustContrast`) также может улучшить оценку уверенности.

### Можно ли извлекать текст из PDF?

Да — сначала преобразуйте каждую страницу PDF в изображение (например, с помощью Aspose.PDF или бесплатной библиотеки PDFium), а затем передайте полученные изображения в тот же OCR‑поток.

### Как обрабатывать несколько языков в одном документе?

Установите `ocrEngine.Language = Language.Multilingual;` или комбинируйте конкретные языки:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Имейте в виду, что более широкий набор языков может

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}