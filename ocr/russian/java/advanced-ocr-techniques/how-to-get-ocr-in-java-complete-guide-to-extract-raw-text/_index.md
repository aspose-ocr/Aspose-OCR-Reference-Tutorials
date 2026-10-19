---
category: general
date: 2026-05-25
description: Как получить OCR в Java и извлечь необработанный текст из изображений.
  Узнайте, как отключить исправление орфографии, распознавать рукописный текст и как
  эффективно загружать изображение.
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: ru
og_description: Как получить OCR в Java и извлечь сырой текст из изображения. Это
  руководство показывает, как отключить исправление орфографии, распознавать рукописный
  текст и правильно загружать изображение.
og_title: Как получить OCR в Java — извлечение необработанного текста шаг за шагом
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: Как получить OCR в Java – Полное руководство по извлечению исходного текста
url: /ru/java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как получить OCR в Java – Полное руководство по извлечению исходного текста

Вы когда‑нибудь задавались вопросом, **как получить OCR** результаты без автоматической очистки библиотеки? Возможно, вы работаете с рукописной заметкой и вам нужны точные символы, которые увидел движок, а не «красиво отформатированная» версия. В этом руководстве мы пройдем практический пример, который показывает, как именно **получить OCR** вывод, как **извлечь исходный текст**, и почему вам может понадобиться **отключить проверку орфографии** при распознавании рукописного текста. К концу вы также узнаете, **как загрузить изображение** в движок Aspose OCR без проблем.

Мы будем использовать Aspose.OCR для Java, но концепции применимы к любому OCR SDK, который предлагает переключатель проверки орфографии. Без громкой теории — только практическое решение «копировать‑вставить», которое вы можете запустить уже сегодня.

---

## Что вы узнаете

- Как настроить Aspose.OCR в Java‑проекте  
- Точные шаги **как получить OCR** необработанный вывод  
- Почему и **как отключить проверку орфографии** для чистого текста  
- Лучший способ **как загрузить изображение** файлы для оптимального распознавания  
- Как **распознать рукописный текст** и проверить результат  

Требования минимальны: установлен Java 8+, IDE, совместимая с Maven (IntelliJ, Eclipse или VS Code), и пример изображения с рукописными символами. Если чего‑то не хватает, просто скачайте JDK с сайта Oracle и изображение со своего телефона — без проблем.

![Diagram illustrating the OCR workflow, showing how to get OCR raw text from an image](/images/ocr-workflow.png){: .center alt="как получить OCR необработанный текст"}

---

## Шаг 1: Добавьте Aspose.OCR в ваш проект

### Зависимость Maven

Если вы используете Maven, вставьте это в ваш `pom.xml`. Это загрузит последнюю библиотеку Aspose.OCR (по состоянию на май 2026).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **Совет:** Всегда проверяйте официальный репозиторий Aspose Maven на наличие более новых версий. Выпуск `23.11` добавляет лучшую поддержку курсивных скриптов, что удобно, когда вы **распознаёте рукописный текст**.

### Альтернатива Gradle

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

После того как зависимость будет разрешена, вы готовы писать код, который действительно **получает OCR** результаты.

---

## Шаг 2: Создайте экземпляр OCR Engine

Движок — сердце процесса. Его создание простое, но настоящая магия начинается, когда вы его настраиваете.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

Зачем нам нужен отдельный объект `OcrEngine`? Он хранит все параметры выполнения, включая переключатель проверки орфографии, который мы рассмотрим дальше. Изоляция движка также позволяет запускать несколько распознаваний параллельно без перекрестного загрязнения.

---

## Шаг 3: Отключите проверку орфографии (если нужен необработанный вывод)

Большинство OCR‑библиотек пытаются помочь, автоматически исправляя опечатки. Это отлично для печатного текста, но катастрофично для извлечения необработанных данных. Вот как **отключить проверку орфографии**:

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

Когда флаг установлен в `false`, движок возвращает точно то, что увидел на битмапе, сохраняя разрывы строк, пунктуацию и даже редкие случайные глифы. Это необходимо, если позже вы передаёте вывод в конвейер машинного обучения, ожидающий оригинальный шум.

---

## Шаг 4: Загрузите изображение — правильный способ

Вы можете подумать, что `engine.getImage().loadFromFile("path")` достаточно, но есть несколько нюансов:

