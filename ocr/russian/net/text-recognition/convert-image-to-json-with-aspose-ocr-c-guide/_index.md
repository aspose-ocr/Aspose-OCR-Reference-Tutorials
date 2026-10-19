---
category: general
date: 2026-01-15
description: Преобразуйте изображение в JSON с помощью Aspose OCR на C#. Узнайте,
  как извлекать текст из изображения, получать ограничивающие рамки в формате JSON
  и распознавать изображения чеков.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: ru
og_description: Преобразуйте изображение в JSON с помощью Aspose OCR на C#. Пошаговое
  руководство по извлечению текста из изображения, распознаванию чека и получению
  ограничивающих рамок в формате JSON.
og_title: Преобразовать изображение в JSON с помощью Aspose OCR C# Руководство
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Конвертировать изображение в JSON с помощью Aspose OCR C# Руководство
url: /ru/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображения в JSON с помощью Aspose OCR C# Руководство

Когда‑то вам нужно было **преобразовать изображение в JSON**, но вы не знали, какая библиотека может предоставить как необработанный текст, так и точные координаты слов? Вы не одиноки. Многие разработчики сталкиваются с этой проблемой, пытаясь извлечь текст из файлов изображений — особенно чеков — и одновременно получить машинно‑читаемую JSON‑нагрузку для дальнейшей обработки.

В этом руководстве мы пройдем полный **пример Aspose OCR C#**, который покажет, как извлечь текст из изображения, распознать чек и вывести **JSON‑ограничивающие рамки** для каждого слова. К концу вы получите готовое консольное приложение, которое печатает красиво отформатированную строку JSON, которую можно передать в любой API, базу данных или аналитический конвейер.

> **Что вы получите**  
> • Полнофункциональный проект C#, который **преобразует изображение в JSON**  
> • Понимание, почему мы включаем `IncludeBoundingBoxes` (это ключ к `json bounding boxes`)  
> • Советы по работе с различными форматами изображений и языками  

Начнём.

---

## Что вам понадобится

Прежде чем погрузиться в код, убедитесь, что у вас установлены следующие предварительные требования:

- **.NET 6.0 SDK** (или более поздняя версия) — код нацелен на .NET 6, но также работает на .NET Framework 4.7+ .  
- **Aspose.OCR for .NET** пакет NuGet — его можно добавить командой `dotnet add package Aspose.OCR`.  
- Пример изображения чека (`receipt.jpg`), размещённый в папке, к которой ваш проект может обратиться.  
- Visual Studio 2022, VS Code или любая другая IDE по вашему выбору.

Никаких внешних сервисов не требуется; всё работает локально.

---

## Преобразование изображения в JSON — Обзор

Суть проста: загрузить изображение, указать Aspose OCR распознавать английский (или любой поддерживаемый язык), включить ограничивающие рамки и запросить результат в формате **JSON**. Библиотека выполняет всю тяжёлую работу — OCR, анализ макета и сериализацию в JSON.

Ниже схематическое представление потока (представьте небольшую картинку):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Эта небольшая схема охватывает весь конвейер, который мы реализуем.

---

## Шаг 1: Создание проекта и установка Aspose OCR

Сначала создайте новый консольный проект и подключите пакет Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Совет:** Если вы используете Visual Studio, щёлкните правой кнопкой мыши по проекту → *Manage NuGet Packages* → найдите **Aspose.OCR** и установите последнюю стабильную версию (на данный момент — 23.12).

---

## Шаг 2: Загрузка изображения для распознавания

Мы будем использовать метод `OcrImage.FromFile` для чтения изображения чека. Убедитесь, что путь указывает на реальный файл; иначе вы получите `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Если ваше изображение находится рядом с файлом `.csproj`, можно просто указать `"receipt.jpg"`.

---

## Шаг 3: Настройка параметров OCR для JSON‑ограничивающих рамок

Магия происходит, когда мы включаем `OutputFormat = OutputFormat.Json` **и** `IncludeBoundingBoxes = true`. Первое заставляет Aspose сериализовать результат в JSON, а второе добавляет `x`, `y`, `width` и `height` для каждого слова — именно то, что нужно для `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Также можно изменить `ocrOptions.Dpi` или `ocrOptions.Language`, если требуется более высокое разрешение или другой язык.

---

## Шаг 4: Выполнение распознавания — Извлечение текста из изображения

Теперь вызываем `Recognize`. Метод возвращает объект `OcrResult`, содержащий строку JSON, необработанный текст и прочее.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Если нужно работать с другими языками, замените `Language.English` на `Language.Spanish`, `Language.French` и т.д. Aspose поддерживает более 30 языков «из коробки».

---

## Шаг 5: Вывод результата — Ваш JSON‑payload

Наконец, выводим JSON в консоль. В реальном приложении, скорее всего, вы запишете его в файл или отправите в сервис.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Запуск программы должен вывести JSON‑документ, похожий на фрагмент ниже.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Обратите внимание, что каждому слову теперь сопоставлена **JSON‑ограничивающая рамка** — идеально для наложения в UI или дальнейшего парсинга.

---

## Полный рабочий пример

Ниже полностью готовая к копированию программа. Никаких скрытых частей, никаких внешних вызовов — чистый C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Обратите внимание:**  
> • **Ошибки пути к файлу** — проверьте расположение изображения.  
> • **Отсутствующий пакет NuGet** — убедитесь, что `Aspose.OCR` подключён.  
> • **Неподдерживаемые форматы изображений** — используйте JPEG, PNG, BMP или TIFF для наилучших результатов.

---

## Часто задаваемые вопросы и особые случаи

### Можно ли преобразовать **страницу PDF** в JSON вместо JPEG?

Да. Сначала преобразуйте страницу PDF в изображение (например, с помощью `Aspose.PDF`), а затем передайте полученное изображение в тот же OCR‑конвейер. Вывод JSON будет идентичным, поскольку шаг OCR работает только с растровыми данными.

### Что делать, если чек размытый?

Увеличьте DPI в `ocrOptions`. Например:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Большее DPI может увеличить потребление памяти, поэтому находите баланс между качеством и производительностью.

### Нужно распознавать **несколько языков** в одном чеке (например, английский + испанский).

Можно передать массив языков:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose попытается распознать каждый язык в указанном порядке.

### Как записать JSON в файл?

Достаточно заменить строку `Console.WriteLine` на:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Теперь у вас будет постоянный файл, который можно передать другим сервисам.

---

## Визуальное резюме

![convert image to json example](convert-image-to-json.png "convert image to json example")

*Скриншот показывает вывод консоли с JSON‑payload после запуска демонстрации.*

---

## Заключение

Мы только что показали, как **преобразовать изображение в JSON** с помощью Aspose OCR в C#. Настроив `OutputFormat` и `IncludeBoundingBoxes`, вы можете **извлекать текст из изображения**, **распознавать чек** и получать точные **JSON‑ограничивающие рамки** для каждого слова. Полный, готовый к запуску код находится в сниппете выше, так что вы можете сразу вставить его в любой .NET‑проект.

Что дальше? Попробуйте передать JSON в фронтенд‑просмотрщик, который подсвечивает каждое слово, или отправьте данные в модель машинного обучения, классифицирующую позиции в чеке. Можно также поэкспериментировать с другими языками, более высоким DPI или пакетной обработкой множества изображений в цикле.

Если возникнут трудности, помните о советах по путям к файлам, DPI и массивам языков. Оставляйте комментарии или открывайте issue в репозитории GitHub, который создадите для этой демо‑версии. Приятного кодинга и удачного превращения картинок в структурированный JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}