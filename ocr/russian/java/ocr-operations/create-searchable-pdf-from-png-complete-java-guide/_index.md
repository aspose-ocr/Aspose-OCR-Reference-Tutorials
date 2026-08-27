---
category: general
date: 2026-01-07
description: Создайте PDF с возможностью поиска из изображения на Java. Узнайте, как
  преобразовать изображение в PDF, извлечь текст из изображения и распознать текст
  из PNG с помощью Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: ru
og_description: Создайте поисковый PDF в Java с помощью Aspose OCR. Это руководство
  показывает, как преобразовать изображение в PDF, извлечь текст из изображения и
  распознать текст из PNG.
og_title: Создать PDF с поиском из PNG – учебник по Java
tags:
- OCR
- Java
- PDF
title: Создать поисковый PDF из PNG – Полное руководство по Java
url: /ru/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из PNG – Полное руководство на Java

Когда‑то вам нужно было **создать поисковый pdf** из отсканированного изображения, но вы не знали, с чего начать? Вы не одиноки — разработчики постоянно сталкиваются с этой задачей при построении конвейеров управления документами. Хорошая новость: с несколькими строками кода на Java и Aspose OCR вы можете **конвертировать изображение в pdf**, добавить скрытый текст и получить полностью поисковый документ.

В этом руководстве мы пройдем весь процесс: загрузка PNG, запуск OCR и сохранение результата в виде поискового PDF. К концу вы сможете **извлекать текст из изображения**, превращать их в **изображение в поисковый pdf** и даже обрабатывать такие случаи, как многостраничные TIFF‑файлы. Никаких внешних сервисов, только чистый Java‑код, который можно запустить уже сегодня.

## Создание поискового PDF – Обзор

Прежде чем перейти к коду, уточним, что означает «поисковый PDF». Поисковый PDF содержит два слоя:

1. **Видимый слой изображения** — оригинальная картинка (ваш PNG, JPEG и т.д.).
2. **Скрытый слой текста** — текст, сгенерированный OCR, который располагается за изображением, делая документ поисковым в любом PDF‑просмотрщике.

Зачем нужны оба слоя? Изображение сохраняет оригинальный внешний вид, а текстовый слой позволяет копировать‑вставлять, индексировать и выполнять полнотекстовый поиск. Это идеальное решение для архивирования, юридического соответствия и создания поисковых архивов.

## Шаг 1: Подключите Aspose OCR в ваш Java‑проект

Первым делом — вам нужна библиотека Aspose OCR. Самый простой способ — добавить зависимость Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Если вы не используете Maven, просто скачайте JAR‑файл с сайта Aspose и добавьте его в classpath. **Совет:** держите версию библиотеки согласованной с вашей версией Java (Java 8+ работает без проблем).

### Почему это важно
Aspose OCR поддерживает широкий набор форматов изображений и языков «из коробки», поэтому вам не придётся писать собственный код обработки пикселей. Кроме того, он предоставляет перечисление `OcrOutputFormat.PDF`, которое мы используем позже для создания поискового PDF.

## Шаг 2: Загрузите изображение, которое нужно обработать

Далее нам нужно указать OCR‑движку, какой файл читать. API принимает `ImageStream`, который можно создать из пути к файлу, `java.io.InputStream` или даже из массива байтов.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

Обратите внимание, что мы используем `ImageStream.fromFile`. Если вам когда‑нибудь понадобится **конвертировать изображение в pdf** из потока (например, загруженного файла), замените этот вызов на `ImageStream.fromInputStream(yourInputStream)`.

### Предупреждение о граничных случаях
Если ваше изображение больше 10 МБ, рассмотрите возможность его масштабирования. Большие изображения сильно увеличивают время OCR и могут вызвать ошибки «out‑of‑memory» на скромных серверах.

## Шаг 3: Запустите OCR и получите результат

Теперь происходит магия. Вызов `recognize()` запускает алгоритм OCR и возвращает объект `OcrResult`, содержащий как распознанный текст, так и информацию о раскладке.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

