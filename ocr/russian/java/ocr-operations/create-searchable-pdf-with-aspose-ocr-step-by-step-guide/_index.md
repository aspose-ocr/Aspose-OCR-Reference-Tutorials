---
category: general
date: 2026-01-02
description: Создайте PDF с возможностью поиска из отсканированного PDF‑изображения
  с помощью Aspose OCR. Узнайте, как установить язык OCR, встроить текстовый слой
  в PDF и применить параметры высокого уровня сжатия PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: ru
og_description: Создавайте поисковые PDF быстро. Это руководство показывает, как преобразовать
  отсканированный PDF‑изображение, добавить текстовый слой, установить язык OCR и
  включить высокую степень сжатия PDF.
og_title: Создание PDF с поисковым текстом с помощью Aspose OCR – Полное руководство
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Создание поискового PDF с помощью Aspose OCR – пошаговое руководство
url: /ru/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – Полный программный учебник

Когда‑то вам нужно **создать поисковый PDF** из отсканированных изображений, но вы не знали, с чего начать? Вы не одиноки. Во многих рабочих процессах, насыщенных документами, обычный PDF, содержащий только изображения, — это тупик для поиска и индексации.  

Хорошая новость: с помощью Aspose OCR вы можете **преобразовать PDF со сканированными изображениями** в полностью поисковый документ всего в несколько строк Java. Этот учебник проведёт вас через каждый шаг — инициализацию OCR‑движка, настройку параметров PDF с высокой компрессией, внедрение скрытого текстового слоя и даже выбор правильного языка OCR.

К концу руководства у вас будет готовая к запуску программа, генерирующая поисковый PDF, файл, который можно без проблем загрузить в любую поисковую систему или систему управления документами.

---

## Создание поискового PDF – Обзор

Прежде чем перейти к коду, уточним, что значит «создать поисковый PDF». Поисковый PDF содержит два параллельных слоя:

1. **Визуальный слой** — исходное отсканированное изображение (или отрисованная страница).  
2. **Текстовый слой** — невидимые, но машинно‑читаемые символы, извлечённые с помощью OCR.

Когда вы открываете такой PDF в Adobe Reader и выделяете текст, вы фактически работаете со скрытым текстовым слоем, а не с картинкой. Такой двойной слой и обеспечивает функциональность **embed text layer PDF**.

---

## Преобразование PDF со сканированным изображением с помощью Aspose OCR

Первое, что вам понадобится, — отсканированное изображение (PNG, JPEG, TIFF), которое вы хотите превратить в PDF. Aspose OCR может прочитать это изображение, выполнить OCR и передать результат писателю PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Почему это работает:**  
- `setCreateSearchablePdf(true)` указывает Aspose генерировать скрытый текстовый слой, удовлетворяя требование **embed text layer pdf**.  
- `setCompressionLevel(9)` переводит файл в диапазон **high compression pdf**, уменьшая конечный размер без потери точности OCR.  
- Параметр `RecognitionLanguage.ENGLISH` демонстрирует, как **set OCR language**; его можно заменить на французский, немецкий и т.д., в зависимости от исходного материала.

---

## Параметры PDF с высокой компрессией

Большие PDF‑файлы со сканами могут быстро вырасти до сотен мегабайт. Aspose предлагает простой API компрессии, работающий на уровне PDF. Метод `setCompressionLevel` принимает значения от 0 (без компрессии) до 9 (максимальная компрессия).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Несколько советов:

- **Используйте безпотерьные форматы изображений** (PNG) для сканов, насыщенных текстом; JPEG лучше подходит для фотографий.  
- **Включите подмножество шрифтов**, если внедряете пользовательские шрифты — Aspose делает это автоматически при создании поискового PDF.  
- **Проверяйте размер результата** после каждого изменения; иногда компрессия уровня 8 даёт 10 % уменьшение размера при почти незаметной потере качества по сравнению с уровнем 9.

---

## Внедрение текстового слоя PDF для возможности поиска

Если пропустить вызов `setCreateSearchablePdf(true)`, полученный файл будет выглядеть нормально, но поиск по его содержимому не будет работать. Скрытый текстовый слой создаётся путём сопоставления каждого распознанного символа с его положением на странице.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**На что обратить внимание:**  

- **Документы с несколькими языками** — возможно, придётся запускать OCR дважды, по одному разу для каждого языка, а затем объединять текстовые слои.  
- **Сложные макеты** (таблицы, несколько колонок) — Aspose справляется довольно хорошо, но стоит проверить результат в PDF‑просмотрщике, который отображает скрытый текст (например, режим «Edit PDF» в Adobe Acrobat).

---

## Установка языка OCR для точного распознавания

Точность OCR‑движка зависит от языка, который вы ему задаёте. Aspose поставляется с набором встроенных языков, а также поддерживает добавление пользовательских языковых пакетов.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Когда менять язык:**  

- Документы содержат **не‑латинские скрипты** (кириллица, арабский) — переключитесь на соответствующий `RecognitionLanguage`.  
- Страницы с несколькими языками — можно вызвать `recognizeImageAndSave` дважды, каждый раз с другим языком, а затем объединить полученные PDF‑файлы.

---

## Запуск полного примера

Ниже представлен полностью готовый к запуску код. Замените заполнители путей реальными расположениями файлов, убедитесь, что JAR‑файл Aspose OCR находится в classpath, и выполните программу.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Ожидаемый вывод:** При запуске программы в консоль будет выведено:

```
Searchable PDF created.
```

Откройте `searchable.pdf` в любом PDF‑просмотрщике, попробуйте выделить текст — вы увидите действие невидимого слоя. Вы успешно **create searchable pdf** из отсканированного изображения.

---

![пример создания поискового pdf](image-placeholder.png "пример создания поискового pdf")

*Скриншот выше (заполнитель) обычно показывает PDF‑просмотрщик с выделяемым текстом поверх отсканированной страницы.*

---

## Заключение

Мы рассмотрели всё, что нужно для **create searchable PDF** файлов с помощью Aspose OCR:

- Инициализировать OCR‑движок.  
- **Convert scanned image PDF** путём передачи PNG/JPEG в `recognizeImageAndSave`.  
- Использовать `setCreateSearchablePdf(true)` для **embed text layer PDF**.  
- Применять `setCompressionLevel(9)` для **high compression PDF**, остающегося лёгким.  
- Выбирать правильный `RecognitionLanguage` для **set OCR language** и максимальной точности.

Отсюда вы можете экспериментировать с пакетной обработкой, различными языками или даже объединять несколько отсканированных страниц в один поисковый PDF. Та же схема работает и для других языков, таких как испанский или японский — просто замените значение перечисления `RecognitionLanguage`.

Если возникнут вопросы, оставляйте комментарии. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}