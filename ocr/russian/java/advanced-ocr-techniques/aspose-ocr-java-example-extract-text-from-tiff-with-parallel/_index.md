---
category: general
date: 2026-06-25
description: Пример Aspose OCR на Java, показывающий, как извлекать текст из файлов
  TIFF, настраивать параметры OCR и включать параллельную обработку OCR для более
  быстрых результатов.
draft: false
keywords:
- aspose ocr java example
- how to extract text
- extract text from tiff
- how to configure ocr
- parallel ocr processing
language: ru
og_description: Пример Aspose OCR на Java, демонстрирующий, как извлекать текст из
  TIFF‑изображений, настраивать OCR и выполнять параллельную обработку OCR для оптимальной
  производительности.
og_title: Пример Aspose OCR на Java – Быстрое извлечение текста из TIFF
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  headline: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  type: TechArticle
- description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  name: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  steps:
  - name: '**Add Aspose OCR to your project**'
    text: '**Add Aspose OCR to your project**'
  - name: '**Compile and execute**'
    text: '**Compile and execute**'
  - name: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
    text: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
  type: HowTo
tags:
- Aspose OCR
- Java
- Text Extraction
title: Пример Aspose OCR на Java – извлечение текста из TIFF с параллельной обработкой
url: /ru/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-tiff-with-parallel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пример Aspose OCR Java – Извлечение текста из TIFF с параллельной обработкой

Когда‑нибудь задумывались **как извлечь текст** из огромных отсканированных документов, не заставляя приложение зависать? Вы не одиноки. В этом **примере Aspose OCR Java** мы пройдем настройку OCR‑движка, запустим параллельную обработку и получим чистый Unicode‑текст из многомегабайтного TIFF‑файла — всё в нескольких строках.

Представьте, что вы даёте вашему Java‑приложению турбо‑сканер, который может проглатывать страницы, пока вы пьёте кофе. К концу этого руководства у вас будет готовая к запуску программа, вы поймёте, почему важна каждая настройка, и узнаете, как подстроить её под свои задачи.

---

## Что нужно перед началом

- **Java 17** (или любой современный JDK), установленный и добавленный в ваш `PATH`.
- Лицензия **Aspose.OCR for Java** или бесплатный оценочный ключ. Вы можете получить его на портале Aspose.
- **Большое TIFF‑изображение** (`large_scan.tif`), которое вы хотите протестировать — желательно несколько мегабайт, чтобы увидеть преимущества параллельной обработки.
- Инструмент сборки, такой как **Maven** или **Gradle**, для получения библиотеки Aspose OCR.

Вот и всё. Нет тяжёлых OCR‑движков или нативных DLL‑файлов, с которыми нужно возиться. Готовы? Приступим.

## Пример Aspose OCR Java: Полный разбор кода

Ниже представлена полная, автономная Java‑программа. Скопируйте её в файл с именем `ParallelOcrDemo.java`, скорректируйте путь к изображению, и вы готовы к работе.

```java
// ParallelOcrDemo.java
// Demonstrates an Aspose OCR Java example with parallel processing.

import com.aspose.ocr.*;
import com.aspose.ocr.config.*;
import com.aspose.ocr.results.*;

public class ParallelOcrDemo {
    public static void main(String[] args) {
        // -------------------------------------------------------------
        // Step 1: Create OCR configuration and enable parallel processing
        // -------------------------------------------------------------
        OcrConfig config = new OcrConfig()
                // ParallelSettings lets us run up to 8 threads simultaneously.
                .setParallelSettings(new ParallelSettings()
                        .setMaxThreads(8)); // Adjust based on CPU cores.

        // -------------------------------------------------------------
        // Step 2: Initialise the Aspose OCR engine with the configuration
        // -------------------------------------------------------------
        AsposeOCR ocrEngine = new AsposeOCR(config);

        // -------------------------------------------------------------
        // Step 3: Recognise text from a large image (extract text from tiff)
        // -------------------------------------------------------------
        // Replace the path with your actual TIFF file location.
        ImageRecognitionResult result = ocrEngine.recognizeImage("YOUR_DIRECTORY/large_scan.tif");

        // -------------------------------------------------------------
        // Step 4: Output the recognised text (how to extract text)
        // -------------------------------------------------------------
        System.out.println("=== OCR Output Start ===");
        System.out.println(result.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

> **Ожидаемый вывод** (усечённый для краткости):  
> ```
> === OCR Output Start ===
> Lorem ipsum dolor sit amet, consectetur adipiscing elit...
> === OCR Output End ===
> ```

> **Иллюстрация изображения**  
> ![Пример обработки изображения Aspose OCR Java](https://example.com/images/aspose-ocr-java-example.png)

> *Alt text:* Пример Aspose OCR Java, показывающий параллельную обработку TIFF‑изображения.

## Как настроить OCR для параллельной обработки OCR

Строка `new ParallelSettings().setMaxThreads(8)` является ядром **параллельной обработки OCR**. Почему это важно?

- **Использование CPU:** Современные серверы часто имеют 8‑ядерные процессоры. Запуская до восьми потоков, движок может одновременно декодировать несколько фрагментов изображения, значительно сокращая общее время выполнения.
- **Учёт памяти:** Каждый поток держит копию внутренних буферов. Если у вас ограниченная память, уменьшите количество потоков (`setMaxThreads(4)`), чтобы избежать `OutOfMemoryError`.
- **Безопасность потоков:** Aspose OCR из коробки потокобезопасен, поэтому дополнительный код синхронизации не требуется.

Если вам понадобится обработать пакет файлов, просто оберните вызов `recognizeImage` в Java `ExecutorService` и переиспользуйте тот же экземпляр `AsposeOCR` — благодаря внутреннему пулу потоков, который вы настроили.

## Как извлечь текст из TIFF‑файлов

TIFF (Tagged Image File Format) популярен для сканированных документов, поскольку может хранить несколько страниц и данные без потерь. Однако не все OCR‑библиотеки корректно работают с многостраничными TIFF.

Aspose OCR автоматически определяет тип изображения и, получив многостраничный TIFF, обрабатывает каждую страницу последовательно *внутри* параллельного движка. Это означает, что вы получаете преимущества многопоточности без написания дополнительного кода цикла.

Если нужен только первый лист, передайте объект `PageOptions`:

```java
ImageRecognitionResult result = ocrEngine.recognizeImage(
        "YOUR_DIRECTORY/large_scan.tif",
        new ImageRecognitionOptions().setPageNumber(1));
