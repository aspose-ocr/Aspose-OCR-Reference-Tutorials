---
category: general
date: 2026-05-31
description: Быстро распознавайте текст на изображениях с помощью Aspose OCR Java.
  Узнайте, как извлекать текст из файлов PNG и задавать язык OCR для оптимальных результатов.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: ru
og_description: распознавайте текст с изображений эффективно с помощью Aspose OCR
  Java. Этот учебник показывает, как извлекать текст из PNG‑файлов и задавать язык
  OCR для пакетной обработки.
og_title: распознавание текста с изображений – Aspose OCR Java Parallel Batch
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Распознавание текста на изображениях с помощью Aspose OCR – Руководство по
  параллельной пакетной обработке в Java
url: /ru/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображений – Aspose OCR Java Parallel Batch Tutorial

Когда‑нибудь задумывались, как **распознавать текст с изображений** так, чтобы UI не «зависал»? Возможно, у вас есть папка, полная сканов, скриншотов или даже смесь PNG и JPEG файлов, и вам нужен текст как можно быстрее. Хорошая новость: с Aspose OCR для Java вы можете запустить многопоточный пакет, который **извлекает текст из png** (и других форматов), пока вы наслаждаетесь чашкой кофе.

В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий, как **установить язык OCR**, запустить четыре параллельных воркера и вывести результаты. К концу вы получите надёжный шаблон, который можно вставить в любой Java‑проект — без лишних «надстроек», только нужный код.

## Что вы узнаете

- Как применить лицензию Aspose OCR, чтобы не столкнуться с ограничениями демо‑версии.  
- Точные шаги для **распознавания текста с изображений** параллельно, повышая пропускную способность на многопроцессорных машинах.  
- Почему и как **установить язык OCR** (во примере — французский) для лучшей точности.  
- Практический способ **извлечения текста из png** файлов, при этом тот же код работает и с JPG, TIFF, BMP и т.д.  

**Предварительные требования** — Java 8 или новее, Maven или Gradle для получения библиотеки Aspose OCR и действительный файл лицензии Aspose OCR (`Aspose.OCR.Java.lic`). Никаких особых трюков в IDE не требуется; любой редактор, способный компилировать Java, подойдёт.

---

## Шаг 1: Добавьте зависимость Aspose OCR

Сначала убедитесь, что JAR Aspose OCR находится в вашем classpath. Если вы используете Maven, добавьте:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Для Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Следите за примечаниями к релизам Aspose; часто добавляются языковые пакеты или улучшения производительности, которые могут сократить время выполнения пакета на несколько секунд.

## Шаг 2: Примените лицензию Aspose OCR

Без лицензии библиотека работает в демо‑режиме и будет вставлять водяные знаки в вывод. Загрузите файл лицензии один раз, желательно при старте приложения.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Вызов `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` гарантирует, что каждый последующий вызов **распознавания текста с изображений** будет выполняться без ограничений.

## Шаг 3: Подготовьте список изображений

В пакетный процессор можно передать любую коллекцию путей к файлам. Ниже показан пример **извлечения текста из png** вместе с JPEG и TIFF — просто замените пути на свои.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Зачем список?** `OcrBatchProcessor` ожидает `List<String>`, чтобы автоматически распределять работу по потокам.

## Шаг 4: Настройте и запустите параллельный пакетный процессор

Теперь к сердцу руководства: создание `OcrBatchProcessor`, указание количества потоков и **установка языка OCR** на французский (можно изменить на `OcrLanguage.ENGLISH` или любой поддерживаемый язык).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Как это работает

- **Количество потоков** — Процессор создаёт пул потоков указанного размера. На ноутбуке с четырёхъядерным процессором `4` — хорошее значение; увеличьте его для серверов с большим числом ядер.  
- **Настройка языка** — Вызвав `setLanguage(OcrLanguage.FRENCH)`, мы просим OCR‑движок сместить словарь в сторону французских символов, что значительно повышает точность для неанглийских документов.  
- **Пакетное распознавание** — Метод `recognize` внутри перебирает переданный список, распределяет работу и возвращает `List<OcrResult>`, сохраняющий исходный порядок. Это самый простой способ **распознавать текст с изображений** без написания собственного кода управления потоками.

## Шаг 5: Проверьте вывод

При запуске программы вы должны увидеть что‑то вроде:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

Если французский файл (`doc1.png`) содержит французский текст, шаг **установки языка OCR** поможет правильно захватить символы с диакритическими знаками. Для PNG‑файлов это демонстрирует чистый способ **извлечения текста из png**, одновременно обрабатывая другие форматы в том же пакете.

---

## Обработка распространённых граничных случаев

### 1️⃣ Отсутствующие или повреждённые изображения

Если путь к изображению недействителен, `OcrBatchProcessor` бросает `IOException`. Оберните вызов в блок `try‑catch`, залогируйте проблемный файл и продолжайте обработку остальных.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ Смешанные языки в одном пакете

Когда документы находятся на разных языках, можно:

- Запустить отдельные пакеты, каждый со своим `setLanguage`.  
- Либо оставить язык неустановленным (`OcrLanguage.AUTO_DETECT`) и позволить Aspose угадывать, хотя точность может пострадать.

### 3️⃣ Ограничения памяти

Обработка очень больших изображений (например, >10 МБ) может увеличить использование кучи. Предварительно уменьшите размер изображений или увеличьте флаг JVM `-Xmx`, если столкнётесь с `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ Настройка параметров OCR

Помимо языка, можно регулировать соотношение скорости и точности распознавания:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

Выбор `ACCURATE` медленнее, но даёт лучшие результаты для шумных сканов.

---

## Полный рабочий пример (все файлы)

Ниже представлен полный набор исходных файлов, которые вам понадобятся. Скопируйте их в Maven‑проект, поправьте путь к лицензии и директорию с изображениями, затем выполните `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Запустите, и вы увидите извлечённый текст каждого файла, выведенный в консоль — именно то, что нужно при построении поисковых архивов, автоматизации ввода данных или инструментах доступности.

---

## Заключение

Мы рассмотрели полностью готовый к продакшну шаблон для **распознавания текста с изображений** с помощью Aspose OCR для Java. Настроив пакетный процессор, вы сможете **извлекать текст из png** (и других форматов) параллельно, а возможность **установки языка OCR** гарантирует максимальную точность для многоязычных нагрузок.

Что дальше? Попробуйте переключить язык на `OcrLanguage.SPANISH` или поэкспериментировать с `OcrRecognitionMode.ACCURATE` для более сложных сканов. Вы также можете интегрировать результаты в базу данных, передать их в поисковый индекс или направить в API перевода.

Есть сложный сценарий — например OCR для PDF или изображений, хранящихся в облаке? Это естественное расширение того, что мы построили сегодня. Погружайтесь, настраивайте параметры и позволяйте OCR‑движку выполнять тяжёлую работу.

Счастливого кодинга, и пусть извлечение текста будет быстрым и точным!

## Что вам стоит изучить дальше?

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}