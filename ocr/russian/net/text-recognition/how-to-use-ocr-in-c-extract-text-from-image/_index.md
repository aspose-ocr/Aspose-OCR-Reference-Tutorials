---
category: general
date: 2026-03-05
description: Как использовать OCR в C# для извлечения текста из изображения. Узнайте,
  как преобразовать изображение в текст, читать корейские символы и быстро загружать
  изображение для OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: ru
og_description: Как использовать OCR в C# и мгновенно извлекать текст из изображения.
  Это руководство показывает, как преобразовать изображение в текст, читать корейские
  символы и загружать изображение для OCR.
og_title: Как использовать OCR в C# – извлечение текста из изображения
tags:
- OCR
- C#
- Aspose
title: Как использовать OCR в C# – извлечь текст из изображения
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – извлечение текста из изображения

Когда‑нибудь задавались вопросом **how to use OCR**, когда у вас есть скриншот, полностью заполненный корейским текстом, и вам нужна обычная строка? Вы не единственный, кто ломает голову над этим. В этом руководстве мы пройдем полный, готовый к запуску пример, который **extracts text from image**, **converts image to text**, и даже покажет, как **read Korean characters** с помощью Aspose.OCR.

Мы также рассмотрим часто упускаемый шаг **loading image for OCR**, чтобы вы не столкнулись с неожиданным «file not found» позже. К концу у вас будет автономная программа, которую можно добавить в любой проект .NET.

## Что понадобится

- .NET 6+ (или .NET Framework 4.7.2 и новее) – код работает в обеих средах.
- Aspose.OCR for .NET – вы можете получить бесплатную пробную версию с сайта Aspose.
- Пример изображения (`korean_doc.png`), содержащий корейский текст.
- Ваш любимый IDE (Visual Studio, Rider, VS Code – что угодно).

Никакие другие сторонние библиотеки не требуются.

## Шаг 1: Настройка проекта и добавление Aspose.OCR

Сначала создайте новое консольное приложение:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Затем добавьте пакет Aspose.OCR через NuGet:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если у вас есть файл лицензии, разместите его в корне проекта; иначе бесплатная пробная версия будет работать, но добавит водяной знак к результату.

## Шаг 2: Как использовать OCR – инициализация движка

Теперь мы напишем код на C#. Первое, что нужно сделать при **how to use OCR**, — создать экземпляр `OcrEngine`. Этот объект является ядром библиотеки; он хранит все настройки, которые понадобятся позже.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Why this matters:** Без корректного экземпляра движка вы не сможете задать язык, загрузить изображения или получить результаты. Движок также управляет внутренними ресурсами, поэтому создание его один раз и повторное использование эффективнее, чем многократное создание новых объектов.

## Шаг 3: Выбор языка – чтение корейских символов

Следующая строка указывает движку, какой язык искать. Поскольку наша цель — **read Korean characters**, мы устанавливаем `OcrLanguage.Korean`. Вы можете заменить его на Arabic, Thai, Gujarati и т.д., в зависимости от вашего случая.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Why it’s important:** Выбор языка значительно повышает точность. OCR‑движок использует словари и модели символов, специфичные для языка; передача ему неправильного языка может привести к искажённому выводу.

## Шаг 4: Загрузка изображения для OCR – преобразование изображения в текст

Прежде чем движок сможет что‑то сделать, вам необходимо **load image for OCR**. Метод `ImageStream.FromFile` читает файл в формат, понятный движку.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Если изображение находится в другой папке, просто скорректируйте путь. Не забудьте установить для файла *Build Action* значение «Copy if newer», чтобы исполняемый файл мог найти его во время выполнения.

> **Common pitfall:** Указание пути с обратными слешами (`\`) в строковом литерале без экранирования вызовет ошибку компиляции. Используйте либо двойные обратные слеши (`\\`), либо дословную строку (`@"C:\path\file.png"`).

## Шаг 5: Выполнение OCR – извлечение текста из изображения

Теперь происходит основная работа. Вызов `Recognize()` запускает OCR‑алгоритм, а свойство `Text` возвращает необработанную строку.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

На этом этапе вы **extracted text from image** и фактически **converted image to text**. Результат может содержать символы новой строки, если исходный макет имел разрывы строк.

## Шаг 6: Показ результата – проверка вывода

Наконец, выведем результат в консоль, чтобы вы могли убедиться, что всё сработало.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### Expected Output

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Если вы видите корейские символы, похожие на изображение, поздравляем — вы освоили **how to use OCR** с Aspose.OCR!

![how to use OCR example diagram](image.png)

*Image alt text: диаграмма примера how to use OCR, показывающая поток от загрузки изображения до вывода распознанного текста.*

## Особые случаи и варианты

### 1. Обработка нескольких страниц

Если вам нужно **extract text from image** файлы, содержащие несколько страниц (например, многостраничный TIFF), выполните цикл по каждой странице и вызовите `Recognize()` для каждого экземпляра `ImageStream`.

### 2. Работа с низкокачественными сканами

Low‑resolution images can hurt accuracy. Before calling `Recognize()`, you can improve the image with Aspose’s preprocessing tools:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Переключение языков на лету

Suppose you have a mixed‑language document. You can change `ocrEngine.Language` between recognitions:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Сохранение результата в файл

If you prefer to **convert image to text** and store it, just write the string to a `.txt` file:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Часто задаваемые вопросы

- **Нужна ли лицензия для запуска этого кода?**  
  Нет. Бесплатная пробная версия подходит для экспериментов, но добавляет водяной знак к результату. Приобретённая лицензия удаляет водяной знак и открывает полную производительность.

- **Можно ли использовать это на Linux?**  
  Конечно. Aspose.OCR кроссплатформенный; просто убедитесь, что у вас установлены необходимые нативные зависимости (libgdiplus для .NET Core на Linux).

- **Что если мое изображение находится в потоке, а не в файле?**  
  Use `ImageStream.FromStream(yourStream)` – the API accepts any `System.IO.Stream`.

## Заключение

Мы пошагово провели вас через **how to use OCR** в C# для **extract text from image**, **convert image to text** и **read Korean characters**, при этом правильно **loading image for OCR**. Полный, готовый к запуску пример выше должен работать сразу, а дополнительные советы дают вам план для более сложных сценариев.

Готовы к следующему вызову? Попробуйте заменить язык, обрабатывать PDF‑файлы постранично или интегрировать вызов OCR в веб‑API, чтобы пользователи могли загружать изображения и получать мгновенный текстовый результат. Возможностей бесконечно, и теперь у вас есть прочная основа для дальнейшего развития.

Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}