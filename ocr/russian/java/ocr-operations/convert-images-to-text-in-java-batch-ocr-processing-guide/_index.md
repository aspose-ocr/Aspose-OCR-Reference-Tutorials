---
category: general
date: 2026-08-28
description: Узнайте, как извлекать текст из png‑изображений в Java с помощью Aspose
  OCR. Этот учебник охватывает пакетную обработку OCR, чтение изображений из папки
  и фильтрацию файлов по расширению.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Узнайте, как извлекать текст из png‑изображений в Java с помощью Aspose
  OCR. Этот учебник охватывает пакетную обработку OCR, чтение изображений из папки
  и фильтрацию файлов по расширению.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Как извлечь текст из png в Java – руководство по пакетному OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Как извлечь текст из png в Java – руководство по пакетному OCR
url: /ru/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь текст из PNG в Java – руководство по пакетному OCR

Если вам когда‑нибудь нужно было **извлечь текст из PNG**‑файлов, но вы не знали, как масштабировать процесс за пределы нескольких изображений, вы попали в нужное место. Многие разработчики начинают с одиночного вызова OCR и быстро сталкиваются с ограничениями производительности, когда папка растёт до десятков или сотен файлов. С Aspose OCR для Java вы можете создать надёжный пакетный конвейер OCR, который обходит каталог, фильтрует только нужные типы изображений, выполняет распознавание параллельно и возвращает результаты в том же порядке, что и исходные файлы. К концу этого руководства у вас будет готовый фрагмент кода Java, который надёжно и эффективно обрабатывает **пакетную OCR‑обработку**.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Быстрые ответы
- **Какая библиотека обрабатывает OCR?** Aspose OCR for Java.
- **Могу ли я обрабатывать PNG и JPG вместе?** Да — пример фильтрует оба расширения.
- **Является ли OCR‑движок потокобезопасным?** Один общий экземпляр `AsposeOCR` безопасен для одновременного использования.
- **Нужна ли лицензия для тестирования?** Бесплатный временный ключ доступен от Aspose.
- **Будут ли автоматически сканироваться подпапки?** `Files.walk` рекурсивно проходит всё дерево.

## Что такое извлечение текста из PNG?

`extract text from png` относится к процессу применения оптического распознавания символов (OCR) к файлам Portable Network Graphics, чтобы видимые символы стали поисковыми, редактируемыми строками. Движок Aspose OCR читает пиксельные данные, определяет формы глифов и возвращает Unicode‑текст одним вызовом метода.

## Почему использовать Aspose OCR для Java?

Aspose OCR поддерживает **30+ языков**, обрабатывает до **500 изображений в минуту** на стандартном 8‑ядерном сервере и может работать с файлами до **200 МБ**, не загружая всё изображение в память. Эти количественные возможности позволяют надёжно запускать крупномасштабные пакетные задания на обычном оборудовании без превышения лимитов памяти.

## Требования
- Java 17 (или любая недавняя LTS‑версия).
- Maven или Gradle для управления зависимостями.
- Каталог, содержащий PNG/JPG‑изображения, которые вы хотите обработать.
- Базовое знакомство с потоками Java и пакетом `java.nio.file`.
- (Опционально) Временный лицензионный ключ Aspose OCR для оценки.

> **Pro tip:** Бесплатный временный ключ истекает через 30 дней, но предоставляет полный доступ к API для тестирования.

## Как пакетный OCR‑конвейер сохраняет порядок?

`Future<OcrResult>` представляет отложенный результат OCR, который можно получить после завершения обработки. Конвейер сохраняет исходный порядок файлов, помещая объекты `Future<OcrResult>` в список, отражающий порядок входной коллекции `Path`. Когда вы позже перебираете futures и вызываете `get()`, каждый вызов блокируется только для соответствующего изображения, поэтому последовательность вывода совпадает с последовательностью ввода без дополнительной сортировки.

## Что такое Aspose OCR для Java?

`AsposeOCR` — основной класс библиотеки Aspose OCR, инкапсулирующий все языковые пакеты, настройки распознавания и внутренние нативные ресурсы. Он предназначен для создания одного экземпляра на время жизни приложения и безопасного совместного использования несколькими потоками. Поскольку языковые данные загружаются только один раз, повторное использование того же экземпляра уменьшает накладные расходы на инициализацию и повышает пропускную способность пакетных операций.

## Как настроить проект и добавить Aspose OCR

Сначала создайте проект Maven (или Gradle) и добавьте зависимость Aspose OCR в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Why this matters:** Объявление зависимости заранее гарантирует, что компилятор увидит `AsposeOCR`, `ParallelRecognizer` и связанные классы. Это также обеспечивает одинаковую версию на всех машинах, что критично для воспроизводимой **пакетной OCR‑обработки**.

Обновите IDE после завершения сборки; теперь вы должны увидеть пакеты Aspose в **External Libraries**.

## Как инициализировать OCR‑движок – использовать один экземпляр

