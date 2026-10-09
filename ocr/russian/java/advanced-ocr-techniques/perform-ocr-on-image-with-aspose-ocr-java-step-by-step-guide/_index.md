---
category: general
date: 2026-09-23
description: Узнайте, как выполнять OCR на изображениях в Java с использованием Aspose
  OCR, извлекать текст из изображения и включать spell correction с помощью custom
  dictionary.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Как выполнять OCR на изображениях в Java с Aspose OCR. Это руководство
  показывает загрузку изображения, извлечение текста из изображения и добавление spell
  correction для получения точных результатов.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Как выполнять OCR на изображениях с помощью Aspose OCR в Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Как выполнять OCR на изображениях с помощью Aspose OCR в Java
url: /ru/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении – полный учебник по Java

Если вы ищете надежный способ **how to perform OCR** на файлов изображений с использованием Java, вы попали в нужное место. С Aspose OCR for Java вы можете извлекать текст из графических ресурсов всего в несколько строк кода, повышать точность с помощью пользовательского словаря и включать исправление орфографии для очистки шумных сканов. Этот учебник проведет вас через каждый шаг — от загрузки изображения для OCR до вывода исправленного текста — чтобы вы могли интегрировать преобразование изображений в текст в свои приложения уже сегодня.

## Краткие ответы
- **Какой основной класс для запуска OCR?** `OcrEngine` is Aspose OCR’s core class that performs optical character recognition.
- **Какой Maven‑артефакт добавляет поддержку OCR?** Add `com.aspose:aspose-ocr` to your `pom.xml`.
- **Нужна ли лицензия для разработки?** A free temporary license works for testing; a commercial license is required for production.
- **Можно ли улучшить точность на сканах низкого качества?** Yes—enable spell‑correction and supply a custom dictionary.
- **Поддерживается ли многостраничность из коробки?** Process each page image in a loop; the engine is thread‑safe for concurrent execution.

## Что такое how to perform OCR?
Фраза **how to perform OCR** относится к процессу преобразования печатного или рукописного текста на изображении в редактируемые, поисковые цифровые символы с использованием технологии оптического распознавания символов. Aspose OCR реализует этот процесс с помощью однопроходного движка, поддерживающего более 20 растровых форматов и более 50 языков.

## Почему использовать Aspose OCR для Java?
Aspose OCR поддерживает **20+ форматов изображений** (включая PNG, JPEG, TIFF, BMP и GIF) и может обрабатывать **пакеты из сотен страниц** без загрузки всего документа в память, обеспечивая до **300 страниц в минуту** на типичном 4‑ядерном сервере. Встроенные функции исправления орфографии и пользовательского словаря снижают типичные ошибки OCR с 12 % до менее 2 % на шумных счетах‑фактурах.

## Предварительные требования
- **Java Development Kit (JDK) 8+** – стандартный Java‑runtime.
- **Aspose OCR for Java** library – получите последнюю JAR‑файл из Maven Central или портала загрузок Aspose.
- Файл изображения (например, `invoice.png`), который вы хотите обработать.
- (Optional) `custom_dict.txt` – UTF‑8 текстовый файл, содержащий слова, специфичные для домена, по одному в строке.

Это всё, что вам нужно — без внешних сервисов и тяжёлых фреймворков.

## Как выполнить OCR на изображении в Java?
Загрузите изображение, включите исправление орфографии, при необходимости предоставьте пользовательский словарь, запустите движок и прочитайте результат. Этот подход работает как для одностраничных файлов, так и для пакетной обработки, а движок автоматически обрабатывает декодирование изображения, определение языка и оценку уверенности, предоставляя надёжный текстовый вывод, готовый к дальнейшей обработке. В следующих разделах каждый шаг подробно разобран с чёткими объяснениями и точным кодом, который вам нужно скопировать.

### Шаг 1: настройка проекта и импорт зависимостей

Добавьте зависимость Aspose OCR Maven в ваш `pom.xml`. Эта одна строка подтягивает основной OCR‑движок и все необходимые транзитивные библиотеки.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Совет:** Проверьте номер версии на Maven Central; более новые релизы добавляют языковые пакеты и улучшения производительности.

### Шаг 2: загрузка изображения для OCR

`OcrEngine` работает с любым `InputStream`. Используйте `ImageStream` для обёртки пути к файлу, массива байтов или URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Определение:** `ImageStream` — лёгкая обёртка Aspose OCR, которая читает данные изображения из различных источников без предварительного преобразования в `BufferedImage`.

### Шаг 3: включить исправление орфографии (необязательно, но эффективно)

Включите встроенный флаг исправления орфографии, чтобы автоматически исправлять типичные ошибки OCR, такие как «l» вместо «1».

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Исправление орфографии может повысить точность до **80 %** на сканах с низким контрастом, превращая «Inv0ice» в «Invoice» без дополнительного кода.

### Шаг 4: предоставить пользовательский словарь (адаптировать движок)

Предоставьте обычный текстовый словарь для отраслевой терминологии — медицинские коды, юридические термины, артикулы продуктов и т.д.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Определение:** `CustomDictionary` загружает список слов в UTF‑8, который OCR‑движок использует во время пост‑обработки, отдавая предпочтение вашей доменной лексике.

### Шаг 5: запуск процесса OCR

Вызовите `process()`, чтобы получить `OcrResult`, содержащий распознанный текст, оценки уверенности и необязательные данные о макете.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Если возникнет ошибка, `ocrResult.getErrorMessage()` вернёт подробное описание, которое можно записать в журнал или отобразить.

### Шаг 6: вывод распознанного (и исправленного) текста

