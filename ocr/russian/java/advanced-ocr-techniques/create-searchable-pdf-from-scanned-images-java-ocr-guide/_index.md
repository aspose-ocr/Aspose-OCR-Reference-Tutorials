---
category: general
date: 2026-06-22
description: Создайте поисковый PDF в Java с помощью Aspose OCR. Узнайте, как конвертировать
  отсканированный PDF, работать с OCR нескольких языков и повышать точность.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: ru
og_description: Создайте поисковый PDF в Java с помощью Aspose OCR. В этом руководстве
  показано, как распознавать документ, обрабатывать текст на нескольких языках и выводить
  поисковый PDF.
og_title: Создайте поисковый PDF из отсканированных изображений – Руководство по OCR
  в Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: Создание PDF с возможностью поиска из отсканированных изображений – Руководство
  по OCR в Java
url: /ru/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из отсканированных изображений – Руководство по OCR на Java

Задумывались ли вы когда‑нибудь, как **создать поисковый PDF** из стопки отсканированных страниц, не тратя целое состояние на сторонние сервисы? Вы не одиноки. Многие разработчики сталкиваются с той же проблемой, когда им нужно **преобразовать отсканированный PDF** в нечто, что пользователи действительно смогут искать.  

В этом руководстве мы пройдем полный, готовый к запуску пример, использующий **Aspose OCR for Java** для **how to OCR document**‑level задач, решающий **mixed language OCR**, и в конце выдающий отполированный поисковый PDF. К концу вы получите автономную программу, которую можно добавить в любой проект Maven или Gradle и сразу начать обработку документов.

## Требования – Что вам понадобится

Перед тем как погрузиться в код, убедитесь, что у вас есть следующее:

- Java 17 (или любой современный JDK), установленный и настроенный в PATH.  
- IDE или редактор, с которым вам удобно работать (IntelliJ IDEA, Eclipse, VS Code…).  
- Библиотека Aspose.OCR for Java — вы можете получить последнюю JAR‑файл из [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/).  
- Многостраничный отсканированный PDF, который вы хотите сделать поисковым.  
- (Опционально) Машина с поддержкой GPU, если вы планируете использовать `setUseGpu(true)` для ускорения обработки.

Наличие этих компонентов позволяет вам скопировать‑вставить код ниже и нажать **Run**, не ищя недостающие зависимости.

## Шаг 1: Настройка проекта и импорт Aspose OCR

Сначала создайте новый Maven‑модуль (или Gradle‑проект) и добавьте зависимость Aspose OCR:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Если вы предпочитаете Gradle, эквивалентная строка выглядит так:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

После синхронизации сборки вы сможете импортировать необходимые классы.

## Шаг 2: Инициализация OCR‑движка

Создание движка простое, но стоит понять, почему мы делаем это сразу. Объект `OcrEngine` хранит конфигурацию, настройки потоков и GPU, которые влияют на все последующие операции.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Создание экземпляра движка один раз и повторное его использование для нескольких файлов снижает накладные расходы, особенно при обработке пакета PDF‑файлов.

## Шаг 3: Загрузка отсканированного PDF (или потока изображения)

Aspose OCR работает с потоками изображений, поэтому мы подаём отсканированный PDF напрямую. Библиотека внутренне растеризует каждую страницу, поэтому вы можете начать с PDF и получить поисковый PDF за один проход.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

Если у вас вместо этого есть набор файлов TIFF или JPEG, просто укажите их в `ImageStream.fromFile`; остальная часть конвейера остаётся той же.

## Шаг 4: Точная настройка OCR‑параметров для поддержки нескольких языков

Здесь **mixed language OCR** проявляет себя. Передавая несколько перечислений `OcrLanguage`, вы указываете движку искать как английский, так и русский (или любую другую комбинацию) на одной странице.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **Why this matters:** Если не указать языки, движок по умолчанию использует только английский, что резко снижает точность распознавания для документов, содержащих кириллицу или другие скрипты.

## Шаг 5: Добавление фильтров предобработки для очистки скана

Отсканированные PDF часто страдают от наклона, пятен или низкого контраста. Добавление `DeskewFilter` и `DenoiseFilter` помогает OCR‑движку лучше видеть символы.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

