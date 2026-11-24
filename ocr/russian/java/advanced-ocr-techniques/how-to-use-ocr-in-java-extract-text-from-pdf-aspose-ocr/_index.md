---
category: general
date: 2026-10-24
description: Узнайте, как запустить пример Aspose OCR Java, который извлекает текст
  из PDF‑файлов, включая параллельную обработку OCR, работу с PDF, защищёнными паролем,
  и преобразование отсканированных PDF в searchable text.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Запустите пример Aspose OCR Java для быстрого извлечения текста из
  PDF. В этом руководстве рассматривается параллельная обработка OCR, PDF, защищённые
  паролем, и преобразование отсканированных PDF в searchable documents.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Пример Aspose OCR Java – быстрое извлечение текста из PDF
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Пример Aspose OCR Java: быстрое извлечение текста из PDF'
url: /ru/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пример Aspose OCR Java: быстрое извлечение текста из PDF

В этом руководстве вы узнаете **как использовать пример Aspose OCR Java**, чтобы превратить отсканированные PDF в поисковые, машинно‑читаемые тексты. Независимо от того, имеете ли вы один многостраничный файл или пакет защищённых паролем PDF, нижеописанные шаги покажут, как настроить OCR‑движок, включить параллельную обработку и получить объединённый результат всего в несколько строк кода Java.

Вы также узнаете, когда следует регулировать количество потоков для оптимальной производительности, как обрабатывать зашифрованные PDF и почему этот подход идеален для преобразования отсканированных PDF‑документов в поисковые архивы.

![как использовать OCR с Aspose OCR Java](/images/ocr-parallel.png "Иллюстрация параллельной обработки OCR в Java – как использовать OCR")
[как использовать OCR с Aspose OCR Java](/images/ocr-parallel.png "Иллюстрация параллельной обработки OCR в Java – как использовать OCR")

## Быстрые ответы
- **Что делает пример Aspose OCR Java?** Он загружает PDF, выполняет OCR на каждой странице параллельно и возвращает полный поисковый текст в виде одной строки.  
- **Можно ли обрабатывать PDF, защищённые паролем?** Да — вы можете передать пароль документа при добавлении файла в `OcrInput`.  
- **Стоит ли использовать параллельную обработку OCR?** На машине с 4‑ядерным процессором это сокращает время обработки на 30‑70 % для PDF более пяти страниц.  
- **Какие языки поддерживаются?** Более 70 языков, включая английский, французский, немецкий, китайский и арабский.  
- **Нужна ли лицензия для продакшн?** Для использования не в пробном режиме требуется коммерческая лицензия Aspose OCR; бесплатная пробная версия подходит для оценки.

## Что такое пример Aspose OCR Java?
**Aspose OCR Java example** — это лаконичная, исполняемая программа, демонстрирующая, как создать экземпляр `OcrEngine`, настроить параллельное выполнение и извлечь текст из PDF‑файлов с помощью библиотеки Aspose OCR for Java. Пример также показывает, как обрабатывать типичные сценарии, такие как документы, защищённые паролем, настройка ограничения памяти и выбор языка, предоставляя надёжную основу для построения более крупных конвейеров обработки документов.

## Зачем использовать параллельную обработку OCR?
Aspose OCR может разбить многостраничный PDF на отдельные страницы и обрабатывать каждую страницу в собственном потоке. На 8‑ядерном сервере документ из 120 страниц обычно обрабатывается менее чем за 30 секунд, по сравнению с более чем минутой при последовательной обработке. Этот прирост скорости особенно ценен, когда необходимо **массово преобразовать отсканированные PDF в поисковые** архивы.

## Предварительные требования
- Java 8 или новее установлен.  
- Инструмент сборки Maven или Gradle (пример использует Maven).  
- Лицензия Aspose OCR for Java (бесплатная пробная версия подходит для тестирования).  

## Как запустить пример Aspose OCR Java шаг за шагом

### Шаг 1: настройте ваш проект

Добавьте зависимость Aspose OCR в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Если вы предпочитаете Gradle, замените фрагмент на эквивалентную строку `implementation`.  
После разрешения зависимости вы можете импортировать необходимые классы в ваш Java‑файл.

### Шаг 2: создайте и настройте OCR‑движок

`OcrEngine` — основной класс, выполняющий оптическое распознавание символов.

Класс `OcrEngine` является главным объектом Aspose OCR, инкапсулирующим все настройки OCR и логику выполнения.  
Включите параллельную обработку и при необходимости ограничьте пул потоков:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Почему это важно:**  
- `setParallelProcessing(true)` распределяет страницы по нескольким ядрам процессора, существенно сокращая время выполнения на многопроцессорном оборудовании.  
- `setMaxThreadCount` защищает ресурсы сервера, не позволяя движку монополизировать все ядра, что критично в средах совместного хостинга или CI.

### Шаг 3: загрузите PDF, который хотите обработать

`OcrInput` представляет коллекцию файлов (PDF, изображения или смешанные медиа), которые движок будет анализировать.

Класс `OcrInput` агрегирует один или несколько источников ввода, позволяя передавать PDF, TIFF или JPEG в OCR‑движок в одной партии.  
Добавьте ваш PDF (или набор PDF) в коллекцию ввода:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Подсказка:** Используйте абсолютный путь или путь, относительный к рабочему каталогу, чтобы избежать `FileNotFoundException`. Метод `add` можно вызывать многократно, чтобы поставить в очередь несколько документов для пакетной обработки.

### Шаг 4: выполните OCR на всех страницах параллельно

`OcrResult` хранит объединённый текстовый вывод и информацию о надёжности для каждой страницы после завершения распознавания.

