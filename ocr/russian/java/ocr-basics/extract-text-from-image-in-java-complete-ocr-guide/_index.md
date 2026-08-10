---
category: general
date: 2026-07-21
description: Извлеките текст из изображения с помощью Java OCR. Узнайте, как преобразовать
  PNG в текст, прочитать текст из PNG, загрузить изображение для OCR и выполнить OCR
  изображения всего за несколько шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: ru
lastmod: 2026-07-21
og_description: Извлекать текст из изображения с помощью Java. Это руководство показывает,
  как преобразовать PNG в текст, читать текст из PNG, загружать изображение для OCR
  и эффективно выполнять OCR на изображении.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Извлечение текста из изображения в Java – пошаговое руководство по OCR
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Извлечение текста из изображения в Java — Полное руководство по OCR
url: /ru/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в Java – Полное руководство по OCR

Когда‑то вам нужно было **извлечь текст из изображения**, но вы не знали, какую Java‑библиотеку выбрать? Вы не одиноки. Будь то оцифровка чеков, сканирование PDF‑файлов или создание поискового архива, извлечение текста из PNG – ежедневная боль многих разработчиков.

В этом руководстве мы пошагово реализуем решение, которое позволяет **конвертировать PNG в текст**, **читать текст из PNG**, **загружать изображение для OCR** и **выполнять OCR над изображением** – всё с помощью нескольких строк чистого Java‑кода. В конце у вас будет готовая к запуску программа, которую можно добавить в любой проект.

## Что вы построите

Мы создадим небольшое консольное Java‑приложение, которое:

1. Загружает PNG‑файл с диска.  
2. Отправляет изображение в OCR‑движок (Tess4J – Java‑обёртка для Tesseract).  
3. Выводит распознанный текст в консоль.

Никаких внешних сервисов, никакой магии – только чистый Java и открытый OCR‑движок.

## Требования

- **Java 17** или новее (код компилируется и в более старых версиях, но Java 17 даёт последние возможности языка).  
- **Maven** или **Gradle** для управления зависимостями.  
- Пример PNG‑файла `sample.png`, размещённый в папке, к которой вы можете обратиться (например, `src/main/resources`).  
- Базовое знакомство с методом `main` в Java и обработкой исключений.

Если что‑то из этого вам незнакомо, не переживайте – каждый шаг содержит краткое пояснение.

## Шаг 1: Создание проекта и добавление OCR‑библиотеки

Сначала создайте новый Maven‑проект (или Gradle, если предпочитаете). Добавьте зависимость Tess4J, которая автоматически подтянет бинарники Tesseract.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Совет:** Если вы используете Gradle, эквивалентная строка выглядит так: `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Эта библиотека предоставляет класс `Tesseract`, который берёт на себя тяжёлую работу **выполнения OCR над изображением**.

## Шаг 2: Загрузка изображения для OCR

Теперь нам нужно **загрузить изображение для OCR**. Tess4J работает с `java.awt.image.BufferedImage`, поэтому прочитаем PNG через `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Метод выше чисто изолирует логику **загрузки изображения для OCR**, делая остальной код проще для тестирования. Обратите внимание на комментарий – он отражает оригинальный фрагмент, но расширен для ясности.

## Шаг 3: Выполнение OCR над изображением

Имея изображение в памяти, мы можем **выполнить OCR над изображением**. Экземпляр `Tesseract` – наш движок; мы настроим его использовать язык по умолчанию (английский), который поставляется с Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Здесь мы объединили оригинальные «Шаг 1» и «Шаг 4» в один метод, потому что объект `Tesseract` создаётся дешево, и нам хочется, чтобы код оставался компактным. Комментарий всё ещё ссылается на исходные шаги для прослеживаемости.

## Шаг 4: Собираем всё вместе – метод `main`

Наконец, объединяем всё в `main`. Здесь вы **прочитаете текст из PNG** и увидите результат в консоли.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Запустив `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (или аналогичную команду в Gradle), вы должны увидеть что‑то вроде:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Этот вывод подтверждает, что вы успешно **извлекли текст из изображения**, **конвертировали PNG в текст** и **прочитали текст из PNG** в одной аккуратной программе.

## Обработка типичных проблем

### Низкокачественные изображения

Если PNG размытый или с низким контрастом, точность OCR падает. Быстрое решение – предварительная обработка изображения:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Поддержка нескольких языков

Tess4J умеет работать со множеством языков. Достаточно скачать нужный файл `.traineddata` и указать `tesseract.setLanguage("spa")` для испанского, например.

### Большие PDF‑файлы или многостраничные изображения

Если нужно **извлечь текст из изображения** внутри PDF, сначала разбейте каждую страницу на PNG (с помощью PDFBox), а затем передайте каждый PNG в тот же OCR‑процесс.

## Полный рабочий пример (весь код в одном месте)

Ниже представлен полностью готовый к запуску Java‑класс. Скопируйте его в `src/main/java/com/example/ocrdemo/OcrDemo.java` – и всё готово.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Запуск класса выводит результат OCR, подтверждая, что вы успешно **выполнили OCR над изображением** и превратили ваш PNG в редактируемый текст.

## Итоги и дальнейшие шаги

Мы начали с **извлечения текста из изображения** с помощью лёгкой Java‑конфигурации. Теперь вы знаете, как **загружать изображение для OCR**, **выполнять OCR над изображением** и **читать текст из PNG** – базовые блоки любой цепочки оцифровки документов.

Хотите идти дальше? Попробуйте следующие идеи:

- **Пакетная обработка:** Пройдитесь по каталогу PNG‑файлов и запишите каждый результат в отдельный `.txt`.  
- **Интеграция с базой данных:** Сохраняйте извлечённые строки вместе с метаданными для поисковых архивов.  
- **Комбинация с NLP:** Передавайте вывод OCR в модель анализа тональности для быстрых инсайтов.  

Все эти расширения опираются на те же фундаментальные концепции, которые мы рассмотрели, так что вы готовы к экспериментам.

---

*Счастливого кодинга! Если возникнут проблемы


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}