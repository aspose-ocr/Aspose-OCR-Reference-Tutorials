---
category: general
date: 2026-08-18
description: Как включить GPU для OCR в Java и быстро распознавать текст на изображении,
  извлекать текст из JPG, добавлять фильтр и задавать язык с помощью Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: ru
lastmod: 2026-08-18
og_description: Как включить GPU для OCR в Java и мгновенно распознавать текст на
  изображениях, извлекать текст из JPG, добавлять фильтр и задавать язык с помощью
  Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Как включить GPU для OCR в Java – полное руководство по Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Как включить GPU для OCR в Java с использованием Aspose.OCR
url: /ru/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить GPU для OCR в Java с помощью Aspose.OCR

Если вам нужно **как включить GPU** для OCR в Java, это руководство проведёт вас через все необходимые шаги. Включение ускорения GPU позволяет **распознавать текст на изображениях** в несколько раз быстрее, что особенно важно при **извлечении текста из JPG** файлов массово. Мы также рассмотрим **как добавить фильтр**, **как задать язык** и как получить окончательный результат.

К концу этого урока у вас будет полностью готовая, исполняемая программа, которая:

* Запускает движок Aspose.OCR с поддержкой GPU.  
* Настраивает язык OCR (например, английский).  
* Применяет фильтр шумоподавления для повышения точности.  
* Загружает JPEG‑изображение, выполняет распознавание и выводит извлечённый текст.

> **Требования:** Java 17 или новее, Maven и лицензия Aspose.OCR for Java (бесплатная пробная версия подходит для оценки).

---

![Как включить GPU для OCR в Java](/images/ocr-gpu.png){alt="Как включить GPU для OCR в Java"}

## Что понадобится

| Элемент | Причина |
|------|--------|
| **Java Development Kit (JDK) 17+** | Необходим для компиляции и запуска примера. |
| **Maven** | Упрощает управление зависимостями Aspose.OCR. |
| **Aspose.OCR for Java** | Предоставляет класс `OcrEngine` и поддержку GPU. |
| **Пример JPEG‑изображения** (`sample.jpg`) | Используется для демонстрации **извлечения текста из JPG**. |
| **Аппаратное обеспечение, совместимое с GPU** (необязательно, но рекомендуется) | Позволяет получить ускорение производительности, которое мы настроим. |

---

## Шаг 1: Настройка Maven‑проекта

Создайте новый Maven‑проект (или добавьте в существующий) и включите зависимость Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Совет:** Держите номер версии актуальным; новые релизы улучшают работу с GPU и добавляют языковые пакеты.

---

## Шаг 2: Инициализация OCR‑движка и **как включить GPU**

Сердце решения — класс `OcrEngine`. Его создание простое, но вам нужно явно включить ускорение GPU:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Зачем включать GPU?**  
При вызове `setUseGpu(true)` Aspose.OCR переносит тяжёлые ядра обработки изображений на видеокарту. На современной видеокарте NVIDIA/AMD скорость распознавания может вырасти с ~200 мс за страницу до < 80 мс, что существенно сокращает общее время обработки больших пакетов.

---

## Шаг 3: **Как задать язык** и **как добавить фильтр**

### 3.1 Задать язык OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR поставляется с языковыми пакетами более чем для 100 языков. Замените `ENGLISH` на `FRENCH`, `CHINESE_SIMPLIFIED` и т.д., в зависимости от вашего исходного материала.

### 3.2 Добавить предобработку фильтром

Шум, артефакты сжатия или неравномерное освещение могут ухудшить точность. Добавление фильтра шумоподавления — типичный **как добавить фильтр** подход:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Другие полезные фильтры: `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` и `FilterType.BINARIZE`. Вы можете цепочкой добавить несколько фильтров, вызывая `addPreprocessFilter` последовательно.

---

## Шаг 4: Загрузка изображения – **извлечение текста JPG**

Теперь укажем движку JPEG‑файл, который нужно обработать:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Замените `YOUR_DIRECTORY` на реальный путь, где находится `sample.jpg`. Aspose.OCR также поддерживает PNG, BMP, TIFF и PDF; тот же вызов работает и для этих форматов.

---

## Шаг 5: Выполнение OCR и **распознавание текста на изображении**

После настройки движка вызовите процедуру распознавания:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Метод `recognize()` обрабатывает изображение на GPU (если он включён) и заполняет внутренний буфер текста. `getText()` возвращает обычный `String`, который можно записать в файл, базу данных или передать в последующие NLP‑конвейеры.

### Ожидаемый вывод

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Если на изображении несколько строк, возвращаемая строка будет содержать символы новой строки (`\n`), сохраняющие оригинальное расположение.

---

## Шаг 6: Проверка использования GPU (необязательно)

Чтобы убедиться, что GPU действительно используется, включите логирование Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

После запуска проверьте `ocr-debug.log`; вы должны увидеть записи вроде `GPU device: NVIDIA GeForce RTX 3080` и `Processing time (GPU): 78 ms`. Если в логе указано **CPU**, проверьте установку драйверов и наличие вызова `setUseGpu(true)`.

---

## Распространённые ошибки и как их избежать

| Симптом | Возможная причина | Решение |
|---------|-------------------|--------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Отсутствуют нативные GPU‑библиотеки | Установите последние драйверы GPU и убедитесь, что нативные бинарники `aspose-ocr` находятся в `java.library.path`. |
| **Плохая точность на тёмных изображениях** | Нет фильтра предобработки | Добавьте `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` или увеличьте `FilterType.CONTRAST`. |
| **`OutOfMemoryError` при больших пакетах** | Переполнение памяти GPU | Обрабатывайте изображения небольшими партиями или отключите GPU (`engine.setUseGpu(false)`) для очень больших разрешений. |
| **Неправильный язык вывода** | Указан неверный язык | Проверьте, что `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` соответствует исходному тексту. |

---

## Полный, готовый к запуску пример

Ниже представлен полностью готовый Java‑класс, который можно скопировать в `src/main/java/com/example/HelloWorldOcr.java`. Он включает все шаги, обработку ошибок и необязательное логирование.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Запуск программы**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Вы должны увидеть распознанный текст в консоли и сохранённый в `output.txt`. Файл `ocr-debug.log` подтвердит использование GPU.

---

## Заключение

В этом руководстве мы показали, **как включить GPU** для Aspose.OCR в Java, как **распознавать текст на изображении**, **извлекать текст из JPG**, **как добавить фильтр** и **как задать язык** — всё в одном самодостаточном приложении. Включив GPU, вы получаете значительный прирост скорости, а фильтры и языковые настройки обеспечивают высокую точность для разнообразных источников изображений.

**Следующие шаги**

* Поэкспериментируйте с дополнительными фильтрами, например `FilterType.BINARIZE`, для сканированных документов.  
* Переключитесь на другие языки (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`), чтобы расширить поддержку многоязычия.  
* Объедините этот OCR‑конвейер с Apache PDFBox для извлечения текста непосредственно из PDF‑страниц.  

Не стесняйтесь адаптировать код для пакетной обработки, интегрировать его в сервис Spring Boot или подключить к очереди сообщений для OCR в реальном времени. Приятного кодинга!

## Что изучать дальше?

Следующие учебные материалы охватывают смежные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}