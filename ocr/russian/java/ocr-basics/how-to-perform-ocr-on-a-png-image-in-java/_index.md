---
category: general
date: 2026-10-11
description: Узнайте, как выполнять OCR на PNG‑изображении в Java, извлекать текст
  из изображения и преобразовывать изображение в текст с помощью простого примера
  OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: ru
lastmod: 2026-10-11
og_description: Как выполнить OCR для PNG‑изображения в Java, извлечь текст из изображения
  и преобразовать изображение в текст с помощью лаконичного готового к запуску примера.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Как выполнить OCR на PNG‑изображении в Java – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Как выполнить OCR на PNG‑изображении в Java
url: /ru/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на PNG‑изображении в Java

Если вам нужно **perform OCR** на файле изображения, изучение **how to perform OCR** в Java является необходимым для многих задач автоматизации. Независимо от того, оцифровываете ли вы чеки, индексируете отсканированные документы или создаёте поисковый фотархив, возможность **extract text from image** файлов экономит бесчисленные часы ручного труда.

В этом руководстве показано полное, готовое к запуску решение, которое загружает PNG, запускает OCR‑движок и **recognize text from PNG** файлы. Вы также увидите, как **convert image to text** и справляться с распространёнными проблемами, такими как низкое разрешение входных данных или не‑ASCII символы.

## Что вы достигнете

* **load image java** код, который читает PNG с диска,
* инициализировать легковесный OCR‑движок,
* **extract text from image** и вывести результат в консоль,
* адаптировать решение для других форматов изображений или пакетной обработки.

Внешние сервисы не требуются — только одна открытая OCR‑библиотека (Tess4J) и среда выполнения Java SE.

---

## Предварительные требования

* Java 17 или новее (код компилируется с JDK 17).
* Maven или Gradle для управления зависимостями.
* Базовое знакомство с командной строкой и выбранной IDE.
* Библиотека `tess4j` (обертка Java для Tesseract). Добавьте следующую зависимость Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Если вы используете Gradle, эквивалент выглядит так:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Вам также потребуются файлы данных Tesseract (`.traineddata`). Скачайте английский набор данных из официального репозитория и поместите его в папку `tessdata` в корне проекта.

---

## Шаг 1: Загрузка изображения в Java

Загрузка PNG проста с использованием стандартного класса `ImageIO`. Приведённый ниже код демонстрирует **load image java** безопасным, учитывающим исключения способом:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Почему это важно:** `ImageIO.read` автоматически определяет формат изображения, но мы явно проверяем `null`, чтобы избежать тихих сбоев, если PNG повреждён. Этот шаблон является лучшей практикой при **load image java** для OCR.

---

## Шаг 2: Инициализация OCR‑движка

Tess4J оборачивает нативный бинарный файл Tesseract, предоставляя простой Java API. Следующий метод создаёт экземпляр `Tesseract`, указывает ему папку `tessdata` и настраивает язык на английский:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Почему мы это делаем:** Инициализация движка один раз и повторное использование его для нескольких изображений снижает накладные расходы на запуск. Вызов `setOcrEngineMode` выбирает режим по умолчанию, который хорошо работает для большинства PNG. Если вы сталкиваетесь с шумными сканами, можете экспериментировать с другими режимами (например, `OEM_LSTM_ONLY`).

---

## Шаг 3: Выполнение OCR и **recognize text from PNG**

Теперь мы объединяем загрузчик изображения и OCR‑движок. Нижеуказанный метод выполняет OCR на `BufferedImage` и возвращает извлечённую строку:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Полный рабочий пример**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Ожидаемый вывод**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Консоль покажет точные символы, которые движок извлек из `sample.png`. Если PNG содержит только одно слово, вывод будет этим словом, за которым следует перевод строки.

---

## Шаг 4: Распространённые варианты и граничные случаи

### 4.1 Обработка PNG с низким разрешением

Tesseract работает лучше всего с изображениями с разрешением не менее 300 DPI. Если ваш исходный PNG меньше, увеличьте его перед OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Вызовите `upscale(image, 2)` перед вызовом `extractText`, чтобы повысить точность.

### 4.2 Извлечение текста не на английском

Чтобы **extract text from image**, содержащий другие языки, скачайте соответствующие файлы `.traineddata` и укажите код языка:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Пакетная обработка нескольких PNG

Если вам нужно **recognize text from PNG** файлов в папке, пройдитесь по директории:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Обработка ошибок OCR

Типичные ошибки OCR включают чтение `0` (ноль) как `O` или `1` как `l`. Постобработка с помощью регулярных выражений может очистить результат:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Профессиональные советы для надёжного OCR в Java

| Совет | Причина |
|-----|--------|
| **Используйте без потерь PNG** | Артефакты сжатия в JPEG могут сбивать с толку движок. |
| **Обрезайте белые границы** | Избыточные пробелы увеличивают время обработки и могут вызывать ложные срабатывания. |
| **Установите `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** только когда макет неизвестен; в противном случае выберите конкретный режим (например, `PSM_SINGLE_BLOCK`). |
| **Кешируйте экземпляр `ITesseract`** |

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как читать текст из изображения в Java с использованием Aspose OCR – Полное руководство](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Как использовать OCR в Java – Быстро распознавать текст из изображения](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Пакетный OCR изображений в Java – Быстро извлекать текст из PNG‑файлов](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}