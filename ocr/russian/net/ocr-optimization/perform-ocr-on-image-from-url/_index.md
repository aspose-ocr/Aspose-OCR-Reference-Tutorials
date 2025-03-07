---
title: Выполните распознавание изображения по URL-адресу в распознавании изображений OCR.
linktitle: Выполните распознавание изображения по URL-адресу в распознавании изображений OCR.
second_title: Aspose.OCR .NET API
description: Изучите бесшовную интеграцию OCR с Aspose.OCR для .NET. Точно распознавайте текст на изображениях.
weight: 10
url: /ru/net/ocr-optimization/perform-ocr-on-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполните распознавание изображения по URL-адресу в распознавании изображений OCR.

## Введение

В области оптического распознавания символов (OCR) Aspose.OCR для .NET выделяется как мощный инструмент, который позволяет разработчикам точно извлекать текстовый контент из изображений. Если вы хотите интегрировать возможности оптического распознавания текста в свое .NET-приложение и без труда выполнять распознавание текста, это пошаговое руководство проведет вас через процесс оптического распознавания изображений по URL-адресу.

## Предварительные условия

Прежде чем углубляться в руководство, убедитесь, что у вас есть следующие предварительные условия:

-  Aspose.OCR для .NET: убедитесь, что библиотека Aspose.OCR интегрирована в ваш проект .NET. Вы можете скачать его с сайта[страница выпуска](https://releases.aspose.com/ocr/net/).

- Среда разработки: на вашем компьютере должна быть установлена работающая среда разработки .NET.

## Импортировать пространства имен

В свой проект .NET включите необходимые пространства имен для доступа к функциям Aspose.OCR. Добавьте в свой проект следующий фрагмент кода:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Шаг 1. Настройте каталог документов

 Начните с указания каталога, в котором хранятся ваши документы. Заменять`"Your Document Directory"` с фактическим путем к вашим документам.

```csharp
string dataDir = "Your Document Directory";
```

## Шаг 2. Получите изображение для распознавания

Укажите URL-адрес изображения, для которого вы хотите выполнить распознавание текста. Убедитесь, что изображение общедоступно.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## Шаг 3: Инициализируйте AsposeOcr

Создайте экземпляр класса AsposeOcr для доступа к функциям OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Шаг 4: Распознайте изображение

Используйте библиотеку Aspose.OCR для распознавания текста по указанному URL-адресу изображения. Настройте параметры распознавания в соответствии с вашими требованиями.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Шаг 5: Распечатайте результат

Отобразите результат распознавания, включая распознанный текст, области и любые предупреждения.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Шаг 6. Выполните и проверьте

Запустите приложение, и если все настроено правильно, вы должны увидеть успешное выполнение процесса OCR.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Заключение

Благодаря Aspose.OCR для .NET интеграция возможностей OCR в ваши .NET-приложения становится простой задачей. Это руководство провело вас через процесс оптического распознавания изображения по URL-адресу, предоставив вам основу для использования возможностей распознавания текста в ваших проектах.

## Часто задаваемые вопросы

### Вопрос 1. Подходит ли Aspose.OCR для работы с несколькими языками?

О1: Да, Aspose.OCR поддерживает распознавание текста на разных языках, что делает его универсальным для международных приложений.

### Вопрос 2: Могу ли я использовать Aspose.OCR для распознавания как однострочного, так и многострочного текста?

А2: Абсолютно! Aspose.OCR обеспечивает гибкость распознавания как однострочного, так и многострочного текста, адаптируясь к вашему конкретному сценарию использования.

### Вопрос 3. Существуют ли какие-либо варианты лицензирования для Aspose.OCR?

 О3: Да, вы можете изучить варианты лицензирования и совершать покупки на[Aspose магазин](https://purchase.aspose.com/buy).

### Вопрос 4: Существует ли бесплатная пробная версия Aspose.OCR?

 О4: Да, вы можете бесплатно опробовать Aspose.OCR, посетив[страница релизов](https://releases.aspose.com/).

### Вопрос 5: Где я могу найти поддержку или обсуждения в сообществе, связанные с Aspose.OCR?

 A5: Посетите[Форум Aspose.OCR](https://forum.aspose.com/c/ocr/16) за поддержку и взаимодействие с сообществом.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
