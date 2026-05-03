---
category: general
date: 2026-05-03
description: Создайте фиксированный пул потоков в Java для быстрого извлечения текста
  из изображений. Узнайте, как запускать OCR, преобразовывать изображение в текст
  и повышать производительность с помощью параллельной обработки OCR.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: ru
og_description: Создайте фиксированный пул потоков в Java для быстрого извлечения
  текста из изображений. Узнайте, как запускать OCR, преобразовывать изображение в
  текст и повышать производительность с помощью параллельной обработки OCR.
og_title: Создать фиксированный пул потоков для параллельного OCR в Java
tags:
- Java
- OCR
- Multithreading
title: Создать фиксированный пул потоков для параллельного OCR в Java
url: /ru/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание фиксированного пула потоков для параллельного OCR в Java

Когда‑то вам нужно **создать фиксированный пул потоков**, чтобы ускорить задачи OCR, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах, где много изображений, узким местом является однопоточный вызов OCR, а решение удивительно простое: запустить пул рабочих потоков и позволить им обрабатывать файлы параллельно.  

В этом руководстве вы узнаете, как **извлекать текст из изображений** с помощью Aspose OCR, как **эффективно запускать OCR** и как **преобразовать изображение в текст**, не перегружая процессор. К концу вы получите готовую к запуску Java‑программу, демонстрирующую **параллельную обработку OCR** на нескольких примерах изображений.

## Что вы построите

Мы соберём небольшое консольное приложение, которое:

* Считывает список путей к изображениям (PNG, JPG, TIFF, BMP).
* **Создаёт фиксированный пул потоков**, размер которого соответствует количеству ядер CPU.
* Отправляет задачу OCR для каждого изображения.
* Сбирает распознанный текст и выводит его в консоль.
* Аккуратно завершает работу исполнителя.

Никаких внешних средств сборки, никаких сложных фреймворков — только чистый Java и библиотека Aspose OCR. Если у вас есть Java 8+ и хороший IDE, вы готовы к работе.

## Требования

* **Java Development Kit (JDK) 8 или новее** — код использует лямбда‑выражения, поэтому более старые версии не скомпилируются.
* **Aspose OCR for Java** — скачайте JAR с сайта Aspose или подключите его через Maven (`com.aspose:aspose-ocr`).
* Папка с несколькими тестовыми изображениями (в коде указано `YOUR_DIRECTORY`).  
* Базовое знакомство с конкуренцией в Java (остальное мы объясним).

> *Pro tip:* Если вы используете Maven, добавьте зависимость в ваш `pom.xml` и позвольте IDE управлять classpath.  

---

## Шаг 1: Добавьте необходимые импорты

Сначала импортируем нужные классы. Это не просто шаблонный код; каждый импорт указывает JVM, где находятся движок OCR, утилиты для работы с изображениями и инструменты конкуренции, позволяющие нам **создавать фиксированный пул потоков**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – основной API OCR.  
* `java.util.*` – коллекции для хранения путей к изображениям и результатов.  
* `java.util.concurrent.*` – пакет конкуренции, содержащий `ExecutorService` и `Future`.

---

## Шаг 2: Определите изображения для обработки

Далее перечисляем файлы, из которых хотим **извлекать текст из изображений**. Использование `Arrays.asList` делает код лаконичным и позволяет заменить каталог без изменения остальной логики.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Не стесняйтесь добавлять новые записи; пул потоков автоматически масштабируется в зависимости от количества ядер процессора.

---

## Шаг 3: **Создайте фиксированный пул потоков**, соответствующий ядрам CPU

Это сердце руководства. Мы запрашиваем у среды выполнения количество доступных ядер и просим фабрику `Executors` создать пул именно такого размера. Почему фиксированный? Потому что предсказуемое количество потоков предотвращает «взрыв потоков», который может лишить ОС ресурсов.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` возвращает логическое количество ядер (включая гипертреды).  
* `newFixedThreadPool(coreCount)` гарантирует, что мы никогда не превысим возможности CPU, что является самым безопасным способом **запускать OCR** параллельно.

---

## Шаг 4: Отправьте задачу OCR для каждого изображения

Теперь каждый путь к файлу превращаем в `Callable`, который **выполняет OCR**, распознаёт текст и возвращает результат. Обратите внимание, что внутри лямбда‑выражения мы создаём новый `OcrEngine` — так мы избегаем небезопасного совместного использования состояния движка между потоками.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Каждый вызов `submit` передаёт лямбду в пул, который планирует её на свободный поток.  
* Объекты `Future<String>` позволяют позже получить распознанный текст, сохраняя порядок, если это необходимо.

---

## Шаг 5: Получите и отобразите распознанный текст

После того как все задачи поставлены в очередь, мы просто проходим по списку `Future`, вызывая `get()`, чтобы блокировать выполнение до завершения каждой OCR‑работы. Здесь и проявляется шаг **преобразовать изображение в текст**: вызов `engine.getText()` возвращает готовую строку.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Типичный вывод в консоль выглядит так:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Если файл не удалось обработать (например, он повреждён), вы увидите строку, начинающуюся с `Failed:` и путь к файлу — удобно для быстрой отладки.

---

## Шаг 6: Очистите сервис исполнителя

Никогда не забывайте закрывать пул; иначе JVM может продолжать работать, полагая, что есть ещё задачи. Корректное завершение позволяет завершить все запущенные задачи перед выходом процесса.

```java
executor.shutdown();
```

При необходимости можно вызвать `awaitTermination`, чтобы задать тайм‑аут, но для большинства консольных утилит достаточно простого `shutdown()`.

---

## Полный рабочий пример

Ниже представлен полностью готовый к запуску код. Скопируйте его в файл `ParallelOcrTutorial.java`, поправьте пути к изображениям и запустите `javac` + `java` как обычно.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Ожидаемый результат:** текстовое содержимое каждого изображения выводится в консоль в том же порядке, что и в списке `imagePaths`. Если какое‑то изображение не может быть обработано, вместо пустой строки появится сообщение о сбое.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображений больше, чем потоков?

Фиксированный пул потоков автоматически ставит лишние задачи в очередь. Как только поток завершит текущую работу OCR, он берёт следующую задачу. Такое поведение очереди — суть **параллельной обработки OCR**: вы получаете максимальную пропускную способность без перегрузки процессора.

### Можно ли изменить язык?

Конечно. Замените `engine.getLanguage().setEnglish(true);` на нужный флаг, например `setFrench(true)` или включите несколько языков, вызвав несколько сеттеров перед `recognize()`.

### Как работать с очень большими изображениями?

Большие файлы могут потреблять много памяти на каждый поток. Если появляется `OutOfMemoryError`, попробуйте уменьшить размер изображения перед передачей его в движок или увеличьте размер кучи с помощью `-Xmx`. Другой вариант — использовать **кеширующий пул потоков** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}