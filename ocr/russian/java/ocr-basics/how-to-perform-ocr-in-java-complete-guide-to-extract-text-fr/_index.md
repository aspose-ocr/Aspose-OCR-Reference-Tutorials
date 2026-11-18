---
category: general
date: 2026-06-06
description: как выполнить OCR в Java — быстро извлечь текст из изображения, преобразовать
  изображение в текст и прочитать текст из JPG с помощью простого примера кода.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: ru
og_description: как выполнить OCR в Java — узнайте, как извлекать текст из изображения,
  преобразовывать изображение в текст и читать текст из jpg с готовым примером.
og_title: Как выполнить OCR в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Как выполнить OCR в Java – Полное руководство по извлечению текста из изображений
url: /ru/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в Java – Полное руководство по извлечению текста из изображений

Вы когда‑нибудь задумывались **how to perform OCR** на фотографии, сделанной на вашем телефоне? Вы не одиноки. Независимо от того, создаёте ли вы приложение для сканирования чеков или просто нужно вытянуть текст из отсканированного PDF, **how to perform OCR** в Java — навык, который быстро окупается. В этом руководстве мы пройдём практический пример, который **extracts text from image** файлы, **converts image to text**, и даже покажет, как **read text from jpg** всего несколькими строками кода.

> *Pro tip:* Тот же подход работает для PNG, BMP или любого формата, поддерживаемого OCR‑движком — просто замените имя файла.

## Как выполнять OCR в Java – Обзор

Оптическое распознавание символов (Optical Character Recognition, OCR) — это технология, превращающая изображения букв в реальный, индексируемый текст. В экосистеме Java существует несколько библиотек — Tesseract, Asprise и коммерческие SDK — все они предоставляют похожий рабочий процесс: загрузить изображение, указать движку ожидаемый язык, запустить распознавание и получить результат. Ниже мы используем обобщённый класс `OcrEngine`, чтобы пример был понятным, но вы можете заменить его любой конкретной реализацией, следующей той же схеме.

### Что вы узнаете

- Установить OCR‑библиотеку (да, **ocr in java** проще, чем кажется).
- Создать и настроить экземпляр OCR‑движка.
- Загрузить JPG (или любое изображение) и задать язык.
- Обработать изображение и **extract text from image** файлы.
- Вывести распознанную строку в консоль.

К концу у вас будет автономная Java‑программа, которую можно добавить в любой проект и сразу запустить.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Шаг 1 – Установить и импортировать OCR‑библиотеку (ocr in java)

Прежде чем написать хоть одну строку Java, вам нужна библиотека, которая действительно выполняет тяжёлую работу. Если вы используете Maven, добавьте зависимость, как показано ниже (замените `com.example.ocr` на реальный group ID выбранного SDK):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Если вы предпочитаете Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Once the JAR is on your classpath, import the classes you’ll need:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Why this matters:** Importing the right classes prevents “cannot find symbol” errors and makes your IDE happy—nothing more frustrating than a missing import when you’re trying to **convert image to text**.

## Шаг 2 – Создать экземпляр OCR‑движка (how to perform OCR)

Now that the library is ready, spin up the engine. Think of the engine as the brain that will look at the pixels and guess the letters.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Создание движка обычно дешево; большинство SDK выделяют внутренние буферы лениво, поэтому вы можете безопасно переиспользовать один и тот же экземпляр для множества изображений, если обрабатываете пакет.

## Шаг 3 – Загрузить изображение и задать язык (extract text from image)

The next step is to give the engine something to read. Here we load a JPEG from disk and tell the OCR engine that the text is in Mongolian (ISO 639‑2 code “mon”). You can change the path or language code to match your use‑case.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Side note:** If you don’t set a language, the engine defaults to English, which can drastically lower accuracy when the text is actually Cyrillic or another script. Always specify the correct language when you can.

## Шаг 4 – Обработать изображение и получить результат (convert image to text)

With the image and language in place, ask the engine to do its magic. The `process()` call runs the OCR algorithm and returns an `OcrResult` object containing the recognized string and confidence scores.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

За кулисами движок может выполнять предобработку — выравнивание, бинаризацию, подавление шума — так что вам не придётся писать эти шаги вручную. Поэтому большинство современных OCR‑библиотек — удовольствие использовать для задач **convert image to text**.

## Шаг 5 – Вывести извлечённый текст (read text from jpg)

Finally, pull the plain‑text out of the result and do something useful with it. For this demo we simply print it to the console, but you could write it to a file, feed it into a search index, or pass it to another service.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Эта строка сама по себе доказывает, что вы успешно **read text from jpg** (или любой поддерживаемый формат). Если вывод выглядит искажённым, дважды проверьте код языка и качество изображения.

## Полный рабочий пример (Все шаги вместе)

Below is a complete, ready‑to‑run Java class that ties every piece together. Copy it into a file named `OcrDemo.java`, adjust the image path and language, then run `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Ожидаемый вывод

If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console will show:

```
=== Recognized Text ===
Сайн байна уу?
```

Если изображение размыто или код языка неверен, вы увидите искажённые символы или пустую строку — распространённые подводные камни, которые мы обсудим дальше.

## Распространённые подводные камни и как их исправить

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| Искажённые кириллические символы | Неправильный код языка (по умолчанию английский) | Set `ocrEngine.getSettings().setLanguage("mon")` or the appropriate code. |
| Нет вывода | Неправильный путь к изображению или файл недоступен | Verify the path, ensure the file exists, and that the process has read permissions. |
| Низкая точность (<70 %) | Изображение с низким контрастом или повернуто | Pre‑process the image: increase contrast, deskew, or convert to grayscale before feeding it to the engine. |
| `OutOfMemoryError` при работе с большими PDF | Загрузка большого количества страниц высокого разрешения одновременно | Process pages one at a time, or downscale images before OCR. |

### Совет: пакетная обработка

If you need to **extract text from image** files in bulk, wrap the core logic in a loop:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Этот фрагмент демонстрирует, насколько легко масштабировать от одного JPG до целой папки сканов.

## Дальше – Что изучать дальше?

- **Language Packs:** Большинство OCR SDK позволяют загружать дополнительные файлы языковых данных. Добавление нового пакета позволяет вам **convert image to text** для языков, помимо английского и монгольского.
- **PDF OCR:** Скомбинируйте этот код с Apache PDFBox для

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображений – основы OCR с Aspose.OCR для Java](/ocr/english/java/ocr-basics/)
- [Преобразование изображения в текст в Java с использованием Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Как распознавать текст на изображении с указанием языка с помощью Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}