Здесь мы также **извлекаем текст из изображения** и выводим его. Этот шаг полезен, когда нужен только «сырой» текст без создания PDF. Позже тот же объект `ocrResult` будет использован для создания поискового PDF.

### Почему этот шаг критичен
OCR‑движок не только читает символы, но и сохраняет их позиции, что и позволяет создать скрытый текстовый слой в финальном PDF. Пропуск этого шага лишит вас поисковой возможности.

## Шаг 4: Сохраните результат как поисковый PDF

Наконец, мы просим Aspose OCR записать вывод в формате PDF. Метод `save` принимает имя целевого файла и перечисление `OcrOutputFormat`.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

Когда откроете `output.pdf` в Adobe Reader или любом современном PDF‑просмотрщике, вы увидите оригинальный PNG, но также сможете искать любые слова, присутствующие на изображении. Это и есть суть **create searchable pdf**.

### Вариации, которые могут понадобиться
- **Несколько страниц:** Если у вас многостраничный TIFF, просто пройдитесь по каждому листу, вызывая `ocrEngine.setImage` для каждого, и добавляйте результаты в один `OcrResult` перед сохранением.
- **Разные языки:** Перед вызовом `recognize()` используйте `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);` (или любой поддерживаемый язык).
- **Пользовательское DPI:** Для размытых сканов можно повысить точность, задав `ocrEngine.getImage().setResolution(300);`.

## Шаг 5: Проверьте результат (Что ожидать)

После выполнения программы проверьте файл `output.pdf`:

1. **Визуальный слой:** PDF отображает точно тот PNG, который вы передали.
2. **Текстовый слой:** Нажмите `Ctrl+F` (или Cmd+F) и найдите слово, которое точно есть на изображении. Оно должно быть найдено мгновенно.
3. **Копировать‑вставить:** Выделите абзац и скопируйте его в текстовый редактор — получите чистый, поисковый текст.

Если поиск не срабатывает, проверьте, что изображение не слишком низкого разрешения и что установлен правильный язык. Часто простое увеличение DPI решает проблему.

## Часто задаваемые вопросы и профессиональные советы

- **Нужна ли лицензия?**  
  Aspose OCR работает в пробном режиме с водяным знаком. Для продакшна приобретите лицензию и задайте её так: `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

- **Можно ли **конвертировать изображение в pdf** без OCR?**  
  Да — используйте `OcrOutputFormat.PDF` вместе с `ocrEngine.setRecognizeText(false);` перед `recognize()`. Вы получите обычный PDF только с изображением.

- **А если нужен только извлечённый текст?**  
  Пропустите вызов `save` и используйте `ocrResult.getText()`; его можно записать в файл `.txt` или передать в поисковый индекс.

- **Совет по производительности:**  
  Переиспользуйте один экземпляр `OcrEngine` для обработки нескольких изображений — это уменьшит накладные расходы на инициализацию.

## Полный рабочий пример (все вместе)

Ниже представлен полностью готовый к запуску Java‑программный код. Замените пути‑заполнители на свои директории, добавьте зависимость Maven, и всё готово.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**Ожидаемый вывод:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

Откройте `output.pdf` в любом PDF‑просмотрщике и попробуйте поискать слово из извлечённого текста — оно должно быть подсвечено, подтверждая, что вы успешно **create searchable pdf**.

## Заключение

Мы только что показали, как **create searchable pdf** из PNG с помощью Java и Aspose OCR. Шаги просты: подключить библиотеку, загрузить изображение, запустить OCR и сохранить результат в PDF. По пути вы также узнали, как **конвертировать изображение в pdf**, **извлекать текст из изображения** и даже **распознавать текст из png** для более продвинутых сценариев.

Что дальше? Попробуйте обработать пакет отсканированных счетов в цикле, сохранить скрытый текст в базе данных для полнотекстового поиска или поэкспериментировать с разными языками и предобработкой изображений. Та же схема работает и для других форматов — просто замените входной файл, и вы сможете **image to searchable pdf** в считанные минуты.

Есть вопросы или возникли трудности? Оставляйте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}