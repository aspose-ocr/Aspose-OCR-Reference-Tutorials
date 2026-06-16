---
category: general
date: 2026-02-22
description: как выполнить OCR изображения с помощью Aspose OCR – удалить шум изображения,
  повысить контраст и быстро извлечь текст из изображения в C#
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: ru
og_description: Узнайте, как выполнять OCR изображения с помощью Aspose OCR, удалять
  шум, повышать контраст и извлекать текст из изображения в C# с полным готовым к
  запуску примером.
og_title: как распознать текст на изображении – увеличить контраст и удалить шум
tags:
- OCR
- C#
- Image Processing
title: 'как распознать изображение: увеличить контраст, удалить шум'
url: /ru/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

.

We must not translate shortcodes, which are the blocks at top and bottom.

We must keep markdown links unchanged; there are none besides maybe none.

We need to translate the text inside code block placeholders? Those are placeholders, not actual code, so we should leave them unchanged.

We need to translate the "Expected output:" and the code block placeholder after.

Also translate the "Common Questions & Tips" etc.

Make sure to keep the same structure.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как распознать текст на изображении – увеличить контраст и удалить шум в C#

Когда‑нибудь задумывались **как распознать текст на изображении**, которое искажено, зернистое или просто трудно читаемое? Вы не одиноки. Во многих реальных проектах — например, сканирование чеков или оцифровка старых документов — исходное изображение редко бывает идеальным. Хорошая новость? С несколькими строками кода на C# и Aspose OCR вы можете **удалить шум с изображения**, **повысить контраст изображения** и наконец **извлечь текст с изображения** без лишних усилий.

В этом руководстве мы пройдем полный сквозной процесс. К концу вы точно будете знать, как настроить движок OCR, очистить шумное изображение и **распознать текст на изображении**, чтобы передать результат туда, где он нужен. Никаких расплывчатых ссылок, только готовый пример кода и обоснование каждого шага.

## Что понадобится

- .NET 6+ (или .NET Core 3.1+ — API одинаковый)
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)
- Пример изображения, которое искажено и шумно (например, `skewed_noisy.jpg`)
- Любая IDE — Visual Studio, Rider или VS Code подойдут

И всё. Если у вас есть эти вещи, можно сразу переходить к коду.

![пример как распознать изображение](/images/ocr-demo.png){alt="пример как распознать изображение"}

## Шаг 1: Инициализация OCR‑движка – как правильно распознать изображение  

Первое, что нужно сделать, — создать экземпляр `OcrEngine` и указать, какой язык ожидать. Английский самый распространённый, но Aspose поддерживает десятки языков «из коробки».

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**Почему это важно:** Движку необходимо знать набор символов; иначе он будет тратить ресурсы на догадки, и точность упадёт. Указание языка заранее также снижает потребление памяти, потому что загружаются только нужные языковые данные.

## Шаг 2: Загрузка изображения и начало удаления шума  

Далее мы загружаем картинку с диска. В большинстве случаев файл — JPEG или PNG, содержащий много зерна. Загрузка его в объект `Image` даёт нам ссылку, которую можно передать через фильтры.

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**Совет:** Если ваше изображение находится в облачном бакете, его можно сразу стримить с помощью `Image.Load(Stream)`. Так вы избегаете создания временного файла.

## Шаг 3: Применение цепочки фильтров – увеличить контраст и очистить шум  

Aspose OCR поставляется с удобным конвейером фильтров. Здесь мы соединяем три фильтра:

1. **DeskewFilter** — исправляет вращение, чтобы текст был горизонтален.  
2. **DenoiseFilter** — удаляет зернистость без размытия букв.  
3. **ContrastFilter** — усиливает разницу между передним планом и фоном, делая бледные символы более заметными.

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**Почему именно эти фильтры?**  
- **Deskew** необходим для точного OCR; даже небольшое отклонение в несколько градусов может вдвое снизить распознавание.  
- **Denoise** решает проблему «удалить шум с изображения», часто встречающуюся при сканировании камерой телефона.  
- **Contrast** — секретный ингредиент для низкоконтрастных документов, например, выцветших чеков.  

Вы можете настроить коэффициент `ContrastFilter` (по умолчанию `1.0f`). Значения выше `1.5f` могут переэкспонировать изображение, поэтому поэкспериментируйте.

## Шаг 4: Распознавание текста на изображении – сердце процесса  

Теперь, когда изображение очищено, передаём его OCR‑движку.

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

Метод `Recognize` возвращает объект `OcrResult`, содержащий извлечённую строку, оценки уверенности и даже ограничивающие рамки, если они нужны для подсветки.

**Особый случай:** Если изображение содержит несколько языков, можно установить `ocrEngine.Language = Language.English | Language.Spanish;`. Движок попробует обе словарные базы.

## Шаг 5: Вывод и проверка – извлечённый текст для вашего приложения  

Наконец, выводим текст в консоль. В реальном приложении вы, вероятно, запишете его в базу данных, файл или передадите в последующий NLP‑конвейер.

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ожидаемый вывод:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

Если видите «мусорные» символы, вернитесь к Шагу 3 и скорректируйте параметры фильтров. Часто помогает увеличить коэффициент контраста или добавить `SharpenFilter`.

## Часто задаваемые вопросы и советы  

### Что делать, если изображение уже черно‑белое?  
Можно пропустить `ContrastFilter` и использовать только `DenoiseFilter`. Переконтрастирование бинарного изображения может создать артефакты.

### Как обрабатывать очень большие файлы (>10 МБ)?  
Загрузите изображение в более низком разрешении (`Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`) перед фильтрацией. OCR‑движок нормально работает с уменьшенными версиями, пока текст остаётся разборчивым.

### Можно ли запустить это в веб‑API?  
Конечно. Оберните ту же логику в контроллер ASP.NET Core, принимайте `IFormFile` и возвращайте результат OCR в виде JSON. Не забудьте освобождать объекты `Image` после использования.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}