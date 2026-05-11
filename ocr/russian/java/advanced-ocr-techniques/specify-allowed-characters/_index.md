---
date: 2026-02-20
description: Узнайте, как извлекать текст из изображений с помощью Aspose.OCR для
  Java, задавать разрешённые символы и применять временную лицензию — полный учебник
  по Aspose OCR Java.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Извлечение текста из изображений с помощью Aspose.OCR – разрешённые символы
url: /ru/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображений с помощью Aspose.OCR – Разрешённые символы

## Введение

Извлечение текста из изображений — распространённая задача в современных приложениях: будь то обработка счетов, сканирование чеков или оцифровка печатных документов. В этом руководстве мы пройдем полный **aspose ocr java tutorial**, который покажет, как **extract text from images** с помощью Aspose.OCR для Java, задать разрешённые символы и применить временную лицензию при тестировании библиотеки.

## Быстрые ответы
- **What does Aspose.OCR do?** Он извлекает текст из изображений с высокой точностью и поддерживает пользовательские наборы символов.  
- **Do I need a license?** Для использования в продакшене требуется временная или постоянная лицензия.  
- **Which JDK version is supported?** Последние версии JDK полностью совместимы.  
- **Can I limit recognized characters?** Да — используйте API `setAllowedCharacters` для ограничения вывода.  
- **How long does the setup take?** Около 10‑15 минут для базовой реализации.

## Что такое “извлечение текста из изображений”?
Извлечение текста из изображений — это процесс преобразования визуального текста (например, печатного или рукописного) в машинно‑читаемые строки. Это позволяет выполнять дальнейшие задачи, такие как поиск, индексация или анализ данных.

## Почему использовать Aspose.OCR для Java?
- **High accuracy** across multiple languages and fonts. → Высокая точность распознавания на множестве языков и шрифтов.  
- **Simple API** that integrates with any Java project. → Простой API, который интегрируется в любой Java‑проект.  
- **Customizable** character sets, language packs, and image preprocessing. → Настраиваемые наборы символов, языковые пакеты и предобработка изображений.  
- **No external dependencies**—the library is self‑contained. → Нет внешних зависимостей — библиотека автономна.

## Предварительные требования

Before you start, make sure you have the following:

### Java Development Kit (JDK)

Ensure you have the latest Java Development Kit installed on your system. You can download it from [here](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Download and install the Aspose.OCR for Java library from the [download link](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

To access the full potential of Aspose.OCR, acquire a valid license. You can obtain one from [here](https://purchase.aspose.com/buy) or explore a [temporary license](https://purchase.aspose.com/temporary-license/) for a trial period.

## Как применить временную лицензию

When you’re evaluating the product, a temporary license removes the evaluation watermark and unlocks full functionality for a limited period. Create the license string in the Aspose portal, then pass it to the `AsposeOCR` constructor as shown in the code example below. For production deployments, replace the temporary key with your permanent license.

## Советы по предобработке изображений для OCR

Good image quality dramatically improves recognition results. Before calling the OCR engine, consider:

- Converting the image to grayscale. → Преобразование изображения в градации серого.  
- Increasing contrast to make characters stand out. → Повышение контрастности для лучшего выделения символов.  
- Removing background noise with a binarization filter. → Удаление фонового шума с помощью бинаризационного фильтра.  
- Resizing low‑resolution images to at least 300 dpi. → Масштабирование изображений низкого разрешения до минимум 300 dpi.

These steps are part of **ocr image preprocessing** and can be performed with any standard Java imaging library before invoking Aspose.OCR.

## Импорт пакетов

Once the prerequisites are ready, import the necessary packages into your Java project:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Пошаговое руководство

### Шаг 1: Установите каталог документов

Define a folder where you’ll store the OCR‑processed results. This path is used later to locate the image file.

```java
String dataDir = "Your Document Directory";
```

### Шаг 2: Укажите путь к изображению

Point the API to the image you want to analyze.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Шаг 3: Создайте экземпляр Aspose.OCR

Instantiate the OCR engine with your license key. The key can be a temporary or permanent license string.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Шаг 4: Выполните распознавание OCR

Call the `RecognizeLine` method to extract a line of text from the image. The result is a plain string that you can further process or store.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** If you need to restrict the output to a specific set of characters (e.g., digits only), use the `setAllowedCharacters` method on the `AsposeOCR` instance before calling `RecognizeLine`. This ensures the engine ignores any characters outside the defined set.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|---------|
| **No output or empty string** | Incorrect image path or unsupported image format | Verify `imagePath` and use a supported format (JPEG, PNG, BMP) |
| **Recognition errors** | Low‑resolution image or noisy background | Pre‑process the image (increase contrast, binarize) before OCR |
| **License not applied** | Missing or invalid license key | Ensure the license string is correct and placed in `AsposeOCR` constructor |

## Часто задаваемые вопросы

**Q: How can I obtain a temporary license for Aspose.OCR?**  
A: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/) to request a trial license.

**Q: Where can I find support for Aspose.OCR?**  
A: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) for help and discussions.

**Q: Can I specify allowed characters in Aspose.OCR?**  
A: Yes, you can customize the character set using the `setAllowedCharacters` API. Refer to the official documentation for details.

**Q: Is Aspose.OCR compatible with the latest JDK versions?**  
A: Absolutely—Aspose.OCR is regularly updated to stay compatible with the newest Java releases.

**Q: Are there additional OCR features beyond line recognition?**  
A: Yes, the library supports block, paragraph, and full‑page recognition, as well as language packs and image preprocessing options.

## Заключение

By following this **aspose ocr java tutorial**, you now have a working solution to **extract text from images** and control which characters are recognized. Explore the full [documentation](https://reference.aspose.com/ocr/java/) to discover advanced features such as multi‑language support, custom preprocessing, and batch processing.

---

**Последнее обновление:** 2026-02-20  
**Тестировано с:** Aspose.OCR for Java 24.11  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}