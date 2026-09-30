---
category: general
date: 2026-01-02
description: Изучите, как распознавать китайский текст и извлекать его из PNG‑файлов
  с помощью офлайн‑распознавания текста Aspose.OCR. Интернет не требуется — выполните
  OCR изображения за несколько шагов.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: ru
og_description: распознавать китайский текст без интернета. Этот учебник показывает,
  как извлекать текст из PNG с помощью офлайн‑распознавания и выполнять OCR изображения
  в C#.
og_title: Распознавание китайского текста офлайн – пошаговое руководство C#
tags:
- OCR
- C#
- Aspose
title: Распознавание китайского текста офлайн — Полный учебник по OCR на C#
url: /ru/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание китайского текста офлайн – Полный C# OCR‑урок

Когда‑то вам нужно было **распознать китайский текст** из отсканированного PNG, но ваше приложение работает на машине без интернета? Вы не одиноки. Во многих корпоративных сценариях — например, на изолированных серверах или полевых устройствах — использование облачных сервисов просто невозможно.  

В этом руководстве мы пройдемся по автономному решению, которое позволяет **извлекать текст из png**‑файлов, выполнять **офлайн‑распознавание текста** и **проводить OCR над изображениями** с помощью Aspose.OCR. К концу вы получите готовую к запуску консольную программу на C#, которая выводит китайские символы прямо в консоль.

## Требования

- .NET 6 SDK (или любая современная версия .NET), установленная локально.  
- Visual Studio 2022 или VS Code — что вам больше нравится.  
- Пакет NuGet Aspose.OCR for .NET (`Aspose.OCR`).  
- Файлы языковых ресурсов для английского и упрощённого китайского (в руководстве показано, как загрузить их автоматически).  
- Изображение с именем `chinese_doc.png`, помещённое в папку, к которой вы можете обратиться (заполнитель `YOUR_DIRECTORY`).

Никаких дополнительных сервисов, никаких API‑ключей — только локальная DLL и пара файлов ресурсов.

---

## Шаг 1 – Скачайте необходимые языковые ресурсы (один раз)

Aspose.OCR хранит языковые пакеты на диске. При первом запуске приложения их нужно загрузить. Вызов `ResourceManager.DownloadResources` делает именно это, а поскольку мы передаём как английский, так и упрощённый китайский, движок позже сможет переключаться между ними без какого‑либо сетевого трафика.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tip:** Храните загруженную папку (`Aspose.OCR.Resources`) под системой контроля версий, если вам нужны воспроизводимые сборки на нескольких машинах.

## Шаг 2 – Инициализируйте OCR‑движок в офлайн‑режиме

Установка `OfflineMode = true` заставляет библиотеку избегать любых HTTP‑запросов. Это ключ к настоящему **офлайн‑распознаванию текста**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Почему это важно:** Некоторые OCR‑библиотеки переключаются на облачные сервисы, если языковой пакет отсутствует. Принудив офлайн‑режим, мы гарантируем детерминированную производительность и соответствие политикам конфиденциальности данных.

## Шаг 3 – Загрузите PNG, который нужно обработать

Мы будем использовать `System.Drawing.Bitmap` для чтения изображения. Если ваш проект нацелен на .NET 6+ на платформах, отличных от Windows, рассмотрите `SkiaSharp` как альтернативу, но для большинства Windows‑ориентированных развертываний `Bitmap` работает отлично.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Edge case:** Если PNG очень большой (более 5 МП), имеет смысл сначала уменьшить его масштаб, чтобы ускорить распознавание и снизить использование памяти:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Шаг 4 – Запустите распознавание с упрощённым китайским языком

Здесь мы явно указываем движку, какой язык использовать. Объект `RecognitionOptions` также позволяет настроить такие параметры, как `DetectOrientation` или `PreserveFormatting`, но значения по умолчанию подходят для большинства печатных документов.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Шаг 5 – Выведите (или дальше обработайте) извлечённый текст

Свойство `OcrResult.Text` содержит текстовое представление. Вы можете вывести его в консоль, записать в файл или передать в последующий NLP‑конвейер.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Ожидаемый вывод

Если `chinese_doc.png` содержит фразу «你好，世界！», консоль покажет:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Note:** Точность OCR зависит от качества изображения, чёткости шрифта и контрастности. Для лучших результатов используйте сканы высокого разрешения (300 dpi и выше) и убедитесь, что текст не наклонён.

---

## Полный рабочий пример

Ниже представлена полностью готовая к копированию и вставке программа. Сохраните её как `Program.cs` в новом консольном проекте и запустите `dotnet run`. Все шаги объединены, так что вы увидите поток от загрузки ресурсов до финального вывода.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tip:** Оберните вызов `ResourceManager.DownloadResources` в блок `try/catch`, если хотите корректно обрабатывать ситуацию, когда интернет действительно недоступен. В противном случае метод бросит `NetworkException`.

---

## Часто задаваемые вопросы (FAQ)

| Question | Answer |
|----------|--------|
| **Can I recognise Traditional Chinese?** | Да — замените `Language.ChineseSimplified` на `Language.ChineseTraditional` и скачайте соответствующий пакет. |
| **What if I need to extract text from a JPEG instead of PNG?** | Тот же код работает; просто измените расширение файла. `Bitmap` поддерживает большинство распространённых растровых форматов. |
| **Is there a way to get bounding boxes for each character?** | Установите `RecognitionOptions.DetectRegions = true`. Тогда `OcrResult` будет содержать объекты `Region` с координатами. |
| **How do I run this on Linux?** | Используйте пакет `System.Drawing.Common` (версии 1.0+). На безголовом Linux может потребоваться нативная зависимость `libgdiplus`. |
| **Can I batch‑process a folder of images?** | Конечно — оберните логику распознавания в цикл `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

---

## Следующие шаги и связанные темы

- **Improve accuracy**: поэкспериментируйте с `RecognitionOptions.PreprocessImage = true`, чтобы движок автоматически улучшал контраст.  
- **Combine languages**: можно передать массив языков в `ResourceManager.DownloadResources` и позволить движку автоматически определять язык.  
- **Integrate with a UI**: перенесите консольный код в приложение WinForms или WPF и выводите результат OCR в текстовое поле.  
- **Explore other Aspose libraries**: `Aspose.PDF` для генерации PDF, `Aspose.Slides` для автоматизации слайдов и т.д.  

Если вас интересует извлечение текста из других форматов изображений, тот же шаблон применим — просто замените путь к файлу и, при необходимости, скорректируйте параметры предобработки. Приятного кодинга!

---

![пример распознавания китайского текста](/images/recognize-chinese-text.png "Скриншот, показывающий вывод распознавания китайского текста в консоли")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}