---
category: general
date: 2026-02-17
description: Узнайте, как использовать фиксированный пул потоков в Java для извлечения
  текста из PNG‑изображений с параллельной обработкой OCR и корректного завершения
  сервиса‑исполнителя.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: ru
og_description: Узнайте, как фиксированный пул потоков в Java может извлекать текст
  из PNG‑изображений параллельно, конвертировать текст отсканированных страниц и безопасно
  завершать работу сервиса исполнителей.
og_title: Фиксированный пул потоков Java – параллельный OCR для PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Фиксированный пул потоков Java – параллельный OCR для PNG
url: /ru/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

with same number of #.

Also maintain bullet list formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# фиксированный пул потоков java – параллельный OCR для PNG

Задумывались когда‑нибудь, как ускорить OCR для множества PNG‑файлов, используя **fixed thread pool java**? В этом руководстве мы пройдемся по **extract text from PNG** изображениям параллельно, **convert scanned pages text** в редактируемые строки и безопасно **shut down executor service**, когда работа завершится.

Если вы когда‑либо смотрели на однопоточный цикл, который тянется минутами, вы знаете, как раздражает ожидание завершения каждой страницы перед началом следующей. Хорошие новости? С несколькими строками Java и Aspose OCR вы можете задействовать все ядра процессора, превратить отсканированные страницы в поисковый текст и сохранить отзывчивость приложения.  

Ниже вы найдёте полностью готовый к запуску пример, а также объяснения, почему каждый элемент важен, типичные подводные камни и советы, которые подойдут для любой OCR‑библиотеки.

---

## Что понадобится

- **Java 17** (или любой современный JDK) – код использует современный синтаксис `var` умеренно, но работает и на более старых версиях.  
- **Aspose.OCR for Java** library – её можно получить из Maven Central или скачать пробную версию с сайта Aspose.  
- Набор **PNG** файлов, которые нужно обработать – например, сканированные чеки, страницы книг или скриншоты.  
- Базовое знакомство с конкуррентностью в Java – не обязательно, но будет полезно.

Это всё. Никаких внешних сервисов, Docker не требуется, только чистый Java и немного магии многопоточности.

## Step 1: Add Aspose OCR Dependency & License (Optional)

Сначала убедитесь, что JAR‑файл Aspose OCR находится в вашем classpath. Если вы используете Maven, добавьте:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Если у вас нет лицензии, библиотека будет работать в режиме оценки; код будет вести себя так же. Чтобы загрузить лицензию (рекомендовано для продакшена), поместите `Aspose.OCR.lic` в папку ресурсов и используйте:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Держите файл лицензии вне системы контроля версий, чтобы избежать случайного раскрытия.

## Step 2: Create a Thread‑Safe `OcrEngine` Instance

`OcrEngine` из Aspose OCR потокобезопасен, пока вы переиспользуете один и тот же экземпляр в разных задачах. Создание его один раз экономит память и избавляет от накладных расходов на повторную инициализацию движка для каждого изображения.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Почему переиспользовать? Представьте движок как тяжёлого работника, который загружает языковые модели в память. Создавать новый движок для каждого изображения — всё равно что нанимать нового специалиста для каждой крошечной задачи — дорого и ненужно.

## Step 3: Set Up a Fixed Thread Pool Java

Теперь звезда шоу: **fixed thread pool java**. Мы зададим его размер равным количеству логических процессоров, чтобы каждый ядро получало работу без переизбытка потоков.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Использование *фиксированного* пула (в отличие от кеширующего) даёт предсказуемое потребление ресурсов и предотвращает страшные всплески «out‑of‑memory», когда одновременно поступают сотни изображений.

## Step 4: List the PNG Files You Want to Process (Extract Text from PNG)

Соберите пути к изображениям, которые нужно распознать. В реальном проекте вы, вероятно, будете сканировать каталог или читать из базы данных; здесь мы просто жёстко зададим несколько примеров.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** Расширение файла **png** важно, потому что Aspose OCR автоматически определяет формат, но вы также можете подавать JPEG или TIFF.

## Step 5: Submit OCR Tasks – Parallel OCR Processing

Каждое изображение превращается в `callable`, который возвращает распознанный текст. Поскольку `OcrEngine` общий, нам нужно лишь передать путь к файлу в задачу.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Зачем оборачивать в `Future`? Это позволяет мгновенно запустить все задачи, а затем собрать результаты в том порядке, в котором они были отправлены – идеально для сохранения порядка страниц при **convert scanned pages text** обратно в документ.

## Step 6: Retrieve Results and Display (Convert Scanned Pages Text)

Теперь ждём завершения каждого `Future` и выводим результат. Вызов `get()` блокирует только до завершения конкретной задачи, а не всего пула.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Типичный вывод в консоль выглядит так:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Если вам удобнее записывать результаты в файлы, замените `System.out.println` на вызов `Files.writeString`.

## Step 7: Cleanly Shut Down the Executor Service

Когда все задачи завершены, критически важно **shut down executor service**; иначе ваш JVM может держать не‑демонские потоки живыми, препятствуя корректному завершению.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Шаблон `awaitTermination` даёт пулу шанс завершить текущую работу перед принудительным завершением. Игнорирование этого шага — частая причина утечек памяти в длительно работающих приложениях.

## Full Working Example

Собрав всё вместе, получаем полностью готовую программу, которую можно скопировать в `ParallelBatchDemo.java` и запустить:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}