---
date: 2025-12-25
description: Повышайте точность OCR с помощью Aspose OCR для .NET, используя проверку
  орфографии и поддержку языков для исправления ошибок и настройки словарей, обеспечивая
  безошибочное распознавание текста.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Улучшите точность OCR с помощью проверки орфографии в изображениях
url: /ru/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Повышение точности OCR с помощью проверки орфографии в изображениях

## Введение

Когда вы работаете с оптическим распознаванием символов (OCR), главная цель — **повысить точность OCR**, чтобы извлечённый текст полностью соответствовал оригинальному изображению. Ошибки в написании слов являются частой причиной ошибок, особенно когда исходное изображение шумное или содержит необычные шрифты. Aspose.OCR for .NET предлагает встроенные возможности проверки орфографии, которые не только исправляют эти ошибки, но и позволяют расширять движок пользовательскими словарями. В этом руководстве вы узнаете, как использовать проверку орфографии для улучшения результатов OCR, увидите вывод «до‑и‑после», а также узнаете, как адаптировать процесс исправления под ваши языковые потребности.

## Краткие ответы
- **Что делает проверка орфографии для OCR?** Она автоматически обнаруживает ошибочно написанные слова в выводе OCR и заменяет их на наиболее вероятные правильные варианты.  
- **Какая библиотека предоставляет эту функцию?** Aspose.OCR for .NET включает готовый к использованию API проверки орфографии.  
- **Нужен ли мне доступ к интернету?** Нет, движок проверки орфографии работает полностью офлайн.  
- **Могу ли я добавить свою терминологию?** Да, вы можете предоставить пользовательский словарь для обработки специфических для домена слов.  
- **Какие языки поддерживаются?** См. раздел «aspose ocr language support» для деталей.

## Что такое проверка орфографии в OCR?

Проверка орфографии анализирует необработанный текст, возвращённый движком OCR, определяет токены, которые не совпадают с известными словами в выбранном языковом словаре, и предлагает или применяет исправления. Этот шаг необходим для **повышения точности OCR**, особенно при обработке отсканированных документов, чеков или форм, где OCR может неправильно интерпретировать символы.

## Зачем использовать поддержку языков Aspose OCR?

Aspose.OCR поставляется с обширными языковыми пакетами и позволяет подключать дополнительные словари. Использование **aspose ocr language support** позволяет работать с многоязычными документами без написания собственных парсеров, а также предоставляет доступ к языковым правилам, которые дополнительно повышают качество распознавания.

## Требования

Прежде чем приступить к магии проверки орфографии, убедитесь, что у вас есть следующее:

- Aspose.OCR for .NET Library: Скачайте и установите библиотеку Aspose.OCR со [release page](https://releases.aspose.com/ocr/net/).

- Document Directory: Убедитесь, что у вас есть выделенный каталог для ваших документов. Замените `"Your Document Directory"` в фрагментах кода на фактический путь.

## Импорт пространств имён

Начнём с импорта необходимых пространств имён в вашем .NET проекте:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Шаг 1: Инициализация Aspose.OCR

Инициализируйте экземпляр Aspose.OCR, чтобы запустить процесс OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Шаг 2: Распознавание изображения

Далее распознайте текст на изображении с помощью Aspose.OCR. Ниже приведён фрагмент, демонстрирующий этот процесс:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Шаг 3: До исправления

Получите результат OCR до исправления, чтобы сравнить его с исправленной версией.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Шаг 4: После исправления

Примените проверку орфографии, чтобы получить исправленный результат. Следующий фрагмент кода иллюстрирует этот шаг:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Шаг 5: Ошибочные слова и предложения

Получите список ошибочно написанных слов вместе с предложенными исправлениями, используя следующий код:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Шаг 6: Коррекция пользовательского текста

Исправьте конкретный пользовательский текст с помощью библиотеки Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Шаг 7: Коррекция с пользовательским словарём

Улучшите исправление, включив пользовательский словарь:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Распространённые проблемы и решения

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| Не возвращаются предложения | Пакет языка не загружен или текст слишком короткий. | Убедитесь, что `RecognitionSettings(Language.Eng)` соответствует языку исходного изображения и что результат OCR содержит достаточное количество символов. |
| Пользовательский словарь не применяется | Неправильный путь или формат файла. | Проверьте, что `dictionary.txt` существует по указанному пути и содержит по одному слову в строке. |
| Проверка орфографии замедляет обработку больших документов | Обработка каждого слова отдельно добавляет накладные расходы. | Обрабатывайте страницы пакетами или увеличьте выделение памяти при работе на .NET Core. |

## Часто задаваемые вопросы

### Q1: Могу ли я использовать Aspose.OCR для языков, отличных от английского?

A1: Да, Aspose.OCR поддерживает несколько языков. Настройте параметры языка соответствующим образом.

### Q2: Как интегрировать Aspose.OCR в мой .NET проект?

A2: Обратитесь к [documentation](https://reference.aspose.com/ocr/net/) для подробных шагов интеграции.

### Q3: Есть ли доступна пробная версия Aspose.OCR?

A3: Да, вы можете ознакомиться с функциями с помощью [free trial version](https://releases.aspose.com/).

### Q4: Могу ли я загрузить пользовательский словарь для проверки орфографии?

A4: Абсолютно! В руководстве показано, как улучшить исправление, используя пользовательский словарь.

### Q5: Где я могу получить поддержку по Aspose.OCR?

A5: Посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) для получения поддержки сообщества и рекомендаций.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Последнее обновление:** 2025-12-25  
**Тестировано с:** Aspose.OCR for .NET latest version  
**Автор:** Aspose