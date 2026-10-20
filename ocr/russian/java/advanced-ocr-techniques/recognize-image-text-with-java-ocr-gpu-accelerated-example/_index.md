---
category: general
date: 2026-03-28
description: Узнайте, как распознавать текст на изображениях в Java с помощью Aspose
  OCR, извлекать текст из PNG‑файлов и использовать ускорение на GPU для быстрого
  OCR больших изображений.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: ru
og_description: Узнайте, как распознавать текст на изображениях в Java, извлекать
  текст из PNG‑файлов и использовать ускорение на GPU для OCR больших изображений.
og_title: Распознавание текста на изображении с помощью Java OCR – пример с ускорением
  на GPU
tags:
- OCR
- Java
- GPU
title: распознавание текста на изображении с Java OCR – пример с GPU‑ускорением
url: /ru/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста на изображении с помощью Java OCR – ускоренный пример с GPU

Когда‑нибудь вам нужно было **распознавать текст на изображении** из огромного PNG, но версия для CPU работала черепашьей походкой? Вы не одиноки. Во многих реальных конвейерах — например сканирование счетов или архивирование исторических документов — размер изображения может вырастать, и стандартный OCR‑движок просто не успевает.  

Хорошие новости: Aspose OCR for Java позволяет **использовать ускорение GPU**, чтобы ускорить процесс, и код удивительно компактный. В этом руководстве вы увидите полностью готовый, исполняемый пример Java OCR, который **извлекает текст из PNG** файлов, использует GPU с поддержкой CUDA и обрабатывает **OCR крупного изображения** всего несколькими строками кода. К концу вы точно будете знать, как подключить это к своему Java‑проекту и почему важна каждая настройка.

## Что вы узнаете

- Как настроить Aspose OCR в проекте Maven или Gradle.  
- Пошаговый процесс **распознавать текст на изображении** на GPU.  
- Почему настройка количества потоков GPU может повысить пропускную способность.  
- Как проверить вывод и устранить распространённые проблемы.  

> **Требования** – Java 17 (или новее), GPU, совместимый с CUDA, с последним драйвером, и действующая лицензия Aspose OCR for Java (бесплатная пробная версия подходит для оценки). Другие внешние библиотеки не требуются.

---

## Шаг 1: Добавьте зависимость Aspose OCR

Сначала добавьте библиотеку Aspose OCR в сборку. Если вы используете **Maven**, добавьте следующий фрагмент в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Для **Gradle** поместите следующее в `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Совет:** Последняя версия (по состоянию на март 2026) включает улучшения производительности для GPU‑нагрузок, поэтому всегда используйте самую свежую версию.

---

## Шаг 2: Инициализируйте OCR‑движок и включите GPU

Создание OCR‑движка простое. Ключевой момент — включить флаг GPU, иначе движок переходит в режим CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Почему включать GPU?

Когда вы вызываете `setUseGpu(true)`, Aspose переносит тяжёлые вычисления сверточных нейронных сетей на видеокарту. Это может сэкономить секунды при обработке **ocr large image**, особенно если изображение превышает 4000 × 4000 px. Если в вашей среде нет совместимого GPU, вызов просто не делает ничего, и движок продолжает работать на CPU — без сбоев, но медленнее.

## Шаг 3: Распознайте PNG‑изображение и извлеките его текст

Теперь укажите движку файл, который нужно обработать. В примере используется `sample-large.png`, но вы можете заменить его любым PNG или JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Этот вывод подтверждает, что операция **recognize image text** завершилась успешно и вы успешно **extract text png** содержимое.

## Шаг 4: Проверьте использование GPU (необязательно, но полезно)

Если вам интересно, действительно ли используется GPU, откройте инструмент мониторинга GPU вашей системы (например, `nvidia-smi` в Linux). Пока работает Java‑процесс, вы должны увидеть небольшой всплеск использования памяти и вычислительных ресурсов.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Если вы не видите активности, проверьте следующее:

1. Драйвер CUDA соответствует модели GPU.  
2. Вызов `setUseGpu(true)` не переопределяется позже в коде.  
3. Ваш файл лицензии (если он есть) не ограничивает использование GPU.

## Шаг 5: Обработка распространённых граничных случаев

### Большие изображения, превышающие память GPU

Когда изображение огромно (например, 8000 × 8000 px), GPU может исчерпать память. Быстрый способ — уменьшить масштаб изображения перед передачей в Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Затем передайте `"sample-resized.png"` в `recognizeImage`. Это сохраняет точность OCR, оставаясь в пределах памяти GPU.

### Многостраничные PDF

Aspose OCR также может обрабатывать PDF постранично. Пройдитесь по каждой странице, преобразуйте её в изображение и передайте в движок. Тот же флаг **use gpu acceleration** применяется, обеспечивая быстрый конвейер PDF‑в‑текст.

## Полный рабочий пример (готовый к копированию и вставке)

Ниже полный Java‑класс, готовый к компиляции и запуску. Замените `YOUR_DIRECTORY` на путь к вашему PNG‑файлу.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Ожидаемый вывод** — простое текстовое представление всего, что движок смог прочитать из изображения. Если изображение содержит таблицу, вы получите содержимое ячеек, объединённое переводами строк; Aspose не сохраняет макет, но при необходимости вы можете пост‑обработать строку.

## Часто задаваемые вопросы

| Вопрос | Ответ |
|----------|--------|
| **Нужна ли платная лицензия?** | Пробная версия работает до 200 страниц и отключает водяной знак для OCR. Для продакшна лицензия снимает ограничения и открывает полный набор возможностей GPU. |
| **Что если мой GPU старый (например, GTX 750)?** | Старые GPU могут работать, но с пониженной скоростью; убедитесь, что у вас как минимум Compute Capability 3.0. |
| **Можно ли обрабатывать файлы JPG или BMP?** | Конечно — `recognizeImage` принимает любой формат, поддерживаемый Java ImageIO. |
| **Есть ли способ пакетно обрабатывать множество изображений?** | Обёрните вызов OCR в цикл и рассмотрите увеличение `setGpuStreams` до количества желаемых параллельных потоков. |
| **Что если нужно сохранить макет?** | Используйте `LayoutOptions` из Aspose OCR, чтобы получить ограничивающие рамки; это выходит за рамки данного краткого руководства, но задокументировано в API. |

## Заключение

Теперь у вас есть лаконичный, сквозной **java ocr example**, который **recognize image text**, **extract text png** и **use GPU acceleration**, ускоряя обработку **ocr large image**. Настраивая количество потоков GPU и, при необходимости, уменьшая масштаб слишком больших изображений, вы можете адаптировать решение под практически любую конфигурацию оборудования.

Готовы к следующему шагу? Попробуйте подать папку со сканированными чеками в тот же конвейер или поэкспериментировать с API `TextRegion` от Aspose, чтобы сохранить оригинальный макет. И если возникнут проблемы, форумы Aspose и Javadoc — отличные ресурсы, просто помните основы, изложенные здесь.

Удачной разработки, и пусть ваш OCR будет молниеносным!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}