---
title: Получите выбор для распознанных символов в распознавании изображений OCR
linktitle: Получите выбор для распознанных символов в распознавании изображений OCR
second_title: Aspose.OCR .NET API
description: Усовершенствуйте свои .NET-приложения с помощью Aspose.OCR для точного распознавания символов. Следуйте нашему пошаговому руководству, чтобы получить варианты выбора распознанных символов при распознавании изображений.
weight: 10
url: /ru/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получите выбор для распознанных символов в распознавании изображений OCR

## Введение

Раскрытие возможностей оптического распознавания символов (OCR) имеет решающее значение в современную цифровую эпоху, и Aspose.OCR для .NET выделяется как надежное решение для точного распознавания символов. В этом уроке мы углубимся в конкретную функцию: получение вариантов выбора для распознанных символов. К концу этого руководства вы сможете легко интегрировать эту функциональность в свои приложения .NET.

## Предварительные условия

Прежде чем приступить к изучению руководства, убедитесь, что у вас есть следующие предварительные условия:

- Базовые знания разработки на C# и .NET.
- Visual Studio установлена на вашем компьютере.
-  Библиотека Aspose.OCR для .NET, которую вы можете скачать[здесь](https://releases.aspose.com/ocr/net/).

## Импортировать пространства имен

В вашем проекте C# начните с импорта необходимых пространств имен:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Шаг 1. Инициализируйте Aspose.OCR

Начните с инициализации экземпляра Aspose.OCR:

```csharp
// Путь к каталогу документов.
string dataDir = "Your Document Directory";

// Инициализировать экземпляр AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Шаг 2. Укажите путь к изображению

Укажите путь к изображению, которое вы хотите проанализировать:

```csharp
//Путь к изображению
string fullPath = dataDir + "sample.png";
```

## Шаг 3: Распознайте изображение

Выполните процесс распознавания изображений:

```csharp
// Распознать изображение
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Настройки по умолчанию или пользовательские настройки
});
```

## Шаг 4. Получите выбор для узнаваемых персонажей

Получить варианты выбора для распознанных символов:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Шаг 5: Распечатайте результаты

Отобразите текст распознавания и варианты выбора:

```csharp
// Распечатать результат
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

Повторите эти шаги, настроив их в соответствии с требованиями вашего приложения.

## Заключение

В этом руководстве мы рассмотрели, как использовать Aspose.OCR для .NET для получения вариантов выбора распознаваемых символов при распознавании изображений. Эта функция добавляет новое измерение к возможностям оптического распознавания символов, повышая универсальность ваших приложений.

## Часто задаваемые вопросы

### Вопрос 1. Подходит ли Aspose.OCR для .NET для крупномасштабной обработки документов?

А1: Абсолютно! Aspose.OCR для .NET предназначен для эффективной и точной обработки больших объемов документов.

### Вопрос 2. Могу ли я использовать Aspose.OCR для .NET в веб-приложении?

О2: Да, вы можете интегрировать Aspose.OCR для .NET в веб-приложения, что делает его универсальным для различных сценариев разработки.

### Вопрос 3. Существуют ли какие-либо варианты лицензирования для Aspose.OCR для .NET?

 О3: Да, вы можете изучить варианты лицензирования и совершить покупку.[здесь](https://purchase.aspose.com/buy).

### Вопрос 4: Как я могу получить поддержку или задать вопросы об Aspose.OCR для .NET?

 А4: Посетите[Форум Aspose.OCR](https://forum.aspose.com/c/ocr/16) чтобы получить поддержку, задать вопросы и связаться с сообществом.

### Вопрос 5: Существует ли бесплатная пробная версия Aspose.OCR для .NET?

 О5: Да, вы можете получить доступ к бесплатной пробной версии.[здесь](https://releases.aspose.com/) чтобы испытать возможности Aspose.OCR для .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