Выведите извлечённую строку в консоль или запишите её в файл. Для быстрой проверки достаточно простого `System.out.println`.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Запуск программы должен вывести чистый, поисковый текст, похожий на:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Если вы заметите лишние символы, пересмотрите ваш пользовательский словарь и рассмотрите предобработку изображения (увеличение контраста, удаление шума или преобразование в градации серого).

## Как извлечь текст из изображения с помощью пользовательского словаря?
Загрузите словарь перед обработкой, затем вызовите `ocrEngine.setCustomDictionary(customDict)`. Движок будет отдавать приоритет словам из списка, резко снижая количество ложных срабатываний для специализированных словарей. Предоставляя термины, специфичные для домена, вы помогаете OCR‑пост‑процессору разрешать неоднозначные символы, например различать букву «O» и цифру «0», что повышает общую точность в технических документах.

## Как правильно добавить java ocr maven зависимость?
Добавьте следующий фрагмент в ваш `pom.xml` внутри секции `<dependencies>`. Эта зависимость подтягивает основную библиотеку Aspose OCR вместе со всеми необходимыми транзитивными компонентами, обеспечивая возможность создания экземпляра OCR‑движка без дополнительной настройки. Не забудьте выполнить `mvn clean install` после обновления файла, чтобы Maven разрешил последнюю версию из центрального репозитория.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Часто задаваемые вопросы и особые случаи

### Что если изображение в другом формате (PDF, TIFF и т.д.)?
Aspose OCR обрабатывает растровые форматы напрямую. Для PDF сначала извлеките каждую страницу как изображение — Aspose PDF for Java предоставляет `PdfExtractor` для эффективного выполнения этой задачи. Как только у вас будет `BufferedImage` или поток байтов, тот же вызов `setImage` сработает. Такой подход позволяет обрабатывать многостраничные документы без загрузки всего PDF в память, сохраняя быстрый и масштабируемый рабочий процесс.

### Как обрабатывать многостраничные документы?
Итерируйте каждое изображение страницы, создавайте новый `OcrEngine` (или сбрасывайте существующий) и объединяйте значения `OcrResult.getText()`. Такой подход сохраняет независимость контекстов проверки орфографии для каждой страницы. Обрабатывая страницы последовательно или в параллельных потоках, вы можете поддерживать высокий пропускной способность, обеспечивая при этом, чтобы каждая страница использовала один и тот же словарь и настройки исправления орфографии.

### Можно ли ограничить язык или набор символов?
Да. Вызовите `ocrEngine.getEngineOptions().setLanguage(Language.English)` (или любой поддерживаемый язык), чтобы сузить область распознавания, что ускоряет обработку до **30 %**. Ограничение языка уменьшает набор символов, которые движок должен учитывать, снижая неоднозначность и улучшая как скорость, так и точность, особенно для документов, содержащих только латинские символы.

### Что насчёт производительности при больших пакетах?
Движок потокобезопасен для операций только чтения. Создайте пул потоков и назначьте каждому изображению свой экземпляр `OcrEngine`. На 4‑ядерной машине можно достичь **≈250 страниц/минуту** при параллельном выполнении. Убедитесь, что выделено достаточное количество памяти heap, и контролируйте загрузку CPU, чтобы избежать узких мест при обработке тысяч изображений высокого разрешения.

## Советы для повышения точности

- **Предобработайте изображение**: увеличьте контраст, примените медианный фильтр или преобразуйте в градации серого перед OCR.
- **Используйте сканы с разрешением 300 dpi или выше**; более низкое разрешение резко повышает уровень ошибок.
- **Сохраняйте пользовательский словарь сфокусированным**: избыток нерелевантных слов может запутать проверку орфографии.
- **Пост‑обрабатывайте с помощью regex**: проверяйте даты, числа или идентификаторы после извлечения, чтобы отловить оставшиеся аномалии.

## Следующие шаги

Теперь, когда вы знаете **how to perform OCR** на изображениях и **how to extract text from image** файлах, вы можете изучить:

- Сохранение вывода OCR в виде поискового PDF с скрытым текстовым слоем.
- Сохранение извлечённых данных счетов напрямую в реляционную базу данных.
- Применение моделей машинного обучения для дальнейшей очистки рукописных заметок.
- Предоставление OCR‑рабочего процесса как RESTful веб‑сервиса для загружаемых пользователями изображений.

Каждое из этих расширений опирается на основные шаги, описанные выше, поэтому переход будет плавным.

---

**Последнее обновление:** 2026-09-23  
**Тестировано с:** Aspose OCR 24.12 for Java  
**Автор:** Aspose  



## Часто задаваемые вопросы

**Q:** Нужно ли Aspose OCR подключение к интернету?  
**A:** Нет. Библиотека работает полностью офлайн; всё распознавание происходит локально в вашей JVM.

**Q:** Какие версии Java поддерживаются?  
**A:** Aspose OCR поддерживает Java 8 до Java 21, включая как стандартные, так и дистрибутивы OpenJDK.

**Q:** Можно ли обрабатывать изображения больше 10 MB?  
**A:** Да. Движок потоково обрабатывает данные и может работать с изображениями до 500 MB, ограниченными только доступной памятью heap.

**Q:** Как лицензировать Aspose OCR для продакшн?  
**A:** Приобретите коммерческую лицензию в магазине Aspose и установите файл лицензии с помощью `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**Q:** Есть ли встроенная поддержка рукописного текста?  
**A:** Aspose OCR включает режим рукописного ввода, который можно включить через `ocrEngine.getEngineOptions().setHandwriting(true);`, улучшая точность на курсивных шрифтах.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Связанные учебники

- [Выполнить OCR на изображении с Aspose OCR Java пошаговое руководство](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Предобработка изображения OCR в Java для повышения точности извлечения текста](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Как включить GPU для OCR в Java для распознавания текста с изображения](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}