---
category: general
date: 2026-02-14
description: 'Пакетное OCR изображений стало простым: узнайте, как извлекать текст
  из PNG‑файлов с помощью Aspose OCR и параллельной обработки в Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: ru
og_description: Учебник по пакетному OCR изображений, показывающий, как извлекать
  текст из PNG‑файлов с использованием асинхронного API Aspose OCR в Java.
og_title: Пакетное распознавание изображений в Java – Быстрое извлечение текста из
  PNG
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Пакетное OCR изображений в Java – быстрое извлечение текста из PNG‑файлов
url: /ru/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

formatting.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетное распознавание изображений OCR в Java – Быстрое извлечение текста из PNG‑файлов

Когда‑нибудь вам нужно было выполнить **batch image OCR** в папке со сканами PNG, но вы беспокоитесь о скорости? Вы не одиноки. Во многих реальных проектах — оцифровка счетов, архивирование отсканированных книг или обработка чеков — разработчики должны **extract text from PNG** изображения быстро и надёжно.  

Хорошая новость? С асинхронным API Aspose OCR вы можете запустить параллельный OCR‑конвейер всего в несколько строк Java. В этом руководстве мы пройдём полный, готовый к запуску пример, объясним, почему каждый элемент важен, и покажем, как проверить результаты. К концу вы получите автономную программу, обрабатывающую целый пакет PNG‑файлов параллельно, выдавая чистый текст с проверкой орфографии.

## Что вы узнаете

- Как собрать список PNG‑файлов для пакетной обработки  
- Как настроить `OcrEngine` от Aspose для английского языка и коррекции орфографии  
- Как запускать OCR асинхронно с помощью `processAsync` и обрабатывать результат `Future`  
- Как читать и выводить распознанный текст для каждого изображения  
- Советы по масштабированию, обработке ошибок и оптимизации производительности  

### Предварительные требования

- Установлен Java 8 или новее (код использует стандартный пакет `java.util.concurrent`)  
- Лицензия Aspose OCR for Java или бесплатная пробная версия (скачайте с сайта Aspose)  
- Папка, содержащая несколько PNG‑скриншотов или отсканированных страниц для тестирования  

Теперь давайте приступим.

## Шаг 1 – Сбор PNG‑файлов для пакетной обработки

Прежде чем движок OCR сможет что‑то сделать, ему нужно знать, какие изображения обрабатывать. Самый простой способ — создать `List<String>` с абсолютными или относительными путями к файлам.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Почему это важно:**  
Создание списка заранее позволяет движку планировать обработку каждого файла независимо, что является основой истинной пакетной обработки. Если позже понадобится сканировать каталог динамически, просто замените статический `Arrays.asList` на поток `Files.walk`.

## Шаг 2 – Инициализация и настройка Aspose OCR Engine

`OcrEngine` от Aspose сильно настраиваемый. Здесь мы задаём язык — английский — и включаем коррекцию орфографии — два параметра, которые значительно повышают качество извлечённого текста, особенно из шумных PNG‑сканов.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Почему такие настройки:**  
- **Выбор языка** сообщает движку, какой набор символов и словарь использовать, уменьшая количество ложных распознаваний.  
- **Коррекция орфографии** исправляет типичные ошибки OCR (например, «1» вместо «l») без необходимости постобработки вывода.

