---
category: general
date: 2026-06-03
description: Выполните OCR изображения и извлеките текст из него с помощью Aspose.OCR.
  Узнайте, как обнаруживать орфографические ошибки и получать предложения по их исправлению
  в одном демонстрационном примере на C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: ru
og_description: Выполните OCR изображения, чтобы извлечь текст, затем обнаружьте орфографические
  ошибки и получите предложения по исправлению с помощью Aspose.OCR в C#.
og_title: Выполнить OCR изображения и обнаружить орфографические ошибки в C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Выполнить OCR изображения и обнаружить орфографические ошибки в C#
url: /ru/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении и обнаружение орфографических ошибок в C#

Задумывались когда‑нибудь, как **perform OCR on image** файлы, не теряя волосы? Вы не одиноки. Будь то оцифровка старых писем, сканирование чеков или создание умного документооборота, извлечение чистого текста из изображений — первая преграда. Хорошие новости? С Aspose.OCR вы можете собрать решение за считанные минуты, а бонус в том, что вы также можете **detect misspelled words** и **get spelling suggestions** за один запуск.

В этом руководстве мы пройдем через полностью готовое к запуску консольное приложение C#, которое **extracts text from image**, запускает английский spell‑checker и выводит каждую ошибку с удобными вариантами исправления. К концу вы точно будете знать **how to extract text**, как подключить API проверки орфографии и как выглядит ожидаемый вывод в консоли.

## Что вы построите

- Загрузить bitmap (или PNG), содержащий типографические ошибки.  
- Запустить Aspose.OCR для **perform OCR on image** и получить необработанные строковые данные.  
- Инициализировать встроенный английский spell‑checker.  
- **Detect misspelled words** и **get spelling suggestions** для каждого.  
- Вывести аккуратный отчет в консоль.

Без внешних сервисов, без сложных HTTP‑запросов — только один пакет NuGet и несколько строк кода.

## Требования

- .NET 6.0 SDK или новее (код также работает на .NET Framework 4.7+).  
- Visual Studio 2022 (или любой другой редактор).  
- NuGet‑пакет Aspose.OCR для .NET (`Aspose.OCR`).  
- Файл изображения (`letter_with_typos.png`), размещённый в месте, откуда его можно ссылаться из проекта.

Если вы никогда не использовали Aspose раньше, не волнуйтесь — установка пакета так же проста, как выполнить:

```bash
dotnet add package Aspose.OCR
```

Теперь давайте погрузимся в реализацию.

## Шаг 1: Создание проекта и установка Aspose.OCR

Создайте новый консольный проект и подключите библиотеку OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

После завершения восстановления откройте `Program.cs`. Мы позже заменим содержимое по умолчанию полным демонстрационным кодом, но сначала расскажем, почему каждый неймспейс важен.

- `Aspose.OCR` — ядро OCR‑движка и обработка изображений.  
- `Aspose.OCR.SpellCheck` — утилиты проверки орфографии, поставляемые с библиотекой.  
- `System` — стандартные базовые классы .NET (например, `Console`).

## Шаг 2: Загрузка изображения и выполнение OCR на изображении

Первая реальная работа — передать изображение OCR‑движку. Aspose.OCR читает множество форматов (PNG, JPEG, TIFF). Вот фрагмент кода, который делает всю тяжёлую работу:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Почему это важно:** `OcrImage.FromFile` абстрагирует детали уровня пикселей, а `OcrEngine.Recognize` запускает обученную нейронную модель, переводящую визуальные глифы в символы Unicode. Свойство `ocrResult.Text` теперь содержит необработанную строку — именно то, что вам нужно для **extract text from image**.  
> **Полезный совет:** Если ваше изображение содержит несколько языков, вы можете установить `ocrEngine.Language = OcrLanguage.Multilingual;` перед вызовом `Recognize`.

## Шаг 3: Инициализация английского Spell‑Checker