Вы можете добавить дополнительные фильтры — такие как `ContrastFilter` или `BinarizationFilter` — если ваш исходный материал особенно загрязнён.

## Шаг 6: Запуск OCR и генерация поискового PDF

Теперь начинается тяжёлая работа. Вызов `recognizeToPdf()` запускает OCR‑конвейер, применяет шаги предобработки и записывает распознанный текст в невидимый текстовый слой внутри PDF.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

Возвращаемый `PdfDocument` — полноценный объект Aspose PDF, что позволяет дополнительно редактировать метаданные, добавлять закладки или объединять его с другими PDF перед сохранением.

## Шаг 7: Сохранение результата и проверка

Наконец, сохраните вывод на диск. Сообщение в консоли даст вам быстрый визуальный сигнал, что всё прошло успешно.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### Ожидаемый вывод

Когда вы откроете `processed.pdf` в Adobe Reader (или любом PDF‑просмотрщике), вы сможете:

1. **Select text** – кликните и перетащите любой слово, затем скопируйте его.  
2. **Search** – нажмите `Ctrl+F` и введите фразу, которая встречается в оригинальных сканах.  
3. **Maintain original layout** – визуальное оформление остаётся идентичным оригинальному скану; добавлен лишь невидимый текстовый слой.

Если вы видите искажённые символы или отсутствующие страницы, проверьте настройки языков и убедитесь, что исходный PDF не защищён паролем.

## Часто задаваемые вопросы и особые случаи

### 1. Что если мой документ содержит более двух языков?

`config.setLanguage` принимает список var‑args, поэтому вы можете передать столько констант `OcrLanguage`, сколько нужно:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

Имейте в виду, что каждый дополнительный язык немного увеличивает время обработки.

### 2. Можно ли запустить это на безголовом сервере без GPU?

Конечно. Установите `config.setUseGpu(false)` или просто опустите этот вызов. Движок переключится на многопоточную обработку CPU, которая всё равно быстра благодаря настроенному пулу потоков.

### 3. Как обрабатывать огромные PDF (сотни страниц)?

Aspose OCR обрабатывает страницы по одной, поэтому потребление памяти остаётся умеренным. Тем не менее, вы можете разбить PDF на более мелкие части с помощью метода `split` библиотеки Aspose PDF, обработать каждую часть, а затем объединить результаты.

### 4. Можно ли сохранить метаданные оригинального PDF (автор, дата создания)?

Да. После получения `searchablePdf` вы можете скопировать метаданные из оригинального PDF:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## Советы для готового к продакшену OCR

- **Batch processing:** Оберните весь процесс в цикл, проходящий по директории файлов. Переиспользуйте один экземпляр `OcrEngine`, чтобы избежать повторных затрат на инициализацию.  
- **Error handling:** Перехватывайте `OcrException`, чтобы логировать файлы, которые не прошли, и продолжайте со следующим документом.  
- **Performance monitoring:** Используйте `System.nanoTime()` до и после `recognizeToPdf()`, чтобы логировать время обработки каждого файла; это поможет решить, масштабировать ли процесс в облачный пул воркеров.  
- **Security:** Если вы работаете с конфиденциальными документами, рассмотрите возможность шифрования выходного PDF с помощью `searchablePdf.encrypt(...)` перед сохранением.

## Заключение

Мы только что рассмотрели всё, что вам нужно, чтобы **создать поисковые PDF** файлы из отсканированных источников с помощью **Aspose OCR for Java**. Руководство показало, как **преобразовать отсканированный PDF**, настроить **mixed language OCR** и точно настроить фильтры предобработки — всё это при сохранении кода лаконичным и готовым к продакшену.  

Отсюда вы можете исследовать добавление миниатюр, генерируемых OCR, интеграцию с системой управления документами или даже передачу извлечённого текста в поисковый индекс, такой как Elasticsearch. Возможности так же широки, как и документы, которые вам нужно оцифровать.  

Есть ещё вопросы о **how to OCR document** в Java, или хотите более глубокий разбор манипуляций с PDF? Оставьте комментарий ниже, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}