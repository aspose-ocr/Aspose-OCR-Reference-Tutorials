---
category: general
date: 2026-02-27
description: Узнайте, как использовать OCR в Java для извлечения текста из изображений
  в файлах TIFF и PDF с помощью параллельной обработки Aspose OCR. Быстрое и простое
  руководство.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: ru
og_description: Узнайте, как использовать OCR в Java для извлечения текста из изображений
  в файлах TIFF и PDF с помощью параллельной обработки Aspose OCR.
og_title: Как использовать OCR в Java – параллельная обработка с Aspose
tags:
- OCR
- Java
- Aspose
title: Как использовать OCR в Java – параллельная обработка с Aspose
url: /ru/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Java – Параллельная обработка с Aspose

Когда‑нибудь задумывались **как использовать OCR**, чтобы извлечь текст из отсканированного документа без особых усилий? Вы не одиноки. Разработчики постоянно сталкиваются с проблемой, когда нужно читать текст с изображений — особенно TIFF и PDF — при этом поддерживая производительность.  

В этом руководстве мы покажем вам полностью готовое решение, которое **извлекает текст из изображений в Java** с помощью Aspose OCR, включает параллельную обработку и даже позволяет ограничить количество потоков. К концу вы получите один класс, способный **perform OCR on PDF** и **extract text from TIFF** за долю времени, требуемого однопоточного подхода.

> **Что вы получите**  
> * Чёткое объяснение, почему параллельный OCR важен.  
> * Полную Java‑программу (без пропущенных импортов).  
> * Советы по настройке использования потоков и устранению распространённых проблем.  

## Требования

- Java 8 или новее (код также компилируется с JDK 11).  
- Библиотека Aspose.OCR for Java – её последнюю JAR‑файл можно взять из Maven Central (`com.aspose:aspose-ocr`).  
- Файл изображения (`.tif`, `.tiff`) или PDF, который нужно обработать.  
- Умеренный объём ОЗУ – параллельная обработка запустит несколько потоков, но Aspose экономичен в использовании памяти.

Если всё это у вас есть, давайте начнём.

![Диаграмма, показывающая конвейер OCR – как использовать OCR в Java с параллельной обработкой](how-to-use-ocr-pipeline.png)

*Текст альтернативного изображения: пример диаграммы использования OCR*

---

## Шаг 1: Настройте проект и добавьте Aspose OCR

### Почему это важно

Прежде чем вы сможете **perform OCR on PDF** или любое изображение, библиотека должна быть в вашем classpath. Без неё компилятор выдаст `ClassNotFoundException`, и вы застрянете на втором шаге.

### Как это сделать

Если вы используете Maven, добавьте зависимость:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Для Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Держите номер версии в синхронизации с примечаниями к выпуску Aspose; новые версии часто включают улучшения производительности для параллельной обработки.

---

## Шаг 2: Создайте OCR‑движок и включите параллельную обработку

### Почему это важно

По умолчанию Aspose OCR работает в одном потоке. Когда вы передаёте ему многостраничный PDF или пакет TIFF‑файлов, движок обрабатывает каждую страницу последовательно – медленно и неэффективно. Включение параллельной обработки позволяет CPU обрабатывать несколько страниц одновременно, резко сокращая время выполнения.

### Код

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

**Объяснение ключевых строк**

- `setUseParallelProcessing(true)`: сообщает Aspose распределить нагрузку между доступными ядрами CPU.  
- `setMaxThreads(...)`: вы можете ограничить пул потоков, если работаете на общем сервере или хотите оставить ресурсы для других сервисов.  
- `processImage(inputPath)`: работает как с файлами изображений, так и с PDF‑документами, поэтому один и тот же вызов **performs OCR on PDF** и на TIFF одинаково.

## Шаг 3: Обработка разных типов входных данных – PDF vs. TIFF

### Почему это важно

Хотя `processImage` принимает строку пути, внутренняя обработка различается. PDF обычно содержит несколько страниц, каждая из которых становится отдельной задачей OCR. TIFF может быть одно‑ или многостраничным; Aspose рассматривает каждый кадр как страницу.

### Что нужно учитывать

