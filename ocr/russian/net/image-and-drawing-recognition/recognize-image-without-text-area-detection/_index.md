---
date: 2025-12-18
description: Узнайте, как использовать OCR с Aspose.OCR для .NET, чтобы извлекать
  текст из PNG‑изображений без обнаружения текстовых областей.
linktitle: Recognize Image without Text Area Detection in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 'Как использовать OCR: распознавать изображение без обнаружения текстовой области'
url: /ru/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR: Распознавание изображения без обнаружения текстовых областей

## Введение

Оптическое распознавание символов (OCR) стало важной технологией для преобразования визуального текста в поисковые, редактируемые данные. Если вы задаётесь вопросом **how to use OCR** в проекте .NET, это руководство покажет вам пошагово, как распознать изображение без использования обнаружения текстовых областей. К концу урока вы сможете **extract text from PNG** файлы быстро, используя Aspose.OCR for .NET.

## Быстрые ответы
- **What does “without text area detection” mean?** OCR‑движок читает всё изображение, а не сначала ищет текстовые блоки.  
- **Which library is required?** Aspose.OCR for .NET (доступна бесплатная пробная версия).  
- **Supported image formats?** PNG, JPEG, BMP, GIF, TIFF и другие.  
- **Do I need a license for development?** Временная или пробная лицензия подходит для тестирования; полная лицензия требуется для продакшн.  
- **Typical execution time?** Несколько сотен миллисекунд для стандартного PNG 300 × 200 px.

## Что такое распознавание изображений OCR?

Распознавание изображений OCR относится к процессу анализа растровых изображений и преобразования обнаруженных символов в машинно‑читаемый текст. С помощью Aspose.OCR вы можете выполнять это преобразование непосредственно в вашем C# коде, что делает его идеальным для таких сценариев, как обработка счетов, архивирование документов или извлечение подписей из скриншотов.

## Почему использовать Aspose.OCR для .NET?

- **No external dependencies** – чистая .NET библиотека.  
- **High accuracy** для печатного и рукописного текста.  
- **Simple API** позволяет сосредоточиться на бизнес‑логике, а не на предобработке изображений.  
- **Full control** – вы можете включать или отключать обнаружение текстовых областей по необходимости.

## Предварительные требования

Перед тем как погрузиться в код, убедитесь, что у вас есть следующее:

1. **Aspose.OCR for .NET** – скачайте и установите библиотеку с официального сайта [here](https://releases.aspose.com/ocr/net/).  
2. **Sample image** – PNG‑файл (например, `sample.png`), содержащий текст, который вы хотите извлечь.  
3. **.NET development environment** – Visual Studio, Rider или любой IDE, поддерживающий C#.

## Импорт пространств имён

В вашем .NET приложении импортируйте необходимые пространства имён для доступа к функционалу Aspose.OCR. Добавьте следующие строки в начало вашего файла кода:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Шаг 1: Установите каталог документов

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на фактический путь к папке, где находится `sample.png`.

## Шаг 2: Инициализируйте Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Это создаёт объект `AsposeOcr`, который даёт вам доступ ко всем методам OCR.

## Шаг 3: Распознайте изображение

```csharp
// Recognize image
string result = api.RecognizeImage(dataDir + "sample.png", false);
```

Флаг `false` сообщает движку **not to perform text area detection**, поэтому он обрабатывает всё изображение за один проход. Это полезно, когда макет изображения простой или когда нужно захватить каждый символ.

## Шаг 4: Отобразите распознанный текст

```csharp
// Display the recognized text
Console.WriteLine(result);
```

Извлечённый текст появляется в консоли. Теперь вы можете сохранить его, выполнить поиск или передать в другой рабочий процесс.

## Шаг 5: Завершите выполнение

```csharp
Console.WriteLine("RecognizeImageWithoutTextAreaDetection executed successfully");
```

Дружелюбное подтверждение сообщает, что операция OCR завершилась без ошибок.

## Общие сценарии использования

- **Batch processing of scanned receipts** где каждый чек – отдельное изображение.  
- **Automated data entry** из скриншотов форм с фиксированным макетом.  
- **Extracting captions** из изображений продуктов для каталогов электронной коммерции.  

## Устранение неполадок и советы

- **Ensure the image is clear** – низкое разрешение или сильно сжатые PNG могут снижать точность.  
- **If you need higher speed**, рассмотрите возможность включения обнаружения текстовых областей (установите второй параметр в `true`).  
- **For multilingual text**, настройте свойство `Language` у экземпляра `AsposeOcr` перед вызовом `RecognizeImage`.  

## Часто задаваемые вопросы

### Q1: Совместим ли Aspose.OCR со всеми форматами изображений?

A1: Aspose.OCR поддерживает различные форматы изображений, включая PNG, JPEG, GIF и BMP. См. [documentation](https://reference.aspose.com/ocr/net/) для полного списка.

### Q2: Могу ли я использовать Aspose.OCR для настольных и веб‑приложений?

A2: Да, Aspose.OCR for .NET одинаково хорошо работает в настольных, веб‑ и облачных .NET приложениях.

### Q3: Доступна ли бесплатная пробная версия Aspose.OCR?

A3: Конечно. Вы можете скачать бесплатную пробную версию [here](https://releases.aspose.com/) для оценки библиотеки перед покупкой.

### Q4: Как получить техническую поддержку Aspose.OCR?

A4: Посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16), чтобы задать вопросы и пообщаться с сообществом.

### Q5: Доступны ли временные лицензии для Aspose.OCR?

A5: Да, вы можете получить временную лицензию [here](https://purchase.aspose.com/temporary-license/) для краткосрочного тестирования или оценки.

## Дополнительные часто задаваемые вопросы

**Q: Как я могу **how to recognize text** из многостраничного PDF?**  
A: Преобразуйте каждую страницу PDF в изображение (например, PNG) и запустите тот же метод `RecognizeImage` для каждой страницы.

**Q: Поддерживает ли Aspose.OCR **text extraction .net** для рукописных заметок?**  
A: Движок включает распознавание рукописного текста, но результаты зависят от качества изображения и разборчивости почерка.

**Q: Какой лучший способ **extract text from png** файлов в массовом порядке?**  
A: Напишите цикл, который перечисляет все PNG‑файлы в папке, вызывает `RecognizeImage` для каждого и сохраняет результат в CSV или базу данных.

**Q: Могу ли я настроить OCR‑движок для повышения точности для конкретного шрифта?**  
A: Да, вы можете тонко настроить распознавание, задав свойства `Language` и `RecognitionOptions` у экземпляра `AsposeOcr`.

## Заключение

Следуя этим шагам, вы теперь знаете **how to use OCR** в среде .NET для **recognize image sample** файлов без использования обнаружения текстовых областей. Этот подход дает вам полный контроль над процессом OCR и открывает возможности для множества сценариев автоматизации, от обработки счетов до индексации контента.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-18  
**Tested With:** Aspose.OCR for .NET 24.11  
**Author:** Aspose