`AsposeOCR` — основной класс OCR‑движка, предоставляемый библиотекой Aspose OCR. Нам нужен **один** экземпляр OCR‑движка для всей работы. Совместное использование его между потоками экономит память и ускоряет процесс, поскольку движок загружает языковые пакеты только один раз.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` потокобезопасен, поэтому его можно безопасно передать `ParallelRecognizer`, который управляет пулом рабочих потоков.

> **Explanation:** `ParallelRecognizer` оборачивает движок в пул потоков. Когда вы отправляете множество файлов, каждый получает свой рабочий поток, обеспечивая истинный параллелизм на многоядерных процессорах.

## Как читать изображения из папки – обход дерева каталогов

`Files.walk` — метод Java NIO, рекурсивно обходящий файловое дерево и возвращающий поток объектов `Path`. Теперь нам нужно **читать изображения из папки** и собрать каждый PNG или JPG. API `Files.walk` делает это однострочником, но мы добавим фильтр, чтобы **извлекать текст из PNG** только при необходимости.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Why we filter here:** Использование `filter` позволяет **фильтровать файлы по расширению** на раннем этапе, что сокращает ненужный ввод‑вывод позже. Это также делает код более читаемым — без сложных регулярных выражений.

## Как отправлять OCR‑задачи асинхронно

`recognizeAsync` отправляет изображение в OCR‑движок для асинхронной обработки и возвращает `Future<OcrResult>`, представляющий отложенный результат. С готовым списком файлов мы передаём каждый путь в `ParallelRecognizer`. Метод `recognizeAsync` возвращает `Future<OcrResult>`, который мы сохраняем для последующего получения.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **What’s happening under the hood?** Каждый вызов помещает задачу во внутренний сервис исполнителей распознавателя. Задачи выполняются параллельно, поэтому папка из 100 изображений может быть обработана за долю времени, требуемого однопоточного цикла.

## Как получать результаты, сохраняя последовательность файлов

`Future<OcrResult>` хранит результат асинхронной OCR‑задачи и предоставляет метод `get()` для получения распознанного текста. Поскольку futures сохранены в том же порядке, что и `imagePaths`, мы просто перебираем список и вызываем `get()`. Вызов блокируется только до завершения конкретного изображения, сохраняя порядок без дополнительного учёта.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Пример вывода консоли (усечённый для краткости):**

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Edge case handling:** Если конкретное изображение бросает исключение (повреждённый файл, неподдерживаемый формат), мы перехватываем его и продолжаем обработку остальных — важная привычка для надёжных **пакетных OCR‑конвейеров**.

## Как очистить ресурсы – завершить работу распознавателя

`ParallelRecognizer.shutdown()` останавливает внутренний пул потоков, гарантируя завершение всех OCR‑задач перед выходом приложения. Никогда не забывайте завершать внутренний пул потоков; иначе ваш JVM может зависнуть при завершении.

```java
recognizer.shutdown();
```

Вот и всё! Программа теперь обходит любой каталог, фильтрует PNG/JPG‑файлы, запускает OCR параллельно и выводит результаты в исходном порядке.

---

## Полный рабочий пример (копировать‑вставить)

Ниже приведён полностью готовый к запуску класс Java. Замените `"YOUR_DIRECTORY"` на путь к папке с вашими изображениями и запустите его из IDE или командной строки.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Запустите класс, наблюдайте, как консоль заполняется извлечёнными строками, и радуйтесь тому, что вы только что **преобразовали изображения в текст** без написания единого цикла, блокирующего ввод‑вывод.

---

## Часто задаваемые вопросы (FAQ)

**В: Могу ли я обрабатывать PDF или TIFF?**  
**О:** Абсолютно. Aspose OCR поддерживает более 30 форматов — включая PDF, TIFF, BMP и GIF — поэтому просто добавьте нужные расширения в фильтр шага обхода каталога.

**В: Что если мне нужен язык, отличный от английского, например испанский?**  
**О:** Замените `RecognitionLanguage.ENGLISH` на `RecognitionLanguage.SPANISH` (или любой поддерживаемый язык). Языковые пакеты включены в библиотеку, дополнительная загрузка не требуется.

**В: Моя папка содержит подпапки — будут ли они сканироваться?**  
**О:** Да. `Files.walk` рекурсивно проходит всё дерево, поэтому каждый вложенный PNG/J

**В: Как обрабатывать чрезвычайно большие изображения, превышающие 200 МБ?**  
**О:** Включите режим потоковой передачи, вызвав `ocrEngine.setUseStreaming(true)`. Это заставит движок читать изображение кусками, резко снижая пиковое потребление памяти.

**В: Есть ли способ ограничить количество одновременно работающих OCR‑потоков?**  
**О:** Да. При создании `ParallelRecognizer` передайте желаемое максимальное количество потоков вторым аргументом (например, `new ParallelRecognizer(ocrEngine, 4)`).

---

**Last Updated:** 2026-08-28  
**Tested with:** Aspose OCR for Java 24.10  
**Author:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Связанные руководства

- [Конвертировать изображения в текст в Java: руководство по пакетной обработке OCR](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Читать текст из изображения в Java: полное руководство Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Извлекать текст из изображений с помощью Aspose.OCR – разрешённые символы](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}