---
category: general
date: 2025-12-27
description: Создайте консольный логгер на C# и включите автоматическую загрузку в
  корректные таблицы с помощью AsposeAI. Узнайте, как отобразить вывод исправленных
  таблиц за несколько шагов.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: ru
og_description: Создайте консольный логгер на C# и включите автоматическую загрузку
  в правильные таблицы с помощью AsposeAI. Следуйте этому руководству, чтобы быстро
  отобразить исправленный вывод таблицы.
og_title: Создайте консольный логгер и исправьте таблицы с помощью AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Создать консольный логгер и исправить таблицы с AsposeAI
url: /ru/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание консольного логгера и корректировка таблиц с AsposeAI

Когда‑нибудь вам нужно было **создать консольный логгер** для C# AI‑конвейера, но вы не знали, с чего начать? В этом руководстве мы пройдем весь процесс — как создать консольный логгер, включить автоматическую загрузку файлов моделей и, наконец, **как корректировать таблицы**, полученные после OCR. К концу вы сможете **отображать исправленные таблицы** в консоли, написав всего несколько строк кода.

Мы охватим всё: от начальной настройки логгера до финальной очистки, чтобы вам не пришлось искать информацию в разных документах. Предыдущий опыт работы с AsposeAI не требуется; достаточно базовых знаний C# и .NET. По пути мы добавим советы по **настройке консольного логгера**, обсудим крайние случаи и покажем, как должен выглядеть результат.

---

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть следующее:

- .NET 6.0 или новее (код использует современные возможности языка)
- Visual Studio 2022 или любой IDE, поддерживающий проекты C#
- NuGet‑пакет **Aspose.AI** установлен (`Install-Package Aspose.AI`)
- NuGet‑пакет **Aspose.OCR** установлен (`Install-Package Aspose.OCR`)
- Объект результата OCR (`ocrResult`), полученный ранее вызовом Aspose.OCR

Если чего‑то не хватает, сделайте паузу и подготовьте всё — позже вам будет благодарно.

---

## Шаг 1: Создание консольного логгера и инициализация AsposeAI

Первое, что нам нужно, — логгер, который пишет напрямую в консоль. Это упрощает отладку и дает мгновенную обратную связь, пока работает AI‑движок.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Почему это важно:**  
`ConsoleLogger` реализует интерфейс `ILogger`, поэтому любые внутренние сообщения AsposeAI (загрузка модели, статус пост‑процессора, ошибки) появляются сразу в вашем терминале. Это самый простой способ **настроить консольный логгер** без подключения внешних фреймворков логирования.

> **Совет:** Если позже понадобится логировать в файл, просто замените `ConsoleLogger` на пользовательский логгер, реализующий `ILogger` — остальной код останется без изменений.

---

## Шаг 2: Включение автоматической загрузки AI‑моделей

AsposeAI может загружать необходимые файлы моделей «на лету». Включив эту опцию, вы избавляетесь от необходимости вручную скачивать большие бинарные файлы.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Что может пойти не так?**  
Если `DirectoryModelPath` указывает на каталог только для чтения, автоматическая загрузка завершится ошибкой, и вы увидите исключение в консоли. Убедитесь, что папка существует и у приложения есть права записи.

---

## Шаг 3: Создание пост‑процессора таблиц (как корректировать таблицы)

Таблицы, извлечённые из OCR, часто бывают «мятыми» — объединённые ячейки, отсутствующие границы или смещённый текст. `TableAIProcessor` от AsposeAI может автоматически их очистить.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Почему режим AUTO?**  
`AITableDetectionMode.AUTO` позволяет движку проанализировать вывод OCR и решить, нужна ли коррекция. Если вы предпочитаете ручное управление, можно использовать `MANUAL` и вызывать `RunCorrection()` самостоятельно.

---

## Шаг 4: Привязка пост‑процессора и его конфигурации

Теперь связываем всё вместе — логгер, конфигурацию модели и процессор таблиц.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

На этом этапе AI‑движок знает, *где* хранить модели, *как* вести логирование и *какую* пост‑обработку применять. Это чистое разделение ответственности, которое упрощает будущие изменения.

---

## Шаг 5: Запуск пост‑процессора на вашем результате OCR

Предполагая, что у вас уже есть `ocrResult` от Aspose.OCR, просто передайте его движку.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Внимание к краевому случаю:**  
Если `ocrResult` не содержит таблиц, процессор тихо пропустит коррекцию. После выполнения можно проверить `tableProcessor.GetResult().Count`, чтобы убедиться, что что‑то действительно обработано.

---

## Шаг 6: Получение и **отображение исправленной таблицы**

Наконец, извлечём очищенный текст таблицы и выведем его в консоль.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

Вывод будет выглядеть примерно так (в зависимости от исходного изображения):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Если вы видите пустую строку, проверьте, действительно ли OCR обнаружил таблицу и успешно ли сработала `AllowAutoDownload`.

---

## Шаг 7: Очистка ресурсов

Хорошая практика — освобождать тяжёлые объекты, когда они больше не нужны.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Пропуск этого шага может оставить открытыми файловые дескрипторы, особенно в Windows, где файлы моделей остаются заблокированными.

---

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать в новый консольный проект. Замените `"YOUR_DIRECTORY"` реальным путём и убедитесь, что `ocrResult` заполнен перед вызовом `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Ожидаемый вывод в консоль** (при простом изображении таблицы):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Часто задаваемые вопросы

- **Нужен ли интернет для автоматической загрузки?**  
  Да. При первом запросе модели AsposeAI обращается к своему CDN. После того как файл окажется в `DirectoryModelPath`, последующие запуски работают офлайн.

- **Что делать, если в таблице объединённые ячейки?**  
  Модель AI пытается разделить их, опираясь на визуальные подсказки. Если результат выглядит неверно, попробуйте предварительно обработать изображение (повысить контраст, выровнять вращение) перед OCR.

- **Можно ли обрабатывать несколько таблиц одновременно?**  
  Конечно. `tableProcessor.GetResult()` возвращает список; просто пройдитесь по нему и выведите каждую таблицу.

- **Является ли `ConsoleLogger` потокобезопасным?**  
  Он пишет напрямую в `System.Console`, что потокобезопасно для простых записей. В сценариях с интенсивным многопоточным использованием предпочтительнее собственный логгер с синхронизацией.

---

## Следующие шаги и смежные темы

Теперь, когда вы знаете **как корректировать таблицы**, вы можете:

- **Включить автоматическую загрузку** для других моделей AsposeAI (например, переводов).
- **Настроить консольный логгер** с разными уровнями (Info, Warning, Error) для более тонкого контроля.
- Исследовать **отображение исправленных таблиц** в GUI (WinForms или WPF) вместо консоли.
- Скомбинировать коррекцию таблиц с **извлечением данных**, чтобы сразу загружать их в базу данных.

Каждый из этих пунктов опирается на основу, которую мы только что построили, так что экспериментируйте смело.

---

## Заключение

Мы прошли весь цикл: **создание консольного логгера**, включение автоматической загрузки и **корректировка таблиц** с помощью AsposeAI, завершив всё чистым способом **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}