---
category: general
date: 2026-03-07
description: Пример Aspose OCR, показывающий, как включить проверку орфографии, добавить
  пользовательский словарь, загрузить изображение для OCR и быстро исправлять ошибки
  OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: ru
og_description: Пример Aspose OCR, который пошагово покажет, как включить проверку
  орфографии, добавить пользовательский словарь, загрузить изображение для OCR и исправить
  типичные ошибки OCR.
og_title: Пример Aspose OCR – Включить проверку орфографии и исправить ошибки
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Пример Aspose OCR – включить проверку орфографии и исправить ошибки в C#
url: /ru/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пример Aspose OCR – Включение проверки орфографии и исправление ошибок в C#

Когда‑то вам нужен **пример Aspose OCR**, который не только читает текст из изображения, но и устраняет назойливые орфографические ошибки? Вы не одиноки. Во многих реальных проектах необработанный вывод OCR заполнен опечатками, особенно когда исходное изображение содержит низкоконтрастные шрифты или рукописные заметки.  

Хорошая новость? С Aspose.OCR вы можете **включить проверку орфографии**, подключить собственный словарь и получить отшлифованную строку всего в несколько строк кода. Ниже вы увидите, **как включить проверку орфографии**, **как добавить словарь** и **как загрузить изображение для OCR**, чтобы наконец‑то **исправлять ошибки OCR**, не теряя волосы.

В этом руководстве мы охватим всё, что нужно — от установки через NuGet до полностью готовой, исполняемой программы, выводящей исправленный текст. К концу вы получите надёжный **пример Aspose OCR**, который можно сразу вставить в любой .NET‑проект.

## Требования

- .NET 6.0 SDK или новее (код работает и с .NET Core, и с .NET Framework)
- Visual Studio 2022 или любой IDE, поддерживающий C#
- Файл изображения (`typed_text.png`) с чётким печатным английским текстом
- Доступ в Интернет для загрузки пакета Aspose.OCR из NuGet

Никаких дополнительных сторонних библиотек не требуется.

---

## Шаг 1 – Установить пакет Aspose.OCR NuGet (Load Image OCR)

Прежде чем писать код, нам нужна библиотека, которая питает движок OCR.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы используете Visual Studio, щёлкните правой кнопкой мыши по проекту → *Manage NuGet Packages* → найдите **Aspose.OCR** и нажмите *Install*.  

Установка пакета даёт доступ к `OcrEngine`, `ImageStream` и встроенным утилитам проверки орфографии, которые мы будем использовать позже. После установки пакета вы готовы к **загрузке изображения для OCR**.

## Шаг 2 – Создать экземпляр OCR‑движка

Создание движка — первый конкретный шаг в любом **примере Aspose OCR**. Думайте о `OcrEngine` как о мозге, который будет анализировать битмап и выдавать текст.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Конструктор `OcrEngine` не требует параметров, что делает его удобным для быстрых прототипов.

## Шаг 3 – Как включить проверку орфографии (и почему это важно)

Необработанный вывод OCR часто содержит неверно распознанные слова, например «teh» вместо «the». Включение встроенной проверки орфографии позволяет Aspose автоматически заменять такие ошибки на наиболее вероятное правильное написание.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Почему стоит включать проверку орфографии?**  
> - **Точность:** Постобработка с проверкой орфографии может повысить общую точность текста на 10‑15 % для печатных документов.  
> - **Опыт пользователя:** Чистый текст означает меньше последующей очистки, когда вы передаёте результат в поисковые индексы или аналитические конвейеры.

## Шаг 4 – Как добавить словарь (пользовательские слова)

Иногда стандартный словарь не знает названий ваших брендов, кодов продуктов или отраслевого жаргона. Здесь в игру вступает **как добавить словарь**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Можно передать массив, список или даже прочитать из файла, если у вас большой пользовательский словарь. Проверка орфографии теперь будет считать эти записи допустимыми, предотвращая ложные исправления.

## Шаг 5 – Загрузить изображение для OCR (Load Image OCR)

Теперь, когда движок настроен, нужно указать ему, какое изображение читать. Помощник `ImageStream.FromFile` абстрагирует детали чтения файла.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Подсказка:** Если ваше изображение находится в подпапке проекта, установите для него свойство *Copy to Output Directory* в значение *Copy always*, чтобы путь разрешался во время выполнения.

## Шаг 6 – Выполнить распознавание и исправить ошибки OCR

После всех настроек один вызов `Recognize()` запускает конвейер OCR, применяет проверку орфографии и сохраняет очищенный результат в `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Ожидаемый вывод

Предположим, `typed_text.png` содержит предложение `The quick brown fox jumps over teh lazy dog`. Консоль выведет:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Обратите внимание, как «teh» автоматически исправилось на «the». Если бы вы добавили «OCRify» в пользовательский словарь и изображение содержало бы это слово, движок оставил бы его без изменений.

---

## Полный рабочий пример (готов к копированию)

Ниже представлена полная программа, которую можно вставить в новый консольный проект. В ней включены все шаги выше, а также несколько комментариев для ясности.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet run`, и вы должны увидеть исправленное предложение в консоли.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если изображение — многостраничный PDF?** | Aspose.OCR может обрабатывать страницы PDF как изображения. Используйте `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` и перебирайте страницы. |
| **Можно ли сменить язык на другой, кроме английского?** | Конечно. Установите `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (или любой поддерживаемый язык). |
| **Мой пользовательский словарь огромен — повлияет ли это на производительность?** | Добавление тысяч слов требует небольших начальных затрат, но поиск происходит за O(1) благодаря хеш‑множеству под капотом. Для очень больших словарей рекомендуется загружать их один раз при старте приложения. |
| **Что если OCR‑движок бросает исключение при повреждённом изображении?** | Оберните `Recognize()` в блок try‑catch и проверьте `ocrEngine.LastError`. Можно также предварительно проверить размеры изображения через `ocrEngine.Image.Width` и `Height`. |
| **Нужна ли лицензия для использования в продакшене?** | Бесплатная оценочная версия подходит для тестирования, но коммерческая лицензия убирает водяной знак оценки и открывает полную производительность. |

---

## Заключение

Теперь у вас есть **полный пример Aspose OCR**, демонстрирующий **как включить проверку орфографии**, **как добавить словарь**, **загрузить изображение для OCR** и **как исправлять ошибки OCR** чистым, готовым к продакшену способом. Настроив проверку орфографии и передав собственный список слов, вы значительно повышаете качество извлечённого текста без написания дополнительной пост‑обработки.

Готовы к следующему шагу? Попробуйте переключить язык на испанский, обработать многостраничный PDF или интегрировать вывод в индексируемый Azure Cognitive Search. Тот же шаблон работает — нужно лишь изменить флаг языка и, возможно, расширить пользовательский словарь.

Если этот гид оказался полезным, поставьте звёздочку на GitHub, поделитесь им с коллегами или оставьте комментарий ниже. Приятного кодинга, и пусть результаты OCR всегда будут без ошибок!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}