Aspose.OCR поставляется со встроенным движком проверки орфографии, который сразу понимает английский. Инициализация занимает одну строку:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Почему этот шаг важен:** Вывод OCR может включать неправильно распознанные символы (например, “l” vs “1”) или реальные опечатки из исходного документа. Проверка орфографии просканирует строку, найдет подозрительные токены и предложит альтернативы.

## Шаг 4: Обнаружение орфографических ошибок и получение предложений по исправлению

Теперь передаем текст OCR в проверщик:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` — это коллекция, где каждая запись содержит ошибочное слово и массив возможных исправлений.

## Шаг 5: Вывод результатов

Наконец, мы проходим по коллекции и выводим человекочитаемый отчет:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Ожидаемый вывод в консоль

Предположим, что `letter_with_typos.png` содержит предложение:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Запуск демо‑примера выдаст примерно следующее:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Обратите внимание, как каждая опечатка сопоставлена с несколькими правдоподобными исправлениями — именно то, что нужно при построении удобного пользовательского интерфейса исправления.

## Полный рабочий пример

Ниже представлена **полная, готовая к копированию** программа. Замените `YOUR_DIRECTORY` реальным путём к вашему файлу изображения.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Возможные граничные случаи**  
> - **Empty Image:** Если OCR‑движок возвращает пустую строку, `spellChecker.Check` просто вернёт пустую коллекцию — без сбоя.  
> - **Non‑English Text:** Замените `OcrLanguage.English` на `OcrLanguage.French` (или любой поддерживаемый язык), чтобы **detect misspelled words** в других локалях.  
> - **Large Documents:** Для многостраничных PDF вы будете проходить по каждой странице, выполнять OCR, а затем агрегировать результаты перед проверкой орфографии.

## Визуальный обзор (Alt‑текст изображения)

![Схема, показывающая поток выполнения OCR на изображении, извлечение текста из изображения и последующее обнаружение орфографических ошибок с предложениями исправлений](perform-ocr-on-image-flow.png)

*Эта схема иллюстрирует сквозной конвейер: изображение → OCR‑движок → необработанный текст → проверка орфографии → предложения.*

## Часто задаваемые вопросы и профессиональные советы

| Question | Answer |
|----------|--------|
| **Нужен ли мне доступ к интернету?** | Нет. Aspose.OCR работает полностью локально; идеально подходит для офлайн‑режима или защищённых окружений. |
| **Насколько точен проверщик орфографии?** | Он использует словарь из ~150 000 английских слов и нечеткое сопоставление, поэтому большинство распространённых опечаток обнаруживаются. |
| **Могу ли я настроить словарь?** | Да. `SpellChecker.AddUserDictionary("custom.txt")` позволяет загрузить термины, специфичные для домена (например, названия продуктов). |
| **Что делать, если изображение наклонено?** | OCR‑движок автоматически определяет ориентацию, но в сложных случаях можно вручную вызвать `ocrEngine.ImagePreprocessing.Rotate(angle)`. |
| **Можно ли подсветить предложения в пользовательском интерфейсе?** | После получения коллекции `misspellings` вы можете сопоставить каждое `entry.Word` с его позицией в `ocrResult.Text` и подчеркнуть его в RichTextBox или веб‑просмотре. |

## Заключение

Мы только что продемонстрировали вам **how to perform OCR on image**, **extract text from image**, а затем **detect misspelled words**, получая **get spelling suggestions** — всё это с помощью компактного консольного приложения C#. Основная идея проста: позволить Aspose.OCR выполнить тяжёлую работу по распознаванию символов, а затем встроенному проверщику орфографии очистить вывод. Отсюда вы можете расширить демонстрацию до полноценного сервиса обработки документов, интегрировать его с веб‑API или подключить к настольному редактору.

Готовы к следующему шагу? Попробуйте переключить язык на испанский, обработать многостраничный PDF или создать небольшое WPF‑приложение, позволяющее пользователям кликать по слову, чтобы принять предложение. Основные блоки уже готовы — остаётся только экспериментировать.

Если вы столкнулись с проблемами или у вас есть идеи для расширений, оставьте комментарий ниже. Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}