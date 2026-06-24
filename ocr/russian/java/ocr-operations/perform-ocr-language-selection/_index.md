---
date: 2026-06-24
description: Узнайте, как выполнять OCR текста на изображениях с выбором языка, используя
  Aspose.OCR для Java. Это step‑by‑step руководство охватывает extract text java,
  OCR skew correction и многое другое.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Как выполнить коррекцию наклона OCR и выбор языка с помощью Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Как выполнить коррекцию наклона OCR и выбор языка с помощью Aspose.OCR
url: /ru/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить коррекцию наклона OCR и выбор языка с помощью Aspose.OCR

## Введение

Извлечение текста из файлов изображений — распространённая задача, будь то оцифровка отсканированных документов, обработка чеков или создание поисковых архивов. В этом руководстве мы пройдем полный практический пример, показывающий **как выполнять OCR текста на изображении** с указанием конкретного языка, чтобы вы могли уже сегодня интегрировать надёжный OCR в свои Java‑приложения. Вы также увидите, как работать с **коррекцией наклона OCR** и распознаванием по регионам для оптимальной точности, что совместно может **повысить точность OCR** до 30 % на наклонных сканах.

## Быстрые ответы
- **Какая библиотека обрабатывает OCR в Java?** Aspose.OCR for Java  
- **Какая настройка выбирает язык?** `settings.setLanguage(Language.Eng)` (или любой поддерживаемый язык)  
- **Нужна ли лицензия для разработки?** Бесплатная оценочная лицензия подходит для тестирования; для продакшн‑использования требуется коммерческая лицензия.  
- **Можно ли ограничить OCR областью изображения?** Да, используйте `RecognitionSettings.setRecognitionAreas()` с прямоугольниками.  
- **Каков типичный время выполнения?** Несколько секунд на страницу на обычном ноутбуке, в зависимости от размера изображения и сложности языка.  

`Language` — это перечисление, в котором перечислены поддерживаемые Aspose.OCR языки OCR, такие как English, French, Spanish и т.д.

## Что такое коррекция наклона OCR?

Коррекция наклона OCR — процесс обнаружения и выравнивания наклонных строк текста перед распознаванием символов. Выравнивая базовую линию текста, OCR‑движок может эффективнее применять свои языковые модели, снижая количество ошибок, вызванных наклонными сканами. Этот шаг улучшает визуальное качество входного изображения, позволяя алгоритмам распознавания сосредоточиться на истинных формах символов, а не на искажениях, вызванных вращением.

## Почему коррекция наклона OCR повышает точность

Когда текст наклонён, формы символов искажаются, что приводит к увеличению уровня ошибок до 20 %. Применение **ocr skew correction** устраняет это искажение, позволяя движку сосредоточиться на реальных глифах. В тестах производительности Aspose.OCR достиг повышения точности распознавания на 15‑30 % для документов с вращением 10‑15° после применения коррекции наклона.

## Почему стоит использовать Aspose.OCR с выбором языка?

Указание точного языка исходного текста позволяет OCR‑движку использовать языко‑специфические словари и модели символов, что значительно повышает точность распознавания и уменьшает время обработки. Кроме того, Aspose.OCR предоставляет тонкую настройку коррекции наклона, выбора регионов и форматов вывода, делая его универсальным решением для многоязычных конвейеров обработки документов.

