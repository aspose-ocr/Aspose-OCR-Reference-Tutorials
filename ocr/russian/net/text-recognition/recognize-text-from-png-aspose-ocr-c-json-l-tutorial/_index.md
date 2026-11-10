---
category: general
date: 2026-03-26
description: Распознавать текст из PNG и извлекать данные чека с помощью Aspose OCR
  на C#. Преобразовать изображение в JSON‑L и обработать чек с помощью OCR в полном
  примере.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: ru
og_description: распознавать текст из PNG и преобразовывать чеки в JSON‑L с помощью
  Aspose OCR на C#. Полный пошаговый код и советы.
og_title: Распознавание текста из PNG – Руководство по Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: распознавание текста из PNG – учебник Aspose OCR C# JSON‑L
url: /ru/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Распознавание текста из PNG – Полное руководство Aspose OCR C#  

Когда‑нибудь вам нужно было **распознавать текст из png** файлов, но вы не знали, какая библиотека даст чистый результат построчно? Вы не одиноки. Во многих небольших бизнес‑приложениях чек хранится как изображение PNG, и извлечение суммы, даты или названия продавца является ежедневной проблемой.  

Хорошие новости? С несколькими строками C# и библиотекой **Aspose OCR** вы можете **извлекать текст из чека**, а затем **конвертировать изображение в jsonl** для последующего анализа. В этом руководстве мы пройдем весь конвейер — загрузка PNG, запуск OCR и запись каждой строки в файл JSON‑L — чтобы вы могли сразу **обрабатывать чек с помощью OCR**.  

Мы расскажем всё, что вам нужно: необходимые пакеты NuGet, полностью готовую к запуску программу, объяснения, почему каждый шаг важен, и несколько практических советов, которые пригодятся, когда чеки становятся неразборчивыми. Внешняя документация не требуется; просто скопируйте‑вставьте, запустите и адаптируйте.  

---  

## Что вы узнаете  

- Как **распознавать текст из png** с помощью `Aspose.OCR`.  
- Как **извлекать текст из чека** из объектов строк и фиксировать оценки уверенности.  
- Как **конвертировать изображение в jsonl**, чтобы каждая строка OCR стала отдельным объектом JSON.  
- Как **обрабатывать чек с OCR** от начала до конца, учитывая крайние случаи, такие как пустые изображения или строки с низкой уверенностью.  
- Советы по устранению распространённых проблем OCR и повышению точности.  

### Предварительные требования  

- .NET 6.0 или новее (код также работает с .NET Core и .NET Framework).  
- Visual Studio 2022 или любой другой предпочитаемый IDE.  
- Действительная лицензия Aspose OCR (можно начать с бесплатной временной лицензии с Aspose.com).  
- Пример чека, сохранённый как `receipt.png` в папке, которой вы управляете.  

---  

## Шаг 1: Распознавание текста из png с помощью Aspose OCR  

Первое, что нам нужно — инициализированный `OcrEngine`. Этот объект хранит настройки OCR‑движка (язык, режим обнаружения и т.д.). По умолчанию используется английский и автоматически определяется макет страницы, что подходит для большинства чеков.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```  

**Почему это важно:**  
`OcrEngine` — это компонент, выполняющий тяжёлую работу; создание его один раз и повторное использование для множества изображений снижает нагрузку на память. Если нужен другой язык (например, испанские чеки), можно установить `ocrEngine.Language = OcrLanguage.Spanish;` перед вызовом `Recognize`.  

---  

## Шаг 2: Извлечение текста из строк чека  

`OcrResult` содержит коллекцию под названием `Lines`. Каждая строка хранит исходный текст и оценку уверенности (0‑100). Выборка этих данных даёт вам гранулированный контроль — вы можете отбрасывать строки с низкой уверенностью или помечать их для ручной проверки.  

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```  

