---
category: general
date: 2026-02-17
description: Как использовать OCR в Java для извлечения текста из PDF, преобразования
  PDF в изображения и выполнения OCR сканированных PDF‑файлов с помощью Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: ru
og_description: Как использовать OCR в Java для извлечения текста из PDF‑файлов. Узнайте,
  как преобразовать PDF в изображения и распознать отсканированный PDF с помощью Aspose.OCR.
og_title: Как использовать OCR в Java – Полное руководство
tags:
- OCR
- Java
- Aspose
title: Как использовать OCR в Java — извлекать текст из PDF с помощью Aspose.OCR
url: /ru/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

bottom.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Java – извлечение текста из PDF с помощью Aspose.OCR

Когда‑нибудь задавались вопросом **как использовать OCR**, чтобы превратить отсканированный PDF в поисковый текст? Вы не одиноки. Большинство разработчиков сталкиваются с проблемой, когда PDF приходит в виде набора изображений, а обычные извлекатели текста просто ничего не возвращают. Хорошая новость? С несколькими строками Java‑кода и Aspose.OCR вы можете **извлекать текст из PDF**, **конвертировать PDF в изображения** и **распознавать отсканированный PDF** в одном простом рабочем процессе.

В этом руководстве мы пройдем всё, что нужно знать — от лицензирования библиотеки до вывода окончательного результата. К концу вы получите готовую к запуску программу, которая вытаскивает обычный текст из любого отсканированного отчёта, счета или электронного книги. Никаких внешних сервисов, никакой магии — только чистый Java‑код, которым вы управляете.

## Что понадобится

- **Java Development Kit (JDK) 8+** — подойдёт любая современная версия.  
- **Aspose.OCR for Java** JAR (скачайте с сайта Aspose).  
- **Действительный файл лицензии Aspose.OCR** (`Aspose.OCR.lic`). Бесплатная пробная версия работает, но лицензия открывает полную точность.  
- **Пример отсканированного PDF** (например, `scanned-report.pdf`).  
- IDE или простой текстовый редактор плюс терминал.

Это всё. Никакого Maven, Gradle или дополнительных зависимостей — только JAR‑файл Aspose.OCR в вашем classpath.

![how to use OCR example](image-placeholder.png "how to use OCR example")

## Шаг 1 – Загрузите лицензию Aspose.OCR (Почему это важно)

Прежде чем движок сможет работать на полной скорости, необходимо указать, где находится ваша лицензия. Пропуск этого шага переводит библиотеку в режим оценки, который добавляет водяные знаки к результату и может ограничивать точность.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Почему это работает:** Класс `License` читает файл `.lic` и регистрирует его глобально. После установки каждый созданный `OcrEngine` автоматически использует лицензированные возможности.

## Шаг 2 – Создайте OCR‑движок (Движок, стоящий за магией)

Экземпляр `OcrEngine` — это рабочая лошадка, которая сканирует изображения и выдаёт текст. Можно сравнить его с мозгом, интерпретирующим пиксельные паттерны.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tip:** Вы можете настроить язык, пороги уверенности или даже включить ускорение GPU через свойства движка. Для большинства английских PDF‑ов значения по умолчанию подходят.

## Шаг 3 – Подготовьте ввод: добавьте ваш PDF (Конвертация PDF в изображения «под капотом»)

Aspose.OCR рассматривает каждую страницу PDF как изображение. При вызове `addPdf` библиотека бесшумно растеризует каждую страницу, что именно нужно для **конвертации PDF в изображения** перед распознаванием.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Что происходит:**  
- PDF открывается.  
- Каждая страница рендерится с 300 dpi (по умолчанию) для сохранения детализации символов.  
- Полученные bitmap‑объекты сохраняются в коллекцию `OcrInput`.

Если вам когда‑нибудь понадобятся исходные изображения (для отладки или пользовательской предобработки), вызовите `ocrInput.getPages()` после этого шага.

## Шаг 4 – Запустите процесс OCR (Выполнение OCR над PDF)

Теперь начинается тяжёлая работа. Метод `recognize` проходит по каждому изображению, запускает алгоритм распознавания и собирает результаты в `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Зачем это нужно:** `OcrResult` содержит не только обычный текст, но и оценки уверенности, ограничивающие рамки и ссылку на оригинальное изображение. Для большинства сценариев вам понадобится только `getText()`.

## Шаг 5 – Получите и отобразите извлечённый текст

Наконец, вытяните строку обычного текста из результата и выведите её. Вы также можете записать её в файл, передать в поисковый индекс или в последующий NLP‑конвейер.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Ожидаемый вывод

Если `scanned-report.pdf` содержит простой абзац, вы увидите что‑то вроде:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Точное форматирование повторяет оригинальную разметку, насколько это возможно, сохраняя разрывы строк.

## Обработка распространённых граничных случаев

### 1. Многоязычные PDF‑ы

Если ваш документ содержит французский или испанский текст, задайте язык перед вызовом `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Можно передать массив языков, чтобы движок автоматически определял их.

### 2. Сканирование с низким разрешением

Для сканов с 150 dpi увеличьте внутреннее DPI рендеринга:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Большее DPI улучшает чёткость символов, но требует больше памяти.

### 3. Большие PDF‑ы (Управление памятью)

Для PDF‑ов с десятками страниц обрабатывайте их пакетами:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Так JVM‑куча не будет раздуваться.

## Полный готовый к запуску пример

Ниже полностью программа — включая импорты и работу с лицензией — чтобы вы могли скопировать и сразу запустить.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Запустите её так:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Вы должны увидеть извлечённый текст, выведенный в консоль.

## Итоги – Что мы рассмотрели

- **Как использовать OCR** в Java с Aspose.OCR.  
- Рабочий процесс **извлечения текста из PDF** файлов.  
- Внутри библиотека **конвертирует PDF в изображения** перед распознаванием символов.  
- Советы по **выполнению OCR над PDF** с несколькими языками, сканами низкого разрешения и большими документами.  
- Полный, исполняемый пример кода, который можно вставить в любой Java‑проект.

## Следующие шаги и связанные темы

Теперь, когда вы умеете **распознавать отсканированный PDF**, рассмотрите следующие идеи:

- **Создание поискового PDF** — наложите OCR‑текст обратно на оригинальный PDF, получив документ, пригодный для поиска.  
- **Сервис пакетной обработки** — оберните код в микросервис Spring Boot, принимающий PDF‑ы через REST.  
- **Интеграция с Elasticsearch** — индексируйте извлечённый текст для быстрого полнотекстового поиска по репозиторию документов.  
- **Предобработка изображений** — используйте OpenCV для исправления наклона или удаления шума со страниц перед OCR, чтобы повысить точность.

Каждая из этих тем опирается на базовые концепции, которые мы изучили, так что экспериментируйте и позволяйте OCR‑движку выполнять тяжёлую работу.

---

*Счастливого кодинга! Если столкнётесь с проблемами — например, ошибками лицензии или неожиданными null‑результатами — оставляйте комментарий ниже. Я всегда готов помочь с отладкой.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}