Объект `OcrResult` содержит конкатенированный простой текст и список объектов `PageResult`, раскрывающих уровни уверенности для каждой обработанной страницы.  
Выполните распознавание:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Под капотом:** Каждая страница передаётся отдельному рабочему потоку (до `maxThreadCount`, который вы задали). Библиотека синхронизирует результаты, поэтому окончательный `OcrResult` сохраняет исходный порядок страниц.

### Шаг 5: получите и отобразите объединённый текст

`OcrResult.getText()` возвращает полную поисковую строку.

Метод `getText()` объекта `OcrResult` возвращает одну `String`, содержащую OCR‑извлечённый текст со всех страниц, при этом сохраняются переносы строк, как они были в исходном PDF.  

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Ожидаемый вывод:** Консоль печатает одну непрерывную строку, содержащую читаемый текст со всех страниц, готовый для индексации, хранения или дальнейшей обработки.

### Шаг 6: обработка особых сценариев

#### Как движок обрабатывает PDF, защищённые паролем?

Передайте пароль при добавлении файла в `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Перегруженный метод `add`, принимающий пароль, расшифровывает документ «на лету», позволяя выполнять OCR без ручного дешифрования.

#### Как ограничить использование памяти для очень больших файлов?

Вызовите `ocrEngine.setMemoryLimit(256);`, чтобы ограничить потребление ОЗУ 256 МБ. Движок автоматически выгружает избыточные данные во временные файлы, предотвращая сбои из‑за нехватки памяти даже при обработке PDF‑документов в несколько сотен страниц.

## Часто задаваемые вопросы и особые случаи

### Действительно ли нужна параллельная обработка?

Если ваш PDF содержит **более нескольких страниц** и у вас минимум четыре ядра процессора, включение параллельной обработки обычно сокращает общее время выполнения на **30‑70 %**. Для одностраничного скана накладные расходы на потоки могут превысить выгоду, поэтому её можно отключить с помощью `ocrEngine.setParallelProcessing(false)`.

### Что происходит, если страница не прошла OCR?

Aspose OCR бросает `OcrException` только при фатальных ошибках, таких как повреждённый файл. Страницы, которые не удалось распознать, просто возвращают пустую строку, которую движок молча конкатенирует. Вы можете исследовать `ocrResult.getPageResults()`, чтобы получить уровни уверенности по каждой странице и вручную обрабатывать страницы с низкой надёжностью.

### Как изменить язык распознавания?

По умолчанию движок использует английский, но вы можете переключить язык так:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Замените `Language.FRENCH` на любой поддерживаемый язык из перечисления. Это необходимо, когда нужно **извлечь текст PDF Java** из многоязычных документов.

## Профессиональные советы для OCR в продакшн

- **Пакетная обработка:** Оберните процесс в цикл, читающий имена файлов из каталога, превратив демонстрацию в масштабируемый сервис.  
- **Логирование:** Установите `ocrEngine.setLogLevel(LogLevel.ERROR)` в продакшн, чтобы подавить подробный вывод.  
- **Очистка результата:** Пост‑обработайте `ocrResult.getText()` регулярными выражениями, удаляя лишние пробелы или артефакты.  
- **Тонкая настройка пула потоков:** Используйте `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` на серверах с большим числом ядер для максимальной пропускной способности.  
- **Бенчмарк производительности:** На 8‑ядерном Intel Xeon документ из 200 страниц (300 МБ) обрабатывается примерно за 22 секунды при включённой параллельной обработке OCR.

## Заключение

Теперь у вас есть полный **пример Aspose OCR Java**, который извлекает поисковый текст из любого отсканированного PDF, поддерживает файлы, защищённые паролем, и использует параллельную обработку для ускорения. Интегрируя этот код в свои приложения, вы сможете создавать мощные конвейеры оцифровки документов, передавать результаты OCR в поисковые индексы или комбинировать их с сервисами перевода для многоязычных архивов.

Готовы к следующему шагу? Попробуйте передать извлечённый текст в Elasticsearch для полнотекстового поиска или связать вывод с API машинного перевода, чтобы создать многоязычный поисковый репозиторий. Приятного кодинга!

---

**Последнее обновление:** 2026-10-24  
**Тестировано с:** Aspose OCR for Java 24.11  
**Автор:** Aspose  

## Часто задаваемые вопросы

**Q: Можно ли использовать этот пример с бесплатной пробной лицензией?**  
A: Да, бесплатная пробная версия Aspose OCR подходит для разработки и тестирования; для продакшн‑развёртываний требуется коммерческая лицензия.

**Q: Поддерживает ли пример OCR для PDF, защищённых паролем?**  
A: Абсолютно — передайте пароль в `OcrInput.add(filePath, password)`, и движок автоматически расшифрует документ.

**Q: Сколько языков распознаёт Aspose OCR?**  
A: Более 70 языков, включая скрипты справа налево, такие как арабский и иврит.

**Q: Каков максимальный размер PDF, который я могу обработать?**  
A: Движок способен обрабатывать PDF‑документы со сотнями страниц; вы можете задать ограничение памяти, чтобы предсказать использование ОЗУ.

**Q: Безопасна ли параллельная обработка OCR на совместных серверах?**  
A: Да, настройкой `setMaxThreadCount` вы контролируете максимальное количество одновременно работающих потоков, предотвращая истощение ресурсов.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Связанные руководства

- [Как использовать OCR в Java с параллельной обработкой с Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Создание поискового PDF с Aspose OCR Java руководство](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Как использовать OCR в Java для извлечения текста из PDF Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}