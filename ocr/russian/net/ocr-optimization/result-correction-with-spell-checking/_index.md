---
title: Коррекция результатов с проверкой орфографии при распознавании изображений OCR
linktitle: Коррекция результатов с проверкой орфографии при распознавании изображений OCR
second_title: Aspose.OCR .NET API
description: Повысьте точность распознавания с помощью Aspose.OCR для .NET. Исправляйте орфографию, настраивайте словари и без труда добивайтесь безошибочного распознавания текста.
weight: 13
url: /ru/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Коррекция результатов с проверкой орфографии при распознавании изображений OCR

## Введение

В сфере оптического распознавания символов (OCR) достижение точных результатов имеет решающее значение для извлечения значимой информации из изображений. Одной из распространенных проблем является работа со словами с ошибками в процессе распознавания. К счастью, Aspose.OCR для .NET предоставляет мощное решение для улучшения результатов распознавания посредством проверки орфографии.

Это руководство проведет вас через процесс исправления результатов с проверкой орфографии с использованием Aspose.OCR для .NET. К концу вы сможете повысить точность текста, полученного с помощью оптического распознавания символов, гарантируя более точный и безошибочный вывод.

## Предварительные условия

Прежде чем мы углубимся в магию проверки орфографии, убедитесь, что у вас есть следующие предварительные условия:

-  Aspose.OCR для библиотеки .NET: загрузите и установите библиотеку Aspose.OCR с сайта[страница выпуска](https://releases.aspose.com/ocr/net/).

- Каталог документов: убедитесь, что у вас есть специальный каталог для ваших документов. Замените «Каталог вашего документа» во фрагментах кода фактическим путем.

## Импортировать пространства имен

Начнем с импорта необходимых пространств имен в ваш .NET-проект:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Шаг 1. Инициализируйте Aspose.OCR

Инициализируйте экземпляр Aspose.OCR, чтобы запустить процесс OCR.

```csharp
// Путь к каталогу документов.
string dataDir = "Your Document Directory";

// Инициализировать экземпляр AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Шаг 2. Распознайте изображение

Затем распознайте текст на изображении с помощью Aspose.OCR. Вот фрагмент, демонстрирующий этот процесс:

```csharp
// Распознать изображение
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Шаг 3: Перед коррекцией

Получите результат OCR перед исправлением, чтобы сравнить его с исправленной версией.

```csharp
// Получить результат
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Шаг 4: После коррекции

Примените проверку орфографии, чтобы получить исправленный результат. Следующий фрагмент кода иллюстрирует этот шаг:

```csharp
// Получить исправленный результат
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Шаг 5. Слова с ошибками и предложения

Получите список слов с ошибками вместе с предлагаемыми исправлениями, используя следующий код:

```csharp
// Получить список слов с ошибками и предложениями
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

## Шаг 6. Исправьте пользовательский текст

Исправьте конкретный предоставленный пользователем текст с помощью библиотеки Aspose.OCR:

```csharp
// Правильный пользовательский текст
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Шаг 7: Исправление с помощью пользовательского словаря

Улучшите коррекцию, включив собственный пользовательский словарь:

```csharp
// Получите исправленный результат с помощью пользовательского словаря
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Заключение

Поздравляем! Вы успешно ознакомились с возможностями Aspose.OCR для .NET по проверке правописания. Эта функция позволяет уточнить результаты оптического распознавания символов, обеспечивая точность и устраняя ошибки.

## Часто задаваемые вопросы

### Вопрос 1: Могу ли я использовать Aspose.OCR для языков, отличных от английского?

О1: Да, Aspose.OCR поддерживает несколько языков. Отрегулируйте языковые настройки соответствующим образом.

### Вопрос 2: Как интегрировать Aspose.OCR в мой проект .NET?

 A2: См.[документация](https://reference.aspose.com/ocr/net/) для получения подробных шагов интеграции.

### Вопрос 3: Существует ли пробная версия Aspose.OCR?

 A3: Да, вы можете изучить функции с помощью[бесплатная пробная версия](https://releases.aspose.com/).

### Вопрос 4. Могу ли я загрузить собственный словарь для проверки орфографии?

А4: Абсолютно! В этом руководстве показано, как улучшить коррекцию с помощью словаря, предоставленного пользователем.

### Вопрос 5: Где я могу получить поддержку для Aspose.OCR?

 A5: Посетите[Форум Aspose.OCR](https://forum.aspose.com/c/ocr/16) за поддержку и руководство сообщества.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
