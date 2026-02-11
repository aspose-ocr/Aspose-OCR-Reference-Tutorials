---
category: general
date: 2026-02-09
description: Узнайте, как выполнять пакетное OCR в Java с помощью Aspose OCR. Извлекайте
  текст из изображений, распознавайте текст из файлов PNG, JPG и TIFF одним вызовом.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: ru
og_description: Освойте пакетное OCR в Java. Это руководство показывает, как извлекать
  текст из изображений PNG, JPG и TIFF с помощью Aspose OCR, предоставляя понятные
  примеры кода.
og_title: Как выполнять пакетное OCR в Java — эффективно извлекать текст из изображений
tags:
- OCR
- Java
- Aspose
title: Как выполнять пакетное OCR в Java – Полное руководство по извлечению текста
  из изображений
url: /ru/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетный OCR в Java – Полное руководство по извлечению текста из изображений

Когда‑то задумывались **как выполнить пакетный OCR** для множества картинок без написания цикла для каждого файла? Вы не одиноки. В реальных проектах часто попадается папка, полная сканов — PNG‑чеков, JPG‑скриншотов или даже многостраничных TIFF‑файлов — и нужен быстрый доступ к тексту.  

Хорошая новость: Aspose OCR позволяет сделать именно это — один вызов метода, который распознаёт текст из PNG, JPG и TIFF файлов сразу. В этом руководстве мы пройдём весь процесс, от настройки проекта до вывода результатов, чтобы вы уже сегодня могли извлекать текст из изображений.

## Что покрывает это руководство

* **Как выполнять пакетный OCR** с помощью `OcrBatchProcessor` от Aspose.
* Способы **извлечения текста из изображений** разных форматов (PNG, JPG, TIFF).
* Советы по управлению параллелизмом, чтобы приложение оставалось отзывчивым.
* Полный, готовый к запуску Java‑пример, который можно скопировать и сразу выполнить.

Никакого предварительного опыта работы с Aspose не требуется — достаточно базовой установки Java и любой IDE. К концу вы получите надёжную основу для распознавания текста из PNG, JPG и TIFF файлов пакетно.

---

![Диаграмма, иллюстрирующая пакетный OCR нескольких файлов изображений](/images/batch-ocr-diagram.png "как выполнить пакетный OCR")

*Текст альтернативы изображения: диаграмма «как выполнить пакетный OCR», показывающая одновременную обработку нескольких файлов изображений.*

## Предварительные требования

| Требование | Почему это важно |
|------------|------------------|
| Java 17 или новее | Aspose OCR ориентирован на современные JVM. |
| Maven или Gradle | Упрощает добавление библиотеки Aspose OCR. |
| Базовые знания Java | Необходимы для понимания потока кода. |
| Набор образцов изображений (`.png`, `.jpg`, `.tif`) | Чтобы увидеть процесс извлечения в действии. |

Если всё уже готово — отлично, приступаем.

## Шаг 1: Добавьте Aspose OCR в проект

Первое, что нужно, — это JAR‑файл Aspose OCR. Для Maven добавьте следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Если вы предпочитаете Gradle, используйте эквивалент:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Добавление зависимости подтягивает всё необходимое для **распознавания текста из png**, **распознавания текста из jpg** и **распознавания текста из tiff**. Дополнительные нативные библиотеки не требуются.

## Шаг 2: Определите файлы изображений, которые нужно обработать

Теперь укажем OCR‑движку, какие файлы обрабатывать. Здесь **как выполнить пакетный OCR** действительно проявляет себя — просто передаёте список путей, а библиотека делает всю тяжёлую работу.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Полезный совет:** Делайте пути к файлам абсолютными или используйте `Paths.get(...)`, чтобы избежать сюрпризов на разных ОС.

## Шаг 3: Создайте процессор пакетов и настройте параллелизм

Aspose OCR поставляется с `OcrBatchProcessor`, который может выполнять несколько распознаваний параллельно. Ограничение количества потоков предотвращает захват CPU, когда у вас десятки изображений.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Зачем ограничивать параллелизм? Если запустить слишком много потоков на скромном ноутбуке, вы можете увидеть замедление вместо ускорения. Метод `setMaxParallelism` позволяет сбалансировать скорость и стабильность.

## Шаг 4: Выполните пакетный вызов OCR

Вот ядро **как выполнить пакетный OCR**: один вызов `recognize`, который возвращает список объектов `RecognitionResult`, по одному на каждое изображение.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Метод блокирует выполнение, пока не обработаются все изображения, а затем отдаёт вам текст. Если нужен асинхронный вариант, его можно обернуть в `CompletableFuture`, но для большинства скриптов синхронный вызов делает код чище.

## Шаг 5: Выведите извлечённый текст

Наконец, пройдитесь по результатам и выведите распознанные строки. Это демонстрирует, что мы успешно **извлекли текст из изображений** разных форматов.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Ожидаемый вывод

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Если OCR‑движок не может прочитать файл, метод `getText()` возвращает пустую строку, поэтому можно добавить простую проверку и вывести предупреждение.

## Полный рабочий пример

Объединив всё вместе, получаем готовый к запуску Java‑класс. Скопируйте его в файл `BatchOcrTutorial.java`, поправьте пути к изображениям и запустите `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Запустите, и консоль выведет извлечённый текст для каждого PNG, JPG и TIFF файла — именно то, что нужно, когда **как выполнить пакетный OCR** стоит перед вами.

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображений больше трёх?

Просто добавьте новые элементы в список `imageFiles`. Процессор пакетов автоматически распределит работу по потокам, настроенным через `setMaxParallelism`.

### Мои изображения находятся в подпапке — нужно ли перечислять каждый вручную?

Можно программно собрать все файлы с нужным расширением:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Это делает код гибким и всё равно сохраняет возможность **выполнять пакетный OCR**.

### Как обрабатывать результаты с низкой уверенностью?

`RecognitionResult` предоставляет метод `getConfidence()`. Можно отфильтровать результаты ниже порога и повторить попытку с более высоким DPI:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Поддерживает ли Aspose OCR другие языки?

Да — просто вызовите `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (или любой поддерживаемый enum) перед вызовом `recognize`. Это расширяет возможности **извлечения текста из изображений** на несколько языков, а не только английский.

## Советы по производительности

* **Размер пакета имеет значение** — большие пакеты снижают накладные расходы, но очень длинные списки могут потреблять больше памяти. Тестируйте с 50–200 изображениями на пакет.
* **Параллелизм** — на 4‑ядерном процессоре обычно оптимально `setMaxParallelism(4)`. Регулируйте в зависимости от нагрузки сервера.
* **Предобработка изображений** — преобразование в градации серого или увеличение контрастности перед OCR может повысить точность, особенно для шумных сканов.

## Заключение

Теперь вы знаете **как выполнять пакетный OCR** в Java с помощью Aspose OCR, как **извлекать текст из изображений** разных форматов и почему важно контролировать параллелизм. Полный пример кода демонстрирует распознавание текста из PNG, JPG и TIFF файлов одним эффективным вызовом.

Готовы к следующему шагу? Попробуйте передать вывод OCR в поисковый индекс, базу данных или даже AI‑резюмирующий сервис. Можно также поэкспериментировать с PDF‑вводом (Aspose OCR его поддерживает) или объединить с библиотеками предобработки изображений, такими как OpenCV, для ещё большей точности.

Счастливого кодинга, и помните — пакетный OCR не обязан быть головной болью. С правильными инструментами и чётким подходом вы превратите кучу картинок в поисковый текст за считанные минуты.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}