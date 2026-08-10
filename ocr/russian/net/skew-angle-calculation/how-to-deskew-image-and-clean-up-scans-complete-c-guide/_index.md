---
category: general
date: 2026-03-18
description: Как исправить наклон изображения и уменьшить шум в отсканированных файлах.
  Узнайте, как загрузить изображение из файла, извлечь текст из TIFF и распознать
  текст с изображения с помощью Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: ru
og_description: Как быстро исправить наклон изображения с помощью Aspose OCR. Это
  руководство покажет, как уменьшить шум, загрузить изображение из файла и извлечь
  текст из TIFF в C#.
og_title: Как выпрямить изображение – Полный учебник OCR на C#
tags:
- OCR
- C#
- Image Processing
title: Как выпрямить изображение и очистить сканы – Полное руководство по C#
url: /ru/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения – Полный учебник по OCR на C# 

Задумывались ли вы когда‑нибудь **как исправить наклон изображения** файлов, которые выглядят так, будто их сняли с шаткого сканера? Вы не одиноки. Большинство разработчиков сталкиваются с этой проблемой, когда исходный TIFF слегка перекошен, и результаты OCR получаются в беспорядке. Хорошая новость? Пара строк кода на C# позволяет выпрямить изображение, избавиться от зернистого фона и извлечь чистый, индексируемый текст прямо из файла.

В этом руководстве мы пройдемся по **как уменьшить шум**, **загрузить изображение из файла**, и, наконец, **распознать текст с изображения** с использованием Aspose OCR. К концу вы сможете **извлекать текст из tiff** документов без усилий.

> **Pro tip:** Если вы уже используете Aspose OCR в других проектах, вы можете добавить эти фильтры без дополнительных проблем с лицензированием.

---

## Что вам понадобится

- .NET 6 или новее (код также работает на .NET Core)  
- Пакет NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Отсканированный TIFF, слегка повернутый или шумный (мы будем использовать `skewed_scanned_doc.tif` в качестве примера)  
- Текстовый редактор или IDE (Visual Studio, VS Code, Rider — выбирайте по вкусу)

Дополнительные библиотеки не требуются; фильтры, которые мы будем использовать, встроены в Aspose OCR.

---

## Шаг 1 – Создать OCR‑движок (Как исправить наклон изображения)

Первое, что вы делаете, — создаёте `OcrEngine`. Считайте его мозгом, который позже будет считывать символы за вас.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Зачем создавать движок заранее? Это дает вам единое место для подключения фильтров предобработки, языковых пакетов и параметров вывода. Если пропустить этот шаг и вызвать `OcrEngine.Recognize` напрямую, вы упустите возможность предварительно очистить изображение, а именно в этом заключается необходимость исправления наклона.

---

## Шаг 2 – Добавить фильтры исправления наклона и уменьшения шума (Как уменьшить шум)

Now we attach two filters:

| Фильтр | Что делает | Почему важно |
|--------|------------|--------------|
| `AutoDeskewFilter` | Обнаруживает и исправляет вращение | Выравнивает строки текста, чтобы OCR‑движок мог их правильно читать |
| `NoiseReductionFilterV2` | Удаляет пятна и зернистый фон | Чистые пиксели означают меньше ошибок распознавания |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Вы можете заменить `NoiseReductionFilterV2` на более старую версию, но алгоритм v2 лучше справляется с современными сканерами. Если ваш документ уже полностью ровный, фильтр исправления наклона просто пропустит изображение без изменений — вреда не будет.

---

## Шаг 3 – Загрузить изображение из файла (Load Image from File)

Aspose предоставляет удобный вспомогательный метод `ImageStream.FromFile`, который читает различные форматы, включая TIFF, JPEG, PNG и BMP. Вот как мы загружаем файл в память:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Замените `YOUR_DIRECTORY` на фактический путь на вашем компьютере. Если вы используете относительный путь, убедитесь, что файл находится рядом с исполняемым файлом или задайте рабочий каталог соответствующим образом.

---

## Шаг 4 – Запустить OCR на предобработанном изображении (Recognize Text from Image)

С установленными фильтрами и загруженным изображением мы наконец просим Aspose прочитать символы:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Внутри движок запускает алгоритм исправления наклона, сглаживает шум, а затем использует распознаватель на основе нейронной сети. Результат упакован в объект `OcrResult`, который предоставляет необработанный текст, оценки уверенности и даже ограничивающие рамки, если они понадобятся позже.

---

## Шаг 5 – Отобразить или сохранить извлечённый текст (Extract Text from TIFF)

Для быстрой демонстрации мы просто выводим текст в консоль, но вы можете записать его в файл, базу данных или передать в последующий процесс.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ожидаемый вывод** (пример, будет отличаться в зависимости от вашего документа):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Если вывод всё ещё содержит искажённые символы, проверьте, что исходный TIFF не имеет слишком низкое разрешение (рекомендуется минимум 300 dpi) и что язык установлен правильно в `ocrEngine.Settings.Language`.

---

## Полный рабочий пример (Все шаги в одном месте)

Ниже представлен полный код программы, который вы можете скопировать и вставить в новый консольный проект и сразу запустить.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet run`, и вы увидите очищенный текст в вашем терминале.

---

## Часто задаваемые вопросы и особые случаи

### Что если мой TIFF содержит несколько страниц?

Aspose OCR может обрабатывать многостраничные изображения, перебирая `image.GetPages()` (или используя `image.Pages`). Каждая страница возвращает свой `OcrResult`. Объедините их с помощью `StringBuilder`, если нужен один общий текст.

### Работает ли фильтр исправления наклона с сильно повернутыми изображениями?

Он справляется с вращением до примерно ±15°. При большем угле может потребоваться предварительно повернуть изображение вручную с помощью графической библиотеки (например, `System.Drawing` или `SkiaSharp`) перед передачей в Aspose.

### Как улучшить точность для текста не на английском?

Установите язык явно:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Вы также можете загрузить пользовательские языковые пакеты, если встроенные не покрывают ваш алфавит.

### Можно ли запускать это на Linux?

Конечно. Aspose OCR кроссплатформенный; просто убедитесь, что нативные зависимости присутствуют (обычно их нет для чистой .NET версии). Используйте `dotnet publish -r linux-x64` для создания автономного бинарника.

---

## Бонус: визуализация исправленного изображения

Если вы хотите увидеть исправленное изображение перед OCR, вы можете сохранить его обратно на диск:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![пример исправления наклона изображения](https://example.com/deskew-demo.png "пример исправления наклона изображения")

*Текст alt изображения:* **пример исправления наклона изображения** — показывает до/после вращённого TIFF, исправленного AutoDeskewFilter.

---

## Заключение

Мы рассмотрели **как исправить наклон изображения** файлов, **как уменьшить шум**, а также весь конвейер для **распознавания текста с изображения**, **загрузки изображения из файла** и **извлечения текста из tiff** с помощью Aspose OCR на C#. Главный вывод? Добавление всего двух фильтров предобработки может превратить дрожащий, зернистый скан в чёткий, индексируемый документ без каких‑либо внешних инструментов.

Готовы к следующему шагу? Попробуйте заменить `AutoDeskewFilter` на `AutoRotateFilter`, если ваши документы перевёрнуты, или поэкспериментировать с `ContrastEnhancementFilter` для выцветших отпечатков. Та же схема — движок → фильтры → загрузка → распознавание — применима ко всем сценариям Aspose OCR, так что вы можете переиспользовать этот каркас для PDF, PNG или даже фотографий с камеры.

Удачной разработки, и пусть ваш OCR всегда будет точным!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}