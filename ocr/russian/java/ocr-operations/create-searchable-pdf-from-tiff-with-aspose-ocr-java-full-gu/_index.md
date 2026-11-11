---
category: general
date: 2026-06-28
description: Создайте поисковый PDF из многостраничного TIFF в Java с использованием
  Aspose OCR. Узнайте, как преобразовать TIFF в PDF и добавить слой текста OCR в PDF
  для мгновенной возможности поиска.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: ru
og_description: Создайте PDF с возможностью поиска из изображения TIFF в Java с использованием
  Aspose OCR. Это руководство показывает, как преобразовать TIFF в PDF и добавить
  слой OCR‑текста в PDF для создания документов, доступных для поиска.
og_title: Создать PDF с возможностью поиска из TIFF с помощью Aspose OCR (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: Создание поискового PDF из TIFF с помощью Aspose OCR (Java) – Полное руководство
url: /ru/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из TIFF с помощью Aspose OCR (Java) – Полное руководство

Задумывались ли вы когда‑нибудь, как **создать поисковый PDF** из отсканированного TIFF, не тратя часы на работу с сторонними инструментами? Вы не одиноки — разработчикам постоянно нужен надёжный способ превратить громоздкие файлы изображений в PDF, которые действительно можно искать.  

В этом руководстве мы пройдём практическое решение от начала до конца, которое не только **конвертирует TIFF в PDF**, но и автоматически **добавляет слой OCR‑текста в PDF**, предоставляя действительно поисковый документ всего в несколько строк Java.

## Что вы узнаете

- Как настроить Aspose OCR для Java и применить лицензию (необязательно, но рекомендуется).  
- Точные шаги для **конвертации TIFF в PDF** с использованием `OcrEngine`.  
- Как настроить `PdfExportOptions`, чтобы сгенерированный файл содержал невидимый, поисковый слой текста — именно то, что означает **add OCR text layer PDF** в реальном мире.  
- Ожидаемый вывод и быстрая проверка, чтобы убедиться, что всё работает.

Предыдущий опыт работы с Aspose не требуется; достаточно базовой среды разработки Java (JDK 8+ и любой IDE).

---

## Шаг 1: Подготовьте проект и примените лицензию Aspose OCR  

Прежде чем вы сможете вызывать любые OCR‑API, вам нужны JAR‑файлы Aspose OCR в вашем classpath. Если у вас есть коммерческая лицензия, разместите файл `.lic` в доступном месте и укажите на него класс `License`. Этот шаг не является строго обязательным — Aspose будет работать в режиме оценки, но лицензия удаляет водяные знаки и открывает полный набор функций.

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro tip:** Храните файл лицензии вне системы контроля версий, чтобы избежать случайного раскрытия.

---

## Шаг 2: Создайте экземпляр OCR Engine  

Создание объекта `OcrEngine` — первый реальный шаг к **create searchable pdf**. Движок хранит все настройки OCR и позже будет управлять конвертацией.

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Зачем отдельный движок? Он позволяет переиспользовать одну и ту же конфигурацию для нескольких файлов, что удобно при пакетной обработке десятков TIFF‑файлов.

---

## Шаг 3: Загрузите ваш многостраничный TIFF  

Aspose OCR упрощает загрузку многостраничного TIFF. Просто добавьте путь к файлу в объект `OcrInput`; библиотека автоматически обнаруживает и ставит в очередь каждую страницу.

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

Если вам когда‑нибудь понадобится **convert TIFF to PDF** по одной странице, вы также можете вызывать `ocrInput.add(pageStream)` внутри цикла — Aspose будет рассматривать каждый вызов как отдельную страницу.

---

## Шаг 4: Настройте параметры экспорта PDF — добавление OCR‑текстового слоя  

Здесь происходит магия для **add OCR text layer pdf**. Переключив несколько флагов, вы говорите Aspose встраивать оригинальный bitmap (чтобы визуальная точность сохранялась) *и* генерировать скрытый текстовый слой, который могут индексировать поисковые системы.

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: гарантирует, что PDF выглядит точно как отсканированное изображение.  
- `setCreateSearchablePdf(true)`: создаёт невидимый текстовый наложение — это суть **add OCR text layer pdf**.  

Не стесняйтесь добавить метаданные (author, title, subject) как показано; это поможет в дальнейшем управлении документами.

---

## Шаг 5: Запустите OCR и экспортируйте поисковый PDF  

Теперь мы связываем всё вместе. Метод `recognizeAndExportPdf` выполняет основную работу: он запускает OCR на каждой странице TIFF, записывает визуальное изображение и накладывает поисковый текст.

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

Когда консоль выведет сообщение об успехе, вы только что **create searchable pdf** из TIFF‑файла. Откройте полученный `searchable.pdf` в любом PDF‑просмотрщике, нажмите `Ctrl+F` и попробуйте найти слово, которое присутствует в оригинальном изображении — оно будет найдено мгновенно.

---

## Проверка результата — быстрый чек‑лист  

1. **Visual fidelity** — PDF должен выглядеть точно как исходный TIFF (благодаря `setEmbedOriginalImage`).  
2. **Searchability** — Используйте функцию поиска в просмотрщике; скрытый текстовый слой должен возвращать совпадения.  
3. **Metadata** — Откройте свойства PDF, чтобы подтвердить автора и название, которые вы задали ранее.  

Если любой из этих пунктов не проходит, проверьте, что `setCreateSearchablePdf(true)` включён, и что ваша лицензия (если есть) не находится в режиме оценки с ограничениями.

---

## Особые случаи и часто задаваемые вопросы  

### Что если мой TIFF одностраничный?  

Тот же код работает — Aspose рассматривает одностраничный TIFF как коллекцию из одного элемента, поэтому дополнительная обработка не требуется.

### Можно ли задать язык OCR?  

Да. Перед вызовом `recognizeAndExportPdf` задайте язык движка:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

Замените `English` на любой поддерживаемый enum языка.

### Как отключить встраивание оригинального изображения для уменьшения размера файла?  

Просто установите `pdfOptions.setEmbedOriginalImage(false)`. PDF будет содержать только поисковый текстовый слой, что значительно уменьшит размер файла, но потеряется визуальное представление.

### Является ли сгенерированный PDF действительно поисковым на всех платформах?  

Современные PDF‑просмотрщики (Adobe Acrobat, Foxit, даже браузеры) учитывают текстовый слой. Некоторые старые, легковесные просмотрщики могут его игнорировать — протестируйте на целевой платформе, если не уверены.

---

## Полный рабочий пример  

Ниже приведён полностью готовый к запуску класс Java. Замените пути‑заполнители реальными, добавьте JAR‑файлы Aspose OCR в ваш проект и запустите.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Ожидаемый вывод (консоль):**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

Откройте `searchable.pdf` и попробуйте найти любое слово, которое присутствует в оригинальном TIFF — вуаля, вы успешно **create searchable pdf**!

---

## Заключение  

Мы только что прошли полный, готовый к продакшену способ **create searchable PDF** из TIFF с помощью Aspose OCR для Java. Настраивая `PdfExportOptions`, вы автоматически **add OCR text layer PDF**, превращая статические изображения в мгновенно поисковые документы.  

Если вы готовы идти дальше, попробуйте поэкспериментировать с:

- **convert TIFF to PDF** с пользовательскими размерами страниц или настройками DPI.  
- Добавление водяных знаков или цифровых подписей после OCR.  
- Пакетная обработка папки с TIFF‑файлами с помощью простого цикла `for`.  

Каждое из этих расширений опирается на те же базовые концепции, которые мы рассмотрели, поэтому переход будет плавным.  

Есть вопросы или возникли проблемы? Оставьте комментарий ниже, и удачной разработки!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Распознавание текста PDF – операции OCR с Aspose.OCR для Java](/ocr/english/java/ocr-operations/)
- [OCR распознавание PDF‑документов в Aspose.OCR для Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Как выполнить OCR PDF в .NET с Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}