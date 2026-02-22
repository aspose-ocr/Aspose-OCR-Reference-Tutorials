---
date: 2026-02-22
description: Узнайте, как выполнять OCR изображения и извлекать текст из него с помощью
  Aspose.OCR для .NET. Это пошаговое руководство покажет, как быстро преобразовать
  изображение в текст.
linktitle: Perform OCR on Image in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Как выполнить OCR изображения – Выполнить OCR на изображении в распознавании
  изображений
url: /ru/net/image-and-drawing-recognition/perform-ocr-on-image/
weight: 14
---

top-button >}}

Make sure to keep placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR изображения – Выполнение OCR на изображении в распознавании изображений

## Introduction

В современных приложениях вопрос **how to OCR image** часто задают разработчики, которым нужно превратить отсканированные документы, скриншоты или фотографии в поисковый, редактируемый текст. Aspose.OCR for .NET предоставляет мощный, простой в использовании API, который позволяет **extract image text**, **convert image to text** и **recognize image text** всего несколькими строками кода. В этом руководстве мы пройдем весь процесс — от настройки библиотеки до отображения распознанного текста — чтобы вы могли интегрировать возможности OCR в свои проекты на C# за считанные минуты.

## Quick Answers
- **Какую библиотеку использовать?** Aspose.OCR for .NET
- **Можно ли обрабатывать PNG, JPEG и TIFF?** Да, поддерживаются все распространённые форматы изображений
- **Требуется ли лицензия для продакшн?** Да, для использования в продакшн необходима коммерческая лицензия
- **Какие версии .NET совместимы?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6
- **Сколько времени занимает базовый вызов OCR?** Обычно менее секунды для изображения стандартного размера

## What is OCR Image Text Extraction?

OCR (Optical Character Recognition) image text extraction — это процесс анализа растрового изображения, идентификации символов и вывода их в виде редактируемого текста. Эта техника лежит в основе всего, от поисковых PDF до автоматического ввода данных с чеков.

## Why Choose Aspose.OCR as Your C# OCR Library?

- **Высокая точность** — встроенные языковые модели дают надёжные результаты даже при сканах низкого качества.  
- **Широкая поддержка форматов** — работает с PNG, JPEG, BMP, TIFF и другими, упрощая **convert image to text** независимо от источника.  
- **Отсутствие внешних зависимостей** — чистая .NET‑библиотека; не требуется установка нативных OCR‑движков.  
- **Расширяемость** — можно тонко настраивать параметры распознавания или интегрировать с другими продуктами Aspose для сквозных документооборотных процессов.

## Prerequisites

Перед тем как приступить к коду, убедитесь, что у вас есть:

1. **Aspose.OCR for .NET Library** — скачайте и установите её по [download link](https://releases.aspose.com/ocr/net/).  
2. **Среда разработки** — любой IDE, совместимый с .NET (Visual Studio, Rider, VS Code и т.д.).  
3. **Пример изображения** — для этого руководства будем использовать `sample.png`, размещённый в любой папке по вашему выбору.

## Import Namespaces

First, add the required namespaces so the compiler knows where to find the OCR classes:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## How to OCR Image using Aspose.OCR for .NET

Below is the end‑to‑end workflow broken into clear, numbered steps. Each step includes a short explanation followed by the exact code you need to copy.

### Step 1: Specify the Document Directory

```csharp
string dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на абсолютный или относительный путь, содержащий `sample.png`. Это указывает API, где искать изображение для обработки.

### Step 2: Initialize Aspose.OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

Создание экземпляра `AsposeOcr` даёт доступ ко всем методам OCR, таким как `RecognizeImage`.

### Step 3: Recognize Image

```csharp
string result = api.RecognizeImage(dataDir + "sample.png");
```

Метод `RecognizeImage` читает файл изображения и возвращает извлечённый текст в виде строки. Здесь происходит основная работа — **recognize image text**.

### Step 4: Display Recognized Text

```csharp
Console.WriteLine(result);
```

Вы можете вывести результат в консоль, записать его в файл или передать другому компоненту для дальнейшей обработки.

### Step 5: Finalize the Process

```csharp
Console.WriteLine("PerformOCROnImage executed successfully");
```

Простое сообщение подтверждения помогает убедиться, что вызов OCR завершился без исключений.

## Convert Image to Text .NET – Additional Tips

- **Используйте `Path.Combine`** для безопасного построения путей к файлам на разных платформах.  
- **Установите язык** при обработке текста не на английском: `api.Language = "eng";` (или соответствующий ISO‑код).  
- **Отрегулируйте качество изображения** предварительной обработкой (масштабирование, бинаризация) для повышения точности при сканах низкого разрешения.

## Common Issues & Troubleshooting

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| Возврат пустой строки | Неправильный путь к изображению или файл не найден | Проверьте `dataDir` и имя файла; используйте `Path.Combine` для безопасности |
| Искажённые символы | Разрешение изображения слишком низкое или язык не поддерживается | Используйте изображение с более высоким разрешением; задайте параметры языка через `api.Language = "eng"` |
| Исключение `System.IO.FileNotFoundException` | Отсутствует `sample.png` | Убедитесь, что файл существует в указанной папке |

## Frequently Asked Questions

**Q: Может ли Aspose.OCR обрабатывать несколько форматов изображений?**  
A: Да, поддерживается широкий спектр форматов, поэтому вы можете **extract image text** из PNG, JPEG, BMP, TIFF и других.

**Q: Доступна ли временная лицензия для тестирования?**  
A: Абсолютно. Вы можете запросить 30‑дневную оценочную лицензию через портал Aspose.

**Q: Где найти полную документацию по Aspose.OCR for .NET?**  
A: Официальное руководство находится в [Aspose.OCR documentation](https://reference.aspose.com/ocr/net/).

**Q: Как получить поддержку или связаться с сообществом?**  
A: Посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16), чтобы задать вопросы и поделиться опытом.

**Q: Можно ли бесплатно опробовать Aspose.OCR for .NET перед покупкой?**  
A: Да, полностью функциональная **free trial** доступна на странице [free trial](https://releases.aspose.com/).

## Conclusion

Следуя приведённым выше шагам, вы теперь знаете **how to OCR image** файлы с помощью Aspose.OCR for .NET. Независимо от того, создаёте ли вы систему управления документами, приложение для обработки чеков или любое решение, которому необходимо **convert image to text**, эта библиотека предоставляет простой, высокопроизводительный путь превращения визуальных данных в поисковый контент.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR for .NET 24.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}