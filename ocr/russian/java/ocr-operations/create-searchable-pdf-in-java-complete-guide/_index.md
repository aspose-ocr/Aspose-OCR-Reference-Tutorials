---
category: general
date: 2026-07-05
description: Создайте поисковый PDF в Java с использованием Aspose OCR. Узнайте, как
  сжимать изображения в PDF, преобразовать отсканированное изображение в PDF и отключить
  встраивание шрифтов в PDF для уменьшения размера файлов.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: ru
og_description: Создайте PDF с возможностью поиска в Java с помощью Aspose OCR. Этот
  учебник показывает, как сжимать изображения в PDF, конвертировать отсканированное
  изображение в PDF и отключать встраивание шрифтов в PDF.
og_title: Создание PDF с возможностью поиска в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Создание PDF с возможностью поиска в Java – Полное руководство
url: /ru/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в Java – Полное руководство

Когда‑нибудь вам нужно было **create searchable PDF** из отсканированного документа, но вы застряли на этапе «как‑это‑сделать»? Вы не одиноки. Во многих проектах преобразование TIFF или JPEG в PDF, по которому действительно можно искать, является *must‑have* функцией, особенно когда вы также хотите **compress images in PDF**, чтобы поддерживать размер файлов в приемлемых пределах.  

В этом руководстве мы пройдем практический пример с использованием Aspose OCR for Java. К концу вы точно будете знать, как **convert scanned image to PDF**, настроить параметр **compress images in PDF** и даже **disable font embedding PDF**, чтобы сэкономить несколько килобайт. Без лишних слов — только полное, готовое к запуску решение, которое вы можете сразу добавить в свой код.

## Что вы узнаете

- Настроить движок Aspose OCR в проекте Java.  
- Выполнить OCR на TIFF (или любом растровом изображении).  
- Настроить `PdfSaveOptions` для **compress images in PDF** и **disable font embedding PDF**.  
- Сохранить результат как **searchable PDF**, который можно сразу индексировать или искать.  

**Требования**  
- Установлен Java 8 или новее.  
- Maven или Gradle для управления зависимостями (мы покажем фрагмент Maven).  
- Отсканированный файл изображения (TIFF, PNG или JPEG), готовый к обработке.  

Если у вас есть всё это, давайте начнём.

![Рабочий процесс создания searchable PDF – Java OCR to PDF conversion](/images/create-searchable-pdf-workflow.png "Diagram showing the steps to create searchable PDF with Aspose OCR")

## Шаг 1: Добавьте зависимость Aspose OCR

Сначала подключите библиотеку Aspose OCR к вашему проекту. С Maven добавьте следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Если вы предпочитаете Gradle, эквивалент выглядит так:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Следите за примечаниями к выпускам Aspose; новые версии часто повышают производительность и точность OCR.

## Шаг 2: Инициализируйте OCR‑движок

Создание OCR‑движка так же просто, как создание экземпляра `OcrEngine`. Этот объект будет обрабатывать всё: от загрузки изображения до извлечения текста.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Зачем нужен отдельный движок? Aspose отделяет тяжёлую работу (предобработка изображений, языковые модели) от остального приложения, поэтому вы можете переиспользовать один и тот же `engine` для нескольких файлов без повторной инициализации тяжёлых ресурсов.

## Шаг 3: Выполните OCR на отсканированном изображении

Теперь мы передаём движку отсканированный файл. Метод `recognizeImage` возвращает `RecognitionResult`, содержащий извлечённый текст и информацию о раскладке.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **What if the image isn’t a TIFF?**  
> Aspose OCR автоматически определяет распространённые растровые форматы, поэтому вы можете указать JPEG, PNG или BMP без изменения кода.

## Шаг 4: Настройте параметры сохранения PDF (Сжатие изображений и отключение встраивания шрифтов)

Здесь проявляются вторичные ключевые слова. Мы укажем Aspose **compress images in PDF** и **disable font embedding PDF**. Оба параметра уменьшают конечный размер файла — удобно, когда вы отправляете десятки документов.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Why compress images?**  
Сканированные страницы часто имеют высокое разрешение; сжатие до 80 % качества может уменьшить 10‑страничный PDF с 12 МБ до менее 3 МБ без заметных потерь в визуальном качестве.

**Why disable font embedding?**  
Если OCR‑движок использует стандартные системные шрифты (например, Arial или Times New Roman), их встраивание избыточно. Отключение этой опции ещё больше уменьшает размер файла, особенно при больших партиях.

## Шаг 5: Сохраните результат OCR как поисковый PDF

Последний шаг объединяет всё: исходное изображение, извлечённый слой текста и параметры PDF, которые мы только что задали.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Когда вы откроете `document.pdf` в Adobe Reader или любом современном просмотрщике, вы увидите оригинальное отсканированное изображение **плюс** невидимый слой текста. Ввод слова в поле поиска подсветит совпадения — именно то, что обещает «create searchable pdf».

### Ожидаемый вывод

Запуск программы с корректным TIFF даёт примерно следующее:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Откройте PDF, нажмите `Ctrl+F`, введите слово, которое присутствует на отсканированной странице, и наблюдайте, как он переходит к нужному месту. Это признак успешного рабочего процесса **create searchable pdf**.

## Распространённые ошибки и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Blank PDF** | `PdfSaveOptions` не передан в `saveAsSearchablePdf`. | Убедитесь, что вызываете перегрузку, принимающую `PdfSaveOptions`. |
| **Garbage characters** | Язык OCR не установлен (по умолчанию English). | Используйте `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` перед `recognizeImage`. |
| **Huge file size** | `setCompressImages(false)` или `setEmbedFonts(true)`. | Оставьте оба флага, как показано выше. |
| **Image distortion** | `setImageQuality` установлен слишком низко (<50). | Оставьте значение 70‑90 для хорошего компромисса. |

## Расширение примера

Теперь, когда вы можете **convert scanned image to PDF** и контролировать размер, вы можете захотеть:

- **Batch process** папку сканов с простым циклом `for(File f : folder.listFiles())`.  
- Добавить **watermarks** с помощью Aspose PDF (`PdfDocument.addWatermarkText`).  
- Экспортировать текст OCR в **plain .txt** файл для систем индексации (`result.getText().writeToFile("doc.txt")`).  

## Полный, готовый к запуску код

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Скопируйте‑вставьте это в вашу IDE, замените `YOUR_DIRECTORY` реальным путём и запустите. Если всё настроено правильно, вы получите **searchable PDF**, который также лёгок благодаря сжатию изображений и отключенному встраиванию шрифтов.

## Заключение

Мы только что рассмотрели всё, что вам нужно для **create searchable pdf** файлов в Java с использованием Aspose OCR. От инициализации движка, выполнения OCR, настройки **compress images in pdf**, и **disable font embedding pdf**, до окончательного сохранения поискового документа — каждый шаг был объяснён с указанием *почему*.

Готовы к следующему вызову? Попробуйте добавить пакеты языков OCR, пакетную обработку целых папок или наложение аннотаций на PDF. Основы, которые вы только что освоили, сделают эти расширения простыми.

Есть вопросы или хотите поделиться своими приёмами? Оставьте комментарий ниже, и удачной разработки!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Распознавание текста PDF – операции OCR с Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR распознавание PDF‑документов в Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Как выполнить OCR PDF в .NET с Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}