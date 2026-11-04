---
category: general
date: 2026-04-08
description: Узнайте, как выполнять OCR изображения и записывать JSON‑файл на C# с
  использованием Aspose OCR. Этот учебник по Aspose OCR C# демонстрирует преобразование
  изображения в JSON с указанием значений уверенности.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: ru
og_description: Выполните OCR изображения и экспортируйте результаты в JSON‑файл на
  C#. Этот учебник охватывает полный рабочий процесс Aspose OCR на C#, включая оценки
  уверенности.
og_title: Выполнить OCR изображения в JSON на C# – Руководство по Aspose OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: Выполнить OCR изображения в JSON на C# с Aspose
url: /ru/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR изображения в JSON на C# с Aspose

Когда‑то вам нужно **выполнить OCR на изображениях**, но вы не знаете, как получить результаты в структурированном виде? Вы не одиноки — разработчики постоянно спрашивают: «Как превратить отсканированную картинку в пригодные данные?» Хорошая новость в том, что Aspose.OCR делает это элементарным, и вы даже можете **записать JSON‑файл C#**‑стилем с включёнными оценками уверенности.

В этом руководстве мы пройдём полный **aspose OCR C# tutorial**, охватывающий всё от загрузки изображения до экспорта распознанного текста в JSON. К концу вы получите готовое консольное приложение, которое **выполняет OCR на изображении**, преобразует вывод в JSON (включая значения уверенности) и сохраняет его одной строкой кода. Никаких скрытых шагов, никаких внешних скриптов — только чистый C#.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или новее (код работает и с .NET Core, и с .NET Framework)
- Visual Studio 2022 (или любой другой редактор)
- Действующая лицензия **Aspose.OCR for .NET** или бесплатная временная лицензия (пробная версия подходит для тестов)
- Файл изображения (`input.png`), который вы хотите обработать (подойдёт любой распространённый формат — PNG, JPG, BMP)

Вот и всё. Если чего‑то не хватает, скачайте сейчас; остальная часть руководства предполагает, что всё уже готово.

## Шаг 1: Установите NuGet‑пакет Aspose.OCR

Первым делом добавьте библиотеку в проект. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Это загрузит последнюю версию (на апрель 2026 года — 23.12) и добавит необходимые DLL‑файлы в папку `bin`. Дополнительная конфигурация не требуется.

## Шаг 2: Инициализируйте OCR‑движок (Perform OCR on Image)

Теперь создаём экземпляр `OcrEngine` и указываем язык. Английский (`"en"`) — самый распространённый, но вы можете заменить его на `"fr"`, `"de"` или любой поддерживаемый язык.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Почему инициализируем здесь:** `OcrEngine` хранит всю конфигурацию, необходимую для процесса распознавания. Установка языка заранее гарантирует, что движок использует правильный набор символов, что значительно повышает точность.

## Шаг 3: Распознайте изображение и получите уверенность

Когда движок готов, передаём ему файл изображения. Метод `RecognizeImage` возвращает объект `OcrResult`, содержащий как извлечённый текст, так и оценку уверенности для каждого слова.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Что происходит «под капотом»?** Aspose использует нейронную сеть, которая анализирует каждый блок пикселей, сравнивает его с языковой моделью и присваивает значение уверенности (0‑100), показывающее, насколько уверенно распознано каждое слово.

## Шаг 4: Преобразуйте результат в JSON (OCR Image to JSON)

Aspose делает преобразование простым. Передавая `includeConfidence: true`, мы получаем JSON‑payload, выглядящий так:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Вот код, который формирует строку JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Зачем включать уверенность?** Если вы планируете передавать данные в последующие процессы (например, валидацию, подсветку в UI), знание «сомнительных» слов позволяет решить, нужно ли запрашивать подтверждение у пользователя.

## Шаг 5: Запишите JSON‑файл C#‑стилем

Теперь мы действительно **записываем JSON файл C#**. Метод `File.WriteAllText` атомарен и кроссплатформенный, что делает его идеальным для консольных приложений.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Это весь процесс — пять лаконичных шагов, которые **выполняют OCR на изображении**, преобразуют вывод в JSON и сохраняют его.

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать в `Program.cs`. Убедитесь, что `input.png` находится в той же папке, что и скомпилированный бинарный файл, либо скорректируйте пути.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Ожидаемый вывод

При запуске программы (`dotnet run`) вы увидите примерно следующее:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

А файл `output.json` будет содержать структурированный JSON, показанный выше, с процентами уверенности для каждого слова.

## Полезные советы и особые случаи

- **Обработка отсутствующего файла:** Оберните вызов `RecognizeImage` в `try/catch` для `FileNotFoundException`, если пути к файлам формируются динамически.
- **Разные языки:** Установите `ocrEngine.Language = "fr"` для французского или загрузите пользовательский языковой пакет через `ocrEngine.LoadLanguage("custom.lang")`.
- **Большие документы:** Для многостраничных PDF сначала преобразуйте каждую страницу в изображение (например, с помощью `Aspose.PDF`) и пройдите цикл OCR для каждой.
- **Тонкая настройка производительности:** Если нужны быстрые результаты, переключитесь на `RecognitionMode.Fast` — немного потеряется точность, но выиграете в скорости.
- **Форматирование JSON:** Хотите красиво отформатированный JSON? Используйте `JsonConvert.SerializeObject` из Newtonsoft с параметром `Formatting.Indented` после десериализации строки JSON от Aspose.

## Часто задаваемые вопросы

**В: Работает ли это с .NET Framework?**  
О: Абсолютно. Тот же NuGet‑пакет нацелен на .NET Standard 2.0, поэтому его можно подключить к .NET Framework 4.6.1 и новее.

**В: А как получить уверенность для всего документа, а не для каждого слова?**  
О: В `OcrResult` также есть свойство `OverallConfidence`. Вы можете добавить его вручную в JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**В: Можно ли напрямую передавать JSON в веб‑API?**  
О: Да. Замените `File.WriteAllText` на POST‑запрос `HttpClient`, который отправит `jsonResult`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}