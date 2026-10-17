---
category: general
date: 2026-02-09
description: Как быстро использовать OCR с Aspose OCR, распознавать текст с изображения
  и извлекать текст из PNG, задавая режим и ограничение памяти GPU.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: ru
og_description: Как эффективно использовать OCR – научитесь распознавать текст на
  изображении, извлекать текст из PNG, устанавливать режим и контролировать ограничение
  памяти GPU в Java.
og_title: Как использовать OCR с ускорением на GPU в Java
tags:
- OCR
- Java
- GPU
- Aspose
title: Как использовать OCR с ускорением на GPU в Java – пошаговое руководство
url: /ru/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---



{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR с ускорением GPU в Java – Полный программный учебник

Когда‑то задумывались **как использовать OCR**, чтобы извлечь текст из изображения без написания миллионов строк кода? Вы не одиноки. Во многих проектах — сканирование счетов, обработка чеков или просто оцифровка старых документов — разработчикам нужен надёжный способ **распознавать текст из файлов изображений**, особенно PNG, которые часто содержат чистую графику высокого разрешения.  

Хорошие новости? Aspose OCR делает это проще простого, а с несколькими настройками вы можете даже перенести тяжёлую работу на ваш GPU. В этом учебнике мы пройдём весь процесс: от загрузки PNG, до **установки режима** для обработки на GPU, до **установки ограничения памяти GPU**, и, наконец, вывода извлечённого текста. К концу вы получите готовую к запуску Java‑программу, которая делает именно то, что нужно.

## Что вы узнаете

- Как установить и импортировать Aspose OCR для Java.  
- Как **распознавать текст из изображения** с помощью библиотеки.  
- Как **извлекать текст из PNG** эффективно.  
- Как **установить режим** на GPU и контролировать объём памяти с помощью **setGpuMemoryLimit**.  
- Распространённые подводные камни и советы для реального использования.

### Требования

- Java 8 или новее (код также компилируется с JDK 11).  
- NVIDIA GPU с драйвером, совместимым с CUDA, если требуется ускорение GPU.  
- Aspose OCR for Java JAR (скачайте с сайта Aspose или добавьте через Maven/Gradle).  
- Пример PNG‑изображения (например, `sample1.png`) в папке, к которой у вас есть доступ.

---

## Как использовать OCR – включить режим GPU

Первое, что нужно сделать, — сообщить Aspose OCR, что вы хотите запускать его на GPU, а не на CPU. Здесь как раз вступает в силу ключевое слово **how to set mode**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Почему это важно:**  
Обработка на GPU может быть значительно быстрее для больших пакетов или изображений высокого разрешения, но она также потребляет видеопамять. Вызвав `setGpuMemoryLimit`, вы предотвращаете захват всей памяти GPU вашим приложением, что критично, когда устройство одновременно выполняет другие задачи (например, UI или модель машинного обучения).

---

## Распознавание текста из изображения с помощью Aspose OCR

Теперь, когда движок настроен, нам нужно указать ему файл, который следует прочитать. Это ядро **recognize text from image**.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**Что происходит «под капотом»?**  
Aspose OCR загружает PNG, предварительно обрабатывает его (бинаризация, исправление наклона и т.д.), затем запускает нейронную сеть OCR на GPU. Объект результата содержит необработанный текст и оценки достоверности для каждой строки.

---

## Извлечение текста из PNG с ограничением памяти GPU

После распознавания извлечение обычной строки тривиально, однако многие разработчики забывают проверить вывод. Ниже показано, как безопасно **extract text from PNG** и отобразить его.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Ожидаемый вывод (пример):**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Если изображение содержит шум или необычные шрифты, вы можете увидеть искажённые символы. В этом случае рассмотрите возможность изменения параметров предобработки (например, `config.setLanguage(Language.ENGLISH)` или `config.setAutoSkewCorrection(true)`).

---

## Полный, готовый к запуску пример

Ниже представлен полный Java‑код, объединяющий всё вместе. Скопируйте его в файл `GpuExample.java`, поправьте путь к изображению и запустите через `javac`/`java` или из вашей IDE.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Запуск программы**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

Убедитесь, что JAR находится в classpath; иначе вы получите `ClassNotFoundException`.

---

## Профессиональные советы и распространённые подводные камни

- **Версия драйвера GPU:** Флаг `ProcessingMode.GPU` бросит исключение, если драйвер CUDA отсутствует или несовместим. Проверьте с помощью `nvidia-smi`.  
- **Бюджетирование памяти:** При одновременной обработке множества изображений увеличьте значение `setGpuMemoryLimit` или выполняйте задания последовательно, чтобы избежать ошибок «out‑of‑memory».  
- **Формат изображения:** PNG работает отлично, но JPEG с высоким уровнем сжатия может вызывать ошибки распознавания. Рассмотрите конвертацию в без‑потерь PNG перед OCR.  
- **Поддержка языков:** По умолчанию Aspose OCR предполагает английский. Для других языков вызовите `config.setLanguage(Language.SPANISH)` (или соответствующий enum) перед `recognize`.  
- **Тестирование производительности:** Проведите быстрый бенчмарк (`System.nanoTime()`) с GPU и без него, чтобы убедиться, что ускорение оправдывает добавленную сложность.

---

## Часто задаваемые вопросы

**Работает ли это на macOS или Linux?**  
Да — Aspose OCR кроссплатформенный. Просто убедитесь, что у вас есть совместимый с CUDA GPU и установлен правильный драйвер для вашей ОС.

**Что делать, если нет GPU?**  
Просто уберите строку `setProcessingMode(ProcessingMode.GPU)`; движок автоматически переключится в режим CPU.

**Можно ли обрабатывать PDF‑файлы напрямую?**  
Aspose OCR ориентирован на растровые изображения. Для PDF сначала извлеките каждую страницу как изображение (например, с помощью Aspose PDF), а затем передайте PNG в OCR‑конвейер.

---

## Заключение

В двух словах, **how to use OCR** с Aspose в Java сводится к трём чётким шагам: настроить движок (включая **how to set mode** и **set GPU memory limit**), указать ваш PNG и прочитать полученную строку. Приведённый выше фрагмент — полностью рабочее, сквозное решение, которое можно внедрить в любой Java‑проект.

Теперь, когда вы освоили **recognize text from image** и **extract text from PNG**, можете расширять процесс: пакетная обработка папок, хранение результатов в базе данных или передача текста в последующие NLP‑конвейеры. Возможности безграничны — просто следите за памятью GPU и совместимостью драйверов.

Есть дополнительные вопросы по OCR, ускорению GPU или функциям Aspose? Оставляйте комментарий или изучайте официальную документацию Aspose OCR для более глубокой кастомизации. Приятного кодинга! 🚀

![how to use ocr diagram](https://example.com/images/ocr-gpu-diagram.png "how to use ocr diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}