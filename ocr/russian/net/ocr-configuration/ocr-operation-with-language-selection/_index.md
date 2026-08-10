---
date: 2026-07-23
description: Узнайте, как библиотека OCR для .NET извлекает текст из изображения C#
  с помощью Aspose.OCR. Это руководство охватывает многоязычный OCR, выбор языка и
  практические советы.
keywords:
- ocr library for .net
- extract image text c#
- Aspose.OCR
- multilingual OCR
lastmod: 2026-07-23
linktitle: Извлечение текста из изображения C# с выбором языка с использованием Aspose.OCR
og_description: Библиотека OCR для .NET позволяет извлекать текст из изображения C#
  с помощью Aspose.OCR. Получите многоязычный OCR, выбор языка и пошаговые примеры
  кода.
og_image_alt: 'Guide: Extract image text C# using Aspose.OCR OCR library for .NET'
og_title: Библиотека OCR для .NET – Извлечение текста из изображения C#
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how the ocr library for .net extracts image text C# using Aspose.OCR.
    This guide covers multilingual OCR, language selection, and practical tips.
  headline: ocr library for .net – Extract image text C#
  type: TechArticle
- questions:
  - answer: Yes, Aspose.OCR supports over 30 languages, providing flexibility for
      multilingual OCR tasks.
    question: Is Aspose.OCR suitable for multilingual text recognition?
  - answer: Absolutely! Adjust parameters like `AutoSkew`, `SkewAngle`, and `LineDetectionMode`
      to optimise results for different scenarios.
    question: Can I fine‑tune OCR settings for specific image characteristics?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support
      and discussions with the community.
    question: Where can I find additional support or community discussions?
  - answer: Yes, explore the [free trial](https://releases.aspose.com/) to experience
      the capabilities of Aspose.OCR.
    question: Is there a free trial available?
  - answer: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).
    question: How can I purchase Aspose.OCR for .NET?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr library
- Aspose.OCR
- C# OCR
- image text extraction
title: Библиотека OCR для .NET – Извлечение текста из изображения C#
url: /ru/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения C# с выбором языка с использованием Aspose.OCR

## Введение

Если вам нужно **извлечение текста из изображения C#** из фотографий или PDF‑файлов в .NET‑приложении, Aspose.OCR — мощная **ocr library for .net**, обеспечивающая быструю, точную и учитывающую язык распознавание. В этом руководстве мы пройдём реальный пример, демонстрирующий OCR‑распознавание изображений с выбором языка, чтобы вы могли получать многоязычный текст из изображений всего несколькими строками кода. К концу вы поймёте, почему такой подход надёжен для производственных нагрузок и насколько легко интегрировать OCR в ваши C#‑проекты.

## Быстрые ответы
- **What does Aspose.OCR do?** Он распознаёт печатный и рукописный текст на изображениях и возвращает извлечённый текст.  
- **Can I choose the language?** Да — вы можете указать любой поддерживаемый язык, например English, German, Spanish, Chinese и т.д.  
- **Do I need a license for development?** Бесплатная пробная версия подходит для оценки; для использования в продакшене требуется лицензия.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Is skew correction automatic?** Вы можете включить `AutoSkew` и точно настроить параметр `SkewAngle`.  

`AutoSkew` автоматически обнаруживает и исправляет наклон изображения. `SkewAngle` позволяет вручную задать угол вращения.

## Что такое «извлечение текста из изображения C#»?

Извлечение текста из изображения в C# — это использование библиотеки для чтения визуального содержимого изображения (PNG, JPEG, TIFF и т.п.) и преобразования его в поисковый, редактируемый текст. **ocr library for .net** Aspose.OCR выполняет это преобразование локально, сохраняя данные на месте и избегая внешних сервисных вызовов.

## Почему стоит выбрать Aspose.OCR для OCR‑задач?

Aspose.OCR обеспечивает **95 %+ accuracy** на стандартных печатных шрифтах и может обрабатывать **up to 300 pages per minute** на типичном сервере с частотой 2.5 GHz, что делает её одной из самых быстрых **ocr library for .net** решений. В комплекте также идут встроенные языковые пакеты, поэтому сторонние ресурсы не требуются, а работа полностью офлайн обеспечивает максимальную безопасность.

