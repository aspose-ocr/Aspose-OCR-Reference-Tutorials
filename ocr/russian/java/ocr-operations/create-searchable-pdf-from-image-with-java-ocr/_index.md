---
category: general
date: 2026-05-06
description: Создайте PDF с возможностью поиска из изображения, используя Aspose OCR
  в Java. Узнайте, как преобразовать изображение в PDF, включить исправление орфографии
  и использовать OCR GPU для быстрых результатов.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Aspose
  OCR в Java. Это руководство показывает, как преобразовать изображение в PDF, включить
  исправление орфографии и использовать OCR GPU.
og_title: Создать поисковый PDF из изображения с помощью Java OCR
tags:
- OCR
- Java
- PDF
title: Создать PDF с возможностью поиска из изображения с помощью Java OCR
url: /ru/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения с помощью Java OCR

Когда‑то вам нужно **создать поисковый PDF** из отсканированного изображения, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда впервые работают с PDF‑файлами, основанными на изображениях. К счастью, с Aspose OCR for Java вы можете **преобразовать изображение в PDF**, сделать текст выделяемым и даже добавить исправление орфографии для более профессионального результата.

В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий, как **использовать OCR GPU**, когда он доступен, как **эффективно обрабатывать изображение OCR** и почему включение исправления орфографии важно для последующего поиска. К концу вы получите способ в один клик генерировать поисковый PDF, который можно распространять пользователям или архивировать для соответствия требованиям.

> **Совет:** Если вы работаете на машине без GPU, код автоматически переходит на CPU, так что переписывать ничего не нужно.

---

## Что понадобится

- **Java 8+** (код компилируется на JDK 8 и новее)
- Библиотека **Aspose OCR for Java** (скачайте последнюю JAR‑ку с сайта Aspose)
- **Входное изображение** (JPEG, PNG, TIFF и т.д.), которое вы хотите превратить в поисковый PDF
- (Опционально) **GPU** с поддержкой CUDA, если вам нужна максимальная скорость распознавания

Никаких дополнительных фреймворков, без Maven/Gradle‑магии — только один JAR в classpath, и всё готово к работе.

---

## Шаг 1: Инициализация OCR‑движка — сердце процесса  

Сначала создаём экземпляр `OcrEngine` и указываем ему исходный файл. Этот объект — рабочая лошадка, которая считывает изображение, запускает нейронную сеть и возвращает нам текст.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Почему это важно:* Инициализировать движок один раз и переиспользовать его позволяет избежать накладных расходов на повторную загрузку нативных библиотек — небольшое, но суммирующееся преимущество при пакетной обработке десятков файлов.

---

## Шаг 2: Выбор устройства обработки — использовать OCR GPU, если возможно  

Если у вашей рабочей станции есть совместимый GPU, вы можете попросить Aspose выполнять тяжёлую работу на нём. В противном случае движок автоматически переключится на CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*В чём выгода?* Ускорение за счёт GPU может сэкономить секунды на каждой странице, особенно для сканов высокого разрешения. Резервный переход на CPU гарантирует, что один и тот же код будет работать везде, поэтому мы рекомендуем **use OCR GPU** как настройку по умолчанию.

---

## Шаг 3: Ускоряем сканирование — задействуем все ядра CPU  

Даже когда GPU занят, предобработку можно выполнять параллельно. Установка количества потоков равным числу доступных процессоров даёт движку возможность обрабатывать несколько частей одновременно.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Примечание:* На ноутбуке с 4‑ядерным процессором будет запущено четыре потока; на рабочей станции с 16 ядрами вы получите полную выгоду. Учтите, что больше потоков — больше потребления памяти.

---

## Шаг 4: Очистка изображения — фильтры предобработки  

Размытие или шум в скане приводят к мусорному тексту. Добавление парочки встроенных фильтров существенно повышает точность.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Зачем эти фильтры?* `DeskewFilter` исправляет наклон, который часто появляется, когда документ подаётся в сканер под углом. `NoiseRemovalFilter` удаляет случайные пиксели, которые иначе могли бы быть приняты за символы. По сути, это как дать OCR‑движку чистый лист бумаги для чтения.

