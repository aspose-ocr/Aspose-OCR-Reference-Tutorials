---
category: general
date: 2026-06-06
description: Извлеките текст из отсканированного изображения с помощью Aspose OCR
  для Java. Узнайте, как распознавать текст из файлов TIFF с параллельной обработкой.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: ru
og_description: Извлекайте текст из отсканированного изображения с помощью Aspose
  OCR. Это руководство показывает, как эффективно распознавать текст из файлов TIFF,
  используя Java.
og_title: Извлечение текста из отсканированного изображения – учебник Aspose OCR Java
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Извлечение текста из отсканированного изображения в Java — Полное руководство
  по Aspose OCR
url: /ru/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из отсканированного изображения – Полное руководство по Aspose OCR

Когда‑то вам нужно было **извлечь текст из отсканированного изображения**, но вы не знали, как это сделать? Вы не одиноки. Будь то оцифровка старых архивов, извлечение данных из счетов‑фактур или создание библиотеки PDF с возможностью поиска, получение надёжного текста из TIFF‑скана может стать проблемой.  

Хорошие новости: с Aspose OCR for Java вы можете **распознавать текст из tiff** файлов всего в несколько строк кода, а также ускорить процесс, ограничив движок несколькими ядрами CPU. В этом руководстве мы пройдём весь процесс — от настройки библиотеки до обработки результата — чтобы вы могли сразу скопировать и вставить рабочий пример.

## Что покрывает это руководство

- Установка Aspose OCR for Java (Maven или ручное добавление JAR)
- Загрузка большого отсканированного TIFF‑изображения
- Настройка движка для использования до 4 потоков (параллельный OCR)
- Запуск процесса OCR и вывод извлечённого текста
- Распространённые подводные камни (память, много‑страничные TIFF) и как их избежать
- Быстрый совет по производительности: когда настраивать `setMaxThreads`

К концу вы сможете **извлекать текст из отсканированных изображений** надёжно и поймёте, почему изменение количества потоков имеет значение при *распознавании текста из tiff* в производственной цепочке.

---

![extract text from scanned image example](example.png "Screenshot showing extracted text from a scanned TIFF image")

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

1. **Java Development Kit (JDK) 8+** — любая современная версия подходит.  
2. **Maven** (или возможность добавить JAR‑файлы вручную) — мы будем использовать Maven для простоты.  
3. Лицензия **Aspose OCR for Java** (бесплатная оценочная версия работает, но добавляет водяной знак).  
4. Большой **TIFF‑скан** (например, `large_scan.tif`), который вы хотите обработать.

Если что‑то из этого вам незнакомо, не переживайте — каждый шаг объяснён ниже.

## Шаг 1: Добавьте Aspose OCR в ваш проект

### Пользователи Maven

Добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Ручная настройка JAR

Скачайте последнюю версию `aspose-ocr-xx.jar` с сайта Aspose и разместите её в classpath.  

> **Pro tip:** Храните JAR в папке `libs/` и укажите её в настройках проекта IDE. Это избавит от неожиданностей типа «class not found» позже.

## Шаг 2: Создайте простой Java‑класс

Создайте файл `ParallelOcrDemo.java` в папке исходного кода (`src/main/java`). Этот класс будет содержать весь рабочий процесс OCR.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Почему мы ограничиваем потоки:** По умолчанию Aspose OCR пытается задействовать все ядра, что может «голодать» другие сервисы на совместно используемом сервере. Установка `setMaxThreads(4)` сообщает движку использовать до четырёх параллельных работников — достаточно для заметного ускорения на большинстве современных процессоров без монополизации ресурсов.

## Шаг 3: Скомпилируйте и запустите

Откройте терминал в корне проекта и выполните:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Если вы не используете Maven, компилируйте с помощью `javac` и запускайте:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Ожидаемый вывод

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

Консоль выведет обычный текст того, что было на отсканированной странице. Если изображение содержит несколько страниц, Aspose OCR объединит их в порядке следования.

## Шаг 4: Обработка много‑страничных TIFF (особый случай)

Распространённый сценарий — **много‑страничный TIFF** — например, отсканированная книга. По умолчанию `OcrInputImage` читает только первый кадр. Чтобы обработать все страницы, используйте `OcrInputImage` с `FileInputStream` и включите поддержку много‑страничных файлов:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Теперь `ocrEngine.process()` вернёт один `OcrResult`, содержащий объединённый текст со всех страниц.

## Шаг 5: Тонкая настройка точности распознавания

Если вы замечаете **искажённые символы** или пропущенные слова, попробуйте следующие настройки:

| Параметр | Что делает | Когда использовать |
|----------|------------|---------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Принудительно использует английскую модель (быстрее и точнее для английских сканов) | Документ однородно на английском |
| `ocrEngine.getSettings().setResolution(300)` | Увеличивает низко‑разрешённые изображения перед распознаванием | Скан ниже 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Пытается очистить пятна и артефакты | Скан с сильным шумом |

Пример кода:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Шаг 6: Экспорт результатов в файл

Вывод в консоль подходит для демонстраций, но в продакшене обычно пишут результат в полезное место:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Теперь у вас есть обычный текстовый файл, который можно передать в поисковый индекс, базу данных или последующий аналитический конвейер.

---

## Часто задаваемые вопросы (FAQ)

**В: Работает ли это с PNG или JPEG?**  
О: Абсолютно. `OcrInputImage` принимает любой формат, который может прочитать Java ImageIO. Просто замените расширение файла в пути.

**В: На моём сервере 8 ядер — нужно ли ставить `setMaxThreads(8)`?**  
О: Можно, но помните, что другим сервисам тоже нужны CPU‑циклы. Хорошее правило — «общее количество ядер – 1» для выделенных OCR‑рабочих.

**В: Что делать, если результат OCR пустой?**  
О: Проверьте, что изображение не полностью белое, что указана правильная язык‑модель, и что разрешение минимум 200 DPI. Скан низкого качества часто требует предварительной обработки (выравнивание, повышение контрастности) перед передачей в Aspose OCR.

---

## Итоги

Мы только что **извлекли текст из отсканированных изображений** с помощью Aspose OCR for Java и теперь знаем, как **распознавать текст из tiff** эффективно, используя параллельную обработку. Полный код находится в приведённых выше фрагментах, и вы можете сразу скопировать‑вставить его в свой проект.

### Что дальше?

- **Пакетная обработка**: перебрать каталог TIFF‑файлов, сохранять каждый результат в отдельный файл.  
- **Интеграция с Elasticsearch**: индексировать извлечённый текст для быстрого полнотекстового поиска.  
- **Добавление определения языка**: использовать `OcrLanguage.AutoDetect` для многоязычных документов.  

Экспериментируйте с этими идеями, и вы быстро превратите гору отсканированных бумаг в поисковые, пригодные к использованию данные.

Удачной разработки, и оставляйте комментарии, если столкнётесь с проблемами!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}