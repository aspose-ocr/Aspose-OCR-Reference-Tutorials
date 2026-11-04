---
category: general
date: 2026-03-28
description: Запустите OCR изображения в Java с помощью Aspose OCR, чтобы преобразовать
  изображение в текст и быстро и надёжно извлекать тайский текст из PNG.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: ru
og_description: Запустите OCR на изображении с помощью Java и Aspose OCR. Узнайте,
  как преобразовать изображение в текст, извлечь тайский текст из PNG и справиться
  с распространёнными проблемами.
og_title: Выполните OCR изображения на Java — быстро извлеките тайский текст
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Запуск OCR на изображении с Java – извлечение тайского текста из PNG
url: /ru/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на изображении с Java – Полнофункциональное руководство

Вы когда‑нибудь задумывались, как **run OCR on image** файлы напрямую из кода Java? Возможно, у вас есть коллекция тайских чеков, отсканированных документов или скриншотов, и вам нужен текст без ручного ввода. Это распространённая проблема, особенно когда источник — PNG, а язык — нелатинский.  

В этом руководстве мы покажем, как именно **run OCR on image** с использованием библиотеки Aspose OCR, преобразовать изображение в обычный текст и надёжно извлечь тайские символы. К концу вы сможете **convert image to text**, **extract text from PNG** и даже **recognize Thai text** всего несколькими строками кода.

## Что рассматривается в этом руководстве

* Настройка зависимости Aspose OCR в проекте Maven/Gradle.  
* Инициализация `OcrEngine` и настройка его для тайского языка.  
* Запуск OCR на файле PNG и обработка возможных ошибок.  
* Вывод результата в консоль и проверка полученных данных.  

Предыдущий опыт работы с Aspose не требуется — достаточно базовой среды разработки Java и файла изображения, который вы хотите обработать.

## Требования

* Установлен Java 8 или новее (библиотека также работает с Java 11+).  
* Инструмент сборки — Maven или Gradle (мы покажем пример для Maven).  
* Лицензия Aspose OCR (бесплатная пробная версия подходит для тестирования, но лицензия снимает ограничения оценки).  
* PNG‑файл, содержащий тайский текст, например `input.png`, размещённый в папке resources вашего проекта.

---

## Шаг 1: Добавьте Aspose OCR в ваш проект

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** Синхронизируйте версию библиотеки с официальными примечаниями к выпуску Aspose; более новые версии добавляют языковые пакеты и улучшения производительности.

После разрешения зависимости ваша IDE должна автоматически импортировать необходимые классы.

## Шаг 2: Инициализируйте OCR‑движок

Движок — сердце процесса, можно сравнить с «мозгом», который анализирует пиксельные шаблоны. Мы также укажем, что нас интересуют только тайские символы.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Зачем явно задавать язык? Потому что указание `"th"` сужает набор символов, что ускоряет распознавание и уменьшает ошибки чтения похожих глифов.

## Шаг 3: Запустите OCR на файле PNG

Теперь мы передаём движку изображение, которое нужно декодировать. Метод `recognizeImage` возвращает объект `OcrResult`, содержащий извлечённую строку и оценки уверенности.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Если файл не найден, Aspose бросает `FileNotFoundException`. Для production‑кода рекомендуется обернуть вызов в блок `try‑catch`, но в этом руководстве мы оставим всё просто.

## Шаг 4: Выведите распознанный текст

Наконец, выводим результат. Метод `getText()` возвращает обычный Java `String`, который можно сохранить, отправить по сети или записать в файл.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Если вывод выглядит искажённым, проверьте, что исходный PNG имеет высокое разрешение (не менее 300 dpi) и что код языка `"th"` соответствует целевому языку.

### Полный листинг

Ниже приведён полный, готовый к запуску Java‑файл. Скопируйте‑вставьте его в свою IDE, при необходимости замените путь к изображению и нажмите **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![пример запуска OCR на изображении](image.png "пример запуска OCR на изображении – Java‑код, извлекающий тайский текст из PNG")

## Шаг 5: Распространённые варианты и граничные случаи

### Преобразование изображения в текст в других форматах

Если вам нужно **convert image to text** для JPEG или BMP, просто измените расширение файла в `imagePath`. Aspose OCR поддерживает PNG, JPEG, BMP, TIFF и даже страницы PDF.

### Извлечение текста из PNG с несколькими языками

Вы можете попросить движок одновременно определять несколько языков:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Результат будет содержать смесь тайских и английских символов, что удобно для двуязычных чеков.

### Обработка изображений низкого качества

Для размытых сканов рассмотрите возможность включения предобработки:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Это активирует встроенные алгоритмы шумоподавления и повышения контрастности, улучшая шаг **extract text from PNG**.

### Активация лицензии

Без лицензии Aspose вставляет строку водяного знака в вывод после 100 страниц. Активируйте лицензию заранее:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

## Часто задаваемые вопросы

**Q: В: Это работает на Linux?**  
**A:** О: Абсолютно. Aspose OCR полностью на Java, поэтому любой OS, совместимый с JVM, подходит.

**Q: В: Что если PNG содержит рукописный тайский?**  
**A:** О: Распознавание рукописного текста ограничено; возможно, понадобится специализированная модель нейронной сети. Aspose OCR отлично справляется с печатным текстом.

**Q: В: Могу ли я пакетно обрабатывать папку изображений?**  
**A:** О: Оберните вызов `recognizeImage` в цикл по `Files.list(Paths.get("folder"))`. Не забудьте переиспользовать один экземпляр `OcrEngine` для повышения производительности.

## Заключение

Мы прошли полный сквозной пример того, как **run OCR on image** файлы в Java, конкретно как **extract Thai text** из PNG. Инициализировав `OcrEngine`, задав язык, вызвав `recognizeImage` и выведя результат, вы теперь имеете надёжный способ **convert image to text** без сторонних сервисов.

Отсюда вы можете:

* массово **extract text from PNG** файлы для проектов по добыче данных.  
* Скомбинируйте вывод OCR с API перевода, чтобы получить английские эквиваленты.  
* Исследуйте другие языки, поддерживаемые Aspose, такие как китайский или арабский, заменив код языка.

Попробуйте с вашими собственными изображениями — настройте параметры предобработки, поэкспериментируйте с разными форматами файлов и посмотрите, насколько надёжным кажется решение в вашем реальном рабочем процессе.

Счастливого кодинга, и пусть ваши OCR‑конвейеры всегда работают точно!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}