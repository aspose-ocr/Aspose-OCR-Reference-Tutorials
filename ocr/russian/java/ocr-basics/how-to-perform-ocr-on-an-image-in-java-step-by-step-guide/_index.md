---
category: general
date: 2026-11-17
description: Узнайте, как выполнять OCR на изображении в Java и извлекать текст из
  картинок с помощью простого примера кода. Включает советы по чтению изображений
  в Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: ru
lastmod: 2026-11-17
og_description: Как выполнить OCR изображения в Java и быстро извлечь текст. Следуйте
  этому руководству, чтобы читать изображение в Java и преобразовать его в текст с
  готовым к запуску примером.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Как выполнить OCR на изображении в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Как выполнить OCR на изображении в Java – пошаговое руководство
url: /ru/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на изображении в Java – пошаговое руководство

Если вам нужно **как выполнять OCR** на картинке, это руководство покажет полное, готовое к запуску решение на Java. Вы увидите, как прочитать файл изображения, настроить OCR‑движок и извлечь текст, который он распознает.

Работа со сканированными документами, чеками или скриншотами часто требует преобразования визуального содержимого в поисковый текст. Это руководство проведёт вас через каждый шаг, от загрузки изображения до вывода извлечённого текста, а также охватит типичные подводные камни, такие как неподдерживаемые форматы файлов и нулевые результаты.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* Java Development Kit (JDK) 8 или новее.
* Инструмент сборки (Maven или Gradle) для получения OCR‑библиотеки.
* Файл изображения (JPEG, PNG, BMP), который вы хотите обработать.

В коде используется **OCR‑библиотека из пакета `com.asprise.ocr`**, потому что она требует только один JAR и работает на всех основных платформах. Замените её другим провайдером (Tesseract, Google Vision и т.д.), заменив импорты и код инициализации движка.

## Шаг 1: Добавьте зависимость OCR

Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Для Gradle поместите эту строку в `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Эти строки гарантируют, что код **read image Java** сможет компилироваться и что OCR‑движок будет доступен во время выполнения.

## Шаг 2: Прочитайте изображение с помощью Java

Чтение файла изображения — первый конкретный шаг в любом рабочем процессе **extract text image**. Встроенный класс Java `ImageIO` обрабатывает большинство распространённых форматов.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Почему это важно:** `ImageIO.read` возвращает `null` для неподдерживаемых форматов или повреждённых файлов. Метод выше логирует проблему и возвращает `null`, чтобы следующий шаг мог корректно отреагировать.

## Шаг 3: Создайте и настройте OCR‑движок

OCR‑движок должен знать, какой язык распознавать. Указание языка значительно повышает точность, особенно для документов не на английском.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Почему это важно:** Запуск движка — относительно тяжёлая операция, поэтому его следует создавать один раз и переиспользовать для нескольких изображений, если приложение обрабатывает пакеты.

## Шаг 4: Выполните OCR и преобразуйте изображение в текст

Теперь, когда изображение загружено, а движок готов, можно выполнить шаг распознавания. Это ядро **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Обработка граничных случаев:** Если изображение `null`, метод возвращает пустую строку вместо выброса `NullPointerException`. Это делает окружающий код более надёжным при работе с файлами, предоставленными пользователем.

## Шаг 5: Выведите извлечённый текст

Наконец, выведите результат в консоль или передайте его в другой компонент (например, базу данных или UI‑виджет).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Когда вы запустите программу командой `java OcrDemo sample.jpg`, консоль покажет распознанные символы. Это завершает цикл **convert image to text**.

### Ожидаемый вывод

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Если изображение не содержит читаемых символов, программа выводит `(no text detected)`.

## Общие варианты и как их адаптировать

| Вариант | Что меняется | Когда использовать |
|-----------|--------------|---------------------|
| **Другой язык** | Замените `"eng"` на `"spa"` для испанского, `"fra"` для французского и т.д. | Документы, написанные не на английском |
| **Пакетная обработка** | Цикл по списку путей к файлам, переиспользуйте один экземпляр `Ocr`. | Большие наборы сканированных страниц |
| **Повышенная точность** | Используйте `Ocr.SPEED_SLOW` или включите `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` для сканов только с цифрами. | Когда качество OCR критично (например, номера счетов) |
| **Альтернатива Tesseract** | Замените импорт на `net.sourceforge.tess4j.Tesseract` и скорректируйте код инициализации. | Проекты, уже зависящие от Tesseract |

## Профессиональные советы

* **Изменяйте размер больших изображений** перед передачей их в движок; скорость OCR масштабируется с количеством пикселей.
* **Предобрабатывайте** изображение (градация в серый, повышение контраста) с помощью библиотек, таких как OpenCV, если исходник шумный.
* **Кешируйте OCR‑движок**, если вызываете его часто за короткий промежуток — запуск и остановка движка требуют ресурсов.
* **Проверяйте результат** регулярными выражениями, когда ожидаете определённый формат (например, даты, номера телефонов).

## Заключение

Теперь вы знаете **how to perform OCR** на изображении в Java, от чтения файла до вывода извлечённого текста. Руководство охватило техники **read image Java**, **extract text image**, **convert image to text** и **image to text java**, а также предоставило практические советы для реальных сценариев.  

Дальше вы можете:

* Интегрировать шаг OCR в веб‑сервис, принимающий загрузки.
* Скомбинировать вывод с поисковым индексом для полнотекстового поиска по сканированным документам.
* Исследовать продвинутые возможности OCR, такие как поддержка нескольких языков или пользовательские наборы символов.

Приятного кодинга и наслаждайтесь превращением картинок в поисковый текст!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}