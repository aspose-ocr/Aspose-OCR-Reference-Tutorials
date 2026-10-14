---
category: general
date: 2026-02-09
description: Как использовать OCR в C# для распознавания текста на изображении, извлечения
  текста и преобразования изображения в текст с помощью Aspose OCR. Полное пошаговое
  руководство.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: ru
og_description: Как использовать OCR в C# для распознавания текста с изображения,
  извлечения текста и преобразования изображения в текст с помощью Aspose OCR. Полное
  руководство с кодом.
og_title: Как использовать OCR в C# – Распознавание текста на изображениях
tags:
- C#
- Aspose OCR
- Image Processing
title: Как использовать OCR в C# – распознавать текст с изображений
url: /ru/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Распознавание текста на изображениях

Когда‑нибудь задавались вопросом **как использовать OCR**, чтобы превратить скриншот в редактируемый текст? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда им нужно *распознавать текст на изображении* файлов, но нет понятного готового примера.  

В этом руководстве мы пройдем весь процесс — загрузка лицензии, создание движка, передача потока изображения и, наконец, извлечение обычного текста. К концу вы сможете **извлекать текст из изображения**, **преобразовывать изображение в текст**, а также понять нюансы работы с **загрузкой потока изображения**.

> **Что вы получите:** полностью готовую к запуску программу на C# с использованием Aspose.OCR, объяснения каждого шага и советы, как избежать распространённых ошибок.

---

## Требования

- .NET 6.0 или новее (API также работает с .NET Framework 4.6+)  
- NuGet‑пакет Aspose.OCR для .NET (`Aspose.OCR`) установлен  
- Действительный файл лицензии Aspose OCR (`Aspose.OCR.lic`) — бесплатная пробная версия работает, но добавляет водяной знак.  
- Изображение (`sample.jpg`) с чётким, машинно‑читаемым текстом.

> **Подсказка:** Если вы работаете в Visual Studio, команда для консоли NuGet выглядит так  
> `Install-Package Aspose.OCR -Version 23.10` (замените на последнюю версию).

---

## Как использовать OCR: загрузить лицензию и инициализировать движок

Первое, что нужно сделать — сообщить Aspose, что у вас есть лицензия. Пропуск этого шага позволит программе запуститься, но в выводе появится водяной знак, и вы потратите лишнее время на проверки режима пробной версии.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**Почему это важно:** объект `License` отключает водяной знак пробной версии и открывает полный набор функций, включая более точные модели и поддержку нескольких языков.  

> **Pro tip:** Храните файл лицензии вне репозитория исходного кода. Используйте переменные окружения или защищённое хранилище для передачи пути к файлу во время выполнения.

---

## Шаг 2 – Загрузить поток изображения (и почему это лучше, чем путь к файлу)

Когда вы *загружаете поток изображения* вместо передачи обычного пути к файлу, вы получаете гибкость: изображение может поступать из базы данных, веб‑запроса или массивa байтов в памяти.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**Объяснение:** `ImageStream` абстрагирует источник, позволяя OCR‑движку обрабатывать всё одинаково. Если позже вы переключитесь на облачное хранилище, вам нужно будет изменить только способ создания `ImageStream`; остальной код останется без изменений.

---

## Шаг 3 – Распознать текст на изображении

Теперь переходим к главному: **распознавать текст на изображении**. Метод `OcrEngine.Recognize` запускает нейронные модели, поставляемые с Aspose, и возвращает объект `OcrResult`, содержащий несколько полезных свойств.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**Что находится в `OcrResult`?**  
- `PlainText` — одна строка со всеми обнаруженными символами.  
- `Words` — коллекция объектов слов с ограничивающими рамками (полезно для подсветки).  
- `Lines` — группировка по строкам, удобна для сохранения разрывов абзацев.

Если вам нужен только «сырой» текст, `PlainText` — самый быстрый путь. Для более продвинутых сценариев (например, наложения результатов на оригинальное изображение) изучите `Words` и `Lines`.

---

## Шаг 4 – Вывести или сохранить извлечённый текст

Наконец, выведем распознанный текст в консоль. В реальном приложении вы можете записать его в базу данных, файл или отправить через API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**Ожидаемый вывод:**  
Если `sample.jpg` содержит предложение *«Hello World!»*, вы увидите:

```
=== OCR Output ===
Hello World!
==================
```

При использовании пробной лицензии в выводе будет небольшая водяная метка «Aspose OCR Demo» в конце текста. С полной лицензией она исчезает полностью.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, готовый к компиляции. Замените пути на свои собственные и вы готовы к работе.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **Помните:** код выше **извлекает текст из изображения** и **преобразует изображение в текст** одним вызовом. Никаких лишних циклов, без ручной обработки пикселей — Aspose делает всю тяжёлую работу.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение размытое или с низким контрастом?

Aspose OCR включает параметры предобработки (например, `ocrEngine.ImagePreprocessor`). Вы можете включить бинаризацию или выравнивание перед распознаванием:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### Как обрабатывать несколько языков?

Установите свойство `Language` у движка:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Движок попытается автоматически определить оба языка.

### Можно ли обрабатывать PDF вместо JPEG?

Да — Aspose OCR умеет читать PDF напрямую, но для извлечения каждой страницы в виде изображения понадобится библиотека Aspose.PDF, после чего полученный поток изображения передаётся в OCR‑движок.

### Что делать с большими пакетами?

Обёрните логику распознавания в цикл и переиспользуйте один экземпляр `OcrEngine`. Создание нового движка для каждого изображения добавляет лишние накладные расходы.

---

## Pro Tips для OCR в продакшене

- **Кешировать объект лицензии**: загрузите его один раз при старте приложения, а не при каждом запросе.  
- **Переиспользовать `OcrEngine`**: движок хранит внутренние буферы; переиспользование снижает нагрузку на сборщик мусора.  
- **Ограничить размер изображения**: очень большие изображения (>5 МП) резко увеличивают время обработки. При необходимости уменьшайте до 150‑300 DPI.  
- **Проверять качество вывода**: OCR не идеален; реализуйте простую проверку уверенности (`ocrResult.Words.Average(w => w.Confidence)`) и помечайте результаты с низкой уверенностью для ручной проверки.  
- **Потокобезопасность**: `OcrEngine` не является потокобезопасным. Создавайте отдельные экземпляры для каждого потока или используйте паттерн пула.

---

## Заключение

Мы рассмотрели **как использовать OCR** в C# от загрузки лицензии до извлечения чистого, пригодного для поиска текста. Следуя описанным шагам, вы сможете **распознавать текст на изображении**, **извлекать текст из изображения** и без труда **преобразовывать изображение в текст**, освоив при этом паттерн **загрузки потока изображения**, который делает ваш код гибким для будущих источников данных.

Готовы к следующему вызову? Попробуйте добавить обрезку области интереса, интегрировать с Azure Blob Storage или передать результат OCR в конвейер обработки естественного языка. Возможности безграничны, а у вас теперь есть надёжная база для дальнейшего развития.

![Схема потока OCR: загрузить лицензию → создать движок → загрузить поток изображения → распознать → вывести текст](image-placeholder.png "как использовать OCR для распознавания текста на изображении")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}