1. **Абсолютные и относительные пути** — используйте `Paths.get(...)` для независимости от платформы.  
2. **Поддерживаемые форматы** — Aspose.OCR работает с PNG, JPEG, BMP, TIFF и GIF.  
3. **Разрешение имеет значение** — более высокое DPI дает лучшее распознавание, особенно для курсивного письма.

Вот надёжный фрагмент кода, демонстрирующий **как безопасно загрузить изображение**:

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

Если вы работаете с потоком (например, загружаете из веб‑формы), замените `loadFromFile` на `loadFromStream`. Главное: всегда проверяйте файл перед передачей его движку, потому что отсутствие файла вызывает непонятный `NullPointerException`, который трудно отладить.

---

## Шаг 5: Выполните распознавание

Теперь наступает момент истины — **как получить OCR** результаты. Метод `recognize()` запускает внутренний конвейер, применяя языковые модели, сегментацию и (если включено) проверку орфографии. Поскольку мы её отключили, вы получите неизменённые символы.

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

Объект `OcrResult` содержит не только текст; вы также можете получить оценки уверенности, ограничивающие рамки и даже вероятности для каждого символа. В этом руководстве мы сосредоточимся на простом тексте.

---

## Шаг 6: Выведите необработанный OCR результат

Наконец, выведите результат в консоль. Это самый простой способ **извлечь необработанный текст** для отладки или последующей обработки.

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### Ожидаемый вывод

Предположим, что `handwritten.png` содержит фразу *«Hello World»* написанную курсивом, вы увидите примерно следующее:

```
Raw OCR output:
H e l l o   W o r l d
```

Обратите внимание на дополнительные пробелы — они намеренные, потому что движок сохраняет точные интервалы, которые он обнаружил. Если позже понадобится убрать лишние пробелы, сделайте это на этапе пост‑обработки.

---

## Распространённые ошибки и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Пустая строка** | DPI изображения слишком низкое или изображение полностью белое. | Убедитесь, что исходное изображение имеет минимум 300 DPI; используйте `engine.getImage().setResolution(300, 300)`. |
| **Мусорные символы** | Неправильный формат файла или повреждённые байты. | Проверьте файл в просмотрщике изображений; повторно экспортируйте как PNG. |
| **Проверка орфографии всё ещё активна** | Случайно включена где‑то в коде. | Оставьте вызов `setSpellCorrectorEnabled(false)` сразу после создания движка. |
| **Рукописный текст не распознаётся** | Язык движка по умолчанию установлен на английский печатный текст. | Вызовите `engine.getEngineOptions().setLanguage(Language.English);` и при необходимости `engine.getEngineOptions().setUseDictionary(false);`. |

---

## Расширение примера: распознавание рукописного текста

Если ваш сценарий специально ориентирован на **распознавание рукописного текста**, вы можете настроить несколько параметров для повышения точности:

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

Это заставляет внутреннюю нейронную сеть отдавать предпочтение курсивным образцам над печатными глифами. На практике вы заметите значительный рост оценок уверенности для подписей, заметок или быстрых набросков.

---

## Полный рабочий пример (готовый к копированию‑вставке)

Ниже представлен полный, автономный Java‑класс, включающий все обсуждаемые шаги. Просто замените `YOUR_DIRECTORY/handwritten.png` на путь к вашему изображению и запустите его.

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

Запустите его с помощью:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

Вы должны увидеть необработанные символы, выведенные точно так, как их прочитал движок.

---

## Заключение

Мы рассмотрели, **как получить OCR** необработанные результаты в Java, продемонстрировали правильный способ **отключить проверку орфографии**, показали лучшую практику **как загрузить изображение**, и объяснили нюансы **распознавания рукописного текста**. Следуя этим шагам, вы сможете надёжно **извлекать необработанный текст**, будь то построение конвейера оцифровки документов, инструмента судебной экспертизы или простого приложения для заметок.

Далее вы можете изучить:

- **Пост‑обработка**: обрезка пробелов, нормализация Unicode или передача вывода в языковую модель.  
- **Пакетная обработка**: перебор каталога изображений и сохранение результатов в базе данных.  
- **Продвинутые опции**: настройка `EngineOptions` для поддержки нескольких языков или пользовательских словарей.

Попробуйте их, и не стесняйтесь задавать вопросы в комментариях. Приятного кодинга, и пусть ваш OCR всегда будет точным!

## Связанные руководства

- [Как выполнить OCR текста изображения с указанием языка с помощью Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Извлечение текста из изображения Java с Aspose.OCR в режиме обнаружения областей](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [распознавание текста изображения с Aspose OCR – Полное руководство по Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}