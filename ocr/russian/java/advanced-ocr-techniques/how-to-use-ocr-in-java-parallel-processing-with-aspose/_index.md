---
category: general
date: 2026-10-24
description: Узнайте, как выполнять OCR в PDF и TIFF‑изображениях на Java с использованием
  parallel processing от Aspose OCR. Быстрое, надёжное руководство для разработчиков.
draft: false
keywords:
- perform ocr pdf
- extract image text
- java ocr library
- process scanned pdf
- aspose ocr maven
lastmod: 2026-10-24
og_description: Выполняйте OCR PDF‑файлов на Java быстро с помощью parallel processing
  от Aspose OCR. В этом руководстве показано, как включить multi‑threaded OCR, настроить
  thread limits и эффективно извлекать текст как из PDF, так и из TIFF‑изображений.
og_image_alt: Diagram of Java OCR pipeline with parallel processing using Aspose OCR
og_title: Выполнение OCR в PDF на Java – Parallel processing с Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to perform OCR on PDF and TIFF images in Java using Aspose
    OCR's parallel processing. Fast, reliable guide for developers.
  headline: How to perform OCR on PDF in Java with parallel processing
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR’s parallel engine runs on Windows, Linux, and macOS as
      long as the JVM can create native threads.
    question: Does the parallel mode work on any operating system?
  - answer: Absolutely—pass the password to `processImage` via the overload that accepts
      a `PdfLoadOptions` object.
    question: Can I process password‑protected PDFs?
  - answer: Aspose OCR supports Java 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  - answer: For images under 300 dpi, accuracy drops to around 80 %; increasing the
      resolution to 400 dpi typically pushes it above 95 %.
    question: How accurate is the OCR for low‑resolution scans?
  - answer: Yes, a valid Aspose license removes evaluation limits and enables full‑performance
      features like parallel processing.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- parallel processing
- PDF
title: Как выполнить OCR в PDF на Java с parallel processing
url: /ru/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в PDF на Java с параллельной обработкой

Вы когда‑нибудь задумывались **как использовать OCR**, чтобы извлечь текст из отсканированного документа без усилий? В этом руководстве вы узнаете, как **выполнять OCR PDF** задачи в Java, используя встроенную параллельную обработку Aspose OCR. Этот подход работает как с PDF, так и с TIFF, значительно сокращает время обработки и предоставляет детальный контроль над использованием потоков. К концу вы получите готовый к запуску класс Java, который может извлекать текст изображений из любого отсканированного PDF или многостраничного TIFF за небольшую часть времени, требуемого однопоточным решением.

## Быстрые ответы
- **Что делает параллельный OCR?** Он распределяет страницы по нескольким ядрам CPU, позволяя обрабатывать несколько страниц одновременно.  
- **Какая библиотека используется?** Aspose.OCR для Java, доступная через Maven Central.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; коммерческая лицензия требуется для продакшна.  
- **Можно ли ограничить количество потоков?** Да — используйте `setMaxThreads(int)`, чтобы ограничить пул потоков.  
- **Совместимо ли решение с Java 8 и новее?** Абсолютно, оно работает на Java 8, 11, 17 и более новых версиях.

## Что такое perform OCR PDF?
`perform OCR PDF` относится к процессу извлечения поискового, редактируемого текста из отсканированных PDF‑документов с помощью оптического распознавания символов. Aspose OCR читает растровое изображение каждой страницы, запускает движок распознавания и возвращает обычный Unicode‑текст, который вы можете сохранять, индексировать или далее обрабатывать.

## Почему использовать параллельную обработку Aspose OCR?
Aspose OCR поддерживает **более 50 форматов ввода** (включая PDF, TIFF, JPEG, PNG, BMP) и может обрабатывать **многостраничные документы** без загрузки всего файла в память. Параллельная обработка обычно сокращает время выполнения на **30‑70 % на ноутбуке с 4 ядрами** и до **80 % на сервере с 32 ядрами**, согласно набору тестов Aspose.

## Требования
- Java 8 или новее (код также компилируется с JDK 11).  
- Библиотека Aspose.OCR для Java — вы можете получить последнюю JAR‑файл из Maven Central (`com.aspose:aspose-ocr`).  
- Файл изображения (`.tif`, `.tiff`) или PDF, который вы хотите обработать.  
- Умеренный объём ОЗУ — параллельная обработка запустит несколько потоков, но Aspose эффективно использует память.

Если всё готово, давайте приступим.

![Диаграмма, показывающая конвейер OCR — как использовать OCR в Java с параллельной обработкой](how-to-use-ocr-pipeline.png)

*Текст alt изображения: пример схемы использования OCR*

---

## Как параллельная обработка улучшает скорость OCR?
Параллельная обработка распределяет работу OCR по всем доступным ядрам CPU, позволяя одновременно распознавать несколько страниц. На типичном ноутбуке с четырьмя ядрами включение параллельного режима сокращает время обработки 100‑страничного PDF примерно с 45 секунд до 18 секунд, а рабочая станция с 16 ядрами может выполнить ту же задачу менее чем за 7 секунд. При этом прирост скорости достигается с минимальными затратами памяти, поскольку каждый поток работает с буфером отдельной страницы.

