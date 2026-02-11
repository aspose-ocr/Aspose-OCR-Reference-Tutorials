---
category: general
date: 2026-02-11
description: Извлечение текста из изображения в C# с помощью Aspose OCR. Узнайте,
  как загрузить изображение для OCR, улучшить точность OCR и исправить ошибки OCR
  с помощью проверки орфографии.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: ru
og_description: Извлечение текста из изображения в C# с помощью Aspose OCR. Это руководство
  показывает, как загрузить изображение для OCR, улучшить точность OCR и исправить
  ошибки OCR.
og_title: Извлечение текста из изображения в C# – Полное руководство по OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Извлечение текста из изображения в C# – Полное руководство по OCR
url: /ru/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – Полное руководство по OCR

Когда‑нибудь вам нужно было **extract text from image**, но результаты выглядели как набор бессмыслицы? Вы не одиноки. Во многих реальных приложениях — например, сканирование чеков, оцифровка заметок или миграция устаревших документов — получение чистого текста из картинки является первым и часто самым сложным препятствием.

К счастью, с Aspose OCR вы можете **load image for OCR**, выполнить проверку орфографии и получить аккуратный, индексируемый текст. В этом руководстве мы пройдем весь конвейер, от чтения JPEG до полировки вывода, и вы увидите, как именно **improve OCR accuracy**, пока вы этим занимаетесь.

> **Что вы получите:** готовую к запуску консольную программу на C#, которая извлекает текст из изображения, исправляет типичные ошибки OCR и выводит как необработанные, так и очищенные результаты.

---

## Что понадобится

- .NET 6 или новее (код также работает на .NET Framework 4.7+)
- Visual Studio 2022 (или любую предпочитаемую IDE)
- Бесплатный пробный ключ Aspose OCR или лицензированная версия
- Файл изображения, содержащий печатный или напечатанный текст (например, `typed_note.jpg`)

Никакие другие сторонние библиотеки не требуются — Aspose автоматически обрабатывает языковые модели и проверку орфографии.

---

## Шаг 1 – Установить пакет Aspose OCR NuGet

Прежде чем мы сможем **extract text from image**, OCR‑движок должен быть доступен на машине.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Или, если вы предпочитаете CLI:

```bash
dotnet add package Aspose.OCR
```

Пакет включает языковые данные, но установка `AutomaticResourceDownload = true` (как мы сделаем позже) гарантирует, что любые отсутствующие словари будут загружены во время выполнения.

---

## Шаг 2 – Загрузить изображение для OCR

Первое, что требуется движку, — это bitmap. Вы можете передать ему любой формат, поддерживаемый `System.Drawing.Image`, например PNG, JPEG, BMP или TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Зачем блок `using`?** Он автоматически освобождает объект `Image`, предотвращая проблемы с блокировкой файлов, которые часто возникают у разработчиков, забывающих освободить ресурсы.

---

## Шаг 3 – Выполнить OCR – «Image to Text C#» в действии

Теперь мы действительно **extract text from image**. Класс `OcrEngine` выполняет основную работу.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

На данном этапе у вас есть строка, отражающая то, что движок видит на изображении. На практике вывод может содержать лишние символы, неправильно распознанные слова или странные разрывы строк — поэтому следует следующий шаг.

---

## Шаг 4 – Повысить точность OCR с помощью проверки орфографии

Aspose поставляется с отдельным `SpellChecker`, который знает язык, который вы обрабатываете. Применение его к необработанной строке часто исправляет наиболее очевидные ошибки.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Совет профессионала:** Если вы работаете со специализированными словарями (например, медицинскими терминами), вы можете передать пользовательский словарь в `SpellChecker` через его перегрузки.

---

## Шаг 5 – Исправить ошибки OCR вручную (по желанию)

Даже лучший проверщик орфографии может пропустить ошибки, зависящие от контекста. Быстрая постобработка может поймать такие вещи, как «l» vs «1» или «O» vs «0».

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

Не стесняйтесь расширять этот раздел своими эвристиками — возможно, таблицей соответствий для кодов продуктов или списком известных аббревиатур.

---

## Полный рабочий пример

Ниже представлен полный код программы, который вы можете скопировать и вставить в новый проект консольного приложения. Он включает каждый обсуждённый шаг, а также полезные комментарии.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Ожидаемый вывод

Если предположить, что `typed_note.jpg` содержит предложение «Hello world, this is a test 123», консоль выведет примерно следующее:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Обратите внимание, как проверка орфографии превратила «H3llo» в «Hello», а регулярное выражение удалило лишнюю «1», появившуюся в «th1s».

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Можно ли использовать другой язык?** | Да. Установите `ocrEngine.Language = OcrLanguage.Spanish` (или любой поддерживаемый enum) и передайте тот же язык в `SpellChecker`. |
| **Что делать, если мое изображение очень большое?** | Уменьшите его перед передачей в OCR; у `Image` есть `GetThumbnailImage` для быстрого изменения размера. |
| **Нужен ли интернет?** | Только в первый раз, когда отсутствует языковой пакет; после этого ресурсы кэшируются локально. |
| **Как обрабатывать многостраничные PDF?** | Преобразуйте каждую страницу в изображение (например, с помощью `PdfRenderer`) и запустите тот же конвейер для каждой страницы. |
| **Проверка орфографии учитывает язык?** | Абсолютно. Он использует ту же языковую модель, которую вы передали OCR‑движку, обеспечивая согласованность. |

---

## Следующие шаги и связанные темы

- **Пакетная обработка:** Оберните код в цикл `foreach`, чтобы обрабатывать папку с изображениями.
- **Рукописный текст:** Переключите на `OcrLanguage.EnglishHandwritten` для получения лучших результатов с курсивными заметками.
- **Параллелизм:** Используйте `Parallel.ForEach` для ускорения больших нагрузок на многопроцессорных машинах.
- **Экспорт в JSON/CSV:** Сериализуйте `finalText` вместе с метаданными (имя файла, оценки уверенности) для последующего анализа.

Если вам интересно превратить извлечённые строки в поисковые PDF, ознакомьтесь с нашим руководством **«Create searchable PDF from image in C#»**. Оно построено непосредственно на том же конвейере OCR, который мы только что рассмотрели.

---

## Заключение

Мы только что продемонстрировали практический способ **extract text from image** в C# с использованием Aspose OCR, а также показали, как **load image for OCR**, **improve OCR accuracy** и **fix OCR errors** с помощью встроенного проверяющего орфографии и небольшого очистки регулярным выражением. Полный пример работает сразу после установки, требует лишь один пакет NuGet и может быть расширен под практически любой сценарий оцифровки документов

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}