```

Но для полного опыта **извлечения текста из TIFF** оставьте параметры пустыми, как показано в примере.

## Как извлечь текст – проверка результата

После завершения работы OCR‑движка `result.getText()` возвращает обычный `String`. Вы можете:

- Записать его в файл `.txt`, используя `Files.writeString(Path.of("output.txt"), result.getText());`.
- Передать его в последующий NLP‑конвейер.
- Искать его с помощью Lucene для быстрого поиска документов.

Не забудьте удалить пробелы, если планируете объединять результаты нескольких страниц:

```java
String cleaned = result.getText().trim();
```

## Распространённые подводные камни и профессиональные советы

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Сбои из‑за нехватки памяти** | Слишком много потоков на виртуальной машине с небольшим объёмом RAM. | Уменьшите `setMaxThreads` или увеличьте размер кучи (`-Xmx2g`). |
| **Пустой вывод** | Неправильный путь к изображению или файл недоступен. | Проверьте абсолютный путь и права доступа к файлу. |
| **Нечитаемые символы** | Исходный TIFF использует неподдерживаемую кодировку. | Предобработайте с помощью ImageMagick, чтобы обеспечить 8‑битный градационный режим. |
| **Низкая производительность на одноядерных машинах** | Параллелизм добавляет накладные расходы. | Установите `setMaxThreads(1)` для одноядерных окружений. |

Быстрый совет: всегда вызывайте `ocrEngine.dispose()` (или используйте try‑with‑resources, если оборачиваете его), чтобы освободить нативные ресурсы после завершения работы. Это небольшая привычка, предотвращающая утечки памяти в длительно работающих сервисах.

## Запуск примера

1. **Добавьте Aspose OCR в ваш проект**  
   Maven:  
   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-ocr</artifactId>
       <version>23.10</version>
   </dependency>
   ```  
   Gradle:  
   ```groovy
   implementation 'com.aspose:aspose-ocr:23.10'
   ```

2. **Скомпилируйте и выполните**  
   ```bash
   javac -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo.java
   java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
   ```

3. **Посмотрите консоль** — вы должны увидеть вывод OCR, размещённый между маркерами `=== OCR Output Start ===`.

Если вывод выглядит искажённым, дважды проверьте, что ваш TIFF не является сжатым вариантом, неподдерживаемым текущей версией библиотеки. Обновление до последней версии Aspose OCR часто решает такие крайние случаи.

## Следующие шаги — расширение примера Aspose OCR Java

Теперь, когда вы освоили основы, рассмотрите следующие эксперименты:

- **Пакетная обработка:** Переберите каталог с TIFF‑файлами, сохраняйте каждый результат в базе данных.
- **Языковые пакеты:** Загрузите дополнительные языковые модели (`ocrEngine.addLanguage(Language.Spanish);`), чтобы повысить точность на неанглийских документах.
- **Предобработка изображений:** Используйте `java.awt` или OpenCV для исправления наклона, удаления шумов или повышения контраста перед передачей изображения в OCR‑движок.
- **Интеграция со Spring Boot:** Откройте REST‑endpoint, принимающий загруженное изображение и мгновенно возвращающий извлечённый текст.

Каждая из этих тем естественно связывается с нашими стратегиями **настройки OCR** и **параллельной обработки OCR**, предоставляя вам надёжный, готовый к продакшн конвейер.

## Заключение

В этом **примере Aspose OCR Java** мы рассмотрели всё, что необходимо знать, чтобы **извлечь текст** из большого TIFF‑файла, настроить OCR‑движок для оптимальной производительности и использовать **параллельную обработку OCR**, чтобы приложение оставалось отзывчивым. Следуя пошаговому коду, регулируя количество потоков и учитывая распространённые подводные камни, вы сможете внедрить высокоскоростной OCR в любой Java‑сервис уже сегодня.

Попробуйте, настройте параметры и позвольте OCR‑движку выполнять тяжёлую работу, пока вы сосредотачиваетесь на создании следующей отличной функции документ‑аналитики. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображений – основы OCR с Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Как распознать TIFF с помощью Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Как использовать OCR — продвинутые техники с Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}