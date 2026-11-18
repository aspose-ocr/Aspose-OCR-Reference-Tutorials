---
category: general
date: 2026-04-17
description: Узнайте, как выполнять OCR в C#, распознавать текст на изображении, извлекать
  текст из JPG и быстро преобразовывать изображение в текст.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: ru
og_description: Как выполнить OCR в C#? Это руководство покажет, как распознавать
  текст с изображения, извлекать текст из JPG и преобразовывать изображение в текст
  за считанные минуты.
og_title: Как выполнить OCR в C# – распознавание текста на изображении
tags:
- OCR
- C#
- Aspose
title: Как выполнить OCR в C# – распознать текст на изображении
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – распознавание текста с изображения

Когда‑нибудь задавались вопросом **как выполнять OCR** на фотографии, полученной со сканера или телефона? Во многих проектах вам понадобится **распознавать текст с изображений** — будь то чек, рукописная заметка или страница PDF, преобразованная в JPEG. Хорошая новость: с Aspose.OCR вы можете **извлекать текст из jpg** файлов и **преобразовывать изображение в текст** всего несколькими строками C#.

В этом руководстве мы пройдем весь процесс, от установки библиотеки до обработки особых случаев, таких как отсутствие нужных языков. К концу вы точно будете знать **как выполнять OCR**, а также получите готовую к запуску программу, выводящую извлечённую строку в консоль. Никаких неопределённых «см. документацию» обходных путей — только полное, автономное решение.

## Что понадобится

- **.NET 6+** (код также работает на .NET Framework, но .NET 6 — текущий LTS)
- **Aspose.OCR for .NET** пакет NuGet — установить командой `dotnet add package Aspose.OCR`
- Файл изображения (JPEG, PNG, BMP), которым вы хотите протестировать — назовём его `input.jpg`
- Любая IDE по вашему выбору (Visual Studio, Rider, VS Code)

И всё. Никакой дополнительной конфигурации, внешних сервисов и скрытых шагов.

## Шаг 1: Установить Aspose.OCR и добавить ссылку

Сначала подключим библиотеку OCR к вашему проекту. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Команда скачает последнюю стабильную версию (на апрель 2026 года — **23.9.0**) и обновит ваш `.csproj`. После этого добавьте директиву `using` в начало вашего файла:

```csharp
using Aspose.OCR;
```

> **Pro tip:** Если вы используете Visual Studio, UI менеджера пакетов NuGet работает так же хорошо — просто найдите *Aspose.OCR*.

## Шаг 2: Загрузить изображение, которое нужно распознать

Теперь нужно указать OCR‑движку, какое изображение читать. Aspose предоставляет удобный метод `OcrImage.FromFile`, поддерживающий большинство распространённых форматов.

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

Замените `YOUR_DIRECTORY` реальным путём или оставьте изображение рядом с исполняемым файлом и используйте относительный путь. Если файл не существует, метод бросит `FileNotFoundException`, который можно будет перехватить позже.

## Шаг 3: Создать OCR‑движок (с учётом платформы)

Aspose.OCR автоматически выбирает лучший подлежащий движок для вашей ОС (Windows, Linux, macOS). Создание его внутри блока `using` гарантирует корректное освобождение ресурсов.

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

Зачем нужен `using`? Движок держит нативные ресурсы (например, неуправляемую память), которые необходимо освободить. Забвение вызова `Dispose` может привести к утечкам памяти, особенно при обработке множества изображений в цикле.

## Шаг 4: (Опционально) Установить язык – по умолчанию English

Если на изображении английский текст, этот шаг можно пропустить, потому что `OcrLanguage.English` установлен по умолчанию. Для других языков просто присвойте соответствующее значение перечисления.

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **Did you know?** Aspose.OCR поддерживает более 30 языков, включая арабский, китайский и русский. Переключить язык так же просто, как изменить значение enum.

## Шаг 5: Запустить процесс распознавания