## Как настроить проект и добавить Aspose OCR
Правильная настройка проекта гарантирует, что движок OCR может быть загружен во время выполнения. Добавив зависимость Aspose OCR в файл сборки, вы делаете классы доступными в classpath, что необходимо для всех последующих операций OCR.

### Почему это важно
Прежде чем вы сможете **выполнять OCR в PDF** файлах, библиотека должна находиться в вашем classpath. Без неё компилятор выдаст `ClassNotFoundException`, и вы застрянете на следующем шаге.

### Как это сделать
Если вы используете Maven, добавьте зависимость:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Для Gradle добавьте:

```gradle
implementation 'com.aspose:aspose-ocr:24.10'
```

> **Совет:** Синхронизируйте номер версии с примечаниями к выпуску Aspose; более новые версии часто включают улучшения производительности для параллельной обработки.

## Что такое класс OcrEngine?
`OcrEngine` — основной класс в Aspose OCR, управляющий процессом распознавания изображений и PDF‑документов.  
`OcrEngine` — ядро Aspose OCR, которое выполняет извлечение текста из изображений и PDF‑файлов. Он предоставляет методы для включения параллельной обработки, установки языка и получения распознанного текста в виде строки. Кроме того, он предлагает параметры конфигурации для оптимизации памяти и выбора языка, делая его гибким для широкого спектра сценариев OCR.

## Как создать движок OCR и включить параллельную обработку
Создание экземпляра `OcrEngine` и включение параллельного режима подготавливает библиотеку к распределению работы по ядрам CPU. Вы также можете настроить язык и другие параметры перед обработкой файлов и, при необходимости, ограничить количество потоков в соответствии с вашей средой развертывания.

Загрузите движок, включите параллельный режим и при желании ограничьте пул потоков:

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseParallelProcessing(true);
ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors() - 1);
```

- `setUseParallelProcessing(true)`: сообщает Aspose разделить нагрузку по доступным ядрам CPU.  
- `setMaxThreads(...)`: вы можете ограничить пул потоков, если работаете на совместном сервере или хотите оставить ресурсы для других сервисов.  
- `processImage(inputPath)`: работает как с файлами изображений, так и с PDF‑документами, поэтому тот же вызов **выполняет OCR в PDF** и в TIFF.

## Как обрабатывать разные типы входных данных — PDF vs. TIFF
Хотя `processImage` принимает строку пути, внутренняя обработка различается. PDF часто содержат несколько страниц, каждая из которых становится отдельной задачей OCR. TIFF могут быть одно- или многостраничными; Aspose рассматривает каждый кадр как страницу.

### На что обратить внимание
| Ввод | Типичная проблема | Рекомендуемое решение |
|------|-------------------|-----------------------|
| PDF | Большие PDF могут исчерпать память, если все страницы загружаются одновременно. | Используйте `ocrEngine.getConfig().setMemoryOptimization(true);` (доступно в новых версиях). |
| Многостраничный TIFF | Некоторые старые TIFF используют неподдерживаемое сжатие. | Сначала преобразуйте в поддерживаемый формат или используйте `TiffImage`‑помощник Aspose. |

Ниже приведён быстрый фрагмент, показывающий, как определить тип файла и записать дружелюбное сообщение:

```java
String ext = Files.getFileExtension(inputPath).toLowerCase();
if (ext.equals("pdf")) {
    System.out.println("Processing PDF document...");
} else if (ext.equals("tif") || ext.equals("tiff")) {
    System.out.println("Processing TIFF image...");
} else {
    System.out.println("Unsupported file type: " + ext);
}
```

## Как проверить вывод — что вы должны увидеть?
После выполнения программа выводит извлечённый текст в консоль, сохраняя разрывы строк и разделители страниц. Проверьте вывод, чтобы убедиться, что весь ожидаемый контент присутствует, а любые нечитаемые участки помечены заполнителями, указывающими, где OCR не смог распознать символы.

Когда программа завершится, вы увидите необработанный извлечённый текст, выведенный в консоль. Для простого отсканированного счета-фактуры вывод может выглядеть так:

```
Invoice #12345
Date: 2023‑07‑15
Total Amount: $1,250.00
...
```

Если OCR испытывает трудности с конкретной страницой, Aspose вставляет строку‑заполнитель вроде `[Unrecognizable]`. При необходимости вы можете отфильтровать их позже, чтобы получить чистые данные.

**Быстрая проверка**  
Запустите программу с известным тестовым файлом и сравните вывод консоли с оригинальным документом. Если текст совпадает с точностью не менее 95 %, ваша настройка работает правильно.

## Как настроить производительность — когда регулировать количество потоков
Регулировка количества потоков позволяет сбалансировать использование CPU и накладные расходы. На машинах с небольшим числом ядер меньшее количество потоков уменьшает переключение контекста, а на серверах с большим числом ядер вы можете увеличить его, чтобы полностью использовать параллелизм, всегда тестируя для поиска оптимального значения.

### Как найти оптимальное значение
Запустите серию тестов производительности с различными значениями `setMaxThreads`, измеряя общее время выполнения для репрезентативного документа. Постройте график результатов, чтобы определить точку, в которой добавление новых потоков больше не даёт прироста скорости.

```java
long start = System.nanoTime();
ocrEngine.processImage("large-document.pdf");
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed ms: " + elapsed / 1_000_000);
```

Запустите программу с разными значениями `setMaxThreads` и запишите времена. Выберите конфигурацию, обеспечивающую наилучшую пропускную способность, и зафиксируйте её для продакшна.

## Как расширить демо — пакетная обработка нескольких файлов
Чтобы автоматически обрабатывать множество файлов, пройдитесь по каталогу и вызовите OCR‑процедуру для каждого документа. Этот внешний цикл также можно параллелизовать с помощью `ExecutorService`, если необходимо обрабатывать большой объём файлов одновременно.

```java
Files.list(Paths.get("input-folder"))
     .filter(Files::isRegularFile)
     .forEach(path -> ocrEngine.processImage(path.toString()));
