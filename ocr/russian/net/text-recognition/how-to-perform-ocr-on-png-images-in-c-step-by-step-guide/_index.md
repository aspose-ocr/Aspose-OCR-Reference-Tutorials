---
category: general
date: 2026-03-29
description: Как выполнять OCR в C# и читать текст из PNG‑файлов. Узнайте, как извлекать
  русский текст, читать текст из PNG и как извлекать текст с помощью Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: ru
og_description: Как выполнить OCR в C# с помощью Aspose OCR. Это руководство показывает,
  как читать текст из PNG, извлекать русский текст и реализовать полное решение OCR
  на C#.
og_title: Как выполнить OCR в C# – Полное извлечение текста из PNG
tags:
- OCR
- C#
- Aspose
title: Как выполнить OCR для PNG‑изображений в C# – пошаговое руководство
url: /ru/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на PNG‑изображениях в C# – Полный учебник

Когда‑нибудь вам нужно было **выполнять OCR** на скриншоте или отсканированном документе, но вы не знали, с чего начать в C#? Вы не одиноки. Разработчики постоянно спрашивают: «Как прочитать текст из PNG‑файлов без отправки их во внешнюю службу?» Хорошая новость в том, что с Aspose.OCR вы можете **извлекать русский текст**, **читать текст из PNG**, и получить чистую строку всего за несколько строк кода.

В этом учебнике мы пройдем всё, что вам нужно: настройку библиотеки, выбор правильной языковой модели, запуск распознавания и обработку распространённых подводных камней. К концу вы сможете **как извлечь текст** из любого PNG‑изображения, будь то английский, русский или любой из более чем 70 языков, поддерживаемых Aspose. Без лишних слов, только практический, готовый к запуску пример, который вы можете сразу добавить в консольное приложение.

---

## Что вы узнаете

- Установить и добавить ссылку на пакет Aspose.OCR NuGet.
- Инициализировать OCR‑движок в его режиме авто‑загрузки по умолчанию.
- Настроить движок для **извлекать русский текст** с использованием кириллической языковой модели.
- Запустить OCR на локальном PNG‑файле и отобразить результат.
- Советы по устранению проблем с отсутствующими языковыми файлами и повышению точности.

**Prerequisites**: .NET 6+ (или .NET Framework 4.7.2+), Visual Studio 2022 или VS Code, и подключение к интернету для первого запуска (языковая модель загружается автоматически).

## Шаг 1 – Установить пакет Aspose.OCR

Чтобы начать, добавьте библиотеку Aspose.OCR в ваш проект. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Или, если вы предпочитаете интерфейс Visual Studio, щёлкните правой кнопкой мыши **Dependencies → Manage NuGet Packages**, найдите **Aspose.OCR** и нажмите **Install**.

> **Pro tip**: Пакет занимает всего несколько мегабайт, а языковые модели загружаются по запросу, поэтому вы не будете раздувать приложение ненужными файлами.

## Шаг 2 – Инициализировать OCR‑движок (Primary Keyword in Action)

Создание движка простое. Конструктор автоматически включает *auto‑download mode*, что означает, что при первом запросе языка, отсутствующего локально, Aspose загрузит его для вас.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Why this matters**: Используя режим авто‑загрузки по умолчанию, вы избегаете ручного управления файлами. Если позже понадобится **читать текст из PNG** на другом языке, просто измените `Language.RussianCyrillic` на соответствующее значение перечисления.

## Шаг 3 – Подготовьте ваше PNG‑изображение

Убедитесь, что изображение, которое вы хотите обработать, доступно во время выполнения. Поместите `sample_russian.png` в ту же папку, что и скомпилированный `.exe`, или используйте абсолютный путь, если хотите. Изображение должно быть чётким сканом или скриншотом; точность OCR резко падает на размытых или сильно сжатых PNG‑файлах.

**Common edge case**: Если PNG содержит несколько языков, вы можете установить `ocrEngine.Language = Language.Multilingual;`, чтобы движок автоматически определял каждый блок.

## Шаг 4 – Запустите приложение и проверьте вывод

Скомпилируйте и запустите программу:

```bash
dotnet run
```

Вы должны увидеть извлечённый русский текст, выведенный в консоль, примерно так:

```
Привет, мир! Это пример текста на русском языке.
```

Если вы получаете пустую строку, проверьте:

1. Путь к файлу правильный.
2. Изображение не полностью белое и не полностью чёрное.
3. Языковая модель успешно загружена (ищите папку `Aspose.OCR` в вашем профиле пользователя).

## Шаг 5 – Расширенные настройки для повышения точности

Хотя настройки по умолчанию работают в большинстве случаев, вы можете захотеть точно настроить движок:

| Setting | Что делает | Когда использовать |
|---------|------------|---------------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | Исправляет небольшое вращение | Сканированные документы, которые не идеально выровнены |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | Фильтрует фоновые пятна | Низкокачественные PNG‑файлы с мобильных камер |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | Ограничивает символы цифрами | Извлечение чисел из счетов-фактур |

Добавьте любой из этих параметров перед вызовом `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

## Шаг 6 – Экспорт результатов в файл (опционально)

Если вам нужно **как извлечь текст** в файл для последующей обработки, просто запишите результат на диск:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

Теперь у вас есть постоянная копия, которую можно передать в базу данных, поисковый индекс или движок перевода.

## Часто задаваемые вопросы

**Q: Работает ли это с другими форматами изображений, например JPEG или BMP?**  
A: Абсолютно. `RecognizeImage` принимает любой формат, поддерживаемый библиотекой .NET `System.Drawing`, включая JPEG, BMP и TIFF.

**Q: Что если мне нужно извлечь английский текст в том же запуске?**  
A: Создайте второй экземпляр `OcrEngine` с `Language.English` или переключайте свойство языка между вызовами.

**Q: Могу ли я выполнять OCR в веб‑API без блокировки основного потока?**  
A: Да. Оберните вызов распознавания в `Task.Run` или используйте асинхронную перегрузку `RecognizeImageAsync` (доступно в более новых версиях Aspose).

**Q: Есть ли ограничение на размер PNG?**  
A: Библиотека может обрабатывать большие изображения, но использование памяти растёт с разрешением. Если возникнет `OutOfMemoryException`, рассмотрите возможность уменьшения масштаба изображения заранее.

## Полный рабочий пример (готовый к копированию)

Ниже приведена полная программа, которую вы можете вставить в новый консольный проект (`dotnet new console`) и запустить сразу после установки пакета NuGet.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**Expected console output** (при условии, что пример содержит фразу “Привет, мир!”):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

## Заключение

Мы рассмотрели **как выполнять OCR** на PNG‑изображениях с помощью C#, от установки Aspose.OCR до настройки параметров предобработки и экспорта результатов. Теперь вы знаете, как **читать текст из PNG**, **как извлечь текст** на разных языках и, конкретно, **извлекать русский текст** с минимальным объёмом кода.

Готовы к следующему вызову? Попробуйте передать вывод OCR в библиотеку определения языка или комбинировать его с Azure Cognitive Services для перевода. Возможности безграничны, когда вы сочетаете надёжный OCR‑движок с мощной экосистемой C#.

Если этот **c# ocr tutorial** оказался полезным, поставьте звёздочку, поделитесь им с коллегами или оставьте комментарий со своими советами. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}