---
category: general
date: 2026-04-26
description: Как выполнять пакетное OCR с помощью Java и Aspose OCR — распознавать
  текст с изображений, извлекать текст из PNG и использовать все ядра процессора для
  параллельной обработки OCR.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: ru
og_description: Как выполнять пакетное OCR в Java. Научитесь распознавать текст на
  изображениях, извлекать текст из PNG и использовать все ядра процессора для быстрой
  параллельной обработки OCR.
og_title: Как выполнять пакетное OCR в Java – руководство по параллельной обработке
tags:
- OCR
- Java
- Aspose
- Performance
title: Как пакетно выполнять OCR в Java с параллельной обработкой
url: /ru/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетный OCR в Java – Полное руководство

Когда‑нибудь задумывались **как выполнять пакетный OCR**, когда у вас десятки скриншотов PNG, уставших от вашего взгляда? Вы не одиноки. Большинство разработчиков сталкиваются с проблемой, как только демонстрация с одним изображением работает, а реальная нагрузка — сотни файлов — начинает перегружать процессор.  

В этом руководстве мы пройдем практическое, сквозное решение, которое **распознает текст с изображений**, извлекает содержимое каждого PNG и **использует все ядра CPU** для ускорения задачи. К концу вы получите переиспользуемый класс Java, который обрабатывает папку с изображениями параллельно, предоставляя скорость многопоточного движка без головной боли по управлению пулами потоков.

> **Что вы получите:** полностью исполняемая Java‑программа (Aspose OCR), пошаговые объяснения, советы по граничным случаям и предварительный просмотр ожидаемого вывода в консоль.

---

## Необходимые условия

- **Java 17** (или любой современный JDK), установлен и настроен `JAVA_HOME`.  
- Библиотека **Aspose OCR for Java** (версия 23.10 или новее). Вы можете получить её из Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Папка, содержащая несколько **PNG‑изображений**, которые вы хотите обработать.  
- Базовое знакомство с синтаксисом Java — ничего сложного не требуется.

Если что‑то из перечисленного вам незнакомо, сделайте паузу и настройте это; остальная часть руководства предполагает, что всё готово.

## Шаг 1 — Создать однопоточный OCR‑движок (базовый вариант)

Сначала: создайте экземпляр `OcrEngine`. Этот объект выполняет основную работу — загрузку изображения, запуск нейронной сети и возврат обычного текста.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Почему это важно:** Повторное использование одного и того же движка для множества файлов избавляет от накладных расходов на многократную загрузку языковых моделей, что может сильно замедлять **пакетную обработку**.

## Шаг 2 — Включить параллельную обработку со всеми доступными ядрами

Теперь мы говорим Aspose OCR распределить работу по каждому логическому процессору, доступному на вашей машине. Вызов `Runtime.getRuntime().availableProcessors()` возвращает это число, будь то ноутбук с 4‑ядерным процессором или сервер с 32‑ядерным.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **Совет профи:** На гипертредированном процессоре вы увидите удвоенное количество ядер, но библиотека интеллектуально ограничивает пул потоков, поэтому вам не нужно вручную настраивать его.

## Шаг 3 — Собрать изображения, которые нужно обработать

Жёстко закодированный небольшой массив подходит для демонстрации, но в реальной пакетной задаче вы, скорее всего, будете сканировать каталог. Ниже показаны оба подхода.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **Зачем это может понадобиться:** Если вам нужно **извлекать текст из PNG**‑файлов, поступающих через конвейер загрузки, динамическая версия автоматически подхватывает новые файлы без изменения кода.

## Шаг 4 — Выполнять OCR для каждого изображения, используя один и тот же движок

Цикл ниже задает текущее изображение, запускает `recognize()` и выводит результат. Поскольку мы включили многопоточность ранее, каждый вызов может выполняться в отдельном рабочем потоке.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### Ожидаемый вывод в консоль

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

Если изображения содержат нелатинские скрипты или имеют низкое разрешение, вы можете увидеть искажённые символы — скорректируйте DPI или настройки подавления шума у движка соответственно (см. раздел «Продвинутые настройки» ниже).

## Продвинутые настройки — Тонкая настройка для реальных пакетных задач

| Ситуация | Предлагаемая настройка | Фрагмент кода |
|-----------|-------------------|--------------|
| PNG с низким разрешением | Увеличить `setResolution` | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| Документы со смешанными языками | Добавить языковые пакеты | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| Очень большие пакеты (10 000+ файлов) | Потоковая обработка файлов вместо загрузки всех имён сразу | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| Ограничения памяти | Освобождать движок после каждых N файлов | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **Помните:** Несмотря на то, что мы **используем все ядра CPU**, ОС всё равно управляет планированием потоков. Если вы заметите, что ваш компьютер стал медленнее, рассмотрите возможность ограничения количества потоков до `availableProcessors() - 1`.

## Распространённые подводные камни и как их избежать

1. **Исчерпание дескрипторов файлов** — Java ограничивает количество открытых файлов на процесс. Закрывайте каждое изображение явно, если сталкиваетесь с ошибкой `Too many open files`:

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **Неправильные разделители путей в Windows** — Используйте `File.separator` или `Paths.get()`, чтобы оставаться независимыми от платформы.

3. **Потокобезопасные пользовательские обратные вызовы** — Если вы добавляете слушатель прогресса, убедитесь, что он потокобезопасен (например, `AtomicInteger`).

## Полный рабочий пример (готовый к копированию и вставке)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **Что делает этот код:** Он сканирует `YOUR_DIRECTORY` в поиске всех `.png`, выполняет OCR параллельно, выводит каждый результат и в конце освобождает ресурсы. Вы можете добавить этот класс в любой Maven‑проект, выполнить `mvn exec:java` и увидеть ускорение по сравнению с однопоточным циклом.

## Заключение

Теперь у вас есть надёжный, готовый к продакшену шаблон для **выполнения пакетного OCR** в Java. Переиспользуя один `OcrEngine`, включив **параллельную обработку OCR** и используя **все ядра CPU**, вы можете **распознавать текст с изображений** за долю времени, которое потребовал бы наивный цикл.

Отсюда вы можете:

- Подключить вывод к поисковому индексу (Elasticsearch) для быстрого поиска.  
- Скомбинировать с конвертером PDF‑в‑PNG, чтобы **извлекать текст из PNG**, встроенных в отсканированные документы.  
- Добавить обработку ошибок и логику повторных попыток для ненадёжных сетевых дисков.

Продолжайте экспериментировать — заменяйте JPEG, настраивайте DPI или даже подавайте видеокадры для транскрипции в реальном времени. Основные идеи остаются теми же, а прирост производительности обычно драматичен.

Удачной разработки, и пусть ваши OCR‑конвейеры работают так же быстро, как ваша кофемашина! 🚀

![Диаграмма, показывающая параллельный рабочий процесс OCR — как выполнять пакетный OCR на нескольких ядрах CPU]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}