```

Этот шаблон хорошо масштабируется, поскольку движок уже обрабатывает страницы каждого файла параллельно. Внешний цикл выполняется последовательно, но вы также можете отправлять каждый файл в `ExecutorService`, если нужно полностью загрузить большую ферму процессоров.

## Распространённые подводные камни и как их избежать
| Симптом | Вероятная причина | Решение |
|---------|-------------------|----------|
| `OutOfMemoryError` | Слишком много страниц загружено одновременно (особенно большие PDF). | Включите оптимизацию памяти (`setMemoryOptimization(true)`) или обрабатывайте PDF постранично с помощью `processPage`. |
| Искажённые символы | Неправильная настройка языка/кодировки. | Вызовите `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` или соответствующий enum языка. |
| Низкая производительность несмотря на параллельный флаг | ОС ограничивает создание потоков или JVM работает с небольшим размером кучи. | Увеличьте флаг кучи `-Xmx` и проверьте ограничения потоков ОС (`ulimit -u`). |
| Пустой вывод | Разрешение входного изображения < 300 dpi. | Увеличьте масштаб изображения перед OCR или используйте сканер, выдающий более высокое разрешение. |

## Итоги — что мы рассмотрели
- **Как выполнять OCR в PDF** и TIFF файлах на Java с помощью `OcrEngine` от Aspose.  
- Включение **параллельной обработки** для ускорения распознавания.  
- Регулировка количества потоков для оптимальной производительности.  
- Обработка граничных случаев, таких как большие PDF, многостраничные TIFF и настройки языка.  
- Расширение демонстрации для одного файла в пакетный процессор для реальных нагрузок.

## Следующие шаги
Теперь, когда вы освоили основы, рассмотрите изучение следующих связанных тем:
- **Extract image text java** из рукописных заметок (включите `setHandwritingRecognition(true)`).  
- Интеграция вывода OCR с Apache Tika для извлечения метаданных.  
- Сохранение результатов в Elasticsearch для поисковых архивов документов.  
- Использование OCR Aspose с другими языками, такими как Python или .NET — принципы остаются теми же.

Не стесняйтесь экспериментировать с различными ограничениями потоков, форматами изображений и языковыми пакетами. Чем больше вы будете экспериментировать, тем лучше поймёте компромиссы между скоростью и точностью.

## Часто задаваемые вопросы
**Q: Работает ли параллельный режим на любой операционной системе?**  
**A:** Да, параллельный движок Aspose OCR работает на Windows, Linux и macOS, при условии, что JVM может создавать нативные потоки.

**Q: Можно ли обрабатывать PDF, защищённые паролем?**  
**A:** Конечно — передайте пароль в `processImage` через перегрузку, принимающую объект `PdfLoadOptions`.

**Q: Какие версии Java официально поддерживаются?**  
**A:** Aspose OCR поддерживает Java 8, 11, 17 и более новые LTS‑версии.

**Q: Какова точность OCR для сканов низкого разрешения?**  
**A:** Для изображений с разрешением ниже 300 dpi точность падает до около 80 %; увеличение разрешения до 400 dpi обычно повышает её выше 95 %.

**Q: Требуется ли коммерческая лицензия для продакшн‑использования?**  
**A:** Да, действующая лицензия Aspose снимает ограничения оценки и включает функции полной производительности, такие как параллельная обработка.

**Последнее обновление:** 2026-10-24  
**Тестировано с:** Aspose.OCR 24.10 for Java  
**Автор:** Aspose  

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

## Связанные руководства

- [Как использовать OCR в Java для извлечения текста из PDF Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)
- [Распознавание текста PDF с Aspose OCR в Java: полное руководство](/ocr/java/ocr-operations/recognize-pdf-text-with-aspose-ocr-in-java-complete-guide/)
- [Как включить GPU для OCR в Java для извлечения текста из изображения](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}