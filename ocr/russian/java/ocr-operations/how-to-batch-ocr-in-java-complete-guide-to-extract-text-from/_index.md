---
category: general
date: 2026-09-18
description: Узнайте, как извлекать текст из изображений в Java с помощью Aspose OCR.
  Пакетно обрабатывайте файлы PNG, JPG и TIFF эффективно в одном вызове.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Освойте извлечение текста из изображений в Java с помощью batch OCR.
  Используйте Aspose OCR для конвертации файлов PNG, JPG и TIFF в одном вызове.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Извлечение текста из изображений в Java – руководство по batch OCR
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Как извлечь текст из изображений в Java с помощью batch OCR
url: /ru/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь текст из изображений в Java с помощью пакетного OCR

Если вам нужно **извлекать текст из изображений** быстро и без написания цикла для каждого файла, пакетный OCR — это решение. Во многих реальных проектах вы получаете папку, полную сканов — PNG‑чеков, JPG‑скриншотов или многостраничных TIFF‑файлов — и должны превратить их в поисковый текст. Aspose OCR позволяет сделать именно это одним вызовом метода, который обрабатывает файлы PNG, JPG и TIFF одновременно, экономя как время разработки, так и ресурсы процессора.

## Быстрые ответы
- **Что делает пакетный OCR?** Он обрабатывает несколько файлов изображений за один запрос, возвращая текст для каждого файла.
- **Какие форматы поддерживаются?** PNG, JPG/JPEG и многостраничные TIFF поддерживаются из коробки.
- **Нужна ли отдельная нативная библиотека?** Нет, JAR‑файл Aspose OCR содержит всё необходимое.
- **Можно ли контролировать количество запущенных потоков?** Да, используйте `setMaxParallelism` в пакетном процессоре.
- **Какая версия Java требуется?** Java 17 или новее.

## Что такое Aspose OCR?
Aspose OCR — это Java‑библиотека, распознающая печатный и рукописный текст в файлах изображений без внешних зависимостей. Она поддерживает более 60 языков и может обрабатывать до 100 изображений за один пакет, что делает её идеальной для масштабной оцифровки документов.

## Что покрывает этот учебник
Загрузите список путей к изображениям, создайте `OcrBatchProcessor`, настройте параллелизм, выполните один вызов `recognize` и выведите извлечённые строки. К концу вы получите готовую к запуску Java‑программу, извлекающую текст из файлов PNG, JPG и TIFF пакетно.

- **Как выполнять пакетный OCR** с помощью `OcrBatchProcessor` от Aspose.
- Способы **извлечения текста из изображений** разных форматов (PNG, JPG, TIFF).
- Советы по контролю параллелизма, чтобы приложение оставалось отзывчивым.
- Полный, исполняемый Java‑пример, который можно скопировать и сразу выполнить.

Предыдущий опыт работы с Aspose не требуется — достаточно базовой установки Java и любой IDE. К концу вы получите надёжную основу для распознавания текста из файлов PNG, JPG и TIFF пакетно.

---

![Диаграмма, иллюстрирующая, как пакетно выполнять OCR нескольких файлов изображений](/images/batch-ocr-diagram.png "как пакетно выполнять OCR")

*Текст alt изображения: диаграмма, показывающая пакетную обработку OCR нескольких файлов изображений.*

## Предварительные требования

| Требование | Почему это важно |
|------------|------------------|
| Java 17 или новее | Aspose OCR ориентирован на современные JVM. |
| Maven или Gradle | Упрощает добавление библиотеки Aspose OCR. |
| Базовые знания Java | Необходимы для понимания потока кода. |
| Набор примерных изображений (`.png`, `.jpg`, `.tif`) | Чтобы увидеть процесс извлечения в действии. |

Если у вас уже есть всё это, отлично — давайте приступим.

## Шаг 1: добавить Aspose OCR в ваш проект

Первое, что вам нужно, — это JAR‑файл Aspose OCR. С Maven добавьте следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Если вы предпочитаете Gradle, эквивалент выглядит так:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Добавление зависимости подтягивает всё необходимое для **извлечения текста из png**, **извлечения текста из jpg** и **извлечения текста из tiff**. Дополнительные нативные библиотеки не требуются.

## Шаг 2: определить файлы изображений, которые нужно обработать

Теперь мы укажем OCR‑движку, какие файлы обрабатывать. Здесь **как пакетно выполнять OCR** действительно проявляет себя — просто передайте список путей, и библиотека выполнит всю тяжёлую работу.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Совет:** Держите пути к файлам абсолютными или используйте `Paths.get(...)`, чтобы избежать неожиданностей на разных ОС.

## Шаг 3: создать пакетный процессор и настроить параллелизм

Aspose OCR поставляется с `OcrBatchProcessor`, который может выполнять несколько распознаваний параллельно. Управление количеством потоков предотвращает перегрузку CPU приложением, когда у вас десятки изображений.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Зачем ограничивать параллелизм? Если запустить слишком много потоков на скромном ноутбуке, вы можете увидеть замедление вместо ускорения. Установка `setMaxParallelism` позволяет сбалансировать скорость и стабильность.