## Требования

Прежде чем перейти к коду, убедитесь, что у вас есть следующие обязательные условия:

- Aspose.OCR for .NET: Убедитесь, что библиотека Aspose.OCR установлена. Вы можете скачать её со страницы [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).

- Development Environment: Настройте рабочую среду с .NET‑приложением. Если вы ещё этого не сделали, обратитесь к [documentation](https://reference.aspose.com/ocr/net/) для получения подробных инструкций.

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

`OcrEngine` — основной класс Aspose.OCR, выполняющий оптическое распознавание символов на изображениях. Начните с создания экземпляра этого класса; это подготовит основу для всех последующих OCR‑операций.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Шаг 2: Указание пути к изображению

Определите абсолютный или относительный путь к изображению, которое нужно обработать. Путь должен указывать на читаемый файл; иначе движок выбросит исключение.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Шаг 3: Распознавание изображения с выбором языка

`RecognizeImage` — метод, который сканирует переданный bitmap, применяет языковые модели и возвращает объект `RecognitionResult`, содержащий извлечённый текст. Установив свойство `Language`, вы указываете движку, какие лингвистические правила применять, что существенно повышает точность для контента не на английском.

Свойство `Language` выбирает модель OCR‑языка, которую следует использовать.

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

После OCR‑операции вы можете получить распознанный текст, ограничительные рамки для каждого слова, любые предупреждения и даже JSON‑дамп для дальнейшей обработки.

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

## Как извлечь текст из изображения C# с выбором языка?

Загрузите изображение с помощью `new OcrEngine()` и задайте `engine.Language = Language.English` (или любой поддерживаемый язык) перед вызовом `engine.RecognizeImage(imagePath)`. Метод возвращает полный текст в виде одной строки, которую вы затем можете вывести, сохранить или передать в другие сервисы. Такой двухшаговый шаблон работает со всеми поддерживаемыми языками и не требует внешних зависимостей.

## Распространённые проблемы и советы

- **Incorrect language selection** – Если вывод выглядит искажённым, дважды проверьте, что свойство `Language` соответствует языку исходного изображения.  
- **Skewed images** – Включите `AutoSkew` или вручную отрегулируйте `SkewAngle` для повышения точности при наклонных сканах.  
- **Large files** – Обрабатывайте большие изображения порциями или уменьшайте разрешение перед передачей их в `RecognizeImage`, чтобы экономить память.  

## Часто задаваемые вопросы

**Q: Is Aspose.OCR suitable for multilingual text recognition?**  
A: Да, Aspose.OCR поддерживает более 30 языков, обеспечивая гибкость для многоязычных OCR‑задач.

**Q: Can I fine‑tune OCR settings for specific image characteristics?**  
A: Абсолютно! Регулируйте параметры такие как `AutoSkew`, `SkewAngle` и `LineDetectionMode` для оптимизации результатов в разных сценариях.

**Q: Where can I find additional support or community discussions?**  
A: Посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) для получения поддержки и обсуждения с сообществом.

**Q: Is there a free trial available?**  
A: Да, ознакомьтесь с [free trial](https://releases.aspose.com/) чтобы оценить возможности Aspose.OCR.

**Q: How can I purchase Aspose.OCR for .NET?**  
A: Для покупки перейдите на [purchase page](https://purchase.aspose.com/buy).

## Заключение

Поздравляем! Вы узнали **как извлечь текст из изображения C#** с выбором языка, используя Aspose.OCR для .NET. Это руководство показало, как настроить OCR‑движок, выбрать подходящий язык и обработать результаты, предоставив вам прочную основу для создания многоязычных функций извлечения текста в ваших приложениях.

---

**Последнее обновление:** 2026-07-23  
**Тестировано с:** Aspose.OCR 24.11 for .NET  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [recognize text image with Aspose OCR for multiple languages](/ocr/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Images – OCR Settings with Aspose.OCR](/ocr/net/ocr-settings/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}