> **Pro tip:** Если ваши изображения содержат несколько языков, вы можете передать список, например `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Шаг 3 – Запуск асинхронной пакетной обработки

Тяжёлая работа происходит в `processAsync`. Он возвращает `Future<List<OcrResult>>`, позволяя главному потоку выполнять другие задачи, пока OCR работает в фоне.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Почему асинхронно:**  
Последовательный запуск OCR может быть ужасно медленным — каждый PNG может занимать секунду и более. Делегируя работу пулу потоков, вы используете несколько ядер CPU и резко сокращаете общее время выполнения.

## Шаг 4 – Получение результатов, когда они готовы

Когда понадобится использовать вывод, просто вызовите `get()` у `Future`. Этот вызов блокируется только до завершения OCR, после чего возвращает список объектов `OcrResult` в том же порядке, что и входной список.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Обработка тайм‑аутов:**  
Если хотите избежать бесконечного ожидания, используйте `ocrFuture.get(60, TimeUnit.SECONDS)` и перехватите `TimeoutException`, чтобы реализовать резервный сценарий.

## Шаг 5 – Вывод распознанного текста для каждого PNG

Теперь, когда результаты получены, пройдитесь по ним и выведите извлечённый текст рядом с оригинальным именем файла. Здесь вы, наконец, **extract text from PNG** файлы.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Пример ожидаемого вывода**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Если движок OCR не может распознать страницу, соответствующий `getText()` вернёт пустую строку — это стоит проверять в продакшн‑коде.

## Полный рабочий пример

Ниже полностью готовая к запуску программа, объединяющая все части. Скопируйте её в файл `ParallelOcrDemo.java`, замените `YOUR_DIRECTORY` на путь к вашей папке с PNG и выполните `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Запуск демо

1. **Компиляция** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Выполнение** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Вы должны увидеть имя каждого PNG‑файла, за которым следует извлечённый текст, разделённый тире.  

> **Note:** Если вы получаете `LicenseException`, убедитесь, что загрузили лицензию Aspose перед созданием движка:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Масштабирование – Советы для реального пакетного OCR

| Ситуация | Рекомендация |
|-----------|----------------|
| **Сотни PNG** | Увеличьте размер пула потоков через `ocrEngine.setThreadPoolSize(8)` (или больше, в зависимости от количества ядер). |
| **Ограничения памяти** | Обрабатывайте файлы небольшими порциями (например, по 50) и освобождайте список `OcrResult` после каждой порции. |
| **Переменное качество изображений** | Включите `setPreprocessingOptions` для автоматического поворота, исправления наклона или повышения контрастности перед распознаванием. |
| **Несколько языков** | Вызовите `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` и при необходимости задайте пользовательский словарь. |
| **Обработка ошибок** | Оберните `ocrFuture.get()` в блок try‑catch для `ExecutionException`, чтобы логировать неудавшиеся файлы без прерывания всей партии. |

Эти стратегии делают ваш **batch image OCR** конвейер надёжным, даже когда объём входных данных растёт.

## Часто задаваемые вопросы

**В: Работает ли это с JPEG или TIFF файлами?**  
О: Абсолютно. Метод `processAsync` принимает любой формат, поддерживаемый Aspose OCR (PNG, JPEG, TIFF, BMP и т.д.). Просто измените расширения файлов в вашем списке.

**В: Как сохранить макет (таблицы, колонки)?**  
О: Aspose OCR предоставляет метод `getLayoutResult()`, который возвращает позиционные данные. Вы можете воссоздать таблицы, анализируя ограничительные рамки каждого слова.

**В: Можно ли запускать это на безсерверной платформе?**  
О: Да — упакуйте JAR с библиотекой Aspose и разверните в AWS Lambda, Azure Functions или Google Cloud Functions. Не забудьте выделить достаточный объём памяти для пула потоков OCR.

## Заключение

Теперь у вас есть полностью готовое, автономное решение **batch image OCR**, эффективно **extract text from PNG** файлы с помощью асинхронного API Aspose OCR в Java. В руководстве рассмотрены все этапы: подготовка списка файлов, настройка языка и коррекции орфографии, запуск параллельной обработки, работа с результатами и масштабирование конвейера для производственных нагрузок.

Готовы к следующему шагу? Попробуйте переключить язык на французский, поэкспериментировать с пользовательскими словарями или интегрировать вывод в поисковый индекс ElasticSearch. Возможности безграничны, когда вы сочетаете быстрый пакетный OCR с современной конкурентностью Java.

Счастливого кодинга, и пусть ваше извлечение текста будет быстрым и точным! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Диаграмма, показывающая параллельных OCR‑работников, обрабатывающих несколько PNG‑файлов"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}