## Шаг 4: выполнить пакетный вызов OCR

Вот ядро **как пакетно выполнять OCR**: один вызов `recognize`, который возвращает список объектов `RecognitionResult`, по одному на изображение.  
`recognize` обрабатывает переданные изображения и возвращает список объектов `RecognitionResult`, каждый из которых содержит извлечённый текст.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Метод блокирует выполнение, пока не будет обработано каждое изображение, затем возвращает текст. Если требуется асинхронное поведение, вы можете обернуть его в `CompletableFuture`, но для большинства скриптов синхронный вызов упрощает код.

## Шаг 5: вывести извлечённый текст

Наконец, пройдитесь по результатам и выведите распознанные строки. Это демонстрирует, что мы успешно **извлекли текст из изображений** разных форматов.  
`RecognitionResult` содержит результат OCR для одного изображения, включая извлечённый текст и оценку уверенности.

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

Если OCR‑движок не может прочитать файл, метод `getText()` возвращает пустую строку, поэтому вы можете добавить простую проверку для записи предупреждений в журнал.

## Полный рабочий пример

Объединив всё вместе, представляем полный готовый к запуску Java‑класс. Скопируйте его в файл с именем `BatchOcrTutorial.java`, скорректируйте пути к изображениям и запустите `javac && java`.

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

Запустите его, и вы увидите, как консоль выводит извлечённый текст для каждого файла PNG, JPG и TIFF — именно то, что нужно, когда **как пакетно выполнять OCR** является вашим вопросом.

## Часто задаваемые вопросы и крайние случаи

### Что если у меня более трёх изображений?
Просто добавьте больше элементов в список `imageFiles`. Пакетный процессор автоматически распределит работу по потокам, настроенным через `setMaxParallelism`.

### Мои изображения находятся в подпапке — нужно ли перечислять каждое вручную?
`Files.list` возвращает лениво заполняемый поток путей в директории.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Это делает код гибким и всё ещё соответствует **как пакетно выполнять OCR**.

### Как обрабатывать результаты с низкой уверенностью?
`getConfidence()` возвращает числовое значение уверенности, указывающее, насколько вероятно, что распознанный текст корректен.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Поддерживает ли Aspose OCR другие языки?
Да — вызовите `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (или любой поддерживаемый enum) перед вызовом `recognize`. Это расширяет возможности за пределы английского, делая **извлечение текста из изображений** действительно многоязычным.

## Советы по производительности

* **Размер пакета имеет значение** — большие пакеты снижают накладные расходы, но очень большие списки могут потреблять больше памяти. Тестируйте с 50–200 изображениями на пакет.
* **Параллелизм** — на 4‑ядерном процессоре `setMaxParallelism(4)` обычно обеспечивает лучшую пропускную способность. Регулируйте в зависимости от нагрузки вашего сервера.
* **Предобработка изображений** — преобразование изображений в градации серого или увеличение контрастности перед OCR может повысить точность, особенно для шумных сканов.

## Заключение

Теперь вы знаете, **как выполнять пакетный OCR** в Java с помощью Aspose OCR, как **извлекать текст из изображений** разных форматов и почему важно контролировать параллелизм. Полный пример кода демонстрирует распознавание текста из файлов PNG, JPG и TIFF одним эффективным вызовом.

Готовы к следующему шагу? Передайте вывод OCR в поисковый индекс, базу данных или AI‑сумматор. Вы также можете поэкспериментировать с вводом PDF (Aspose OCR поддерживает его) или объединить это с библиотеками предобработки изображений, такими как OpenCV, для ещё большей точности.

Удачной разработки, и помните — пакетный OCR не должен быть головной болью. С правильными инструментами и чётким подходом вы быстро превратите кучу картинок в поисковый текст.

## Часто задаваемые вопросы

**Q: Можно ли запускать это на безголовом сервере?**  
A: Да, Aspose OCR полностью написан на Java и не требует UI‑компонентов, поэтому он прекрасно работает в безголовых средах.

**Q: Требуется ли лицензия для продакшн‑использования?**  
A: Для продакшн‑развёртываний нужна коммерческая лицензия; доступна бесплатная пробная версия для оценки.

**Q: Какие операционные системы поддерживаются?**  
A: Любая ОС, способная запускать Java 17+, включая Windows, Linux и macOS.

**Q: Сколько языков может распознавать Aspose OCR?**  
A: Более 60 языков поддерживаются из коробки, от английского и испанского до арабского и китайского.

**Q: Каков максимальный размер файла, который может обработать Aspose OCR?**  
A: Поддерживаются отдельные файлы изображений до 200 МБ; более крупные файлы следует разбивать перед обработкой.

---

**Последнее обновление:** 2026-09-18  
**Тестировано с:** Aspose OCR 24.9 for Java  
**Автор:** Aspose

## Связанные учебники

- [Извлечение текста из изображений — основы OCR для Java](/ocr/java/ocr-basics/)
- [Как выполнить пакетный OCR в Java: полное руководство по извлечению текста из](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Предобработка изображений OCR в Java: повышение точности извлечения текста](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}