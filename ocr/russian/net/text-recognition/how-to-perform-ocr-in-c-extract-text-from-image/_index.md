---
category: general
date: 2026-04-03
description: Узнайте, как выполнять OCR в C# и извлекать текст из изображения с помощью
  Aspose OCR, с проверкой орфографии для русского языка.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: ru
og_description: Узнайте, как выполнять OCR в C# и извлекать текст из изображения с
  помощью Aspose OCR, с проверкой орфографии для русского языка.
og_title: Как выполнить OCR в C# — извлечь текст из изображения
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Как выполнить OCR в C# — извлечь текст из изображения
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – Извлечение текста из изображения

Когда‑нибудь задавались вопросом **how to perform OCR** на фотографии рукописной заметки? Возможно, у вас есть отсканированный чек, вывеска на иностранном языке или страница PDF, которую нельзя копировать‑вставлять. Хорошая новость? С несколькими строками C# и библиотекой Aspose OCR вы можете превратить эту картинку в редактируемый текст в мгновение ока.  

В этом руководстве мы не только покажем вам **how to perform OCR**, но и пройдемся по **extract text from image**, **convert image to text**, а также **how to spell check** результат, когда вы работаете с документами на русском языке. Звучит сложно? Оставайтесь — мы разберём всё шаг за шагом.

## Что вы узнаете

* Настроить Aspose OCR для поддержки русского языка.  
* Загрузить файл изображения и выполнить оптическое распознавание символов, чтобы **extract text from image**.  
* Использовать встроенный проверщик орфографии для автоматического исправления опечаток — идеальный ответ на вопрос “**how to spell check**” вывода OCR.  
* Вывести очищенную строку в консоль, готовую к дальнейшей обработке или сохранению.

**Prerequisites** – вам понадобится:

* .NET 6.0 или новее (код также работает с .NET Framework 4.8).  
* Действительная лицензия Aspose OCR или временный оценочный ключ.  
* Файл изображения, содержащий русский текст (для демонстрации будем использовать `russian_note.jpg`).  

Если что‑то из этого вам незнакомо, не переживайте. Ниже указана точная команда NuGet для получения Aspose OCR, а код полностью автономный.

![пример выполнения OCR](/images/ocr-demo.png "пример выполнения OCR в C# example")

## Шаг 1 – Установить Aspose OCR и добавить пространства имён

Сначала вам нужна сама библиотека. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Эта команда скачивает последнюю стабильную версию (по состоянию на апрель 2026 это 22.9). После восстановления пакета добавьте необходимые директивы `using` в начало вашего C# файла:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Совет:* Если вы используете Visual Studio, IDE предложит добавить их автоматически, как только вы начнёте вводить первое имя класса.

## Шаг 2 – Инициализировать OCR‑движок для русского языка

Часть **how to perform OCR** начинается с создания экземпляра `OcrEngine`. Указав `OcrLanguage.Russian`, мы говорим движку загрузить набор кириллических символов и языковые эвристики.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Почему это важно? Без указания языка движок по умолчанию использует английский и будет неправильно интерпретировать многие кириллические символы, что приводит к искажённому выводу. Явная настройка языка значительно повышает точность.

## Шаг 3 – Загрузить изображение и **Convert Image to Text**

Теперь загрузим картинку в память. Метод `Image.FromFile` работает с большинством распространённых форматов (JPG, PNG, BMP). После загрузки вызываем `Recognize`, чтобы **convert image to text**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

Переменная `rawText` теперь содержит «сырой» вывод OCR, который всё ещё может включать опечатки или неверно распознанные символы. Вы можете вывести её, чтобы увидеть, что захватил движок:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Шаг 4 – **How to Spell Check** результат OCR

Русский OCR может быть шумным, особенно при сканировании с низким разрешением. Aspose предоставляет класс `SpellChecker`, который «из коробки» понимает русские словари. Вот как его вызвать:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

Метод `CheckAndCorrect` возвращает новую строку, где ошибочные слова заменены на наиболее вероятные правильные варианты. Он также сохраняет пунктуацию, так что вы не получите «стену» текста.

*Пограничный случай:* Если вывод OCR пуст (например, изображение полностью белое), `CheckAndCorrect` просто вернёт пустую строку. Хорошая идея — проверять это, если вы планируете записывать результат в файл.

## Шаг 5 – Вывести очищенный результат

Наконец, выводим исправленную строку. В реальном приложении вы могли бы записать её в базу данных, JSON‑API или документ Word. Для этой демонстрации достаточно вывести её в консоль:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

При запуске программы вы должны увидеть что‑то вроде:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Обратите внимание, как проверщик орфографии превратил «Привeт» (смешанный латинский ‘e’) в правильное кириллическое «Привет». Это магия **how to spell check** вывода OCR.

## Полный рабочий пример

Ниже представлен полностью готовый к запуску код, объединяющий все шаги. Скопируйте‑вставьте его в новый консольный проект и нажмите **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Ожидаемый вывод

Запуск программы с чёткой, высоко‑разрешающей фотографией русского рукописного текста обычно даёт чистое, читаемое человеком предложение. Если изображение размыто, вы всё равно можете получить частично правильные слова, но проверщик орфографии сгладит большинство очевидных ошибок.

## Частые проблемы и советы

| Проблема | Почему происходит | Как исправить / избежать |
|----------|-------------------|--------------------------|
| **Garbage characters** | Низкое DPI или шумный фон | Предобработайте изображение (увеличьте контраст, масштабируйте до ≥300 dpi) перед передачей в `Recognize`. |
| **Empty output** | Неправильный путь к файлу или неподдерживаемый формат | Проверьте путь и используйте `Image.FromFile` внутри блока `try/catch`, чтобы отобразить ошибки. |
| **Spell checker misses errors** | Редкие слова отсутствуют в словаре | Расширьте словарь, загрузив пользовательский список через `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Performance lag on large batches** | OCR требует много CPU | Запускайте OCR в фоновом потоке или используйте `Parallel.ForEach` для обработки нескольких изображений. |
| **License exception** | Использование оценочной версии после окончания пробного периода | Приобретите лицензию и вызовите `License license = new License(); license.SetLicense("Aspose.Total.lic");` перед созданием `OcrEngine`. |

## Следующие шаги – выход за пределы простого OCR

Теперь, когда вы освоили **how to perform OCR**, рассмотрите следующие расширения:

* **Batch processing** – Пройдите по папке с изображениями и запишите каждый исправленный текст в файл `.txt`.  
* **PDF conversion** – Используйте Aspose PDF, чтобы встроить извлечённый текст обратно в поисковый PDF.  
* **Language detection** – Если нужно обрабатывать несколько языков, сначала проанализируйте результат OCR и переключите `OcrLanguage` соответственно.  
* **Integration with Azure Cognitive Services** – Сравните результаты Aspose с OCR‑API Microsoft для гибридного подхода.

Все эти темы естественно включают вторичные ключевые слова **extract text from image**, **convert image to text**, и **how to spell check**, так что

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}