---
category: general
date: 2026-05-25
description: Извлечение текста из изображения в Java с использованием OCR. Узнайте,
  как загрузить изображение для OCR, распознать текст на фотографии и получить текст
  из OCR с простым примером кода.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: ru
og_description: Извлеките текст из изображения в Java с пошаговым руководством. Научитесь
  загружать изображение для OCR, распознавать текст на фото и эффективно получать
  текст из OCR.
og_title: Извлечение текста из изображения в Java – Получить текст с помощью OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Извлечение текста из изображения в Java – Получение текста с помощью OCR
url: /ru/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в Java – Получить текст с помощью OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не знали, какую Java‑библиотеку выбрать? Вы не одиноки. Будь то оцифровка чеков, извлечение серийных номеров с фотографий продуктов или просто эксперимент с интересным побочным проектом, преобразование картинки в редактируемый текст — распространённая задача.

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет, как **загрузить изображение для OCR**, настроить движок и, наконец, **распознать текст с фотографии**, чтобы вы могли **получить текст из OCR** всего в несколько строк кода. Никаких расплывчатых ссылок — всё, что нужно, прямо здесь.

## Что вы узнаете

* Как настроить лёгкий OCR‑движок в Java.  
* Точные шаги для **загрузки изображения для OCR** и работы с различными путями к файлам.  
* Почему настройка языка важна, когда вы хотите **извлечь текст из изображения**, которое не на английском.  
* Как безопасно вывести результат и что делать, когда движок ничего не возвращает.  
* Несколько профессиональных советов, чтобы избежать самых распространённых ошибок.

К концу этого руководства у вас будет автономная программа, которая читает JPEG (или PNG) с украинскими символами и выводит распознанную строку в консоль. Не стесняйтесь менять язык или изображение — всё модульно.

---

![Диаграмма, показывающая процесс извлечения текста из изображения с использованием Java OCR движка](/images/extract-text-from-image-java.png)

*Alt text: Диаграмма процесса извлечения текста из изображения в Java.*

## Предварительные требования

* **Java Development Kit (JDK) 11+** – код использует современную модульную систему, но более старые версии работают с небольшими правками.  
* **Maven или Gradle** – для загрузки OCR‑библиотеки (мы будем использовать **Asprise OCR** как лёгкую, бесплатную для разработки опцию).  
* Пример файла изображения (например, `ukrainian_sign.jpg`), размещённый там, где программа сможет его прочитать.  
* Базовое знакомство с методом `main` в Java и обработкой исключений.

Если всё это у вас есть, можно начинать. В противном случае скачайте JDK с Oracle или AdoptOpenJDK и настройте простой Maven‑проект — ничего сложного.

---

## Шаг 1: Добавьте зависимость OCR

Сначала укажите вашему инструменту сборки загрузить OCR‑движок. Для Maven поместите следующее в `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Если вы предпочитаете Gradle, эквивалент выглядит так:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Эти координаты подтягивают компактный JAR, включающий `OcrEngine`, `OcrLanguage` и вспомогательные классы, которые мы будем использовать. Для базовых латинских и кириллических скриптов дополнительные нативные бинарники не требуются.

---

## Шаг 2: Создайте Java‑класс для **извлечения текста из изображения**

Теперь напишем саму программу. Сохраните следующее как `ExtractTextDemo.java` в `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Почему такая структура работает

* **Отдельные пронумерованные блоки** упрощают восприятие, особенно когда вы ищете, где **загружать изображение для OCR** или **распознавать текст с фотографии**.  
* `try/catch` вокруг загрузки изображения и распознавания гарантирует «мягкую» ошибку — полезно, если путь к файлу неверен или OCR‑движок не может найти языковые данные.  
* Установка языка на раннем этапе (шаг 2) значительно повышает точность для неанглийских скриптов. Если позже понадобится **java image to text** для других языков, просто замените `OcrLanguage.UKRAINIAN` на `OcrLanguage.ENGLISH`, `FRENCH` и т.д.

---

## Шаг 3: Сборка и запуск программы

Из корня проекта выполните:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Или, если вы используете Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Предположим, `ukrainian_sign.jpg` содержит текст *«Ласкаво просимо»* (украинское «Welcome»), вы должны увидеть что‑то вроде:

```
=== OCR Result ===
Ласкаво просимо
```

Этот вывод подтверждает, что вы успешно **извлекли текст из изображения** и **получили текст из OCR** за один запуск.

---

## Шаг 4: Настройте процесс – от **Java Image to Text** в реальных проектах

Хотя демонстрация минимальна, в реальных приложениях часто требуется чуть больше:

| Сценарий | Что изменить | Причина |
|----------|----------------|--------|
| **Пакетная обработка** | Пройтись в цикле по `List<Path>` и сохранить каждый результат в базе данных. | Сокращает ручную работу, когда у вас сотни фотографий. |
| **Разные форматы изображений** | Использовать `ImageIO.read(new File(path))` для предварительной обработки, затем передать `BufferedImage` в `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Поддерживает PNG, BMP и даже PDF после конвертации. |
| **Тонкая настройка производительности** | Вызвать `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`, если вас устраивает немного ниже точность. | Ускоряет распознавание на слабом оборудовании. |
| **Пост‑обработка** | Обрезать пробелы, заменить типичные ошибки OCR (`0` → `O`, `1` → `I`). | Улучшает качество данных для дальнейшей обработки. |

Эти варианты сохраняют основную идею — **распознавать текст с фотографии** — и дают гибкость для производственных нагрузок.

---

## Распространённые ошибки и профессиональные советы

1. **Неправильная настройка языка** – если пропустить шаг 2, движок по умолчанию использует английский, превращая кириллические символы в бессмыслицу. Всегда проверяйте код языка.  
2. **Качество изображения имеет значение** – низкое разрешение или размытые фото снижают точность. При необходимости предварительно улучшайте контраст или бинаризуйте изображение.  
3. **Особенности путей к файлам** – в Windows обратные слеши нужно экранировать (`C:\\images\\file.jpg`). Использование `Path.of(...)` из `java.nio.file` избавляет от этой проблемы.  
4. **Утечки памяти** – `OcrEngine` держит нативные ресурсы. Вызывайте `ocrEngine.dispose()` после завершения работы, особенно в длительно работающих сервисах.  
5. **Потокобезопасность** – движок не является потокобезопасным «из коробки». Создавайте отдельный экземпляр на каждый поток или синхронизируйте доступ.

---

## Полный рабочий пример (все в одном файле)

Ниже один файл, который можно скопировать в любую IDE. Он включает вызов `dispose()` и небольшую вспомогательную функцию, чтобы код выглядел чище.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Запуск этой программы даст тот же вывод в консоль, что и ранее. Не стесняйтесь заменить `OcrLanguage.UKRAINIAN` на `OcrLanguage.ENGLISH` или любой другой поддерживаемый язык, чтобы увидеть, как движок адаптируется.

---

## Заключение

Мы прошли всё, что нужно для **извлечения текста из изображения** с помощью Java: от добавления OCR‑зависимости до **загрузки изображения для OCR**,


## Связанные руководства

- [распознавание текста на изображении с Aspose OCR – Полный Java OCR учебник](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Как выполнять OCR текста изображения с указанием языка с помощью Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Конвертировать изображение в текст в Java с использованием Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}