---

## Шаг 5: Включаем интеллектуальные функции — исправление орфографии и автоопределение языка  

Если вы работаете с многоязычными документами или просто хотите уменьшить количество опечаток, включите встроенный проверщик орфографии и позвольте движку определить язык автоматически.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Когда это полезно?* Представьте, что ваш скан содержит как английские, так и испанские разделы. Функция автоопределения переключает словари «на лету», а исправление орфографии устраняет ошибочно распознанные символы, например «0» вместо «O». Этот шаг необходим для создания **поискового PDF**, который действительно возвращает корректные результаты.

---

## Шаг 6: Сохранение результата — преобразование изображения в PDF и создание поискового слоя  

Наконец, просим движок записать PDF, где оригинальное изображение находится за невидимым текстовым слоем. Это классический **convert image to PDF**‑workflow, но теперь PDF становится поисковым.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Полученный файл (`output-searchable.pdf`) открывается в любом PDF‑просмотрщике; вы сможете выделять, копировать и искать текст так же, как в нативном PDF. Дополнительные инструменты не требуются.

---

## Полный рабочий пример — копировать‑и‑запускать  

Ниже представлен весь код программы, готовый к компиляции. Замените `YOUR_DIRECTORY` на путь к папке, где находится `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Ожидаемый вывод:** При запуске программы в консоли появится строка *«Searchable PDF generated successfully.»* Открыв `output-searchable.pdf` в Adobe Reader, вы сможете ввести слово из оригинального изображения в поле поиска и мгновенно перейти к его расположению.

---

## Часто задаваемые вопросы и особые случаи  

- **Что если GPU не обнаружен?**  
  Вызов `setDeviceType(OcrDeviceType.GPU)` не бросает исключения; он лишь пытается использовать GPU в первую очередь. При неудаче движок тихо переходит на CPU.

- **Можно ли обрабатывать несколько изображений за один запуск?**  
  Да. Оберните код в цикл, меняйте имя файла на каждой итерации и переиспользуйте один экземпляр `OcrEngine`, чтобы снизить расход памяти.

- **Мой PDF огромный — как его уменьшить?**  
  После OCR можно воспользоваться API оптимизации PDF от Aspose или просто уменьшить разрешение исходного изображения перед передачей в движок (`ImageStream.fromFile(...).setResolution(150)` для 150 DPI).

- **Нужно сохранить оригинальное разрешение изображения для юридических целей.**  
  Формат `PDF_SEARCHABLE` сохраняет исходный битмап без изменений; невидимый текстовый слой добавляется сверху, не ухудшая визуальное качество.

---

## Визуальное резюме  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")

*Alt text:* *пример создания поискового PDF — OCR‑движок Java преобразует отсканированный JPG в поисковый PDF.*

---

## Заключение  

Теперь у вас есть **полное сквозное решение** для превращения любого изображения в **поисковый PDF** с помощью Aspose OCR for Java. Путём **конвертации изображения в PDF**, **включения исправления орфографии** и **использования OCR GPU**, когда это возможно, вы получаете быстрые, точные и поисковые результаты, работающие на всех платформах.

Что дальше? Попробуйте поэкспериментировать с:

- **Различными форматами вывода** (`PDF`, `DOCX`, `HTML`), чтобы увидеть, как ведёт себя текстовый слой.
- **Пользовательскими словарями**, если вы обрабатываете отраслевой жаргон.
- **Пакетной обработкой** для автоматической работы с тысячами сканов.

Не стесняйтесь менять количество потоков, заменять фильтры или подключать собственный конвейер предобработки. Основной шаблон остаётся тем же: загрузить → предобработать → настроить → OCR → сохранить.

Счастливого кодинга, и пусть ваши PDF‑файлы всегда остаются поисковыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}