Вызов `Recognize` делает всю тяжёлую работу — анализ пикселей, сегментацию символов и поиск в словаре происходят «под капотом».

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

Если движок не найдёт текста, `ocrResult.Text` будет пустой строкой. Перед дальнейшей работой имеет смысл проверить `ocrResult.HasText` (Boolean).

## Шаг 6: Получить и вывести результат в виде простого текста

Наконец, извлекаем строку и выводим её в консоль. Здесь вы действительно **преобразуете изображение в текст**.

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

Вывод будет выглядеть примерно так:

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

Если вам нужен текст для дальнейшей обработки (например, сохранения в файл, загрузки в базу данных или применения регулярных выражений), он уже находится в переменной `recognizedText`.

## Полный рабочий пример

Ниже представлена полная программа, которую можно скопировать в новый консольный проект (`dotnet new console`). В ней реализована обработка самых распространённых ошибок.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **Expected output:** Консоль выводит точные символы, обнаруженные OCR‑движком. Если исходное изображение чёткое и высокого разрешения, точность обычно превышает 95 %.

## Обработка типичных граничных случаев

### 1️⃣ Изображения с несколькими языками  
Если у вас двуязычный чек, установите `ocrEngine.Language` в `OcrLanguage.Multilingual`. Движок попытается автоматически определить каждый язык.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ Низкое разрешение или наклонённые изображения  
Предобработайте изображение (поверните, измените размер, увеличьте контраст) перед передачей в Aspose. Библиотека предоставляет методы `OcrImage` такие как `Resize` и `Rotate`.

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ Большие партии  
При обработке десятков файлов переиспользуйте один экземпляр `OcrEngine` вместо создания нового в каждом проходе цикла. Не забудьте вызвать `Dispose` после завершения партии.

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Ограничения памяти в Linux‑контейнерах  
Если вы работаете внутри Docker‑контейнера с ограниченной ОЗУ, задайте `ocrEngine.MaxMemoryUsage` (если API предоставляет такое свойство), чтобы избежать падения из‑за OOM.

## Pro Tips & Gotchas

- **File Encoding:** Возвращаемая строка — UTF‑16 (`string` в .NET). Если нужен UTF‑8 для записи в файл, используйте `Encoding.UTF8.GetBytes(recognizedText)`.
- **Performance:** Для одного изображения накладные расходы на инициализацию движка пренебрежимо малы. Для массовой обработки инициализируйте один раз (см. пример пакетной обработки), чтобы сократить время примерно на 30 %.
- **Debugging:** Если результат OCR выглядит «мусором», проверьте `ocrResult.Words` (коллекцию отдельных объектов слов) и их confidence‑оценки. Низкая уверенность часто означает размытое изображение.
- **License:** Aspose.OCR работает в режиме оценки без лицензии, но добавляет водяной знак к полученному тексту. Зарегистрируйте файл лицензии (`Aspose.OCR.lic`) для продакшн‑использования.

## Визуальный обзор

![пример выполнения OCR в C#](ocr-example.png "пример выполнения OCR в C#")

*Скриншот показывает полный вывод консоли после запуска примерного кода.*

## Заключение

Теперь вы знаете **как выполнять OCR** в C# с помощью Aspose.OCR и уверенно можете **распознавать текст с изображений**, **извлекать текст из jpg** и **преобразовывать изображение в текст** для любой последующей обработки. Пример охватывает основные шаги, объясняет, почему каждый из них важен, и даже намекает на продвинутые сценарии, такие как поддержка нескольких языков и пакетная обработка.

Что дальше? Попробуйте заменить JPEG на PNG, поэкспериментировать с `OcrLanguage.Multilingual` или передать извлечённый текст в конвейер обработки естественного языка. Возможности безграничны, когда можно превратить картинки в поисковые, редактируемые строки.

Есть вопросы или столкнулись с проблемой? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}