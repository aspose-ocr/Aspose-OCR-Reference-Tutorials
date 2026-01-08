---
category: general
date: 2026-01-07
description: Создайте PDF с возможностью поиска из изображения с помощью Aspose OCR
  в Java. Узнайте, как преобразовать изображение в PDF, распознать текст на изображении
  и создать PDF из JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Aspose
  OCR в Java. Пошаговое руководство по преобразованию изображения в PDF, распознаванию
  текста на изображении и созданию PDF из JPG.
og_title: Создание PDF с возможностью поиска из изображения – Руководство по OCR в
  Java
tags:
- OCR
- Java
- PDF
- Aspose
title: Создание PDF с поиском из изображения с OCR – учебник по Java
url: /ru/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения с OCR – Java Tutorial

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного изображения, но вы не знали, с чего начать? Вы не одни — многие разработчики сталкиваются с этой проблемой, когда впервые пытаются превратить JPEG в PDF, по которому действительно можно искать.

В этом руководстве мы пройдем полный, исполняемый пример, показывающий, как **конвертировать изображение в PDF**, **распознавать текст с изображения** и, наконец, **создавать PDF из JPG** с помощью Aspose OCR for Java. Никаких расплывчатых ссылок, только код, который вы можете скопировать‑вставить и запустить сегодня.

## Что понадобится

* **Java 17** или новее (API работает с любой современной JDK).  
* **Aspose.OCR for Java** library — вы можете получить последнюю JAR‑файл из Maven Central или с сайта Aspose.  
* Пример изображения, например `sample.jpg`, размещенный в папке, к которой вы можете обратиться.  
* IDE или простой текстовый редактор плюс терминал — что вам удобнее.

Вот и всё. Никаких тяжёлых фреймворков, никаких дополнительных нативных зависимостей. Приступим.

## Шаг 1 – Создание поискового PDF: инициализация OCR‑движка

Первое, что мы делаем, — создаём экземпляр `OcrEngine` и указываем ему исходное изображение. Этот объект — сердце Aspose OCR; он обрабатывает всё, от загрузки битмапа до предоставления распознанного текста.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Почему это важно:** Правильная инициализация движка гарантирует, что библиотека сможет прочитать формат изображения, которое вы передаёте. Если путь неверный, вы получите `FileNotFoundException`, и весь конвейер остановится.

## Шаг 2 – Повышение производительности: включение GPU, многопоточного CPU и исправление орфографии

OCR может сильно нагружать CPU, особенно при работе с большими документами. Aspose предоставляет несколько параметров, которые вы можете настроить, чтобы процесс стал быстрее и точнее.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Совет:** Если вы работаете на сервере без GPU, `setUseGpu(false)` не навредит — вы просто перейдёте к обработке на многопоточном CPU.

## Шаг 3 – Улучшение качества изображения: исправление наклона и удаление шумов (необязательно, но рекомендуется)

Сканы редко бывают идеальными. Небольшой наклон или шумы могут сбить с толку распознаватель. Класс `ImageProcessingOptions` позволяет очистить изображение перед тем, как движок попытается его прочитать.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Пограничный случай:** Если исходное изображение уже чистое, вы можете пропустить этот шаг. Это не навредит, но добавит несколько миллисекунд накладных расходов.

## Шаг 4 – Распознавание текста с изображения и генерация PDF

Теперь происходит магия. Мы вызываем `recognize()`, и движок возвращает `OcrResult`. Затем мы можем сохранить результат в различных форматах — PDF является самым распространённым для поисковых документов.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Что вы увидите:** `sample-output.pdf` содержит оригинальное изображение в качестве фонового слоя, а распознанный текст размещён сверху как невидимая наложенная подсказка. Откройте его в Adobe Reader и попробуйте выделить текст — вы будете удивлены.

## Шаг 5 – Проверка созданного поискового PDF

После записи файла рекомендуется дважды проверить, что PDF действительно поисковый.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Откройте PDF, нажмите **Ctrl F**, введите слово, которое, как вы знаете, присутствует на изображении — если поиск найдёт его, вы успешно **создали поисковый PDF**!

## Как использовать OCR в реальных сценариях (Бонус)

* **Пакетная обработка:** Оберните код в цикл, который проходит по папке с JPG‑файлами. Не забудьте переиспользовать один экземпляр `OcrEngine`, чтобы снизить потребление памяти.  
* **Поддержка языков:** Aspose OCR поддерживает более 60 языков. Просто вызовите `ocrEngine.getEngineOptions().setLanguage(Language.English);` (или любое другое значение enum).  
* **Обработка ошибок:** Перехватывайте `OcrException`, чтобы корректно обрабатывать повреждённые файлы.  

Эти настройки делают решение достаточно надёжным для производственных конвейеров.

## Полный пример на Java — создание поискового PDF из JPG

Ниже представлен полный, автономный код, который можно скомпилировать и запустить как есть. Замените `YOUR_DIRECTORY` реальным путём на вашем компьютере.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Ожидаемый вывод:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Откройте сгенерированный PDF, и вы сможете искать любое слово, которое было в `sample.jpg`. Если слой текста не отображается, дважды проверьте путь к изображению и убедитесь, что OCR‑движок не генерирует скрытые исключения.

## Заключение

Мы только что показали, как **создать поисковый PDF** из JPEG с помощью Aspose OCR for Java. От загрузки изображения, настройки параметров производительности, очистки картинки до окончательного распознавания текста и сохранения поискового PDF — каждый шаг был объяснён с *почему* и *как*.

Теперь вы можете **конвертировать изображение в PDF**, **распознавать текст с изображения** и **генерировать PDF из JPG** в своих приложениях. Далее попробуйте обработать целую папку сканов, поэкспериментировать с разными языками или добавить защиту паролем к выходному PDF. Возможности безграничны.

Есть вопросы о пограничных случаях, лицензировании или настройке производительности? Оставьте комментарий ниже, и счастливого кодинга! 

![Диаграмма, иллюстрирующая конвейер OCR — создание поискового PDF](/images/ocr-pipeline.png "Диаграмма создания поискового PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}