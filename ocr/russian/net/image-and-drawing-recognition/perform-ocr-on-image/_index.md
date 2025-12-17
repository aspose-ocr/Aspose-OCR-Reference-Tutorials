---
date: 2025-12-17
description: Узнайте, как выполнять OCR изображений и извлекать текст из изображений
  с помощью Aspose.OCR для .NET. Этот пошаговый руководствo покажет, как быстро преобразовать
  изображение в текст.
linktitle: Perform OCR on Image in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Как выполнить OCR изображения – Выполнить OCR изображения в распознавании изображений
url: /ru/net/image-and-drawing-recognition/perform-ocr-on-image/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR изображения – Выполнить OCR на изображении в распознавании изображений

## Введение

В современных приложениях **how to ocr image** — это частый вопрос у разработчиков, которым необходимо преобразовать отсканированные документы, скриншоты или фотографии в поисковый, редактируемый текст. Aspose.OCR for .NET предоставляет мощный, простой в использовании API, который позволяет **extract image text**, **convert image to text** и **recognize image text** всего несколькими строками кода. В этом руководстве мы пройдем весь процесс — от настройки библиотеки до отображения распознанного текста — чтобы вы могли интегрировать возможности OCR в свои проекты на C# за считанные минуты.

## Быстрые ответы
- **Какую библиотеку использовать?** Aspose.OCR for .NET
- **Можно ли обрабатывать PNG, JPEG и TIFF?** Yes, all common image formats are supported
- **Требуется ли лицензия для продакшн?** Yes, a commercial license is needed for production use
- **Какие версии .NET совместимы?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6
- **Сколько времени занимает базовый вызов OCR?** Typically under a second for a standard‑size image

## Требования

Прежде чем погрузиться в код, убедитесь, что у вас есть:

1. **Aspose.OCR for .NET Library** – Скачайте и установите её по [download link](https://releases.aspose.com/ocr/net/).  
2. **Development Environment** – Любая IDE, совместимая с .NET (Visual Studio, Rider, VS Code и т.д.).  
3. **A sample image** – Для этого руководства мы будем использовать `sample.png`, размещённый в папке по вашему выбору.

## Импорт пространств имён

First, add the required namespaces so the compiler knows where to find the OCR classes:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Как выполнить OCR изображения с помощью Aspose.OCR for .NET

Ниже представлен сквозной процесс, разбитый на четкие нумерованные шаги. Каждый шаг включает короткое объяснение и точный код, который необходимо скопировать.

### Шаг 1: Укажите каталог документов

```csharp
string dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на абсолютный или относительный путь, содержащий `sample.png`. Это указывает API, где искать изображение для обработки.

### Шаг 2: Инициализировать Aspose.OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

Создание экземпляра `AsposeOcr` предоставляет доступ ко всем методам OCR, таким как `RecognizeImage`.

### Шаг 3: Распознать изображение

```csharp
string result = api.RecognizeImage(dataDir + "sample.png");
```

Метод `RecognizeImage` читает файл изображения и возвращает извлечённый текст в виде строки. Здесь происходит основная работа — **recognize image text**.

### Шаг 4: Отобразить распознанный текст

```csharp
Console.WriteLine(result);
```

Вы можете вывести результат в консоль, записать его в файл или передать другому компоненту для дальнейшей обработки.

### Шаг 5: Завершить процесс

```csharp
Console.WriteLine("PerformOCROnImage executed successfully");
```

Простое сообщение подтверждения помогает убедиться, что вызов OCR завершился без исключений.

## Почему использовать Aspose.OCR для проектов на C#?

- **High Accuracy** – Встроенные языковые модели обеспечивают надёжные результаты даже при низком качестве сканирования.  
- **Broad Format Support** – Поддерживает PNG, JPEG, BMP, TIFF и другие форматы, упрощая **convert image to text** независимо от источника.  
- **No External Dependencies** – Чистая .NET‑библиотека; не требуется установка нативных OCR‑движков.  
- **Extensible** – Вы можете тонко настраивать параметры распознавания или интегрировать с другими продуктами Aspose для сквозных документооборотных процессов.

## Распространённые проблемы и их устранение

| Симптом | Возможная причина | Решение |
|---------|-------------------|--------|
| Empty string returned | Image path incorrect or file not found | Verify `dataDir` and filename; use `Path.Combine` for safety |
| Garbled characters | Image resolution too low or unsupported language | Use a higher‑resolution image; set language options via `api.Language = "eng"` |
| Exception `System.IO.FileNotFoundException` | Missing `sample.png` | Ensure the file exists in the specified folder |

## Часто задаваемые вопросы

**Q: Может ли Aspose.OCR обрабатывать несколько форматов изображений?**  
A: Yes, it supports a wide range of formats, so you can **extract image text** from PNG, JPEG, BMP, TIFF, and more.

**Q: Доступна ли временная лицензия для тестирования?**  
A: Absolutely. You can request a 30‑day evaluation license from the Aspose portal.

**Q: Где я могу найти полную документацию по Aspose.OCR for .NET?**  
A: The official guide is the [Aspose.OCR documentation](https://reference.aspose.com/ocr/net/).

**Q: Как я могу получить поддержку или связаться с сообществом для помощи?**  
A: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) to ask questions and share experiences.

**Q: Могу ли я попробовать Aspose.OCR for .NET бесплатно перед покупкой?**  
A: Yes, a fully functional **free trial** is available at the [free trial](https://releases.aspose.com/) page.

## Заключение

Следуя приведённым выше шагам, вы теперь знаете **how to ocr image** файлы с помощью Aspose.OCR for .NET. Независимо от того, создаёте ли вы систему управления документами, приложение для обработки чеков или любое решение, которому необходимо **convert image to text**, эта библиотека предоставляет простой и высокопроизводительный путь преобразования визуальных данных в поисковый контент.

---

**Последнее обновление:** 2025-12-17  
**Тестировано с:** Aspose.OCR for .NET 24.12 (latest at time of writing)  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}