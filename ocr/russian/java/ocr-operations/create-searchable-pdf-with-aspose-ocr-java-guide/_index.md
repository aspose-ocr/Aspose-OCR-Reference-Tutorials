---
category: general
date: 2026-03-26
description: Создайте поисковый PDF с помощью Aspose.OCR Java — узнайте, как загрузить
  изображение для OCR, установить основной язык, извлечь текст из изображения и сохранить
  PDF с OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: ru
og_description: Создайте PDF с возможностью поиска с помощью Aspose.OCR Java. Пошаговое
  руководство по загрузке изображения для OCR, установке основного языка, извлечению
  текста из изображения и сохранению PDF с OCR.
og_title: Создание PDF с поисковыми возможностями с помощью Aspose.OCR – руководство
  по Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Создание PDF с поиском с помощью Aspose.OCR – руководство по Java
url: /ru/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с Aspose.OCR – Руководство для Java

Когда‑то вам нужно **создать поисковый pdf** из отсканированного документа, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этим, когда впервые берутся за OCR в Java. Хорошая новость в том, что Aspose.OCR делает весь конвейер — от загрузки изображения до установки основного языка и, наконец, сохранения PDF с поддержкой OCR — довольно простым. В этом руководстве мы пройдем полный, готовый к запуску пример, который **извлекает текст из изображения**, позволяет **установить основной язык**, и заканчивается **сохранением OCR pdf**, которое можно открыть в любом просмотрщике.

Мы также расскажем о нескольких практических советах, таких как включение ускорения GPU для более быстрой обработки и работа с документами, содержащими несколько языков (в нашем случае тамильский + английский). К концу вы получите надёжный, готовый к продакшену фрагмент кода, который можно вставить в ваш проект.

## Что понадобится

- **Java 17** (или любой современный JDK; Aspose.OCR поддерживает Java 8+)
- **Aspose.OCR for Java** библиотека (скачайте с официального сайта или добавьте через Maven)
- Файл **лицензии** (или 30‑дневная пробная версия)
- Файл изображения, содержащий текст (в демонстрации используется `sample-mixed-tamil-eng.jpg`)

Никаких дополнительных фреймворков, никаких нативных зависимостей — только чистый Java и JAR‑файлы Aspose.

---

## Шаг 1: Создание поискового PDF — Настройка проекта

Прежде чем перейти к коду, убедимся, что проект готов к **созданию поискового pdf**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Держите номер версии актуальным; новые релизы часто включают исправления производительности для использования GPU.

Теперь создайте простой Java‑класс под названием `RecentFeaturesDemo`. В этом классе будет вся логика, необходимая для **load image OCR**, настройки языков и, наконец, **save OCR pdf**.

---

## Шаг 2: Загрузка изображения OCR и инициализация движка

Первый реальный шаг в конвейере — **load image OCR**. Он указывает Aspose.OCR, какой файл анализировать.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Почему это важно:** Включение GPU (`setUseGpu(true)`) может сократить время обработки до 70 % на современном оборудовании, а параллельная обработка гарантирует, что CPU не простаивает, пока работает GPU.

---

## Шаг 3: Установка основного языка (и вторичного)

Если пропустить этот шаг, Aspose.OCR будет пытаться угадать язык, что медленнее и менее точно. Ниже показано, как **set primary language** на тамильский и добавить английский в качестве резервного.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Основной язык влияет на набор символов и словарь, используемые во время распознавания. Добавление вторичного языка критично для документов со смешанными скриптами (например, чек с тамильским и английским текстом).  
> **Edge case:** Если ваш документ содержит более двух языков, вы можете вызвать `addAdditionalLanguage(...)` для каждого дополнительного.

---

## Шаг 4: Предобработка изображения — Выравнивание и удаление шума

Отсканированные изображения часто имеют вращение или фоновой шум. Предобработка помогает движку OCR **extract text from image** более надёжно.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Если вы знаете, что изображение уже чистое, можно пропустить `setDenoise(true)`, экономя несколько миллисекунд.

---

## Шаг 5: Загрузка файла изображения

Теперь, когда движок готов, указываем ему файл, который нужно проанализировать.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Что если путь неверный?** Aspose.OCR бросает понятный `FileNotFoundException`. Оберните вызов в `try‑catch`, если требуется более мягкая обработка ошибок.

---

## Шаг 6: Запуск OCR и извлечение текста из изображения

С полной конфигурацией пришло время запустить распознавание. Этот шаг одновременно **extracts text from image** и подготавливает данные для создания PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Типичный вывод в консоль для демонстрационного изображения выглядит так:

```
வணக்கம் World
This is a mixed language sample.
```

Вы заметите, что тамильская строка отображается корректно, за ней следует английская. Это результат правильного **set primary language**.

---

## Шаг 7: Сохранение OCR PDF — Последний шаг

Последний элемент головоломки — **save OCR pdf**. Aspose.OCR может внедрить невидимый слой текста поверх оригинального изображения, делая PDF поисковым.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Откройте `searchable.pdf` в Adobe Reader, нажмите **Ctrl + F**, и сможете искать как тамильские, так и английские слова — именно то, что обещает workflow **create searchable pdf**.

---

## Полный рабочий пример (Copy‑Paste)

Ниже представлен полный код программы, который можно сразу скомпилировать и запустить. Замените пути‑заполнители на свои каталоги.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Запустите его так:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Вы увидите извлечённый текст, выведенный в консоль, а затем подтверждение, что **searchable pdf** был записан на диск.

---

## Часто задаваемые вопросы и особые случаи

### Что если нужно **load image OCR** из массива байтов?

Можно заменить `ImageStream.fromFile(imagePath)` на `ImageStream.fromBytes(byteArray)`. Это удобно, когда изображение поступает из базы данных или веб‑сервиса.

### Как работать с PDF, которые уже содержат изображения?

Aspose.OCR может работать напрямую со страницами PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Движок растеризует каждую страницу внутри себя перед распознаванием.

### Мой GPU не обнаружен — оставлять `setUseGpu(true)`?

Если `setUseGpu(true)` не срабатывает, Aspose.OCR автоматически переходит на CPU. Перед включением можно проверить `ocrEngine.getEngineSettings().isGpuAvailable()`.

### Можно ли **save OCR pdf** с пользовательскими метаданными?

Да. После распознавания используйте `ocrEngine.getPdfSaveOptions().setTitle("My Document")` или `setAuthor("John Doe")` перед вызовом `save`.

---

## Советы по производительности для больших пакетов

- **Пакетная обработка:** Переиспользуйте один экземпляр `OcrEngine` для нескольких изображений. Между запусками вызывайте только `ocrEngine.clear()`.
- **Пул потоков:** Оберните каждую задачу обработки изображения в `Callable` и отправьте в `ExecutorService`. Поскольку включена параллельная обработка, каждый поток получит выгоду от многопоточности.
- **Управление памятью:** Для гига‑пиксельных изображений рассмотрите уменьшение масштаба с помощью `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)`, чтобы не перегружать ОЗУ.

---

## Заключение

Мы только что прошли полный workflow **create searchable pdf** с использованием Aspose.OCR для Java. Начиная с **load image OCR**, мы

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}