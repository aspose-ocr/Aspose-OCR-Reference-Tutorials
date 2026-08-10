---
category: general
date: 2026-02-22
description: Как использовать OCR в Java для быстрого извлечения текста из PDF с помощью
  Aspose OCR — пошаговое руководство, охватывающее параллельную обработку и полный
  пример кода.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- aspose ocr java example
- parallel OCR processing
- Java PDF extraction
language: ru
og_description: Как использовать OCR в Java для быстрого извлечения текста из PDF
  с помощью Aspose OCR — полное руководство с параллельной обработкой и готовым кодом.
og_title: Как использовать OCR в Java – извлечение текста из PDF (Aspose OCR)
tags:
- OCR
- Java
- Aspose
- PDF
title: Как использовать OCR в Java — извлечение текста из PDF (Aspose OCR)
url: /ru/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Java – извлечение текста из PDF (Aspose OCR)

Задумывались ли вы когда‑нибудь **как использовать OCR** в Java, когда у вас есть стопка отсканированных PDF, которые нужно сделать доступными для поиска? Вы не одиноки. Во многих проектах узким местом является извлечение чистого, поискового текста из многостраничного документа без излишней нагрузки на процессор. В этом руководстве мы покажем, **как использовать OCR** с Aspose OCR для Java, включив параллельную обработку, чтобы вы могли мгновенно извлекать текст из PDF‑файлов.

![как использовать OCR с Aspose OCR Java](/images/ocr-parallel.png "Иллюстрация параллельной обработки OCR в Java – как использовать OCR")

## Что вы получите

- Инициализировать `OcrEngine` из библиотеки Aspose OCR.  
- Включить **параллельную обработку** и при необходимости ограничить пул потоков.  
- Загрузить многостраничный PDF через `OcrInput`.  
- Запустить OCR на всех страницах одновременно и собрать объединённый текст.  
- Вывести результат на консоль или передать его в любую downstream‑систему по вашему выбору.

Вы также узнаете, когда следует регулировать количество потоков, как обрабатывать PDF, защищённые паролем, и почему может потребоваться отключить параллелизм для небольших файлов.

---

## Как использовать OCR с Aspose OCR Java

### Шаг 1: Настройка проекта

Прежде чем писать код, убедитесь, что библиотека Aspose OCR для Java находится в вашем classpath. Самый простой способ — использовать Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Если вы предпочитаете Gradle, просто замените фрагмент соответствующим образом. После разрешения зависимости вы готовы импортировать необходимые классы.

### Шаг 2: Создание и настройка OCR‑движка

`OcrEngine` — ядро библиотеки. Включение параллельной обработки заставляет Aspose создать пул рабочих потоков, каждый из которых обрабатывает отдельную страницу.

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Почему это важно:**  
- `setParallelProcessing(true)` разбивает нагрузку, что может значительно сократить время обработки на многоядерных процессорах.  
- `setMaxThreadCount` предотвращает захват всех ядер движком, что является полезной защитой на общих серверах или в CI‑конвейерах.

### Шаг 3: Загрузка PDF для обработки

Aspose OCR работает с любым форматом изображений, но также принимает PDF напрямую через `OcrInput`. Вы можете добавить несколько файлов или даже смешать изображения и PDF в одной партии.

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Подсказка:** Держите путь к PDF абсолютным или относительным к рабочей директории, чтобы избежать `FileNotFoundException`. Кроме того, метод `add` можно вызывать многократно, если нужно обработать несколько PDF за один запуск.

### Шаг 4: Запуск OCR на всех страницах параллельно

Теперь движок выполняет тяжёлую работу. Вызов `recognize` возвращает `OcrResult`, который агрегирует текст со всех страниц.

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Под капотом:** Каждая страница передаётся отдельному потоку (до `maxThreadCount`, который вы задали). Библиотека управляет синхронизацией, поэтому окончательный `OcrResult` уже упорядочен корректно.

### Шаг 5: Получение и вывод объединённого текста

Наконец, получите вывод в виде обычного текста. Вы можете записать его в файл, отправить в поисковый индекс или просто вывести на консоль для быстрой проверки.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Ожидаемый вывод:** Консоль покажет одну строку, содержащую читаемый текст со всех страниц, с сохранёнными переводами строк, как они были в оригинальном PDF.

---

## Полный пример Aspose OCR Java – готов к запуску

Объединив все части, представляем полностью самостоятельную программу, которую вы можете скопировать в файл `ParallelOcrDemo.java` и запустить.

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

Run it with:

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

Если всё настроено правильно, вы увидите извлечённый текст, выведенный в консоль вскоре после запуска программы.

---

## Часто задаваемые вопросы и особые случаи

### Нужно ли действительно включать параллельную обработку?

Если ваш PDF содержит **более нескольких страниц** и вы работаете на машине с минимум 4 ядрами, включение параллельной обработки может сократить общее время выполнения на **30‑70 %**. Для одностраничного скана накладные расходы на управление потоками могут превысить выгоду, поэтому вы можете просто вызвать `ocrEngine.setParallelProcessing(false)`.

### Что делать, если страница не прошла OCR?

Aspose OCR бросает `OcrException` только при фатальных ошибках (например, повреждённый файл). Нераспознаваемые страницы просто возвращают пустую строку для этой страницы, которую движок бесшумно конкатенирует. Вы можете проверить `ocrResult.getPageResults()`, чтобы увидеть оценки уверенности для каждой страницы и вручную обработать страницы с низкой уверенностью.

### Как управлять языком вывода?

По умолчанию движок использует английский, но вы можете переключить язык с помощью:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Замените `FRENCH` на любой поддерживаемый enum языка. Это удобно, когда нужно **извлекать текст из PDF** документов на разных языках.

### Можно ли ограничить использование памяти?

Да. Используйте `ocrEngine.setMemoryLimit(256);`, чтобы ограничить потребление памяти 256 МБ. Библиотека тогда будет выгружать избыточные данные во временные файлы, предотвращая падения из‑за нехватки памяти при работе с огромными PDF.

---

## Профессиональные советы для OCR в продакшене

- **Пакетная обработка:** Оберните весь процесс в цикл, который читает имена файлов из каталога. Это превратит демо в масштабируемый сервис.  
- **Логирование:** Aspose OCR предоставляет метод `setLogLevel` — установите его в `LogLevel.ERROR` в продакшене, чтобы избежать шумного вывода.  
- **Очистка результата:** После обработки `ocrResult.getText()` удаляйте лишние пробелы или артефакты переводов строк. Для этого хорошо подходят регулярные выражения.  
- **Тонкая настройка пула потоков:** На сервере с большим количеством ядер экспериментируйте с `setMaxThreadCount(Runtime.getRuntime().availableProcessors())` для оптимальной пропускной способности.  

---

## Заключение

Мы рассмотрели **как использовать OCR** в Java с Aspose OCR, продемонстрировали полный рабочий процесс **извлечения текста из PDF**, и предоставили полный **пример Aspose OCR Java**, который работает параллельно для повышения скорости. Следуя приведённым шагам, вы сможете превратить любой отсканированный PDF в поисковый текст всего несколькими строками кода.

Готовы к следующему вызову? Попробуйте передать вывод OCR в Elasticsearch для полнотекстового поиска или объединить его с API перевода, чтобы построить многоязычный конвейер обработки документов. Возможности безграничны, как только вы освоите основы.

Если столкнётесь с проблемами, оставьте комментарий ниже — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}