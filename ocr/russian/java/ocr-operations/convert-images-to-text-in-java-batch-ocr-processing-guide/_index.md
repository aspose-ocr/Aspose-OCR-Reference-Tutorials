---
category: general
date: 2026-01-02
description: Преобразуйте изображения в текст с помощью Java и Aspose OCR. Освойте
  пакетную обработку OCR, считывайте изображения из папки и фильтруйте файлы по расширению.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: ru
og_description: Быстро преобразуйте изображения в текст с помощью Java. Этот учебник
  охватывает пакетную обработку OCR, чтение изображений из папки и фильтрацию файлов
  по расширению.
og_title: Преобразование изображений в текст на Java — полное руководство по пакетному
  OCR.
tags:
- OCR
- Java
- Aspose
title: Преобразование изображений в текст на Java – Руководство по пакетной обработке
  OCR
url: /ru/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображений в текст на Java – Руководство по пакетной обработке OCR

Когда‑то вам нужно было **convert images to text**, но вы не знали, как обработать десятки файлов одновременно? Вы не одиноки — разработчики постоянно борются с извлечением данных из PNG, JPG и других сканов. Хорошая новость? С Aspose OCR вы можете за считанные минуты создать конвейер пакетной обработки OCR, читать изображения из структуры папок и даже фильтровать файлы по расширению, работая только с нужными.

В этом руководстве мы построим автономную программу на Java, которая обходит каталог, выбирает каждый `.png` или `.jpg`, отправляет каждое изображение в Aspose OCR асинхронно и выводит извлечённый текст в исходном порядке. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект, требующий **convert images to text** в масштабе.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Что вы построите

- Один движок `AsposeOCR`, общий для всех потоков (эффективный и thread‑safe).  
- `ParallelRecognizer`, который запускает OCR‑задачи параллельно, идеально подходит для **batch OCR processing**.  
- Логику, которая **reads images from folder** с использованием `java.nio.file.Files`.  
- Простые фильтры для **extract text from PNG** файлов, при этом поддерживая JPG.  
- Чистое завершение внутреннего пула потоков, чтобы избежать утечек ресурсов.

### Предварительные требования

- Java 17 (или любая современная LTS‑версия).  
- Maven или Gradle для получения библиотеки Aspose OCR.  
- Папка, заполненная PNG/JPG изображениями, которые вы хотите обработать.  
- Базовое знакомство с Java streams — ничего сложного не требуется.

> **Pro tip:** Если у вас ещё нет лицензии, Aspose предлагает бесплатный временный ключ для тестирования.

---

## Шаг 1 – Настройка проекта и добавление Aspose OCR

Сначала создайте новый Maven‑проект (или Gradle, как вам удобнее). Добавьте зависимость Aspose OCR в `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Why this matters:** Объявление зависимости заранее гарантирует, что компилятор увидит `AsposeOCR`, `ParallelRecognizer` и связанные классы. Это также обеспечивает использование одной и той же версии на всех машинах, что критично для воспроизводимой **batch OCR processing**.

После завершения сборки обновите IDE, и вы должны увидеть пакеты Aspose в `External Libraries`.

---

## Шаг 2 – Convert Images to Text – Инициализация OCR‑движка

Нужен только **one** экземпляр OCR‑движка на всё выполнение. Совместное использование его в потоках экономит память и ускоряет работу, поскольку движок загружает языковые пакеты лишь один раз.

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

> **Explanation:** `ParallelRecognizer` оборачивает движок в thread‑pool. Когда вы отправляете множество файлов, каждый получает свой рабочий поток, обеспечивая истинный параллелизм на многоядерных процессорах.

---

## Шаг 3 – Read Images from Folder – Обход дерева каталогов

Теперь нам нужно **read images from folder** и собрать все PNG и JPG. API `Files.walk` делает это в одну строку, но мы добавим фильтр, чтобы **extract text from PNG** только при необходимости.

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

> **Why we filter here:** Использование `filter` позволяет **filter files by extension** на раннем этапе, что сокращает ненужный ввод‑вывод позже. Это также делает код более читаемым — без сложных регулярных выражений.

---

## Шаг 4 – Batch OCR Processing – Отправка задач асинхронно

Имея готовый список файлов, мы передаём каждый путь в `ParallelRecognizer`. Метод `recognizeAsync` возвращает `Future<OcrResult>`, который мы сохраняем для последующего получения.

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

> **What’s happening under the hood?** Каждый вызов ставит задачу в внутренний executor‑service распознавателя. Задачи выполняются параллельно, поэтому папка с 100 изображениями может быть обработана за долю времени, требуемого однопоточного цикла.

---

## Шаг 5 – Retrieve Results in Original Order – Сохранение последовательности файлов

Поскольку futures сохранены в том же порядке, что и `imagePaths`, мы просто проходим по списку и вызываем `get()`. Вызов блокируется только до завершения конкретного изображения, сохраняя порядок без дополнительного учёта.

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

**Sample console output** (truncated for brevity):

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

> **Edge case handling:** Если конкретное изображение вызывает исключение (повреждённый файл, неподдерживаемый формат), мы перехватываем его и продолжаем обработку остальных — важная привычка для надёжных **batch OCR processing** конвейеров.

---

## Шаг 6 – Clean Up – Завершение работы распознавателя

Никогда не забывайте завершать внутренний пул потоков; иначе ваш JVM может зависнуть при выходе.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Вот и всё! Программа теперь обходит любой каталог, фильтрует PNG/JPG файлы, запускает OCR параллельно и выводит результаты.

---

## Полный рабочий пример

Ниже полностью готовый к копированию Java‑класс. Замените `"YOUR_DIRECTORY"` на путь к вашей папке с изображениями и запустите его из IDE или командной строки.

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

Запустите класс, наблюдайте, как консоль заполняется извлечёнными строками, и радуйтесь тому, что вы только что **converted images to text** без написания единого цикла, блокирующего ввод‑вывод.

---

## Часто задаваемые вопросы (FAQs)

**Q: Can I process PDFs or TIFFs as well?**  
A: Absolutely. Aspose OCR supports many formats—just add the appropriate file extensions to the filter in Step 2.

**Q: What if I need a different language, like Spanish?**  
A: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`. Make sure the language pack is installed (Aspose includes most major languages out of the box).

**Q: My folder contains sub‑folders—will they be scanned?**  
A: Yes. `Files.walk` traverses the entire tree recursively, so every nested PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}