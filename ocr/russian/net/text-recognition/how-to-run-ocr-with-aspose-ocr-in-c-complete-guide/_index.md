---
category: general
date: 2026-02-28
description: как запустить OCR в C# с использованием Aspose OCR — узнайте, как извлекать
  текст из изображения, конвертировать изображение в JSON или XML за несколько шагов.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: ru
og_description: как запустить OCR в C# с использованием Aspose OCR – узнайте, как
  извлекать текст из изображения и преобразовывать изображение в JSON или XML с готовым
  примером.
og_title: Как запустить OCR с Aspose OCR в C# – Полное руководство
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как запустить OCR с помощью Aspose OCR в C# – Полное руководство
url: /ru/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как запустить OCR с Aspose OCR в C# – Полное руководство

Если вы задаётесь вопросом **как запустить OCR** на изображении чека с помощью C#, вы попали по адресу. В этом руководстве мы пройдём через **extract text from image** и затем **convert image to JSON** или **convert image to XML** с Aspose OCR — всё в одной самостоятельной программе.

Представьте, что вы создаёте приложение для учёта расходов и нужно извлекать позиции из сфотографированных чеков. Вручную вводить каждую запись — это хлопотно, верно? К концу этого руководства у вас будет переиспользуемый фрагмент кода, который читает любое изображение, возвращает структурированный текст и предоставляет представления в JSON и XML, готовые к дальнейшей обработке.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или новее (код также работает на .NET Framework 4.8)
- Visual Studio 2022 (или любой другой предпочитаемый редактор)
- Активный пакет **Aspose.OCR** NuGet (`Install-Package Aspose.OCR`)
- Пример изображения (например, `receipt.png`) в папке, к которой вы можете обратиться

Дополнительная настройка не требуется; библиотека поставляется со всеми необходимыми OCR‑моделями.

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *Alt text: Receipt image for OCR processing – how to run OCR*

## Пошаговая реализация

Ниже мы разбиваем решение на логические части. Каждый шаг объясняет **почему** мы делаем то или иное, а не только **что** делает код.

### 1️⃣ Initialize the OCR Engine – the foundation of **how to run OCR**

Класс `OcrEngine` является точкой входа. Его создание загружает внутренние языковые модели и подготавливает движок к распознаванию.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Pro tip:** Re‑using the same `OcrEngine` across multiple images reduces memory churn and speeds up batch processing.

### 2️⃣ Load the Image – the core of **extract text from image**

Aspose OCR работает со своим обёрткой `Image`. Использование конструкции `using` гарантирует своевременное освобождение файлового дескриптора.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Если изображение в другом формате (BMP, TIFF, PDF), тот же метод `Load` справится с ним — дополнительное преобразование не требуется.

### 3️⃣ Run OCR Recognition – the heart of **how to run OCR**

Вызов `Recognize` выполняет основную работу: анализ макета, сегментацию символов и классификацию с учётом языка.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Возвращаемый `OcrResult` содержит необработанный текст, оценки уверенности и детальное дерево макета, которое можно сериализовать.

### 4️⃣ Convert Image to JSON – the straightforward way to **convert image to json**

JSON идеально подходит для веб‑API или NoSQL‑хранилищ. Метод `ToJson` выдаёт красиво отформатированную строку, что упрощает отладку.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Типичный вывод JSON выглядит так (усечён для краткости):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Теперь вы можете напрямую передать этот JSON в REST‑конечную точку или сохранить в Azure Cosmos DB.

### 5️⃣ Convert Image to XML – when **convert image to xml** is required

Некоторые устаревшие системы всё ещё используют XML. Aspose предоставляет `ToXml` для чистого, совместимого со схемой представления.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Пример фрагмента XML:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Оба формата сохраняют одну и ту же иерархическую структуру, так что выбирайте тот, который лучше вписывается в ваш конвейер.

## Распространённые подводные камни и надёжное извлечение текста

Даже при использовании надёжной библиотеки реальные изображения могут подкидывать сюрпризы. Ниже три типичных проблемы и способы их решения.

### 📏 Low‑Resolution Images

**Почему это важно:** Маленькие шрифты сливаются, снижается уровень уверенности.  
**Решение:** Предобработайте изображение — увеличьте масштаб с помощью `Image.Resize` или примените фильтр резкости перед вызовом `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Poor Contrast

**Почему это важно:** Светлый текст на тёмном фоне сбивает алгоритм сегментации.  
**Решение:** Инвертируйте цвета или отрегулируйте яркость/контраст через `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Multi‑Language Documents

**Почему это важно:** Модель по умолчанию обучена только английскому; смешанные языки приводят к искажённому выводу.  
**Решение:** Установите `ocrEngine.Language = OcrLanguage.Multilingual;` перед распознаванием.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Устранение этих граничных случаев делает **how to extract text** из любого изображения надёжной процедурой, а не азартной игрой.

## Полный рабочий пример (готовый к копированию)

Ниже представлена полная программа, готовая к компиляции и запуску. Просто замените `YOUR_DIRECTORY` на путь к вашему изображению и нажмите F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Ожидаемый вывод в консоли** (отформатирован для читаемости) показывает структуры JSON и XML с извлечённым текстом и координатами ограничивающих рамок.

## Итоги – Что мы рассмотрели

- **how to run OCR** с Aspose OCR в C#
- Пошаговый процесс **extract text from image**
- Два варианта сериализации: **convert image to json** и **convert image to xml**
- Советы по работе с низким разрешением, плохим контрастом и многоязычными сценариями
- Полный, готовый к копированию код, который можно вставить в любой .NET‑проект

## Что дальше?

Теперь, когда вы умеете **how to extract text** и получать структурированные данные, рассмотрите следующие идеи:

- Передавать JSON в Azure Function, сохраняющую чеки в Cosmos DB.
- Использовать XML‑вывод для заполнения существующей SOAP‑базированной бухгалтерской системы.
- Комбинировать Aspose OCR с моделью машинного обучения для автоматической классификации типов расходов.

Экспериментируйте — заменяйте `receipt.png` на счета, визитные карточки или рукописные заметки. Та же схема работает для

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}