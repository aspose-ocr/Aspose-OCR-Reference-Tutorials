---
category: general
date: 2026-06-16
description: Узнайте, как выполнять OCR изображений в Java. В этом руководстве рассматриваются
  распознавание текста из PNG, извлечение текста из изображения, преобразование изображения
  в текст и загрузка изображения для OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: ru
og_description: Выполните OCR изображения с помощью Java. Это руководство показывает,
  как распознавать текст из PNG, извлекать текст из изображения и преобразовывать
  изображение в текст с готовым к запуску примером.
og_title: Выполнение OCR изображения в Java – Полный учебный курс по программированию
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Выполнить OCR изображения в Java – Полное пошаговое руководство
url: /ru/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении в Java – Полное пошаговое руководство

Когда‑то вам нужно **perform OCR on image** файлов, но вы не знали, какую Java‑библиотеку выбрать? Вы не одиноки. Будь то сканер чеков, архиватор документов или просто любопытство по поводу превращения картинок в поисковый текст — умение **perform OCR on image** с помощью Java будет полезным.

В этом руководстве мы пройдем всё, что нужно для **perform OCR on image** файлов: загрузка изображения, настройка движка, распознавание текста и вывод результата. К концу вы сможете **recognize text from PNG** файлов, **extract text from image** источников и **convert image to text** всего несколькими строками кода.

## Prerequisites

- Java 17 или новее (код компилируется любой современной JDK)
- Maven установлен (или ваш любимый инструмент сборки)
- Базовое знакомство с синтаксисом Java
- PNG‑файл для теста (назовём его `hello.png`)

> **Pro tip:** Если PNG‑файла нет, сделайте скриншот любого текста и сохраните его как `hello.png` в папке `resources`.

## Что мы построим

Небольшое консольное приложение `OcrDemo`, которое:

1. **Loads image for OCR** – читает PNG с диска.
2. **Performs OCR on image** – использует движок Tesseract через Tess4J.
3. **Extracts text from image** – возвращает `String` с распознанным содержимым.
4. Выводит результат в консоль.

Поехали.

## Шаг 1: Создание проекта и добавление Tess4J

Сначала создайте новый Maven‑проект (или Gradle, если предпочитаете). Добавьте зависимость Tess4J, которая оборачивает популярный OCR‑движок Tesseract.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Почему Tess4J?** Он активно поддерживается, кросс‑платформенный и предоставляет чистый Java‑API для задач **perform OCR on image**.

## Шаг 2: Подготовка логики загрузки изображения

Теперь напишем вспомогательный метод, который **load image for OCR**. Метод использует `ImageIO` из Java для чтения PNG в `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Обратите внимание, что название метода явно отражает намерение **load image for OCR**, делая код самодокументирующимся.

## Шаг 3: Настройка OCR‑движка для **Perform OCR on Image**

Имея изображение, создаём экземпляр `Tesseract`, включаем автоматическое определение языка и вызываем `doOCR`. Это ядро того, как мы **perform OCR on image** данные.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Зачем включать автоопределение?** Это позволяет движку выбрать лучшую языковую модель для изображения, что особенно полезно, когда вы **convert image to text** из источников, содержащих английский и другие скрипты.

## Шаг 4: Собираем всё вместе – главное приложение

Вот точка входа, которая **recognize text from PNG**, **extract text from image** и выводит результат. Полный, готовый к запуску пример.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Ожидаемый вывод

Если `hello.png` содержит фразу «Hello, OCR world!», консоль покажет примерно следующее:

```
=== Recognized Text ===
Hello, OCR world!
```

Точный вывод может немного отличаться в зависимости от качества изображения, но вы должны увидеть текст, помещённый в PNG.

## Шаг 5: Обработка распространённых краевых случаев

### 5.1 Работа с изображениями низкого разрешения

Если исходный PNG размытый, точность OCR падает. Быстрое решение — увеличить изображение перед передачей его в движок:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Вызовите `upscale(image, 2)` перед `engine.recognize(image)`, чтобы улучшить результаты.

### 5.2 Многоязычные документы

Если ожидаются французский или немецкий тексты, просто добавьте коды языков в `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Движок затем попытается **extract text from image**, используя комбинированные языковые модели.

### 5.3 Пропуск пустых страниц

Иногда отсканированная PDF‑страница сохраняется как пустой PNG. Обнаружение пустого изображения экономит время обработки:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Шаг 6: Сборка и запуск приложения

1. **Скомпилировать:** `mvn clean compile`
2. **Запустить:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Убедитесь, что папка `tessdata` (с языковыми файлами) находится рядом с скомпилированным JAR‑файлом или укажите её абсолютный путь в `OcrEngine`.

## Заключение

Теперь у вас есть надёжный, готовый к продакшну шаблон для **perform OCR on image** файлов с помощью Java. От **loading image for OCR** до **recognize text from PNG** мы рассмотрели, как **extract text from image**, **convert image to text**, а также как справляться с низким разрешением и многоязычным контентом.

Дальше вы можете изучить:

- **Batch processing** – перебор каталога PNG и запись каждого результата в файл `.txt`.
- **PDF generation** – встраивание извлечённого текста обратно в поисковые PDF‑файлы.
- **Cloud OCR services** – сравнение локальной производительности Tesseract с API вроде Google Vision или Azure Cognitive Services.

Экспериментируйте, настраивайте параметры и делитесь результатами. Приятного кодинга, и пусть ваши изображения всегда превращаются в чистый, поисковый текст! 

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}