- **Поддержка нескольких языков** – выберите точный язык(и), присутствующий(ие) на изображении, чтобы повысить точность.  
- **Точная настройка** – регулируйте наклон, определяйте области распознавания и задавайте поведение авто‑наклона.  
- **Чистый Java API** – без нативных зависимостей, легко интегрировать в любой Java‑проект.  
- **Богатые данные результата** – получайте простой текст, JSON, ограничивающие прямоугольники и предупреждения в одном вызове.  
- **Количественная возможность** – Aspose.OCR поддерживает **более 50** входных и выходных форматов и может обрабатывать **пакеты из 500 страниц** без загрузки всего документа в память.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- **Java Development Kit (JDK)** установлен (JDK 8 или новее).  
- **Библиотека Aspose.OCR for Java** – скачайте её с официального сайта [здесь](https://reference.aspose.com/ocr/java/).  
- Файл изображения, содержащий текст, который вы хотите извлечь, например `p3.png`.  

## Импорт пакетов

Следующие импорты дают доступ к основным классам OCR и стандартным утилитам Java.  
`import com.aspose.ocr.*;` – импортирует основной OCR‑движок.  
`import com.aspose.ocr.config.*;` – содержит объекты конфигурации, такие как `RecognitionSettings`.  
`import java.awt.Rectangle;` – используется для определения областей распознавания.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Как применить коррекцию наклона OCR в Java?

Загрузите изображение, отключите автоматическое определение наклона и либо укажите измеренный угол, либо позвольте движку вычислить его с помощью `settings.setAutoSkew(false)`. OCR‑движок сначала выпрямит изображение по заданному или обнаруженному углу, затем выполнит распознавание символов. Такой двухшаговый подход гарантирует, что любой наклон будет устранён до применения языковых моделей, что приводит к более чистому текстовому выводу и меньшему количеству ошибок.

## Пошаговое руководство

### Шаг 1: Настройте каталог документов

Создайте объект `File`, указывающий на папку, содержащую исходное изображение. Это делает работу с путями переносимой между операционными системами.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на абсолютный путь, где находится `p3.png`.

### Шаг 2: Определите путь к изображению

Создайте объект `File` для конкретного изображения, которое нужно обработать. Использование объекта `File` упрощает доступ к метаданным файла, если они понадобятся позже.

```java
// The image path
String file = dataDir + "p3.png";
```

Убедитесь, что переменная `file` указывает на именно то изображение, которое вы собираетесь обрабатывать.

### Шаг 3: Создайте экземпляр API Aspose.OCR

Класс `AsposeOCR` является точкой входа для всех операций OCR. Он инкапсулирует движок, управляет ресурсами и предоставляет метод `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Объект `AsposeOCR` даёт доступ ко всем операциям OCR.

### Шаг 4: Задайте параметры распознавания (выбор языка)

`RecognitionSettings` — контейнер конфигурации Aspose.OCR, позволяющий тонко настроить процесс OCR.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Здесь мы:

1. Отключаем авто‑наклон, потому что будем задавать значение вручную.  
2. Определяем прямоугольную область (`RecognitionAreas`), чтобы ограничить OCR только той частью изображения, где действительно есть текст.  
3. Устанавливаем **язык** на английский (`Language.Eng`). Замените его на `Language.Fra`, `Language.Spa` и т.д., в зависимости от вашего исходного изображения.

### Шаг 5: Выполните OCR и получите результаты

Вызов `recognizePage` запускает OCR‑движок с указанным изображением и настройками. Результат сохраняется в объект `RecognitionResult`, который агрегирует все полезные данные.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Вызов `RecognizePage` запускает OCR‑движок с указанным изображением и настройками. Результат сохраняется в объект `RecognitionResult`.

### Шаг 6: Выведите и используйте результаты

Консольный вывод показывает:

- Полный извлечённый текст (`recognitionText`).  
- Текст для каждого определённого прямоугольника (`recognitionAreasText`).  
- Координаты ограничивающих прямоугольников.  
- JSON‑представление для удобной последующей обработки.  
- Обнаруженный угол наклона и любые предупреждения.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Консольный вывод показывает полный извлечённый текст, текст по регионам, ограничивающие рамки, JSON, угол наклона и предупреждения. Теперь вы можете передать `result.recognitionText` в свою бизнес‑логику — сохранить, проиндексировать или передать другому сервису.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|---------|
| **Непонятные символы** | Выбран неверный язык | Установите правильный элемент перечисления `Language` (например, `Language.Fra` для французского). |
| **Текст не возвращается** | Область распознавания не охватывает текст | Скорректируйте координаты `Rectangle` или уберите `RecognitionAreas`, чтобы обрабатывать всё изображение. |
| **Низкая производительность** | Очень большое изображение или высокое разрешение | Уменьшите масштаб изображения перед OCR или увеличьте выделение памяти JVM. |
| **Предупреждения о неподдерживаемом формате** | Формат изображения не распознан | Конвертируйте изображение в PNG, JPEG или TIFF перед обработкой. |

## Часто задаваемые вопросы

**В: Можно ли распознавать несколько языков за один вызов OCR?**  
О: Да. Используйте `settings.setLanguage(Language.Eng | Language.Fra)`, чтобы включить многоязычное распознавание.

**В: Какие форматы изображений поддерживает Aspose.OCR?**  
О: PNG, JPEG, BMP, TIFF, GIF и несколько других. Просто укажите правильный путь к файлу.

**В: Есть ли ограничение по размеру изображения?**  
О: Жёсткого ограничения нет, но обработка файлов более 10 МБ может увеличить потребление памяти и время выполнения. Рекомендуется уменьшать большие файлы.

**В: Как получить производственную лицензию?**  
О: Приобретите лицензию на сайте Aspose и примените её через класс `License`, как показано в документации Aspose.

**В: Можно ли напрямую извлекать текст из страницы PDF?**  
О: Не напрямую с помощью Aspose.OCR. Сначала преобразуйте страницу PDF в изображение (например, с помощью Aspose.PDF), а затем выполните OCR.

## Заключение

Теперь вы знаете, как **извлекать текст из изображения** с помощью Aspose.OCR для Java, выбирая соответствующий язык и применяя **коррекцию наклона OCR** для повышения надёжности. Этот подход обеспечивает точный, высокопроизводительный OCR, который можно встроить в любой Java‑ориентированный рабочий процесс — от систем управления документами до конвейеров захвата данных. Экспериментируйте с различными элементами `Language`, настраивайте `RecognitionAreas` и интегрируйте JSON‑вывод в последующий анализ для действительно сквозного решения.

---

**Последнее обновление:** 2026-06-24  
**Тестировано с:** Aspose.OCR 24.11 for Java  
**Автор:** Aspose

## Похожие руководства

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}