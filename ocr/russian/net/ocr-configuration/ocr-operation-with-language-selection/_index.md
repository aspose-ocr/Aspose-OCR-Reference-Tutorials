---
date: 2026-02-25
description: Узнайте, как извлекать текст из изображений на C# с помощью Aspose.OCR
  для .NET. Это пошаговое руководство демонстрирует многоязычное OCR, выбор языка
  и практические советы.
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: Извлечение текста из изображения на C# с выбором языка с использованием Aspose.OCR
url: /ru/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR

## Введение

Если вам нужно **extract image text C#** из фотографий и PDF в .NET‑приложении, Aspose.OCR для .NET предлагает быстрое, точное и учитывающее язык решение. В этом руководстве мы пройдём реальный пример, демонстрирующий распознавание изображений OCR с выбором языка, чтобы вы могли извлекать многоязычный текст из изображений всего несколькими строками кода. К концу вы увидите, как легко интегрировать OCR в ваши C#‑проекты и почему такой подход является надёжным выбором для производственных нагрузок.

## Быстрые ответы
- **Что делает Aspose.OCR?** Он распознает печатный и рукописный текст на изображениях и возвращает извлечённый текст.  
- **Могу ли я выбрать язык?** Да — вы можете указать любой поддерживаемый язык, например English, German, Spanish, Chinese и т.д.  
- **Нужна ли лицензия для разработки?** Бесплатная пробная версия подходит для оценки; лицензия требуется для использования в продакшене.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Автоматически ли исправляется наклон?** Вы можете включить `AutoSkew` и точно настроить параметр `SkewAngle`.  

## Что такое “extract image text C#”?

Извлечение текста из изображения в C# означает использование библиотеки для чтения визуального содержимого изображения (PNG, JPEG, TIFF и т.д.) и преобразования его в поисковый, редактируемый текст. Aspose.OCR предоставляет эту возможность локально, без отправки данных во внешние сервисы, что сохраняет ваш рабочий процесс безопасным и соответствующим требованиям.

## Почему стоит выбрать Aspose.OCR для задач OCR?

- **Высокая точность** при работе с разными шрифтами и качеством изображений.  
- **Встроенный выбор языка** устраняет необходимость во внешних языковых пакетах.  
- **Простой API**, который легко интегрируется в существующие C# проекты, делая процесс **extract image text C#** простым.  
- **Нет внешних зависимостей** — всё работает локально, обеспечивая безопасность ваших данных.  

## Предварительные требования

Перед тем как перейти к коду, убедитесь, что у вас есть следующие требования:

- Aspose.OCR for .NET: Убедитесь, что библиотека Aspose.OCR установлена. Вы можете скачать её со страницы [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).

- Development Environment: Настройте рабочую среду с .NET приложением. Если вы ещё этого не сделали, обратитесь к [documentation](https://reference.aspose.com/ocr/net/) для подробных инструкций.

## Импорт пространств имён

В вашем .NET‑приложении начните с импорта необходимых пространств имён:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Шаг 1: Инициализация Aspose.OCR

Начните с создания экземпляра класса Aspose.OCR. Это подготовит основу для использования возможностей OCR в вашем приложении.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Шаг 2: Указание пути к изображению

Далее определите путь к изображению, которое нужно распознать. Убедитесь, что изображение доступно вашему приложению.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Шаг 3: Распознавание изображения с выбором языка

Теперь происходит основная операция OCR. Используйте библиотеку Aspose.OCR для распознавания текста из указанного изображения. Настройте параметры распознавания, включая выбор языка, чтобы оптимизировать процесс **extract image text C#**.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Шаг 4: Вывод и отображение результатов

После операции OCR выведите и отобразите результаты, включая распознанный текст, области, предупреждения и представление в формате JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Распространённые проблемы и советы

- **Неправильный выбор языка** — Если вывод выглядит искажённым, проверьте, что свойство `Language` соответствует языку исходного изображения.  
- **Искажённые изображения** — Включите `AutoSkew` или вручную отрегулируйте `SkewAngle` для лучшей точности при наклонных сканах.  
- **Большие файлы** — Обрабатывайте большие изображения порциями или уменьшайте разрешение перед передачей в `RecognizeImage`, чтобы экономить память.  

## Часто задаваемые вопросы

**Q: Подходит ли Aspose.OCR для распознавания многоязычного текста?**  
A: Да, Aspose.OCR поддерживает различные языки, обеспечивая гибкость для многоязычных задач OCR.

**Q: Можно ли точно настроить параметры OCR для конкретных характеристик изображения?**  
A: Абсолютно! Регулируйте такие параметры, как угол наклона, распознавание строк и обнаружение областей, чтобы оптимизировать OCR под разные сценарии.

**Q: Где можно найти дополнительную поддержку или обсуждения в сообществе?**  
A: Посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) для получения поддержки и общения с сообществом.

**Q: Доступна ли бесплатная пробная версия?**  
A: Да, изучите [free trial](https://releases.aspose.com/) чтобы оценить возможности Aspose.OCR.

**Q: Как приобрести Aspose.OCR для .NET?**  
A: Для покупки перейдите на [purchase page](https://purchase.aspose.com/buy).

## Заключение

Поздравляем! Вы узнали **how to extract image text C#** с выбором языка, используя Aspose.OCR для .NET. Это руководство показало, как настроить движок OCR, выбрать подходящий язык и обработать результаты, предоставив вам прочную основу для создания функций многоязычного извлечения текста в ваших приложениях.

---

**Last Updated:** 2026-02-25  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}