| Ввод | Типичная проблема | Рекомендуемое решение |
|------|-------------------|-----------------------|
| PDF | Большие PDF могут исчерпать память, если все страницы загружаются одновременно. | Используйте `ocrEngine.getConfig().setMemoryOptimization(true);` (доступно в новых версиях). |
| Multi‑page TIFF | Некоторые старые TIFF используют неподдерживаемое сжатие. | Сначала конвертируйте в поддерживаемый формат или используйте помощник Aspose `TiffImage`. |

Ниже приведён быстрый фрагмент кода, показывающий, как определить тип файла и вывести дружелюбное сообщение:

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

---

## Шаг 4: Проверка вывода – Что вы должны увидеть?

Когда программа завершится, в консоли будет напечатан необработанный извлечённый текст. Для простого отсканированного счёта вывод может выглядеть так:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Если OCR сталкивается с проблемой на конкретной странице, Aspose вставит строку‑заполнитель вроде `[Unrecognizable]`. Позже вы можете отфильтровать такие строки, если нужны чистые данные.

**Быстрая проверка**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Шаг 5: Настройка производительности – Когда менять количество потоков

### Почему это важно

Большее количество потоков не всегда означает более быстрый результат. На ноутбуке с 4‑ядерным процессором запуск 8 потоков может вызвать накладные расходы на переключение контекста. На сервере с 32 ядрами вы, наоборот, захотите задействовать всю мощность.

### Как найти оптимальное значение

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Запустите программу с разными настройками и измерьте время:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Запишите результаты, выберите конфигурацию, дающую наибольшую пропускную способность, и зафиксируйте её для продакшна.

---

## Шаг 6: Расширение демо – пакетная обработка нескольких файлов

Если вам нужно **extract image text java** из целой папки, оберните основную логику в цикл:

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

Этот шаблон хорошо масштабируется, потому что движок уже обрабатывает страницы каждого файла параллельно. Внешний цикл выполняется последовательно, но при необходимости вы можете отправлять каждый файл в `ExecutorService`, чтобы задействовать полностью большую ферму CPU.

---

## Распространённые ошибки и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| `OutOfMemoryError` | Слишком много страниц загружается одновременно (особенно большие PDF). | Включите оптимизацию памяти (`setMemoryOptimization(true)`) или обрабатывайте PDF постранично с помощью `processPage`. |
| Искажения символов | Неправильная конфигурация языка/кодировки. | Вызовите `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` или соответствующий язык. |
| Низкая производительность несмотря на включённый параллелизм | ОС ограничивает создание потоков или JVM запущена с небольшим размером кучи. | Увеличьте параметр кучи `-Xmx` и проверьте ограничения потоков ОС (`ulimit -u`). |
| Пустой вывод | Разрешение входного изображения < 300 dpi. | Увеличьте масштаб изображения перед OCR или используйте сканер с более высоким разрешением. |

## Итоги – Что мы рассмотрели

- **Как использовать OCR** в Java с `OcrEngine` от Aspose.  
- Включение **параллельной обработки** для ускорения **perform OCR on PDF** и **extract text from TIFF**.  
- Настройка количества потоков для оптимальной производительности.  
- Обработка крайних случаев, таких как большие PDF, многостраничные TIFF и настройки языка.  
- Расширение демо с одним файлом до пакетного процессора для реальных нагрузок.  

## Следующие шаги

Теперь, когда вы освоили основы, рассмотрите следующие темы:

- **Extract image text java** из рукописных заметок (включите `setHandwritingRecognition(true)`).  
- Интеграция вывода OCR с Apache Tika для извлечения метаданных.  
- Сохранение результатов в Elasticsearch для поисковых архивов документов.  
- Использование OCR от Aspose с другими языками, такими как Python или .NET – принципы остаются теми же.

Не стесняйтесь экспериментировать с различными ограничениями потоков, форматами изображений и языковыми пакетами. Чем больше вы будете играться, тем лучше поймёте компромиссы между скоростью и точностью.

---

### Приятного кодинга!

Если вы столкнётесь с проблемами или у вас есть идеи по дальнейшей оптимизации, оставьте комментарий ниже. Я всегда рад обсудить трюки с OCR – без усилий, только код.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}