**Почему мы экранируем JSON:**  
Текст чека может содержать кавычки (`"`) или обратные слеши (`\`), которые сломают наивную JSON‑строку. Метод `EscapeJson` гарантирует корректную JSON‑строку.  

**Как выглядит вывод:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```  

Каждая строка — отдельная запись, идеально подходящая для потоковой передачи в озеро данных или подачи в модель машинного обучения.  

---  

## Шаг 3: Конвертировать изображение в JSONL — обработка крайних случаев  

Когда вы обрабатываете пакет чеков, некоторые изображения могут быть пустыми, повреждёнными или иметь чрезвычайно низкие оценки уверенности. Сделаем конвейер более надёжным.  

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```  

**Почему фильтруем:**  
Чеки, напечатанные на выцветшей бумаге, могут давать случайные символы с низкой уверенностью. Отбрасывание всего, что ниже 80 %, обычно удаляет шум, оставляя полезные данные.  

---  

## Шаг 4: Обрабатывать чек с OCR — пример от начала до конца  

Объединив всё вместе, представляем **полную, готовую к запуску** программу. Замените `YOUR_DIRECTORY` на путь к папке, где находится ваш PNG‑файл.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```  

**Запуск кода:**  
1. Откройте терминал в папке проекта.  
2. `dotnet add package Aspose.OCR` – устанавливает библиотеку.  
3. `dotnet run` – вы должны увидеть сообщение об успехе и появление файла `receipt.jsonl`.  

**Ожидаемый результат:** Файл JSON, где каждая строка соответствует строке чека и содержит оценки уверенности. Теперь вы можете передать этот файл в Power BI, Elastic или любой аналитический инструмент, понимающий JSON‑L.  

---  

## Распространённые проблемы и профессиональные советы  

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Пустой вывод** | Неправильный путь к изображению или файл не PNG. | Проверьте путь, используйте `File.Exists(imagePath)`. |
| **Непонятные символы** | Низкое DPI или сильно сжатый PNG. | Используйте сканы минимум 300 dpi; избегайте агрессивного JPEG‑сжатия. |
| **Слишком много строк с низкой уверенностью** | Чек напечатан на термобумаге с выцветанием. | Увеличьте порог `minConfidence` или предварительно обработайте изображение (контраст/порог). |
| **Ошибки парсинга JSON** | Неэкранированные кавычки в тексте чека. | Оставьте вспомогательную функцию `EscapeJson` или переключитесь на `System.Text.Json` для надёжной сериализации. |

**Профессиональный совет:** Если нужно извлечь конкретные поля (например, общую сумму), выполните простое регулярное выражение над каждым `line.Text` после получения файла JSON‑L. Это отделяет OCR от бизнес‑логики и упрощает отладку.  

---  

## Расширение решения  

- **Пакетная обработка:** Оберните логику `Main` в `foreach` по всем PNG‑файлам в директории.  
- **Поддержка нескольких языков:** Установите `ocrEngine.Language = OcrLanguage.Spanish;` (или любой поддерживаемый язык) перед `Recognize`.  
- **Структурированный вывод:** Вместо построчного JSON построьте объект `Receipt` с полями `Date`, `Merchant`, `Total`, а затем выполните одну сериализацию.  

Все эти варианты всё равно **конвертируют изображение в jsonl** в ядре, так что вы можете менять downstream‑потребителя, не трогая часть OCR.  

---  

## Заключение  

Мы только что показали, как **распознавать текст из png** файлов с помощью Aspose OCR, **извлекать текст из чека** и **конвертировать изображение в jsonl** для лёгкой последующей обработки. Полная, автономная программа на C# демонстрирует весь рабочий процесс — от загрузки PNG, обработки крайних случаев, до записи чистого файла JSON‑L — чтобы вы могли сразу **обрабатывать чек с OCR** в своих проектах.  

Попробуйте на нескольких образцах чеков, отрегулируйте порог уверенности, и вы увидите, как быстро шумный набор изображений превращается в структурированные данные, готовые к аналитике. Когда будете уверены, исследуйте пакетную обработку или добавьте небольшую модель ML для автоматической классификации категорий расходов.  

Есть вопросы или нашли хитрый приём? Оставьте комментарий ниже — happy coding!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}