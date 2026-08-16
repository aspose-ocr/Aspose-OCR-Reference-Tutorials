---
category: general
date: 2026-03-29
description: Как использовать OCR с Aspose для извлечения текста из PNG‑файлов и преобразования
  изображений в текст. Узнайте пошаговое асинхронное OCR на C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: ru
og_description: Как использовать OCR с Aspose в C# для извлечения текста из PNG‑файлов.
  Это руководство проведёт вас через асинхронный OCR, код и советы.
og_title: Как использовать OCR в C# – извлекать текст из PNG‑изображений
tags:
- OCR
- C#
- Aspose
title: Как использовать OCR в C# – быстро извлекать текст из PNG‑изображений
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Быстро извлекать текст из PNG‑изображений

Когда‑нибудь задавались вопросом **как использовать OCR**, чтобы извлечь текст из нескольких PNG‑скриншотов? Возможно, у вас есть отсканированные чеки, счета или макеты интерфейса, и вам нужен этот текст в поисковом формате. Хорошая новость? С Aspose.OCR вы можете преобразовать изображения в текст всего за несколько строк асинхронного кода на C#.  

В этом руководстве мы покажем, как именно извлекать текст из PNG‑файлов, объясним, почему каждый шаг важен, и предоставим готовую к запуску программу, которая выводит распознанный текст для каждой страницы. К концу вы сможете **извлекать текст из изображений** без необходимости копаться в документации.

## Что вы узнаете

- Установить и подключить пакет NuGet Aspose.OCR.  
- Инициализировать OCR‑движок и задать язык (в этом примере английский).  
- Передать массив PNG‑файлов в `RecognizeImagesAsync` для быстрого, неблокирующего выполнения.  
- Пройтись по объектам `OcrResult` и вывести извлечённые строки.  

Никаких внешних сервисов, сложных обратных вызовов — только чистый, асинхронный C#, работающий на .NET 6+.

---

## Требования

| Требование | Причина |
|------------|---------|
| .NET 6 SDK (или новее) | Современные возможности языка, такие как `async Main`. |
| Visual Studio 2022 или VS Code | IDE для компиляции и запуска кода. |
| Пакет NuGet Aspose.OCR (`Aspose.OCR`) | Предоставляет класс `OcrEngine`, используемый в примере. |
| Несколько PNG‑изображений (`page1.png`, `page2.png`, …) | Входные файлы для процесса OCR. |

Если у вас уже есть .NET‑проект, просто выполните `dotnet add package Aspose.OCR`. В противном случае создайте новый консольный проект командой `dotnet new console -n OcrDemo`.

## Шаг 1: Установить Aspose.OCR и настроить проект

Сначала добавьте OCR‑библиотеку в ваш проект:

```bash
dotnet add package Aspose.OCR
```

Почему это важно: Aspose.OCR включает собственный OCR‑движок, языковые пакеты и простой API. Подключая его через NuGet, вы гарантируете совместимость версий и автоматические обновления.

## Шаг 2: Инициализировать OCR‑движок и выбрать язык

Движку необходимо знать, какой язык искать. Английский — самый распространённый, но вы можете заменить его на `Language.Spanish`, `Language.French` и т.д.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro tip:** Всегда задавайте язык явно; оставление значения по умолчанию может снизить точность и увеличить время обработки.

## Шаг 3: Подготовить список PNG‑файлов

Можно передать один файл или массив. Передача массива позволяет движку пакетно обрабатывать их асинхронно, что идеально для небольшого количества страниц.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Если ваши изображения находятся в подпапке, просто добавьте относительный путь (`"images/page1.png"`). Движок выбросит понятное исключение `FileNotFoundException`, если путь неверен — поэтому дважды проверьте имена файлов.

## Шаг 4: Запустить асинхронный OCR для всех изображений

Метод `RecognizeImagesAsync` возвращает массив `OcrResult`. Поскольку он асинхронный, ваш UI (или консоль) остаётся отзывчивым, пока OCR работает в фоне.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Почему async?**  
Если вы интегрируете OCR в веб‑API или настольное приложение, вам не нужно блокировать поток, пока движок сканирует каждый пиксель. `await` освобождает поток обратно в пул, повышая масштабируемость.

## Шаг 5: Вывести извлечённый текст для каждой страницы

Теперь, когда у нас есть результаты, пройдёмся по ним и выведем распознанный текст. Свойство `Text` содержит обычный текстовый вывод, готовый к дальнейшей обработке (например, сохранению в базе данных).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Ожидаемый вывод

Предположим, `page1.png` содержит «Invoice #12345», а `page2.png` — «Total: $89.99», вы увидите что‑то вроде:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Если OCR не найдёт ни одного символа, свойство `Text` будет пустой строкой — обработайте этот случай в продакшн‑коде, проверяя `string.IsNullOrWhiteSpace`.

## Полный рабочий пример

Ниже представлен полный код программы, который можно скопировать в `Program.cs`. Он включает все директивы `using`, асинхронный `Main` и комментарии, поясняющие каждый шаг.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Сохраните файл, разместите PNG‑файлы рядом с исполняемым файлом (или скорректируйте пути) и запустите:

```bash
dotnet run
```

Вы должны увидеть извлечённый текст, напечатанный в консоли, что подтверждает успешное **преобразование изображений в текст**.

## Обработка распространённых граничных случаев

| Ситуация | Что делать |
|----------|------------|
| **Low‑resolution PNG** | Увеличьте `ocrEngine.ImageProcessingOptions.Dpi` перед распознаванием. |
| **Multiple languages** | Установите `ocrEngine.Language = Language.English | Language.Spanish;` (побитовое ИЛИ). |
| **Large batch (hundreds of files)** | Обрабатывайте порциями (например, по 20 файлов за один вызов `RecognizeImagesAsync`), чтобы избежать всплесков памяти. |
| **Need the confidence score** | Используйте `ocrResults[i].Confidence` (число с плавающей точкой от 0 до 1) для фильтрации низкокачественных результатов. |

Эти настройки делают ваш OCR‑конвейер надёжным, особенно при переходе от демо‑версии к продакшн.

## Бонус: Сохранение результатов в текстовый файл

Если вам нужен постоянный копия вместо вывода в консоль, добавьте небольшую вспомогательную функцию:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Теперь у вас есть один файл, который **извлекает текст из изображений** для последующей обработки — идеально для индексации, поиска или передачи в языковую модель.

## Заключение

Мы прошли через **как использовать OCR** в C# с Aspose для **извлечения текста из PNG**‑файлов и **преобразования изображений в текст** эффективно. Асинхронный подход гарантирует, что приложение остаётся отзывчивым, а простой API делает код читаемым и поддерживаемым.  

Попробуйте с вашими документами, экспериментируйте с разными языками и, возможно, передавайте вывод в поисковый индекс или сервис суммирования. Возможности безграничны, когда вы надёжно превращаете картинки в поисковые строки.

### Следующие шаги и связанные темы

- **Извлекать текст из изображений** в других форматах (JPEG, TIFF) — просто измените расширения файлов.  
- **Пакетная обработка с Parallel.ForEach** для огромных объёмов.  
- **Очистка после OCR** с помощью регулярных выражений для нормализации дат, сумм или идентификаторов.  
- **Интеграция с Azure Cognitive Services**, если нужен облачный OCR с дополнительными функциями.  

Не стесняйтесь оставлять комментарии, если столкнётесь с проблемами, или делиться тем, как вы расширили этот базовый поток. Приятного кодинга!   (Image: ![Скриншот результата OCR, показывающий извлечённый текст](/images/ocr-result.png){.align-center alt="пример вывода использования OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}